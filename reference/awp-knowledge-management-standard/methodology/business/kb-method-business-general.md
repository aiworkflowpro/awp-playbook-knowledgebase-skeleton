---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-general
language: en
publication: public
title: "Business Methodology  -  General Principles"
---

# Business Methodology  -  General Principles

> Manage how business assets classify, how to tag them, how to cross-reference. Applies to any industry, any organization size.
> Does not manage specific business (which product, which customer, what price), nor specific how-to (how film video, how upload, how file taxes)—latter belongs to workflows.

## I. Role Names and Paths

This methodology suite does not hard-code any directory paths. These role names have fixed meaning across all business methodology documents; when deployed, map to your organization's actual locations.

| Role | Stores |
|------|--------|
| Business Root | Total directory for all operations assets |
| Brand Root | Brand strategy, operations, identity, content |
| Workflow Library | Standard operation procedures and method notes |
| Credential Library | API keys, accounts, certificates |
| Experience Library | Technology selection, decision records, pitfall records |
| Research Area | Undeployed planning proposals |
| Research Library | Topic materials and reference materials |
| Visual Asset Library | Logos, covers, usage images |
| Personal Area | Private matters unrelated to business |

Path examples use form `{business_root}/{brand}/{channel}/`; braces are slots filled with your actual names.

## II. Two Dimensions

Every business asset carries two things simultaneously:

```text
Business Asset = Primary Classification (7 types, single choice) × Facet Label (7 facets, multi-choice)
                 ─────────────────────   ──────────────────────
                 Determines directory     Determines search and filter
                 skeleton shape
```

Primary classification alone cannot say "this project is both a project record, produces tangible output, and is in e-commerce." Only labels fail—assets of same class each write separately, no uniform skeleton. Use both together.

Facet means "one side of an asset." An asset has 7 sides; each side picks one or more values.

## III. Seven Primary Classifications (Single Choice)

| # | Type | Definition | Typical Assets | Details |
|---|------|-----------|-----------------|---------|
| 1 | Project Planning | End-to-end planning from 0 to 1 | New track planning, new product kickoff, new site plan | `kb-method-business-planning.md` |
| 2 | Project Record | One-time deliverable with start/end | Single video, article, course, consultation, engineering project | `kb-method-business-archive.md` |
| 3 | Operating Asset | Continuously-maintained live resource | Website content, products for sale, retail locations, equipment, content section | `kb-method-business-asset.md` |
| 4 | Customer Relationship | External stakeholder record | Customer, student, supplier, partner, subscriber | `kb-method-business-customer.md` |
| 5 | Strategic Decision | Single major decision + long-term retrospective | Pricing, pivot, expansion, selection, strategic shift | `kb-method-business-decision.md` |
| 6 | Operations Data | Periodic indicators and reports | Daily, weekly, monthly, quarterly, annual reports, metric dashboard | `kb-method-business-metrics.md` |
| 7 | Event Archive | One-time activity complete record | Launch, conference, promotion, crisis, activity | `kb-method-business-event.md` |

Primary classification is asset **type label**, not seven parallel folders under business root. Physical directory layout by brand, channel, product; type goes in asset metadata.

## IV. Seven Facets (Multi-Choice, Controlled Vocabulary)

| Facet | Possible Values | Function |
|-------|-----------------|----------|
| Brand | Brand directory name | Brand routing |
| State | Planning / In Progress / Pending Release / Published / Archived / Concluded | Lifecycle filter |
| Output Form | Text / Audio-Video / Picture-Text / Physical / Service / Data Report / Code / Relationship Contract / Mixed / Other | Physical form filter |
| Industry | Content Creation / E-Commerce / Software Service / Consulting / Education / Healthcare / Building / Manufacturing / Retail / Finance / Law / Food Service / Logistics / Agriculture / Nonprofit / Other | Industry filter |
| Business Type | Organization-defined label | Business type filter |
| Corresponding Workflow | Point to workflow library file, or "None" | Link dynamic process |
| Owner | Individual / Team-{role} / Outsourced / Partner | Accountability filter |

Two hard rules:

- Values only from above table. Output Form and Business Type allow extension, but extended vocabulary must be consistent within organization.
- Prohibit synonym variants. "Complete" writes as "Archived" or "Concluded," not "done," "Done," "finished."

### Business Type Value Set

Business type names per organization's business context; this methodology does not mandate. Example: content creation industries often use: long-form video, short-form video, podcast, long-form text, course, livestream, column. Other industries apply the same thinking.

## V. Nine-Field Metadata

Every project or asset has an explanatory file (project record calls it `project.md`, operating asset calls it `asset.md`, by classification), with this table at start:

```markdown
| Field | Value |
|-------|-------|
| Classification | Project Planning / Project Record / Operating Asset / Customer Relationship / Strategic Decision / Operations Data / Event Archive |
| State | Planning / In Progress / Pending Release / Published / Archived / Concluded |
| Output Form | {Controlled vocabulary value} |
| Industry | {Controlled vocabulary value, or "Other"} |
| Business Type | {Organization-defined label} |
| Corresponding Workflow | → {workflows_root}/{workflow_file}, or "None" |
| Owner | {Individual / Team role / Outsourced} |
| Created | YYYYMMDD |
| Updated | YYYYMMDD |
```

