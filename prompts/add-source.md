# Add source

## Purpose

Track new source. No extraction yet.

## Inputs

- `{{source_url}}`
- `{{proposed_id}}`
- `{{author_name}}`
- `{{author_github}}`
- `{{license}}`
- `{{license_path}}`
- `{{pinned_sha}}`
- `{{notes}}`

## Preconditions

- id not in [`../sources.yml`](../sources.yml)
- SHA resolves upstream
- license checked

## Steps

1. add entry to [`../sources.yml`](../sources.yml)
2. add source row to [`../README.md`](../README.md)
3. add clone line to [`../sources/README.md`](../sources/README.md)
4. note under `Unreleased` in [`../CHANGELOG.md`](../CHANGELOG.md)

## Output

Touch only:

- `sources.yml`
- `README.md`
- `sources/README.md`
- `CHANGELOG.md`

Do not touch `skills/`, `analysis/`, `evals/`.

Commit: `chore(sources): track {{proposed_id}}`

## Post-checks

- run [`validate-repo.md`](validate-repo.md)
- if license is `unknown`, open follow-up issue before extraction
