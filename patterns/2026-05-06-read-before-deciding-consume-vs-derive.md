---
title: "Read existing struct shapes before brainstorming consume-vs-derive"
type: pattern
project: "global"
tags: [topic/architecture, topic/workflow]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Pattern

During brainstorming, when a question arises like "should the new layer consume an existing struct or re-derive from source data?", **read the existing struct's builder code before deciding**. The decision often reverses once you see how much logic lives in the builder.

## Why

In one observed session, the brainstorm settled on "Markdown formatters read source data directly (don't go through existing structs)" with the rationale "existing structs are JSON-shaped." Q1 was approved. Then while writing the plan, reading `BuildSurveyForm` revealed it encodes ~200 lines of barycentre composite, HZCO source-row selection, and outer-system composite walk logic. The existing struct wasn't "JSON-shaped" — it was the natural intermediate representation for any rendering target. The Q1 decision had to be reversed mid-plan.

Catching this earlier (during brainstorming, before spec) would have saved one spec-revision cycle and one "stop, wait, this is wrong" moment.

## How to apply

When brainstorming raises a "consume vs re-derive" question:

1. Pause the brainstorm.
2. Read the existing builder function from start to end — note its line count and the kinds of transformations it does.
3. Resume brainstorming with that data.

Heuristic: if the builder is >50 lines and does any non-trivial flattening (composite rows, sorted aggregations, post-fill derivations), the struct is the right intermediate. Re-deriving means duplicating the builder.

If the builder is <20 lines and just copies fields, "re-derive" is fine and decoupling has marginal value.

## Related

- [[2026-04-29-prefer-durable-options]] — same family: prefer the option that's stable as the system evolves; reading the code before deciding is how you find the durable option.
