---
title: "Bash close-escape-open quoting in single-quoted awk"
type: context
project: "global"
tags: [lang/shell, tool/copilot, topic/debugging]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Inside a single-quoted bash string, `'\''` is the standard idiom for a literal single quote: close-quote, escape-single-quote, open-quote. POSIX-portable, works in all shells.

```bash
awk '
  gsub(/^["'\'']|["'\'']$/, "", val)
' file
```

The awk program receives `gsub(/^["']|["']$/, "", val)` — a valid awk regex that strips leading/trailing single OR double quotes.

## Why this matters

Shellcheck and `bash -n` both pass cleanly on this pattern. Pattern-matching AI reviewers (e.g. GitHub Copilot reviewer) sometimes flag it as a Bash syntax error because they see literal `'` mid-string and conclude the surrounding quote is terminated.

## How to apply

When a reviewer claims this is broken, refute with: `bash -n script.sh`, `shellcheck script.sh`, and a runtime test showing expected output. Don't change the code.
