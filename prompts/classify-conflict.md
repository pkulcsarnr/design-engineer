# Classify item

## Purpose

Decide if draft item is:

- new topic
- aligned
- conflict

## Inputs

- `{{candidate}}`
- `{{candidate_source_id}}`

## Preconditions

- candidate exists in draft block
- canonical analysis has been read

## Steps

1. find matching canonical topics
2. if none -> add as new topic
3. if match -> compare using taxonomy in [`../analysis/misalignment.md`](../analysis/misalignment.md)
4. aligned -> merge into `alignment.md`
5. conflict -> create `misalignment.md` entry with `defer`
6. add to `skills/` only if rules allow

## Output

May touch:

- `analysis/alignment.md`
- `analysis/misalignment.md`
- `skills/design-engineer-aligned/SKILL.md`
- `skills/design-engineer-full/SKILL.md`

Do not touch `sources.yml` or `CHANGELOG.md`.

Commit: `analysis: classify candidate "<kebab-case-topic>" from {{candidate_source_id}}`

## Post-checks

- no leftover draft for this item
- canonical entries have provenance
- run [`validate-repo.md`](validate-repo.md)
