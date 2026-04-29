---
title: "PR review-feedback workflow"
type: pattern
project: "global"
tags: [tool/git, tool/copilot, topic/workflow]
created: 2026-04-29
updated: 2026-04-29
status: active
---

When inline review comments arrive on a PR (Copilot or human reviewer), the expected workflow:

1. **Fetch and triage all comments.** For each one assign a verdict: false positive (with verification), real bug (cheap fix), description-only fix, or decline (with reason).
2. **Present triage with recommendation.** Don't act before the user reviews the assessment.
3. **Confirm completeness.** After the user approves the bulk, surface any remaining "your call" items explicitly.
4. **Act on approved items.** Apply fixes, push, edit PR body for description-only items.
5. **Reply inline on every comment** — including the ones that were addressed via commit or PR-body edit. The user said: "We need to respond to all comments." A summary comment is not enough.

## Why

Reviewers (and future readers) need to see how each finding was resolved against the comment that raised it, not buried in a commit message or top-level summary. Inline replies make the conversation auditable.

## How to apply

After pushing fixes, loop through every reviewer comment ID and post an inline reply describing what changed (or why it was declined). Reference the fix commit SHA in replies for "fixed" items. See [[2026-04-29-gh-pr-review-comment-reply]] for the API mechanism.
