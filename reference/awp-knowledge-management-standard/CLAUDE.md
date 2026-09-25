---
document_id: awp-knowledge-management-standard/package-index
language: en
publication: public
title: "Knowledge Base Management Standard"
---

# Knowledge Base Management Standard

> Governs how to organize the knowledge base itself: directory structure, file naming conventions, and how to write content in each domain.
> Does not govern how things are created within it: code development, Agent construction, and content production each have their own standards.
> Before creating a new directory, creating a new file, batch renaming, or writing materials for a domain, start here to locate the relevant standard.

## Scope of Coverage

| Covered | Not Covered |
|---------|-------------|
| Organization rules for all directories and files in the knowledge base | Code development (covered by a separate development standard) |
| Cross-directory naming systems and document identity standards | Agent construction (covered by a separate Agent standard) |
| Directory structure skeletons for each area | Content writing methodology (covered by a separate content standard) |
| How materials should be written in each domain (methodology) | Markdown formatting and layout (covered by a separate document formatting standard) |
| Mapping and sync boundaries between two knowledge bases | Objective facts about publishing platforms (covered by a separate platform standard) |

## Three Dimensions

```text
naming/        What to name a file, what identity to give it     → Uniform across entire library, no exceptions
directory/     Where to place files, how to structure directories  → Select mode first, then build areas
methodology/   What to write in this directory, how to write it    → Divided by domain
```

The relationship between the three is **determine location first, then name, then content**:

1. Creating a new area: read `directory/kb-directory-pattern-registry.md` to select organization mode, read `directory/kb-directory-decision-composition.md` to confirm compatibility.
2. Area determined: read `naming/kb-naming-segment-convention.md` to name files, read `naming/kb-file-structure-metadata.md` to add metadata.
3. Writing content: read the corresponding domain volume in `methodology/`.

## Document Index

| Document | English Name | Description |
|----------|-------------|-------------|
| `kb-term-package-glossary.md` | Unified Terminology Index | 183 entries organized in 12 groups, with disambiguation for same-name conflicts |

### naming/ (4 documents)

| Document | English Name | Description |
|----------|-------------|-------------|
| `naming/kb-naming-segment-convention.md` | File Naming Segment Standard | Segments divided by hyphen count from zero to four segments, governing all library files and directory names |
| `naming/kb-file-structure-metadata.md` | File Structure and Metadata Standard | Common structure for all `.md` files, metadata fields, quality grading, change log |
| `naming/kb-document-identity-revision.md` | Document Identity and Revision Standard | `document_id` format, publication scope, source revision number, sync policy |
| `naming/kb-naming-governance-migration.md` | Naming Governance and Migration Standard | Directory-level batch renaming process: research, mapping, execution, acceptance |

### directory/ (18 documents)

**Universal Rules (7)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `directory/kb-vault-architecture-mapping.md` | Dual Knowledge Base Architecture and Directory Mapping | Relationship between source and distribution libraries, top-level directory mapping, cross-library sync scope |
| `directory/kb-directory-pattern-registry.md` | Directory Organization Mode Registry | All registered directory modes, their structure, and who uses them |
| `directory/kb-directory-decision-composition.md` | Directory Mode Decision Tree and Combination Rules | How to select modes, whether they can be combined, which practices are prohibited |
| `directory/kb-entry-authoring-standard.md` | `CLAUDE.md` Authoring Main Standard | Position of index files, iron rules, legal sections, capacity budget, and machine validation |
| `directory/kb-entry-layer-levels.md` | `CLAUDE.md` Layer-by-Layer Detailed Explanation | Six-layer system with how each layer is written and division of labor between layers |
| `directory/kb-entry-antipattern-archiving.md` | `CLAUDE.md` Anti-Patterns and Archiving Governance | Error pattern dictionary, handling orphaned index references after directory retirement |
| `directory/kb-entry-multiagent-compatibility.md` | `CLAUDE.md` Multi-Framework Compatibility Standard | How to distribute the same routing to multiple Agent frameworks |

