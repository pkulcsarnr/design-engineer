[//]: # (Sources are tracked in `../sources.yml`. Short SHAs used here must match pinned short SHAs.)

# Alignment

Shared items across sources. Two sources tracked; threshold = 2/2.

## Topics

### `interruptible-css-transitions`

| field | value |
|-------|-------|
| sources | `emil-design-eng`, `make-interfaces-feel-better` |
| statement | For interactive state changes that may be triggered rapidly (hover, toggle, open/close), prefer CSS transitions over keyframe animations. Transitions retarget mid-animation; keyframes restart from zero. |
| evidence | `emil-design-eng@ecf66bb` §"Use CSS transitions over keyframes for interruptible UI"; `make-interfaces-feel-better@3845620` §"Interruptible Animations" |

### `no-transition-all`

| field | value |
|-------|-------|
| sources | `emil-design-eng`, `make-interfaces-feel-better` |
| statement | Never use `transition: all`. Always list the exact properties that change. |
| evidence | `emil-design-eng@ecf66bb` §"Review Checklist" (`transition: all` row); `make-interfaces-feel-better@3845620` §"Never Use `transition: all`" |

### `animate-gpu-properties-only`

| field | value |
|-------|-------|
| sources | `emil-design-eng`, `make-interfaces-feel-better` |
| statement | Restrict animation to GPU-compositable properties (transform, opacity, filter, clip-path). Avoid animating layout or paint properties. |
| evidence | `emil-design-eng@ecf66bb` §"Only animate transform and opacity"; `make-interfaces-feel-better@3845620` §"Use `will-change` Sparingly" + performance.md Useful Properties table |

### `scale-on-press`

| field | value |
|-------|-------|
| sources | `emil-design-eng`, `make-interfaces-feel-better` |
| statement | Apply a subtle scale-down on press (0.96–0.97) to pressable elements for tactile feedback. Never go below 0.95. |
| evidence | `emil-design-eng@ecf66bb` §"Buttons must feel responsive" (0.97); `make-interfaces-feel-better@3845620` §"Scale on Press" (0.96) |
| note | Exact value differs — see `misalignment.md#scale-on-press-value`. Principle is aligned; specific number is merged. |

### `stagger-entries`

| field | value |
|-------|-------|
| sources | `emil-design-eng`, `make-interfaces-feel-better` |
| statement | When multiple elements enter together, stagger their appearance instead of animating them as one block. |
| evidence | `emil-design-eng@ecf66bb` §"Stagger Animations" (30–80ms per item); `make-interfaces-feel-better@3845620` §"Split and Stagger Enter Animations" (~100ms per group) |
| note | Exact stagger duration differs — see `misalignment.md#stagger-timing`. |

### `review-as-before-after-table`

| field | value |
|-------|-------|
| sources | `emil-design-eng`, `make-interfaces-feel-better` |
| statement | Present UI review findings as a markdown table with Before and After columns, one row per change. Never use inline "Before:" / "After:" lines. |
| evidence | `emil-design-eng@ecf66bb` §"Review Format (Required)"; `make-interfaces-feel-better@3845620` §"Review Output Format" |
| note | Emil adds a third "Why" column; MIFB groups by principle with one table per section. Superset format chosen for `full` — see `misalignment.md#review-table-columns`. |

Source list: [`../README.md`](../README.md), [`../sources.yml`](../sources.yml).
