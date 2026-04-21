# Validate repo

## Purpose

Read-only audit. Must pass before PR.

## Inputs

None.

## Output format

One line per failure:

`VIOLATION <id>: <file>:<line-or-section> - <msg>`

Then:

- `OK`
- or `FAIL: <n> violation(s)`

## Checks

- `C1` `sources.yml` matches [`../schemas/sources.schema.json`](../schemas/sources.schema.json)
- `C2` no duplicate source ids
- `C3` README source table matches `sources.yml`
- `C4` every source has clone line in [`../sources/README.md`](../sources/README.md)
- `C5` every merged skill item has valid provenance tag
- `C6` resolution tags only appear in `full` and point to real conflict entry
- `C7` `aligned` items meet threshold
- `C8` no `unknown`-license source appears in merged content
- `C9` `misalignment.md` entries match template
- `C10` eval cases match template
- `C11` no orphan refs (`source=`, `resolution.id`, `sources_probed`)
- `C12` no bad `TBD` in released artifacts
- `C13` no emojis in `skills/**/*.md`

## Notes

- no file edits
- this prompt is post-check for all other prompts
