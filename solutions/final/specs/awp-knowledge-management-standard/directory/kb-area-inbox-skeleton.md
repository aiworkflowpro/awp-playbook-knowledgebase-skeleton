---
document_id: awp-knowledge-management-standard/directory/kb-area-inbox-skeleton
language: en
publication: public
title: "Knowledge Base Inbox/ Directory Skeleton"
---

# Inbox/ Directory Skeleton

> Defines the subdirectory structure, organization patterns used, and customization interfaces of the `{inbox_root}` root directory.

## Responsibilities

The transfer zone of the knowledge base, handling four things only: concurrent scheduling across multiple Agents, archiving, screenshot transit, and cross-machine file transit.

The inbox is **not a repository**. Materials whose ownership can be determined go directly to their actual locations in business, research, tools, brand, standards, and commerce areas; they don't stay here.

## Directory Structure

```text
{inbox_root}
├── CLAUDE.md              ← Fixed; entry point
├── {dispatch_hub}/        ← Optional; multi-Agent task pools, batches, outputs, run logs
├── screenshots/           ← Fixed; cross-machine screenshot transit, delete after use
├── editing-materials/     ← Optional; raw footage and draft-video transit for video editing
├── workstation-transit/   ← Optional; two-way sync between two machines
│   ├── input/{YYYYMM}/
│   └── output/{YYYYMM}/
└── archive/               ← Fixed; global soft deletion area, partitioned by month
    └── {YYYYMM}/
```

- Path variable `{inbox_root}` is declared in `{specs_root}layout.yaml`, resolved as `inbox/`.
- Root directory permits only `CLAUDE.md` and subdirectories declared above.
- Root directory prohibits: specification files, unowned Markdown, temporary notes, downloaded files, unclassified media, executable projects, scattered images.
- When root directory contains items that shouldn't be there, **determine ownership and handle within this task**. Do not defer cleanup to "next time."

### Processing Pipeline

```text
Material arrives
  ├─ Ownership can be determined    → goes directly to actual target directory, not inbox
  ├─ Batch concurrent tasks         → dispatch hub directory
  ├─ Ended, archive-only            → archive/{YYYYMM}/
  ├─ Cross-machine temp screenshot  → screenshots/ (delete after use)
  └─ Cross-machine large file       → workstation-transit/{input|output}/{YYYYMM}/
```

### Archive Naming

```text
archive/{YYYYMM}/{YYYYMMDD}-{type}-{object}-{disposition}/
```

| Field | Description | Values |
|------|------------|--------|
| Date | Archive date | Eight digits |
| Type | Archive content category | workflow / tool / brand / standard / material / source / channel / course / run-data / product / business / data / plan |
| Object | What is being archived | Self-explanatory short name |
| Disposition | Archive reason | archived / sealed / retained / deprecated / retired / replaced / backup |

### Workstation-Transit Naming

```text
workstation-transit/{input|output}/{YYYYMM}/{YYYYMMDDHHmm}-{model}-{topic}-{nature}/
  logs/ and config/ inside workstation-transit/ are runtime artifacts and exempt from batch naming.
```

| Field | Description |
|------|------------|
| Timestamp | Generation time of first file in batch, twelve digits, consistent with parent month directory |
| Model | Model or pipeline short name; product and model names retain original |
| Topic | What is being tested, short phrase, identical across series |
| Nature | Batch purpose: trial-run / benchmark / control / sample / final; omit if not applicable, making three segments |

Two hard constraints:

- `input/` and `output/` root directories contain only month directories, not loose files. Tool default drop paths must point to batch directories.
- Files in batch directory retain original generator names; do not apply four-segment naming—filename resolution and step counts are execution evidence.

When cleaning up, move entire batch directory into `archive/{YYYYMM}/{archive-item}/`, preserving original batch name within archive item, no renaming.

### Lifecycle

