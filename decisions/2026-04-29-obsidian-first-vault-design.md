---
title: "Obsidian-first vault design — Obsidian owns the field, Hugo adapts"
type: decision
project: "philoserf/notes"
tags: [tool/obsidian, tool/hugo, topic/architecture]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Decision

When proposing frontmatter changes that touch both Obsidian and Hugo, design from the Obsidian side first. Hugo adapts to what Obsidian provides, not the other way around.

## Rationale

The vault is Obsidian-first. The user corrected an earlier proposal that kept Hugo's `date` convention as authoritative and added `publishDate` as a workaround. The corrected design: `created` belongs to Obsidian (universal), `date` belongs to Hugo's `Published/` notes only (a publishing artifact).

## Field ownership (current)

- **Obsidian Linter (automatic, all notes):** `created`, `lastmod`
- **Manual, Hugo Published/ only:** `date`, `status`

## How to apply

Before suggesting frontmatter field names or conventions:

1. Ask which system "owns" the field.
2. Default to Obsidian conventions; treat Hugo-facing fields as scoped exceptions for `Published/`.
3. Don't overload one field across both systems (e.g., a `date` that means creation date in Obsidian and publication date in Hugo).
