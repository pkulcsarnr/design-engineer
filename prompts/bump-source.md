# Bump source SHA

## Purpose

Move tracked source to new SHA and update refs.

## Inputs

- `{{source_id}}`
- `{{new_sha}}`
- `{{diff_summary}}`

## Preconditions

- source exists
- new SHA resolves
- license unchanged

## Steps

1. read old SHA from [`../sources.yml`](../sources.yml)
2. diff old vs new upstream content
3. update touched items in `skills/`
4. update touched analysis entries
5. set new SHA + `last_reviewed` in `sources.yml`
6. log under `Unreleased` in [`../CHANGELOG.md`](../CHANGELOG.md)

If item meaning changed a lot, reclassify it. If removed upstream, remove it here too.

## Output

- `sources.yml`
- `skills/design-engineer-aligned/SKILL.md`
- `skills/design-engineer-full/SKILL.md`
- `analysis/*`
- `CHANGELOG.md`

Commit: `chore(sources): bump {{source_id}} {{old_sha_short}} -> {{new_sha_short}}`

## Post-checks

- run [`validate-repo.md`](validate-repo.md)
- no old short SHA left in `skills/`
