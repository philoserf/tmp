---
title: "macOS BSD cp resolves empty destination to cwd"
type: reference
project: "global"
tags: [lang/shell, urgency/gotcha]
created: 2026-04-29
updated: 2026-04-29
status: active
---

On macOS (BSD `cp`), passing an empty string as the destination does not error. It resolves to the current directory and attempts the copy. If the source is a file at the project root (e.g., a build artifact), the copy targets itself and `cp` emits:

```text
cp: ./src.file and src.file are identical (not copied).
```

This is a misleading error. The underlying cause is usually an unset or empty environment variable in a shell command like `cp a b "$DEST"`.

## How to apply

- When you see "source and dest are identical" for a file that obviously shouldn't match, check whether the destination is an unset env var expanding to empty, not a real path-collision.
- Harden any shell-based `cp` with a guard: `test -n "$DEST" || { echo "DEST not set"; exit 1; }`.
- For Bun projects, prefer native TS scripts using `Bun.$` — see [[2026-04-29-bun-dotenv-asymmetry]] for why package.json shell scripts are especially prone to this.

## Source

Originally captured on `philoserf/obsidian-metadator` (~2026-04-16). Migrated from per-project auto-memory to the agent memory vault on 2026-04-29.
