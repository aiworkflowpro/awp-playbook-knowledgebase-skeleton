---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-operations
language: en
publication: public
title: "Business Methodology  -  Operations Directory"
---

# Business Methodology  -  Operations Directory

> Manage each business unit's operations directory: the eight-directory structure for website products, dimension pool and selection matrix for non-website channels, detailed writing for each dimension.
> Inherits all constraints from `kb-method-business-general.md`.

Business units include channels (official website, video platform, text subscription platform, image social platform, short video platform, code hosting platform, Q&A community, short-form social platform), products (courses, online services, physical products), storefronts, and applications. Each business unit has an operations directory under `{business_root}/{brand}/{unit}/operations/`.

## One. Eight Design Principles

- **One dimension pool, one matrix**: All business units select from the same dimension pool, not split by business type.
- **Directory name is dimension name**: Each subdirectory represents one operations dimension; name is self-explanatory.
- **Enable as needed**: Not every business model needs all dimensions; enablement conditions in the selection matrix.
- **Build skeleton first**: Website products have all eight directories pre-built at creation time, even if temporarily empty, maintaining consistent structure. Non-website channels still enable on-demand.
- **Time binding**: Dimensions with continuous output organize internally by `{YYYYMMDD}/` date directories.
- **Align with workflows**: When a dimension has a corresponding workflow, the directory name matches the workflow sub-stream name.
- **Composite attribution**: Operations directory is spatial aggregation; each internal file maintains independent classification (operational metrics, operational assets, project archive), not creating new top-level categories.
- **Dual classification metadata**: The operations directory index file's "classification" field reads as "operational metrics + operational assets".

## Two. Website Products: Unified Eight Directories

All website products (official website, online service site, product site, content site, regardless of tech stack) use the following eight-directory numbered structure, not dimension pool on-demand selection.

```text
{product_name}/
├── CLAUDE.md
├── 01-product-definition/   Product positioning, target users, core use cases, roadmap
├── 02-payment-collection/   Pricing, payment channels, order processing, post-sale boundaries
├── 03-search-optimization/  Complete search optimization: index submission, keywords, indexing audit, internal links, backlinks
├── 04-content-operations/   Topic pool, scheduling, publishing cadence, content architecture
├── 05-growth-promotion/     Publishing growth, paid placement, backlinks, channel experiments, conversion funnel
├── 06-operations-data/      Core metrics, competitor monitoring, periodic post-mortems
├── 07-customer-feedback/    User feedback, waitlist, support records, feature requests
└── 08-asset-evidence/       Screenshots, audit reports, test records, validation evidence, deployment operations
```

### Deployment and Runtime Placement

| What to Place | Location |
|--------|------|
| Tech stack summary, endpoint status, main site legal presentation | Official website or product root `CLAUDE.md` |
| Long-form troubleshooting, incident archives, health check logs | `08-asset-evidence/` (website products), or channel operations evidence folder |
| Orchestration files, reverse proxy config, deployment scripts | Deployment code repo or product source repo |
| Region codes, tokens, keys | Credential library, credentials only |

Prohibited: creating a brand-level operations total repo under the brand business root.

### Applicable Scope

- Applicable: official website, online service product site, tool site.
- Not applicable: non-website channels (video platform, text subscription platform, short-form social platform, code hosting platform), which use the dimension pool below.

### Naming of management documents inside the eight directories

Management documents in `01` through `08` use File Naming Segment Convention §5 (three hyphens):

```text
{type}-{dimension}-{topic}-{scope}.md
```

| Slot | Holds | Values |
|------|--------|--------|
| type | Nature of the file | `plan` · `status` · `strategy` · `judgment` · `report` · `list` · `record` · `data` · `retro` · `guide` · `constraint` · `schedule` · `ledger` |
| dimension | Operations dimension | `product` · `checkout` · `SEO` · `keyword` · `content` · `growth` · `email` · `ops` · `competitor` · `tech` · `theme` · `incident` · `traffic` · `index` · `backlink` · `experience` · `conversion` · `retro` · `audit` · `citation` · `strategy` · `data` |
| topic | What the file is about | Concatenate words; no hyphen inside a slot |
| scope | Coverage or date | `general` for standing docs; dated reports use `YYYYMMDD` |

