---
document_id: awp-knowledge-management-standard/directory/kb-area-research-skeleton
language: en
publication: public
title: "Knowledge Base Research/ Directory Skeleton"
---

# Research/ Directory Skeleton

> Defines the subdirectory structure, organization patterns used, and customization interfaces of the `{research_root}` root directory.

## Responsibilities

Houses cross-brand research material library: books, articles, videos, papers, reports, code repos from outside are imported, originals stored, standardized documents written, navigation and interpretation added as needed.

## Directory Structure

```text
{research_root}
├── CLAUDE.md          ← Fixed; entry
├── discovery/         ← Fixed; machine index, sole authoritative source for entire knowledge base
├── topics/            ← Fixed; generic long-term directions
│   └── {topic_name}/
│       ├── CLAUDE.md  ← Required; scope + search + index
│       └── materials/{YYYYMM}/{project}/
└── focus-areas/       ← Fixed; current focus areas
    └── {special_topic_name}/
        ├── CLAUDE.md  ← Required; scope + current judgment + index
        └── materials/{YYYYMM}/{project}/
```

- Path variable `{research_root}` is declared in `{specs_root}layout.yaml`, resolved as `research/`.
- `topics/` and `special-topics/` have identical structures; distinction is positioning only: topics are long-term directions, special-topics are current focus.
- Under partition root, **only** `CLAUDE.md` and `materials/` exist; no other subdirectories.
- Do not place checklist files under month directories; write checklists in partition root `CLAUDE.md`.
- One material physically exists in one place only; other places write path references only.

### Prohibited Directories Within Partition

`knowledge/`  -  `design/`  -  `progress/`  -  type-based subdirectories  -  month-level `CLAUDE.md`  -  batch directories  -  scattered list-type content files.

### Project Internal Structure

Each item under `materials/{YYYYMM}/` is a "project"; project directory name itself is four-segment:

```text
{YYYYMMDD}-{main_type}-{language_code}-{title}/
├── {YYYYMMDD}-raw-{language_code}-{title}[.{extension}|/]  ← Required  -  Unique  -  Original unchanged
├── {YYYYMMDD}-std-{language_code}-{title}.md               ← Required  -  Unique  -  Standardized content
├── {YYYYMMDD}-nav-{language_code}-navigation.md            ← Optional  -  Unique  -  For coordinate extraction
├── {YYYYMMDD}-card-{language_code}-interpretation.md       ← Optional  -  Unique
├── {YYYYMMDD}-{srt|note|ref}-...                             ← Optional whitelist
├── CLAUDE.md                                               ← Optional  -  Complex projects only
└── process/
    └── {YYYYMMDD}-proc-{language_code}-...                   ← Optional  -  Deletable  -  Not in machine index
```

Prohibited in project root: non-four-segment `.md` (except `CLAUDE.md`), `assets/` directory, short-name files (`std.md` `nav.md` `card.md` `raw.*`), process files at root level.

### Quality Tiers

| Tier | Required | Meaning |
|----|------|------|
| In-library | Original + standardized content | Material is in knowledge base |
| Extractable | Add navigation (when content has section structure) | Can read specific segment by coordinates |
| Referenceable | Add interpretation | Has usage judgment |

New projects in special-topics default to "extractable" tier or above.

### Ingestion Flow

```text
Download → Create four-segment project directory → Place original → Write standardized content
    → (Optional) Write navigation and interpretation → Update partition CLAUDE.md → Run health check → Refresh machine index
```

## Organization Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → partition type | **E3 Functional responsibility** | `discovery` `topics` `special-topics` |
| Partition → materials → month → project | **K1 Two-layer topics** | Material layer accumulates over time |
| `discovery/` | **K2 Index plus view** | Machine-read data files plus human-facing views |
| Project files | Four-segment naming | `{date}-{role}-{language}-{title}` |

Pattern definitions see `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{research_root}` | Root path of this area | `research/` (see `layout.yaml`) |
| Partition types | Which partition containers exist under root | `discovery`  -  `topics`  -  `special-topics` (closed set) |
| Topics list | Which partitions exist under `topics/` | Registered by user in root `CLAUDE.md` |
| Special-topics list | Which partitions exist under `special-topics/` | Registered by user in root `CLAUDE.md`; heat-up from topics, cool-down back to topics |
| Main type vocabulary | Second segment of project directory name | book  -  article  -  video  -  paper  -  report  -  code-repo  -  podcast  -  course  -  case  -  interview  -  dataset  -  analysis  -  field-test |
| Role vocabulary | Second segment of project file names | original  -  standardized  -  navigation  -  interpretation  -  subtitle  -  note  -  reference  -  process (closed set, no extension) |
| Language code | Third segment of project name and filename | Two lowercase language codes |
| Title length limit | Total length of project directory name | Eighty characters, unique across knowledge base |
| Default quality tier | Target tier for new projects | Topics as needed; special-topics at least "extractable" |

## ⑦ Build Procedure

Research uses both folder types at once, in the fixed order: dimension outside, time inside. Topics are meaning; material piles up in month buckets. Never the other way around, never deeper than four levels.

### Interview Questions (ask one at a time)

| # | Ask | Maps to |
|---|-----|--------|
| 1 | What topics are you actively tracking right now? (two or three is plenty) | One topic directory per answer |
| 2 | Do you have existing material you want to bring in? | Files filed into the correct topic month folder |

### Agent Rules

- Create a topic CLAUDE.md for each topic, saying what it covers and what belongs in it.
- Create a material directory with the current month folder inside.
- Write a topic index in the research root CLAUDE.md: one line per topic.
- If material is provided, file it by the naming standard into the correct month folder.
- Never create a date folder wrapping a topic. From root to any file: maximum four levels.
- Print the file tree and stop.

### Build Verification

- Print the full file tree of `{research_root}`
- File one piece of material — confirm the path is `{topic}/material/{YYYYMM}/` and the name follows the naming standard
- Check against § Checklist item by item

## Related Methodology

- `../methodology/research/` — how to write standardized content, how to mark coordinates for navigation, depth standards for interpretation cards, output types at cognition layer, version management for design documents.

## Checklist

**New Project**

- [ ] Directory name four-segment, unique across knowledge base, not exceeding eighty characters
- [ ] Located under `materials/{YYYYMM}/`
- [ ] Has exactly one original, one standardized content
- [ ] Metadata fields of standardized content pass validation
- [ ] Role words of extension files in whitelist
- [ ] Process files only under `process/`
- [ ] Project root has no short-name files, no `assets/`, no non-four-segment scattered `.md`

**New Partition**

- [ ] Partition root contains only `CLAUDE.md` and `materials/`
- [ ] `{research_root}CLAUDE.md` and index of partition type updated

**After Pipeline Run**

- [ ] Health check command has no errors
- [ ] Directory and navigation recalculated after changes to standardized content
- [ ] Machine index refreshed, count equals parseable projects

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted skeleton from research specification |
