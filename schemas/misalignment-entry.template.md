# Misalignment entry template

Copy this block into [`../analysis/misalignment.md`](../analysis/misalignment.md) under `## Entries` when classifying a conflict. Replace every `{{placeholder}}`.

```markdown
### `{{kebab-case-id}}`

| Field | Value |
|-------|-------|
| Id | `{{kebab-case-id}}` |
| Type | {{contradiction | scope-difference | emphasis-difference | framing-difference | version-drift}} |
| Source A | `{{source_id_a}}` @ {{short_sha_a}} — section `"{{section_a}}"` |
| Source A position | {{1–3 sentences quoting or paraphrasing the upstream stance}} |
| Source B | `{{source_id_b}}` @ {{short_sha_b}} — section `"{{section_b}}"` |
| Source B position | {{1–3 sentences quoting or paraphrasing the upstream stance}} |
| Resolution strategy | {{prefer-A | prefer-B | merge | scope-split | fork | prefer-current | defer}} |
| Rationale | {{2–5 sentences explaining why this strategy is correct}} |
| Resolved in | {{design-engineer-full vX.Y.Z | unreleased | n/a while deferred}} |
```

## Rules

- `id` is unique across the file and kebab-case.
- `Type` must be one of the taxonomy values in [`../analysis/misalignment.md`](../analysis/misalignment.md).
- `source_id_a` and `source_id_b` must exist in [`../sources.yml`](../sources.yml).
- `short_sha_a` and `short_sha_b` are the first 7 chars of the current pinned SHAs.
- `Resolution strategy` is `defer` initially; only changes via the [`../prompts/resolve-conflict.md`](../prompts/resolve-conflict.md) task.
- `Resolved in` is `n/a while deferred` until resolution; becomes `unreleased` once the merged skill is updated, then the release version once cut.

Extend to 3+ sources by adding `Source C`, `Source C position`, etc. rows in the same style.
