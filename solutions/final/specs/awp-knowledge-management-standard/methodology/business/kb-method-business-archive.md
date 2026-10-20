---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-archive
language: en
publication: public
title: "Business Methodology  -  Project Archive"
---

# Business Methodology  -  Project Archive

> Manage business with clear start and end, one-time delivery: three-section skeleton, state machine, milestones.
> Inherits all constraints from `kb-method-business-general.md`, this file adds only what applies to project archive specifically.

## I. What We Manage

Every industry has lots of project-based work: one article or one video episode in content creation, one product selection and listing in e-commerce, one consulting delivery, one construction in engineering, one research topic in science, one event in event planning. Common features: they have a start, an end, and delivery happens once.

Endlessly circulating resources do not belong here; they go to operating assets.

## II. Four Core Principles

- **Start and finish**: A project must have a clear start and end.
- **Unified three-section skeleton**: Production, publish, archive apply across industries; project structure is the same regardless of the work.
- **State machine driven**: State decides which files should exist and which operations are allowed.
- **Traceable milestones**: A project must have milestone records, not just directories and files.

## III. Three-Phase Skeleton

Each project organizes by the structure below, sections enabled by project state. This is an archive completeness requirement, not a product development phase plan.

```text
{project_directory}/
├── project.md          # metadata + facet + milestones (required for whole lifecycle)
├── CLAUDE.md           # project navigation index (optional, recommended for complex projects)
├── production/         # drafts, materials, intermediate deliverables (required when state is "in progress")
├── publish/            # final deliverables + publishing info (required when state is "ready to publish")
└── archive/            # data snapshots, retrospective, material sedimentation (required when state is "archived")
```

### Enabled by State

| State | Required sections | Optional sections |
|------|-------|-------|
| Planned | `project.md` | production / publish / archive |
| In progress | `project.md` + `production/` | publish / archive |
| Ready to publish | `project.md` + `production/` + `publish/` | archive |
| Published | `project.md` + `production/` + `publish/` (archive recommended) | — |
| Archived | `project.md` + `production/` + `publish/` + `archive/` | — |

### Historical Projects

Old projects completed before this spec took effect are handled leniently:

- Must add `project.md` (metadata plus facet).
- `publish/` and `archive/` may be skipped; use the "external entry reference" field in `project.md` metadata to point to the channel operations directory instead.
- Empty directories must not be created just for formal completeness.

Judge "before spec took effect" by comparing project creation date with spec release date, or let the organization define it.

### Division of Labor Between the Two Files

| File | Duty | Required |
|------|------|------|
| `project.md` | Project metadata source of truth: facet, milestones, external entry reference, corresponding workflow reference | Whole lifecycle |
| `CLAUDE.md` | Navigation index: subdirectory jumps, trigger words | Complex projects only |

The two do not overlap: `project.md` answers "what is this project's metadata", `CLAUDE.md` answers "what is in this directory, how to navigate". Simple projects only need `project.md`. Complex projects (over 20 files, or multiple subdirectories) need both.

### `project.md` Extra Required Fields

In addition to the universal nine fields:

| Field | Description | Required from |
|------|------|------------|
| Milestones | Timeline table (date + event), appended as it goes | Whole lifecycle |
| Final deliverable path | Points to `publish/{deliverable_file}` | When state is "ready to publish" |
| External entry reference | Points to external entry in channel operations directory | When state is "published" |
| Retrospective path | Points to `archive/retrospective.md` | When state is "archived" |

## IV. State Machine

### Core Three States (every industry needs these)

```text
Planned ──→ In progress ──→ Done
```

Whether to keep editing or archive after done is the organization's own decision.

### Recommended Five States (projects with a publish action)

```text
Planned ──→ In progress ──→ Ready to publish ──→ Published ──→ Archived
   │            │               │               │           │
allow empty   production   publish must   trigger relay   read-only
draft         must have    have complete  to external     no edit
              intermediate deliverable   display domain
```

Applies to projects with a "publish" action: content creation, software version release, product listing.

### Industry Extended State Machines

| Business type | Recommended state sequence |
|------|------------|
| Construction and engineering | Initiation → Design → Bidding → Construction → Acceptance → Warranty → Settlement |
| Software and online services | Requirements → Design → Development → Testing → Release → Operations → Deprecation |
| Research and academia | Initiation → Investigation → Experiment → Writing → Review → Publication → Closing |
| Consulting services | Approach → Diagnosis → Proposal → Execution → Acceptance → Retrospective |
| Legal cases | Acceptance → Investigation → Evidence → Litigation → Judgment → Execution |
| Medical diagnosis and treatment | First visit → Examination → Diagnosis → Treatment → Follow-up → Case closing |
| Advertising campaigns | Planning → Materials → Delivery → Monitoring → Optimization → Retrospective |

