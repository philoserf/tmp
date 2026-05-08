---
title: "Use git commit -- pathspec to isolate from in-flight work"
type: pattern
project: global
tags: [tool/git, urgency/gotcha]
created: 2026-05-08
updated: 2026-05-08
status: active
---

## Pattern

When the working tree contains pre-staged files or unstaged changes that aren't yours, use `git commit -m "..." -- <pathspec>` to commit only changes matching the pathspec. Other staged paths remain in the index for the user to commit separately.

## Why

`git add -A` followed by `git commit` sweeps in everything — including the user's pre-staged files (e.g., a batch of new files they staged manually before delegating a task to you). Result: your commit silently bundles their unrelated work. They can't selectively keep yours and revert theirs.

Pathspec-scoped commits stay narrow:

```bash
git add -A -- Drafts/
git commit -m "..." -- Drafts/
```

`git status` after the commit confirms the user's pre-staged paths are still indexed.

## When to apply

- The user delegated a multi-file task while their working tree had other in-flight work.
- You're about to commit and `git status` shows staged files you didn't add.
- The repo conventions discourage `git add .` / `git add -A` for safety.

## Verification

After the commit, run `git status --short`. Anything still showing `A ` or `M ` in the staging column is preserved correctly.

## Example

Issue #58 cleanup session — working tree had 23 pre-staged Traveller files unrelated to the editing task. Committed Drafts/ changes with explicit pathspec. Verified the Traveller staging survived each of 4 commits.
