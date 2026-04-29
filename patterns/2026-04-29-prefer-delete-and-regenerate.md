---
title: "Prefer delete-and-regenerate over scripted renames"
type: pattern
project: "philoserf/notes"
tags: [tool/obsidian, topic/migration]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Pattern

When migrating frontmatter fields that a tool (Obsidian Linter, plugin) manages automatically, **remove the old field and let the tool regenerate the new one** — don't script a rename-in-place.

## Rationale

Mark simplified a 5-step frontmatter migration to 3 steps by noting "Linter will create `created` for us." Scripting the rename would have been more complex and less reliable than letting the authoritative tool handle it.

## How to apply

Before writing migration scripts:

1. Check what Obsidian Linter or other plugins will handle automatically.
2. Identify which fields the tool owns (auto-managed vs manual).
3. Script only what the tools can't do.
4. For tool-owned fields: delete the old field, let the tool repopulate on next index.