| Subdirectory | Policy |
|--------|--------|
| Dispatch hub | Keep batch records long-term for audit; valuable outputs migrate directly to actual business directories |
| `archive/` | Long-term retention; hard deletion requires asking first |
| `screenshots/` | Temporary, delete after use |
| `workstation-transit/` | Temporary, clean after processing; move entire batch directory |

## Organization Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → subdirectory | **E3 Functional responsibility** | Fixed structure, not time-driven growth |
| `archive/` | **T2 Month bucket with date-prefix directory** | Each archive event is independent |
| `workstation-transit/{input,output}/` | **T2 Month bucket with date-prefix directory** | One run, one batch directory |
| Within batch directory | No naming rules applied | Retain generator original names |

Pattern definitions see `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{inbox_root}` | Root path of this area | `inbox/` (see `layout.yaml`) |
| Allowed subdirectories list | Which directories can exist under root | `screenshots`  -  `archive` required; dispatch hub, workstation-transit, run-data as needed |
| Dispatch hub directory name | Name of multi-Agent dispatch workspace | Named by user per tool used |
| Archive type vocabulary | Second segment of archive directory name | See above table; can extend per business, register in root `CLAUDE.md` after extension |
| Archive disposition vocabulary | Fourth segment of archive directory name | archived / sealed / retained / deprecated / retired / replaced / backup |
| `workstation-transit/` enabled | Build only when cross-machine large file sync needed | Disabled |
| Transit nature vocabulary | Fourth segment of batch directory name | trial-run / benchmark / control / sample / final; can omit |

## ⑦ Build Procedure

Build modes: `interview` → `analysis`

The inbox is a staging area. Everything new lands here first; nothing gets organized in its old place. The agent sorts items out by the rules of the areas they belong to.

### Interview (interview)

Information to collect:

| # | Information | Required | Ask | Maps to |
|---|------------|:--------:|-----|---------|
| 1 | Location of old files | Optional | Do you have old files to bring in? Point me at the folder. | Files copied into inbox |
| 2 | Exclusion list | Optional | Anything in there the agent should not touch? | Excluded items stay in inbox |

### Material Analysis (analysis)

Read each file in the inbox and determine which area it belongs to:

| Content type | Route to |
|-------------|----------|
| Person-related (experience, expertise, decision preferences) | `{owner_root}` matching dimension |
| Brand-related (voice, positioning, visual assets) | `{brand_root}` matching brand domain |
| Business deliverables (articles, videos, client files) | `{business_root}` matching arena |
| Reference material (articles, notes, saved links) | `{research_root}` matching topic, current month folder |
| Rule-type content (naming conventions, format requirements) | `{specs_root}` |
| Uncertain | Stay in inbox |

- Move to target location, rename by the naming standard
- When unsure, leave in inbox — never guess

### Agent Rules

- After sorting, print a report: what moved where, what stayed, and why.
- An empty inbox is a goal, not a requirement.
- Print the file tree and stop.

### Build Verification

- Print the sorting report: what moved where, what stayed in inbox, why
- Confirm every item left in inbox has a valid reason
- Confirm moved files follow the naming standard
- Check against § Checklist item by item

## Related Methodology

- `../methodology/operations/` — how to judge ownership, boundaries between soft and hard deletion, enforcement of root discipline.

## Checklist

- [ ] Root directory contains only `CLAUDE.md` and declared subdirectories, no loose files
- [ ] Each new file belongs to some responsibility system
- [ ] Materials whose ownership can be determined have gone directly to actual target directories
- [ ] Batch concurrent task outputs are in dispatch hub directory
- [ ] Ended, archive-only content is in `archive/{YYYYMM}/`
- [ ] Archive directory names are four segments, disposition words in vocabulary
- [ ] `workstation-transit/` `input/` `output/` root directories have no loose files
- [ ] Batch directory names match four-segment format, files within retain original names
- [ ] Run logs, tasks, todos, handoffs are not in inbox, but in `{dashboard_root}`

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-14 | Declared editing-materials, transit logs/config |
| 2026-08-07 | Extracted skeleton from inbox specification |
