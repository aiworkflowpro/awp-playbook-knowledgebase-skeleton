---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-decision
language: en
publication: public
title: "Business Methodology  -  Strategic Decisions"
---

# Business Methodology  -  Strategic Decisions

> Manage single major decisions and long-term retrospectives: context, options, rationale, assumptions, retrospective.
> Inherits all constraints from `kb-method-business-general.md`, this file adds only what applies to strategic decisions specifically.

## I. What We Manage

Decisions with major long-term business impact: pricing strategy, category pivot, platform choice, technology selection, expansion or contraction, personnel change, acquisition or partnership.

Purpose: let your future self or team know two things—why this choice was made, and whether it still holds.

## II. Four Core Principles

- **Record decisions, not execution**: This section records "why choose this," not "how execute it." The latter goes to project records or workflows.
- **Rationale matters more than conclusion**: Knowing "what decision" has short-term value; knowing "why" has long-term value.
- **Must retrospect**: Every decision needs a retrospective date, to verify assumptions.
- **Compare assumptions to reality, not right vs. wrong**: In retrospective, lay actual outcome against decision-time assumptions; do not simplify to "right or wrong."

## III. Required Sections

| Section | Content |
|---------|---------|
| Metadata | Nine fields plus decision tier |
| Context | Why this decision was needed; one paragraph |
| Decision-Time Reality | Key facts, data, constraints; can cite sources |
| Options Compared | Considered options and tradeoffs each |
| Final Decision | Which chosen; one-sentence explanation |
| Key Rationale | 3–5 decision grounds |
| Assumptions | Key assumptions this decision rests on, to verify in retrospective |
| Next Retrospective Date | Mandatory |
| Retrospective Records | Rolling append; never modify history |

## IV. Decision Tier Value Set

| Tier | Meaning | Retrospective Frequency |
|------|---------|------------------------|
| Strategic | Affects business direction, business model, long-term positioning | Every half year |
| Tactical | Affects specific product line, channel, annual plan | Every quarter |
| Operational | Affects specific process, tool, single execution | Monthly or as-needed |

## V. Retrospective Record Format

Each retrospective appends one entry; never modify history:

```markdown
## Retrospective Records

### YYYYMMDD (Retrospective #N)

| Item | Content |
|-----|---------|
| This retrospective answers | {question} |
| Assumption verification | Original assumption A: {confirmed / invalidated / partially confirmed} |
| Reality gap | {What actually happened, beyond expectation} |
| Adjust decision or not | Yes / No, with rationale |
| Next retrospective | YYYYMMDD |
```

Prohibit deleting or modifying historical retrospective records; only append.

## VI. Recommended Sections

| Section | Explanation |
|---------|-------------|
| Risk Inventory | Main risks identified during decision, response |
| Stakeholders | People and relationships affected |
| Quantified Evidence | Data and calculation supporting decision; use range |
| References | Research sources, benchmarks |

## VII. Industry-Specific Optional Sections

| Decision Type | Add Recommended |
|---------------|-----------------|
| Finance and Investment | Financial model, payback period, ROI |
| Technology Selection | Architecture Decision Record (ADR) format |
| Strategic Pivot | SWOT analysis + opportunity cost analysis |
| Personnel | Role definition + performance metric design |
| Pricing | Pricing model, competitor comparison, gross margin estimate |
| Compliance | Regulatory basis + compliance risk |

Industry-optional sections add to required sections; do not replace required sections.

## VIII. Naming

`decision-{topic_summary}.md`

- No date prefix; decision date in metadata.
- Optional tier prefix: `decision-{tier}-{topic}.md`.

## IX. Deduplication Boundaries

| Content | Goes To | Does Not Go To |
|---------|---------|----------------|
| Decision execution details | Project Records | Strategic Decision |
| Decision-referenced report data | Operations Data | Decision (embed large data) |
| Private finance decision | Personal Area Finance | Business Strategy Decision |
| Brand business model long-term summary | Brand Operations Sector | Cross-reference relation |
| Technology stack long-term selection | Experience Library + cross-reference here | Cross-reference both directions |

## X. Checklist

- [ ] Metadata contains nine fields plus decision tier
- [ ] Context, reality, options, decision, rationale, assumptions six sections complete
- [ ] Next retrospective date set
- [ ] Existing retrospective records never modified, append only
- [ ] Decision rationale verifiable, not "gut feel" or "sense"
- [ ] Specific amounts use range or percentage, not absolute
- [ ] No project execution detail

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Migrated from strategic decision spec and generalized |
