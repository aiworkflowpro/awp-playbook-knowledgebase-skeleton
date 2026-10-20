---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-customer
language: en
publication: public
title: "Business Methodology  -  Customer Relationships"
---

# Business Methodology  -  Customer Relationships

> Manage external stakeholder records: relationship type, activity level, contact history, privacy boundaries.
> Inherits all constraints from `kb-method-business-general.md`, this file adds only what applies to customer relationships specifically.

## I. What We Manage

All external stakeholders: customers, students, subscribers, suppliers, partners, channel partners, resellers. Answer three questions—who influences business, how much influence, what contact history.

## II. Four Core Principles

- **Record relationships, not directories**: This section records relationship state and interaction history, not complete contact info.
- **Privacy first**: Information about others is inherently sensitive; default to restricted access level.
- **Separate from audience persona**: Business customers are **concrete individuals**; brand audience is **abstract persona**; connect via association field, do not merge.
- **Relationships cool down**: Periodically verify the relationship is still active.

## III. Required Sections

| Section | Content |
|---------|---------|
| Metadata | Nine fields plus relationship type |
| Basic Info | Name, relationship start date, current activity level |
| Contact History | Rolling record of important interactions (date + event + result) |
| Value and Contribution | Value of relationship to business; summarize not absolute figures |
| Next Follow-up Date | Calculated from activity level |

## IV. Relationship Type Value Set

| Type | Meaning |
|------|---------|
| Customer | Pays for product or service |
| Student | Education-specific subtype |
| Subscriber | Free subscriber or follower |
| Supplier | Provides materials, services, collaboration resource |
| Channel Partner | Distributes or resells |
| Partner | Co-produce, cross-promote, joint venture |
| Investor | Financial relationship |
| Other | Above not applicable |

## V. Activity Level Value Set

| Value | Judgment | Follow-up Suggestion |
|-------|----------|----------------------|
| Active | Interaction within last 30 days | Maintain |
| Warm | No interaction 30–90 days | Initiate contact |
| Cold | No interaction 90–180 days | Targeted activation |
| Dormant | Over 180 days | Evaluate to abandon |
| Terminated | Explicitly ended | Move to archive |

## VI. Privacy Defaults

This section stricter than others. "Not in database" below means not stored anywhere in knowledge base; use encrypted password manager or notes app.

| Content | Default Level | Explanation |
|---------|---------------|------------|
| Relationship type + activity level | Internal only | Internal use |
| Contact history summary | Restricted | Involves others' interactions |
| Value and contribution (summary) | Restricted | Avoid absolute figures |
| Complete contact info (phone, address) | Not in database | Mandatory |
| ID number and ID document image | Not in database | Mandatory |
| Specific contract amount | Restricted or not in database | Use range instead |

Prohibit writing negative appraisals of others, rumors, or unexposed privacy details in this section.

## VII. Recommended Sections

| Section | Explanation |
|---------|------------|
| Related Audience Persona | Point to brand operations audience persona |
| Related Projects | Point to project records for this counterparty |
| Related Contracts | Key points of current agreement; do not store full contract |
| Notes | Preferences, taboos, attention items |

## VIII. Industry-Specific Optional Sections

| Counterparty Type | Add Recommended |
|-----------------|-----------------|
| Enterprise Customer | Decision chain, procurement cycle, budget |
| Individual Customer | Long-term value estimate (range), repeat purchase, referral |
| Student | Enrolled course, progress, Q&A record |
| Supplier | Capacity, quality, lead time, backup tier |
| Partner | Collaboration type, revenue split, term |
| Investor | Stage, share (range), post-investment role |

## IX. Naming

| Form | Naming |
|------|--------|
| Single Individual | `{individual_name}.md` |
| Classification Directory | `{relationship_type}/{individual_name}.md` |
| Index | `{relationship_type}/CLAUDE.md` |

## X. Deduplication Boundaries

| Content | Goes To | Does Not Go To |
|---------|---------|----------------|
| Abstract target demographic | Brand operations audience persona | Customer Relationship |
| Private personal relationship | Personal Area | Customer Relationship |
| Specific project for this customer | Project Record (cross-reference) | Customer Relationship |
| Complete contact info, ID documents | Encrypted notes or password manager | Knowledge Base |
| This customer's operations data summary | Operations Data | Customer Relationship |

## XI. Checklist

- [ ] Metadata contains nine fields plus relationship type
- [ ] Activity level set
- [ ] Contact history rolling
- [ ] Sensitive info per default privacy level
- [ ] Complete contact info and ID not in knowledge base
- [ ] Next follow-up date set
- [ ] No negative appraisals of others

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Migrated from customer relationship spec and generalized |
