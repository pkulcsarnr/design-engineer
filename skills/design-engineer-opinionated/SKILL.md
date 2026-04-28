---
name: design-engineer-opinionated
description: Opinionated UI-tactics skill. Use when building or reviewing UI and you want pragmatic, maintainer-authored rules on hierarchy, contrast, shadows, borders, icon sizing, accent color, and button hierarchy. These items are not merged from tracked sources; they are rewritten from public UI-design writing and maintainer experience.
---

# Design Engineer - Opinionated

Opinionated UI-tactics layer. Items here are **not** merged from tracked sources in [`../../sources.yml`](../../sources.yml). They are either maintainer-authored or rewritten in repo voice from publicly visible UI-design writing.

For the consensus-only skill, see [`../design-engineer-aligned/SKILL.md`](../design-engineer-aligned/SKILL.md). For the merged, conflict-aware skill, see [`../design-engineer-full/SKILL.md`](../design-engineer-full/SKILL.md). For the combined output that applies `full` then this layer, see [`../design-engineer-extended/SKILL.md`](../design-engineer-extended/SKILL.md).

For authoring rules, see [`../../CONVENTIONS.md`](../../CONVENTIONS.md) and [`../../schemas/opinion.md`](../../schemas/opinion.md). Use [`../../prompts/author-opinionated-skill.md`](../../prompts/author-opinionated-skill.md) to add or change items.

## Precedence

If an item here conflicts with a tracked-source item in `full`, the `full` item wins. Opinionated items are supplemental, not a substitute. Treat them as defaults you can override when a tracked-source item says otherwise.

## Text hierarchy

<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Use color and weight to create hierarchy instead of size" reviewed=2026-04-28 -->
### Lead with weight and color, not size, for text hierarchy

Before reaching for a bigger font size, change the weight or the color. Reserve size changes for true headings and display text; use weight and color to separate primary, secondary, and tertiary text inside a single block. Keep the palette for body text to three tones: one near-dark for primary, one mid-gray for secondary, one lighter gray for ancillary. Keep weight to two values for UI: a regular (400 or 500) and a bold (600 or 700). Do not use weights below 400 for small UI text; if text should feel quieter, lighten the color or shrink the size instead.

## Contrast on color

<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Don't use grey text on colored backgrounds" reviewed=2026-04-28 -->
### Never put neutral gray text on a colored background

Gray-on-white reads as de-emphasized because it lowers contrast against white. On a colored background, gray reintroduces contrast against the hue and reads as dirty. Instead, lower the foreground in one of two ways: reduce the opacity of white text so the background hue bleeds through, or hand-pick a tint from the same hue as the background with adjusted saturation and lightness. Use opacity for solid surfaces, hand-picked tints for images, gradients, or patterns where opacity dulls the text too much.

## Depth and shadows

<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Offset your shadows" reviewed=2026-04-28 -->
### Offset shadows vertically; do not inflate blur and spread

Real light sources shine down. A flat radial halo around an element reads as fake depth; a small vertical offset reads as a lit surface. Drop shadows should use a modest blur and a vertical offset of roughly the same magnitude, not a large spread. The same rule applies to inset shadows on wells and form inputs: offset downward to imply light from above. If you need more visual weight, layer two shadows rather than cranking spread on one.

## Borders versus other separators

<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Use fewer borders" reviewed=2026-04-28 -->
### Reach for spacing, background contrast, or shadow before a border

Borders add one visual line per element. A layout full of them reads as busy even when every individual rule is justified. Before adding a border, try three cheaper alternatives: increase the gap so the separation is spatial, shift one side to a slightly different background so the edge is implied, or add a subtle offset shadow so the edge is lit. Borders are correct for dividers and table cells; they are overused almost everywhere else. When two techniques overlap, remove the border.

## Icon sizing

<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Don't blow up icons that are meant to be small" reviewed=2026-04-28 -->
### Do not inflate 16 to 24 pixel glyphs into hero illustrations

Vector glyphs stay sharp at any size, but glyphs drawn for 16 to 24 pixel use are drawn with chunky strokes and low detail on purpose. Scaled to 48 or 64 pixels they read as cheap. If the layout wants a bigger visual anchor, keep the glyph at its intended size and wrap it in a larger shape with a background color or tint. If the design truly needs large iconography, use an icon set drawn for that size, not a scaled-up small glyph.

## Accent color

<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Use accent borders to add color to a bland design" reviewed=2026-04-28 -->
### Use accent borders as restrained color, not decoration

A thin colored bar on one side of a card, alert, or active nav item adds brand color without asking for graphic-design skill. Keep it restrained: one accent edge per component, applied to meaningful states (selection, severity, active route). Do not outline every surface with an accent; the trick works because it is selective. Pull accent values from a constrained palette rather than a full color picker so the set stays coherent across the product.

## Button hierarchy

<!-- opinion: basis=public url="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886" section="Not every button needs a background color" reviewed=2026-04-28 -->
### Style buttons by hierarchy first, semantics second

On any screen, actions form a pyramid: one primary action, one or two secondary actions, zero or more tertiary actions. Map visual weight to that pyramid before mapping it to semantics. Primary action: solid, high-contrast fill. Secondary action: outline or low-contrast fill. Tertiary action: plain link styling. Destructive actions are not automatically red-filled; a destructive secondary action should look like a secondary button with a red label, and only a destructive *primary* action (for example, a confirmation dialog) earns the loud red fill. Filling every button with its semantic color flattens the hierarchy and makes every action feel equally important.

## Attribution

This skill is not derived from tracked sources in [`../../sources.yml`](../../sources.yml). Items above are rewritten in maintainer voice with an `opinion` tag pointing to the public page that inspired them; see [`../../schemas/opinion.md`](../../schemas/opinion.md).