**Area Skeletons (11)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `directory/kb-area-owner-skeleton.md` | `{owner_root}` Directory Skeleton | Subdirectory structure and customization interface for `{owner_root}` |
| `directory/kb-area-brand-skeleton.md` | `{brand_root}` Directory Skeleton | Subdirectory structure and customization interface for `{brand_root}` |
| `directory/kb-area-commerce-skeleton.md` | `{commerce_root}` Directory Skeleton | Subdirectory structure and customization interface for `{commerce_root}` |
| `directory/kb-area-workflows-skeleton.md` | `{workflows_root}` Directory Skeleton | Subdirectory structure and customization interface for `{workflows_root}` |
| `directory/kb-area-tools-skeleton.md` | `{tools_root}` Directory Skeleton | Subdirectory structure and customization interface for `{tools_root}` |
| `directory/kb-area-business-skeleton.md` | `{business_root}` Directory Skeleton | Subdirectory structure and customization interface for `{business_root}` |
| `directory/kb-area-research-skeleton.md` | `{research_root}` Directory Skeleton | Subdirectory structure and customization interface for `{research_root}` |
| `directory/kb-area-standards-skeleton.md` | `{specs_root}` Directory Skeleton | Subdirectory structure and customization interface for `{specs_root}` |
| `directory/kb-area-dashboard-skeleton.md` | `{dashboard_root}` Directory Skeleton | Subdirectory structure and customization interface for `{dashboard_root}` |
| `directory/kb-area-inbox-skeleton.md` | `{inbox_root}` Directory Skeleton | Subdirectory structure and customization interface for `{inbox_root}` |
| `directory/kb-area-inbox-ingest.md` | Document Ingestion Specification | Per-document import process: Place (copy whole doc) or Extract (merge info into existing files), confidence scoring, user confirmation, archive-not-delete |
| `directory/kb-area-personal-skeleton.md` | `{personal_root}` Directory Skeleton | Subdirectory structure and customization interface for `{personal_root}` |

### methodology/ (40 documents)

**Brand (7)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `methodology/brand/kb-method-brand-identity.md` | Brand Identity Modeling Methodology | How identity is layered, what each layer answers, decision trail preservation |
| `methodology/brand/kb-method-brand-persona.md` | AI Persona Modeling Methodology | Character brand's loadable inner settings, ten-layer questions and minimal loading |
| `methodology/brand/kb-method-brand-audience.md` | Audience Persona Methodology | Target audience identification, needs, and conversion path |
| `methodology/brand/kb-method-brand-businessmodel.md` | Business Model Methodology | Monetization path, revenue sources, customer acquisition channels and core principles |
| `methodology/brand/kb-method-brand-competitor.md` | Competitor Analysis Methodology | Four-component model, eight dimensions, threat level, review mechanism |
| `methodology/brand/kb-method-brand-reference.md` | Reference Materials Methodology | Six reference types' file skeleton and sharing rules |
| `methodology/brand/kb-method-brand-visual.md` | Brand Visual Asset Management Methodology | Visual asset organization, naming, sizing and reuse rules |

**Commerce (2)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `methodology/commerce/kb-method-commerce-scanning.md` | Direction Scanning Methodology | Continuously finding new business opportunities, assessing candidate value |
| `methodology/commerce/kb-method-commerce-dailyscan.md` | Daily Scan Report Methodology | Five fixed sections, character minimums and required fields for each |

