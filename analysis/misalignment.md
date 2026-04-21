# Misalignment

Conflicts across sources + chosen fix for `full`.

Status: placeholder.

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

## Entry shape

- id
- type
- source positions
- strategy
- rationale

## Entries

### `tbd`

| field | value |
|-------|-------|
| id | `tbd` |
| type | _TBD_ |
| source A position | _TBD_ |
| source B position | _TBD_ |
| strategy | _TBD_ |
| rationale | _TBD_ |

Source list: [`../README.md`](../README.md), [`../sources.yml`](../sources.yml)