Nine fields = classification + six written Facets + creation date + update date. Seventh Facet "Brand" expressed by path itself, not a separate row.

Rules:

- State changes, simultaneously update "Updated" date.
- State changes to "Published," trigger handoff (see Section VII).
- Every Facet must be present. Business Type and Corresponding Workflow can fill "None," but field row must exist.

## VI. Three-Layer Section Stacking

Every business asset has three section layers:

```text
① Required Sections—all industries, all types must fill
② Recommended Sections—most types apply; absence requires explanation
③ Industry-Optional—add per industry; use slots not redefine required sections
```

Each classification's details file declares its own three-layer boundaries. Industry-optional sections only add content inside required sections, never create top-level chapters or replace required ones.

## VII. Handoff Rules

Business area is internal perspective, external sedimentation in other domains. Both connect via cross-reference, not content duplication or file moving.

```text
Business (Internal Perspective)              External Domain (External Sedimentation)
─────────────────────────────────────────────────────────────────────
Project Record  -  Published    ──cross-ref──→  Channel Operations Area (external item, not copy)
Operating Asset  -  For Sale    ──reference───→ Product Root / Product Definition
Operating Asset  -  Ongoing     ──reference───→ Channel Operations Area
Customer Relationship  -  Audience ──associate→ Target Audience Area / Audience Persona
Customer Relationship  -  Private  ──move───→   Personal Area
Strategic Decision  -  Brand      ──reference──→ Brand Operations Area / Business Model
Strategic Decision  -  Personal Finance ──move→ Personal Area Finance
Operations Data  -  Aggregate     ──reference──→ Brand Operations Area / Business Model (revenue)
Event Archive  -  Reusable Material ──sediment→ Visual Asset Library + Research Library
All Classifications  -  Workflow Reference ──point→ Workflow Library
All Classifications  -  Credential Reference ──point→ Credential Library
All Classifications  -  Decision Tool ──point→ Experience Library
```

### Three Product Locations

One product exists in three places, each stores separately:

| Location | Perspective | Stores | Who Reads |
|----------|-------------|--------|----------|
| `{business_root}/{brand}/{business_type}/{project}/` | Creation and Reference | Production process, publishing materials, version decisions, source files | When needing creation reference |
| `{business_root}/{brand}/products/` | Product Fact | Product definition, pricing, benefits, roadmap | When answering product, pricing, member rights |
| `{business_root}/{brand}/{channel}/operations/` | Channel Fact | Account, publication strategy, data snapshot, channel investment | When answering channel and data |

### Four Cross-Reference Requirements

- Product fact has one canonical copy in product directory.
- Project Record state to "Published" must create cross-reference entry in corresponding channel operations directory—only title, link, date metadata.
- Operating asset goes on-sale must create product definition file in product directory.
- Both sides point via project ID or path field.

### Four Cross-Reference Prohibitions

- Do not duplicate content. Product definition, channel data, promotion link cannot replicate in brand layer.
- Do not physically move. State to "Published" does not trigger any file movement.
- Do not "published but channel operations has no external entry"—external perspective loses a piece.
- Do not conflate "mirror" with "copy." Mirror only means cross-reference.

## VIII. Naming Conventions

Segment count and separator rules by `../../naming/kb-naming-segment-convention.md`. This section names each primary type uses.

| Type | Naming Pattern | Example Slots |
|------|----------------|--------------|
| Project Record | `{sequence}-{type}-{title}/` (directory) | `{sequence}-{type}-{title}/` |
| Operating Asset | `{asset_name}/` or `{asset_name}.md` | `{asset_name}.md` |
| Customer Relationship | `{individual_name}.md` or `{relationship_type}/{individual_name}.md` | `{customer_name}.md` |
| Strategic Decision | `decision-{topic}.md` | `decision-{topic}.md` |
| Operations Data | `{metric_type}-{period}.md` | `{report_type}-{year_month or week}.md` |
| Event Archive | `{event_name}-{year_month}.md` | `{event_name}-{YYYY-MM}.md` |

Three taboos:

- Pure date prefix prohibited. `2026-04-{file}.md` becomes `{file}-2026-04.md`.
- Meaningless ID prohibited. `doc1.md` becomes meaningful name.
- Mixed separators prohibited. Use `-` uniformly.

### Content Directory Naming Universal Rule

All channel content directories start `{YYYYMMDD}-`, date always **publication date** (see `kb-method-business-article.md § Directory Name Date Extraction` for order). After date, per channel:

| Channel Type | After Date |
|--------------|-----------|
| Text subscription, member platform | Four-part short name `{tool}-{topic}-{angle}` |
| Website | `{slug}`, matches URL |
| Text social, video | `{sequence}-{title_keywords}` |
| Course unit | 1–3 fields coarse-to-fine, no forced four-part |

