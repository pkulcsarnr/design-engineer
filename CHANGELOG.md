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
