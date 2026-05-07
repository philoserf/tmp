---
title: "related: frontmatter field removed (2026-04-18) — backlinks replace it"
type: decision
project: "philoserf/notes"
tags: [tool/obsidian, topic/architecture, topic/frontmatter]
created: 2026-04-29
updated: 2026-05-06
status: active
---

Related vault-schema decision: [[2026-04-29-obsidian-first-vault-design]].

## Decision

The `related:` frontmatter field (a YAML list of wikilinks to related notes) was removed from all 330 vault notes on **2026-04-18**. It is no longer part of the note schema.

The `/connect-orphans` command was deleted as part of the same change. The `/find-stale` staleness scoring was simplified to count only backlinks.

## Rationale

The user judged that explicit curated related-links "were not serving the complexity." The maintenance cost (choosing, updating, reviewing) exceeded the retrieval benefit, given that Obsidian backlinks already surface connections implicitly.

## How to apply

- **Do not** add `related:` to any new notes or templates.
- **Do not** suggest the user populate a `related:` list as part of any workflow.
- For connection-building, rely on backlinks, tags, and inline wikilinks in the note body.
- If the user asks for "related notes," treat it as a discovery request (grep, backlinks, tags) — not a schema field to populate.
