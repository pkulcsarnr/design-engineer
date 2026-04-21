# sources/

This folder is a **local-only workspace** for reviewing and diffing the original skills we aggregate from. It is gitignored (except for this README) so we never redistribute upstream content.

## Why it exists

To compare sources we need them side-by-side on disk. Clone each upstream repo into this folder using the exact folder names below so any tooling or analysis notes can rely on consistent paths.

## Expected layout

```
sources/
├── README.md                         # this file (committed)
├── make-interfaces-feel-better/      # git clone of jakubkrehel/make-interfaces-feel-better
└── emil-design-eng/                  # the emil-design-eng subtree from emilkowalski/skill
```

## Clone instructions

From the repo root:

```bash
# Jakub Krehel — Make Interfaces Feel Better
git clone https://github.com/jakubkrehel/make-interfaces-feel-better.git sources/make-interfaces-feel-better

# Emil Kowalski — emil-design-eng
# The skill lives inside a larger repo; clone the whole thing, then symlink or copy the subfolder.
git clone https://github.com/emilkowalski/skill.git sources/_emilkowalski-skill
ln -s _emilkowalski-skill/skills/emil-design-eng sources/emil-design-eng
```

## Updating

Sources are pinned in [`../sources.yml`](../sources.yml) (the single source of truth for commit SHAs). When refreshing:

1. `cd` into the source folder and `git fetch`.
2. Check out the SHA currently pinned in `../sources.yml` for that source to see what the merged skills were derived from.
3. Diff against `origin/main` (or the upstream default branch) to see what changed.
4. If adopting the new upstream: bump `pinned_sha` and `last_reviewed` in `../sources.yml`, then re-run comparisons and update `../skills/design-engineer-aligned/SKILL.md` and `../skills/design-engineer-full/SKILL.md` plus the analysis files.
5. Every touched provenance tag in the merged skills MUST reference the new short SHA.

## Attribution

All content inside this folder belongs to its original authors under their original licenses. Nothing in this folder is committed to this repository.
