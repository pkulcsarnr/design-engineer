# Cut release

## Purpose

Version a merged skill and write release notes.

## Inputs

- `{{skill}}`
- `{{bump}}`
- `{{summary}}`

## Preconditions

- validator passes
- `Unreleased` has entries
- needed evals exist

## Steps

1. compute next semver
2. bump `version` in `skills/{{skill}}/SKILL.md`
3. move matching `Unreleased` notes into dated section in [`../CHANGELOG.md`](../CHANGELOG.md)
4. reset `Unreleased`
5. create annotated git tag

## Output

- `skills/{{skill}}/SKILL.md`
- `CHANGELOG.md`

Commit: `release: {{skill}} v<new-version>`

## Post-checks

- version matches changelog
- run [`validate-repo.md`](validate-repo.md)
- no `TBD` in released skill
