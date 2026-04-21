# Extract items

## Purpose

Pull candidate items from one source. Draft only. No merge yet.

## Inputs

- `{{source_id}}`
- `{{source_local_path}}`

## Preconditions

- source exists in [`../sources.yml`](../sources.yml)
- local checkout matches pinned SHA

## Steps

1. find upstream skill file
2. extract candidate items with:
   - `title`
   - `body`
   - `section`
   - `kind`
   - `scope`
3. append them as draft block in [`../analysis/alignment.md`](../analysis/alignment.md)
4. do not touch `skills/`

## Output

Touch only `analysis/alignment.md`.

Commit: `chore(analysis): extract candidates from {{source_id}}`

## Post-checks

- all 5 fields present
- `section` matches upstream heading text
- run [`validate-repo.md`](validate-repo.md)
