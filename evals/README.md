# Evals

How we validate that the merged skills are worth installing.

> Status: **scaffold**. No evals have been run yet.

## Why evals exist in this repo

The thesis in [`../MOTIVATION.md`](../MOTIVATION.md) claims the merged skills are better than loading the upstreams individually. That claim is empirically checkable. This folder is where we check it.

A merged skill passes if, across a representative set of prompts:

1. It does not regress on behaviors the upstream authors consider core.
2. It does not emit contradictory guidance (resolved conflicts stay resolved).
3. It produces equal-or-better output than loading both upstreams simultaneously.

## Eval structure

Each eval is a plain-markdown file in `evals/cases/<case-id>.md` with this shape:

```markdown
---
id: <case-id>
tags: [<topic>, <topic>]
sources_probed: [<source-id>, <source-id>]
---

## Prompt

<The prompt given to the agent.>

## Setup

- Skill loaded: `design-engineer-aligned` | `design-engineer-full` | `<upstream-id>` | `multi:<a>+<b>`

## Expected behaviors

- [ ] <behavior>
- [ ] <behavior>

## Anti-behaviors (should NOT happen)

- [ ] <anti-behavior>

## Observed output

<Paste the agent's response.>

## Verdict

pass | partial | fail — <one-line rationale>
```

## Authoring and running evals

- **Authoring:** do not hand-write case files. Use [`../prompts/author-eval.md`](../prompts/author-eval.md), which copies from the canonical template at [`../schemas/eval-case.template.md`](../schemas/eval-case.template.md) and enforces the shape.
- **Running (manual):**
  1. Load the skill variant under test into your agent of choice.
  2. Paste the prompt from `cases/<id>.md`.
  3. Check observed behaviors against expected and anti-behaviors.
  4. Commit the updated case file with `observed output` and `verdict` filled in.

Automated eval runners are out of scope for v1 — manual runs are enough to catch gross regressions. The structured case shape is designed so a runner can be added later without reauthoring cases.

## Minimum eval coverage before tagging a skill release

Before cutting any version of `design-engineer-aligned` or `design-engineer-full`:

- At least one eval per top-level heading in the merged `SKILL.md`.
- At least one eval per resolved conflict in [`../analysis/misalignment.md`](../analysis/misalignment.md) — specifically probing that the resolution holds.
- At least one comparative eval that loads the merged skill vs. loading multiple upstreams at once, on a prompt likely to trigger conflicts.

## Cases

_TBD — add `cases/*.md` files as topics are extracted from sources._
