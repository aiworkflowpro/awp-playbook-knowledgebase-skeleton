---
document_id: awp-knowledge-management-standard/methodology/brand/kb-method-brand-businessmodel
language: en
publication: public
title: "Business Model Methodology"
---

# Business Model Methodology

> Managing how to write brand business model files: revenue paths, income sources, customer acquisition channels, and core principles.
> Applicable to any industry and any brand.

---

## Positioning

Business models are placed in the operational domain at `{brand_root}/{brand}/operations/business-model/`, with a low loading frequency, answering "how to monetize and what price tier to sell at."

Two boundaries:

- The strategic domain only keeps positioning and boundaries, **does not accumulate product lists**; narrative paths go in this directory.
- Audiences and competitors are in two other directories in the same domain, see `kb-method-brand-audience.md` and `kb-method-brand-competitor.md`.

---

## Design Philosophy

- **Clear pathways**: From customer acquisition to monetization at a glance.
- **Strategies are executable**: Each step is concrete enough to take action.
- **No duplication across boundaries**: The definitive version of behavior red lines is in the strategic domain's boundary file; this file only references them.

---

## Organizational Framework

### Required Sections

| # | Section | Content |
|---|---------|---------|
| 1 | Business Model Overview | Core pathway diagram from acquisition to monetization |
| 2 | Revenue Sources | Product or service + pricing + target customer segment, in table format |
| 3 | Customer Acquisition Channels | Positioning and strategy for each channel |
| 4 | Core Principles | Business operation principles, as numbered list |
| 5 | Change Log | Date and change description, no version numbers |

### Optional Sections

| Section | When to Use |
|---------|------------|
| Channel Matrix | Multi-channel brands, separating free and paid tiers |
| Customer Acquisition Conversion Path | Businesses with clear conversion steps, describing each channel's lead generation action |
| Content and Touchpoint Strategy | Operational details for each channel's touchpoints, such as comments, communities, customer service |
| Content Reuse Chain | Brands distributing one piece of content across multiple channels |
| Partnership Model | Brands with partner channels or distribution |
| Cost Structure | Brands where Agents need to demonstrate cost awareness |
| Competitive Strategy | Brands where Agents need to understand the competitive landscape |

---

## Section-by-Section Details

### Business Model Overview

✅ Use arrow diagrams or flowcharts to show the core pathway from acquisition to monetization.
✅ Label key actions at each step.

Industry examples:

Content creators:

```
Free content (build trust) → Audience retention → Paid products (monetize)
```

Software services:

```
Content marketing and search → Free trial → Paid conversion → Renewal and upselling
```

Consulting services:

```
Public data (build expertise) → Public courses → Diagnostic services → Long-term advisory
```

### Revenue Sources

✅ Use a table with at least: product or service name / pricing model / target customer segment.
⚪ May add columns: launch date, scale, channel.

❌ Do not expose inappropriate pricing details in external content. If needed to restrict, mark as "internal only."

### Customer Acquisition Channels

✅ List all customer acquisition channels and their positioning.
✅ Describe three things for each channel: channel name / content format / core purpose.

⚪ Multi-channel brands can use a table:

```markdown
| Tier | Channel | Content Format | Core Purpose |
|------|---------|-----------------|------------|
| Free | {Channel A} | {Format} | {Purpose} |
| Paid | {Channel B} | {Format} | {Purpose} |
```

### Customer Acquisition Conversion Path (Optional)

⚪ Each major channel gets its own subsection.
✅ List conversion steps for each channel as 3–5 numbered points.
✅ Steps must be concrete enough to execute.

| Good | Bad | Why |
|------|-----|-----|
| "Add product link in video description" | "Promote product in video" | Former is actionable |
| "Add trial entry at end of article" | "Guide users to try" | Former specifies location |

### Core Principles

✅ Numbered list of 3–8 principles.
✅ One sentence per principle, ⚪ may add brief explanation.

---

## Deduplication Boundaries

| Content | Include in This File | Keep Elsewhere |
|---------|---------------------|-----------------|
| Monetization paths, channel strategies | ✅ | — |
| Behavior red lines (absolute no-nos) | ❌ | Goes to strategic domain's boundary file; this file only references |
| Industry-specific boundaries (e.g., paid vs. free content division) | ❌ | Goes to strategic domain's boundary file; this file only references |
| Contact info, platform account links | ❌ | Goes to brand introduction file |
| Business evolution history | ❌ | Goes to owner layer's experience directory |

Reference format:

```markdown
> Red lines and behavior boundaries are detailed in `{strategic_domain_boundary_file}` § Absolute Do-Nots
```

---

## Checklist

- [ ] Original is in `{brand_root}/{brand}/operations/business-model/`
- [ ] Business model overview diagram is complete
- [ ] Revenue sources table has at least product, pricing, and customer segment columns
- [ ] Customer acquisition channels cover all active channels
- [ ] Core principles: 3–8 items
- [ ] Red lines are references to strategic domain's boundary file, not duplicated
- [ ] Does not include contact information (belongs in brand introduction)
- [ ] Does not include business history timeline (belongs in owner layer's experience directory)

---

## Related Methodologies

| Topic | File |
|-------|------|
| Identity layering and loading priority | `kb-method-brand-identity.md` |
| Audience persona | `kb-method-brand-audience.md` |
| Competitor analysis | `kb-method-brand-competitor.md` |

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|--------|
| 2026-08-07 | Extracted from brand standards into reusable methodology |
