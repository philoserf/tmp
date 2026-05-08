---
title: "Calibration round before scaling editing/refactoring work"
type: pattern
project: global
tags: [topic/editing]
created: 2026-05-08
updated: 2026-05-08
status: active
---

## Pattern

When a task involves applying judgment across many files (copyedit, refactor, lint-rule application), do a small calibration batch first and present results before scaling.

## Why

Surface-level metrics (word counts, lint hits, type errors) overstate the cuttable subset. Calibration on a representative sample catches:

- Style questions you didn't know to ask ("how aggressive on `fundamental`?")
- Patterns that look like filler but are load-bearing in the local idiom
- Promotion/side-effect decisions that should be checkpointed before propagating

## How

1. Pick 3–5 highest-density files from the metric.
2. Apply judgment, make edits, commit them in one labeled commit.
3. Report back with cuts/keeps, judgment calls flagged, sample diff.
4. Wait for sign-off (or redirect) before scaling to the rest.

## Example

Issue #58 in philoserf/notes — 582 filler-word instances across 301 drafts. Calibration on 5 dense drafts surfaced that ~80% of instances were load-bearing in the author's rhetorical idiom. Going straight to bulk-edit would have flattened the prose.

## Cousin patterns

- [[2026-04-29-execute-dont-editorialize]] — once calibrated, push through
- [[2026-04-29-prefer-durable-options]] — calibration favors durable judgment over speed
