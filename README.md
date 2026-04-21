# design-engineer

An aggregator of **design engineer skills** from across the community.

## What this is

This repository collects, compares, and merges design engineer skills published by different authors and organizations. The goal is to provide a single reference that makes it easy to see where sources agree, where they disagree, and to use a consolidated version in your own workflow.

## Repo layout

```
design-engineer/
├── README.md                   # this file
├── sources/                    # local-only workspace (gitignored) for reviewing originals
│   └── README.md               # how to clone the tracked upstream repos locally
├── skills/                     # deliverables — installable agent skills
│   ├── design-engineer-aligned/SKILL.md
│   └── design-engineer-full/SKILL.md
└── analysis/                   # comparison work that feeds the skills above
    ├── alignment.md
    └── misalignment.md
```

- Installable skills: [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md), [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md)
- Detailed analysis: [`analysis/alignment.md`](analysis/alignment.md), [`analysis/misalignment.md`](analysis/misalignment.md)
- Local sources workspace: [`sources/README.md`](sources/README.md)

## Principles

- **Full credit to original authors.** Every skill included here retains attribution to its source (author, repository, and license where applicable).
- **Actively seeking more sources.** If you know of a design engineer skill set we should include, please open an issue or PR.
- **Respect for authors.** If any source author would like their content removed, we will remove it as soon as possible — just open an issue or contact the maintainer.

## Sources

We maintain a list of the sources we aggregate from. Each source is linked and credited.

| Source | Author | Link | License | Date added |
|--------|--------|------|---------|------------|
| make-interfaces-feel-better | Jakub Krehel ([@jakubkrehel](https://github.com/jakubkrehel)) | [github.com/jakubkrehel/make-interfaces-feel-better](https://github.com/jakubkrehel/make-interfaces-feel-better) | MIT | 2026-04-21 |
| emil-design-eng | Emil Kowalski ([@emilkowalski](https://github.com/emilkowalski)) | [github.com/emilkowalski/skill/tree/main/skills/emil-design-eng](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | See repo | 2026-04-21 |

## Alignment table

Skills and concepts that appear across multiple sources — where there is broad agreement. Detailed, per-topic evidence lives in [`analysis/alignment.md`](analysis/alignment.md).

| Skill / Concept | Sources in agreement | Notes |
|-----------------|----------------------|-------|
| _TBD_           | _TBD_                | _TBD_ |

## Misalignment table

Skills and concepts where sources disagree, or where the framing / scope / emphasis differs meaningfully. Detailed positions and resolution notes live in [`analysis/misalignment.md`](analysis/misalignment.md).

| Skill / Concept | Source A position | Source B position | Nature of disagreement |
|-----------------|-------------------|-------------------|------------------------|
| _TBD_           | _TBD_             | _TBD_             | _TBD_                  |

## Skill versions

We publish two versions of the aggregated skill set:

1. **Aligned** — only the skills and guidance that all (or the large majority of) sources agree on. Conservative, high-confidence baseline. See [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md).
2. **Full** — all skills from all sources, merged and deduplicated, with conflicts resolved or noted. Broader coverage, includes contested material. See [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md).

## Removal requests

If you are the author of a source included here and would like it removed, please open an issue or reach out to the maintainer. We will remove it as soon as possible, no questions asked.

## Contributing

- Suggest a new source by opening an issue with a link and author info.
- Propose alignment / misalignment entries via PR.
- All contributions must preserve attribution to original authors.
