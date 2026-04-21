# Misalignment entry template

Copy into [`../analysis/misalignment.md`](../analysis/misalignment.md). Replace all `{{...}}`.

```markdown
### `{{kebab-case-id}}`

| Field | Value |
|-------|-------|
| Id | `{{kebab-case-id}}` |
| Type | {{contradiction | scope-difference | emphasis-difference | framing-difference | version-drift}} |
| Source A | `{{source_id_a}}` @ {{short_sha_a}} — section `"{{section_a}}"` |
| Source A position | {{source A stance}} |
| Source B | `{{source_id_b}}` @ {{short_sha_b}} — section `"{{section_b}}"` |
| Source B position | {{source B stance}} |
| Resolution strategy | {{prefer-A | prefer-B | merge | scope-split | fork | prefer-current | defer}} |
| Rationale | {{why this strategy}} |
| Resolved in | {{design-engineer-full vX.Y.Z | unreleased | n/a while deferred}} |
```

## Rules

- `id` unique, kebab-case
- `Type` must match taxonomy
- source ids must exist in [`../sources.yml`](../sources.yml)
- short SHAs = current pinned short SHAs
- start with `defer`
- `Resolved in` moves from `n/a while deferred` -> `unreleased` -> release version

For 3+ sources, add more source rows in same style.
