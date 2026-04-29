# Vault Conventions

This document defines the schema and rules for entries in this vault. Read this before creating or modifying notes.

## Frontmatter Schema

Every note MUST include this YAML frontmatter block:

```yaml
---
title: "Short descriptive title"
type: context | decision | pattern | reference | journal | handoff
project: "repo-name or 'global'"
tags: [list, of, tags]
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active | superseded | archived
---
```

### Field Definitions

| Field | Required | Description |
|---|---|---|
| `title` | Yes | Human-readable title, quoted |
| `type` | Yes | One of: `context`, `decision`, `pattern`, `reference`, `journal`, `handoff` |
| `project` | Yes | Repository name (e.g., `philoserf/tmp`) or `global` for cross-project entries |
| `tags` | Yes | YAML list of tags from the taxonomy below (may be empty `[]`) |
| `created` | Yes | ISO date when the note was first written |
| `updated` | Yes | ISO date of the most recent edit (same as `created` initially) |
| `status` | Yes | One of: `active`, `superseded`, `archived` |

### Status Lifecycle

- **`active`**: Current and accurate.
- **`superseded`**: Replaced by a newer entry. Add a wikilink to the replacement in the note body: `Superseded by [[YYYY-MM-DD-new-slug]]`.
- **`archived`**: No longer relevant but kept for historical reference.

## Naming Convention

```
YYYY-MM-DD-short-slug.md
```

- Use the date the note was created.
- Use lowercase, hyphen-separated slugs.
- Keep slugs short but descriptive (2-5 words).
- Example: `2026-04-29-vault-bootstrap.md`

## Tag Taxonomy

Use these prefixes. Agents may add new tags within these namespaces.

### Language

- `#lang/python`
- `#lang/go`
- `#lang/typescript`
- `#lang/javascript`
- `#lang/rust`
- `#lang/shell`

### Tooling

- `#tool/claude-code`
- `#tool/amp`
- `#tool/git`
- `#tool/cursor`
- `#tool/copilot`

### Topics

- `#topic/testing`
- `#topic/architecture`
- `#topic/deployment`
- `#topic/debugging`
- `#topic/performance`
- `#topic/security`

### Urgency

- `#urgency/gotcha` — Critical knowledge agents should check before acting.

## Wikilinks

- Use `[[YYYY-MM-DD-short-slug]]` (without `.md`) to link related entries.
- Always add links when a new entry relates to existing entries.
- When superseding a note, add a forward link in the old note and a back link in the new one.

## Create vs. Update vs. Supersede

- **Create** a new note for genuinely new knowledge.
- **Update** an existing note when information changes. Bump the `updated` field.
- **Supersede** when the old note's core premise is wrong or obsolete. Set `status: superseded`, add a wikilink to the replacement. Do not delete.
