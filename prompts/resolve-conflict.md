# Resolve conflict

## Purpose

Turn deferred conflict into:

- resolved `misalignment` entry
- `full` skill item
- maybe `aligned` item

## Inputs

- `{{conflict_id}}`
- `{{proposed_strategy}}`
- `{{rationale}}`

## Preconditions

- conflict exists
- strategy is valid
- involved licenses are allowed

## Steps

1. set strategy + rationale in [`../analysis/misalignment.md`](../analysis/misalignment.md)
2. write merged item for `full`
3. add provenance + resolution tags
4. if threshold is met and strategy allows, also update `aligned`
5. log in [`../CHANGELOG.md`](../CHANGELOG.md)

## Output

- `analysis/misalignment.md`
- `skills/design-engineer-full/SKILL.md`
- maybe `skills/design-engineer-aligned/SKILL.md`
- `CHANGELOG.md`

Commit: `analysis: resolve {{conflict_id}} via {{proposed_strategy}}`

## Post-checks

- new `skills/` items have required tags
- `resolution.id` exists in `misalignment.md`
- run [`validate-repo.md`](validate-repo.md)
