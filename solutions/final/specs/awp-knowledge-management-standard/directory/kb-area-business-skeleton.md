---
document_id: awp-knowledge-management-standard/directory/kb-area-business-skeleton
language: en
publication: public
title: "Knowledge Base Business/ Directory Skeleton"
---

# Business/ Directory Skeleton

> Defines the subdirectory structure of the `{business_root}` directory, the organizational modes it uses, and its customization interface.

## Responsibilities

This area hosts the ground-level operation of products and channels: what to sell, where to publish, what was published, what the data show, and how scheduling is arranged. The brand layer governs "who we are and how we speak"; the business layer governs "what we did and what the results look like."

## Directory Structure

```text
{business_root}
├── CLAUDE.md                  ← Fixed; cross-brand entry point with a synthesis dashboard
└── {brand_name}/              ← One directory per brand
    ├── CLAUDE.md              ← Fixed; entry point for this brand's business
    ├── products/              ← Fixed; index of product originals
    │   └── {product_name}/
    ├── content-registry/      ← Optional; cross-channel content ID mapping
    ├── {channel_name}/        ← One per channel, e.g., official-site / YouTube / X
    │   ├── CLAUDE.md
    │   ├── content/           ← Required; originals of deliverables (X and GitHub: see exception)
    │   ├── operations/        ← Required; data and growth
    │   └── schedule/          ← Optional; build only with continuous production
    └── {large_volume_product}/ ← Optional; promoted from products/ to the brand root
```

- The path variable `{business_root}` is declared in `{specs_root}layout.yaml`.
- The brand root has only three kinds of first-level subdirectories: **channels**, **products**, and **content registry**. Categorize a new directory before creating it.
- The brand root holds no loose files other than `CLAUDE.md`.
- Cross-brand summaries go only in `{business_root}CLAUDE.md`; do not create another copy at the brand level.

### Three Kinds of First-Level Subdirectories

| Type | Naming | Contents | Criterion |
|------|--------|----------|-----------|
| Channel | Platform name (official-site / YouTube / X / GitHub ...) | Workspace for external publishing or distribution | There is external publishing activity |
| Product | `products/` index; large-volume products may be promoted to the brand root | Definition and workspace of a sellable product | There is pricing and paid activity |
| Content Registry | `content-registry/` | Cross-channel content ID mapping table | The same content appears on two or more channels |

When a directory satisfies both the channel and the product criteria, classify it by its primary responsibility. `content-registry/` is an independent third type; it cannot be merged into any channel or product directory.

### Internal Skeleton of a Business Unit

Every channel or business-form directory uses the same set of three subdirectories (X and GitHub units expand type directories instead of `content/`):

```text
{business_unit}/
├── CLAUDE.md          ← Index
├── content/           ← Required; one directory per content unit
├── operations/        ← Required; data → competitors → growth experiments
└── schedule/          ← Optional; topic pool → schedule table → source routing
```

| Subdirectory | Timing | Responsibility |
|--------------|--------|----------------|
| `content/` | In-progress | Originals of content units |
| `operations/` | After-the-fact | Monitoring and growth, ongoing |
| `schedule/` | In-progress | Production scheduling |

Up-front research and plan design do not land here; they go into `{dashboard_root}research/{YYYYMM}/`. Only what grows out of a plan after it has been proven out enters the business unit.

### Operations Dimension Pool

Each subdirectory under `operations/` is one operations dimension, chosen on demand from a single shared pool; dimension ownership is not split by business form.

| Dimension Directory | Responsibility |
|---------------------|----------------|
| `data/` | Core metrics archived by date |
| `competitors/` | Competitive intelligence archived by target |
| `content-planning/` | Topic pool plus scheduling |
| `positioning/` | Goals, audience, differentiation |
| `search-optimization/` | On-platform search optimization |
| `promotion/` | Paid placement and cross-channel traffic |
| `conversion/` | Tracking of business outcomes |
| `retrospective/` | Periodic reviews |
| `growth-experiments/` | Records of hypothesis verification |
| `product-definition/` | Positioning, pricing, delivery, entry points |
| `course-design/` | Structure, boundaries, path, promise |
| `purchase-path/` | Conversion funnel, trial, hesitation resolution |
| `learner-operations/` | Community, case studies, Q&A |
| `sales-materials/` | Selling points, evidence, scripts |
| `{business_form_specific}/` | Operating mechanisms unique to that business form |

Enablement conditions and details for each dimension are in `../methodology/business/kb-method-business-operations.md`.

Create only the dimensions you actually need; omit the rest. Dimension directories with ongoing output archive their contents under `{YYYYMMDD}/`.

### The Eight-Directory Skeleton for Website Products

Website-type products (official sites, SaaS sites, product sites, content sites) do not use the dimension pool above. They use a fixed, numbered set of eight directories instead, all pre-created when the product is set up:

```text
{product_name}/
├── CLAUDE.md
├── 01-product-definition/
├── 02-payment-collection/
├── 03-search-optimization/
├── 04-content-operations/
├── 05-growth-promotion/
├── 06-operations-data/
├── 07-customer-feedback/
└── 08-asset-evidence/
```

What each directory holds, and the details, are in `../methodology/business/kb-method-business-operations.md`.

Non-website channels still select from the dimension pool; do not apply the eight-directory layout to them.

### Explicitly Prohibited First-Level Directories

