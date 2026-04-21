# Evals

Check merged skills are worth using.

Status: scaffold.

## Pass bar

Merged skill should:

1. keep core upstream behavior
2. avoid unresolved contradictions
3. do at least as well as loading multiple upstreams together

## Case shape

See [`../schemas/eval-case.template.md`](../schemas/eval-case.template.md).

## Author

Use [`../prompts/author-eval.md`](../prompts/author-eval.md). Don't hand-write case files.

## Run

1. load skill
2. paste prompt
3. compare output vs expected / anti-behaviors
4. fill observed output + verdict

## Release minimum

- 1 eval per top-level skill section
- 1 eval per resolved conflict
- 1 compare run vs multi-skill loading

## Cases

_TBD_
