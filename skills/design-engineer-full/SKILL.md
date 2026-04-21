---
name: design-engineer-full
description: Merged design-engineer skill. All tracked-source items, deduped, with every conflict logged and resolved. Use when building, reviewing, or teaching UI polish — animation decisions, easing, press feedback, popovers, tooltips, surfaces, typography, accessibility, gesture physics, performance, and the markdown Before/After review format.
---

# Design Engineer - Full

Every item pulled from the tracked sources. Items with two-source support are aligned; items with one-source support are explicitly attributed; conflicts are resolved in place with a `resolution` tag that points at [`../../analysis/misalignment.md`](../../analysis/misalignment.md).

For the narrower, consensus-only skill, see [`../design-engineer-aligned/SKILL.md`](../design-engineer-aligned/SKILL.md).

For authoring rules, see [`../../CONVENTIONS.md`](../../CONVENTIONS.md) and [`../../schemas/provenance.md`](../../schemas/provenance.md).

## Mindset

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Taste is trained, not innate" -->
### Taste is trained, not innate

Good taste is not personal preference — it is a trained instinct, the ability to recognize what elevates a design. Build it by surrounding yourself with great work, reverse-engineering the interactions you admire, and practicing relentlessly.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Unseen details compound" -->
### Unseen details compound

Most details users never consciously notice. That is the point. When a feature behaves exactly as assumed, users proceed without a second thought. The aggregate of invisible correctness creates interfaces people love without knowing why.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Beauty is leverage" -->
### Beauty is leverage

People pick tools based on the full experience, not just functionality. Good defaults and good animations are real differentiators. Beauty is underutilized in software — use it.

## Animation decisions

<!-- provenance: source=emil-design-eng sha=ecf66bb section="1. Should this animate at all?" -->
### Decide first whether to animate at all

Ask how often users will see this animation. Actions triggered 100+ times per day (keyboard shortcuts, command-palette toggles) should not animate at all. Frequent interactions (hover effects, list navigation) should animate minimally or not at all. Occasional UI (modals, drawers, toasts) gets standard animation. Rare moments (onboarding, celebrations) can afford delight. Never animate keyboard-initiated actions — animation makes repeated actions feel slow and disconnected from the keypress.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="2. What is the purpose?" -->
### Every animation needs a clear purpose

Before writing animation code, name the job it does: spatial consistency (toasts enter and exit the same direction so swipe-to-dismiss feels intuitive), state indication (a morph shows that state changed), explanation (marketing), feedback (press scale confirms the press was heard), or preventing jarring changes (fade instead of pop). If the only answer is "it looks cool" and users see it often, don't animate.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Skip Animation on Page Load" -->
### Skip entry animation on initial page load

Use `initial={false}` on `AnimatePresence` so elements that are already in their default state on first render do not animate in. Icon swaps, toggles, tabs, and segmented controls should only animate on subsequent state changes. Do not use this on staggered page heroes or loading states where the initial animation is the point.

## Easing and duration

<!-- provenance: source=emil-design-eng sha=ecf66bb section="3. What easing should it use?" -->
### Pick easing by purpose

Entering or exiting: `ease-out` — starts fast, feels responsive. Moving or morphing on screen: `ease-in-out` — natural acceleration and deceleration. Hover / color change: `ease`. Constant motion (marquee, progress bar): `linear`. Default: `ease-out`. Never use `ease-in` for UI — it delays the initial movement at the exact moment the user is watching, which reads as sluggish even at the same duration.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="3. What easing should it use?" -->
### Use stronger custom easing curves, not the built-ins

