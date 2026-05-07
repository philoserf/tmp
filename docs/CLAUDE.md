# Docs

Bootstrap artifacts and out-of-band documents. **Not a type-folder.** Entries here do not follow the vault's frontmatter schema.

## What's here

- `superpowers/specs/` — original design specs from the vault's bootstrap.
- `superpowers/plans/` — original implementation plans from the vault's bootstrap.

## What NOT to do here

- **Don't add new vault entries to `docs/`.** New context, decisions, patterns, references, journals, and handoffs go in their type-folders, with `YYYY-MM-DD-slug.md` naming and the schema from `../CONVENTIONS.md`.
- **Don't rewrite the existing files.** They're period-accurate records of how the vault was bootstrapped on 2026-04-29. The vault has evolved since (`INDEX.md`, the `vault-audit` skill, more entries) but the originals stay as written.

## When to write here

Rarely. Only for genuine out-of-band documents that don't fit any type-folder — for example, a new spec for a vault-wide structural change, or a plan for a multi-session refactor that the type-folders can't host.
