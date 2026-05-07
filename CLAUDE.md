# Agent Memory Vault

This is a long-term memory store for Claude-based AI coding agents. It lives at `~/source/philoserf/tmp`.

## What This Is

An Obsidian vault where agents read and write structured notes across sessions. It stores project context, architecture decisions, coding patterns, reference material, task history, and agent-to-agent handoffs.

## How to Read

1. **By index**: Start at [[INDEX]] for a project- and topic-grouped map of all entries.
2. **By folder**: Navigate to the relevant folder (`context/`, `decisions/`, `patterns/`, `references/`, `journal/`, `handoffs/`).
3. **By frontmatter**: Grep for `type:`, `project:`, `status:`, or `tags:` in YAML frontmatter to find matching entries.
4. **By wikilinks**: Follow `[[wikilinks]]` in notes to traverse related entries.
5. **Active entries only**: Filter by `status: active` to skip superseded or archived notes.

## How to Write

1. Read `CONVENTIONS.md` for the full schema.
2. Pick the correct folder for the content type.
3. Name the file: `YYYY-MM-DD-short-slug.md`.
4. Include all required frontmatter fields (see `CONVENTIONS.md`).
5. Add `[[wikilinks]]` to related existing entries.
6. Commit the change.

## When to Write

- After making a significant decision.
- At session end, if reusable knowledge was produced.
- When encountering a project for the first time.
- When learning something that would benefit future sessions.

After adding an entry, also add it to [[INDEX]] under the right project/topic section.

## Folder Map

| Folder        | Contents                                                        |
| ------------- | --------------------------------------------------------------- |
| `context/`    | Project & codebase context — architecture, tech stacks, gotchas |
| `decisions/`  | Architecture & design decisions with rationale                  |
| `patterns/`   | Coding preferences, style conventions, reusable approaches      |
| `references/` | API docs, snippets, templates, prompts                          |
| `journal/`    | Task history, session logs, lessons learned                     |
| `handoffs/`   | Agent-to-agent context transfers                                |
