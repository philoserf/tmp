---
title: "Showboat walkthrough: regenerate vs surgical patch"
type: reference
project: "global"
tags: [tool/claude-code, topic/deployment]
created: 2026-04-30
updated: 2026-04-30
status: active
---

When `uvx showboat verify walkthrough.md` reports mismatches, the trigger for full regeneration vs. surgical fix is whether the embedded `bash` commands themselves are still valid.

## Regenerate from scratch when

- Any `actual` block contains "no such file or directory", "not found", or similar — means the doc references files that have been deleted or renamed (e.g., a `utils.ts` split into multiple modules).
- ≥5 block mismatches — usually indicates structural drift, not single-spot edits.

## Patch with `verify --output` when

- Mismatches are pure output drift (version strings, test counts, line ranges) and every embedded `bash` command still resolves.

## Workflow

```sh
mv walkthrough.md walkthrough.md.bak
uvx showboat init walkthrough.md "Project Walkthrough"
uvx showboat note walkthrough.md <<'EOF'
## Section title
Commentary text...
EOF
uvx showboat exec walkthrough.md bash "sed -n '10,30p' src/foo.ts"
# ... alternate note and exec ...
uvx showboat verify walkthrough.md
rm walkthrough.md.bak
```

`note` accepts heredoc on stdin. `exec` runs the command and captures output as both a `bash` block (the command) and an `output` block. `verify` re-runs every block and diffs.

## Origin

The 2026-04-30 obsidian-metadator 2.2.0 release walkthrough had 20 mismatches with several `sed: src/utils.ts: No such file or directory` lines. Patching would have left the narrative referencing dead structure; regenerating produced a doc that matched the post-split layout.