Hard rules:

- A management document must have exactly three hyphens.
- Dates use the compact form and sit in the fourth slot.
- Fixed entries stay: `CLAUDE.md` · `description.md` · `ghost-awp.md` · `ghost-xy.md`.
- External dumps (`csv` / `xlsx` / `json` / sitemap) keep the original name.
- `content/` follows the live site slug and does not use this table.
- Workflows that write into these directories must use this table. Short zero-hyphen names such as `positioning.md` or `summary.md` are not allowed.

## Three. Dimension Pool

14 standard dimensions available for operations directories plus industry-specific extensions.

| # | Dimension | Directory | Responsibility | Enable Condition | Classification |
|---|------|--------|------|---------|---------|
| 1 | Data | `data/` | Core metrics by date archive | Required for all | Operational Metrics |
| 2 | Competitors | `competitors/` | Competitive intelligence by subject archive | Required for all | Operational Assets |
| 3 | Content Planning | `content-planning/` | Topic pool + schedule | Required if continuous content output | Operational Assets |
| 4 | Positioning | `positioning/` | Goals, audience, differentiation | Required if independent external identity | Operational Assets |
| 5 | Search Optimization | `search-optimization/` | Platform in-search optimization | Required when search traffic ≥20% | Operational Assets |
| 6 | Promotion | `promotion/` | Paid placement + cross-channel acquisition | Required if paid promotion or active acquisition | Operational Assets |
| 7 | Conversion | `conversion/` | Business result tracking | Required if clear conversion path | Operational Metrics |
| 8 | Post-mortem | `retrospective/` | Periodic review | Required when operations rhythm stable (monthly or higher) | Operational Metrics |
| 9 | Growth Experiments | `growth-experiments/` | Hypothesis validation records | Required if active growth need | Project Archive |
| 10 | Product Definition | `product-definition/` | Positioning, pricing, delivery, entry | Required if sellable product | Operational Assets |
| 11 | Course Design | `course-design/` | Structure, scope, path, promise | Required if course or educational product | Operational Assets |
| 12 | Purchase Path | `purchase-path/` | Conversion funnel, trial, objection handling | Required if paid product | Operational Assets |
| 13 | Learner Operations | `learner-operations/` | Community, case studies, Q&A | Required if community or Q&A mechanism | Operational Assets |
| 14 | Sales Materials | `sales-materials/` | Value props, evidence, talking points | Required if multi-channel acquisition | Operational Assets |
| — | Industry-specific | `{specific_name}/` | Industry-unique operations mechanism | See below | Operational Assets |

### Industry-Specific Dimensions

Only create industry-specific directories when a business model has unique operations mechanisms not covered by the 14 standard dimensions. Use industry's own terminology, self-explanatory. Examples:

| Business Model | Specific Directory | Manages |
|------|---------|--------|
| Video Platform | `channel/` | Playlists, end screens, community pages, short video strategy |
| Short Video Platform | `collections/` | Series collections management + placement experiments |
| Code Hosting Platform | `repositories/` | Repository facade strategy, README, topic tags |

No industry-specific directories for models without unique mechanisms.

### Standard Skeleton

```text
{business_unit}/operations/
├── CLAUDE.md              ← Required: dimension index, tool binding, trigger words
├── data/                  ← ① Core metrics
├── competitors/           ← ② Competitive intelligence
├── content-planning/      ← ③ Topics + schedule
├── positioning/           ← ④ Goals & audience
├── search-optimization/   ← ⑤ Search optimization
├── promotion/             ← ⑥ Paid placement
├── conversion/            ← ⑦ Business results
├── retrospective/         ← ⑧ Periodic review
├── growth-experiments/    ← ⑨ Hypothesis validation
├── product-definition/    ← ⑩ Product archive
├── course-design/         ← ⑪ Course structure
├── purchase-path/         ← ⑫ Purchase funnel
├── learner-operations/    ← ⑬ Community Q&A
├── sales-materials/       ← ⑭ Value props/talking points
└── {industry_specific}/   ← As-needed extension
```

