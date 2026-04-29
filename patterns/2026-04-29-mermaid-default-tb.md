---
title: "Default Mermaid flowcharts to top-to-bottom (TB) for narrow screens"
type: pattern
project: "philoserf/notes"
tags: [topic/diagrams, topic/mobile]
created: 2026-04-29
updated: 2026-04-29
status: active
---

## Pattern

Default to `flowchart TB` (top-to-bottom) for Mermaid diagrams in vault notes. Avoid `LR` unless the diagram is short (≤4 nodes) or horizontal orientation carries semantic meaning.

## Rationale

The vault is read primarily on iPhones and tablets. Horizontal layouts overflow narrow viewports; Mermaid does not auto-wrap layout at render time, so the choice of direction is a fixed mobile-readability decision.

## How to apply

- New diagrams: start with `TB`.
- Existing `LR` diagrams: if the user mentions mobile, narrow screens, or readability issues, suggest flipping to `TB` before other restructuring.
- Short diagrams (≤4 nodes) are the exception — `LR` is fine when it fits.
