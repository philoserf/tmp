---
title: "Changelog.md is plugin-managed (not collateral damage)"
type: context
project: "philoserf/notes"
tags: [tool/obsidian, topic/gotcha, topic/git]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Gotcha

`Changelog.md` at the vault root is auto-maintained by an Obsidian plugin. Every time a note is edited, the plugin appends a timestamped wikilink and reorders existing lines the next time Obsidian indexes the change.

When `git status` shows `modified: Changelog.md` after a session you didn't expect to touch, **this is the plugin, not collateral damage** from your edits.

## How to apply

- Don't try to revert `Changelog.md` — the plugin will rewrite it on the next index.
- Don't include it in atomic-commit organization as if it were intentional content; it rides along with whatever notes were edited.
- If you stage notes individually and commit, just stage `Changelog.md` alongside — its diff is automatic and expected.
- If `Changelog.md` is the _only_ modified file, the plugin re-indexed something but no edits were made; no commit is needed.
