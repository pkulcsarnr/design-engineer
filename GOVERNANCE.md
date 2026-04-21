# Governance

## Aligned threshold

Rule:

`aligned` needs `max(2, ceil(N * 2 / 3))` supporting sources.

| N | need |
|---|------|
| 2 | 2 |
| 3 | 2 |
| 4 | 3 |
| 5 | 4 |
| 6 | 4 |

Notes:

- silence != support
- contradiction != support
- new source can push old item out of `aligned`

## Full

`full` can include all source items, but only if:

- conflict is classified
- provenance exists
- source is tracked in [`sources.yml`](sources.yml)

## Add source

1. add to [`sources.yml`](sources.yml)
2. merge source-only PR first
3. then update analysis + skills
4. note change in [`CHANGELOG.md`](CHANGELOG.md)

## Remove source

1. remove from `sources.yml`
2. remove its provenance refs
3. drop or re-check affected items
4. log in changelog

Target: ack 48h, PR 7d.

## Bump SHA

1. diff old vs new
2. update touched items + SHAs
3. update conflicts if needed
4. update `sources.yml`
5. log in changelog

## Cadence

- review sources every 90d
- release on any merged `SKILL.md` change

## Versioning

- major = breaking behavior change
- minor = new item / changed resolution
- patch = wording / tag / SHA only

## Disputes

If conflict resolution is unclear, use `defer`. Keep item out of `full` until settled.
