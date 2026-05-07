---
title: "git stash pop conflicts after cross-branch moves"
type: context
project: "global"
tags: [tool/git, topic/debugging]
created: 2026-04-29
updated: 2026-05-06
status: active
---

If you stash on branch A (which has commits not on B) and pop on branch B, every file touched by an A-only commit will conflict. The stash baseline includes those commits' content; the new branch doesn't.

Related stash gotcha: [[2026-04-29-git-stash-unmerged-paths]].

## Why

Stash records a working-tree diff against the index at stash time. The "baseline" of that diff is the post-A-only-commit state. Apply to a tree without those commits → 3-way merge sees both sides changed.

## How to apply

Before `git stash pop` on a different branch, run `git log A..B` and `git log B..A` to find divergent commits. If any divergent commit on A touches files in the stash, cherry-pick that commit to B first, then pop. Or use `git rebase --onto` to relocate before stashing.
