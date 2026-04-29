---
title: "Index-file audit pattern (counts + entries vs. directory)"
type: pattern
project: "global"
tags: [topic/documentation, tool/obsidian]
created: 2026-04-29
updated: 2026-04-29
status: active
---

When auditing folder index files (e.g., Obsidian per-folder `index.md` files that link to local PDFs), check:

1. **Claimed counts vs. actual.** Index says "Files: N PDFs"? Run `ls | wc -l` to verify.
2. **Entry lists vs. actual filenames.** Diff the index's wikilinks against `ls` output.
3. **Section headings vs. content.** Section title implies a categorisation; verify entries within actually fit it. (E.g., a "decks 1 & 2" section that contains entries describing different deck counts.)
4. **Abbreviation expansions.** If the heading expands an abbreviation appearing in filenames, verify the expansion against canonical sources. Bug found this way: "P of S" wrongly read as "port of starboard" instead of "Plug of Ship".

## Wikilink style trade-off

- Bare `[[Filename]]` — concise but assumes vault-wide unique basenames.
- Fully-qualified `[[Folder/Filename.pdf|Display]]` — robust but verbose.

For collections with stable, unique filenames, bare links are fine. For vaults that may contain duplicate basenames in other folders, prefer qualified.

Used in [[2026-04-29-clement-todo-cleanup]].
