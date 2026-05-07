---
title: "Habit-words to flag in philoserf/notes drafts"
type: context
project: "philoserf/notes"
tags: [topic/editing]
created: 2026-05-07
updated: 2026-05-07
status: active
---

## Pattern

Across the philoserf/notes `Drafts/` corpus (301 files), these filler/habit words recur as soft prose. Counts as of 2026-05-07:

| Word           | Total | Files |
| -------------- | ----: | ----: |
| fundamental    |   176 |    95 |
| actually       |    93 |    68 |
| simultaneously |    68 |    57 |
| genuinely      |    60 |    52 |
| simply         |    59 |    53 |
| fully          |    55 |    44 |
| ultimately     |    28 |    25 |
| truly          |    24 |    19 |
| necessarily    |    19 |    17 |

## When Editing

Flag aggressively as `[filler]` in `/editor` Edit Mode. Most uses are intensifier-creep that weakens the surrounding claim:

- "captures a fundamental tension" → "captures a tension"
- "operates on two levels simultaneously" → "operates on two levels"
- "genuinely interesting" → "interesting"
- "simply because" → "because"

Exceptions where the word earns its place:

- Mathematical/physics contexts ("fundamental theorem")
- Closing-line emphasis ("exactly the right question")
- Where the word does real epistemic or temporal work

## Search Pattern

```sh
grep -nE '\b(genuinely|simultaneously|fully|simply|fundamental|actually|truly|ultimately|necessarily)\b' Drafts/*.md
```

## Related

- philoserf/notes#58 — open issue tracking the corpus-wide cleanup pass
- [[2026-05-07-inbox-triage-edit-pass]]
