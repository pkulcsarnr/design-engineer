# Author eval

## Purpose

Create one eval case.

## Inputs

- `{{case_id}}`
- `{{topic}}`
- `{{target_skill}}`
- `{{related_item_or_conflict}}`

## Preconditions

- template read
- case id unused
- target item exists if needed

## Steps

1. copy [`../schemas/eval-case.template.md`](../schemas/eval-case.template.md)
2. fill frontmatter
3. write prompt
4. write setup
5. write expected behaviors
6. write anti-behaviors
7. leave observed output + verdict empty

## Output

Create only `evals/cases/{{case_id}}.md`.

Commit: `evals: add case {{case_id}}`

## Post-checks

- file matches template
- expected behaviors are testable
- run [`validate-repo.md`](validate-repo.md)
