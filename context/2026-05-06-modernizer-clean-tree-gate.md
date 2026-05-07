---
title: "Modernizer-clean-tree gate fires on any uncommitted Go diff, not just go fix output"
type: context
project: "global"
tags: [tool/task, lang/go, urgency/gotcha]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Gotcha

Go projects that gate `task check` (or `just check`) on `go fix ./...` producing no diff often implement it as:

```yaml
modernize:
  cmds:
    - go fix ./...
    - |
      if ! git diff --quiet -- '*.go'; then
        echo "ERROR: go fix ./... produced changes."
        exit 1
      fi
```

This compares the working tree against `HEAD`. The error message blames `go fix`, but the gate fires on **any uncommitted Go diff** — including the implementer's own intentional edits made before staging. Subagents repeatedly hit this on first `task check` after their implementation, get a misleading error, and waste time investigating "what did `go fix` change?" before discovering the cure is simply to stage their own changes first.

## How to apply

When dispatching subagents to implement Go changes that end with `task check && task test`:

1. Anticipate the gate's behavior — tell the subagent explicitly: "If `task check` reports modernizer drift, stage your changes first and re-run; the gate compares working tree against HEAD."
2. Or rewrite the gate to compare `go fix`'s output specifically (e.g., snapshot the tree before/after).

The behavior is correct (modernizer hints should be staged or applied before commit), but the error message is misleading and a known source of subagent friction.

## Project precedent

- `philoserf/world-builder` `Taskfile.yml` exhibits this exact pattern. Several subagents during the cmd/wbh Markdown sub-project hit it on their first `task check` invocation.
