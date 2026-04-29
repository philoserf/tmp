---
title: "Copilot self-review checklist for first-cut PRs"
type: pattern
project: "global"
tags: [topic/debugging, tool/copilot, urgency/gotcha]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Recurring failure pattern observed across 12 PRs in the obsidian-metadator session: I tend to ship "Copilot-bait" — first cuts that miss the same categories of edge cases Copilot reliably catches. Use this checklist before opening a PR to surface them yourself.

## The checklist

When **changing a return type** (e.g., adding `null` cases, switching to a discriminated union):

- What's the next action a caller takes after each branch?
- Does the loader/saver/caller's behavior preserve the prior version's invariants on every branch?
- Concrete scenario from this session: `migrateSettings` returning `null` on a future-version load → loader fell through to defaults → next save would clobber the forward-version file. Fix: discriminated `MigrationResult` so the caller can distinguish "missing" from "future".

When **using a platform API** (`crypto`, `fetch`, browser globals):

- Is this called _unconditionally_ on the request path, or only behind a feature flag?
- Does the platform actually expose this on every supported deployment target (mobile WebViews, older Electron versions)?
- Concrete scenario: `crypto.randomUUID()` called on every metadata generation, not only when debug logging was on. Older mobile WebViews would have thrown. Fix: feature-detect with fallback chain.

When **refactoring to structured/typed output** (replacing prose logs, replacing raw errors with custom classes):

- Did the previous version emit any signal (stack trace, error name, original exception) that the new version drops?
- If yes, capture those into the new structure.
- Concrete scenario: replaced `console.error("...", error)` with `logError({ errorMessage })`. Lost the stack trace. Fix: add `errorName` + `errorStack` fields.

When **renaming or moving code**:

- Did any documentation reference the old path?
- Doc inaccuracies show up as "wait, where did X go?" in the next PR. Cheap to fix as part of the PR that does the rename.
- Concrete scenario: moved `MIGRATIONS` from `main.ts` to `settingsMigrate.ts`. CLAUDE.md still said "in `main.ts`". Caught later, costing an extra PR cycle.

When **introducing a permissive parser** (`parseInt`, `parseFloat`, `Number`):

- Does it accept inputs the validation message promises to reject?
- `Number.parseInt("1.5", 10) === 1` — silent truncation is a bug if the UI says "must be a positive integer".
- Concrete scenario: settings UI accepted `"1.5"` and saved `1`. Existing test even encoded the bug as expected behavior.

## How to apply

Spend 60 seconds running through the checklist before pushing. If any item triggers, either fix it in the same PR or note it in the PR description as deferred. Catching even one of these per PR avoids a full review-fix-merge round trip.
