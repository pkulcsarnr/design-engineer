# Changelog

All notable changes to the merged skills are documented here. Both skills are versioned independently per [`GOVERNANCE.md`](GOVERNANCE.md).

Format loosely follows [Keep a Changelog](https://keepachangelog.com/). Dates are ISO 8601.

## Unreleased

### Added
- Repository scaffold: `skills/design-engineer-aligned/`, `skills/design-engineer-full/`, `analysis/alignment.md`, `analysis/misalignment.md`, [`sources.yml`](sources.yml), [`MOTIVATION.md`](MOTIVATION.md), [`CONVENTIONS.md`](CONVENTIONS.md), [`GOVERNANCE.md`](GOVERNANCE.md), [`evals/README.md`](evals/README.md).
- Two sources tracked in [`sources.yml`](sources.yml) (pinned SHAs pending): `make-interfaces-feel-better`, `emil-design-eng`.

### Pending
- First content extraction from upstream sources.
- First eval cases under `evals/cases/`.
- `emil-design-eng` license confirmation.

---

## Template for future releases

```markdown
## design-engineer-aligned vX.Y.Z — YYYY-MM-DD

### Added
- <item> (provenance: source=<id> sha=<short-sha>)

### Changed
- <item>: <what changed and why>

### Removed
- <item>: <reason — takedown, threshold drop, resolved conflict, etc.>

### Sources
- Bumped `<source-id>` pinned_sha <old> → <new>.
```
