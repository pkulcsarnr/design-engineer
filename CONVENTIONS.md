# Conventions

## Tags

Every merged item needs:

- provenance tag
- plus resolution tag in `full` if conflict was resolved

Spec lives in [`schemas/provenance.md`](schemas/provenance.md). Don't copy regex elsewhere.

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
- `license: unknown` => no extraction yet
- repo license covers repo structure, not source-derived content
