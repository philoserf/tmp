---
title: "Markdown formatters consume existing form structs (philoserf/world-builder)"
type: decision
project: "philoserf/world-builder"
tags: [topic/architecture, lang/go]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Decision

The Markdown rendering layer for the IISS survey forms (Class 0/I, Class II/III, Class IV-P) consumes the existing `stars.SurveyForm` and `worlds.IISSClass23Form` structs directly. Class IV-P, which has no struct yet, reads from `*DetailedPlacement` and `stars.System` directly.

## Considered alternatives

### A. Independent re-derivation (rejected)

Markdown formatters read from `stars.System` / `worlds.SystemDetail` source data and re-derive the per-row Stars table, Objects table, and other flattened representations. Originally chosen during brainstorming with the rationale "existing structs are JSON-shaped, decoupling renderers is good."

**Why rejected:** `stars.BuildSurveyForm` encodes ~200 lines of non-trivial logic — barycentre composite rows (Aab/AB/Cab/ABC), HZCO source-row selection, the running outer-system composite walk. Re-implementing this for Markdown would duplicate it. Caught while writing the implementation plan, before any code was written.

### B. Refactor to introduce an intermediate "rows" type (rejected)

Extract a shared `(System) → IntermediateRows` builder, then `IntermediateRows → SurveyForm` (existing) and `IntermediateRows → MarkdownString` (new).

**Why rejected:** `BuildSurveyForm` already plays the role of "the builder" — `(System, Metadata) → SurveyForm`. The struct it produces is plain Go (native types, no JSON-specific encoding). Adding an intermediate type adds indirection without behavioral gain. The struct IS the seam.

### C. Consume existing structs (chosen)

Markdown formatters take `SurveyForm` / `IISSClass23Form` as input. Class IV-P (no struct) reads source data directly.

**Why chosen:** No duplication. The structs are plain Go types with native fields, not transport-encoded — they serve any rendering target equally well. Re-derivation would have been ~200 lines of duplicated logic to maintain in parallel.

## Trade-offs accepted

- The Markdown layer is downstream of `BuildSurveyForm` and `RenderIISSClass23`. If those builders change shape, the Markdown formatters update too. Acceptable — the structs and the formatters change together for the same reasons.
- Class IV-P remains asymmetric (reads source data, no struct). Refactoring `RenderIISSClass4P` to produce a struct is a deferred enhancement; would give JSON parity for Class IV-P. Not blocking.

## Related

- [[2026-05-06-read-before-deciding-consume-vs-derive]] — the general pattern this decision came from.
- See `docs/specs/2026-05-06-cmd-wbh-markdown-output-design.md` in the repo for the full design.
