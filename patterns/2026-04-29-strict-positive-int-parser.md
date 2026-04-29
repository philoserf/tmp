---
title: "Strict positive-integer parser pattern"
type: pattern
project: "global"
tags: [lang/typescript, lang/javascript, topic/security]
created: 2026-04-29
updated: 2026-04-29
status: active
---

`Number.parseInt(value, 10)` is too permissive for input validation that promises "positive integer":

- `parseInt("1.5", 10) === 1` (silent truncation)
- `parseInt("100abc", 10) === 100` (prefix parsing)
- `parseInt("-1", 10) === -1` (no sign check)
- `parseInt("", 10) === NaN` and `parseInt(" ", 10) === NaN` (only NaN catches some)

When the UI tells the user "must be a positive integer", the parser should match that contract.

## The helper

```ts
export function parseStrictPositiveInt(value: string): number | null {
  const trimmed = value.trim();
  if (!/^\d+$/.test(trimmed)) return null;
  const n = Number(trimmed);
  return n > 0 ? n : null;
}
```

- `^\d+$` rejects floats, prefixes, signs, empty, whitespace.
- `> 0` rejects `"0"` (which the regex would accept).
- Returns `null` on rejection, not `NaN` or `0` — caller pattern-matches with `=== null`.

## Caller pattern

```ts
const parsed = parseStrictPositiveInt(value);
if (parsed === null) {
  new Notice("Field must be a positive integer");
  text.setValue(this.plugin.settings.field.toString());
  return;
}
this.plugin.settings.field = parsed;
await this.plugin.saveSettings();
```

## When to apply

Any UI text input where the field type is "positive integer" — token limits, file caps, retry counts, port numbers. Any place a `Number.parseInt` is feeding a setting that the UI promised would be sanitized.

## Source

Adopted in `obsidian-metadator/src/settingsTab.ts` after Copilot caught `Number.parseInt` accepting `"1.5"` → `1` for both `Content Token Limit` and `Max Bulk Files`. See [[2026-04-29-obsidian-metadator-techdebt-sweep]].
