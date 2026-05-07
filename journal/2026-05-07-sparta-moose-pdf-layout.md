---
title: "Sparta Moose schedule one-page PDF via pandoc + typst"
type: journal
project: "philoserf/notes"
tags: [tool/pandoc, tool/typst, topic/pdf]
created: 2026-05-07
updated: 2026-05-07
status: active
---

## Task

Cleaned up `Inbox/Sparta Moose May 2026 Schedule.md` (verbose bullets → unified day-keyed tables for recurring schedule, special events, and social quarters hours), then generated a one-page PDF via `pandoc --pdf-engine=typst` with a custom typst template.

## Outcome

One-page PDF with table-caption-as-title pattern, asymmetric row inset for vertical breathing room, and left-aligned tables. User embedded the resulting PDF in the source markdown via `![[Sparta Moose May 2026 Schedule.pdf]]`.

## Lessons

- `mdls` page counts are unreliable on macOS — see [[2026-05-07-macos-pdf-page-count-mdls-stale]]. Reported "1 page" multiple times when `pdfinfo` showed 2. Caused at least one outright wrong claim to the user.
- Pandoc + typst figure overrides are documented in [[2026-05-07-pandoc-typst-figure-overrides]].
- The user said "we have vertical space" — meaning grow the gaps (row padding, figure spacing), not the font. I bumped font instead and had to be redirected explicitly. **Lesson: when a user says "vertical space," reach for `inset.y` and figure `spacing`, not `text.size`.**
- Iterating across multiple typst variables (font, margin, inset, figure-spacing) per round lost the ability to attribute outcomes. Move one lever at a time and verify each.

## Workflow snapshot

```bash
pandoc input.md -o out.pdf --pdf-engine=typst --template=template.typ
pdfinfo out.pdf | grep Pages
```

Verifying with `pdfinfo` after every build is non-negotiable when the goal is a specific page count.
