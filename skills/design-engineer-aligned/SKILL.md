---
name: design-engineer-aligned
description: Consensus-only design-engineer skill. Use when building or reviewing UI and you only want guidance that every tracked source agrees on. Covers interruptibility, transition hygiene, GPU-friendly animation, press feedback, staggered entries, and the markdown Before/After review format.
---

# Design Engineer - Aligned

Only items that every tracked source agrees on. With two tracked sources, every item below is supported by both.

For the broader, merged skill with single-source items and resolved conflicts, see [`../design-engineer-full/SKILL.md`](../design-engineer-full/SKILL.md).

For authoring rules (provenance tags, merge policy), see [`../../CONVENTIONS.md`](../../CONVENTIONS.md) and [`../../schemas/provenance.md`](../../schemas/provenance.md).

## Animation

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Use CSS transitions over keyframes for interruptible UI" | source=make-interfaces-feel-better sha=3845620 section="Interruptible Animations" -->
### Prefer CSS transitions over keyframes for interruptible UI

For any interaction that may be re-triggered mid-flight (hover, toggle, open/close, list add/remove), use CSS transitions. Transitions retarget to the latest state and interpolate smoothly from the current position. Keyframes run on a fixed timeline and restart from zero, which reads as a jump when interrupted. Reserve keyframes for one-shot sequences (loading spinners, scripted intros).

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Review Checklist" | source=make-interfaces-feel-better sha=3845620 section="Never Use `transition: all`" -->
### Never use `transition: all` — list exact properties

`transition: all` (and Tailwind's bare `transition` shorthand) forces the browser to watch every property and produces unintended animations when unrelated properties change. Always name the properties you mean to animate, for example `transition-property: transform, opacity`. In Tailwind, use bracket syntax (`transition-[transform,opacity]`) or the scoped helper `transition-transform` (which already covers transform, translate, scale, rotate).

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Only animate transform and opacity" | source=make-interfaces-feel-better sha=3845620 section="Use `will-change` Sparingly" -->
### Only animate GPU-compositable properties

The GPU can composite `transform`, `opacity`, `filter`, and `clip-path` without going through layout or paint. Animating `width`, `height`, `top`, `left`, `padding`, `margin`, or colors forces layout and paint on every frame and causes dropped frames under load. Move all motion to transform and opacity; use filter and clip-path for visual effects.

## Press feedback

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Buttons must feel responsive" | source=make-interfaces-feel-better sha=3845620 section="Scale on Press" -->
### Add a subtle scale-down on press

Pressable elements should scale down slightly while the pointer is active, so the interface feels like it is listening. Use a value in the 0.96–0.97 range. Never go below 0.95 — anything smaller reads as exaggerated. Combine with a short `transition-property: scale` (or `transform`) so the release animates back smoothly.

```css
.button {
  transition-property: transform;
  transition-duration: 150ms;
  transition-timing-function: ease-out;
}
.button:active {
  transform: scale(0.96);
}
```

Provide an opt-out (e.g. a `static` prop) for contexts where the motion would distract.

## Entry animations

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Stagger Animations" | source=make-interfaces-feel-better sha=3845620 section="Split and Stagger Enter Animations" -->
### Stagger grouped entries instead of animating one container

When multiple elements enter together (a page hero, a list, a card's title + description + actions), split them into semantic units and stagger the entry. A cascade reads as alive; a single container slide reads as a slab. Keep the delay short so the full sequence still finishes quickly, and never block interaction while stagger is playing.

## Review output

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Review Format (Required)" | source=make-interfaces-feel-better sha=3845620 section="Review Output Format" -->
### Present UI reviews as a markdown Before/After table

When reviewing UI code, output findings as an actual markdown table with one row per change. Never use inline "Before:" / "After:" lines — those are unscannable. Each row should cite the specific property that changed when it isn't obvious from the snippet. If a principle was reviewed and nothing needed to change, omit that table — empty tables add noise.

| Before | After |
| --- | --- |
| `transition: all 300ms` | `transition: transform 200ms ease-out` |
| `<span>{count}</span>` on animated counter | `<span className="tabular-nums">{count}</span>` |

## Attribution

Derived from tracked sources in [`../../README.md`](../../README.md) and [`../../sources.yml`](../../sources.yml). Every item above carries a provenance tag pointing to its supporting sections in both sources at their pinned SHAs.
