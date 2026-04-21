# Extract candidate items from a source

## Purpose

Read a tracked upstream skill and produce a list of **candidate** items suitable for later classification. This prompt does not mutate `skills/**` — output goes into draft sections of the analysis files only.

## Inputs

- `{{source_id}}` — the `id` in [`../sources.yml`](../sources.yml).
- `{{source_local_path}}` — path under [`../sources/`](../sources/) where the source has been cloned (e.g. `sources/{{source_id}}`).

## Preconditions

- `{{source_id}}` is present in `../sources.yml` with a `license` that is not `unknown`.
- The checked-out working tree at `{{source_local_path}}` is at the pinned SHA from `../sources.yml`. If not, check it out first.

## Procedure

1. Identify the SKILL-bearing file(s) in `{{source_local_path}}` (typically `SKILL.md` or `skills/<name>/SKILL.md`).
2. For each substantive recommendation in the source, extract a candidate item with these fields:
   - `title` — imperative short title ("Use tabular numerals for dynamic values").
   - `body` — minimum-necessary body, paraphrased source-agnostically but faithful.
   - `section` — the heading or anchor in the upstream file (will feed the provenance tag).
   - `kind` — one of: `rule`, `recommendation`, `pattern`, `example`, `anti-pattern`.
   - `scope` — e.g. `typography`, `animation`, `elevation`, `forms`. Keep to one or two.
3. Emit the list as a draft block at the bottom of [`../analysis/alignment.md`](../analysis/alignment.md) under a temporary heading `## Draft: candidates from {{source_id}} @ <short-sha>`. Each candidate is a bullet with the fields above.
4. Do NOT write items into `skills/**`. Do NOT merge with existing items yet.

## Output contract

Files modified:

- `analysis/alignment.md` — one new draft section appended.

Files NOT modified:

- Anything under `skills/`.
- `sources.yml`.
- `CHANGELOG.md` (drafts are not releasable).

Commit message: `chore(analysis): extract candidates from {{source_id}}`.

## Post-checks

- Each candidate has all five fields populated.
- `section` strings are exact quotes from the upstream headings, not paraphrases.
- Run [`validate-repo.md`](validate-repo.md) — it tolerates draft sections but will still check structural invariants.

## Next step

Run [`classify-conflict.md`](classify-conflict.md) for each candidate against existing items from other sources, then move promoted items out of the draft section into the canonical part of `alignment.md` / `misalignment.md` / the merged skills.
