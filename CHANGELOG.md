# Changelog

Skill changes. Semver per [`GOVERNANCE.md`](GOVERNANCE.md).

## Unreleased

### Added

- repo scaffold
- tracked sources: `make-interfaces-feel-better`, `emil-design-eng`
- first extraction pass on both tracked sources
- pinned SHAs: `make-interfaces-feel-better@3845620`, `emil-design-eng@ecf66bb` (reviewed 2026-04-21)
- six aligned items populated in `skills/design-engineer-aligned/SKILL.md` with multi-source provenance
- merged items populated in `skills/design-engineer-full/SKILL.md` with provenance per item and resolution tags on conflicts
- five classified conflicts in `analysis/misalignment.md`: `scale-on-press-value`, `stagger-timing`, `icon-swap-entry-scale`, `icon-swap-bounce`, `review-table-columns`
- opinion tag spec in `schemas/opinion.md` and authoring prompt in `prompts/author-opinionated-skill.md`
- new output `skills/design-engineer-opinionated/SKILL.md` with seven maintainer-authored UI tactics inspired by the public Refactoring UI post "7 Practical Tips for Cheating at Design" (reviewed 2026-04-28)
- new wrapper output `skills/design-engineer-extended/SKILL.md` applying `full` then `opinionated` with `full` winning on conflicts
- validator checks `C14`-`C17` for opinion tags and wrapper integrity

### Pending

- first eval cases in `evals/`
- first release cut

## Release template

```markdown
## design-engineer-aligned vX.Y.Z - YYYY-MM-DD

### Added
- <item> (source=<id> sha=<short-sha>)

### Changed
- <item>: <why>

### Removed
- <item>: <reason>

### Sources
- <source-id> <old> -> <new>
```
