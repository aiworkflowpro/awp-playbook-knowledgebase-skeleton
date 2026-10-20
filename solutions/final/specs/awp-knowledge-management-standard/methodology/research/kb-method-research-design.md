---
document_id: awp-knowledge-management-standard/methodology/research/kb-method-research-design
language: en
publication: public
title: "Design Directory Versioning Methodology"
---

# Design Directory Versioning Methodology

> Manage One Thing: Topic-level product or service design research using version snapshot management.
> Doesn't manage material digest (that's interpretation-card methodology), doesn't manage cross-material synthesis cognition (that's cognition-layer methodology).

## Responsibility

Design directory carries **implementation-facing decision plan**. Division with cognition-layer:

| Dimension | Cognition Layer | Design Layer |
|-----------|--------|----------|
| Output | Synthesis doc, concept-page | Design plan, research report, review doc |
| Source | Extract from material | Produce from discussion and research |
| Serve | Anyone needing topic knowledge | Product or service team for this topic |
| Update | Incremental sedimentation | Versioned snapshot |

Design directory **build-as-needed**, not force all-topic have. Criterion: Research target not only "understand one domain", but "design one product or service".

## Why Version Snapshot, Not Incremental Sedimentation

Three reasons:

**Decision need fix.** Design plan serve product implement, team need one-time align "current plan what-is". Incremental-accumulate doc can't give clear-baseline, version snapshot can—each version dir is one complete decision-state.

**Orthogonal with cognition-layer responsibility.** Cognition-layer answer "about this topic we know what", design-layer answer "based-on known-cognition we intend do what". First naturally-grow per material-accumulate, second jump-wise per product-phase. Update rhythm and lifecycle completely-different, separate manage let each independent-evolve.

**Lifecycle have endpoint.** Design plan finalize then migrate to specification directory and business directory, design directory as history-archive retain. Cognition-layer no endpoint—knowledge forever accumulate. This fundamental-difference decide design-layer version, cognition-layer increment.

## Directory Structure

Version dir directly-hang under `design/`, no `version/` middle-layer.

```text
{topic}/design/
├── status.md                    ← version index: each version's number, status, one-line
├── v01-{lang}-{slug}/           ← first version snapshot
│   ├── {code}-design-plan.md    ← main (decision consolidate)
│   ├── {code}-{topic}.md        ← research output
│   ├── {code}-review-{perspective}.md    ← review doc
│   └── ...
└── v02-{lang}-{slug}/           ← next version (copy-from previous-version main as start-point)
```

Version dir-name three-segment, `-` connect:

| Segment | Value | Example |
|---|------|-----|
| `v{NN}` | Two-digit number, from `v01` increment | `v05` |
| `{lang}` | This version document main-language | `zh`  -  `en` |
| `{slug}` | One-line code, say clear this-version differ-from previous | `preserve-true-express-shift` |

`status.md` must-have, put in `design/` root, one-version one-line, record version-number, status, one-line.

## Version Number Only Number Sequence, Not Stage

Number from `v01` two-digit increment, don't use decimal. Design walk-to which-stage write in `status.md` status-column, not-number-into version—same topic maybe emit five version still-in-design stage, use `v0.x` / `v1.0` stage-number force false-finalize-mark.

| Status Value | Meaning |
|--------|------|
| InProcess | This version still research, discuss, plan iterate |
| Complete | This version decision finalize, can start-point for next-version |
| Finalize | Design final, enter specification-write |
| Deprecated | Direction abandon, only history-archive view |

## Version Operation

| Scenario | Operation |
|----------|--------|
| Product owner say "create version" | Create new `v{NN+1}-{lang}-{slug}/`, copy previous-version main as start, modify in new-dir |
| Product owner not-say create version | Direct modify in current-version-dir |
| Every modify main | In main's "version record" table add one-row: version-number, date, change-summary, source-trigger |
| Every create version | In `design/status.md` append one-row |

## Main Rules

- Design plan main (`{code}-design-plan.md`) is each version-dir core-file.
- Main record all confirmed-decision (number D-01, D-02......) and pending-design (number P-01, P-02......).
- Research doc and review doc are main **input material**—main extract conclusion, not-repeat-full.

## Document Type

| Type | Name Format | Property |
|------|----------|---------|
| Design Plan | `{code}-design-plan.md` | Live doc, continuous-update |
| Research Report | `{code}-{topic}.md` | Read-only, complete-after not-change |
| Review Doc | `{code}-review-{perspective}.md` | Read-only, complete-after not-change |
| Incremental Update | `design-update-{topic}.md` | When-only partial change, not-copy full |

Version snapshot is version-dir itself, not-again save `{code}-design-plan-v{N}.md`.

## Connection with Product Lifecycle

```text
Design finalize  →  Specification write  →  Business dir + code repo
  (research dir)      (specification dir)    (business dir + separate repo)
```

- After design-plan finalize, formal-specification write move to specification-dir.
- Implement product migrate to business-dir and separate code-repo.
- `design/` dir as history-archive retain, not-delete.
- Design-plan finalize **before**, forbid pre-build formal file in specification or business dir—that cause two-version conflict.

## Checklist

- [ ] Version dir directly-hang under `design/`, no `version/` middle
- [ ] Version dir naming correct (`v{NN}-{lang}-{slug}/`)
- [ ] `design/status.md` exist, each version-dir one-row
- [ ] Main exist, contain version-record table
- [ ] Every modify record in version-record
- [ ] Research & review doc mark read-only
- [ ] Doc naming use unified product-code prefix
- [ ] Before finalize not-pre-build formal-file in specification or business-dir

## Change Log

> Rolling window, retain last 3 entries, ≤20 characters each.

| Date | Content |
|------|---------|
| 2026-08-07 | Generalized from design-directory spec |