Only create dimensions marked "required" in the matrix or "optional" and actually needed; don't create the rest.

## Four. Business Model Dimension Selection Matrix

One table covers all business models. Markings: Required = must have, Optional = as-needed, — = not applicable.

| Dimension | Official | Video | Text Sub | Image Social | Short Video | Code Hosting | Q&A | Short Social | Course | Online Svc | Physical |
|------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Data/ | Required | Required | Required | Required | Required | Required | Required | Required | Required | Required | Required |
| Competitors/ | Required | Required | Required | Required | Required | Optional | Optional | Optional | Required | Required | Required |
| Content Planning/ | Required | Required | Required | Required | Required | Required | Required | Required | Required | Optional | — |
| Positioning/ | Required | Required | Required | Required | Required | Required | Required | Required | Optional | Optional | Optional |
| Search Optimization/ | Required | Required | Required | Required | Required | Required | Required | — | — | — | — |
| Promotion/ | Required | Required | Optional | Optional | Required | — | — | — | Optional | Optional | Optional |
| Conversion/ | Required | Required | Required | Required | Required | Required | Optional | Optional | Optional | Optional | Optional |
| Post-mortem/ | Required | Required | Optional | Optional | Optional | Optional | — | — | Optional | Optional | Optional |
| Growth Experiments/ | Optional | Optional | Optional | Optional | Optional | Optional | — | — | Optional | Required | Optional |
| Product Definition/ | — | — | — | — | — | — | — | — | Required | Required | Required |
| Course Design/ | — | — | — | — | — | — | — | — | Required | — | — |
| Purchase Path/ | — | — | — | — | — | — | — | — | Required | Required | Required |
| Learner Operations/ | — | — | — | — | — | — | — | — | Optional | — | — |
| Sales Materials/ | — | — | — | — | — | — | — | — | Optional | Optional | Optional |
| Channel/ | — | Required | — | — | — | — | — | — | — | — | — |
| Collections/ | — | — | — | — | Required | — | — | — | — | — | — |
| Repositories/ | — | — | — | — | — | Required | — | — | — | — | — |

## Five. Search Optimization Dimension Platform Differences

Same "search optimization" dimension has different internal structure across platforms.

### Official Website (General Search Engines)

Contains 10 workflow subdirectories, driven by continuous operations workflow:

```text
search-optimization/
├── 01-strategy-positioning/
├── 02-data-collection/
├── 03-traffic-diagnosis/
├── 04-indexing-audit/
├── 05-keyword-planning/
├── 06-content-planning/
├── 07-backlink-management/
├── 08-retrospective-archive/
├── 09-page-experience/
└── 10-conversion-analysis/
```

`search-optimization/` only manages search optimization's 10 subflows. Positioning, data, content planning, competitors, conversion, post-mortem remain as standard dimensions with separate directories.

### Video Platform

```text
search-optimization/
├── keywords/              ← Video title keyword strategy
├── title-optimization/    ← Title A/B test records
└── timestamps/            ← Chapter marking strategy
```

### Text Subscription Platform

```text
search-optimization/
├── keywords/              ← Platform search hot words + article title coverage
└── optimization-log/      ← Title rewrites + effect tracking
```

### Image Social Platform

```text
search-optimization/
├── keywords/              ← Platform trending terms + note title coverage
└── save-optimization/     ← Save-rate uplift strategy + image info density
```

### Short Video Platform

```text
search-optimization/
├── keywords/              ← Search trending + video title coverage
└── collection-optimization/  ← Collection title keywords + completion rate optimization
```

