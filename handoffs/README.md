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
