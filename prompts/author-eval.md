# Author an eval case

## Purpose

Produce a single eval case file under `../evals/cases/` that exercises a specific merged-skill behavior or a specific resolved conflict.

## Inputs

- `{{case_id}}` — kebab-case, unique within `../evals/cases/`. Describes the behavior under test (e.g. `tabular-nums-for-counter`).
- `{{topic}}` — short topic tag (e.g. `typography`, `animation`).
- `{{target_skill}}` — one of: `design-engineer-aligned`, `design-engineer-full`, a specific upstream `source_id`, or `multi:<a>+<b>` for a comparative run.
- `{{related_item_or_conflict}}` — the heading in the merged `SKILL.md` OR the `id` of a misalignment entry this case probes. At least one must be provided.

## Preconditions

- The eval case template at [`../schemas/eval-case.template.md`](../schemas/eval-case.template.md) has been read.
- `{{case_id}}.md` does not already exist under `../evals/cases/`.
- If `{{target_skill}}` references a skill variant, the referenced item exists in that variant.

## Procedure

1. Copy the template at `../schemas/eval-case.template.md` to `../evals/cases/{{case_id}}.md`.
2. Fill the frontmatter:
   - `id: {{case_id}}`
   - `tags: [{{topic}}]`
   - `sources_probed: [...]` — list every source whose item is relevant to this case.
3. Write the `## Prompt` section. The prompt should be concrete and self-contained; a tester must not need outside context.
4. Fill `## Setup`: the exact skill(s) loaded, matching `{{target_skill}}`.
5. Write `## Expected behaviors` as checkbox items, one behavior per line, each independently verifiable.
6. Write `## Anti-behaviors` — specific wrong answers the skill should prevent.
7. Leave `## Observed output` and `## Verdict` empty; they are filled on first run.

## Output contract

Files created:

- `evals/cases/{{case_id}}.md` — conforms to the template.

Files NOT modified:

- `skills/**`, `analysis/**`, `sources.yml`, `CHANGELOG.md`.

Commit message: `evals: add case {{case_id}}`.

## Post-checks

- The file validates against the shape described in `../schemas/eval-case.template.md`.
- Every expected-behavior line is specific enough that two reviewers would agree whether output passes.
- Run [`validate-repo.md`](validate-repo.md).
