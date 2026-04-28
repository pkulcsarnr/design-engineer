# design-engineer

Merge design-engineer skills into 4 outputs:

- `aligned` = shared guidance only
- `full` = merged guidance + open conflict handling
- `opinionated` = maintainer-authored UI tactics, not merged from tracked sources
- `extended` = `full` + `opinionated`, with `full` winning on conflicts

AI-first repo: agents edit via [`prompts/`](prompts/). Humans review. Agents start with [`AGENTS.md`](AGENTS.md).

## Why

Many skills loaded together = more ctx, hidden conflicts, weak audit trail. Better: merge once, write it down, review it. See [`MOTIVATION.md`](MOTIVATION.md).

## Repo map

```text
README.md
AGENTS.md
MOTIVATION.md
CONVENTIONS.md
GOVERNANCE.md
CHANGELOG.md
sources.yml
prompts/
schemas/
sources/
skills/
analysis/
evals/
```

Quick links:

- agent guide: [`AGENTS.md`](AGENTS.md)
- prompts: [`prompts/README.md`](prompts/README.md)
- rules: [`CONVENTIONS.md`](CONVENTIONS.md)
- policy: [`GOVERNANCE.md`](GOVERNANCE.md)
- sources: [`sources.yml`](sources.yml)
- outputs: [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md), [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md), [`skills/design-engineer-opinionated/SKILL.md`](skills/design-engineer-opinionated/SKILL.md), [`skills/design-engineer-extended/SKILL.md`](skills/design-engineer-extended/SKILL.md)
- analysis: [`analysis/alignment.md`](analysis/alignment.md), [`analysis/misalignment.md`](analysis/misalignment.md)
- evals: [`evals/README.md`](evals/README.md)

## Principles

- full credit
- more sources welcome
- remove fast if author asks

## Sources

Source of truth: [`sources.yml`](sources.yml).

| id | author | link | license | sha | reviewed |
|----|--------|------|---------|-----|----------|
| [`make-interfaces-feel-better`](https://github.com/jakubkrehel/make-interfaces-feel-better) | Jakub Krehel ([@jakubkrehel](https://github.com/jakubkrehel)) | [repo](https://github.com/jakubkrehel/make-interfaces-feel-better) | unknown (allowed) | `3845620` | 2026-04-21 |
| [`emil-design-eng`](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | Emil Kowalski ([@emilkowalski](https://github.com/emilkowalski)) | [repo](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | unknown (allowed) | `ecf66bb` | 2026-04-21 |

## Alignment

Shared items live in [`analysis/alignment.md`](analysis/alignment.md).

| topic | sources | note |
|-------|---------|------|
| Prefer CSS transitions over keyframes for interruptible UI | `emil-design-eng`, `make-interfaces-feel-better` | both scope to interactive state changes |
| Never use `transition: all` — list exact properties | `emil-design-eng`, `make-interfaces-feel-better` | both explicitly ban the shorthand |
| Only animate GPU-compositable properties (transform, opacity, filter, clip-path) | `emil-design-eng`, `make-interfaces-feel-better` | same property set, same rationale |
| Subtle scale-down on press (0.96–0.97) for tactile feedback | `emil-design-eng`, `make-interfaces-feel-better` | exact value differs; see misalignment |
| Split and stagger grouped entry animations | `emil-design-eng`, `make-interfaces-feel-better` | exact timing differs; see misalignment |
| Output UI reviews as a markdown Before/After table | `emil-design-eng`, `make-interfaces-feel-better` | column count differs; see misalignment |

## Misalignment

Conflicts + resolutions live in [`analysis/misalignment.md`](analysis/misalignment.md).

| topic | source A | source B | type |
|-------|----------|----------|------|
| `scale-on-press-value` | `emil-design-eng` (0.97, range 0.95–0.98) | `make-interfaces-feel-better` (0.96 exact) | emphasis-difference |
| `stagger-timing` | `emil-design-eng` (30–80ms per item) | `make-interfaces-feel-better` (~100ms per group) | emphasis-difference |
| `icon-swap-entry-scale` | `emil-design-eng` (never from scale(0); start ≥0.9) | `make-interfaces-feel-better` (icon swaps start at scale 0.25) | scope-difference |
| `icon-swap-bounce` | `emil-design-eng` (0.1–0.3 when used, else 0) | `make-interfaces-feel-better` (always 0 for icon swaps) | scope-difference |
| `review-table-columns` | `emil-design-eng` (Before / After / Why) | `make-interfaces-feel-better` (Before / After, grouped by principle) | emphasis-difference |

## Outputs

1. `aligned` -> safer, narrower, consensus-led. See [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md).
2. `full` -> broader, merged, conflict-aware. See [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md).
3. `opinionated` -> maintainer-authored UI tactics; not merged from tracked sources. See [`skills/design-engineer-opinionated/SKILL.md`](skills/design-engineer-opinionated/SKILL.md).
4. `extended` -> wrapper that applies `full` then `opinionated`, with `full` winning on conflicts. See [`skills/design-engineer-extended/SKILL.md`](skills/design-engineer-extended/SKILL.md).

## Use

- copy `skills/design-engineer-aligned/`, `skills/design-engineer-full/`, `skills/design-engineer-opinionated/`, or `skills/design-engineer-extended/`
- or load raw `SKILL.md`

No claim yet that `npx skills add <repo>` works.

## Removal

If you're source author and want removal, open issue or contact maintainer. SLA: ack in 48h, PR in 7d. See [`GOVERNANCE.md`](GOVERNANCE.md#remove-source).

## Contrib

- add source -> first update [`sources.yml`](sources.yml)
- extracted items need provenance tags
- opinionated items need opinion tags per [`schemas/opinion.md`](schemas/opinion.md); use [`prompts/author-opinionated-skill.md`](prompts/author-opinionated-skill.md)
- keep attribution intact
