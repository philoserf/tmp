---
title: "philoserf/notes — research-to-Inbox save pipeline"
type: context
project: "philoserf/notes"
tags: [tool/claude-code, topic/workflow]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Context

The `philoserf/notes` Obsidian vault accepts `/last30days` (and similar research-skill) outputs as Inbox notes with zero friction. This is a stable, reusable pipeline for "research-then-file" flows.

## Pipeline

1. Run the research skill (e.g., `/last30days`).
2. Strip the conversational opening line from the output.
3. Write to `Inbox/<Title Case Title>.md` with required frontmatter:

   ```yaml
   ---
   created: YYYY-MM-DD
   description: One-line summary.
   lastmod: YYYY-MM-DD
   tags: [lowercase-with-dashes]
   ---
   ```

4. The PostToolUse format hook reformats with prettier on save — works cleanly if every code fence has a language tag.
5. Reply with a one-line acknowledgment (filename + tags). No re-display of content.

## Gotcha — tag vocabulary

**Before writing tags**, read `Reference/Tag Vocabulary.md` in the vault. Tags must come from the curated vocabulary; any new tag should be marked `[NEW]` for periodic review.

In the 2026-04-29 session I skipped this check and used uncurated tags (`claude`, `ai-tools`, `editing`, `publishing`, `education`, `research`). Some likely already exist; some may need `[NEW]` marking. The cheapest fix is reading the vocabulary file once at the start of a save batch.

## Gotcha — linking convention

The vault uses **index → topic links only**. No topic → topic wikilinks. Two new notes on the same theme should NOT cross-link directly — they should be surfaced as candidates for the same index parent during `/inbox-triage`.

## Useful follow-up commands

- `obsidian vault=notes unresolved` — check for broken wikilinks after batch saves
- `obsidian vault=notes orphans` — find notes with no incoming links (most fresh Inbox notes will appear here, expected)

## Output structure that fits this user

The `/last30days` template (headline event → industry/landscape context → community patterns → notable dissent → stats block → sources) was accepted twice without revision in this session. Stable shape for research-and-save deliverables in this vault.