**Business (12)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `methodology/business/kb-method-business-general.md` | Business Methodology  -  General Principles | How business assets are classified, tagged, and cross-referenced |
| `methodology/business/kb-method-business-operations.md` | Business Methodology  -  Operations Directory | Business unit operations directory's eight-directory structure and dimension selection matrix |
| `methodology/business/kb-method-business-contentid.md` | Business Methodology  -  Content ID | Unique identity for content across channels, mapping table, renaming gate |
| `methodology/business/kb-method-business-article.md` | Business Methodology  -  Article Directory | Official website content directory, single article structure, six-layer header metadata, state machine |
| `methodology/business/kb-method-business-course.md` | Business Methodology  -  Course Materials | Three-layer assets: main content, delivery, resources; two naming systems, channel derivation |
| `methodology/business/kb-method-business-asset.md` | Business Methodology  -  Operations Assets | Actively maintained resources: status, maintenance frequency, zombie determination |
| `methodology/business/kb-method-business-planning.md` | Business Methodology  -  Project Planning | Five-stage pipeline, four proof gates, solution document skeleton |
| `methodology/business/kb-method-business-archive.md` | Business Methodology  -  Project Archive | One-time deliverables with clear start/end: three skeleton sections, state machine, milestones |
| `methodology/business/kb-method-business-decision.md` | Business Methodology  -  Strategic Decision | Single major decision plus long-term review: background, options, assumptions |
| `methodology/business/kb-method-business-metrics.md` | Business Methodology  -  Operating Metrics | Cycle types, metric comparison, data sources, data anonymization |
| `methodology/business/kb-method-business-customer.md` | Business Methodology  -  Customer Relations | Relationship types, activity level, contact history, privacy boundary |
| `methodology/business/kb-method-business-event.md` | Business Methodology  -  Event Archive | One-time major events: planning, execution, review three sections |

**Research (4)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `methodology/research/kb-method-research-interpretation.md` | Interpretation Card Methodology | Seven required sections, depth standards by material type |
| `methodology/research/kb-method-research-cognition.md` | Cognition Layer Methodology | Converging knowledge scattered across multiple materials into stable knowledge |
| `methodology/research/kb-method-research-design.md` | Design Directory Versioning Methodology | Topic-level design research version snapshot management |
| `methodology/research/kb-method-research-theory.md` | Theory Guiding Practice Methodology | Complete chain from theory → methodology → workflow → output |

**Operations (10)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `methodology/operations/kb-method-dashboard-role.md` | Role Protocol Methodology | Behavior rules and task assignment rules for multiple Agent roles working together |
| `methodology/operations/kb-method-dashboard-channel.md` | Channel Operations Four-Layer Matching Methodology | Four true sources (brand, role, workflow, business) each in their place |
| `methodology/operations/kb-method-engagement-strategy.md` | Operations Engagement Strategy Methodology | Complete loop for replies, comments, private messages: selection and writing |
| `methodology/operations/kb-method-task-file.md` | Task File Methodology | One file, one task: path, naming, metadata, body structure |
| `methodology/operations/kb-method-task-statemachine.md` | Task State Machine Methodology | Task state sets and allowed transitions |
| `methodology/operations/kb-method-task-output.md` | Output Contract Methodology | How to feed back content to knowledge base after auto-executed task completes |
| `methodology/operations/kb-method-task-runreport.md` | Run Report Methodology | Flat report required after each inspection run |
| `methodology/operations/kb-method-task-automation.md` | Automation Registration Methodology | How to register mirror of scheduled tasks in knowledge base |
| `methodology/operations/kb-method-inbox-placement.md` | Placement Analysis Methodology | How to determine where a piece of content should go |
| `methodology/operations/kb-method-inbox-archive.md` | Archiving Methodology | How to organize the unique soft-delete area, naming, lifecycle |

**Personal (3)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `methodology/personal/kb-method-personal-finance.md` | Personal Finance Domain Methodology | Investment, insurance, major decisions, asset archive file writing |
| `methodology/personal/kb-method-personal-growth.md` | Personal Growth Domain Methodology | Reading, learning, reflection, skill file writing |
| `methodology/personal/kb-method-personal-leisure.md` | Personal Leisure Domain Methodology | Film/TV, travel, food, hobbies file writing |

**Tools (2)**

| Document | English Name | Description |
|----------|-------------|-------------|
| `methodology/tools/kb-method-practice-authoring.md` | Best Practice Authoring Methodology | Unified skeleton for tool tutorials, multi-carrier organization, version lifecycle |
| `methodology/tools/kb-method-credential-management.md` | Credential Management Methodology | Auth info file format, machine parsing, layered loading, expiration handling |

