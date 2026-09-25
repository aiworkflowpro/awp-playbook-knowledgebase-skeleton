---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-dashboard-channel
language: en
publication: public
title: "Channel Operations Four-Layer Matching Methodology"
---

# Channel Operations Four-Layer Matching Methodology

> Manage one thing: the four categories of account operations truth — brand, role, workflow, business — each hold its position. Change one, others only point to it.
> Applies to account operations with operational roles + creative workflows + business channel repositories.
> Does not govern platform facts (character limits, review policies), nor does it teach interaction strategy methodology.

## What Each Layer Manages

| Layer | Path Pattern | Only Manages | Does Not Manage |
|-------|----------|--------|--------|
| **Brand** | `{brand_root}{brand}/` | Slow-changing identity, strategic positioning, experiment conclusions | Daily quota, specific post content, scheduled config |
| **Role** | `{dashboard_root}roles/{operational_role}/` | Dispatch, execution quota, four-stage retrospectives, failure case studies | Full strategy text, creation steps, published originals |
| **Workflow** | `{workflows_root}{workflow}/` | Repeatable process: steps, gates, scripts, reference materials and judgment criteria loading | Published posts, today's count |
| **Business** | `{business_root}{brand}/{channel}/` | Published content originals, channel strategy, performance data, account status | Dispatch procedures, intermediate review drafts |

Process cache is not a fifth layer original: `{run_output_root}{YYYYMM}/{YYYYMMDD}/...` is traceable and expirable, **not** content original.

## Dual Landing Points

Creative output must land at two locations:

| Landing | Path | Nature |
|---------|------|--------|
| First | `{run_output_root}...` | Process + evidence chain |
| Second | `{business_root}{brand}/{channel}/{type}/` | **Published content original** |

Successful publication requires the second landing. Do not stop at temporary directory only, nor at workflow output directory only.

## Where to Change What

| I want to change... | Change only | Example |
|---------|------|------|
| Today's count, time to publish, downtime | **Role** handbook quota or guide | Ramp status table, automation guide |
| Steps / scripts / gates / reference material format | **Workflow** | Step files, script directory, reference library |
| Published post text, links, post type | **Business** content directory | Each content type directory |
| Who to reply to, selection logic (execution) | **Workflow** steps and scripts | Selection scripts |
| Who to reply to, response format, time slot (analysis and strategy) | **Business** `operations/strategy/` | Selection observations, response format |
| Exposure and interaction numbers | **Business** `operations/data/` | Content performance table |
| Who is who, experiment objective | **Brand** | Identity, strategy |
| Transferable experiment conclusion | **Brand** `exploration/` | Experiment conclusion for main brand |

**Iron rule**: Original content exists in only one original. Elsewhere, only write path pointers.

## Four-Stage Retrospective for Operational Roles

Operational roles **actively** consolidate findings and improvement proposals. **Do not default to modifying workflow**. Pipeline changes execute only after decision maker approval.

| Stage | Handbook File Naming | Write | Landing |
|-------|------------|--------|------|
| **L0 Observation** | `data-{channel}-observation-round.md` | Each round's phenomena | Handbook only |
| **L1 Experiment** | `data-{channel}-experiment-record.md` | Falsifiable hypotheses | Handbook only, escalate when case closed |
| **L2 Strategy** | `data-{channel}-strategy-proposal.md` | Proposal to change business strategy | Write to business `operations/strategy/` after approval |
| **L3 Pipeline** | `data-{channel}-pipeline-candidate.md` | Candidate to change workflow | **Proposal only**, change workflow after approval |

Each role handbook contains one governing document explaining promotion rules.

### Promotion Thresholds

| From → To | Threshold |
|---------|------|
| L0 → L1 | Falsifiable and worth retrying |
| L1 → L2 | Multiple same-direction results, or critical issue justifying skip |
| L2 → L3 | Policy written but execution remains unstable, or machine enforcement required |
| Any → Case Study | Caused or nearly caused operational error |

### How the Interaction Learning Loop Connects

Fields, sample size, and attribution dimension defined by operational interaction strategy methodology. **Where feedback lands** follows this methodology; strategy instance directories prioritized:

```text
{business_root}{brand}/{channel}/operations/strategy/
```

- Workflow resource library keeps only reference materials, identity loading, guardrails, and visuals. Selection execution logic lives in workflow steps and scripts.
- Business `operations/strategy/` holds **analysis and strategy proposals after execution**, not fed to workflow loading.

## Collaboration Formula

```text
Brand (who is who) ──load──► Workflow resource library
Role handbook (what to do today) ──dispatch──► Workflow (collect / write / publish)
                      │
                      ├─ Process → {run_output_root}
                      └─ Published → {business_root}{brand}/{channel}/{type}/
After publish ──collect data──► {business_root}.../operations/data/
Role L0–L3 ──pace in handbook──►
                      ├─ L2 approved → {business_root}.../operations/strategy/
                      └─ L3 candidate → await decision maker approval before workflow change
Weekly conclusion transferable ──────────► {brand_root}.../exploration/
```

| Subject | Default Does | Default Does Not |
|-------|--------|----------|
| Operational role | Dispatch, acceptance, L0–L3, L2 change business strategy | Change workflow steps or scripts |
| Temporary creation window | Follow workflow write and publish, dual landing | Change handbook quota, change pipeline skeleton |
| Decision maker | Approve direction, workflow changes, and L3 promotion | — |

## Checklist

- [ ] What layer is this based on? Change only that layer.
- [ ] Any process artifacts wrongly treated as business originals?
- [ ] Any business strategy wrongly copied into role handbook or workflow resource library?
- [ ] Has operational role changed workflow without approval (forbidden)?
- [ ] Did L2 already change business and write back proposal status?
- [ ] Did L3 stay in candidate table only, without unauthorized pipeline change?

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|--------|
| 2026-08-07 | Generalized from four-layer matching spec |
