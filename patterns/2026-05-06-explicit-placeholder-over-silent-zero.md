---
title: "Explicit placeholder rendering over silent zero values"
type: pattern
project: "global"
tags: [topic/architecture, topic/testing]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Pattern

When rendering structured data with optional/nullable sub-sections, never silently emit zero or empty values for missing data. Always render an explicit placeholder so the absence is unambiguous to a reader.

## Concrete examples

For nil pointer sub-fields in a 2-column table:

```text
### Atmosphere

| Field | Value |
|---|---|
| Status | (not generated) |
```

For zero/empty scalar values where the source treats zero as "not applicable":

```text
| Aab (A) | — | 1.836 | — | — | 1.419 |
                       ^^^^^^^ — em-dash, not 0.000
```

The em-dash matches the printed source's "—" convention for "not applicable."

## Why

Silent zeros are a documented anti-pattern that recurs across implementations. If a downstream calculation reads `0.000` and treats it as "data is zero" instead of "data is missing," the bug propagates silently. The most reliable cure is to make absence visually distinct from zero at the rendering boundary.

## How to apply

- Every nil-pointer guard renders an explicit `(not generated)` row, not a skipped section.
- Every zero scalar where zero means "not applicable" renders em-dash, not `0.000`.
- Every test of the rendering layer asserts the placeholder's presence, not just the populated case.

## Related

- [[2026-04-29-canon-contradiction-protocol]] — same family: surface divergences explicitly rather than paper over them.
