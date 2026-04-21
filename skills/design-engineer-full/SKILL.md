---
name: design-engineer-full
description: Comprehensive design engineering skill set merged from all tracked sources, deduplicated, with conflicts resolved or explicitly noted. Broader coverage than the aligned variant — includes contested material.
---

# Design Engineer — Full

> Status: **placeholder**. Content not yet derived from sources.

This skill contains the **union** of design engineering guidance across all tracked sources listed in the repo-level [README](../../README.md). Duplicates are merged, and where sources disagree the resolution is noted inline (with a link to [`../../analysis/misalignment.md`](../../analysis/misalignment.md) for the full reasoning).

See [`../../MOTIVATION.md`](../../MOTIVATION.md) for why this skill exists.

## Authoring rules

Every item MUST carry a provenance tag per [`../../CONVENTIONS.md`](../../CONVENTIONS.md). Items that resolve a conflict MUST additionally carry a `resolution` tag pointing at an entry in [`../../analysis/misalignment.md`](../../analysis/misalignment.md). Example:

```markdown
<!-- provenance: source=make-interfaces-feel-better sha=abc1234 section="Borders vs shadows" | source=emil-design-eng sha=def5678 section="Depth cues" -->
<!-- resolution: id=borders-vs-shadows strategy=scope-split -->
### Use shadows for elevation, borders for separation within the same plane
...
```

Items without provenance (and, where applicable, resolution) tags MUST NOT be merged.

## Skills

_TBD — to be populated from source analysis._

## Conflicts and resolutions

See [`../../analysis/misalignment.md`](../../analysis/misalignment.md) for the full taxonomy, per-conflict reasoning, and strategy definitions.

## Attribution

Derived from the sources listed in [`/README.md`](../../README.md) and machine-tracked in [`/sources.yml`](../../sources.yml). All credit to original authors; their licenses are preserved per-item via provenance tags.
