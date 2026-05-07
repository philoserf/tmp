---
title: "Sysprompt currentDate field can be 23+ hours stale"
type: context
project: global
tags: [tool/claude-code, urgency/gotcha]
created: 2026-05-06
updated: 2026-05-06
status: active
---

## Gotcha

The session-start hook injects a `currentDate: YYYY-MM-DD` field into the sysprompt. This value can be hours-to-a-day stale relative to the actual system clock. Observed: sysprompt said `2026-04-30` while the real clock had been on `2026-05-01` for ~23 hours.

## Impact

If you trust `currentDate` for date-sensitive work (daily reviews, journal entries, time-bounded queries), you can produce artifacts dated wrong. In the observed case, four "real-time" daily reviews were actually retrospective backfills — the work stood once reframed, but the framing had to change.

## Fix

For any date-sensitive work, run `date "+%Y-%m-%d %A %H:%M %Z"` once at the start of the task. Treat sysprompt `currentDate` as a hint, not authority. The file system clock (or `date`) is ground truth.

## Corroborating signals you can read

- `ls -la <file>` mtime stamps in OS format (e.g. `May 1 19:48`)
- File `lastmod:` frontmatter values
- Most recent commit dates from `git log`

If any of these disagree with sysprompt `currentDate`, cross-check `date` immediately.

## Source

Observed in a journal-review session on 2026-05-06 (philoserf/notes vault). The user corrected with one line: "It has been 5/1 for 23 hours." Worth memorializing because the failure mode is silent — sysprompt assertion looks authoritative.
