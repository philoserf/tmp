---
title: "Surface structural notes prominently in /editor output"
type: pattern
project: "philoserf/notes"
tags: [topic/editing, tool/claude-code]
created: 2026-05-07
updated: 2026-05-07
status: active
---

## Rule

When the `/editor` skill produces structural recommendations (cut paragraphs, reorganize, merge, trim to length), surface them prominently — not buried after the line-edit flag block. The user wants to act on them, not hunt for them.

## Why

In a 2026-05-07 session, the user was reviewing 10 edit passes back-to-back. After task #9, they noted: "Hit those structural elements in 10. I almost missed them in the other context." The structural notes for `Strong Opinions, Weakly Held` recommended cutting three paragraphs (4, 8, 9) — a load-bearing change that took the piece from 9 paragraphs to 6 (in published-essay range). That recommendation was the most important output of the edit, but it sat below the line-by-line bracket-flag block.

## How to Apply

When `/editor` output includes structural recommendations:

- **If structural cuts are the load-bearing fix** (paragraphs to remove, sections to merge, length out of published range), lead with them. Section heading like `**Structural notes (the load-bearing issue):**` calls them out.
- **If structural notes are minor** (one observation, optional), leave them where they fit — but ensure they're visually separated from line edits.
- **Always check published-corpus length**: in philoserf/notes, the published-essay range is 3–7 paragraphs. Drafts longer than 7 are trim candidates worth flagging.

## Skill-level Improvement Candidate

Consider updating the `/editor` skill output template to require an explicit "Structural" section above the per-paragraph fixes when cuts are recommended. Current template lets structural notes drift to the bottom.

## Related

- [[2026-05-07-inbox-triage-edit-pass]]
