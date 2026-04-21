# Prompts

Reusable, parameterized prompts — one per standard operation on this repo.

Every mutation to the repo goes through one of these prompts. This is not convention, it is the design: prompts are the repo's "functions", and [`AGENTS.md`](../AGENTS.md) is the entry point that dispatches to them.

## How to use a prompt

1. Open the prompt file.
2. Read its **Inputs** section to gather what you need (source id, SHA, item text, etc.).
3. Fill the `{{variables}}` — do not paraphrase, do not skip.
4. Execute the **Procedure** step by step.
5. Validate your output against the prompt's **Output contract**.
6. Run [`validate-repo.md`](validate-repo.md) before proposing a PR.

## Prompt index

| Task | Prompt |
|------|--------|
| Add a new source to tracking | [`add-source.md`](add-source.md) |
| Bump an existing source to a new SHA | [`bump-source.md`](bump-source.md) |
| Extract candidate items from a source | [`extract-items.md`](extract-items.md) |
| Classify a pair of items as aligned / conflict | [`classify-conflict.md`](classify-conflict.md) |
| Resolve a classified conflict | [`resolve-conflict.md`](resolve-conflict.md) |
| Author an eval case | [`author-eval.md`](author-eval.md) |
| Validate the whole repo | [`validate-repo.md`](validate-repo.md) |
| Cut a release | [`cut-release.md`](cut-release.md) |

## Prompt file shape

Every prompt in this folder follows the same structure so agents can parse it deterministically:

```markdown
# <Task name>

## Purpose
One sentence.

## Inputs
- `{{var_name}}` — description, constraints.

## Preconditions
- What must be true before running.

## Procedure
1. Step.
2. Step.

## Output contract
- What files are created/modified.
- What the commit / PR description should contain.

## Post-checks
- Run `validate-repo.md`.
- Any task-specific checks.
```

When adding a new prompt, follow this shape. Prompts are themselves under [`CONVENTIONS.md`](../CONVENTIONS.md) — propose changes via PR.