The built-in CSS easings are too weak for polished UI. Prefer custom cubic-bezier curves:

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);        /* strong ease-out */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);    /* strong ease-in-out */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);     /* iOS-like drawer */
```

Don't author curves from scratch. Use tools like easing.dev or easings.co.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="4. How fast should it be?" -->
### Keep UI animations under 300ms

| Element | Duration |
| --- | --- |
| Button press feedback | 100–160ms |
| Tooltips, small popovers | 125–200ms |
| Dropdowns, selects | 150–250ms |
| Modals, drawers | 200–500ms |
| Marketing / explanatory | Can be longer |

A 180ms dropdown feels snappier than a 400ms one. A fast-spinning spinner makes loading feel faster at identical load times. Perception of speed is as important as actual speed.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Perceived performance" -->
### Instant tooltips after the first

Once a tooltip is open, hovering adjacent tooltips should open them instantly (no delay, no animation). The initial delay still prevents accidental activation, but subsequent hovers feel instantaneous.

## Interruptibility and interruption-safe motion

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Use CSS transitions over keyframes for interruptible UI" | source=make-interfaces-feel-better sha=3845620 section="Interruptible Animations" -->
### Prefer CSS transitions over keyframes for interactive UI

For any interaction that may be re-triggered mid-flight (hover, toggle, open/close, rapid toast add/remove), use CSS transitions. Transitions retarget to the latest state and interpolate smoothly from the current position; keyframes run on a fixed timeline and restart from zero. Reserve keyframes for one-shot sequences.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Interruptibility advantage" -->
### Springs maintain velocity on interruption

Springs settle based on physics, not a fixed duration, and they preserve velocity when interrupted. This makes them ideal for drag interactions with momentum, elements that should feel alive (like Apple's Dynamic Island), gestures that can be cancelled mid-motion, and decorative mouse-tracking effects.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Spring configuration" -->
### Prefer Apple-style spring configuration

Prefer the Apple-style form (`{ type: "spring", duration: 0.5, bounce: 0.2 }`) over traditional `{ mass, stiffness, damping }` — duration and bounce are easier to reason about. Keep bounce subtle (0.1–0.3) when used, and avoid bounce in most UI. Reserve bounce for drag-to-dismiss or playful moments.

## Entry animations

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Stagger Animations" | source=make-interfaces-feel-better sha=3845620 section="Split and Stagger Enter Animations" -->
<!-- resolution: id=stagger-timing strategy=merge -->
### Split entries into semantic chunks and stagger them

Do not animate a single container. Break a hero into `title` / `description` / `actions`; break a list into individual items. Stagger by roughly 30–80ms between list items and 50–100ms between semantic groups. For long titles, staggering by word at ~80ms also works. Combine `opacity`, `translateY`, and `filter: blur` for the per-element transform. Never block interaction while stagger is still playing.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Never animate from scale(0)" -->
### Never animate a general element from scale(0)

Nothing in the real world appears from nothing. General element entries (cards, toasts, modals, popovers) should start at `scale(0.9)` or higher combined with `opacity: 0`. Even a barely-visible initial scale reads as a balloon inflating rather than materializing out of void.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Animate enter states with @starting-style" -->
### Use `@starting-style` for CSS-only entry animations

Modern browsers expose `@starting-style` to animate elements from their mount values without JavaScript:

```css
.toast {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 400ms ease, transform 400ms ease;

  @starting-style {
    opacity: 0;
    transform: translateY(100%);
  }
}
```

Prefer this over the `useEffect` + `data-mounted` pattern when browser support allows; fall back to the legacy mount flag otherwise.

## Exit animations

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Subtle Exit Animations" -->
### Make exits subtle and shorter than entries

Exit animations should be softer than entries. The user's focus is moving to the next thing — do not fight for attention. Use a small fixed `translateY` (e.g. `-12px`) instead of the element's full height. Reserve full slide-outs for cases where the spatial context genuinely matters (a card returning to a list, a drawer closing). Keep the duration roughly half of the enter duration (e.g. 150ms exit vs 300ms enter).

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Asymmetric enter/exit timing" -->
### Slow presses, fast releases

Where the user is deliberating, motion can be slow (hold-to-delete: 2s linear). Where the system is responding, motion must be snappy (release: 200ms ease-out). This asymmetry applies well beyond press interactions — whenever the user is deciding, slower motion feels intentional; whenever the system is answering, faster feels alive.

## Icon swap animations

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Contextual Icon Animations" -->
<!-- resolution: id=icon-swap-entry-scale strategy=scope-split -->
### Use exact values for contextual icon swaps

When an icon swaps for another inside a button or control (play → pause, empty → liked, outline → filled), animate with exactly these values: `scale` from 0.25 to 1, `opacity` from 0 to 1, `filter: blur` from 4px to 0px. The scale:0.25 start is intentional for icon swaps — it reads as the icon arriving through focus. For general element entries, the `scale(0.9–0.95)` start above still applies.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Contextual Icon Animations" -->
<!-- resolution: id=icon-swap-bounce strategy=scope-split -->
### Spring bounce for icon swaps must be 0

If the project has `motion` / `framer-motion`, use `transition: { type: "spring", duration: 0.3, bounce: 0 }`. Bounce must always be `0` for icon swaps — any nonzero value feels wrong for a repeated micro-interaction. Bounce in the 0.1–0.3 range is reserved for decorative motion and gesture-driven interactions (drag-to-dismiss, playful accents), not icon swaps.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Contextual Icon Animations" -->
### CSS fallback: cross-fade with both icons in DOM

If no motion library is installed, do not add one just for icon transitions. Keep both icons in the DOM with one absolutely positioned over the other and cross-fade them with CSS transitions using `cubic-bezier(0.2, 0, 0, 1)`. Because neither icon unmounts, both enter and exit animate smoothly without `AnimatePresence`.

## Press feedback

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Buttons must feel responsive" | source=make-interfaces-feel-better sha=3845620 section="Scale on Press" -->
<!-- resolution: id=scale-on-press-value strategy=merge -->
### Scale-down on press (0.96–0.97)

Pressable elements should scale down slightly while `:active`. Use a value in the 0.96–0.97 band; default to `0.96`. Never go below `0.95` — anything smaller reads as exaggerated.

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

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Scale on Press" -->
### Provide a `static` opt-out for press scale

Not every button benefits from press scale — some contexts (inside a busy list, inside a table row, during a drag) make the motion feel noisy. Expose a `static` prop (or equivalent) on your button component that disables the scale class. Default on; opt out where needed.

## Popovers, tooltips, modals

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Make popovers origin-aware" -->
### Popovers must scale from their trigger, not from center

The default `transform-origin: center` is wrong for almost every popover. Popovers should scale in from the trigger position. Radix exposes `--radix-popover-content-transform-origin`; Base UI exposes `--transform-origin`. Modals are an exception — they are not anchored to a specific trigger, so keep `transform-origin: center`.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Tooltips: skip delay on subsequent hovers" -->
### Tooltips skip their delay (and animation) on subsequent hovers

The first tooltip delays before appearing so the user does not trigger one by accident. Once one is open, adjacent tooltips should open with zero delay and zero animation. This makes toolbars feel faster without losing the accidental-activation guard.

```css
.tooltip[data-instant] {
  transition-duration: 0ms;
}
```

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Use blur to mask imperfect transitions" -->
### Use blur to mask imperfect crossfades

When a crossfade between two states feels off despite trying different easings and durations, add `filter: blur(2px)` during the transition. Without blur, the eye sees two distinct objects overlapping; blur bridges the gap so the eye perceives a single smooth transformation. Keep blur under 20px — heavy blur is expensive, especially in Safari.

## CSS transform techniques

<!-- provenance: source=emil-design-eng sha=ecf66bb section="translateY with percentages" -->
### Use percentage values in `translate()` for self-relative motion

Percentage values in `translate()` are relative to the element's own size. `translateY(100%)` moves an element by exactly its own height, regardless of the actual dimensions. This is how Sonner positions toasts and how Vaul hides a drawer before animating in. Prefer percentages over hardcoded pixel offsets — they adapt to content and are less error-prone.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="scale() scales children too" -->
### `scale()` scales children — use it on purpose

Unlike `width` / `height`, `scale()` also scales the element's children (including text and icons) proportionally. When scaling a button on press, everything inside scales with it. This is a feature, not a bug.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="3D transforms for depth" -->
### Use 3D transforms for real depth

`rotateX()` / `rotateY()` combined with `transform-style: preserve-3d` produce real 3D effects in CSS — orbiting animations, coin flips, and parallax depth — without any JavaScript.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="transform-origin" -->
### Set `transform-origin` to match the trigger

Every transform has an anchor point. The default is the element center. Any time the element logically comes from a specific location (a popover from its trigger, a tooltip from its anchor, a detail view from a grid cell), set `transform-origin` to that location so the motion reads as spatially correct.

## clip-path as an animation tool

<!-- provenance: source=emil-design-eng sha=ecf66bb section="The inset shape" -->
### Animate `clip-path: inset()` for reveals and wipes

`clip-path: inset(top right bottom left)` defines a rectangular clipping region. Each value "eats" into the element from that side. Animating between `inset(0 100% 0 0)` (hidden) and `inset(0 0 0 0)` (visible) produces a clean left-to-right reveal. `clip-path` is GPU-composited, so these transitions stay smooth.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Tabs with perfect color transitions" -->
### Tabs: duplicate and clip for perfect color transitions

Duplicate the tab list; style the copy as "active" (different background and text color); clip the copy so only the active tab shows; animate the clip position on tab change. Crossfading individual colors can never match the sharpness of a clip transition, because the copy already has the final colors baked in.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Hold-to-delete pattern" -->
### Hold-to-delete: clip + asymmetric timing

Use `clip-path: inset(0 100% 0 0)` on a colored overlay. On `:active`, transition to `inset(0 0 0 0)` over 2s linear — the slow fill reads as "holding". On release, snap back in 200ms ease-out. Combine with `scale(0.96)` on the button for press feedback.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Image reveals on scroll" -->
### Reveal images on scroll with clip-path

Start with `clip-path: inset(0 0 100% 0)` (fully clipped from the bottom). Animate to `inset(0 0 0 0)` when the element enters the viewport using `IntersectionObserver` or `useInView` with `{ once: true, margin: "-100px" }`.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Comparison sliders" -->
### Before/after comparison sliders via clip-path

Overlay two images. Clip the top one with `clip-path: inset(0 50% 0 0)` and adjust the right inset based on drag position. No extra DOM elements needed, fully hardware-accelerated.

## Gesture and drag

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Momentum-based dismissal" -->
### Dismiss on velocity, not just distance

Don't force the user to drag past a threshold. Calculate velocity (`Math.abs(distance) / elapsedMs`) and dismiss when it exceeds ~0.11, regardless of distance. A quick flick should be enough.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Damping at boundaries" -->
### Damp drag past boundaries

When a user drags past the natural limit of a control (drawer up when already at top, list pulled past its end), do not stop dead — apply damping so each additional pixel moves the element less. Things in the real world slow before they stop.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Pointer capture for drag" -->
### Use pointer capture during drag

Once a drag starts, capture the pointer on the element so the drag continues even when the pointer leaves the element's bounds. Without pointer capture, fast flicks can "escape" the element mid-drag.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Multi-touch protection" -->
### Ignore extra touch points during drag

If a drag has started, ignore additional touches until the gesture ends. Without this, switching fingers mid-drag snaps the element to the new pointer position.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Friction instead of hard stops" -->
### Use friction, not invisible walls

Instead of preventing upward drag on a bottom drawer entirely, allow it with rising friction. Hard stops feel like bugs; friction feels like physics.

## Surfaces

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Concentric Border Radius" -->
### Concentric border radius on nested rounded surfaces

When nesting rounded elements, `outerRadius = innerRadius + padding`. Mismatched radii on nested elements is the single most common detail that makes interfaces feel off. If padding is larger than ~24px, the surfaces no longer read as nested — choose radii independently.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Optical Alignment" -->
### Align optically, not geometrically, when centering looks off

Some icons and glyphs have a geometric center that is not their visual center. Rules of thumb: for buttons with a text label and a trailing icon, use `icon-side padding = text-side padding - 2px`. For play triangles, shift right by ~2px. For asymmetric icons (stars, arrows), fix the SVG's viewBox or path directly when possible so no component-side margin hack is needed.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Shadows Instead of Borders" -->
### Prefer layered box-shadow over solid borders for elevation

For buttons, cards, and containers that use a border for depth, use a layered `box-shadow` instead. Shadows use transparency so they adapt to any background; solid borders don't. Light mode: three layers (ring + lift + ambient). Dark mode: a single white ring with low opacity — layered depth shadows are invisible on dark backgrounds.

```css
:root {
  --shadow-border:
    0px 0px 0px 1px rgba(0, 0, 0, 0.06),
    0px 1px 2px -1px rgba(0, 0, 0, 0.06),
    0px 2px 4px 0px rgba(0, 0, 0, 0.04);
}
```

Do not apply this to dividers (`border-t`, `border-b`, list separators, table cell boundaries) — those should stay as borders.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Image Outlines" -->
### Image outlines: pure black or pure white only

Add a `1px` outline with low opacity to images for consistent depth on surfaces. Light mode: `rgba(0, 0, 0, 0.1)`. Dark mode: `rgba(255, 255, 255, 0.1)`. Never use a tinted near-black or near-white (slate-900, zinc-900, `#0a0a0a`) — tinted outlines pick up the surrounding surface color and read as dirt on the image edge. Use `outline-offset: -1px` so the outline is inset and does not add to layout.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Minimum Hit Area" -->
### Minimum 40×40px hit area on every interactive element

