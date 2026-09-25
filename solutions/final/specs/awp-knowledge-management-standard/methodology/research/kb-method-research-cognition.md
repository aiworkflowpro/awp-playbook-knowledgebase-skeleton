---
document_id: awp-knowledge-management-standard/methodology/research/kb-method-research-cognition
language: en
publication: public
title: "Cognition Layer Methodology"
---

# Cognition Layer Methodology

> Manage One Thing: Converge cognition scattered across multiple sources into cross-source stable knowledge.
> Doesn't manage how single source digests (that's interpretation-card methodology), doesn't manage product design plan (that's design-directory methodology).

## Responsibility

Cognition layer manages one topic's `knowledge/` directory, output only **stable cross-source synthesized knowledge**:

| Output Type | File Location | Question Answered |
|---------|---------|-----------|
| State Table | `knowledge/state.md` | Which sources cognition layer includes, which pending |
| Synthesis Doc | `knowledge/synthesis.md` | About this topic, what do we know overall |
| Concept Page | `knowledge/cp-{lang}-{slug}/std.md` | Certain core methodology, framework, or model's cross-source deep-parse |
| Version Record | `knowledge/version/{YYYYMMDD}-{note}.md` | Audit log each cognition-layer change |
| Graph Export | `knowledge/graph/nodes.json` `edges.json` | Machinery-derive from concept-page metadata |

Concept-page naming `cp-{lang}-{slug}` (three-segment, no-date). Each concept-page one directory, internal body-file fixed-name.

**Cognition layer build-as-needed, not every topic needs one.** Criterion: Does cross-source synthesis conclusion actually have human or workflow reading it. Unread synthesis = pure maintenance burden.

## Five Design Principles

**Stability First.** Only pre-build slowly-changing knowledge—concept evolution-chain, multi-source verified framework, topic overview. Tool comparison, person info, writing context those dynamic-content leave Agent handle real-time.

**Incremental Accumulate.** Synthesis doc and concept-page append per-material growth, not-full-rewrite. New material come only modify that-one-two concept-page it affects.

**Accuracy-or-Nothing.** Write only cognition truly extracted from source material, don't fabricate unsupported-by-source opinion. Each cognition-point must mark source-entry.

**Use-First Facing.** Cognition-layer readers are action-takers. "How-use" write weightier than "what-is".

**Markdown Canonical.** Graph derivative-output, can't reverse become truth-source.

## What Not Pre-Build

These content look should-go-cognition-layer, actually Agent compile cheaper:

| Type Want-Build | Why Not Pre-Build | Compile-How |
|--------------|------------|-----------|
| Entity page (tool, person) | Info change-fast, pre-build outdates easily | Search related-interpretation-card real-time-splice |
| Compare page | New source come compare-change, maintain-costly | Per-need read 2-3 interpretation-card do real-time compare |
| Assert library | Multi-state flow + source-version track, maintain-cost far-exceed-gain | Concept-page "core-framework" section already contain reusable-judge |
| Writing pack | Every article-write context totally-differ, pre-build next-unused | Writing-workflow real-time compile synthesis-doc and interpretation-card |

## Directory Structure

```text
{topic}/knowledge/
├── state.md              # Coverage statistics (required)
├── synthesis.md          # Topic overview (required)
├── cp-{lang}-{slug}/     # Concept page (build-as-needed)
│   └── std.md
├── version/              # Audit log (required)
│   └── {YYYYMMDD}-{note}.md
└── graph/                # Derivative export (build-as-needed)
    ├── nodes.json
    └── edges.json
```

`state.md`, `synthesis.md`, `version/` minimum config. Concept-page build-when-threshold per-needed.

### When Produce What

| Output | Create or Update When |
|--------|--------------|
| State Table | After cognition-extraction update count; after new entry in-repo mark pending |
| Synthesis Doc | First extraction build framework; after each material-batch append incrementally |
| Concept Page | When satisfy build-threshold create new; new material affect exist-concept append source |
| Version Record | Each cognition-layer change write one-line |
| Graph Export | When need visualization or program-query, machinery-generate from metadata |

## Synthesis Document

Topic's "single-page overview"—read-complete know "about this topic, our complete current-understanding what".

### Structure

```markdown
# {Topic}  -  Synthesis Cognition

> Based N material, already-interpret M. Last update: YYYYMMDD.

## Core Framework

### {Direction 1}
{This direction's core-cognition, each-point mark source}

### {Direction 2}
...

## Open Question

{What we not-yet-know, what material need collect}

## Material Citation Index

| Entry | Contribute What Cognition |
|------|-----|
```

