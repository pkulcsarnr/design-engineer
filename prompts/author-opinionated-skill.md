# Author opinionated skill

## Purpose

Add or update an item in [`../skills/design-engineer-opinionated/SKILL.md`](../skills/design-engineer-opinionated/SKILL.md). Opinionated items are not sourced from [`../sources.yml`](../sources.yml); they are maintainer-authored or public-blog-inspired.

## Inputs

- `{{item_title}}`
- `{{basis}}`        - `public` or `author`
- `{{url}}`          - required when `basis=public`
- `{{section}}`      - required when `basis=public`, exact heading on the public page
- `{{reviewed}}`     - YYYY-MM-DD, today
- `{{rule_body}}`    - the rule in the maintainer's own words

## Preconditions

- item is not already in any tracked-source skill file
- if `basis=public`, URL is publicly reachable without login or paywall
- if `basis=public`, upstream license is permissive or unknown-but-public; all-rights-reserved repos are ineligible
- `rule_body` does not reproduce upstream prose; it is rewritten in repo voice

## Steps

1. read [`../schemas/opinion.md`](../schemas/opinion.md)
2. pick the matching regex form for `basis`
3. append the item under the correct section heading in [`../skills/design-engineer-opinionated/SKILL.md`](../skills/design-engineer-opinionated/SKILL.md) with:
   - opinion tag on the line above the item
   - a short `###` heading for the rule
   - rule body in one or two paragraphs, no emojis, no `transition: all`-style vagueness
4. if a related `design-engineer-full` item already expresses the same rule, stop - the full item wins; do not duplicate
5. log the change under `Unreleased` in [`../CHANGELOG.md`](../CHANGELOG.md)

## Output

Touch only:

- `skills/design-engineer-opinionated/SKILL.md`
- `CHANGELOG.md`

Do not touch `sources.yml`, `analysis/`, or `skills/design-engineer-aligned/`, `skills/design-engineer-full/`, `skills/design-engineer-extended/`.

Commit: `skills(opinionated): add {{item_title}}`

## Post-checks

- opinion tag matches regex in [`../schemas/opinion.md`](../schemas/opinion.md)
- no `provenance` or `source=` tags on the new item
- no verbatim copy from `url`
- run [`validate-repo.md`](validate-repo.md)
