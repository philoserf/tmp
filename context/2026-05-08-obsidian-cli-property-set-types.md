---
title: "Obsidian CLI property:set requires type= for non-text values"
type: context
project: "philoserf/notes"
tags: [tool/obsidian-cli, topic/frontmatter]
created: 2026-05-08
updated: 2026-05-08
status: active
---

`obsidian vault=notes property:set` accepts these args:

```text
name=<name>         (required)
value=<value>       (required)
type=text|list|number|checkbox|date|datetime
file=<name>
path=<path>
```

It defaults to `type=text`, which YAML-quotes everything. To get the right shape, match `type=` to the property:

| YAML target        | Use                                     |
| ------------------ | --------------------------------------- |
| `math: true`       | `value="true" type=checkbox`            |
| `tags: [a, b]`     | `value='["a", "b"]' type=list`          |
| `count: 5`         | `value="5" type=number`                 |
| `date: 2026-05-08` | `value="2026-05-08" type=date`          |
| `title: "..."`     | `value="..."` (default text is correct) |

## Failure modes

- Omitting `type=checkbox` for booleans writes `math: "true"` (quoted string). Hugo's math gate does not fire on quoted-string values — silent breakage.
- Omitting `type=list` for arrays writes `tags: "[a, b]"` (quoted string). This broke 830+ files during April 2026 tag consolidation.

## Discovery

`obsidian help property:set` shows the `type=` parameter. Run it before assuming the CLI cannot produce a given YAML shape — earlier sessions hit the boolean issue and worked around it via the Edit tool because the `type=checkbox` option was overlooked.
