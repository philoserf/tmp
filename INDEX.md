# Vault Index

Navigable map of vault entries. Grouped by **project** first (where most navigation starts), then by **topic cluster** for cross-cutting global entries. Counts follow the [[2026-04-29-index-file-audit]] pattern: claim vs. actual.

**Counts:** 13 context · 3 decisions · 27 patterns · 7 references · 9 journal · 0 handoffs = **59 entries** across 6 folders.

## By project

### philoserf/notes (Obsidian vault)

Decisions

- [[2026-04-29-obsidian-first-vault-design]] — Obsidian owns the field, Hugo adapts
- [[2026-04-29-related-frontmatter-field-removed]] — backlinks replace `related:`

Context

- [[2026-04-29-notes-vault-research-save-pipeline]] — research-to-Inbox flow
- [[2026-04-29-task-check-pre-commit-gate]] — baseline before adding
- [[2026-04-29-changelog-md-plugin-managed]] — not collateral damage
- [[2026-04-29-obsidian-cli-property-set-list-syntax]] — JSON array required for lists
- [[2026-04-29-things-mcp-logbook-unreliable]] — filters by creation, not completion

Patterns

- [[2026-04-29-frontmatter-field-ownership]] — Linter vs. manual
- [[2026-04-29-status-vocabulary-imperative]] — draft → develop → review → publish
- [[2026-04-29-obsidian-note-format]] — formatting conventions
- [[2026-04-29-prefer-delete-and-regenerate]] — over scripted renames
- [[2026-04-29-mermaid-default-tb]] — top-to-bottom for narrow screens
- [[2026-05-06-retrospective-journal-framing]] — honest framing for backfills
- [[2026-05-06-three-way-voice-filter]] — Drafts/Reference/delete decision tree

Journal

- [[2026-04-29-last30days-research-save-cycles]] — two save cycles into the vault
- [[2026-05-06-multi-horizon-journal-backfill]] — daily/weekly/monthly backfill session
- [[2026-05-07-sparta-moose-pdf-layout]] — one-page schedule PDF via pandoc + typst

### philoserf/obsidian-metadator (plugin)

Context

- [[2026-04-29-obsidian-metadator-architecture]] — project shape

Journal

- [[2026-04-29-obsidian-metadator-techdebt-sweep]] — 9 issues, 12 PRs
- [[2026-04-30-obsidian-metadator-2-2-0-release]] — release flow

Patterns/references produced from this work

- [[2026-04-29-strict-positive-int-parser]]
- [[2026-04-29-bun-test-mock-module-gotchas]]
- [[2026-04-29-bun-dotenv-asymmetry]]
- [[2026-04-29-copilot-self-review-checklist]]

### philoserf/world-builder

Decisions

- [[2026-05-06-markdown-consumes-structs]] — formatters consume existing form structs

Context

- [[2026-05-06-lsp-diagnostic-lag]] — UndeclaredName lag ~30s after file creation
- [[2026-05-06-modernizer-clean-tree-gate]] — gate fires on any uncommitted Go diff

Journal

- [[2026-05-06-world-builder-completion]] — physical rules + Markdown output

Patterns produced from this work

- [[2026-05-06-hybrid-markdown-form-layout]]
- [[2026-05-06-explicit-placeholder-over-silent-zero]]
- [[2026-05-06-verify-subagent-test-claims]]
- [[2026-05-06-read-before-deciding-consume-vs-derive]]
- [[2026-05-06-commit-toolchain-migrations-first]]

### Traveller/Clement (sourced-prose project)

Journal

- [[2026-04-29-clement-todo-cleanup]] — TODO cleanup and canon-contradiction sweep

Patterns produced

- [[2026-04-29-canon-contradiction-protocol]]
- [[2026-04-29-orphan-fact-disposition]]
- [[2026-04-29-index-file-audit]]

### philoserf/tmp (this vault, meta)

- [[2026-04-29-vault-bootstrap]] — initial scaffolding journal
- [[2026-05-06-vault-audit-and-index]] — audit, link cleanup, INDEX creation
- [[2026-05-06-vault-concurrent-writers]] — context: expect rebase divergence
- `docs/superpowers/specs/2026-04-29-agent-memory-vault-design.md` — design spec
- `docs/superpowers/plans/2026-04-29-agent-memory-vault.md` — implementation plan

## By topic cluster (global entries)

### Workflow discipline

- [[2026-04-29-dig-and-advise-pattern]]
- [[2026-04-29-execute-dont-editorialize]]
- [[2026-04-29-prefer-durable-options]]
- [[2026-05-06-read-before-deciding-consume-vs-derive]]
- [[2026-04-29-no-design-plan-docs-in-commits]]

### Trust-but-verify

- [[2026-04-29-check-before-alarming]]
- [[2026-04-29-verify-migration-scripts-empirically]]
- [[2026-05-06-verify-subagent-test-claims]]

### Git / PR workflow

- [[2026-04-29-git-stash-pop-cross-branch]]
- [[2026-04-29-git-stash-unmerged-paths]]
- [[2026-04-30-squash-merge-cleanup]]
- [[2026-04-29-pr-review-reply-workflow]] ↔ [[2026-04-29-gh-pr-review-comment-reply]]
- [[2026-05-06-commit-toolchain-migrations-first]]
- [[2026-04-29-no-design-plan-docs-in-commits]]

### Tooling gotchas (claude-code, MCPs, language tooling)

- [[2026-05-06-lsp-diagnostic-lag]]
- [[2026-05-06-modernizer-clean-tree-gate]]
- [[2026-05-06-sysprompt-currentdate-staleness]]
- [[2026-04-29-bash-close-escape-open-quoting]]
- [[2026-04-29-things-mcp-logbook-unreliable]]
- [[2026-04-29-macos-cp-empty-destination]]
- [[2026-05-07-macos-pdf-page-count-mdls-stale]] — `mdls` lags after rebuilds; use `pdfinfo`

### Bun / TypeScript

- [[2026-04-29-bun-test-mock-module-gotchas]]
- [[2026-04-29-bun-dotenv-asymmetry]]
- [[2026-04-29-strict-positive-int-parser]]

### Markdown rendering / release tooling

- [[2026-05-06-hybrid-markdown-form-layout]]
- [[2026-05-06-explicit-placeholder-over-silent-zero]]
- [[2026-04-30-walkthrough-regen-heuristic]]
- [[2026-04-30-changelog-section-extract-awk]]
- [[2026-05-07-pandoc-typst-figure-overrides]] — pandoc + typst custom template for table layout

### Code review

- [[2026-04-29-copilot-self-review-checklist]]
- [[2026-04-29-pr-review-reply-workflow]]

### Documentation / canon (sourced-prose projects)

- [[2026-04-29-canon-contradiction-protocol]]
- [[2026-04-29-orphan-fact-disposition]]
- [[2026-04-29-index-file-audit]]

### Vault meta-patterns

- [[2026-05-06-trigger-specificity-over-merging]] — read before merging similar-titled patterns

## Maintenance

This index is hand-maintained. When adding a new entry:

1. Add it to the appropriate project section (or topic cluster, for global entries).
2. Bump the count line at the top.
3. Run the [[2026-04-29-index-file-audit]] check: `ls <folder> | wc -l` against the claimed count.
