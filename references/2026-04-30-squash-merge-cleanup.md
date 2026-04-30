---
title: "Squash-merge breaks git branch -d"
type: reference
project: "global"
tags: [tool/git, urgency/gotcha]
created: 2026-04-30
updated: 2026-04-30
status: active
---

GitHub's squash-merge creates a new commit on the target branch, so the local PR branch never becomes an ancestor of `main`. `git branch -d <branch>` checks reachability and refuses with:

```text
error: the branch '<branch>' is not fully merged
```

The branch IS merged in the GitHub sense — its changes are upstream as one new commit — but git's local check can't see that.

## Resolution

1. Confirm the PR is actually merged: `gh pr view <num> --json state,mergeCommit -q .state`.
2. Then `git branch -D <branch>`.

Don't `-D` blindly — the rule "never clean up branches until the associated PR is confirmed merged" still applies. The PR-merged check is what makes `-D` safe; without it, `-D` could discard real local-only work.

## Alternative

If your team uses merge commits (not squash), `-d` works fine — squash and rebase-merge are the cases that trip this.
