---
title: "No design/plan docs in commits"
type: pattern
project: "global"
tags: [tool/git, topic/workflow]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Do not commit design docs or implementation plans (`design.md`, `plan.md`, `specs/`) to the repository.

## Why

They are working documents used during brainstorming and planning, not deliverables. Only the skill/code itself should be committed.

## How to apply

When the brainstorming or writing-plans skill creates spec/plan files, keep them local for the session but exclude them from git commits. If a subagent commits one, remove it before pushing.
