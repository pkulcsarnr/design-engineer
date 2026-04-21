# Schemas

Machine-checkable shapes for every structured artifact in this repo.

These files exist so an agent can self-verify its output against an objective spec before opening a PR. [`../prompts/validate-repo.md`](../prompts/validate-repo.md) is the canonical consumer.

| File | Governs |
|------|---------|
| [`sources.schema.json`](sources.schema.json) | Shape of [`../sources.yml`](../sources.yml) |
| [`provenance.md`](provenance.md) | Regex + rules for `<!-- provenance: ... -->` and `<!-- resolution: ... -->` tags in `skills/**/*.md` |
| [`eval-case.template.md`](eval-case.template.md) | Shape of files in `../evals/cases/` |
| [`misalignment-entry.template.md`](misalignment-entry.template.md) | Shape of entries in [`../analysis/misalignment.md`](../analysis/misalignment.md) |

## Principles

- **One rule, one file.** If you find yourself checking the same shape in two places, consolidate here.
- **Templates, not examples.** Template files use `{{placeholders}}` and are intended to be copied. Examples live in prose docs.
- **Canonical regex.** The provenance tag regex lives here and only here; prompts and CONVENTIONS link to it.
