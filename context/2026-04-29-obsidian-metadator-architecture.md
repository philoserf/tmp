---
title: "Obsidian Metadator architecture snapshot"
type: context
project: "philoserf/obsidian-metadator"
tags: [topic/architecture, lang/typescript]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Snapshot of the codebase after the 2026-04-29 tech-debt sweep. See [[2026-04-29-obsidian-metadator-techdebt-sweep]] for the work that produced this state.

## Layers

- `src/main.ts` — Plugin lifecycle and command/menu registration. Owns `loadSettings` / `saveSettings`. Refuses to save when a forward-version data file is detected (`futureSchemaBlocked`).
- `src/settings.ts` — `MetadataToolSettings` interface, `DEFAULT_SETTINGS`, `CURRENT_SCHEMA_VERSION`, valid-option enums.
- `src/settingsMigrate.ts` — Pure migration code. Returns a discriminated `MigrationResult` (`kind: "ok" | "missing" | "future"`). `applyMigrations` throws on missing target-version entry to catch bump-without-migration bugs at load time.
- `src/settingsTab.ts` — Settings UI with `parseStrictPositiveInt` for numeric fields.
- `src/metadata.ts` — Single-file generation flow. `addMetadataWithClaude` mints a per-call `requestId` and threads it through structured logs.
- `src/bulkOrchestrator.ts` + `src/bulkGenerate.ts` — Folder-level run with retry. `computeDelayMs` applies full jitter `[0.5x, 1.5x]` and honors `Retry-After` capped at 2x base.
- `src/bulk{Confirm,Progress,Summary}Modal.ts` — UI modals. Confirm modal hard-caps `willChange` with an override checkbox.
- `src/adapters/claude.ts` — Anthropic SDK wrapper. **Only file allowed to import `@anthropic-ai/sdk`** (Biome-enforced). Forces `submit_metadata` tool call, validates input, classifies errors into `ClaudeApiError`.
- `src/adapters/frontmatter.ts` — `updateFrontMatter` over `app.fileManager.processFrontMatter`.
- `src/content/` — `getContent.ts`, `tokens.ts`, `truncate.ts`, `types.ts`.
- `src/logger.ts` — Structured logging boundary. `logDebug`/`logError` emit `console.log/error("[Metadator]", { event, ...fields })`.

## Boundaries enforced

- **SDK boundary**: Biome `noRestrictedImports` rule on `@anthropic-ai/sdk`, with overrides for `src/adapters/claude.ts` and `**/*.test.ts`. Test override is required because tests use `mock.module(...)` and dynamic `await import(...)` to grab mocked SDK error constructors.
- **Schema versioning**: every saved `data.json` carries `schemaVersion`. Migrations live in `MIGRATIONS` map keyed by target version. Bumping `CURRENT_SCHEMA_VERSION` without adding a migration entry throws at load time.

## Tech stack gotchas

- `dangerouslyAllowBrowser: true` is set on the Anthropic client because Obsidian's renderer is Electron — tolerable but flagged.
- `main.js` is committed (Obsidian distributes the bundle).
- Externals during build: `obsidian`, `electron`.
- Tests use Bun native runner. `src/test-preload.ts` mocks the Obsidian API globally.
- Tests mocking the Anthropic SDK use `mock.module("@anthropic-ai/sdk", ...)` _plus_ dynamic `await import("@anthropic-ai/sdk")` to retrieve mocked error constructors for retry tests.

## Event vocabulary (debug logs)

`claude_request_start` / `claude_request_completed` / `claude_request_failed` (per call), `claude_retry_scheduled` (bulk retry loop), `frontmatter_write_failed`, `generation_failed`. Per-call `requestId` (8 hex chars), file path joins attempts within a bulk retry.
