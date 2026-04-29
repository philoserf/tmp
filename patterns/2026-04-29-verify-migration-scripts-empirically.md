---
title: "Verify migration scripts empirically before deleting them"
type: pattern
project: "global"
tags: [topic/migration, topic/git]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Pattern

When a script looks like a one-shot migration (`migrate_*`, `fix_*_format`, `convert_*`, etc.), **don't delete it based on commit history alone**. Run a grep for the pattern the script targets; only delete after confirming zero (or near-zero, with stragglers fixed by hand) matches remain.

## Rationale

During the 2026-04-13 tech-debt audit on `philoserf/notes`, three migration scripts were deleted. For `migrate_date_to_created.py` the empirical check found 1 stray `date:` outside `Published/` that the script had missed — fixed by hand before deletion. **Trusting git history alone would have left that field in place.**

## How to apply

Before removing scripts named `migrate_*`, `fix_*_format`, or `convert_*`:

1. Read the script to learn its target pattern.
2. Grep the codebase/vault for that pattern.
3. Either confirm zero matches, or hand-fix the stragglers.
4. Then delete the script.

Applies broadly — any project, any language. Git history shows that the script _ran_, not that it _finished the job_.
