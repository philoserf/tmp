---
title: "Things MCP get_logbook filters by creation date, not completion date"
type: context
project: "philoserf/notes"
tags: [tool/things-mcp, topic/gotcha]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Gotcha

`mcp__things__get_logbook` is unreliable for tracking completed tasks. The underlying `things.last()` call filters by **creation date**, not completion date. Tasks completed today but created more than `period` days ago silently disappear from the result.

The bug is in the `things-mcp` package and cannot be fixed without patching the library.

## Status in this project

The `daily-review` skill in `philoserf/notes` had logbook checks removed entirely after this was identified. Do not add them back.

## How to apply

- Do not use `get_logbook` for "what did I complete recently" workflows.
- If completed-task tracking is needed in future, use a different approach: query by completion date directly via the Things URL scheme, or another library method.
- The related `period: "1d"` workaround (use `"2d"` instead) does not actually fix the root issue — same-day completions of older tasks are still missed.
