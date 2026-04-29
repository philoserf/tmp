---
title: "Check authoritative source before alarming"
type: pattern
project: "global"
tags: [tool/git, topic/workflow]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Before reacting with alarm to unexpected state (branch deleted, file changed, remote missing, etc.), check the authoritative source first — `gh pr view`, `git branch -a`, the actual file. Agents have no visibility into user actions in other editors, GitHub operations, or anything that happens outside the session, so the instinct to treat surprises as problems is unreliable.

## Why

During a `/vc-sync` run, a PR merged while the sync was in progress. `git sweep` correctly deleted the local feature branch because its upstream was gone. The agent reported this as "unexpected branch deletion" and asked the user to investigate, rather than just running `gh pr view` first. The user pushed back: "you tried to be smart rather than executing /vc-sync as written" and "you are so often wrong about things that happen elsewhere."

## How to apply

When a tool produces surprising output — especially for git/remote/PR state — verify against the authoritative source before flagging it as a problem. Skills like `/vc-sync` are simple and correct by design; when their behavior looks wrong, the assumption is probably wrong, not the skill. Don't editorialize surprises into alarms.