## Coverage Matrix

**Library-wide common standards** — apply to every directory and file:

| Layer | Documents |
|------|-----------|
| Naming and Identity | All 4 documents in `naming/` |
| Directory Organization | `directory/kb-directory-pattern-registry.md`, `directory/kb-directory-decision-composition.md` |
| Index Files | All 4 `directory/kb-entry-*.md` documents |
| Cross-Library Mapping | `directory/kb-vault-architecture-mapping.md` |

**Layer by area** — on top of common layer, each area receives additional constraints:

| Area | Directory Skeleton | Domain Methodology |
|------|-----------------|------------------|
| `{owner_root}` Owner | `kb-area-owner-skeleton` | — |
| `{brand_root}` Brand | `kb-area-brand-skeleton` | `methodology/brand/` 7 documents |
| `{commerce_root}` Commerce | `kb-area-commerce-skeleton` | `methodology/commerce/` 2 documents |
| `{workflows_root}` Workflow | `kb-area-workflows-skeleton` | — |
| `{tools_root}` Tools | `kb-area-tools-skeleton` | `methodology/tools/` 2 documents |
| `{business_root}` Business | `kb-area-business-skeleton` | `methodology/business/` 12 documents |
| `{research_root}` Research | `kb-area-research-skeleton` | `methodology/research/` 4 documents |
| `{specs_root}` Standards | `kb-area-standards-skeleton` | — |
| `{dashboard_root}` Dashboard | `kb-area-dashboard-skeleton` | `methodology/operations/` 8 documents: role, channel, engagement, task |
| `{inbox_root}` Inbox | `kb-area-inbox-skeleton` | `methodology/operations/kb-method-inbox-placement.md`, `methodology/operations/kb-method-inbox-archive.md` |
| `{personal_root}` Personal | `kb-area-personal-skeleton` | `methodology/personal/` 3 documents |

Areas without listed domain methodology are subject only to the common layer and their own directory skeleton. Content writing methodology for those areas is managed by other standards — workflows by the Agent Workflow Authoring standard, standard packages themselves by the Standard Authoring standard.

## Superseded Standards

Sixteen earlier standard packages were merged into this one. Their package IDs are retired and their source directories are archived. This table records what each retired package covered and where that content lives now, so an old reference can still be resolved.

| Retired Package Subject | Merged Into |
|----------------------|------------|
| Naming systems and directory organization | All of `naming/` + `directory/kb-directory-*` |
| Dual knowledge base mapping | `directory/kb-vault-architecture-mapping` |
| Index file authoring and area skeletons | `directory/kb-entry-*` + `directory/kb-area-*-skeleton` |
| Brand modeling | `methodology/brand/` (all 6 except persona) |
| AI persona modeling | `methodology/brand/kb-method-brand-persona.md` |
| Commerce direction scanning | `methodology/commerce/` |
| Business asset writing | `methodology/business/` |
| Research materials and interpretation | `methodology/research/` (all 3 except theory) |
| Theory-to-practice chain | `methodology/research/kb-method-research-theory.md` |
| Role protocol and channel operations | `methodology/operations/kb-method-dashboard-*` |
| Engagement strategy | `methodology/operations/kb-method-engagement-strategy.md` |
| Task management | `methodology/operations/kb-method-task-*` |
| Inbox placement and archiving | `methodology/operations/kb-method-inbox-*` |
| Personal domain writing | `methodology/personal/` |
| Best practice authoring | `methodology/tools/kb-method-practice-authoring.md` |
| Credential management | `methodology/tools/kb-method-credential-management.md` |

## Metadata

| Field | Value |
|------|-------|
| Status | Active |
| Last Updated | 2026-08-07 |
| Review | 2026-08-07 |

## Change Log

> Rolling window: keep 3 most recent entries, max 20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Package created, 16 legacy standards merged |
