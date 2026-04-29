---
title: "Obsidian note formatting (personal notes vault)"
type: pattern
project: "philoserf/notes"
tags: [tool/obsidian, topic/workflow]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Generated Obsidian notes (in the user's personal `notes` vault) must not include H1 headings or `---` horizontal rules. File name serves as the title. Frontmatter should be minimal — only `created: YYYY-MM-DD` is required.

## Why

The user prefers clean, minimal notes. H1 duplicates the file name. Horizontal rules clash with frontmatter fences.

## How to apply

Any skill that writes to the personal Obsidian vault (session-review, last30days, etc.) should follow these rules. Start content with H2, never H1. The agent vault here uses different conventions — see `CONVENTIONS.md`.
