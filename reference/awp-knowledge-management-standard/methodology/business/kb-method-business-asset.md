---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-asset
language: en
publication: public
title: "Business Methodology  -  Operating Assets"
---

# Business Methodology  -  Operating Assets

> Manage continuously-maintained resources with no fixed endpoint: state, maintenance frequency, zombie detection.
> Inherits all constraints from `kb-method-business-general.md`, this file adds only what applies to operating assets specifically.

## I. What We Manage

Live resources under active operation and sale: product catalogs, website sections, retail locations, equipment, feature directories for online services, content series, long-term contracts. These are not "complete and done" projects, but ongoing resources that require continuous maintenance and monitoring.

## II. Four Core Principles

- **No endpoint but has state**: Operating assets have no completion date, but must declare current state (active / suspended / retired / iterating).
- **Maintenance frequency documented**: Each asset must declare maintenance frequency, otherwise it becomes a zombie.
- **Data freshness required**: Operations data older than 30 days warrants a warning; older than 90 days warrants re-evaluation.
- **Handoff with project records**: What a project produces becomes an operating asset.

## III. File Format: Single File Default

Default to a single file—the required sections and index content of an operating asset go into the directory's `CLAUDE.md`, not a separate `asset.md`.

Only split into `CLAUDE.md` (index only) + `asset.md` (detailed record) when any of these apply:

- Subdirectories exceed 10, and the index itself exceeds 100 lines.
- Maintenance logs or change records are high-frequency updates that would bloat `CLAUDE.md`.
- This asset and other operating assets share one parent `CLAUDE.md`—each asset gets its own `{asset_name}.md`.

Prohibit splitting into two files just to "look more structured." Small and medium assets stay clearer in one file.

### Merge Example

```markdown
# {Asset Name}

> Operating asset  -  {one-line positioning}

## Metadata

| Field | Value |

## Cross-Reference

| Internal View (This Directory) | Work Area Content |
| Product or Channel View | → Product Catalog or Channel Operations Directory |

## Subdirectories and Sub-Asset Index

## Maintenance Log

| Date | Event |

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.
```

## IV. Required Sections

Whether merged into `CLAUDE.md` or in a standalone `asset.md`, these sections must be present:

| Section | Content |
|---------|---------|
| Metadata | Nine fields plus asset number (if any) |
| Positioning | One-line purpose of this asset |
| Current State | Active / Suspended / Retired / Iterating |
| Key Attributes | Core fields for this asset type, defined by industry |
| Maintenance Log | Rolling record of updates, changes, events |
| Next Review Date | Calculated from maintenance frequency |

## V. State Value Set

| Value | Meaning |
|-------|---------|
| Active | Operating normally |
| Suspended | Temporarily paused |
| Retired | Permanently retired |
| Iterating | Major overhaul, paused for external audiences |

## VI. Maintenance Frequency

Each operating asset must declare maintenance frequency:

| Frequency | When Used |
|-----------|-----------|
| Daily | High-volume transactions, livestreams, customer service |
| Weekly | Active products, active sections |
| Monthly | Stable products, stable sections |
| Quarterly | Long-term contracts, tail assets |
| As-needed | Event-triggered |

Judgment rule: If an asset's update date is more than "maintenance frequency × 2" days old, treat it as a zombie asset requiring re-evaluation or retirement.

## VII. Recommended Sections

| Section | Explanation |
|---------|-------------|
| Related Projects | Point to the project record that created this asset |
| Related Customers | Point to customer relationships this asset serves |
| Related Data | Point to metrics for this asset in operations data |
| Historical Versions | Important iteration milestones for the asset |

## VIII. Industry-Specific Optional Fields

| Business Type | Recommended Additional Fields |
|---------------|-------------------------------|
| Physical Products for Sale | SKU, specifications, supply chain, inventory, ratings |
| Online Service Features | Version, interface, dependencies, user count, failure history |
| Website Sections and Content Series | Section positioning, publication cadence, SEO keywords |
| Retail Locations | Address, area, staff, hours of operation, equipment |
| Equipment | Model, purchase date, maintenance, depreciation |
| Service Plans | Content, pricing, coverage scope |
| Contracts and Subscriptions | Counterparty, term, amount, renewal |

Prohibit storing production workflow files in operating assets—those belong in project records.

## IX. Naming

| Form | Naming |
|------|--------|
| Single Asset File | `{asset_name}.md` |
| Asset Directory | `{asset_name}/` |
| Asset Collection Index | `{type}/CLAUDE.md` |

## X. Deduplication Boundaries

| Content | Goes To | Does Not Go To |
|---------|---------|----------------|
| Asset production process | Project Record | Operating Asset |
| Asset monthly/quarterly data | Operations Data | Operating Asset (keep latest snapshot only) |
| Customer for this asset | Customer Relationship | Operating Asset |
| Credentials used by asset | Credential Library | Operating Asset |
| Asset's product definition after launch | Product Definition in Product Catalog | Operating Asset (cross-reference) |

## XI. Checklist

- [ ] Metadata contains nine fields
- [ ] State field explicit (active / suspended / retired / iterating)
- [ ] Maintenance frequency documented
- [ ] Last update not older than "maintenance frequency × 2"
- [ ] Key attributes filled per industry
- [ ] Related projects, customers, data cross-referenced
- [ ] No spillover into project records or operations data

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Migrated from operating asset spec and generalized |
