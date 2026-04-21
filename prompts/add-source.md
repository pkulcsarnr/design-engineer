# Add a new source

## Purpose

Register a new upstream skill as a tracked source **without** extracting any content from it yet. Content extraction happens in a follow-up PR via [`extract-items.md`](extract-items.md).

## Inputs

- `{{source_url}}` — canonical URL to the upstream skill (not the author's GitHub account).
- `{{proposed_id}}` — kebab-case identifier. Must be stable, must not contain the author's name, must be unique in [`../sources.yml`](../sources.yml).
- `{{author_name}}` — human-readable name of the upstream author.
- `{{author_github}}` — GitHub handle (no `@`).
- `{{license}}` — SPDX identifier (e.g. `MIT`, `Apache-2.0`, `CC-BY-4.0`) or `unknown`.
- `{{license_path}}` — path to the LICENSE file inside the upstream repo, or `null` if unknown.
- `{{pinned_sha}}` — full 40-char commit SHA from the upstream default branch as of today.
- `{{notes}}` — free-form; subpath of the source inside a multi-skill repo, caveats, etc.

## Preconditions

- `{{proposed_id}}` is not already in [`../sources.yml`](../sources.yml).
- `{{pinned_sha}}` resolves in the upstream repo (`git show {{pinned_sha}}` succeeds).
- The upstream license has been read. If it is not a permissive license (MIT, Apache-2.0, BSD, CC-BY) or unknown, escalate per [`../AGENTS.md`](../AGENTS.md) — do not proceed.

## Procedure

1. Append an entry to [`../sources.yml`](../sources.yml) under `sources:` with the fields from Inputs. Match the shape of existing entries exactly. Set `last_reviewed: <today-YYYY-MM-DD>`.
2. Add a row to the Sources table in [`../README.md`](../README.md). Link the `id` to the upstream `{{source_url}}`.
3. Add a `git clone` line for the new source to [`../sources/README.md`](../sources/README.md) under the existing clone block, using the folder name `{{proposed_id}}`.
4. Append an `### Added` entry under `## Unreleased` in [`../CHANGELOG.md`](../CHANGELOG.md) naming the new source id.

## Output contract

Files modified:

- `sources.yml` — one new entry appended.
- `README.md` — one new row in the Sources table.
- `sources/README.md` — one new clone command.
- `CHANGELOG.md` — one new entry under Unreleased.

Files NOT modified in this PR:

- Any file under `skills/`, `analysis/`, or `evals/`. Content work is a separate PR.

Commit message: `chore(sources): track {{proposed_id}}`.

## Post-checks

- Run [`validate-repo.md`](validate-repo.md).
- Confirm the license field is **not** `unknown` before the follow-up extraction PR. If `unknown`, open an issue asking the upstream author to confirm.
