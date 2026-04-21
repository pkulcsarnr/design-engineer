# Bump a source to a new SHA

## Purpose

Update the pinned commit SHA of a tracked source and propagate the change to every provenance tag, analysis entry, and release note that cites it.

## Inputs

- `{{source_id}}` — the `id` in [`../sources.yml`](../sources.yml).
- `{{new_sha}}` — the new full 40-char commit SHA (short form is computed as the first 7 chars).
- `{{diff_summary}}` — a 1–3 sentence summary of what changed upstream between the current pinned SHA and `{{new_sha}}`.

## Preconditions

- `{{source_id}}` exists in [`../sources.yml`](../sources.yml).
- `{{new_sha}}` resolves in the upstream repo.
- The upstream `LICENSE` at `{{new_sha}}` is the same as at the currently pinned SHA. If it changed, escalate.

## Procedure

1. Read the current `pinned_sha` for `{{source_id}}` from [`../sources.yml`](../sources.yml). Call it `{{old_sha}}`.
2. Produce a structured diff of the upstream skill file(s) between `{{old_sha}}` and `{{new_sha}}`. For each changed section, note: heading, nature of change (content/rename/removal), whether it affects a currently-merged item.
3. For each affected item in `../skills/design-engineer-aligned/SKILL.md` and `../skills/design-engineer-full/SKILL.md`:
   - If content is unchanged: update only the `sha=` value in the provenance tag to the short form of `{{new_sha}}`.
   - If content changed non-substantively (typos, wording): update the item body and the `sha=` value. Flag for review in the PR description.
   - If content changed substantively: move the item to a draft block in [`../analysis/alignment.md`](../analysis/alignment.md) or [`../analysis/misalignment.md`](../analysis/misalignment.md) (whichever applies) and invoke [`classify-conflict.md`](classify-conflict.md) against the other sources.
   - If the upstream section was removed: remove the item; record in `CHANGELOG.md`.
4. For each affected analysis entry, update source-referenced SHAs.
5. Update [`../sources.yml`](../sources.yml): set `pinned_sha: {{new_sha}}` and `last_reviewed` to today.
6. Append a `### Changed` entry to `## Unreleased` in [`../CHANGELOG.md`](../CHANGELOG.md). Include `{{diff_summary}}` and a short-SHA pair (`{{old_sha_short}} → {{new_sha_short}}`).
7. If any merged-skill behavior changed, consider whether a minor or major version bump is warranted (see [`../GOVERNANCE.md`](../GOVERNANCE.md#versioning)).

## Output contract

Files modified:

- `sources.yml` — `pinned_sha` and `last_reviewed` for `{{source_id}}`.
- `skills/design-engineer-aligned/SKILL.md` — every provenance tag citing `{{source_id}}` updated.
- `skills/design-engineer-full/SKILL.md` — same.
- `analysis/alignment.md` / `analysis/misalignment.md` — any affected entries.
- `CHANGELOG.md` — one `### Changed` entry under Unreleased.

Commit message: `chore(sources): bump {{source_id}} {{old_sha_short}} → {{new_sha_short}}`.

## Post-checks

- Run [`validate-repo.md`](validate-repo.md).
- Confirm no provenance tag in `skills/` still references `{{old_sha_short}}`. Any that do are bugs — either the content was missed or it should have been removed.
