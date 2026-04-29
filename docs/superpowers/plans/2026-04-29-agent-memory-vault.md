# Agent Memory Vault Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold an Obsidian vault at `~/source/philoserf/tmp` that serves as long-term memory for Claude-based AI coding agents.

**Architecture:** Flat-ish folder structure by memory type, with YAML frontmatter on every note for programmatic querying. A `CLAUDE.md` bootstraps agents into the vault; `CONVENTIONS.md` defines the schema. Each folder has a `README.md` with purpose and entry template.

**Tech Stack:** Obsidian-flavored Markdown, YAML frontmatter, git.

---

## File Structure

Files to create (all new — repo is currently empty):

| File | Responsibility |
|---|---|
| `CLAUDE.md` | Agent bootstrap: what this vault is, how to read/write, path conventions |
| `CONVENTIONS.md` | Schema reference: frontmatter fields, naming rules, tag taxonomy |
| `context/README.md` | Folder purpose + entry template for project/codebase context |
| `decisions/README.md` | Folder purpose + entry template for architecture decisions |
| `patterns/README.md` | Folder purpose + entry template for coding preferences/patterns |
| `references/README.md` | Folder purpose + entry template for API docs/snippets/templates |
| `journal/README.md` | Folder purpose + entry template for task history/session logs |
| `handoffs/README.md` | Folder purpose + entry template for agent-to-agent transfers |

---

### Task 1: Create CLAUDE.md

**Files:**
- Create: `CLAUDE.md`

- [ ] **Step 1: Create `CLAUDE.md`**

```markdown
# Agent Memory Vault

This is a long-term memory store for Claude-based AI coding agents. It lives at `~/source/philoserf/tmp`.

## What This Is

An Obsidian vault where agents read and write structured notes across sessions. It stores project context, architecture decisions, coding patterns, reference material, task history, and agent-to-agent handoffs.

## How to Read

1. **By folder**: Navigate to the relevant folder (`context/`, `decisions/`, `patterns/`, `references/`, `journal/`, `handoffs/`).
2. **By frontmatter**: Grep for `type:`, `project:`, `status:`, or `tags:` in YAML frontmatter to find matching entries.
3. **By wikilinks**: Follow `[[wikilinks]]` in notes to traverse related entries.
4. **Active entries only**: Filter by `status: active` to skip superseded or archived notes.

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

## Folder Map

| Folder | Contents |
|---|---|
| `context/` | Project & codebase context — architecture, tech stacks, gotchas |
| `decisions/` | Architecture & design decisions with rationale |
| `patterns/` | Coding preferences, style conventions, reusable approaches |
| `references/` | API docs, snippets, templates, prompts |
| `journal/` | Task history, session logs, lessons learned |
| `handoffs/` | Agent-to-agent context transfers |
```

- [ ] **Step 2: Verify the file renders correctly**

Run: `head -50 CLAUDE.md`
Expected: The full file content, valid markdown.

- [ ] **Step 3: Commit**

```bash
git add CLAUDE.md
git commit -m "Add CLAUDE.md agent bootstrap"
```

---

### Task 2: Create CONVENTIONS.md

**Files:**
- Create: `CONVENTIONS.md`

- [ ] **Step 1: Create `CONVENTIONS.md`**

```markdown
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
```

- [ ] **Step 2: Verify the file renders correctly**

Run: `head -80 CONVENTIONS.md`
Expected: The full file content, valid markdown with no broken formatting.

- [ ] **Step 3: Commit**

```bash
git add CONVENTIONS.md
git commit -m "Add CONVENTIONS.md vault schema and rules"
```

---

### Task 3: Create context/README.md

**Files:**
- Create: `context/README.md`

- [ ] **Step 1: Create `context/README.md`**

```markdown
# Context

Project and codebase context — architecture overviews, tech stack details, known gotchas, environment setup notes.

## When to Write Here

- When an agent encounters a project for the first time and gathers context worth preserving.
- When architecture, tech stack, or environment details are discovered that future sessions would benefit from.
- When a gotcha or non-obvious behavior is encountered.

## Entry Template

```yaml
---
title: ""
type: context
project: ""
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active
---
```

### Suggested Sections

- **Overview**: What the project does, its purpose.
- **Tech Stack**: Languages, frameworks, key libraries.
- **Architecture**: High-level structure, key components.
- **Gotchas**: Non-obvious behaviors, common pitfalls.
- **Related**: Wikilinks to related entries.
```

- [ ] **Step 2: Commit**

```bash
git add context/README.md
git commit -m "Add context/ folder with README template"
```

---

### Task 4: Create decisions/README.md

**Files:**
- Create: `decisions/README.md`

- [ ] **Step 1: Create `decisions/README.md`**

```markdown
# Decisions

Architecture and design decisions with rationale. Similar to ADRs (Architecture Decision Records).

## When to Write Here

- When a significant technical decision is made during a session.
- When choosing between approaches and the reasoning should be preserved.
- When a previous decision is revisited or reversed.

## Entry Template

```yaml
---
title: ""
type: decision
project: ""
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active
---
```

### Suggested Sections

- **Context**: What prompted this decision.
- **Options Considered**: Brief description of alternatives.
- **Decision**: What was chosen and why.
- **Consequences**: Trade-offs, follow-up actions.
- **Related**: Wikilinks to related entries.
```

- [ ] **Step 2: Commit**

