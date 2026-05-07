---
title: "Frontmatter field ownership — Linter vs manual"
type: pattern
project: "philoserf/notes"
tags: [tool/obsidian, tool/hugo, topic/frontmatter]
created: 2026-04-29
updated: 2026-05-06
status: active
---

Related: [[2026-04-29-obsidian-first-vault-design]] (where the ownership rule comes from), [[2026-04-29-status-vocabulary-imperative]] (the `status` field's vocabulary).

## Pattern

Frontmatter fields have clear ownership as of 2026-04-02:

| Field     | Owner                  | Scope                   |
| --------- | ---------------------- | ----------------------- |
| `created` | Obsidian Linter (auto) | All notes               |
| `lastmod` | Obsidian Linter (auto) | All notes               |
| `date`    | Manual                 | `Published/` only       |
| `status`  | Manual                 | `Drafts/`, `Published/` |

Linter sort order: `title, aliases, series, description, related, tags, status, created, date, lastmod`.

(Note: `related` was later removed — see [[2026-04-29-related-frontmatter-field-removed]]. Sort order may have been updated since.)

## Rationale

Resolved an overloaded `date` field that previously served as both creation date (Obsidian) and Hugo publish date.

## How to apply

When adding new frontmatter fields:

1. Decide which system owns the field.
2. Scope it to that system's folders only.
3. Don't overload fields across systems.
4. If Linter manages the field, the Linter config is the source of truth — update it there, not by editing notes by hand.