## IX. Output Lookup Table

Unsure which type applies? Look by output type.

### Creation and Content

| Output | Type | Explanation |
|--------|------|-------------|
| Long video, short video, podcast, livestream archive | Project Record | Single delivery |
| Article, essay, short, column | Project Record | Single delivery |
| Course, bootcamp, book | Project Record | Single delivery |
| Ongoing channel or content section | Operating Asset | Continuous operation |

### Products and Physical

| Output | Type | Explanation |
|--------|------|-------------|
| New product R&D, prototype | Project Record | R&D phase |
| Product on-sale | Operating Asset | Continuous sale |
| Product iteration version | Project Record → Operating Asset | State transition |

### Software and Technology

| Output | Type | Explanation |
|--------|------|-------------|
| Feature development, version | Project Record | Single delivery |
| Online service, API, running system | Operating Asset | Continuous operation |
| Open-source project | Project Record + Operating Asset | By activity |
| Technology architecture decision | Strategic Decision | — |

### Engineering and Construction

| Output | Type | Explanation |
|--------|------|-------------|
| Single engineering project | Project Record | Start/end |
| Continuously-maintained asset or equipment | Operating Asset | Continuous care |
| Tender, selection decision | Strategic Decision | — |

### Service and Delivery

| Output | Type | Explanation |
|--------|------|-------------|
| Consulting, delivery case | Project Record | Single delivery |
| Ongoing service (subscription, outsource) | Operating Asset | Continuous delivery |
| Customer, student, patient record | Customer Relationship | — |

### Documents and Contracts

| Output | Type | Explanation |
|--------|------|-------------|
| Contract, agreement, memorandum | Customer Relationship | Relationship attribute |
| Legal document, litigation file | Project Record (single) or Customer Relationship | By purpose |
| Medical prescription, patient record | Project Record or Customer Relationship | High privacy |

### Data and Reports

| Output | Type | Explanation |
|--------|------|-------------|
| Daily, weekly, monthly, quarterly, annual | Operations Data | Periodic |
| Metric dashboard | Operations Data | Continuous |
| One-time research report, analysis | Project Record | Single |

### Activity and Events

| Output | Type | Explanation |
|--------|------|-------------|
| Launch, conference, summit | Event Archive | One-time |
| Promotion, activity, ceremony | Event Archive | One-time |
| Crisis, major announcement | Event Archive | One-time |

### Decision and Strategy

| Output | Type | Explanation |
|--------|------|-------------|
| Strategic shift, pricing adjustment | Strategic Decision | Single |
| Investment, acquisition decision | Strategic Decision | Single |
| Organization and personnel major decision | Strategic Decision | Single |

Items not in table: first fit nearest, then decide if classification extension needed. **Do not create primary type for single business type.**

## X. Lifecycle and Retrospective Cadence

| Type | Cadence | Trigger |
|------|---------|---------|
| Project Record | After finish + quarterly batch | One week post-publication retrospective, quarterly review all |
| Operating Asset | Monthly check | State change or data update |
| Customer Relationship | Quarterly refresh | Relationship still active? |
| Strategic Decision | Quarterly | Still valid? Adjust needed? |
| Operations Data | Per period | Daily/weekly/monthly/quarterly/yearly per schedule |
| Event Archive | Immediately after | One week post-event retrospective |

## XI. Cascade Check

Modify left side, check right side.

| Modified | Check |
|----------|-------|
| Project state to "Published" | Channel operations directory has external entry? |
| Operating asset product launch | Product directory has product definition? |
| Strategic decision pricing change | Product definition and business model sync needed? |
| Operations data month report released | Business model revenue source needs update? |
| Customer relationship from business to personal | Move to personal area needed? |
| Any asset "Corresponding Workflow" reference | Referenced workflow file exists? |

## XII. Checklist

**New Business Asset (Universal)**

- [ ] Metadata contains nine fields
- [ ] Primary classification fits definition (judge against seven types)
- [ ] Facet values from controlled vocabulary
- [ ] Business type self-defined or filled "None"
- [ ] Corresponding workflow cross-referenced or filled "None"
- [ ] Naming fits this type's pattern

**Project Record Type**

- [ ] Three-phase skeleton (production / publication / archive) directories exist
- [ ] `project.md` includes milestones
- [ ] State "Published" created cross-reference in channel operations directory

**Operating Asset Type**

- [ ] In-use state clear
- [ ] Maintenance frequency declared
- [ ] Data update date not older than 30 days

**Customer Relationship Type**

- [ ] Relationship type declared
- [ ] Activity level clear
- [ ] Complete contact info and ID documents not in knowledge base

**Strategic Decision Type**

- [ ] Context, reality, options, decision, rationale, retrospective date complete
- [ ] No process stream detail

**Operations Data Type**

- [ ] Period clear
- [ ] Data source traceable
- [ ] Cross-period comparable

**Event Archive Type**

- [ ] Planning, execution, retrospective three phases complete
- [ ] Reusable material sedimented to visual asset library or research library

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Extracted from business spec and generalized |
