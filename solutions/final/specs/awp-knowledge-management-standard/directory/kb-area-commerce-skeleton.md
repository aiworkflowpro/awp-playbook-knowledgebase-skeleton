---
document_id: awp-knowledge-management-standard/directory/kb-area-commerce-skeleton
language: en
publication: public
title: "Knowledge Base Commerce/ Directory Skeleton"
---

# Commerce/ Directory Skeleton

> Defines the subdirectory structure under `{commerce_root}`, the organizational patterns it uses, and its customization interface.

## Responsibilities

Hosts the direction-scanning pipeline: scan the web for opportunities, decide whether they deserve further attention, and later verify whether those decisions were right. It answers only "is this worth a look?" — never "how do we run a business we have already committed to?"

## Directory Structure

```text
{commerce_root}
├── CLAUDE.md                 ← Fixed; entry point with the module list
├── discovery/                ← Fixed; find opportunities
│   └── {module_name}/        ← Three-piece set
├── judgment/                 ← Fixed; pick opportunities
│   ├── deep-analysis/        ← Three-piece set
│   └── decision/             ← Three-piece set; continue or stop a candidate direction
├── retrospective/            ← Fixed; verify judgments
│   └── review/               ← Three-piece set
├── methodology/              ← Fixed; flat .md files, no subdirectories
└── market-perspective/       ← Optional; external intelligence
    ├── discovery-industry-news/
    ├── judgment-cognition-gaps/
    └── best-practices/
```

- The path variable `{commerce_root}` is declared in `{specs_root}layout.yaml`.
- The three stage directories are always named `discovery`, `judgment`, and `retrospective` — **no numeric prefixes**.
- Under each stage, directories are built per module, and module names are short descriptive phrases.
- Do not create "established-business" directories in this area (product lists, audience, competitors).

### Three-Piece Set

Every scan module has the same fixed internal structure:

```text
{phase}/{module_name}/
├── CLAUDE.md              ← States which workflow it corresponds to
├── daily-scan/            ← Results of a single run
├── index.md               ← Full aggregation
└── to-{next_station}.md   ← Handoff to the next stage
```

| File | Responsibility |
|------|------|
| `daily-scan/` | One file per run; the filename carries a timestamp |
| `index.md` | Aggregates the daily-scan results into one table |
| `to-*.md` | Handoff file; the name varies with the stage: discovery produces `to-judge.md`, judgment produces `to-execute.md`, operations produces `to-retrospective.md` |
| `CLAUDE.md` | States which workflow drives this module |

If a module needs to store additional long-term material (for example, a candidate list library), this must be stated in the module's `CLAUDE.md`, and such material cannot replace the three-piece set.

### Handoff Chain

```text
discovery/{module}/to-judge.md            →  judgment/deep-analysis/
judgment/deep-analysis/to-execute.md      →  solidify into the brand operations domain, or land in the business area
{brand_root}{brand_name}/operations/to-retrospective.md  →  retrospective/review/
retrospective/review/index.md             →  can feed back into discovery
```

### Explicitly Do Not Store in This Area

| Content | Correct Landing |
|------|---------|
| Established product lists and pricing | `{brand_root}{brand_name}/operations/business-model/` |
| Established audience conclusions | `{brand_root}{brand_name}/operations/audience/` |
| Competitor system write-ups | `{brand_root}{brand_name}/operations/competitors/` |
| Execution and scheduling | `{business_root}` |

## Organizational Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → stage | **E3 Functional Responsibility** | Short descriptive phrases; the structure is fixed and does not grow over time |
| Stage → module | **K3 Business Scanning Three-Piece Set** | daily-scan + index + to-{next_station} |
| Module → daily-scan file | **T3 variant** | `{timestamp}-{topic}.md` |
| `methodology/` | Flat | No subdirectories |

Pattern definitions are in `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{commerce_root}` | Root path of this area | `commerce/` (see `layout.yaml`) |
| Stage vocabulary | Which stage directories exist under the root | `discovery`  -  `judgment`  -  `retrospective` (closed set; no extension) |
| Module list | Which modules exist under each stage | Registered by the user in the root `CLAUDE.md` |
| Handoff file name | The next station in `to-{next_station}.md` | discovery→`to-judge`, judgment→`to-execute`, operations→`to-retrospective` |
| Daily-scan file name | Naming for the results of a single run | `{YYYYMMDDHHmm}-{topic}.md` |
| Methodology file name | Naming under `methodology/` | `{YYYYMM}-{stage}-{name}.md` |
| `market-perspective/` enabled | Build it only when external intelligence needs separate storage | Off |
| Run frequency | Whether a module runs on a schedule | As needed; stopping the scheduled task does not mean the module goes offline |

### Adding a Scan Module

All three must be in place at the same time; if any one is missing, do not build:

1. One methodology file under `methodology/`.
2. One corresponding workflow.
3. The `{phase}/{module_name}/` three-piece-set directory.

After building it, add one registration line to `{commerce_root}CLAUDE.md`.

## Related Methodologies

- `../methodology/commerce/` — How to write daily-scan content, the threshold a candidate direction must clear before entering judgment, and how the methodology, the workflow, and the output directory map to one another.

## Checklist

- [ ] Stage directory names have no numeric prefixes
- [ ] Each module has all four items: `daily-scan/` + `index.md` + `to-*.md` + `CLAUDE.md`
- [ ] Handoff file names match the stage they are in
- [ ] Daily-scan file names carry timestamps
- [ ] Files under `methodology/` are flat, with no subdirectories
- [ ] No product lists, audience conclusions, or competitor write-ups appear in this area
- [ ] When adding a module, the methodology, the workflow, and the output directory are all in place
- [ ] Registered in `{commerce_root}CLAUDE.md`

## Change Log

> Rolling window; keep the most recent 3 entries, each ≤20 characters.

| Date | Change |
|------|---------|
| 2026-08-14 | Fixed methodology/ dir name |
| 2026-08-07 | Extracted skeleton from the commerce specification |