Three requirements:

- Any organization can customize its state machine, but must state in `project.md` metadata which set it uses.
- The state machine must cover the meaning of the core three states: has a start, has a middle, has an end.
- Vague states are forbidden. "Progress 1" or "Phase A" are not state names; state names must carry meaning.

### Hard Constraints on State Transitions (five-state version)

| From | To | Constraint |
|---|---|------|
| Planned | In progress | Must start the `production/` subdirectory or workspace |
| In progress | Ready to publish | Must create final deliverable in the `publish/` subdirectory |
| Ready to publish | Published | Must create external entry in channel operations directory (cross-reference, not copy) |
| Published | Archived | Must complete retrospective record |

Three prohibitions:

- Skipping intermediate states is forbidden, e.g. going straight from "in progress" to "published".
- A "published" state without a corresponding external entry is forbidden.
- Archived projects must not be edited again; only read and reference.

Hard constraints on industry extended state machines are defined by the organization itself. This methodology only requires "has start, has middle, has end" plus "explicit declaration".

## V. Required Sections

| Section | Location | Required from |
|------|------|----------------|
| Metadata plus milestones | Top of `project.md` | Whole lifecycle |
| Goal and deliverable definition | `project.md § Goal` | Planned |
| Production intermediate deliverables | Several files under `production/` | In progress |
| Final deliverable | `publish/{deliverable_file}` | Ready to publish |
| Publishing info | `publish/publishing-info.md` (platform, link, publish time) | Published |
| Retrospective | `archive/retrospective.md` | Within a week after published |

## VI. Recommended Sections

| Section | Location | Description |
|------|------|------|
| Data snapshot | `archive/data-snapshot.md` | Key metrics after publish, desensitize as needed |
| Material sedimentation | `archive/material-sedimentation.md` | Reusable material index, pointing to visual asset library or research library |
| Collaboration record | `production/collaboration.md` | Division of labor and communication in multi-person collaboration |

## VII. Industry-Specific Optional Sections

Add by business type to sub-files under `production/` or appended fields in `project.md`.

| Industry | Addition suggestions |
|------|---------|
| Content creation | Topic selection, script, shooting checklist, cover, search metadata |
| Software development | Requirements document, interface design, test report, change log |
| Physical R&D | Design drawings, bill of materials, prototype records, test reports |
| Engineering construction | Construction drawings, material lists, acceptance records, safety reports |
| Consulting services | Client background, diagnosis, proposal, deliverable list |
| Research projects | Literature review, method, dataset, conclusion |
| Legal services | Engagement contract, evidence records, documents |
| Medical diagnosis and treatment | Case, examination, plan (high privacy, be cautious entering the knowledge base) |

Industry-specific optional sections must not duplicate the three-phase skeleton; only add, never replace.

## VIII. Naming

Project directory naming: `{sequence}-{type-or-tag}-{title}/`

| Segment | Description | Slot |
|---|------|------|
| Sequence | Increments across years or per platform | `{NN}` |
| Type or tag | Optional short tag | `{type}` |
| Title | Project topic | `{title}` |

Taboos: pure date prefix, meaningless `project1/project2/`, spaces in the name (use `-` instead).

## IX. Deduplication Boundaries

| Content | Belongs to | Not to |
|------|------|------|
| Continuously maintained live resources | Operating assets | Project archive |
| Client and supplier records | Customer relationships | Project archive |
| Major strategic decisions | Strategic decisions | Project archive |
| Periodic reports | Operations data | Project archive |
| One-time activities or events | Event archive | Project archive (except the product itself) |
| External entries, data, links | Channel operations directory | Project archive (cross-reference, not copy body) |
| Concrete operating steps | Workflow library | Project archive (reference via facet) |

## X. Checklist

**New project**

- [ ] `project.md` contains nine metadata fields
- [ ] Three-section skeleton directories created per state
- [ ] Milestone table exists
- [ ] Corresponding workflow referenced or marked "none"

**State transition**

- [ ] When going from "ready to publish" to "published", external entry created in channel operations directory
- [ ] When going from "published" to "archived", `archive/retrospective.md` completed
- [ ] State change synced to "updated" date

**Archiving a project**

- [ ] Archive trio complete: retrospective, data snapshot, material sedimentation
- [ ] Corresponding archive entry exists in channel operations directory
- [ ] `project.md` state field set to "archived"
- [ ] Content locked, no more edits

## Change Record

> Rolling window, keep latest 3 entries, each ≤20 chars.

| Date | Change |
|------|---------|
| 2026-08-07 | Migrated from project archive spec and generalized |
