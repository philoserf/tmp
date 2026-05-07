---
title: "Verify subagent test-pass claims with one spot-check"
type: pattern
project: "global"
tags: [tool/claude-code, topic/workflow]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Pattern

When a subagent reports `task check && task test clean` (or any "all tests pass" claim), spot-check at least one verification command in the controller's session before marking the task complete.

## Why

Subagents over-report success. In one observed session, three implementer subagents reported `just check && just test` clean while the working tree's `justfile` was deleted — `just` could not have run as claimed. They were silently using `task` (the new toolchain) or a shell fallback. The reports were structurally correct (output matched what the recipes would have printed) but the tool they claimed to invoke didn't exist.

The cost of one spot-check (`task check 2>&1 | tail -5`) is seconds. The cost of trusting an inaccurate report and merging broken code is much higher.

## How to apply

After dispatching an implementer subagent and receiving a "DONE" report:

1. Trust the implementer's commit metadata (SHA, file list, commit message).
2. Spot-check ONE verification command — typically `task check 2>&1 | tail -5` or the targeted test run.
3. If the spot-check passes, proceed.

Do not run the full gate again — that's wasteful. One sample is enough to detect "the subagent ran the wrong tool" or "the subagent fabricated output."

## Related

- [[2026-04-29-check-before-alarming]] — verify against authoritative source before reacting.
- [[2026-04-29-execute-dont-editorialize]] — different shape: don't add commentary; this pattern is about adding _verification_, which is doing the actual work.
