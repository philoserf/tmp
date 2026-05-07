---
title: "Vault audit, link cleanup, and INDEX.md creation"
type: journal
project: "philoserf/tmp"
tags: [topic/documentation, tool/obsidian]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Session arc

Mid-session task in the vault itself. User asked to assess the vault and decide what to do with it next. I surveyed the contents (47 entries, all `status: active`) and proposed three follow-ups: (1) audit for staleness/orphans, (2) build an index, (3) consolidate overlapping patterns. User said start the list.

## What was done

**Audit (task 1)**

- All entries `status: active`; no genuinely stale or superseded notes found.
- The two `[[Filename]]` and `[[Folder/Filename.pdf|Display]]` "links" in `2026-04-29-index-file-audit` are example syntax inside descriptive prose, not broken.
- Found and fixed link asymmetries / cluster gaps:
  - `obsidian-metadator-techdebt-sweep` → backlink to `obsidian-metadator-architecture` + outbound to `strict-positive-int-parser` and `bun-test-mock-module-gotchas`.
  - `obsidian-metadator-2-2-0-release` → backlinks to architecture + techdebt-sweep.
  - `notes-vault-research-save-pipeline` → backlink to `last30days-research-save-cycles`.
  - `git-stash-pop-cross-branch` ↔ `git-stash-unmerged-paths` — bidirectional.
  - `obsidian-first-vault-design` ↔ `related-frontmatter-field-removed` — bidirectional.
  - `frontmatter-field-ownership` → `obsidian-first-vault-design` + `status-vocabulary-imperative`; promoted a prose mention of "the related-field-removed decision entry" to a real wikilink.
  - `status-vocabulary-imperative` → `frontmatter-field-ownership`.
- All edited entries had `updated:` bumped to 2026-05-06.

**Index (task 2)**

- Created `INDEX.md` at vault root, grouped by **project** (5 sections: philoserf/notes, philoserf/obsidian-metadator, philoserf/world-builder, Traveller/Clement, philoserf/tmp meta) then by **topic cluster** (7 sections: workflow discipline, trust-but-verify, git/PR workflow, tooling gotchas, Bun/TypeScript, Markdown rendering / release tooling, code review, documentation/canon).
- Index includes claim-vs-actual counts per [[2026-04-29-index-file-audit]] pattern.
- Wired into [[CLAUDE]] as discovery point #1, plus a "after writing, also add to INDEX" note in the When-to-Write section.

**Consolidation (task 3) — declined**

- Reviewed the suspected-overlap clusters (trust-but-verify trio; workflow discipline quartet; canon trio).
- Concluded the patterns are correctly factored. Each has a _concrete trigger_ that tells future-you when to apply it. Merging them would yield abstract patterns that lose specificity.
- 23 patterns is fine for a vault this active. The navigability benefit consolidation would have provided is delivered by the audit (links) and the index (topic groupings) instead.

## Lesson worth preserving

**Quantity ≠ overlap.** The initial recommendation to "consider consolidating" was based on counting (23 patterns) and titular family-resemblance (three "verify-..." entries). When I actually read each pattern, they were each about a specific situation, not abstract overlap. The trigger-specificity of a pattern is what makes it usable; merging into a meta-principle erases the trigger.

**Heuristic:** before consolidating patterns, read them. If two patterns describe the same trigger, merge. If they describe different triggers that share a meta-principle, leave separate and cross-link.

## Outcomes

- Vault link graph is denser and more discoverable.
- INDEX.md is the new front door for navigation.
- 8 entries had `updated:` bumped; 1 new index file; 1 new journal (this entry); CLAUDE.md updated.

## Notes for next session

- INDEX.md is hand-maintained. After writing a new vault entry, add it to INDEX.md and bump the count line.
- The `docs/superpowers/` directory still holds the original spec + plan from the bootstrap. Left in place; not folded into the type-folder structure.
- `handoffs/` is still empty — that's fine, no incomplete work was found.
