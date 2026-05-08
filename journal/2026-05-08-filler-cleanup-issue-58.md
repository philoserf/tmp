---
title: "Filler-word cleanup pass across Drafts/ (issue #58)"
type: journal
project: philoserf/notes
tags: [topic/editing]
created: 2026-05-08
updated: 2026-05-08
status: active
---

## Task

Issue #58 — cut filler words (`fundamental`, `actually`, `simultaneously`, `genuinely`, `simply`, `fully`, `ultimately`, `truly`, `necessarily`) across 301 Drafts/ files. 582 instances total.

## Approach

Calibration round on 5 most filler-dense drafts → review with user → expand to per-word passes across the corpus. Each pass got its own commit with cut/keep heuristics in the message.

## Outcome

73 cuts of ~320 instances reviewed across 5 passes. 4 commits on `main`. 3 drafts promoted from `develop` → `review`. Issue stayed open for the remaining `fundamental` (~150) and `actually`/`truly`/`ultimately`/`necessarily` (~160) instances.

| Pass                   | Cuts | Total instances |
| ---------------------- | ---- | --------------- |
| Calibration (5 drafts) | 19   | —               |
| simply                 | 12   | 57              |
| simultaneously         | 12   | 70              |
| genuinely              | 10   | 57              |
| fully                  | 0    | 53              |
| fundamental (partial)  | 20   | 176             |

## Lessons

The author's prose is more disciplined than raw counts suggest. Most "filler words" are doing real argumentative or rhetorical work in this corpus:

- Paired contrasts ("not simply X but Y")
- Modal-paired ("cannot simply X")
- Distinguishing real from apparent ("genuinely X vs claimed X")
- Parallel structures ("neither firmly... nor fully...")

Only ~23% of reviewed instances were bare-intensifier filler. Future passes should expect a low cut rate, not bulk cleanup.

## Patterns produced

- [[2026-05-08-calibration-round-before-scale]]
- [[2026-05-08-git-commit-pathspec-isolation]]
- [[2026-05-08-philoserf-notes-fully-load-bearing]]
