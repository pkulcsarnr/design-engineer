# Misalignment

Conflicts across sources + chosen fix for `full`.

## Types

| type | meaning | usual fix |
|------|---------|-----------|
| `contradiction` | opposite advice | `prefer-A`, `prefer-B`, `fork` |
| `scope-difference` | same idea, diff scope | `scope-split` |
| `emphasis-difference` | same advice, diff strength | `merge` |
| `framing-difference` | same advice, diff wording | `merge` |
| `silence` | one speaks, one doesn't | no conflict entry |
| `version-drift` | changed over time | `prefer-current` |

## Strategies

`prefer-A`, `prefer-B`, `merge`, `scope-split`, `fork`, `prefer-current`, `defer`

## Entries

### `scale-on-press-value`

| Field | Value |
|-------|-------|
| Id | `scale-on-press-value` |
| Type | emphasis-difference |
| Source A | `emil-design-eng` @ ecf66bb — section `"Buttons must feel responsive"` |
| Source A position | Use `transform: scale(0.97)` on `:active`. Range 0.95–0.98 acceptable. |
| Source B | `make-interfaces-feel-better` @ 3845620 — section `"Scale on Press"` |
| Source B position | Always use `scale(0.96)`. Never use a value smaller than 0.95. |
| Resolution strategy | merge |
| Rationale | Both agree the effect is subtle, both forbid values below 0.95. The exact number inside the 0.95–0.98 band is aesthetic. Merge as a narrow band with a default. |
| Resolved in | unreleased |

### `stagger-timing`

| Field | Value |
|-------|-------|
| Id | `stagger-timing` |
| Type | emphasis-difference |
| Source A | `emil-design-eng` @ ecf66bb — section `"Stagger Animations"` |
| Source A position | 30–80ms between staggered items. Long delays feel slow. |
| Source B | `make-interfaces-feel-better` @ 3845620 — section `"Split and Stagger Enter Animations"` |
| Source B position | ~100ms between grouped content chunks. ~80ms between individual words in a title. |
| Resolution strategy | merge |
| Rationale | Numbers overlap at the edges. MIFB talks about semantic groups (heavier), Emil talks about list items (lighter). Keep both bands and note the unit. |
| Resolved in | unreleased |

### `icon-swap-entry-scale`

| Field | Value |
|-------|-------|
| Id | `icon-swap-entry-scale` |
| Type | scope-difference |
| Source A | `emil-design-eng` @ ecf66bb — section `"Never animate from scale(0)"` |
| Source A position | Entering elements should start from `scale(0.9)` or higher (plus opacity). Nothing in the real world appears from nothing. |
| Source B | `make-interfaces-feel-better` @ 3845620 — section `"Contextual Icon Animations"` |
| Source B position | Contextual icon swaps must start at `scale: 0.25` (exact) with opacity 0 and blur 4px. |
| Resolution strategy | scope-split |
| Rationale | Emil's rule targets general element entries (cards, toasts, modals). MIFB's rule targets swapping one icon for another inside a button, where scale 0.25 combined with blur reads as the icon arriving through focus — a different visual grammar. Different scopes, both correct. |
| Resolved in | unreleased |

### `icon-swap-bounce`

| Field | Value |
|-------|-------|
| Id | `icon-swap-bounce` |
| Type | scope-difference |
| Source A | `emil-design-eng` @ ecf66bb — section `"Spring configuration"` |
| Source A position | Keep bounce subtle (0.1–0.3) when used. Avoid bounce in most UI. Use it for drag-to-dismiss and playful interactions. |
| Source B | `make-interfaces-feel-better` @ 3845620 — section `"Contextual Icon Animations"` |
| Source B position | For icon spring animations `bounce` must always be `0`. Never `0.1` or any other value. |
| Resolution strategy | scope-split |
| Rationale | MIFB's absolute applies specifically to contextual icon swaps (repetitive, subtle micro-interaction). Emil's range applies to decorative or gesture-driven motion (drag, playful moments). No contradiction once scoped. |
| Resolved in | unreleased |

### `review-table-columns`

| Field | Value |
|-------|-------|
| Id | `review-table-columns` |
| Type | emphasis-difference |
| Source A | `emil-design-eng` @ ecf66bb — section `"Review Format (Required)"` |
| Source A position | Markdown table with three columns: Before, After, Why. |
| Source B | `make-interfaces-feel-better` @ 3845620 — section `"Review Output Format"` |
| Source B position | Markdown table with two columns: Before, After. Group by principle with a heading per table. |
| Resolution strategy | merge |
| Rationale | Emil's 3-column format is a superset of MIFB's 2-column format — the Why column adds reasoning that also teaches. MIFB's per-principle grouping still applies. Use Before/After/Why tables grouped by principle. |
| Resolved in | unreleased |

Source list: [`../README.md`](../README.md), [`../sources.yml`](../sources.yml).
