# Agent guide

Read first.

## Repo

This repo tracks source skills in [`sources.yml`](sources.yml), compares them in [`analysis/alignment.md`](analysis/alignment.md) + [`analysis/misalignment.md`](analysis/misalignment.md), and ships 4 skills:

- [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md)
- [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md)
- [`skills/design-engineer-opinionated/SKILL.md`](skills/design-engineer-opinionated/SKILL.md)
- [`skills/design-engineer-extended/SKILL.md`](skills/design-engineer-extended/SKILL.md)

Why this exists: [`MOTIVATION.md`](MOTIVATION.md).

## Base rule

AI edits. Humans review. Use prompts, not freestyle.

## Must

1. Add provenance to every merged item.
2. Use only ids + SHAs from [`sources.yml`](sources.yml).
3. Classify every conflict.
4. `license: unknown` is allowed. Keep attribution.
5. Run [`prompts/validate-repo.md`](prompts/validate-repo.md) before PR.

## Must not

1. Write `skills/**/*.md` by hand.
2. Change pinned SHAs without `bump-source`.
3. Make eval files off-template.
4. Invent new conventions inside skill files.

## Flow

1. Read `AGENTS.md`.
2. Read task prompt in [`prompts/`](prompts/).
3. Read [`CONVENTIONS.md`](CONVENTIONS.md), relevant file in [`schemas/`](schemas/), and [`sources.yml`](sources.yml).
4. Edit.
5. Run `validate-repo`.

If docs conflict, stop and flag it.

## Tasks

| task | prompt |
|------|--------|
| add source | [`prompts/add-source.md`](prompts/add-source.md) |
| bump source | [`prompts/bump-source.md`](prompts/bump-source.md) |
| extract items | [`prompts/extract-items.md`](prompts/extract-items.md) |
| classify | [`prompts/classify-conflict.md`](prompts/classify-conflict.md) |
| resolve conflict | [`prompts/resolve-conflict.md`](prompts/resolve-conflict.md) |
| author opinionated skill | [`prompts/author-opinionated-skill.md`](prompts/author-opinionated-skill.md) |
| author eval | [`prompts/author-eval.md`](prompts/author-eval.md) |
| validate repo | [`prompts/validate-repo.md`](prompts/validate-repo.md) |
| cut release | [`prompts/cut-release.md`](prompts/cut-release.md) |

## Escalate to human

- unclear / bad license
- takedown request
- unclassifiable conflict
- validator error you can't fix
- upstream reverses old resolution

## Fast paths

- overview: [`README.md`](README.md)
- rules: [`CONVENTIONS.md`](CONVENTIONS.md)
- policy: [`GOVERNANCE.md`](GOVERNANCE.md)
- prompts: [`prompts/README.md`](prompts/README.md)
- schemas: [`schemas/README.md`](schemas/README.md)
