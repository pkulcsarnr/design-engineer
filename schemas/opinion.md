# Opinion spec

Source of truth for opinionated-item tags. Used only in `skills/design-engineer-opinionated/SKILL.md`. Do not copy regex elsewhere.

## Scope

`opinion` tags label items that are **not** derived from a tracked source in [`../sources.yml`](../sources.yml). They carry:

- `basis`: `public` (rewritten from a publicly visible URL) or `author` (maintainer-authored, no external basis)
- `url`: canonical public URL when `basis=public`; omitted when `basis=author`
- `section`: exact heading or stable anchor on the public page; omitted when `basis=author`
- `reviewed`: YYYY-MM-DD the maintainer last checked the URL or authored the item

## Regex

Public-basis form:

```regex
^<!-- opinion: basis=public url="[^"]+" section="[^"]+" reviewed=[0-9]{4}-[0-9]{2}-[0-9]{2} -->$
```

Author-basis form:

```regex
^<!-- opinion: basis=author reviewed=[0-9]{4}-[0-9]{2}-[0-9]{2} -->$
```

## Rules

1. one per item, line above item
2. only allowed in `skills/design-engineer-opinionated/SKILL.md`
3. never use `provenance` or `resolution` tags on opinion items
4. never use `source=` values from [`../sources.yml`](../sources.yml) inside an opinion item; opinion items are not counted as merged source items
5. rewrite public-basis items in the maintainer's own words; do not copy prose from the URL verbatim

## Examples

Public basis:

```markdown
<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Use color and weight to create hierarchy instead of size" reviewed=2026-04-28 -->
```

Author basis:

```markdown
<!-- opinion: basis=author reviewed=2026-04-28 -->
```

## Violations

Validator fails if:

- opinion item has no opinion tag
- tag regex fails
- opinion tag appears outside `skills/design-engineer-opinionated/SKILL.md`
- item carries both `opinion` and `provenance` tags
- `url` is missing when `basis=public`
- `reviewed` is not YYYY-MM-DD
