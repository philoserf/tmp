---
title: "Extract a CHANGELOG section with awk"
type: reference
project: "global"
tags: [lang/shell, tool/git, topic/deployment]
created: 2026-04-30
updated: 2026-04-30
status: active
---

For Keep-a-Changelog-style files (`## X.Y.Z` headings), extract one version section to feed to `gh release edit --notes`:

```sh
awk '/^## 2\.2\.0$/{flag=1; next} /^## /{flag=0} flag' CHANGELOG.md
```

- The `next` after `flag=1` skips the heading itself (release notes show the version in their title already).
- The second `/^## /` catches the next version heading and stops printing.
- Escape the dots in the version pattern (`2\.2\.0`) or they match any character.

## Use with `gh release edit`

```sh
BODY=$(awk '/^## 2\.2\.0$/{flag=1; next} /^## /{flag=0} flag' CHANGELOG.md)
gh release edit 2.2.0 --notes "$BODY"
```

Quote the variable expansion or multi-line content collapses.
