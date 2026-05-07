---
title: "obsidian-metadator 2.2.0 release"
type: journal
project: "philoserf/obsidian-metadator"
tags: [tool/claude-code, tool/git, topic/deployment]
created: 2026-04-30
updated: 2026-05-06
status: active
---

Cut 2.2.0 release. Used `/obsidian-release-check` → custom prep PR → `/obsidian-release` flow. Bundles the work from [[2026-04-29-obsidian-metadator-techdebt-sweep]]; project context at [[2026-04-29-obsidian-metadator-architecture]].

## Starting state

`/obsidian-release-check` flagged 4 FAILs:

- `Tag available`: 2.1.0 already tagged, 31 commits since.
- `Walkthrough current`: 20 mismatched blocks — substantial structural drift.
- `Deps current` + `Clean working tree`: `bun update --latest` had bumped `@biomejs/biome`, `@types/bun`, `typescript` patch versions and rebuilt `main.js`.

## Prep PR (#146)

Single atomic commit `chore: prep 2.2.0 release` containing:

- Version bump (`package.json` 2.1.0 → 2.2.0, then `npm_package_version=2.2.0 bun run version-bump.ts` to sync `manifest.json` + `versions.json`).
- New `## 2.2.0` CHANGELOG section (Added / Fixed / Internal) drawn from the 31 commits.
- Full `walkthrough.md` regen via `uvx showboat init/note/exec/verify` — surgical patch wasn't viable because `utils.ts` had been split into `src/content/` + `src/adapters/`, so embedded `sed` commands referenced gone files.
- Patch dep bumps + rebuilt `main.js`.

After commit, gate showed 13 PASS + 2 expected post-merge FAILs (clean tree / on default branch).

## Tag and release

After merge: synced main, tagged `2.2.0` on `da4b24a`, pushed. Release workflow attached `main.js` + `manifest.json` (no `styles.css` in this plugin). Release notes updated from CHANGELOG via `awk '/^## 2\.2\.0$/{flag=1; next} /^## /{flag=0} flag' CHANGELOG.md`.

Local `release/2.2.0` branch needed `-D` (squash-merge made `-d` fail "not fully merged").

## Lessons

See [[2026-04-30-walkthrough-regen-heuristic]] and [[2026-04-30-squash-merge-cleanup]].
