---
name: design-engineer-extended
description: Extended design-engineer skill. Wrapper that applies the merged tracked-source rules from `design-engineer-full` and then the maintainer-authored UI tactics from `design-engineer-opinionated`. Use when you want both the audited merged rules and the opinionated UI-tactics layer.
---

# Design Engineer - Extended

Wrapper skill. Contains no standalone rules. Apply the two underlying skills in order:

1. [`../design-engineer-full/SKILL.md`](../design-engineer-full/SKILL.md) - merged, tracked-source rules with provenance and resolved conflicts.
2. [`../design-engineer-opinionated/SKILL.md`](../design-engineer-opinionated/SKILL.md) - maintainer-authored UI tactics; not sourced from [`../../sources.yml`](../../sources.yml).

For the narrower, consensus-only output, see [`../design-engineer-aligned/SKILL.md`](../design-engineer-aligned/SKILL.md).

## Precedence

When the two layers disagree, the `full` rule wins. Opinionated items are supplemental defaults; they are overridden by any tracked-source item that addresses the same topic. This keeps audited guidance authoritative and uses the opinionated layer to fill gaps.

## Scope split

- Animation, easing, interruptibility, press feedback, entries and exits, icon-swap motion, popovers and tooltips, transforms, `clip-path`, gesture physics, surfaces, typography, performance, accessibility, component principles, review output, debugging - covered by `full`.
- Text hierarchy via weight and color, contrast on colored backgrounds, vertical-offset shadows, border restraint, small-icon sizing, accent color, and button hierarchy by importance versus semantics - covered by `opinionated`.

If a topic appears in both files, follow `full`. If a topic appears only in `opinionated`, follow `opinionated`.

## Using this skill

An agent loading `design-engineer-extended` should:

1. read `full` first and treat every item there as binding
2. read `opinionated` second and apply each item only where `full` is silent on the same topic
3. when writing a review, cite `full` items by their provenance tag and `opinionated` items by their opinion tag
4. never upgrade an opinionated item to tracked-source status without running [`../../prompts/add-source.md`](../../prompts/add-source.md) and [`../../prompts/extract-items.md`](../../prompts/extract-items.md)

## Attribution

Derived from tracked sources listed in [`../../README.md`](../../README.md) and [`../../sources.yml`](../../sources.yml) via `full`, plus maintainer-authored opinion items via `opinionated`. No content is added in this file; both underlying files retain their own tags.
