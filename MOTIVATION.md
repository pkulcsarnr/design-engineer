# Motivation

## Problem

Loading many skills at once causes:

1. more ctx cost
2. hidden conflicts
3. weak audit trail

## Thesis

Explicit merge once > implicit merge every turn.

This repo ships:

- `design-engineer-aligned` = consensus only
- `design-engineer-full` = merged set + logged conflict handling

Goal: one coherent skill, not random mix.

## Tradeoffs

- stale vs upstream -> pin SHAs in [`sources.yml`](sources.yml)
- less author voice -> keep `aligned` strict, `full` traceable
- more attribution work -> require provenance tags

## Don't use this repo if

- you want one author's exact taste
- you are source author
- your design system is already very opinionated

## Why not just link sources?

Links help humans read. Skills help agents act. This repo ships the merged skill; analysis just makes it trustworthy.

## Success

1. `aligned` feels safe.
2. `full` is traceable item by item.
3. adding source is reviewable in one PR.
4. takedown is one clean PR.
