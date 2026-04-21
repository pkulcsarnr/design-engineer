# Governance

Policies that decide what goes into the merged skills, how changes happen, and how we respond to upstream authors.

## Aligned threshold

> **An item qualifies for `design-engineer-aligned` if it is endorsed — explicitly or by clear paraphrase — by at least `ceil(N * 2 / 3)` of the tracked sources, where `N` is the current source count, and by at least 2 sources regardless.**

Consequences of this rule:

| N sources | Threshold |
|-----------|-----------|
| 2         | 2 (unanimous)           |
| 3         | 2                       |
| 4         | 3                       |
| 5         | 4                       |
| 6         | 4                       |

- "Endorsed" means the source includes the item. Silence is not endorsement and is not opposition.
- If a source is in `contradiction` (per [`analysis/misalignment.md`](analysis/misalignment.md)) with an item, it does **not** count as endorsing it.
- When a new source is added, `aligned` is re-evaluated; items that no longer meet the threshold drop out, with a `CHANGELOG.md` entry explaining why.

## Full policy

`design-engineer-full` includes every item from every source, subject to:

- Every conflict is classified per [`analysis/misalignment.md`](analysis/misalignment.md) taxonomy.
- Every item has a provenance tag per [`CONVENTIONS.md`](CONVENTIONS.md).
- Items with `license: unknown` in [`sources.yml`](sources.yml) are **excluded** until the license is resolved.

## Adding a source

1. Open a PR that adds an entry to [`sources.yml`](sources.yml) with `license`, `pinned_sha`, and `last_reviewed`.
2. Do not extract content in the same PR. Merge the source-tracking PR first.
3. In a follow-up PR, update [`analysis/alignment.md`](analysis/alignment.md) and [`analysis/misalignment.md`](analysis/misalignment.md), then regenerate the merged skills.
4. Update [`CHANGELOG.md`](CHANGELOG.md) describing what moved into/out of `aligned` and what conflicts were added/resolved.

## Removing a source (takedown requests)

If an upstream author asks us to stop aggregating their skill:

1. Open a PR that removes their entry from `sources.yml`.
2. `grep` provenance tags referencing that `source=<id>` across `skills/` and `analysis/`.
3. Delete every item whose sole provenance was that source. For items that also cited other sources, strip the removed source from the tag and re-evaluate whether the item still meets the aligned threshold.
4. Update `CHANGELOG.md` with a takedown note (the author's name can be included or omitted per their preference).
5. Target timeline: acknowledge within 48 hours, ship the PR within 7 days.

## Bumping a source SHA

1. Diff upstream `HEAD` against `pinned_sha` in `sources.yml`.
2. For each changed section referenced by a provenance tag, update the merged skill and bump the tag's `sha`.
3. If the upstream change introduces or resolves a conflict, update `analysis/misalignment.md`.
4. Update `sources.yml` (`pinned_sha`, `last_reviewed`) in the same PR.
5. Add a `CHANGELOG.md` entry.

## Cadence

- **Source review:** every source's `last_reviewed` date should be within the last 90 days. A maintainer runs a bulk diff on a quarterly schedule.
- **Skill releases:** on any change to a merged `SKILL.md`, cut a tagged release `<skill>-vX.Y.Z` with the CHANGELOG section as release notes.

## Versioning

Both merged skills use semver, independently:

- **major** — breaking changes to skill behavior that a consumer would notice (removed recommendations, inverted advice).
- **minor** — new recommendations added, or a resolved conflict changes resolution strategy.
- **patch** — wording, typos, provenance tag updates, SHA bumps with no behavioral change.

## Disputes

If maintainers disagree on a resolution strategy for a conflict, the default is `defer` (see [`analysis/misalignment.md`](analysis/misalignment.md)). The item stays out of `design-engineer-full` until consensus is reached. No voting; no tie-breakers. Unresolved items are visible as open issues so upstream authors can weigh in.
