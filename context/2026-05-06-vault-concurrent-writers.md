---
title: "Agent memory vault has concurrent writers — expect rebase divergence"
type: context
project: "philoserf/tmp"
tags: [tool/git, topic/workflow, urgency/gotcha]
created: 2026-05-06
updated: 2026-05-06
status: active
---

This vault (`~/source/philoserf/tmp`) is written by multiple agent sessions concurrently. Within hours of one session pushing, another session may push entries to non-conflicting paths.

## Observed

On 2026-05-06, two sessions worked the vault within the same evening:

- Audit + INDEX session (this one) — modified existing entries + added INDEX.md.
- "Multi-horizon journal backfill" session — added 4 new entries in `context/`, `journal/`, `patterns/`.

The audit session's first `git push` was rejected because remote had advanced. Recovery: `git pull --rebase` (clean — no path conflicts), update INDEX.md to reflect the 4 new entries, commit, push.

## How to apply

- Run `git fetch` early in any vault session to surface upstream activity before doing significant local work.
- When `git push` is rejected, **prefer `git pull --rebase`** over merge. New entries from rebased commits are usually in non-conflicting paths.
- After the rebase, **update INDEX.md** to reflect any new entries the rebase brought in (counts + project section + topic-cluster section). The vault-audit skill at `.claude/skills/vault-audit/SKILL.md` codifies the full move.

## Why this matters

Stale INDEX.md is a quiet failure: the index claims one count, the directory has another, and future agents don't notice until the next audit. Bumping the count after a rebase is a 30-second move that prevents weeks of drift.