### Code Hosting Platform

```text
search-optimization/
├── keywords/              ← README target keywords
└── topic-tags/            ← Repository tag strategy
```

### Q&A Community

```text
search-optimization/
├── keywords/              ← External search trends + site hotlist
└── answer-strategy/       ← Word count, timeliness, engagement window
```

## Six. Data Dimension Industry Differences

| Business Model | Core Metrics | Data Source | Pull Method |
|------|---------|---------|---------|
| Official Website | Clicks, impressions, CTR, rankings, sessions | Search console, website analytics tool, keyword data service | Command-line automation |
| Video Platform | Subscribers, views, watch time, engagement rate, traffic source | Platform data API | Command-line automation |
| Text Subscription Platform | Followers, reads, read completion, forwards, recommendations | Platform backend | Semi-automatic |
| Image Social Platform | Followers, saves, engagement, search traffic | Platform backend | Manual |
| Short Video Platform | Followers, views, completion rate, forwards, comments | Platform backend | Manual |
| Code Hosting Platform | Stars, forks, clones, page views | Platform data API | Command-line automation |
| Q&A Community | Followers, reads, upvotes, saves | Platform backend | Manual |
| Short-form Social Platform | Followers, engagement, forwards, quotes | Platform data API | Command-line automation |
| Course | Learners, content pieces, sales per channel, update frequency | Platform backends | Manual |
| Online Services | MAU, DAU, retention, MRR, churn rate, revenue per user | Product backend + payment provider | Command-line automation |
| Physical Products | GMV, order count, conversion rate, average order value, return rate | E-commerce backend | Semi-automatic |

Data directories can use single file `dashboard.md` (small data volume) or date-archive subdirectories (large volume), not enforced. Dashboard files must end with the data refresh command, either in code block or manual steps.

## Seven. Conversion Dimension Industry Differences

| Business Model | Conversion Goal | Tracking Method |
|------|---------|---------|
| Official Website | Product purchase (in-site or external) | Website analytics tool checkout initiation event |
| Video Platform | Video to product link clicks | Platform cards + end screens click + source params |
| Text Subscription Platform | Article to product entry or group join | Original link clicks + QR code scans |
| Image Social Platform | Note to DM or subscription account acquisition | DM keyword stats |
| Short Video Platform | Video to monetization entry | Platform backend conversion data |
| Code Hosting Platform | README to official website or product link | Source param tracking |
| Course | User journey from awareness to payment | Managed with `purchase-path/` |
| Online Services | Registration → trial → paid | Product backend funnel |
| Physical Products | Browse → add to cart → purchase | E-commerce backend conversion data |

## Eight. Dimension Deep Dive: Course Design

Manages course product structure design — how to organize content so users perceive value and are willing to pay.

Required documents:

| File | Responsibility | Required Fields |
|------|------|---------|
| `free-paid-boundary.md` | Clarify which content is free lead-gen, which is paid-only | Free tier scope, paid tier exclusive value, boundary rationale |
| `learning-path.md` | Split into 3–5 paths for user goals, each 15–20 pieces | Path name, target users, course list, estimated hours, outcome promise |
| `outcome-promise.md` | Concrete outcomes per path after completion | Path name, verifiable outcome descriptions (specific deliverable, not abstract skills) |

Optional documents:

| File | Enable Condition |
|------|---------|
| `update-cadence.md` | Course continuous updates: define what, how often, how users perceive |
| `content-tiers.md` | Course multiple tiers (basic/advanced/expert): define each tier scope |

Course design directory does not hold course content — content lives in `content/`. This holds design decisions and structure planning.

## Nine. Dimension Deep Dive: Purchase Path

Manages user journey from "knowing this product exists" to "paying" complete link design.

Required documents:

