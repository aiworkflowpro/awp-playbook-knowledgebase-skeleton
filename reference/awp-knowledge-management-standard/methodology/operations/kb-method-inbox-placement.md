---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-inbox-placement
language: en
publication: public
title: "Placement Analysis Methodology"
---

# Placement Analysis Methodology

> Manage one thing: when receiving content, how to judge where it belongs in the knowledge base.
> This methodology does not hard-code routing — Agent uses four-dimensional analysis plus target directory `CLAUDE.md` for on-site judgment.

## Four-Dimensional Analysis

Receiving content for placement, answer four questions in sequence.

### Dimension One: What Type of Content

| Type | Signal |
|------|---------|
| Creative reference | Others' articles, videos, posts. Has view count, likes. Has platform and author info. |
| Data report | Institution source. Contains statistics, charts, percentages. Has methodology statement. |
| Thinking framework | Methodology, model, or principle. Reusable analysis tool. |
| Real case | Specific person or company solved what problem with what tool. |
| Tool documentation | Command-line, API, config description, operation tutorial. |
| Workflow | Complete path from A to B. |
| Industry knowledge | Terminology definition, concept explanation, technical principle. |
| Personal life | Non-work content: health, finance, relationships, leisure, home, growth. |

### Dimension Two: Who Consumes This

| Consumer | Definition | Corresponds to Top Area |
|--------|------|-------------|
| Agent during writing | Reference for article or script | Reference material zone, or corresponding creation workflow |
| Agent during execution | Needs to know how to operate | `{workflows_root}` or `{tools_root}` |
| Agent during decision | Needs rules, standards, guardrails | `{specs_root}` or target directory `CLAUDE.md` |
| User query time | Check business data or progress | `{business_root}` |
| User personal | Life management | `{personal_root}` |

### Dimension Three: Which Sub-domain

After determining top-level zone, **read that directory's `CLAUDE.md`** to find subdirectory. Cannot skip this step — top level only classifies broadly. Subdirectory boundaries live in each directory's entry file. This methodology does not duplicate them.

| Top Area | Subdirectory Judgment Basis |
|---------|--------------|
| Reference material zone | Target directory `CLAUDE.md` + reference methodology. Each reference type has clear boundary. |
| Creation workflow materials and examples | Material directory inside workflow or example index. Pacing touch samples follow workflow maintenance. |
| `{research_root}` | By topic and type |
| `{workflows_root}` | By process type |
| `{tools_root}` | By tool type |
| `{business_root}` | Judge brand or product line first, then specific unit. Cross-brand index in business root entry. |
| `{specs_root}` | By spec type |
| `{personal_root}` | By life domain |

### Dimension Four: New Directory or Append

| Scenario | Method | Action |
|------|---------|------|
| Target directory already has same-topic file | Read target `CLAUDE.md` + list directory | Append to existing |
| Target directory lacks same-topic content | Same | New subdirectory plus file |
| Target directory has same account or same source | Check existing account subdirectory | Join existing subdirectory |

## Judgment Logic

1. **What question does this answer?** → Match top area positioning
2. **What is this content used for?** → Match subdirectory function
3. **Which spec governs this type?** → Extract by spec skeleton
4. **New or append?** → Read target `CLAUDE.md` compare

**Never "unsure where it goes, leave in inbox"** — inbox is processing pipeline, not storage. When judgment unclear, either gather more info then judge again, or confirm it has no retention value and clean it. Do not stall long-term in inbox.

## Key Boundaries

These pairs confuse most. Each has clear criterion:

| Easy to Mix | Distinction |
|---------|---------|
| Hit vs. case | Hit is writing style reference (how written). Case is tool application reference (how done). |
| Data vs. case | Data is macro statistics report. Case is micro individual story. |
| Framework vs. spec | Framework is optional thinking tool. Spec is mandatory standard. |
| Tool vs. workflow | Tool is single capability (how call). Workflow is multi-step sequence (how complete task). |
| Project archive vs. operating asset | Project has start and end, single delivery. Asset is continuous resource in use. |
| External industry data vs. own business data | Former is external report. Latter is own business table. |

## Code Does Not Enter Knowledge Base

When script, command-line tool, or service code arrives, it goes to code repo, not knowledge base. Only two stay in knowledge base: usage documentation (best practices) and credentials it needs.

## Checklist

Before placement:

- [ ] Four-dimensional analysis all four questions have answers (type / consumer / subdomain / new or append). Recorded in proposal table.
- [ ] Read target directory `CLAUDE.md`
- [ ] Read spec for target file's domain
- [ ] Confirm subdirectory exists (avoid duplicate)
- [ ] When creating subdirectory, synced parent `CLAUDE.md` index
- [ ] Proposal table complete (action / target file / source file)

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from placement analysis spec |
