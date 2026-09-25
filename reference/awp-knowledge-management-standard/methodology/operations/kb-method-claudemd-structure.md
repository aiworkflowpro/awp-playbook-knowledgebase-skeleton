---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-claudemd-structure
language: en
publication: public
title: "Role CLAUDE.md Unified Structure"
---

# Role CLAUDE.md Unified Structure

> A role's `CLAUDE.md` is **a map, not a manual**. Operational details, parameter tables, command references, and troubleshooting records all live in the operations handbook; the CLAUDE.md holds only pointers.
> Parent: `../../directory/kb-area-dashboard-skeleton.md` (dashboard directory skeleton)

## 1. Design Principles

1. **Map principle**: the CLAUDE.md tells the role "who you are, what you manage, and where to find the operations handbook" — it does not teach the role how to operate.
2. **Single source of truth**: every piece of information is written in exactly one place. If content in the CLAUDE.md already exists in the operations handbook or a spec, keep only a pointer.
3. **Unified structure**: the `##`-level section names and order are the same across all roles, making cross-role reviews and maintenance straightforward.
4. **Required + optional**: some sections exist for every role; others appear only when needed. When an optional section is absent, leave no empty placeholder.

## 2. Section Roster and Order

| # | Section name (`##`-level) | Required | What goes in | What stays out |
|---|---------------------------|----------|-------------|----------------|
| 1 | **Role card** | Required | Identity, mission, does / doesn't do, boundary, escalation path | No operational details |
| 2 | **Decision framework** | Required | Judgment rules unique to this role (3–5 items) | No general rules (those live in the shared rules) |
| 3 | **Trigger words** | Required | Keywords that activate this role | — |
| 4 | **What to do on load** | Required | Files to read in order (required + on-demand); confirmation action after loading | No file contents — only paths |
| 5 | **Execution rules** | Required | Core behavior rules unique to this role (5–8 items) | Parameters, commands, detailed procedures → point to the operations handbook |
| 6 | **Evaluation criteria** | Required | Pass / outstanding / fail criteria (1–2 sentences each) | — |
| 7 | **Tool quick reference** | Optional | The 3–5 most-used commands or tools for this role | Full command table → operations handbook |
| 8 | **Collaboration map** | Optional | Who exchanges what (table) | No repeating the role card's boundary |
| 9 | **Dispatch and windows** | Required | Task-card template for delegation + workflow entry points | — |
| 10 | **Shared rules** | Required | Pointers to the spec and the shared directory — no restating | — |
| 11 | **Task management** | Required | Pointer to canonical source | — |
| 12 | **Change log** | Required | Latest 3 entries, each ≤ 20 characters | — |

### Role-specific sections

Some roles have domain-specific blocks (operations officer's "scheduled roster", chairman's "delegation selector", video producer's "jurisdiction boundary", etc.). These blocks:

- Go **after evaluation criteria and before dispatch and windows** (between items 6 and 9)
- Use `##`-level headings
- No more than 3 — anything beyond moves to the operations handbook

### Governance-layer variations

The chairman, CEO, and inspector have different end-of-task notification flows than the execution layer; each writes those in their own CLAUDE.md. This is the only exception the spec allows; record the details in whichever collaboration spec your knowledge base uses.

## 3. Line Count Targets

| Type | Target lines | Notes |
|------|-------------|-------|
| Lean roles (aide, narrative, etc.) | 80–120 | No domain-specific sections |
| Standard roles (content, brand, dev, etc.) | 120–180 | 1–2 domain-specific sections |
| Heavyweight roles (video producer, ops officer, chairman) | 150–220 | 2–3 domain-specific sections |

Anything over 220 lines triggers a review: are operational details still sitting in the CLAUDE.md instead of the handbook?

## 4. Operations Handbook Standard Files

Every role's `operations-handbook/` directory must include at least:

| File | Required | Content |
|------|----------|---------|
| `CLAUDE.md` | Required | Handbook index (file list + when to load) |
| `items-daily-work-general.md` | Required | What this role normally does |

Other files follow four-segment naming `{type}-{domain}-{topic}-{scope}.md`; type prefixes:

| Type prefix | Content |
|------------|---------|
| `items-` | Daily work, schedules |
| `process-` | Standard operating procedures (SOPs) |
| `method-` | How to do something (methodology) |
| `guide-` | Quick-reference tables, tool environments |
| `data-` | Production archives, progress tracking, environment config |
| `plan-` | Planning, selection proposals |
| `experience-` | Troubleshooting records |

## 5. Standard Content Patterns for Each Section

### Role card

```markdown
## Role card

- **Identity**: {one-line positioning}, trust level {L1/L2}. Reports to {who}.
- **Mission**: {one-line mission}.
- **Does**: {3–5 items, grouped by stage or dimension}
- **Doesn't do**: {2–3 items, drawing clear lines with easily confused roles}
- **Escalation path**: {2–3 items, what situation goes to whom}
```

### What to do on load

```markdown
## What to do on load

Required reading (in order):
1. This file
2. {path} ({one-line description})
3. ...

On-demand (read when the task involves it):
- {path} ({when to read it})
- ...

Load confirmation: {one-line confirmation action}
```

### Execution rules

```markdown
## Execution rules

1. **{Rule name}**: {one-line description}. See `operations-handbook/{filename}`.
2. ...
```

5–8 rules. One sentence each. Parameters and commands do not go here — write "See `operations-handbook/xxx`".

### Shared rules

```markdown
## Shared rules

> **Rules** (survive a fleet swap) → `specs/{your-collaboration-spec}/collaboration.md`
> **Live state** (changes with company state) → `dashboard/roles/shared/CLAUDE.md`
>
> Both are canonical sources. Read as needed; do not copy into this file.
```

## 6. Checklist

- [ ] `##`-level section names and order match section 2 of this spec
- [ ] Line count within the target range
- [ ] No command tables, parameter tables, or detailed procedures embedded in the CLAUDE.md (should be in the handbook)
- [ ] Shared rules section contains only pointers, no restating
- [ ] Operations handbook has at least `CLAUDE.md` and `items-daily-work-general.md`
- [ ] Change log keeps only the latest 3 entries

## Change Log

| Date | Change |
|------|--------|
| 2026-08-18 | Created: unified structure, section roster, handbook standard, checklist |
