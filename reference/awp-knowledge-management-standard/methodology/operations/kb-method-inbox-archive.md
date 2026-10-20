---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-inbox-archive
language: en
publication: public
title: "Archiving Methodology"
---

# Archiving Methodology

> Manage one thing: how the knowledge base's only soft-delete area organizes, names, and goes through lifecycle.
> Does not govern originals still in use (those belong in their true directories).

## What Archive Holds

Archive is knowledge base's **only global soft-delete zone**, holding "stopped using but cannot hard-delete" content:

- Deprecated specifications, workflows, tools (historical approaches)
- Abandoned drafts and explorations (not deployed but have retrospective value)
- Sealed source materials (legal compliance, audit trail)
- Templates replaced by new versions

It is not "things we cannot bear to delete" — if you cannot bear it, it belongs in formal directory or delete outright.
It is not "things we have not figured where to put" — if you can determine ownership, put in true directory. If no retention value, clean after confirmation.

## Organization Principles

| Rule | Definition |
|------|------|
| Each archive item gets own subdirectory | Do not scatter files. One archiving decision equals one subdirectory. |
| Subdirectory must contain `CLAUDE.md` | State what content is, why archived, how to restore |
| Sync update original location index | Mark "archived" at original and point to archive path |
| No hard delete | Archive entry is soft delete |
| No scattered files | Archive root only allows `CLAUDE.md` and monthly directories |

## Subdirectory Naming

Use month directory plus front-dated four-segment:

```text
{YYYYMM}/{YYYYMMDD}-{type}-{object}-{status}
```

| Field | Rule |
|------|------|
| `YYYYMMDD` | Archive or seal date. Timestamp is first segment. |
| `type` | Short noun, e.g., "excerpt", "research", "handoff", "tool", "source", "material" |
| `object` | short descriptive phrase, keep necessary proper names |
| `status` | "sealed", "archived", "deprecated", "replaced", "retained" |

```text
archive/
├── CLAUDE.md
├── 202603/
│   └── 20260329-plan-longform-multi-agent-parallel-sealed/
└── 202604/
    ├── 20260430-material-industry-package-replaced/
    └── 20260430-export-whiteboard-workspace-retained/
```

Multiple archives same day for same object: add stable short word to object segment (e.g., "batch2"), not fifth segment after status.

## Subdirectory Entry File Required Skeleton

```markdown
# {Archive Item Name}

> One sentence: what is this.

## Metadata

| Field | Value |
|------|-----|
| Seal date | YYYYMMDD |
| Original location | {Knowledge base relative path, or "external source"} |
| Archive reason | Deprecated / abandoned / replaced / compliance retention |
| Replacement plan | {New plan path, if any} |
| Restore method | {How to restore from archive to use, or "no restore"} |
| Cleanup planned | {Date or "long-term retention"} |

## Content List

{List key files or subdirectories in this archive item and their purpose}

## Background

{Why archived, context and decision basis}
```

## Four Archiving Scenarios

| Scenario | When | Restore Likelihood |
|------|--------|-----------|
| **Deprecated** | Feature removed but code or docs have history value | Low |
| **Abandoned** | Exploratory plan not deployed, keep retrospective value | Very low |
| **Replaced** | New version takes over, old version archived | Medium (for rollback) |
| **Compliance retention** | Legal or audit requires no deletion | No restore, destroy at expiry |

## Archiving Process

```text
Identify content to archive
  ↓
Judge matches one of four scenarios
  ↓ Yes
Create own subdirectory under archive/{YYYYMM}/
  ↓
Move content into subdirectory
  ↓
Write CLAUDE.md (complete metadata + background)
  ↓
Update original location index (mark archived + point to path)
  ↓
Update archive root CLAUDE.md archive table
```

Do not skip any step — especially original location index update. Skipping leaves broken reference in formal directory.

## Archive Root Entry File

Archive root `CLAUDE.md` must maintain three things:

1. **Positioning note**: One sentence explaining archive use
2. **Rules summary**: 3-5 core rules
3. **Archive item table**: All subdirectories by date, source, reason

Archive item table fields:

| Directory | Content | Seal Date | Original Location | Reason |

## Lifecycle

| Phase | Action | Trigger |
|------|------|---------|
| Inbound | Create subdirectory + `CLAUDE.md` | Archive decision |
| Dormant | Long-term retention | Default state |
| Review | Inspect once | Once per year |
| Archive compress | Package | Over 3 years no access |
| Destroy | Hard delete | Compliance retention expires only, user confirms |

**Agent must not autonomously destroy any archive item** — destroy decision must be user-initiated.

## Boundary with Adjacent Areas

| Confusion | Distinction |
|--------|------|
| Archive vs. run data | Run data is troubleshoot, collect, interim state. Archive is retained seal. |
| Archive vs. draft | Draft may continue editing. Archive is dead historical material. |
| Archive vs. spec entry | Spec entry is live rules and routing. Archive is dead historical plan. |
| Archive vs. business event archive | Business event archive is completed but queryable business activity. Archive is cross-domain soft delete. |

## Checklist

**Before archiving**

- [ ] Matches one of four scenarios
- [ ] Confirmed has real retention value, not just reluctance to delete
- [ ] User confirmed (if no explicit permission)

**Archive execution**

- [ ] Own subdirectory created under monthly directory
- [ ] Content moved in
- [ ] Subdirectory `CLAUDE.md` metadata complete
- [ ] Original location index updated (mark archived + point to path)
- [ ] Archive root `CLAUDE.md` table appended

**Annual review**

- [ ] Each archive item "planned cleanup" field still valid
- [ ] No broken references (original location link still points to archive path)
- [ ] Items over 3 years no access proposed for compression

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from archive area spec |
