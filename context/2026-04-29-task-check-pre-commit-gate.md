---
title: "task check is the pre-commit gate — baseline before adding"
type: context
project: "philoserf/notes"
tags: [topic/git, topic/ci, tool/task]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Gotcha

`Taskfile.yml` defines `task check`. `.claude/settings.json` wires a PreToolUse hook on `Bash(git commit*)` to call it. **Whatever runs inside `task check` therefore runs on every git commit and can block it (exit 2).**

Wiring a new check without baseline-checking the existing codebase is a foot-gun: the new check will block all future commits if any existing file fails it.

## Precedent

During the 2026-04-13 audit, adding ruff/shellcheck/shfmt to `task check` surfaced a pre-existing `local`-outside-function bug in `strip_singletons.sh:56` that would have blocked all future commits if not fixed first.

## How to apply

Before adding any new check to `task check`:

1. Run that check against the existing codebase manually.
2. Fix or accept any failures.
3. Wire it into `task check` only after the baseline is clean.

Existing checks use `--write` semantics (auto-format), not `--check`. Match that style for any new formatters added to the gate.