### Depth Requirement

| Dimension | Standard |
|-----------|----------|
| Core-framework count | At-least cover topic 3 major-direction |
| Each framework paragraph | 200-500 char, contain concrete method, step, data |
| Source mark | Each cognition-point mark **complete entry-dir-name**, not truncate |
| Concept-page link | Mentioned core-concept link-to concept-page |
| Open question | At-least list 3 awaiting-deep-direction |
| Material index | Must have "material citation index" section, each processed-material one-row |

### Word-Count Grow Per Accumulate

| Processed Entry Count | Expected Word-Count |
|------------|---------|
| 1-5 | 1000-2000 |
| 6-20 | 2000-5000 |
| 20+ | 5000-10000 |

Synthesis doc word-count naturally-grow per material-accumulate, not one-time write-complete.

## Concept Page

Certain core methodology, framework or model's cross-source deep-parse. Different from interpretation-card: interpretation-card from "one material" start, concept-page from "one concept" start, consolidate all material involve it.

### Metadata

```yaml
---
concept: {concept-name}
created: YYYY-MM-DD
sources:
  - {entry-dir-name-full}
  - {entry-dir-name-full}
related_concepts:
  - {related-concept}
lifecycle_phase: SEED
vitality: 0.8
superseded_by:
supersession_date:
scope_note:
---
```

`sources` each item must complete entry-dir-name, match disk exactly—tool rely it map concept-page to entry, truncate-name break.

### Structure

```markdown
# {Concept-Name}

{One-paragraph define this-concept}

## Evolution Lineage
{History develop—who propose, who develop, who operationalize}

## Core Framework
{Complete parse—each component, dimension, or step}

## Operation Method
{How use in actual-work}

## Application Scenario
{How hook-to own-business concrete-situation}

## Common Misconception
{Most common-mistake when-use this-concept}

## Core Source
{What material contribute understand}
```

### Depth Requirement

| Dimension | Standard |
|-----------|----------|
| Total word-count | 2000-5000 |
| Evolution lineage | Say clear lineage, not just list-name |
| Core framework | Complete parse, same-depth as interpretation-card |
| Multi-source cross | At-least reference 2 source |
| Operation method | Executable-level |
| Application scenario | At-least 3 concrete-scenario |
| Common misconception | At-least 3 |

### Lifecycle Phase

| Phase | Meaning | Enter Condition |
|-------|---------|----------|
| `SEED` | Auto-create, minimal-page | Satisfy build-threshold |
| `PATTERN` | Concept enrich, multi-source converge | 3+ source coalesce |
| `VALIDATED` | Pass checklist | Satisfy all check-item |
| `CANONICAL` | Other-concept depend this | Reference 2+ other-concept-page |

Phase forward-only never-revert. `vitality` (reference-frequency) and `superseded_by` (successor-relation) can-change anytime.

### Build Threshold

| Condition | Build-or-Not |
|-----------|--------|
| 3+ interpretation-card mention same methodology or framework | Build—multi-source verify, stable |
| Concept have clear evolution-chain | Build—history-lineage, stable |
| Only 1-2 interpretation-card mention, not-core-framework | Not-build, keep in-interpretation-card |
| Only 2 interpretation-card mention, two-opinion conflict | Not-build, not-yet-converge |

## State Table

Cognition-layer operation entry, record coverage-scope, not-write actual-cognition-content.

### Structure

```markdown
# {Topic}  -  Cognition State

> After each cognition-layer change update.

## State Summary

| Field | Value |
|------|-----|
| Topic | {topic} |
| Total Entry Count | N |
| Interpretation-Card Count | M |
| Cognition-Layer Integrate | K |
| Concept-Page Count | P |
| Recent Update | YYYYMMDD |

## Integrated Source

| Source | Contribute What | Integrate Date |
|--------|-----------|---------|

## Pending

{New-add but-not-yet-integrate interpretation-card list}

## Version Record Index

{Link-to version/ directory}
```

### Update Rule

- After new interpretation-card add, go "pending".
- After cognition-extract, move to "integrated source", write version-record.
- New material affect exist-concept-page mark in version-record.

### Count & Source ID Iron Rule

Complete-check use "can-find same-name entry-dir on disk by source-table source-id" judge stale-count. Write-wrong = report-false stale.

