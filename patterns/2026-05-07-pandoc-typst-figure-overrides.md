---
title: "Pandoc + Typst custom template patterns for table layout"
type: pattern
project: "global"
tags: [tool/pandoc, tool/typst, topic/pdf]
created: 2026-05-07
updated: 2026-05-07
status: active
---

## When

Generating single-page PDFs from markdown with pandoc and the typst engine, where the default output centers tables, places captions below tables, and emits a heavy title block.

## Pattern

Pandoc emits each table as `#figure(align(center)[#table(...)], caption: ..., kind: table)`. Show rules at the figure level override the inner `align(center)` and the default caption position.

```typst
#set page(paper: "us-letter", margin: 0.5in)
#set text(size: 10pt)
#set table(inset: (x: 5pt, y: 5pt), stroke: 0.4pt + gray, align: left)

#show figure.where(kind: table): set figure.caption(position: top)
#show figure.caption: it => align(left)[
  #text(size: 13pt, weight: "bold", it.body)
]
#show figure: it => block(spacing: 0.9em)[
  #align(left, it)
]

$body$
```

In the markdown, replace `## Section Heading` with a pandoc table caption to make the section title visually merge with the table:

```markdown
| Day | Hours     |
| --- | --------- |
| Sun | 10am–10pm |

: Social Quarters Hours
```

## Why

- `align(center)` wrapping each table is hard-coded by pandoc; only a figure-level override removes it.
- Default caption position is `bottom`; for table-titles, set to `top`.
- `inset: (x: pt, y: pt)` lets you grow vertical row height without widening tables.
- Avoid `breakable: false` on figures unless you genuinely cannot allow page splits — it pushes too-tall figures to a fresh page, often producing more page count than expected.

## Gotchas

- Typst paper sizes use country prefixes: `us-letter`, not `letter`. `letter` produces a runtime error.
- Frontmatter `title:` only renders if your custom template references `$title$`. A template that omits it silently suppresses the pandoc title block — useful for compact layouts.
- `mdls -name kMDItemNumberOfPages` lags after rebuilds; verify page counts with `pdfinfo`. See [[2026-05-07-macos-pdf-page-count-mdls-stale]].

## How to apply

For any markdown-to-PDF task with multiple tables that need to fit a page budget, start from this template, tune row inset (`y`) and figure spacing (`spacing`) for breathing room, and use captions instead of headings to let tables own their titles.
