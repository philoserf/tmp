---
title: "Status vocabulary is imperative verbs (draft → develop → review → publish)"
type: pattern
project: "philoserf/notes"
tags: [topic/frontmatter, topic/publishing]
created: 2026-04-29
updated: 2026-05-06
status: active
---

Related: [[2026-04-29-frontmatter-field-ownership]] (where `status` ownership is defined).

## Pattern

The `status` frontmatter field uses imperative verbs naming **what to do with the note**:

```text
draft → develop → review → publish
```

Only `publish` (in `Published/`) is consumed by the obsidian-publisher gate; the others live in `Drafts/`.

## Scope

- **Folders that carry `status`:** `Drafts/`, `Published/`
- **Folders that do NOT:** `Reference/`, `Private/`, `Holding/`, `Traveller/`, `Inbox/`

## Trued up 2026-04-17

Replaced a prior mixed vocabulary (`emerging` / `developing` / `pending` / `published`). Mixed grammar in one field (state participles + imperative) made the semantics inconsistent. Imperative was chosen because `publish` was already the gate value in the publisher rewrite, and the rest now match.

## Constraints

- `Data/Publishing Pipeline.base` filters on these exact strings — any rename must update the base file's view filters and the `status_order` formula together.
- The publisher gate regex matches `^status:\s*publish\s*$` (unquoted). Linter must not wrap this scalar in quotes.
- Historical notes (`Journals/`, old code reviews in `Inbox/`) may still show the old vocabulary — leave as period-accurate record, do not mass-rewrite.

## How to apply

- New notes in `Drafts/` start at `draft`.
- Promotion is manual (`draft` → `develop` → `review` → `publish`).
- Do not invent new status values without updating the base view filters and the publisher regex.
