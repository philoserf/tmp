---
name: vault-audit
description: Use when auditing this agent-memory vault for stale entries, broken or asymmetric wikilinks, missing cluster cross-links, or INDEX.md drift; or when periodic vault maintenance is requested ("audit", "clean up", "review the wiki", "what should we do with this").
---

# Vault Audit

## Overview

Maintenance skill for the agent-memory vault at `~/source/philoserf/tmp`. Sweeps for staleness, link asymmetries, cluster gaps, and INDEX.md drift, then fixes them. Closes with a session journal entry and a single commit.

This vault uses: type-folder layout (`context/`, `decisions/`, `patterns/`, `references/`, `journal/`, `handoffs/`), `YYYY-MM-DD-slug.md` naming, YAML frontmatter with `title`/`type`/`project`/`tags`/`created`/`updated`/`status`. See `CONVENTIONS.md` at vault root.

## Audit checklist

### 1. Survey state

```bash
# Counts per folder vs. INDEX.md claim
for d in context decisions patterns references journal handoffs; do
  count=$(ls "$d" 2>/dev/null | grep -vE '^(README|CLAUDE)\.md$' | grep -c '\.md$')
  echo "$d: $count"
done
```

```bash
# Non-active entries (should be rare)
grep -rE "^status: (superseded|archived)" --include="*.md" .
```

### 2. Extract link graph

```bash
for f in $(find . -name "*.md" ! -name "CLAUDE.md" ! -name "README.md" ! -name "CONVENTIONS.md" ! -name "INDEX.md" ! -path "./docs/*" ! -path "./.claude/*"); do
  links=$(grep -oE '\[\[[^]]+\]\]' "$f" | sort -u | tr '\n' ' ')
  echo "$f :: $links"
done | sort
```

### 3. Find issues in the link graph

- **One-way links that should be bidirectional.** A journal links to a pattern it produced, but the pattern doesn't backlink. Or two related decisions in the same `project` don't link.
- **Cluster gaps.** Entries sharing a `project` field, or describing variants of the same gotcha, with no link between them.
- **Prose mentions that should be wikilinks.** Entries mentioning "the X decision entry" or "see X" in plain text instead of `[[X]]`.
- **Example syntax — don't fix.** `[[Filename]]` inside code blocks or descriptive prose is illustration, not a broken link.

### 4. Apply fixes

For each fix:

- Add the wikilink in the right place — usually a "Related: ..." line near the top of the body, or in the section where the relationship lives.
- Bump `updated:` to today's date in the frontmatter.
- Don't change anything else in the entry.

### 5. INDEX.md maintenance

When the audit (or remote commits pulled in during the session) added entries:

- Bump the **counts** line at the top of `INDEX.md`.
- Add new entries to their **project** section AND to any **topic cluster** section that fits.
- Re-run the count check (step 1) and verify claim matches actual.

### 6. Pattern consolidation check (optional)

If the patterns folder seems large and titles look redundant, before merging:

- **Read each candidate fully.** Don't merge based on title family-resemblance.
- Merge only if two patterns describe the **same concrete trigger**.
- If they share a meta-principle but have different triggers, **leave separate and cross-link.** Trigger-specificity is what makes a pattern usable; merging loses it.

### 7. Close the session — journal entry

Write `journal/YYYY-MM-DD-vault-audit-and-index.md` (or similar) capturing:

- What was found: counts, staleness, link issues, judgment calls.
- What was changed: specific entries with `[[wikilinks]]` to them.
- Any non-obvious decision worth preserving (e.g., why a consolidation candidate was rejected).

Add the new journal entry to `INDEX.md` and bump the count again.

### 8. Commit

Single commit, stage files explicitly:

```bash
git add CLAUDE.md INDEX.md path/to/each/edited/entry.md ...
git commit -m "session YYYY-MM-DD: vault audit, link cleanup, INDEX.md"
```

**Confirm with the user before pushing.** If the push is rejected (remote diverged), `git pull --rebase`, update INDEX.md to reflect any new entries from the rebase, commit the index update, and push.

## Common mistakes

| Mistake                                            | Fix                                                                       |
| -------------------------------------------------- | ------------------------------------------------------------------------- |
| Mass-spamming wikilinks for any topical similarity | Add a link only when there's a genuine relationship, not "both about git" |
| Merging patterns that share a meta-principle       | Trigger-specificity is what makes a pattern usable — cross-link instead   |
| Forgetting to bump INDEX count line                | Per the `index-file-audit` pattern, claim must match actual               |
| Treating example syntax as broken links            | `[[Filename]]` in code/prose context is illustration                      |
| Modifying entries beyond the wikilink fix          | `updated:` covers the link change; don't sneak in unrelated edits         |
| Pushing without rebasing first                     | Other sessions write to this vault; expect divergence and rebase cleanly  |

## Notes on this vault's structure

- `.obsidian/` is per-machine Obsidian config; gitignored.
- `docs/superpowers/` holds the original design spec and implementation plan; left in place outside the type-folder structure.
- `handoffs/` is typically empty; no incomplete work between sessions is the norm.
- The vault has a sibling personal vault (`philoserf/notes`, ~2,400 notes) with **different** conventions (index→topic only, no cross-links, status vocabulary, no `related:`). This skill does not apply there.
