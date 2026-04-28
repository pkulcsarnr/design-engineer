# Conventions

## Tags

Every merged item needs:

- provenance tag
- plus resolution tag in `full` if conflict was resolved

Spec lives in [`schemas/provenance.md`](schemas/provenance.md). Don't copy regex elsewhere.

Every opinionated item needs:

- opinion tag

Spec lives in [`schemas/opinion.md`](schemas/opinion.md). Opinion tags are only allowed in [`skills/design-engineer-opinionated/SKILL.md`](skills/design-engineer-opinionated/SKILL.md).

Merged items and opinionated items are mutually exclusive: never mix `provenance` and `opinion` tags on the same item.

Why tags:

- trace source
- update on SHA bump
- support takedown
- let validator self-check

## Names

- source ids: kebab-case, stable
- skill dirs: `design-engineer-<variant>`
- keep `analysis/` flat until it gets too big

## Markdown

- use `#` headings
- tag code fences
- no emojis in skill files
- no forced line wrap

## License

- every source needs `license`
- `license: unknown` => allowed
- repo license covers repo structure, not source-derived content
- opinionated items must be rewritten in maintainer voice; never copy prose verbatim from the `url` on an opinion tag
