---
title: "Execute, don't editorialize"
type: pattern
project: "global"
tags: [topic/workflow]
created: 2026-04-29
updated: 2026-04-29
status: active
---

When asked to run a skill or command, run it. Don't speculate about whether it's the right time or whether preconditions are met — the skill itself handles that.

## Why

The user corrected the agent for assuming a PR hadn't been merged when asked to run `vc-sync`. The assumption was wrong and wasted time editorializing instead of executing.

## How to apply

If the user says "run X", run X. If there's actually a problem, the command will surface it. Don't pre-empt with assumptions about repo state.

Also applies to multi-step skills: when a skill says "after X appears, proceed to step N", start step N immediately — don't wait for additional user input or confirmation. The skill workflow is the instruction; follow it without pausing.
