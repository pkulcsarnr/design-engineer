---
id: {{case_id}}
tags: [{{tag1}}{{, tag2}}]
sources_probed: [{{source_id_1}}{{, source_id_2}}]
---

## Prompt

{{prompt}}

## Setup

- Skill loaded: {{design-engineer-aligned | design-engineer-full | <source_id> | multi:<a>+<b>}}

## Expected behaviors

- [ ] {{expected behavior 1}}
- [ ] {{expected behavior 2}}

## Anti-behaviors

- [ ] {{bad output 1}}
- [ ] {{bad output 2}}

## Observed output

{{agent output}}

## Verdict

{{pass | partial | fail}} - {{why}}
