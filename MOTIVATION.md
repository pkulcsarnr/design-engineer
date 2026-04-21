# Motivation

## The problem

AI coding assistants (Claude Code, Codex, Cursor, etc.) can load "skills" — small prompt packs that inject opinionated guidance into every turn. The ecosystem is producing good ones for design engineering (see the [Sources section of the README](README.md#sources)).

Loading **multiple** skills at once has three failure modes:

1. **Context bloat.** Every skill costs tokens on every turn, whether the guidance is relevant or not.
2. **Silent conflicts.** Two skills recommend different shadow tokens, different animation durations, or contradictory advice on borders vs. shadows. The model resolves the conflict at inference time, unpredictably, per turn.
3. **No audit trail.** When the output looks off, you cannot tell which skill caused it, or whether the author of skill A would even agree with the behavior that the model produced when it was co-loaded with skill B.

## The thesis

> A merge decision made **once, explicitly, and reviewably** beats a merge decision made implicitly by the model on every turn.

This repo makes those decisions once, writes them down, and publishes the result as two skills:

- **`design-engineer-aligned`** — only what multiple sources agree on. Low risk, narrow scope.
- **`design-engineer-full`** — everything, with conflicts resolved in the open and the resolution logged.

The consumer picks one. They get a coherent, auditable skill instead of a stochastic mixture.

## Tradeoffs we accept

- **Staleness.** Upstream skills evolve; our merged skill lags. Mitigation: pinned SHAs in [`sources.yml`](sources.yml) and a review cadence. See [`GOVERNANCE.md`](GOVERNANCE.md).
- **Loss of author voice.** A merge abstracts away individual taste. Mitigation: the `aligned` variant is conservative; the `full` variant preserves contested items with provenance tags so the origin is always recoverable.
- **Attribution complexity.** MIT and similar licenses require preserving copyright notice. Mitigation: per-item provenance tags are mandatory (see [`CONVENTIONS.md`](CONVENTIONS.md)), plus the [Sources section of the README](README.md#sources) lists every upstream with license.

## When NOT to use this repo

Pick an individual upstream skill instead of the merged one if:

- **You trust one author's taste specifically.** If you want Emil Kowalski's exact opinions, install [`emil-design-eng`](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) directly. The merge loses some of that signal on purpose.
- **You are the upstream author.** You already have the coherent view we're trying to reconstruct.
- **Your design system is strongly opinionated.** A merged skill will recommend things your system already overrides; a narrower skill is lower-noise.

## Why not just publish a list of links?

A list of links gives a human a reading task. A skill gives an agent an instruction pack. This repo exists because the installable output is the deliverable — the analysis and comparison tables are the work that makes the output trustworthy, not the product itself.

## What success looks like

1. A consumer installs `design-engineer-aligned` and gets advice that no upstream author would object to.
2. A consumer installs `design-engineer-full` and can trace any piece of advice back to the specific upstream source, commit SHA, and (when relevant) the recorded conflict resolution.
3. When a new source is added, the diff to both merged skills is reviewable in a single PR.
4. When an upstream author asks for removal, it takes one PR to comply and the merged skill remains coherent.
