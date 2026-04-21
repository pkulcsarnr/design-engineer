# Conventions

Rules that keep the merged skills auditable, attributable, and regeneratable.

## Provenance and resolution tags

Every rule, recommendation, or code snippet in [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md) and [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md) MUST carry a provenance tag. Items in the `full` skill that resolve a conflict MUST additionally carry a resolution tag.

**The canonical regex, rules, and examples for both tags live in [`schemas/provenance.md`](schemas/provenance.md).** That file is the single source of truth; do not reproduce the regex here.

What the provenance tags buy us:

- **Regeneration.** When `sources.yml` bumps a SHA, we can diff the old item against the new upstream section and know exactly what to re-review.
- **Legal attribution.** Every piece of derived content points at the original author and commit.
- **Removal.** When an author asks for takedown, a single `grep` finds every affected item.
- **Self-verification.** [`prompts/validate-repo.md`](prompts/validate-repo.md) enforces the regex and cross-references against `sources.yml` and `analysis/misalignment.md`, catching violations before PR.

## File naming

- Source ids are **kebab-case**, stable, and never include author names to avoid confusion on re-attribution. Author is tracked in `sources.yml`.
- Skill folders under `skills/` are named `design-engineer-<variant>`; `<variant>` is lowercase, no other namespaces.
- Analysis files under `analysis/` are flat markdown until one grows past ~400 lines, at which point split by topic into `analysis/topics/<topic>.md`.

## Markdown style

- ATX headings (`#`), sentence case.
- Code fences always language-tagged.
- No emojis in skill output — they leak into agent-generated code.
- Line wrap: none. Prose wraps at the renderer.

## Licensing hygiene

- Every source in [`sources.yml`](sources.yml) MUST have a `license` field. If unknown, set `license: unknown` and do not extract content until resolved.
- The repo's own license ([`LICENSE`](LICENSE), when added) covers the aggregation, comparison notes, and merged structure — not the derived content, which stays under upstream licenses per item.
