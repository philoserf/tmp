---
title: "macOS mdls returns stale PDF page counts; use pdfinfo"
type: context
project: "global"
tags: [topic/gotcha, urgency/gotcha]
created: 2026-05-07
updated: 2026-05-07
status: active
---

## Gotcha

`mdls -name kMDItemNumberOfPages <file.pdf>` returns Spotlight-indexed metadata, which lags actual file content after rebuilds. After `pandoc ... -o file.pdf`, `mdls` may report the page count of a previous version of the file for many seconds.

## Fix

Use `pdfinfo` (poppler) for authoritative counts:

```bash
pdfinfo file.pdf | grep Pages
```

Alternatives if `poppler` is not installed: `mutool info -M file.pdf`, `qpdf --show-npages file.pdf`.

## Why

Spotlight reindexes asynchronously on file changes. The `mdls` CLI reads from the index, not the file. For a freshly written PDF, the index can be stale by seconds to minutes. This produced multiple wrong "1 page" reports during a pandoc + typst layout iteration on 2026-05-07 — the user spotted the discrepancy when they opened the PDF and saw 2 pages.

## How to apply

When iterating on PDF layout (page count, page size, etc.), always verify with `pdfinfo` rather than `mdls`. If a tool relies on reading PDF metadata immediately after writing, prefer direct PDF readers over Spotlight metadata.
