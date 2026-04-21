# Conventions

Rules that keep the merged skills auditable, attributable, and regeneratable.

## Provenance — mandatory per item

Every rule, recommendation, or code snippet in [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md) and [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md) MUST carry a provenance tag.

### Tag format

An HTML comment immediately preceding the item:

```markdown
<!-- provenance: source=<source-id> sha=<short-sha> section="<heading or anchor>" -->
```

- `source` — the `id` field from [`sources.yml`](sources.yml), e.g. `make-interfaces-feel-better`.
- `sha` — short (7-char) commit SHA the item was extracted from. Must match the pinned SHA in `sources.yml`.
- `section` — the heading, anchor, or snippet locator inside the source file. Quote it.

For items that appear in multiple sources (typical in `design-engineer-aligned`), list all of them space-separated:

```markdown
<!-- provenance: source=make-interfaces-feel-better sha=abc1234 section="Tabular numbers" | source=emil-design-eng sha=def5678 section="Numbers in UI" -->
```

### Example

```markdown
<!-- provenance: source=make-interfaces-feel-better sha=abc1234 section="Tabular numbers for dynamic values" -->
### Use tabular numerals for values that change

When a number updates frequently (timers, counters, prices), apply `font-variant-numeric: tabular-nums;` so digit widths don't shift during re-renders.
```

### What this buys us

- **Regeneration.** If `sources.yml` bumps a SHA, we can diff the old item against the new upstream section and know exactly what to re-review.
- **Legal attribution.** Every piece of derived content points at the original author and commit.
- **Removal.** When an author asks for takedown, a single `grep` finds every affected item.

## Conflict markers — mandatory in `design-engineer-full`

When an item in `design-engineer-full` resolves a conflict between sources, the provenance tag is followed by a resolution tag:

```markdown
<!-- provenance: source=A sha=... section="..." | source=B sha=... section="..." -->
<!-- resolution: id=<conflict-id> strategy=<strategy> -->
```

- `id` — matches an entry id in [`analysis/misalignment.md`](analysis/misalignment.md).
- `strategy` — one of the strategies defined in that file (e.g. `prefer-A`, `merge`, `scope-split`, `fork`).

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
