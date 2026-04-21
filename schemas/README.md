# Schemas

Machine-checkable shapes used by [`../prompts/validate-repo.md`](../prompts/validate-repo.md).

| file | use |
|------|-----|
| [`sources.schema.json`](sources.schema.json) | `sources.yml` |
| [`provenance.md`](provenance.md) | provenance + resolution tags |
| [`eval-case.template.md`](eval-case.template.md) | `evals/cases/*.md` |
| [`misalignment-entry.template.md`](misalignment-entry.template.md) | `analysis/misalignment.md` entries |

Rules:

- one rule, one file
- use templates, not prose examples
- keep canonical regex here only
