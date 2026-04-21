# Provenance spec

Source of truth for skill tags. Do not copy regex elsewhere.

## Provenance

### Regex

```regex
^<!-- provenance: (source=[a-z0-9]+(?:-[a-z0-9]+)* sha=[0-9a-f]{7} section="[^"]+")( \| source=[a-z0-9]+(?:-[a-z0-9]+)* sha=[0-9a-f]{7} section="[^"]+")* -->$
```

### Rules

1. one per item, line above item
2. `source=` must exist in [`../sources.yml`](../sources.yml)
3. `sha=` must match pinned short SHA
4. `section` is exact heading / stable anchor
5. multi-source order: alpha by source id

### Examples

```markdown
<!-- provenance: source=emil-design-eng sha=abc1234 section="Tabular numbers" -->
```

Multi-source:

```markdown
<!-- provenance: source=emil-design-eng sha=def5678 section="Numbers in UI" | source=make-interfaces-feel-better sha=abc1234 section="Tabular numbers for dynamic values" -->
```

## Resolution

### Regex

```regex
^<!-- resolution: id=[a-z0-9]+(?:-[a-z0-9]+)* strategy=(prefer-A|prefer-B|merge|scope-split|fork|prefer-current|defer) -->$
```

### Rules

1. only in `full`
2. line right below provenance
3. `id` must exist in [`../analysis/misalignment.md`](../analysis/misalignment.md)
4. `strategy` must match conflict entry

### Example

```markdown
<!-- provenance: source=emil-design-eng sha=def5678 section="Depth cues" | source=make-interfaces-feel-better sha=abc1234 section="Shadows instead of borders" -->
<!-- resolution: id=borders-vs-shadows strategy=scope-split -->
```

## Violations

Validator fails if:

- item has no provenance tag
- tag regex fails
- source id missing
- SHA mismatch
- resolution tag outside `full`
- bad `resolution.id`
- bad `resolution.strategy`