| Prohibited | Reason | Correct Landing |
|------------|--------|-----------------|
| Brand root `promotion/` | Overlaps with the channel `operations/` responsibilities | Channel-specific items go to `{channel}/operations/promotion/`; cross-channel short links go to the main conversion channel's `05-growth-promotion/` |
| Brand root `infrastructure/` | Double-writes with product deployment evidence | Run summaries go in the channel or product `CLAUDE.md`; troubleshooting and evidence go in `08-asset-evidence/`; deployment code goes in the code repository |
| Brand root `assets/` | Brand visuals do not belong to the business layer | `{brand_root}{brand_name}/identity/visual/assets/` |
| Business root `synthesis-dashboard.md` | A duplicate entry point alongside the root `CLAUDE.md` | Write it into `{business_root}CLAUDE.md` |
| `planning/` under a business unit | Plans are in-flight documents | `{dashboard_root}research/{YYYYMM}/` |

## Organizational Modes Used

| Layer | Mode | Description |
|-------|------|-------------|
| Root → Brand → Unit | **E1 Brand × Dimension** | Bucket by brand first, then expand by channel or product |
| Unit → Three subdirectories | Fixed vocabulary | `content/` `operations/` `schedule/`. Exception: X and GitHub units skip `content/` and expand type directories directly (X: `tweets/` `threads/` `replies/` `articles/` `engagement/`; GitHub: `repos/`), equivalent to their content layer |
| `operations/` → Dimension | **E3 Functional Responsibility** | Select from the dimension pool as needed |
| Website product → Eight directories | Fixed numbering | All pre-created when the product is set up |
| Dimension → Date archive | **T2 Variant** | `{YYYYMMDD}/` or `{YYYYMMDD}-{description}/` |
| Content unit | Domain deep path | `{channel}/content/{category}/{YYYYMMDD}-{short_name}/` |

Mode definitions are in `kb-directory-pattern-registry.md`. Content-unit paths in the business area run deeper than the four-layer limit; follow this skeleton and do not mechanically apply the depth cap.

## Customization Interface

| Parameter | Description | Default |
|-----------|-------------|---------|
| `{business_root}` | Root path of this area | `business/` (see `layout.yaml`) |
| Brand list | Which brand directories exist under the root | Keep consistent with the brand directory names under `{brand_root}` |
| Channel list | Which channels exist under each brand | Created by the user according to the platforms actually used for publishing |
| `content-registry/` enabled | Create it when the same content appears on two or more channels | Off |
| `schedule/` enabled | Create it when there is a continuous production need | Off |
| Operations dimension selection | Which dimensions to create under `operations/` | `data/` and `competitors/` are required; the rest follow the enablement conditions in `../methodology/business/kb-method-business-operations.md` |
| Website product skeleton | Whether website-type products use the eight-directory layout | Enabled |
| Product promotion threshold | Condition for promoting a product from `products/` to the brand root | More than twenty files and an independent operating rhythm; keep a one-line pointer in `products/` |
| Business-form vocabulary | Classification words for content units | Defined by the user according to the business context |

## ⑦ Build Procedure

The business area is the personal slot of the framework — its contents differ for every owner. An agent interviews the owner to discover their arenas and builds a directory per arena.

### Interview Questions (ask one at a time)

| # | Ask | Maps to |
|---|-----|---------|
| 1 | Where does your work actually end up — platforms, clients, classes, products? (list every arena) | One `{channel_name}/` per arena |
| 2 | What do you deliver in each arena? | Each arena's `CLAUDE.md` description |
| 3 | Which arena matters most right now? | Priority note in root `CLAUDE.md` |
| 4 | Do you sell a product or service? If yes: what, at what price? (skip if not yet) | `products/` directory |

### Agent Rules

- Create only the arenas the owner names. Never create aspirational arenas — "I might start a podcast" does not become a directory.
- Different owners get completely different contents: a creator gets `youtube/` and `x/`; a consultant gets `clients/`; a teacher gets `courses/`. This is the whole point of the slot.
- Each arena gets a `CLAUDE.md` that says what gets delivered there, in what form, how often.
- Update the root `CLAUDE.md` into an arena index: one line per arena so the agent can route future output by reading it.
- Print the file tree and stop.

### Build Verification

- Print the full file tree of `{business_root}`
- Confirm every arena directory has a `CLAUDE.md` that states what gets delivered there
- Check against § Checklist item by item

## Related Methodologies

- `../methodology/business/` — Skeletons for the seven main categories, values of the seven retrieval facets, content-unit directory structure, content numbering rules, operations-dimension details, project planning and project archives, customer relations, strategic decisions, operating data, and event archives.

## Checklist

- [ ] The brand root has only three kinds of directories: channels, products, and content registry
- [ ] The brand root has no loose files besides `CLAUDE.md`
- [ ] No brand-root `promotion/`, `infrastructure/`, or `assets/`
- [ ] Every business unit has `content/` and `operations/`
- [ ] `operations/` contains only the dimensions actually needed; `data/` and `competitors/` exist
- [ ] All eight directories for website products are pre-created
- [ ] Research reports and plan designs are not in business directories
- [ ] Content-unit originals are in `content/`; topics and scheduling are in `schedule/`; the two never mix
- [ ] Cross-brand summaries appear only in `{business_root}CLAUDE.md`
- [ ] The content root contains no machine-generated lists or export files

## Change Log

> Rolling window; keep the last 3 entries, each ≤20 characters.

| Date | Change |
|------|--------|
| 2026-08-14 | X/GitHub type-directory exception declared |
| 2026-08-08 | Dimension enablement conditions now point to the methodology |
| 2026-08-07 | Extracted the skeleton from the business specification |
