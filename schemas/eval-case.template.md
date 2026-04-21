---
id: {{case_id}}
tags: [{{tag1}}{{, tag2}}]
sources_probed: [{{source_id_1}}{{, source_id_2}}]
---

## Prompt

{{The prompt given to the agent. Concrete, self-contained, reproducible.}}

## Setup

- Skill loaded: {{design-engineer-aligned | design-engineer-full | <source_id> | multi:<a>+<b>}}

## Expected behaviors

- [ ] {{specific, independently verifiable behavior 1}}
- [ ] {{specific, independently verifiable behavior 2}}

## Anti-behaviors

- [ ] {{specific wrong answer the skill should prevent 1}}
- [ ] {{specific wrong answer the skill should prevent 2}}

## Observed output

{{Paste the agent's response on first run. Leave empty until run.}}

## Verdict

{{pass | partial | fail}} — {{one-line rationale, or leave empty until run}}
