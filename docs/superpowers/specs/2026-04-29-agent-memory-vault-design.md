# Agent Memory Vault — Design Spec

## Purpose

An Obsidian vault that serves as long-term memory for Claude-based AI coding agents. Agents autonomously read and write entries across sessions, storing project context, decisions, preferences, reference material, task history, and handoff context.

## Location

`~/source/philoserf/tmp` (this repository).

## Access Patterns

- **CLAUDE.md references**: Projects point agents to this vault via CLAUDE.md / AGENTS.md instructions.
- **Direct file reads**: Agents use `Read`, `grep`, and `glob` against the vault at its known path.

## Vault Structure

```
.
├── CLAUDE.md              # Bootstrap: tells agents what this vault is, how to use it
├── CONVENTIONS.md         # Schema: naming, frontmatter fields, tagging rules
├── context/               # Project & codebase context (architecture, tech stacks, gotchas)
│   └── README.md
├── decisions/             # Architecture & design decisions with rationale
│   └── README.md
├── patterns/              # Coding preferences, style conventions, reusable approaches
│   └── README.md
├── references/            # API docs, snippets, templates, prompts
│   └── README.md
├── journal/               # Task history, session logs, lessons learned
│   └── README.md
└── handoffs/              # Agent-to-agent context transfers
    └── README.md
```

Each folder contains a `README.md` with its purpose and an entry template.

## Frontmatter Schema

Every note uses YAML frontmatter:

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

- **`type`** mirrors the folder — redundant so agents can grep without relying on path.
- **`project`** scopes entries; `global` for cross-project knowledge.
- **`status`** indicates currency. `superseded` entries link to their replacement via wikilink.
- **`tags`** are freeform but seeded with a starter taxonomy.

## Naming Convention

```
YYYY-MM-DD-short-slug.md
```

Example: `2026-04-29-tmp-vault-bootstrap.md`

## Agent Interaction Model

### Reading

- Search by folder to narrow scope.
- Grep frontmatter fields (`type`, `project`, `status`, `tags`) to find relevant entries.
- Follow wikilinks to traverse related notes.

### Writing

- Target the appropriate folder based on content type.
- Include all required frontmatter fields.
- Follow the naming convention.
- Add wikilinks to related existing entries.

### When to Write

- After significant decisions.
- At session end, if reusable knowledge was produced.
- When encountering a project for the first time.
- When learning something that would benefit future sessions.

### Create vs. Update vs. Supersede

- **Create** a new note for new knowledge.
- **Update** an existing note when information changes (bump the `updated` field).
- **Supersede** rather than delete: set `status: superseded` and add a wikilink to the replacement.

## Starter Tag Taxonomy

Seeded in `CONVENTIONS.md`; agents may extend organically.

- `#lang/python`, `#lang/go`, `#lang/typescript` — language-specific
- `#tool/claude-code`, `#tool/amp`, `#tool/git` — tooling
- `#tool/cursor`, `#tool/copilot` — other agents for reference
- `#topic/testing`, `#topic/architecture`, `#topic/deployment` — domains
- `#urgency/gotcha` — things agents should know before acting

## Design Decisions

- **No index files**: Agents use grep/glob against frontmatter. Avoids stale indexes.
- **Flat-ish by type**: Balances discoverability with simplicity. No deep nesting.
- **Redundant `type` field**: Allows querying without path dependency.
- **Obsidian-flavored markdown**: Wikilinks and YAML frontmatter are first-class. Acceptable since consumers are primarily Claude-based agents that handle this natively.
- **Read-write by agents**: Fully autonomous. No human gating on writes.
