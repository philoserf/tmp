---
title: "Bun dotenv loading is asymmetric across invocation modes"
type: reference
project: "global"
tags: [tool/bun, lang/typescript, urgency/gotcha]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Bun's `.env` / `.env.local` auto-loading is NOT symmetric across invocation modes:

- **Sees the vars**: `bun <file.ts>`, `bun --eval "..."`, any native Bun runtime code reading `process.env` or `Bun.env`
- **Does NOT see them**: shell commands in `package.json` `"scripts"` entries invoked via `bun run <script>`. The shell that bun spawns gets an env without the dotenv values, so `"$VAR"` expands empty.

## Verification

```bash
# Proves the runtime loads the var:
bun --eval 'console.log(process.env.MY_VAR)'

# Proves the shell doesn't see it:
bun run --silent -- bash -c 'echo "from-shell: $MY_VAR"'
```

## Workaround

Make the script a native Bun TS file (e.g. `scripts/deploy.ts`) that reads `process.env` directly, and point the package.json script at it: `"deploy": "bun run deploy.ts"`. `Bun.$` inside the TS handles shell-style composition with correct quoting.

## Symptom in the wild

A `cp main.js manifest.json "$DEST"` in package.json silently copies files onto themselves because `$DEST` expands empty and macOS BSD cp resolves `""` destination to `.`. See [[2026-04-29-macos-cp-empty-destination]].

## Source

Originally captured on `philoserf/obsidian-metadator` (~2026-04-16). Migrated from per-project auto-memory to the agent memory vault on 2026-04-29.