```bash
git add decisions/README.md
git commit -m "Add decisions/ folder with README template"
```

---

### Task 5: Create patterns/README.md

**Files:**
- Create: `patterns/README.md`

- [ ] **Step 1: Create `patterns/README.md`**

```markdown
# Patterns

Coding preferences, style conventions, and reusable approaches. The user's preferred way of doing things.

## When to Write Here

- When a coding preference or convention is stated or observed.
- When a reusable approach or pattern is discovered.
- When a library choice or configuration preference is established.

## Entry Template

```yaml
---
title: ""
type: pattern
project: "global"
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active
---
```

### Suggested Sections

- **Pattern**: What the preference or approach is.
- **Rationale**: Why this is preferred.
- **Examples**: Code snippets or references demonstrating the pattern.
- **Exceptions**: When this pattern does NOT apply.
- **Related**: Wikilinks to related entries.
```

- [ ] **Step 2: Commit**

```bash
git add patterns/README.md
git commit -m "Add patterns/ folder with README template"
```

---

### Task 6: Create references/README.md

**Files:**
- Create: `references/README.md`

- [ ] **Step 1: Create `references/README.md`**

```markdown
# References

API documentation excerpts, code snippets, reusable templates, and prompt patterns.

## When to Write Here

- When an API or library's usage is non-obvious and worth documenting.
- When a useful code snippet is created that could be reused.
- When a prompt pattern proves effective and should be preserved.

## Entry Template

```yaml
---
title: ""
type: reference
project: "global"
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active
---
```

### Suggested Sections

- **Summary**: What this reference covers.
- **Content**: The actual reference material (code, API details, prompt text).
- **Usage**: When and how to use this.
- **Source**: Where the information came from (URL, docs, etc.).
- **Related**: Wikilinks to related entries.
```

- [ ] **Step 2: Commit**

```bash
git add references/README.md
git commit -m "Add references/ folder with README template"
```

---

### Task 7: Create journal/README.md

**Files:**
- Create: `journal/README.md`

- [ ] **Step 1: Create `journal/README.md`**

```markdown
# Journal

Task history, session logs, and lessons learned. A chronological record of what agents did and what they learned.

## When to Write Here

- At the end of a significant work session.
- When a task produces lessons worth preserving.
- When troubleshooting reveals non-obvious solutions.

## Entry Template

```yaml
---
title: ""
type: journal
project: ""
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active
---
```

### Suggested Sections

- **Summary**: What was done in this session/task.
- **Outcome**: What was achieved, what state things were left in.
- **Lessons Learned**: What would be useful to know for next time.
- **Related**: Wikilinks to related entries.
```

- [ ] **Step 2: Commit**

```bash
git add journal/README.md
git commit -m "Add journal/ folder with README template"
```

---

### Task 8: Create handoffs/README.md

**Files:**
- Create: `handoffs/README.md`

- [ ] **Step 1: Create `handoffs/README.md`**

```markdown
# Handoffs

Agent-to-agent context transfers. When one agent session ends and another needs to pick up the work.

## When to Write Here

- When a session ends with incomplete work that another session should continue.
- When transferring complex context that can't be captured in a commit message.
- When a task requires multiple sessions and continuity matters.

## Entry Template

```yaml
---
title: ""
type: handoff
project: ""
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active
---
```

### Suggested Sections

- **Current State**: Where things stand right now.
- **What Was Done**: Summary of completed work.
- **What Remains**: Specific next steps.
- **Key Context**: Important decisions, constraints, or gotchas the next agent needs.
- **Files Touched**: Paths to files that were modified or are relevant.
- **Related**: Wikilinks to related entries.
```

- [ ] **Step 2: Commit**

```bash
git add handoffs/README.md
git commit -m "Add handoffs/ folder with README template"
```

---

### Task 9: Create seed journal entry

**Files:**
- Create: `journal/2026-04-29-vault-bootstrap.md`

- [ ] **Step 1: Create `journal/2026-04-29-vault-bootstrap.md`**

```markdown
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
```

- [ ] **Step 2: Commit**

```bash
git add journal/2026-04-29-vault-bootstrap.md
git commit -m "Add seed journal entry for vault bootstrap"
```

---

### Task 10: Verify vault integrity

- [ ] **Step 1: Verify all expected files exist**

Run:
```bash
find . -name '*.md' -not -path './.git/*' -not -path './docs/*' | sort
```

Expected output:
```
./CLAUDE.md
./CONVENTIONS.md
./context/README.md
./decisions/README.md
./handoffs/README.md
./journal/2026-04-29-vault-bootstrap.md
./journal/README.md
./patterns/README.md
./references/README.md
```

- [ ] **Step 2: Verify all READMEs contain frontmatter template blocks**

Run:
```bash
for f in context/README.md decisions/README.md patterns/README.md references/README.md journal/README.md handoffs/README.md; do
  echo "=== $f ==="
  grep -c "^title:" "$f" || echo "MISSING frontmatter template"
done
```

Expected: Each file prints `1`.

- [ ] **Step 3: Verify seed journal entry has valid frontmatter**

Run:
```bash
head -10 journal/2026-04-29-vault-bootstrap.md
```

Expected: YAML frontmatter block with all required fields populated.

- [ ] **Step 4: Verify git log shows all commits**

Run:
```bash
git log --oneline
```

Expected: 9 commits (spec + 8 vault files).
