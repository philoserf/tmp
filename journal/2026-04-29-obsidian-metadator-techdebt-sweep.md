---
title: "Obsidian Metadator tech-debt sweep — 9 issues, 12 PRs"
type: journal
project: "philoserf/obsidian-metadator"
tags: [topic/architecture, topic/testing, lang/typescript, tool/copilot]
created: 2026-04-29
updated: 2026-05-06
status: active
---

Long iterative session resolving the open tech-debt backlog on the obsidian-metadator plugin (Anthropic API → Obsidian YAML frontmatter generator). For the project shape see [[2026-04-29-obsidian-metadator-architecture]].

## Closed issues

| #    | Title                                              | Outcome                                                                           |
| ---- | -------------------------------------------------- | --------------------------------------------------------------------------------- |
| #117 | Boolean flag parameters in `addMetadataWithClaude` | `WritePolicy` / `PresentationMode` mode types                                     |
| #122 | Retry backoff fixed, no jitter                     | Full jitter `[0.5x, 1.5x]`, `Retry-After` honored capped at 2x base               |
| #124 | Three modal classes in one file                    | Split into `bulkConfirmModal.ts` / `bulkProgressModal.ts` / `bulkSummaryModal.ts` |
| #114 | Bulk run no upper bound                            | `maxBulkFiles` setting (default 500) + override checkbox                          |
| #121 | No schema version field                            | `schemaVersion` + ordered `MIGRATIONS` map + future-version save refusal          |
| #139 | `migrateSettings` lives in `main.ts`               | Extracted to `src/settingsMigrate.ts`                                             |
| #140 | Duplicated per-helper unit tests                   | Trimmed; helpers unexported; one new integration case                             |
| #141 | `architecture.test.ts` is a lint rule              | Replaced with Biome `noRestrictedImports`                                         |
| #120 | No correlation IDs / structured logging            | `src/logger.ts` with per-call requestId, event vocabulary                         |

Plus #137 docs sync, plus closed #111 / #112 as already-resolved.

## Net state of repo

- 189-ish tests passing across 9 files
- `main.ts` slimmed to ~90 lines (lifecycle + load/save delegation)
- SDK boundary lint-enforced; `src/adapters/claude.ts` is the only static importer
- Schema versioning prevents forward-version data corruption
- Structured logs with per-call requestId + event vocabulary for diagnosis

## Reusable knowledge produced

- [[2026-04-29-strict-positive-int-parser]] — pattern for the `maxBulkFiles` parsing in #114.
- [[2026-04-29-bun-test-mock-module-gotchas]] — testing pattern from the SDK adapter tests.

## Lessons

See [[2026-04-29-copilot-self-review-checklist]] for the recurring self-review failure pattern this session surfaced.

## Future work

- Echo Anthropic `request-id` header in success logs (needs `.withResponse()` migration; deferred)
- `src/bulk/` subfolder move
- Cost estimation + worker-pool concurrency for bulk runs (feature work)
