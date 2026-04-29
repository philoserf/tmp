---
title: "git stash refuses unmerged paths even without active merge"
type: reference
project: "global"
tags: [tool/git, urgency/gotcha]
created: 2026-04-29
updated: 2026-04-29
status: active
---

`git stash push -- <path>` fails with `error: could not write index / <path>: needs merge` if the path is in UU (unmerged) state, even when there is no active `MERGE_HEAD`, `REBASE_HEAD`, or `CHERRY_PICK_HEAD` (stale residue state from a prior aborted operation).

## Workflow to stash conflict residue

1. Check there is no active merge operation:

   ```bash
   ls .git/{MERGE,REBASE,CHERRY_PICK}_HEAD 2>&1 | grep -v "No such"
   ```

2. `git add <path>` — stages current working-tree content (including conflict markers), marking the path resolved in the index.
3. `git stash push -m "..." -- <path>` — now succeeds; stash contains the conflict markers as a normal diff against HEAD.
4. Working tree reverts to HEAD's version of the path.

## Restoring

`git stash pop stash@{N}`. The conflict markers come back in the working tree, not in the index — typically what you want for further investigation.

## Source

Verified 2026-04-24 on `philoserf/obsidian-metadator main.js` (21 conflict marker lines from a prior botched merge of the committed build artifact). Migrated from per-project auto-memory to the agent memory vault on 2026-04-29.