| File | Responsibility | Required Fields |
|------|------|---------|
| `conversion-funnel.md` | Draw complete path's each stage | Stage name, user action, conversion friction, design to reduce friction |
| `trial-design.md` | Let users experience paid content before payment | Trial content selection criteria, trial scope, trial entry location |
| `hesitation-points.md` | Buyer hesitation points and resolution strategies | Hesitation point, frequency, resolution strategy, corresponding materials |

Typical funnel stages:

```text
Free content (various acquisition channels)
  → Trial experience (free sample or mini course)
    → Product page (details + student cases + outcome showcase)
      → Purchase
        → Onboarding guide (learning path recommendations)
```

## Ten. Dimension Deep Dive: Product Definition

Boundary:

- Software product from concept to launch is product fact source, following product development methodology, not in operations directory.
- Operations directory `product-definition/` only takes operations-side info: positioning, pricing, delivery, entry, rights, purchase path.
- When product fact source and operations directory conflict, product fact source is authoritative; operations directory only references and operational sedimentation.

Required fields:

| Field | Description |
|------|------|
| Positioning | One-line product positioning |
| Pricing | Price per platform |
| Delivery Form | Online / download / hybrid |
| Purchase Entry | Links per platform |
| Content Scope | Number of pieces or modules |
| Service Scope | What's included, what's not |

## Eleven. Dimension Deep Dive: Learner Operations

Enable when community or Q&A mechanism exists.

| File | Responsibility |
|------|------|
| `community-strategy.md` | Community operations rules, activity maintenance approach |
| `faq.md` | Frequently asked questions and standard responses; continuous sedimentation |
| `learner-cases.md` | Real student outcomes using course content; strongest sales evidence |
| `completion-tracking.md` | Student completion path and bottleneck analysis |

## Twelve. Dimension Deep Dive: Sales Materials

Enable for multi-channel acquisition. Store materials directly reusable across channels.

| File | Responsibility |
|------|------|
| `selling-points.md` | 5–8 core value props, each with one-liner + evidence |
| `learner-stories.md` | Stories distilled from student cases, anonymized for publication |
| `copy-templates.md` | Copy templates for each channel |

## Thirteen. Dimension Deep Dive: Growth Experiments

Enable on-demand when active growth need exists.

Must include `template.md`, standardizing experiment format:

```markdown
# Experiment: {experiment_name}

| Field | Value |
|------|---|
| Code | {prefix}-{NNN} |
| Hypothesis | If {intervention}, then {metric} will {change}, because {mechanism} |
| Core Metric | {single measurement metric} |
| Period | {start} to {end} |
| Status | Design / In Progress / Completed / Abandoned |

## Experiment Design
## Data Comparison
## Conclusion & Next Steps
```

Three requirements:

- Hypothesis must use three-part format: if X, then Y, because Z.
- Completed experiments must have conclusion section, stating verification or refutation, plus next step.
- No hypothesis = not an experiment; doesn't belong in this directory.

## Fourteen. Dimension Deep Dive: Competitors

One file per observed entity. Skeleton:

| Section | Content |
|------|------|
| Subject Info | Name, scale, positioning, why observe |
| Observation Dimensions | By business model selection, see table below |
| Discovery Log | Date, subject, finding, actionable insight |

Industry observation dimension table (reference, not exhaustive):

| Business Model | Recommended Observation Dimensions |
|------|------------|
| Content Creation | Topics, titles, covers, duration, frequency, engagement strategy, monetization model |
| E-commerce | Pricing, details page, reviews, promotions, logistics, service, visual |
| Online Services | Features, pricing, docs, community, release frequency, acquisition channels |
| Education & Courses | Curriculum, pricing, instructors, reputation, acquisition, completion rate, free content scope, piracy routes |
| Offline Services | Location, decor, service, price, membership, reputation |

## Fifteen. Dimension Deep Dive: Content Planning

Required for business units with continuous content output.

```text
content-planning/
├── topic-pool.md        ← All candidate topics; continuously maintained
├── schedule.md          ← Confirmed production schedule for current cycle
└── source-routing.md    ← Translation/adaptation source file correspondence (optional)
```

