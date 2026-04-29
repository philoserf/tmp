---
title: "gh CLI: reply to a PR review comment"
type: reference
project: "global"
tags: [tool/git]
created: 2026-04-29
updated: 2026-04-29
status: active
---

To reply to a PR inline review comment via gh CLI:

```bash
gh api repos/<owner>/<repo>/pulls/<pr_number>/comments \
  -f body="<reply text>" \
  -F in_reply_to=<comment_id>
```

The `/repos/.../pulls/comments/{id}/replies` endpoint returns 404; the correct mechanism is the new-comment endpoint with `in_reply_to` referencing the parent comment ID.

To find comment IDs for a PR:

```bash
gh api repos/<owner>/<repo>/pulls/<pr>/comments --jq '.[] | "\(.id) \(.path):\(.line)"'
```

Used in [[2026-04-29-pr-review-reply-workflow]].
