---
title: "Trigger-specificity beats merging when consolidating patterns"
type: pattern
project: "global"
tags: [topic/documentation, topic/workflow]
created: 2026-05-06
updated: 2026-05-06
status: active
---

When tempted to consolidate two patterns that look similar by title, read both fully before merging.

**Rule:** Merge only if the two patterns describe the **same concrete trigger**. If they share a meta-principle but have different triggers, **leave separate and cross-link.**

## Why

Trigger-specificity is what makes a pattern usable. A pattern's value comes from naming the exact situation that should activate it ("when a subagent reports tests pass," "when about to delete a `migrate_*` script," "when surprised by remote git state"). Merging three trigger-specific patterns into one abstract "verify before acting" pattern erases the trigger and produces generic advice that doesn't fire when needed.

## Surfaced

During the 2026-05-06 vault audit, three patterns looked like consolidation candidates by title:

- [[2026-04-29-check-before-alarming]]
- [[2026-04-29-verify-migration-scripts-empirically]]
- [[2026-05-06-verify-subagent-test-claims]]

Each was a _concrete instantiation_ of a "verify before acting" meta-principle, with three distinct triggers. Merging would have produced one abstract pattern that no future agent would actually invoke. Decision: keep separate, the cross-links between them are the right level of relationship.

## How to apply

When the patterns folder feels large, before proposing a merge:

1. Read each consolidation candidate fully — not just the title.
2. Identify each pattern's **trigger** (the situation that should activate it).
3. If two patterns have the same trigger → merge.
4. If they share a meta-principle but have different triggers → leave separate, add cross-links.
5. If unsure, leave separate. Splitting is cheap; un-merging is not.

## Anti-pattern

"23 patterns is too many" is a count-based vibe, not a structural argument. Don't refactor on vibes — read first.
