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

## Opinionated

`opinionated` is a separate output for maintainer-authored or public-blog-inspired rules. Rules:

- items never use `provenance`/`resolution` tags; they use `opinion` tags per [`schemas/opinion.md`](schemas/opinion.md)
- items do not count toward the `aligned` threshold
- items do not appear in [`analysis/alignment.md`](analysis/alignment.md) or [`analysis/misalignment.md`](analysis/misalignment.md)
- `basis=public` items must be rewritten in maintainer voice; no verbatim copying from the cited URL
- only sources with a permissive or unknown-but-public posture are eligible; all-rights-reserved repos are not eligible

## Extended

`extended` is a wrapper skill that instructs agents to apply `full` first, then `opinionated` where relevant. It contains no standalone rules; precedence and scope are documented inline.

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

## Takedown for opinionated items

If the author of a `basis=public` URL requests removal:

1. remove the item from `skills/design-engineer-opinionated/SKILL.md`
2. log in [`CHANGELOG.md`](CHANGELOG.md)

Target: ack 48h, PR 7d.
