# Classify a candidate against existing items

## Purpose

Given a candidate item (from [`extract-items.md`](extract-items.md)) and the current repo state, decide whether it is a new topic, an alignment with an existing topic, or a conflict — and route it accordingly.

## Inputs

- `{{candidate}}` — the full candidate record from the draft section in [`../analysis/alignment.md`](../analysis/alignment.md).
- `{{candidate_source_id}}` — which source it came from.

## Preconditions

- The candidate exists in a `## Draft: candidates from ...` section in `../analysis/alignment.md`.
- All existing canonical entries in `../analysis/alignment.md` and `../analysis/misalignment.md` have been read into context.

## Procedure

1. Find every existing canonical entry (in either analysis file) that shares topic or scope with `{{candidate}}`.
2. If none match:
   - Classify as **new-topic**.
   - If only `{{candidate_source_id}}` covers this topic, record it as a single-source item in `../analysis/alignment.md` under the topic's canonical section with one provenance citation. It does NOT qualify for `design-engineer-aligned` yet (threshold not met) but is eligible for `design-engineer-full` once merged into the skill.
3. If one or more existing entries match:
   - For each match, compare the candidate's guidance to the existing entry's guidance. Use the taxonomy in [`../analysis/misalignment.md`](../analysis/misalignment.md):
     - `silence` — not applicable here since both sides speak.
     - `framing-difference` — same advice, different words → promote to aligned.
     - `emphasis-difference` — same advice, different strength → promote to aligned; note weaker source.
     - `scope-difference` — adjacent but not equivalent → keep separate; both go into `full`.
     - `contradiction` — directly opposing → conflict; route to [`resolve-conflict.md`](resolve-conflict.md).
     - `version-drift` — historical agreement, diverged now → conflict; route to `resolve-conflict.md`.
4. For aligned cases:
   - Move the candidate out of the draft section.
   - Merge it into the canonical alignment entry by adding its source to the Sources field and expanding the Evidence field.
   - Re-evaluate whether the entry now meets the aligned threshold (see [`../GOVERNANCE.md`](../GOVERNANCE.md#aligned-threshold)). If yes, queue it for inclusion in `../skills/design-engineer-aligned/SKILL.md`.
5. For conflict cases:
   - Move the candidate out of the draft section.
   - Open a new entry in `../analysis/misalignment.md` with id `<kebab-case-topic>`, type set per the taxonomy, both positions recorded, resolution strategy set to `defer` until resolved.
   - Do NOT add to `../skills/design-engineer-full/SKILL.md` yet. That is [`resolve-conflict.md`](resolve-conflict.md)'s job.

## Output contract

Files modified:

- `analysis/alignment.md` — candidate moved out of draft into canonical entry; evidence/sources expanded.
- `analysis/misalignment.md` — new conflict entry if applicable.
- `skills/design-engineer-aligned/SKILL.md` — new or updated item only if the threshold is met.
- `skills/design-engineer-full/SKILL.md` — new item only if the candidate is non-contested (alignment or solo new-topic with known license).

Files NOT modified:

- `sources.yml`.
- `CHANGELOG.md` (wait until release cut).

Commit message: `analysis: classify candidate "<kebab-case-topic>" from {{candidate_source_id}}`.

## Post-checks

- No candidate remains in the draft section for this source.
- Every newly-canonical entry has complete provenance.
- Run [`validate-repo.md`](validate-repo.md).
