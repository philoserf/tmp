---
title: "Commit toolchain migrations before unrelated work"
type: pattern
project: "global"
tags: [tool/git, topic/workflow, urgency/gotcha]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Pattern

When you find uncommitted toolchain migration changes (e.g., `justfile` deleted + `Taskfile.yml` added, or `package.json` script renames, or a `Cargo.toml` build-tool swap) at the start of a session, **commit them in their own focused commit before starting any unrelated sub-project**.

## Why

In one observed session, the user had a `just` → `task` migration sitting as uncommitted working-tree changes (deleted `justfile`, new `Taskfile.yml`, modified `CLAUDE.md` and `README.md` to update command references). The migration carried through ~5 hours of session work covering multiple sub-projects on multiple feature branches. Side effects:

- Subagents reported `just check && just test` clean even though `just` couldn't run — they were silently using the new toolchain.
- The newly-written plan referenced `just check` everywhere and had to be sed-replaced before dispatch.
- A feature branch created on top of dirty main carried the migration as bleed-into commits unless explicitly addressed.

The toolchain migration was four files, ~50 line diff. Committing it first would have prevented all three of the above costs.

## How to apply

At the start of every session, run `git status`. If the working tree shows changes that look like a toolchain or infrastructure migration:

1. Stop and inspect: `git diff CLAUDE.md README.md justfile Taskfile.yml` (or whatever).
2. Ask the user "I see an in-flight toolchain migration. Should I commit this first, or is it intentionally pending?"
3. If commit-first: do it as a focused `chore: migrate from X to Y` commit on main.
4. Only then start the sub-project work.

The exception: if the user explicitly says "I'm in the middle of migrating, work around it for now." Even then, flag the side effects before they bite.

## Related

- [[2026-04-29-task-check-pre-commit-gate]] — same family: don't add new gates without baselining first; same logic applies to migrations.
