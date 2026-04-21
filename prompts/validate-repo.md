# Validate the whole repo

## Purpose

Run a read-only audit that reports every violation of the schemas and conventions. Every other prompt requires this to pass before PR.

## Inputs

None.

## Preconditions

- Working tree is clean (or at least, everything you intend to check is on disk).
- Able to read YAML, JSON, and markdown.

## Procedure

Run every check below. For each failing check, emit one violation line: `VIOLATION <check-id>: <file>:<line-or-section> — <message>`. At the end, emit either `OK` (zero violations) or `FAIL: <n> violation(s)`.

### C1 — `sources.yml` conforms to schema

Load [`../sources.yml`](../sources.yml) and validate against [`../schemas/sources.schema.json`](../schemas/sources.schema.json). Report any schema violation.

### C2 — No duplicate source ids

In `../sources.yml`, every `id` is unique.

### C3 — README sources table matches `sources.yml`

Every `id` in `../sources.yml` has a corresponding row in the Sources table of [`../README.md`](../README.md), and vice versa. The Author and License columns match.

### C4 — `sources/README.md` has clone instructions for every source

Every `id` in `../sources.yml` has a `git clone` line in [`../sources/README.md`](../sources/README.md) using that id as the target folder name.

### C5 — Every merged-skill item has a valid provenance tag

For each item (heading or discrete recommendation) in `../skills/design-engineer-aligned/SKILL.md` and `../skills/design-engineer-full/SKILL.md`:

- The preceding line matches the provenance regex in [`../schemas/provenance.md`](../schemas/provenance.md).
- Every `source=` value is an id in `../sources.yml`.
- Every `sha=` value is the first 7 chars of the current `pinned_sha` for that source. (Exception: if the source's `pinned_sha` is `TBD`, the item must not be merged at all — report as a violation.)

### C6 — Resolution tags only in the full skill

Any `<!-- resolution: ... -->` tag in `../skills/design-engineer-aligned/SKILL.md` is a violation. Every item in `../skills/design-engineer-full/SKILL.md` that has a `resolution` tag must have its `id` present as an entry in [`../analysis/misalignment.md`](../analysis/misalignment.md), and the `strategy` must match the entry's recorded strategy.

### C7 — Aligned threshold respected

For each item in `../skills/design-engineer-aligned/SKILL.md`, count the distinct `source=` values in its provenance tag. That count must be ≥ `max(2, ceil(N * 2/3))` where `N` is the number of sources in `../sources.yml`. Violations list the under-threshold items.

### C8 — No `unknown`-licensed source contributes content

For each source in `../sources.yml` with `license: unknown`, no `source=<that-id>` appears in any provenance tag across `../skills/**/*.md`.

### C9 — Misalignment entries conform to template

Every entry in `../analysis/misalignment.md` under `## Entries` has the fields specified in [`../schemas/misalignment-entry.template.md`](../schemas/misalignment-entry.template.md): `Id`, `Type`, both source positions, `Resolution strategy`, `Rationale`, `Resolved in`.

### C10 — Eval cases conform to template

Every file in `../evals/cases/*.md` has the frontmatter and sections specified in [`../schemas/eval-case.template.md`](../schemas/eval-case.template.md).

### C11 — No orphan references

- Every `source=` in any tag is in `../sources.yml`.
- Every `resolution.id` is in `../analysis/misalignment.md`.
- Every `sources_probed` entry in an eval case is in `../sources.yml`.

### C12 — No `TBD` in released artifacts

Only allowed places for `TBD` strings: `sources.yml` (`pinned_sha`, `last_reviewed` only), `CHANGELOG.md` under `## Unreleased`, placeholder sections of `analysis/*.md` that are not yet populated, `## Draft: candidates from ...` sections in `analysis/alignment.md`. Any `TBD` in `../skills/**/*.md` is a violation.

### C13 — No emojis in skill output

No emoji codepoints in any `../skills/**/*.md` file (they leak into agent-generated code).

## Output contract

Files modified: none (this is read-only).

Emit a structured report with one line per violation and a final summary line. Example:

```
VIOLATION C5: skills/design-engineer-full/SKILL.md:42 — provenance tag references source 'foo' not in sources.yml
VIOLATION C11: evals/cases/tabular-nums.md — sources_probed includes 'bar' not in sources.yml
FAIL: 2 violation(s)
```

## Post-checks

None — this IS the post-check for every other prompt.
