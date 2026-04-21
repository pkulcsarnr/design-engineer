# design-engineer

Merge design-engineer skills into 2 outputs:

- `aligned` = shared guidance only
- `full` = merged guidance + open conflict handling

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
- outputs: [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md), [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md)
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
| [`make-interfaces-feel-better`](https://github.com/jakubkrehel/make-interfaces-feel-better) | Jakub Krehel ([@jakubkrehel](https://github.com/jakubkrehel)) | [repo](https://github.com/jakubkrehel/make-interfaces-feel-better) | MIT | _TBD_ | _TBD_ |
| [`emil-design-eng`](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | Emil Kowalski ([@emilkowalski](https://github.com/emilkowalski)) | [repo](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | unknown (allowed) | _TBD_ | _TBD_ |

## Alignment

Shared items live in [`analysis/alignment.md`](analysis/alignment.md).

| topic | sources | note |
|-------|---------|------|
| _TBD_ | _TBD_   | _TBD_ |

## Misalignment

Conflicts + resolutions live in [`analysis/misalignment.md`](analysis/misalignment.md).

| topic | source A | source B | type |
|-------|----------|----------|------|
| _TBD_ | _TBD_    | _TBD_    | _TBD_ |

## Outputs

1. `aligned` -> safer, narrower, consensus-led. See [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md).
2. `full` -> broader, merged, conflict-aware. See [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md).

## Use

- copy `skills/design-engineer-aligned/` or `skills/design-engineer-full/`
- or load raw `SKILL.md`

No claim yet that `npx skills add <repo>` works.

## Removal

If you're source author and want removal, open issue or contact maintainer. SLA: ack in 48h, PR in 7d. See [`GOVERNANCE.md`](GOVERNANCE.md#remove-source).

## Contrib

- add source -> first update [`sources.yml`](sources.yml)
- extracted items need provenance tags
- keep attribution intact