| Rule | Specification |
|------|------|
| Use Complete Dir-Name | "Integrated Source" column-one must complete entry-dir-name, match disk-char exact |
| Not Truncate | Don't truncate for-table-width; truncate make tool can't-recognize entry |
| Not Write Old Punctuation Variant | Don't write already-remove-from-dir-name char |
| Not Write Old Number | Use complete dir-name, not-historical short-number |
| Count Match Disk | Three count-field must equal current-disk actual count, sync-after-extract |
| Every Update "Recent" | Write `YYYYMMDD` |

## Version Record

Cognition-layer audit-log, each change write one-line.

```markdown
# {YYYYMMDD} {note}

## Version Info

| Field | Value |
|------|-----|
| version_id | {topic}-cognition-{YYYYMMDD}-{number} |
| type | init / incremental / graph-export |
| created_at | YYYYMMDD |

## This Input

{Process which interpretation-card}

## Change Summary

{New-add or-update which concept-page, synthesis-doc which-paragraph append content}

## New or Change Relation Edge

{Concept-between relate, successor, etc.}

## Pending Issue

{Discover what need-follow-up later}
```

## Graph Export

Graph directory only hold export-product, don't hand-write truth. Generate from concept-page metadata `related_concepts`, `superseded_by`, `absorbed_into` field.

Allow export: `nodes.json` / `edges.json`.

Forbid: Hand-maintain graph-data inconsistent-with-Markdown; use database replace synthesis-doc and concept-page truth.

Exportable relation-edge:

```text
concept -> related_to -> concept        # related_concepts field
concept -> superseded_by -> concept     # superseded_by field
concept -> absorbed_into -> concept     # absorbed_into field
source -> proposes -> concept           # sources field reverse
```

New relation-type first-modify this-methodology, then-modify export-script.

## Incremental Update

### When New Material Arrive

```text
New entry in-repo → interpretation-card generate
    ↓
Scan interpretation-card key-concept (extract from keyword and core-opinion section)
    ↓
├── Concept already-have concept-page → Append "core source" one-row + vitality +1
├── Concept 3+ interpretation-card mention but-no concept-page → Create concept-page (SEED)
└── Concept only 1-2 mention → Not-build, keep in-interpretation-card
    ↓
Synthesis-doc relevant-section append one-sentence new-find (not-rewrite-full-section)
    ↓
State-table update count + write version-record
```

### Incremental Rule

| Correct Do | Anti-Pattern |
|-----------|--------|
| Synthesis-doc relevant-chapter append new-cognition | Every new-material rewrite entire-synthesis-doc |
| Concept-page "core source" table append one-row | Discover new-perspective after-delete old-content rewrite |
| New concept-page only satisfy-threshold create | Every interpretation-card trigger build-page |
| Graph from metadata export | Hand-maintain separate-graph-data |

## Checklist

**State Table**

- [ ] `state.md` exist
- [ ] Record total-entry, interpretation-card, cognition-layer-integrate, concept-page count
- [ ] Three count-field match disk-actual
- [ ] "Integrated Source" each-row complete dir-name, stale-count zero
- [ ] Version-record index point `version/`

**Synthesis Document**

- [ ] Head mark based-how-many-material, interpret-how-many, update-date
- [ ] Core-framework cover at-least 3 direction
- [ ] Each cognition-paragraph mark complete-source entry-dir-name
- [ ] Open-question at-least 3
- [ ] Have "material citation index" section
- [ ] Word-count reach corresponding-stage minimum

**Concept Page**

- [ ] Metadata contain concept / created / sources / related_concepts / lifecycle_phase
- [ ] `sources` each-item complete entry-dir-name
- [ ] Six required-chapter all-have content
- [ ] At-least reference 2 source cross-verify
- [ ] Operation-method executable
- [ ] Common-misconception at-least 3
- [ ] Total word-count 2000-5000

**Version Record**

- [ ] Each change have `version/{YYYYMMDD}-{note}.md`
- [ ] Record this-input, change-summary, pending-issue

**General**

- [ ] All cognition-point mark complete-source entry-dir-name
- [ ] No unsource-support opinion
- [ ] `knowledge/` root no-whitelist-outside scatter-file

## Change Log

> Rolling window, retain last 3 entries, ≤20 characters each.

| Date | Content |
|------|---------|
| 2026-08-07 | Generalized from cognition-layer spec |
