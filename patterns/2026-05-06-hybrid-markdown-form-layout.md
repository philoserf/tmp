---
title: "Hybrid Markdown layout for rendering structured forms"
type: pattern
project: "global"
tags: [topic/architecture]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Pattern

When rendering a printed form (IISS survey, government form, lab report, etc.) as Markdown, use a **hybrid layout**:

- **Real Markdown tables** for actually-tabular sections — one row per record (Stars, Objects, Subordinates, line items).
- **2-column `Field | Value` tables** for grouped per-field sections (Header, Orbit, Atmosphere — sections with 4–8 labeled scalars).
- **H3 sub-section headers** within each form's H2 for section grouping.

## Why this beats alternatives

Mirror-perfect (whitespace-aligned plain text):

- Whitespace alignment is brittle across Markdown renderers (terminal, GitHub, editor preview render differently).
- Loses table structure for downstream parsers.

Idiomatic Markdown (pure bullet/definition lists, no tables):

- Loses the form's structural cues. A "Header" or "Composition" section reads as prose, not as the labeled grid the source had.

Hybrid:

- Real tables render reliably across all targets.
- 2-column Field|Value tables compress 4–8 fields into a compact, scan-able block.
- H3 headers preserve section grouping. Reader can skim by heading.

## How to apply

```markdown
## IISS Class IV-P Survey — Form 0407F-IV PART P

### Header

| Field            | Value    |
| ---------------- | -------- |
| World            | Aab IV d |
| System Age (Gyr) | 6.336    |

### Orbit

| Field      | Value   |
| ---------- | ------- |
| AU         | 1.06    |
| Period (h) | 7050.00 |

### Subordinates

| Designation | Size | Diameter (km) | Period (h) |
| ----------- | ---- | ------------- | ---------- |
| Aab IV a    | 2    | 3200          | 28.50      |
| Aab IV d    | 5    | 8163          | 624.69     |
```

Use [[2026-05-06-explicit-placeholder-over-silent-zero]] for missing-value handling within the same layout.

## Project precedent

- `philoserf/world-builder` `cmd/wbh -format markdown` uses this layout for IISS Class 0/I, Class II/III, and Class IV-P forms.
