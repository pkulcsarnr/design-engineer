# sources/

Local-only source workspace. Gitignored except this file.

## Layout

```text
sources/
README.md
make-interfaces-feel-better/
emil-design-eng/
```

## Clone

```bash
git clone https://github.com/jakubkrehel/make-interfaces-feel-better.git sources/make-interfaces-feel-better

git clone https://github.com/emilkowalski/skill.git sources/_emilkowalski-skill
ln -s _emilkowalski-skill/skills/emil-design-eng sources/emil-design-eng
```

## Update

Source of truth: [`../sources.yml`](../sources.yml).

1. `git fetch`
2. check pinned SHA
3. diff vs upstream head
4. if adopting new SHA, update `sources.yml`, analysis, and `skills/`
5. update touched provenance tags

## Note

Upstream content stays under upstream license. Do not commit it here.
