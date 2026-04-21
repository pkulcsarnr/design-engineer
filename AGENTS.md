# Agent operating manual

Read this file **first** when you are an AI agent working on this repo. It is the task-oriented index into everything else.

## What this repo is (one paragraph)

An aggregator of design engineer agent-skills. It tracks upstream skills in [`sources.yml`](sources.yml), analyzes their agreements ([`analysis/alignment.md`](analysis/alignment.md)) and disagreements ([`analysis/misalignment.md`](analysis/misalignment.md)), and publishes two merged skills: [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md) (consensus only) and [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md) (everything, conflicts resolved in the open). Full rationale: [`MOTIVATION.md`](MOTIVATION.md).

## Operating assumption

All modifications to this repo are performed by AI agents through prompts. Humans review PRs; they do not hand-edit content. Everything in this repo is designed so an agent can operate it deterministically.

## Non-negotiables

You MUST:

1. **Tag provenance on every merged-skill item** per [`CONVENTIONS.md`](CONVENTIONS.md). No exceptions.
2. **Use only source ids and SHAs present in [`sources.yml`](sources.yml)**. Never invent them. If you need a new source, run the `add-source` task first.
3. **Classify every conflict** using the taxonomy in [`analysis/misalignment.md`](analysis/misalignment.md). Never merge contested items without a classified entry.
4. **Exclude items from sources whose license is `unknown`** per [`GOVERNANCE.md`](GOVERNANCE.md).
5. **Run [`prompts/validate-repo.md`](prompts/validate-repo.md) before proposing the PR.** If it reports violations, fix them; do not ship.

You MUST NOT:

1. Hand-author items in `skills/**/*.md` without running the `extract-items` → `classify` → (optional `resolve`) → merge sequence from [`prompts/`](prompts/).
2. Modify a pinned `sha` in [`sources.yml`](sources.yml) without using the `bump-source` task, which updates every affected provenance tag in the same PR.
3. Add an eval case outside the shape defined in [`schemas/eval-case.template.md`](schemas/eval-case.template.md).
4. Introduce new conventions in the merged skills; propose them to [`CONVENTIONS.md`](CONVENTIONS.md) first.

## Task catalog

Every standard operation has a prompt. Pick the matching task, open the prompt, fill parameters, run.

| Task | Prompt | Files mutated | Must pass before PR |
|------|--------|---------------|---------------------|
| Add a new source to tracking | [`prompts/add-source.md`](prompts/add-source.md) | `sources.yml`, `README.md` summary table, `sources/README.md` clone instructions | `validate-repo` |
| Bump an existing source to a new SHA | [`prompts/bump-source.md`](prompts/bump-source.md) | `sources.yml`, every `SKILL.md` provenance tag citing that source, `analysis/*`, `CHANGELOG.md` | `validate-repo` |
| Extract candidate items from a source | [`prompts/extract-items.md`](prompts/extract-items.md) | `analysis/alignment.md` OR `analysis/misalignment.md` (draft entries only) | n/a (advisory output) |
| Classify a pair of items as aligned/conflict | [`prompts/classify-conflict.md`](prompts/classify-conflict.md) | `analysis/alignment.md` or `analysis/misalignment.md` | `validate-repo` |
| Resolve a classified conflict | [`prompts/resolve-conflict.md`](prompts/resolve-conflict.md) | `analysis/misalignment.md`, `skills/design-engineer-full/SKILL.md` | `validate-repo` |
| Author an eval case | [`prompts/author-eval.md`](prompts/author-eval.md) | `evals/cases/<id>.md` | schema match |
| Validate the whole repo | [`prompts/validate-repo.md`](prompts/validate-repo.md) | none (read-only) | n/a |
| Cut a release | [`prompts/cut-release.md`](prompts/cut-release.md) | `CHANGELOG.md`, skill frontmatter version | `validate-repo` |

## Repo state at a glance

An agent should be able to answer each of these by reading one file:

| Question | File |
|----------|------|
| What sources are tracked and at which SHAs? | [`sources.yml`](sources.yml) |
| What merged items exist and where did each come from? | `skills/**/*.md` (provenance tags) |
| What conflicts have been classified? | [`analysis/misalignment.md`](analysis/misalignment.md) |
| What agreements have been recorded? | [`analysis/alignment.md`](analysis/alignment.md) |
| What has been released and when? | [`CHANGELOG.md`](CHANGELOG.md) |
| What are the hard rules? | [`CONVENTIONS.md`](CONVENTIONS.md), [`GOVERNANCE.md`](GOVERNANCE.md) |
| What prompts exist? | [`prompts/README.md`](prompts/README.md) |
| What schemas constrain structured files? | [`schemas/`](schemas/) |

## Session preamble

At the start of every session that will mutate this repo:

1. Read this file (`AGENTS.md`).
2. Read the prompt for your task from [`prompts/`](prompts/).
3. Read [`CONVENTIONS.md`](CONVENTIONS.md) and the relevant schema in [`schemas/`](schemas/).
4. Read [`sources.yml`](sources.yml) to know the current source state.
5. Only then touch files.

If any of steps 1–4 surface a contradiction with the task prompt, **stop and surface the contradiction**. Do not resolve it by guessing.

## When to surface a human

Escalate (open an issue, do not auto-PR) when:

- A source's license is unclear or appears incompatible.
- A takedown request is received.
- A conflict cannot be classified under the existing taxonomy.
- [`prompts/validate-repo.md`](prompts/validate-repo.md) reports violations you cannot mechanically fix.
- An upstream change reverses a previously-resolved conflict.

## Useful paths

- `README.md` — human-facing overview
- `MOTIVATION.md` — why this exists
- `CONVENTIONS.md` — authoring rules
- `GOVERNANCE.md` — policies
- `sources.yml` — source manifest
- `schemas/` — machine-checkable shapes
- `prompts/` — reusable operations
- `skills/` — deliverables
- `analysis/` — comparison work
- `evals/` — validation
- `sources/` — local-only workspace (gitignored)
