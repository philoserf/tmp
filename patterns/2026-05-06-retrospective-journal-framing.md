---
title: "Honest retrospective framing for journal backfills"
type: pattern
project: philoserf/notes
tags: [topic/journaling, tool/claude-code]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Pattern

When backfilling journal Review sections from past dates (because reviews were skipped or the conversation date was off), open each Review with an explicit retrospective marker:

```markdown
## Review

_Retrospective review written YYYY-MM-DD from limited evidence: <brief description of source material>._
```

## Why

Without the marker, real-time daily entries and post-hoc reconstructions look identical in the historical record. The marker:

1. Lets a future reader (or the user reading their own past work) distinguish lived-then-recorded from reconstructed-from-traces.
2. Disciplines the synthesis — naming "limited evidence" forces honesty about what's known vs. inferred.
3. Preserves the value of the backfill while keeping the artifact distinct.

## Companion practice

When tomorrow's-focus is set retrospectively, parenthetically note that the "tomorrow" being referenced is in the past:

```markdown
### Tomorrow's Focus

_(Tomorrow from 4/27's perspective was 4/28. This is retrospective; the actual 4/28 work is in [[2026-04-28]].)_

1. ...
```

## Source

Observed in a multi-day journal backfill session (4/27-4/30, 5/2-5/5) on philoserf/notes. The user accepted retrospective backfills as legitimate work product so long as they were framed honestly — "skip because it's late" was not the answer; "write it but mark it" was.

## Related

- [[2026-05-06-three-way-voice-filter]] — Drafts/Reference/delete decision tree from the same session
