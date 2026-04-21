# Cut a release

## Purpose

Tag a new version of one or both merged skills and produce the release notes.

## Inputs

- `{{skill}}` — `design-engineer-aligned` or `design-engineer-full`.
- `{{bump}}` — `major`, `minor`, or `patch` per [`../GOVERNANCE.md`](../GOVERNANCE.md#versioning).
- `{{summary}}` — 1–3 sentences describing the release at a high level.

## Preconditions

- [`validate-repo.md`](validate-repo.md) passes with zero violations.
- `## Unreleased` in [`../CHANGELOG.md`](../CHANGELOG.md) is non-empty for `{{skill}}`.
- At least one eval case in `../evals/cases/` covers each new or changed top-level heading in the merged `SKILL.md`, and every resolved conflict has a dedicated eval case (per [`../evals/README.md`](../evals/README.md)).

## Procedure

1. Determine the new version. Read the current version from the frontmatter of `../skills/{{skill}}/SKILL.md` (field: `version`). If absent, start at `0.1.0`. Apply `{{bump}}` semver-style.
2. Update the `version` field in `../skills/{{skill}}/SKILL.md` frontmatter.
3. In `../CHANGELOG.md`, convert the `## Unreleased` section (entries that apply to `{{skill}}`) into a dated release header: `## {{skill}} v<new-version> — <today-YYYY-MM-DD>`. Keep the existing bullet structure (`### Added`, `### Changed`, `### Removed`, `### Sources`).
4. Reset the `## Unreleased` section with empty subsections, ready for the next cycle.
5. Write release notes on top of the existing CHANGELOG block using `{{summary}}` as the opening sentence.

## Output contract

Files modified:

- `skills/{{skill}}/SKILL.md` — `version` field bumped.
- `CHANGELOG.md` — Unreleased section consumed, dated release appended.

Commit message: `release: {{skill}} v<new-version>`.

Also: create an annotated git tag `<skill>-v<new-version>` pointing at the commit. The tag body is the new CHANGELOG section.

## Post-checks

- The `version` field matches the CHANGELOG header.
- Run [`validate-repo.md`](validate-repo.md) again.
- No items in the released skill have `TBD` placeholders.
