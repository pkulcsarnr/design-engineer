# design-engineer

An aggregator of **design engineer skills** from across the community.

## What this is

This repository collects, compares, and merges design engineer skills published by different authors and organizations, and publishes two merged skills — `aligned` (consensus only) and `full` (everything, with conflicts resolved in the open).

**Why a merge instead of installing each skill separately?** Loading multiple skills causes context bloat, silent conflicts at inference time, and no audit trail when output goes wrong. A merge decision made once — explicitly and reviewably — beats an implicit merge the model performs every turn. See [MOTIVATION.md](MOTIVATION.md) for the full argument, tradeoffs, and when **not** to use this repo.

## Repo layout

```
design-engineer/
├── README.md                   # this file
├── MOTIVATION.md               # why this repo exists; tradeoffs; when NOT to use it
├── CONVENTIONS.md              # provenance tag format; authoring rules
├── GOVERNANCE.md               # aligned threshold, takedowns, versioning, cadence
├── CHANGELOG.md                # per-release notes for the merged skills
├── sources.yml                 # machine-readable manifest of tracked sources (pinned SHAs)
├── sources/                    # local-only workspace (gitignored) for reviewing originals
│   └── README.md               # how to clone the tracked upstream repos locally
├── skills/                     # deliverables — installable agent skills
│   ├── design-engineer-aligned/SKILL.md
│   └── design-engineer-full/SKILL.md
├── analysis/                   # comparison work that feeds the skills above
│   ├── alignment.md            # per-topic agreements
│   └── misalignment.md         # typed conflicts + resolution strategies
└── evals/                      # validation that the merged skills actually work
    └── README.md
```

Key entry points:

- Why this repo exists: [`MOTIVATION.md`](MOTIVATION.md)
- Installable skills: [`skills/design-engineer-aligned/SKILL.md`](skills/design-engineer-aligned/SKILL.md), [`skills/design-engineer-full/SKILL.md`](skills/design-engineer-full/SKILL.md)
- Source manifest (source of truth): [`sources.yml`](sources.yml)
- Authoring rules: [`CONVENTIONS.md`](CONVENTIONS.md)
- Policies: [`GOVERNANCE.md`](GOVERNANCE.md)
- Analysis: [`analysis/alignment.md`](analysis/alignment.md), [`analysis/misalignment.md`](analysis/misalignment.md)
- Validation: [`evals/README.md`](evals/README.md)
- Release history: [`CHANGELOG.md`](CHANGELOG.md)
- Local sources workspace: [`sources/README.md`](sources/README.md)

## Principles

- **Full credit to original authors.** Every skill included here retains attribution to its source (author, repository, and license where applicable).
- **Actively seeking more sources.** If you know of a design engineer skill set we should include, please open an issue or PR.
- **Respect for authors.** If any source author would like their content removed, we will remove it as soon as possible — just open an issue or contact the maintainer.

## Sources

The authoritative list of tracked sources with pinned commit SHAs, licenses, and review dates lives in [`sources.yml`](sources.yml). The table below is a human-friendly summary kept in sync with that file.

| Source id | Author | Link | License | Pinned SHA | Last reviewed |
|-----------|--------|------|---------|------------|---------------|
| [`make-interfaces-feel-better`](https://github.com/jakubkrehel/make-interfaces-feel-better) | Jakub Krehel ([@jakubkrehel](https://github.com/jakubkrehel)) | [repo](https://github.com/jakubkrehel/make-interfaces-feel-better) | MIT | _TBD_ | _TBD_ |
| [`emil-design-eng`](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | Emil Kowalski ([@emilkowalski](https://github.com/emilkowalski)) | [repo](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | unknown (pending confirmation) | _TBD_ | _TBD_ |

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

## Using the skills

The `SKILL.md` files follow the agent-skill conventions used by the upstream sources. Until a formal installer / registry entry is confirmed, the supported usage is:

- **Manual copy.** Copy `skills/design-engineer-aligned/` or `skills/design-engineer-full/` into your agent's skills directory.
- **Direct load.** Point your agent's skill loader at the raw `SKILL.md` file path.

We are not yet claiming `npx skills add <this-repo>` works — that will be verified (and documented here) before being promised. See [`evals/README.md`](evals/README.md) for how we validate the skills themselves.

## Removal requests

If you are the author of a source included here and would like it removed, please open an issue or reach out to the maintainer. We will acknowledge within 48 hours and ship the removal PR within 7 days. The full takedown playbook is documented in [`GOVERNANCE.md`](GOVERNANCE.md#removing-a-source-takedown-requests).

## Contributing

- Suggest a new source by opening an issue with a link, author info, and license.
- Before extracting content from a new source, land a PR that adds it to [`sources.yml`](sources.yml) per [`GOVERNANCE.md`](GOVERNANCE.md#adding-a-source).
- Every merged-skill item must carry a provenance tag per [`CONVENTIONS.md`](CONVENTIONS.md).
- All contributions must preserve attribution to original authors.
