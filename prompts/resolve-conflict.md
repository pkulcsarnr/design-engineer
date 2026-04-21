# Resolve a classified conflict

## Purpose

Turn a conflict entry (status: `defer`) in [`../analysis/misalignment.md`](../analysis/misalignment.md) into a resolution and a corresponding item in [`../skills/design-engineer-full/SKILL.md`](../skills/design-engineer-full/SKILL.md).

## Inputs

- `{{conflict_id}}` — the `id` of the entry in `../analysis/misalignment.md`.
- `{{proposed_strategy}}` — one of the strategies defined in that file's taxonomy: `prefer-A`, `prefer-B`, `merge`, `scope-split`, `fork`, `prefer-current`, or `defer`.
- `{{rationale}}` — 2–5 sentences explaining why this strategy is correct for this conflict.

## Preconditions

- Entry `{{conflict_id}}` exists in `../analysis/misalignment.md` with `type` set and both positions recorded.
- `{{proposed_strategy}}` is defined in the "Resolution strategies" section of that file.
- Both involved sources have `license` set to a known permissive value in `../sources.yml`.

## Procedure

1. Update the entry for `{{conflict_id}}` in `../analysis/misalignment.md`:
   - Set `Resolution strategy` to `{{proposed_strategy}}`.
   - Write `Rationale` using `{{rationale}}`, expanded with any references to specific sections of the source positions.
2. Produce the merged-skill item text. Follow the strategy:
   - `prefer-A` / `prefer-B` — use the chosen source's wording directly (paraphrased source-agnostically).
   - `merge` — combine non-contradictory pieces into a single coherent item.
   - `scope-split` — produce two items, each narrowed to its stated scope; each gets its own provenance tag.
   - `fork` — produce one item that presents both options with a "choose one" instruction; rare — only when neither dominates.
   - `prefer-current` — use the newer source's wording; record both SHAs in the provenance tag.
3. Insert the produced item(s) into `../skills/design-engineer-full/SKILL.md` under the appropriate heading. Each item MUST carry:
   - A `<!-- provenance: ... -->` tag citing every involved source + SHA + section.
   - A `<!-- resolution: id={{conflict_id}} strategy={{proposed_strategy}} -->` tag on the next line.
4. If and only if `{{proposed_strategy}}` is `prefer-A`, `prefer-B`, or `merge` AND the item now meets the aligned threshold per [`../GOVERNANCE.md`](../GOVERNANCE.md#aligned-threshold), also insert a corresponding item into `../skills/design-engineer-aligned/SKILL.md`. Otherwise, the aligned skill is untouched.
5. Append a `### Changed` entry (if replacing a deferred item) or `### Added` entry (if first-time inclusion) to `## Unreleased` in `../CHANGELOG.md`, referencing `{{conflict_id}}`.

## Output contract

Files modified:

- `analysis/misalignment.md` — entry `{{conflict_id}}` resolved.
- `skills/design-engineer-full/SKILL.md` — new or updated item(s).
- `skills/design-engineer-aligned/SKILL.md` — updated only if the threshold is now met under a non-fork strategy.
- `CHANGELOG.md` — one entry under Unreleased.

Commit message: `analysis: resolve {{conflict_id}} via {{proposed_strategy}}`.

## Post-checks

- Every new item in `skills/**` has both a `provenance` tag and a `resolution` tag.
- The `resolution.id` references a real entry in `../analysis/misalignment.md`.
- Run [`validate-repo.md`](validate-repo.md).
