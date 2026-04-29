---
title: "Vault bootstrap — initial scaffolding"
type: journal
project: "philoserf/tmp"
tags: [topic/architecture]
created: 2026-04-29
updated: 2026-04-29
status: active
---

# Vault Bootstrap

## Summary

Scaffolded the agent memory vault at `~/source/philoserf/tmp`. Created the folder structure, `CLAUDE.md` bootstrap, `CONVENTIONS.md` schema, and README templates for all six content folders.

## Outcome

The vault is ready for agents to read from and write to. All conventions are documented. Folder READMEs contain entry templates.

## Lessons Learned

- Flat-ish folder structure by content type balances discoverability with simplicity.
- Redundant `type` frontmatter field allows querying without path dependency.
- No index files needed — agents grep frontmatter directly.

## Related

- [[CONVENTIONS|CONVENTIONS.md]] — The schema this vault follows.
