# Misalignment

Detailed, per-topic disagreements across the tracked sources, plus the resolution adopted in [`design-engineer-full`](../skills/design-engineer-full/SKILL.md). Each resolved conflict is referenced from the merged skill via a `resolution` tag (see [`../CONVENTIONS.md`](../CONVENTIONS.md)).

> Status: **placeholder**. Analysis not yet performed.

## Conflict taxonomy

Not every difference is a conflict. Before writing an entry, classify it.

| Type | Definition | Typical resolution |
|------|------------|--------------------|
| **contradiction** | Sources give directly opposing recommendations for the same situation. | `prefer-A` / `prefer-B` with rationale, or `fork` if neither dominates. |
| **scope-difference** | Sources agree conceptually but apply to different scopes (e.g. one covers buttons, the other covers surfaces). | `scope-split`: keep both, narrow each to its stated scope. |
| **emphasis-difference** | Same recommendation, but one treats it as critical and the other as optional. | `merge`: adopt the stronger framing, note the weaker source. |
| **framing-difference** | Same underlying advice, different vocabulary or rationale. | `merge`: one canonical phrasing, credit both. |
| **silence** (not a conflict) | One source addresses it, the other doesn't. | No entry needed. Item goes into `full` under the speaking source's provenance; does **not** qualify for `aligned`. |
| **version-drift** | Sources agreed historically but one has since updated. | `prefer-current`: adopt the newer source, record the old SHA in notes. |

## Resolution strategies (tag values)

Use these exact strings in `<!-- resolution: ... strategy=<value> -->` tags:

- `prefer-A` / `prefer-B` — adopt one source verbatim; the other is noted but not used.
- `merge` — combine non-contradictory pieces into a single item.
- `scope-split` — keep both, each narrowed to its stated scope.
- `fork` — present both options in the merged skill with a "choose one" note; used sparingly.
- `prefer-current` — pick the more recently updated source; requires recording both SHAs.
- `defer` — conflict noted but not resolved yet; item is excluded from `design-engineer-full` until decided.

## How to read this file

- **Id** — kebab-case, stable; referenced from provenance tags in the merged skills.
- **Topic** — the skill or concept being compared.
- **Type** — one of the taxonomy entries above.
- **Positions** — each source's stance, quoted or paraphrased with file+section pointer.
- **Resolution** — strategy + rationale.

## Entries

### `TBD`

| Field | Value |
|-------|-------|
| Id | `tbd` |
| Type | _TBD_ |
| Source A position | _TBD_ |
| Source B position | _TBD_ |
| Resolution strategy | _TBD_ |
| Rationale | _TBD_ |

---

Sources tracked in this repo are listed in the top-level [README](../README.md) and machine-tracked in [`/sources.yml`](../sources.yml).
