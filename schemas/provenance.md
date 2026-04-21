# Provenance and resolution tag spec

Canonical shape for the HTML-comment tags that precede every item in [`../skills/design-engineer-aligned/SKILL.md`](../skills/design-engineer-aligned/SKILL.md) and [`../skills/design-engineer-full/SKILL.md`](../skills/design-engineer-full/SKILL.md).

This file is the single source of truth. [`../CONVENTIONS.md`](../CONVENTIONS.md) and every prompt reference this file; do not duplicate the regex elsewhere.

## Provenance tag

### Regex

```regex
^<!-- provenance: (source=[a-z0-9]+(?:-[a-z0-9]+)* sha=[0-9a-f]{7} section="[^"]+")( \| source=[a-z0-9]+(?:-[a-z0-9]+)* sha=[0-9a-f]{7} section="[^"]+")* -->$
```

### Rules

1. One per item, placed on the line immediately preceding the item's heading or content.
2. Every `source=` value MUST appear as an `id` in [`../sources.yml`](../sources.yml).
3. Every `sha=` value MUST be the first 7 chars of the `pinned_sha` currently recorded for that source in `../sources.yml`.
4. `section` is a literal quoted string — either the exact heading text or a stable anchor from the upstream file.
5. Multiple citations are separated by ` | ` (space-pipe-space). Order: alphabetical by source id.

### Examples

Single source:

```markdown
<!-- provenance: source=emil-design-eng sha=abc1234 section="Tabular numbers" -->
```

Multiple sources (alignment):

```markdown
<!-- provenance: source=emil-design-eng sha=def5678 section="Numbers in UI" | source=make-interfaces-feel-better sha=abc1234 section="Tabular numbers for dynamic values" -->
```

## Resolution tag

### Regex

```regex
^<!-- resolution: id=[a-z0-9]+(?:-[a-z0-9]+)* strategy=(prefer-A|prefer-B|merge|scope-split|fork|prefer-current|defer) -->$
```

### Rules

1. Present ONLY on items in `../skills/design-engineer-full/SKILL.md` (never in the aligned skill).
2. Placed on the line immediately after the provenance tag.
3. `id` MUST match an entry id in [`../analysis/misalignment.md`](../analysis/misalignment.md).
4. `strategy` MUST match the recorded strategy for that entry.

### Example

```markdown
<!-- provenance: source=emil-design-eng sha=def5678 section="Depth cues" | source=make-interfaces-feel-better sha=abc1234 section="Shadows instead of borders" -->
<!-- resolution: id=borders-vs-shadows strategy=scope-split -->
```

## Violations

The self-check in [`../prompts/validate-repo.md`](../prompts/validate-repo.md) reports a violation for any of:

- An item in `skills/**/*.md` with no provenance tag.
- A provenance tag that does not match the regex above.
- A `source=` value not in `sources.yml`.
- A `sha=` value that does not match the current pinned SHA for that source.
- A resolution tag outside `design-engineer-full/SKILL.md`.
- A resolution tag whose `id` is not present in `analysis/misalignment.md`.
- A resolution tag whose `strategy` differs from the strategy recorded for that id.