### `topic-pool.md` Required Fields

| Column | Meaning |
|----|------|
| Topic | Title or theme description |
| Source | Original / Translation / Adaptation |
| Target Keywords | Primary search keywords (if applicable) |
| Priority | P0 / P1 / P2 |
| Status | Under Evaluation / Scheduled / Completed / Abandoned |

### `schedule.md` Required Fields

| Column | Meaning |
|----|------|
| Week or Date | Target publication date |
| Topic | From topic pool |
| Type | Tutorial / Comparison / Quick Reference / Guide |
| Source | Original / Translation (note source path) |
| Status | Scheduled / In Production / Awaiting Review / Awaiting Publication / Published |

Published entries remain in schedule and marked as status, not deleted. Entries over 3 months old can move to "History" section at schedule end.

### `source-routing.md` Required Fields

Required for business models with translation/adaptation needs.

| Column | Meaning |
|----|------|
| Topic | Corresponds to topic in schedule |
| Source Path | Original file absolute path |
| Coverage | Complete Coverage / Partial Coverage / Inspiration Only |
| Supplementary | Original missing content target version needs |

## Sixteen. Operations Directory Index File Template

```markdown
# {business_unit}  -  Operations

> {One-sentence positioning}
> Methodology → Business Methodology  -  Operations Directory

## Metadata

| Field | Value |
|------|---|
| Classification | Operational Metrics + Operational Assets |
| Maintenance Frequency | {Weekly / Monthly / Quarterly} |
| Created | {YYYYMMDD} |

## Dimension Index

| Dimension | Directory | Classification | Status | Description |

## Tool Binding

| Purpose | Tool | Core Command |
|------|------|---------|

## Trigger Words

{business_unit} operations, {business_unit} data

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.
```

## Seventeen. Deduplication Boundaries

| Content | Belongs To | Does Not Belong To |
|------|------|------|
| Operational data aggregate | `data/` | Parent directory index file |
| Strategy and tactics | Corresponding dimension directory | Parent directory scattered files |
| Single growth experiment | `growth-experiments/{experiment}.md` | Data directory (reference conclusion only) |
| Cross-unit aggregate | Business root index file | Single operations directory |
| Business unit overall archive | Parent directory index file | Operations directory |
| Specific operation steps | Workflow library | Operations directory (reference only) |
| Course content | `content/` | Operations directory |
| Cross-channel `content_id` | Content registry | Operations directory |

## Eighteen. Checklist

**New website product directory (eight-directory structure)**

- [ ] All eight numbered directories pre-built, allowed to be temporarily empty
- [ ] Index file contains: eight subdirectory index, original file index, tool binding table, trigger words
- [ ] Parent directory index file has entry row for product directory
- [ ] `03-search-optimization/` contains search engine index submission status table covering all search engines

**New non-website channel operations directory (dimension pool structure)**

- [ ] `operations/` directory created under corresponding business unit
- [ ] Index file contains: dual-classification metadata, dimension index with classification column, tool binding table, trigger words
- [ ] Enable required dimensions for this business model per matrix
- [ ] Parent directory index file has entry row for operations directory
- [ ] Trigger words follow `{business_unit} {action_verb}` pattern

**Dimension content checks**

- [ ] Data dimension contains dashboard or first data snapshot
- [ ] Competitors dimension contains at least one subject file
- [ ] Content operations dimension contains topic pool + schedule
- [ ] Search optimization dimension contains index submission status (website products required)

**Maintenance**

- [ ] Data snapshot not older than 30 days
- [ ] Schedule status matches actual production progress
- [ ] Topic pool regularly cleaned of abandoned entries
- [ ] Competitors have recent discovery records
- [ ] Tool binding matches actual tools

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-15 | Eight-dir docs use four-seg |
| 2026-08-07 | Migrated from operations directory specification and generalized |