Any interactive element needs at least a 40×40px hit area (44×44px per WCAG). When the visible control is smaller — a 20×20 checkbox, a small icon button — extend the hit area with an `::after` pseudo-element. Two interactive elements must never have overlapping hit areas; if extending one would overlap a neighbor, shrink it to the largest non-overlapping size.

## Typography

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Text Wrapping" -->
### Text wrapping: `balance` for headings, `pretty` for body

Use `text-wrap: balance` on headings and other short text blocks (6 lines or fewer in Chromium, 10 in Firefox) — it distributes text evenly across lines and prevents orphans. Use `text-wrap: pretty` as the default for short-to-medium body text (paragraphs, descriptions, captions, list items) — it fixes orphans without equalizing lines. Skip both on very long text (10+ lines) — the browser default is fine and you avoid unnecessary layout cost.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Font Smoothing (macOS)" -->
### Apply `-webkit-font-smoothing: antialiased` to the root

On macOS, text renders heavier than designers usually intend. Apply antialiased smoothing at the root (`html { -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }` or Tailwind's `antialiased` on `<html>`). Apply once at the root, never per element. Other platforms ignore these properties, so it's safe to apply universally.

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Tabular Numbers" -->
### `font-variant-numeric: tabular-nums` for any numbers that change

Counters, timers, prices, animated numbers, scoreboards, and numeric table columns all need `tabular-nums` to prevent layout shift as values change. Do not apply to static display numbers, phone numbers, zip codes, version strings, or decorative numerals — those keep proportional figures. Some fonts (including Inter) widen and recenter `1` in tabular mode; this is expected.

## Performance

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Only animate transform and opacity" | source=make-interfaces-feel-better sha=3845620 section="Use `will-change` Sparingly" -->
### Animate only GPU-compositable properties

The GPU can composite `transform`, `opacity`, `filter`, and `clip-path` without triggering layout or paint. Animating `width`, `height`, `top`, `left`, `padding`, `margin`, `background`, `border`, or `color` triggers layout and/or paint every frame and drops frames under load.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Review Checklist" | source=make-interfaces-feel-better sha=3845620 section="Never Use `transition: all`" -->
### Never use `transition: all` — list exact properties

Always name the properties you mean to transition. Tailwind's `transition` shorthand maps to `transition-property: all`; prefer bracket syntax (`transition-[transform,opacity]`) or the scoped helper `transition-transform` (covers `transform`, `translate`, `scale`, `rotate`).

<!-- provenance: source=make-interfaces-feel-better sha=3845620 section="Use `will-change` Sparingly" -->
### Use `will-change` sparingly

`will-change` pre-promotes an element to its own GPU compositing layer, avoiding a micro-stutter on the first animation frame. Restrict it to compositor-friendly properties (`transform`, `opacity`, `filter`, `clip-path`). Never use `will-change: all`. Never apply it to layout or paint properties (`background`, `padding`, `width`). Add it only when you can see first-frame stutter — Safari benefits most. Each extra compositing layer costs memory.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="CSS variables are inheritable" -->
### Don't drive animations through inherited CSS variables

Changing a CSS variable on a parent recalculates styles for every child. In a drawer or list with many items, updating `--swipe-amount` on the container triggers expensive recalc on each child. Update `transform` directly on the animated element instead.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Framer Motion hardware acceleration caveat" -->
### Framer Motion `x` / `y` shorthands are not hardware-accelerated

Framer Motion's shorthand props (`x`, `y`, `scale`) run through `requestAnimationFrame` on the main thread — they drop frames when the browser is simultaneously loading content or running scripts. For hardware acceleration, use the full transform string (`animate={{ transform: "translateX(100px)" }}`) or switch to pure CSS for predetermined animations.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="CSS animations beat JS under load" -->
### CSS animations beat JS animations under load

CSS animations run off the main thread. JS-driven animations (Framer Motion, rAF libraries) compete with script execution and page loads and drop frames when the main thread is busy. Use CSS for predetermined animations; reach for JS only when the animation must be dynamic or interruptible in ways CSS can't express.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Use WAAPI for programmatic CSS animations" -->
### WAAPI gives you JS control with CSS performance

The Web Animations API (`element.animate(...)`) runs on the compositor like CSS animations but exposes a JS handle for programmatic control. Use it for dynamic clip-path reveals, timeline-based sequences, or any scripted animation where you want CSS-level performance without a library.

## Accessibility

<!-- provenance: source=emil-design-eng sha=ecf66bb section="prefers-reduced-motion" -->
### Respect `prefers-reduced-motion` — reduce, don't remove

Reduced motion means fewer and gentler animations, not zero. Keep opacity and color transitions that aid comprehension. Remove transform-based motion and large translations.

```css
@media (prefers-reduced-motion: reduce) {
  .element {
    animation: fade 0.2s ease;
    /* no transform-based motion */
  }
}
```

In JS/React, use a `useReducedMotion()` hook to branch on translate values.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Touch device hover states" -->
### Gate hover animations behind `@media (hover: hover) and (pointer: fine)`

Touch devices trigger `:hover` on tap and hold it until the user taps elsewhere. Gating hover animations behind `@media (hover: hover) and (pointer: fine)` prevents false positives on mobile.

## Library and component principles

<!-- provenance: source=emil-design-eng sha=ecf66bb section="The Sonner Principles (Building Loved Components)" -->
### Optimize for developer experience, not options

Minimal setup wins. `<Toaster />` once, `toast()` from anywhere — no hooks, no context, no config object. The less friction to adopt, the more people use it. Default-good beats configurable-good.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="The Sonner Principles (Building Loved Components)" -->
### Good defaults matter more than options

Most users never customize. Ship beautiful out of the box. Default easing, timing, and visual design should already be the opinionated right answer.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="The Sonner Principles (Building Loved Components)" -->
### Handle edge cases invisibly

Pause toast timers when the tab is hidden. Fill gaps between stacked toasts with pseudo-elements to keep hover state. Capture pointer events during drag. Users never notice these — and that is exactly right.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="The Sonner Principles (Building Loved Components)" -->
### Build a real documentation site

Let people touch the product before they adopt it. Interactive examples with ready-to-use snippets lower the barrier far more than prose reference docs.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Cohesion matters" -->
### Match motion to the component's personality

A playful component can be bouncier. A professional dashboard should be crisp and fast. Pick duration and easing that fit the component's vibe — Sonner is slightly slower than typical UI and uses `ease` instead of `ease-out` because that cohesion with the design matters more than conforming to a generic UI norm.

## Review output

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Review Format (Required)" | source=make-interfaces-feel-better sha=3845620 section="Review Output Format" -->
<!-- resolution: id=review-table-columns strategy=merge -->
### Present reviews as a Before / After / Why markdown table, grouped by principle

When reviewing UI code, output findings as a real markdown table — never as inline "Before:" / "After:" lines. Use three columns: Before, After, Why. The Why column briefly justifies the change so the review also teaches. Group tables by principle with a heading above each, and keep each row focused on one diff. If a principle was reviewed and nothing needed changing, omit its table entirely — empty tables add noise.

#### Example

| Before | After | Why |
| --- | --- | --- |
| `transition: all 300ms` | `transition: transform 200ms ease-out` | Name exact properties; avoid `all`. |
| `transform: scale(0)` | `transform: scale(0.95); opacity: 0` | Nothing in the real world appears from nothing. |
| `ease-in` on dropdown | `ease-out` with custom curve | `ease-in` delays the movement the user is watching for. |

## Debugging

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Slow motion testing" -->
### Play animations in slow motion to catch timing bugs

Temporarily increase duration 2–5× or use the DevTools Animations panel to slow playback. Look for: two distinct states overlapping during a crossfade (add blur), abrupt starts or stops (adjust easing), wrong transform-origin, and out-of-sync coordinated properties.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Frame-by-frame inspection" -->
### Step through animations frame by frame in DevTools

The Chrome DevTools Animations panel lets you step frame by frame. This reveals timing mismatches between coordinated properties (opacity, transform, color) that are invisible at full speed.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Test on real devices" -->
### Test touch interactions on real hardware

For drawers, swipe gestures, and any touch-driven motion, test on a physical device. Connect your phone via USB, visit your local dev server by IP, and use Safari's remote devtools. Simulators can approximate layout but not gesture feel.

<!-- provenance: source=emil-design-eng sha=ecf66bb section="Review your work the next day" -->
### Review animations with fresh eyes the next day

You notice timing and easing imperfections the morning after that you missed while building. Re-review every non-trivial animation at least once after a break.

## Attribution

Derived from tracked sources in [`../../README.md`](../../README.md) and [`../../sources.yml`](../../sources.yml). Every item above carries a provenance tag pointing to its supporting section(s) at the pinned SHA; every resolution tag points to a classified conflict entry in [`../../analysis/misalignment.md`](../../analysis/misalignment.md).
