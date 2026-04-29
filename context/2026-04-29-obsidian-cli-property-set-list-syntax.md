---
title: "Obsidian CLI property:set requires JSON array for lists"
type: context
project: "philoserf/notes"
tags: [tool/obsidian-cli, topic/gotcha]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Gotcha

`obsidian vault=notes property:set name="tags" value="[a, b]"` writes `tags: "[a, b]"` — a quoted string, not a YAML list. The vault tag index sees this as one literal tag string and breaks downstream queries.

## Fix

Quote each element as JSON and pass `type=list`:

```bash
# Wrong — writes a quoted string
obsidian vault=notes property:set name="tags" value="[a, b]"

# Right — writes a proper YAML list
obsidian vault=notes property:set name="tags" value='["a", "b"]' type=list
```

## Why

The CLI treats `[a, b]` as a raw string but parses `["a", "b"]` as a JSON array, then expands it into multi-line YAML list items. This trap broke 830+ files during the April 2026 tag consolidation before being identified.

## How to apply

Always use JSON-quoted elements with `type=list` when setting list properties via the CLI. The vault's `.scripts/` tag scripts were updated to use this format — match that style for any new tag-manipulation tooling.
