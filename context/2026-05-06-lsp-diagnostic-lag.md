---
title: "LSP UndeclaredName diagnostics lag ~30s after file creation"
type: context
project: "global"
tags: [tool/claude-code, lang/go, urgency/gotcha]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Gotcha

After creating a new Go file with a function, the editor's LSP layer reports `(UndeclaredName)` errors against test files that reference the new function — even though the file exists on disk and `go test` passes. The LSP cache is stale for ~30 seconds.

## Why this matters

Across a single multi-task session, this fired four times in a row, each immediately after a successful subagent implementation commit. Treating the diagnostics as authoritative would have prompted unnecessary investigation or "fixes" to working code.

## How to apply

When `(UndeclaredName)` or similar compiler-style diagnostics fire on freshly-created code:

1. Do not investigate the diagnostics directly.
2. Verify with `grep -n "func <Name>" <file>` — is the function actually defined?
3. Verify with `go test ./<package>/ -run <TestName> -v` — does the test actually pass?
4. If both are true, the diagnostics are stale LSP cache. Move on.

This is a tooling artifact, not a project bug. It applies to any Go project under active editing in an LSP-aware editor while running test-driven workflows.

## Related

- [[2026-04-29-check-before-alarming]] — same shape: verify against authoritative source before reacting to surprises.
