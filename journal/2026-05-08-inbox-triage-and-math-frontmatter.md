---
title: "Inbox triage, status assignment, math frontmatter audit"
type: journal
project: "philoserf/notes"
tags: [tool/obsidian-cli, topic/frontmatter]
created: 2026-05-08
updated: 2026-05-08
status: active
---

## Session summary

- Triaged 30 oldest Inbox notes into Drafts/ and Reference/ across three batches of 10.
- Assigned `status` (draft | develop | review) to 29 Drafts notes that lacked one. Result: 22 review, 5 develop, 2 draft.
- Audited Drafts and Published for notes using LaTeX math notation. Added `math: true` to 5 Drafts notes; verified all 3 Published math notes were already correct.
- Discovered the `type=` parameter on `obsidian property:set` and updated the corresponding gotcha memory.

## Patterns observed

- AI-generated essay-shape notes (3-7 paragraphs, third-person, exploratory) routinely belong in Drafts/ rather than Reference/, even without first-person voice.
- Most polished essay-shape Drafts arrive at `review` readiness on first pass; the formulaic three-paragraph thesis/counter/synthesis shape is `develop`.
- Math-bearing notes are rare (5 Drafts, 3 Published total).

## Lesson

When a CLI tool's output shape is wrong (e.g., `math: "true"` instead of `math: true`), check `<tool> help <subcommand>` for type/format flags before falling back to post-edit. See [[2026-05-08-obsidian-cli-property-set-types]].
