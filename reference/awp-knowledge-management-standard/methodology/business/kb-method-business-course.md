---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-course
language: en
publication: public
title: "Business Methodology  -  Course Materials"
---

# Business Methodology  -  Course Materials

> Manage course unit directory organization: main text, delivery, and resources—three asset layers; two naming schemes for units and chapters; state machine; channel derivation.
> Inherits all constraints from `kb-method-business-general.md`.

Applies to paid courses, bootcamps, member courses, member mirrors, tutorial resource packages.

Does not apply to website content—see `kb-method-business-article.md` for website articles.

## I. Core Positioning

- Member course local canonical source stays in course directory, not in a separate directory per platform.
- Unit directory name is `{YYYYMMDD}-{1 to 3 fields from coarse to fine}/`; segment count follows whether the title naturally splits, not forced. Chapters within multi-chapter units have their own naming scheme; rules and judgment both in "Naming Rules" section.
- `content_id` recorded in directory's `channel-mapping.md`.
- Member course main text file always named `course-text.md`; filename does not repeat `content_id`.
- `course-text.md` contains only main text, not metadata like state, `content_id`, channel paths, or usage instructions; those go in unit's `CLAUDE.md`.
- For member-operable courses, `course-text.md` starts with ~400 characters of short prompt, followed by usage instructions; full deployment prompt goes in `delivery/` specialized file.
- Other channels are derivative drafts, placed in respective channel directories, not in course unit.
- `CLAUDE.md` is unit metadata entry point, recording state, channel paths, resource inventory, boundaries, and creation log. Optional: when absent, cross-channel links use `channel-mapping.md`.
- Course Markdown files default to no website platform header metadata. To publish on website, generate separate publication file in website content directory.
- Course units organize in three asset layers: `course-text.md` is member text, `delivery/` contains member-usable, copyable, executable, downloadable, deployable deliverables, `resources/` contains authoring and verification materials.
- `delivery/` targets members, contains copyable, executable, downloadable, deployable content; default flat layout, no pre-built type directory.
- Single-file deliverables in `delivery/` use "purpose + keyword" naming, balancing visual recognition and retrieval.
- If `delivery/` itself is a deployment guide executable by any Agent, must provide both `delivery/AGENTS.md` and `delivery/CLAUDE.md`; content can be identical.
- Only multi-file source packages, complete capability packages, complete CLI tool packages—"asset itself is a directory"—get subdir under `delivery/` per asset name.
- `resources/` targets authoring, holds materials, cloud references, book materials, local practice, visual materials; does not hold member deliverables.

## II. Standard Unit Structure

```text
{major_category}/{unit_directory}/
├── CLAUDE.md
├── course-text.md
├── channel-mapping.md
├── delivery/
│   ├── CLAUDE.md
│   ├── {deliverable}.md
│   └── {asset-name}/  # multi-file assets only
├── resources/
│   ├── CLAUDE.md
│   ├── materials/
│   │   └── materials.md
│   ├── cloud-reference/
│   ├── book-materials/
│   ├── local-practice/
│   └── visual-materials/
└── archive/
```

### Files That Must Exist (Only These Two)

```text
course-text.md       Member course local canonical source
channel-mapping.md   Cross-channel correspondence: page ID, complete links per channel
```

### Optional Files

Write per the responsibility below; absence is not violation.

```text
CLAUDE.md            Unit metadata, channel paths, resource inventory, creation log
delivery/CLAUDE.md   Delivery directory index and member usage boundaries
resources/CLAUDE.md  Resource directory index and authoring material classification
resources/materials/materials.md   Topic, title, materials, arguments, channel differences, facts to verify
```

### Directories That Must Exist

```text
delivery/         Member-copyable, executable, downloadable, deployable deliverables entry point; default flat
resources/        Authoring, verification, retrospective materials entry point
resources/materials/     Creation input, drafts, processing records, argument materials
archive/          Discarded drafts, old structure snapshots, obsolete materials
```

### Optional Directories

```text
delivery/{purpose-Keyword}.md                  Single-file deliverable: prompt, template, best practice, install guide, checklist
delivery/{asset-name}/                         Multi-file deliverable: source package, CLI tool package, capability package, complete example
delivery/AGENTS.md                             Agent universal entry point; required when delivery directory self-executable
resources/cloud-reference/  Official docs, web materials, search results, web snapshots, cloud product pages
resources/book-materials/  Book excerpts, reading notes, chapter cards, page references, reading list rationale
resources/local-practice/  Local real config experience, tool best practice snapshots, run records, pitfall records
resources/visual-materials/  Screenshot sources, cover references, config photo references, operation screenshot materials
resources/materials/processing/  Historical drafts, iteration records, long material drafts
resources/materials/original/  Raw input, old originals, unorganized materials
```

## III. `channel-mapping.md`

This is the sole entry point for cross-channel coordination. Every channel gets complete link; published: fill link, not sent: fill `-`.

```markdown
# Channel Mapping

- page_id: {page_identifier}
- database: {database_alias}
- content_id: {content_id}
- Short name: {unit_directory_name}
- Sync time: {date_time}

| Channel | Status | Published | Title | Link | Local Path |
|---------|--------|-----------|-------|------|-----------|
| {paid_course_platform} | Sent | - | {title} | {complete_link} | This directory/course-text.md |
| {text_subscription_platform} | Not Sent | - | - | - | - |
| {paid_membership_platform} | Not Sent | - | - | - | - |
| Website | Not Sent | - | - | - | - |
| {text_social_platform} | Not Sent | - | - | - | - |
```

Link field rules:

- Per-channel link uses that platform's complete URL format, filled by sync tool or manually.
- Unpublished channel link: write `-`, never leave blank.

## IV. Channel Derivative Paths

Course unit keeps only the canonical source. Derivatives go to respective channel directory:

```text
Course canonical source:
{business_root}/{brand}/{course_name}/content/{major_category}/{unit_directory}/course-text.md

Social channel lead-generation draft:
{business_root}/{brand}/{social_channel}/content/{unit_directory}/channel.md

Member platform mirror:
{business_root}/{brand}/{member_platform}/content/{unit_directory}/membership.md

Website version:
{business_root}/{brand}/website/content/{column}/{YYYYMMDD}-{site_slug}/{site_slug}.md
```

Cross-channel correspondence logged to `{business_root}/{brand}/content-registry/content-registry.yml`.

## V. Unit `CLAUDE.md` Template

````markdown
# {Unit Title}

> **State**: `draft`  -  {YYYYMMDD} created  -  {YYYYMMDD} updated
> **Major Category**: {category_name}
> **Form**: {Tutorial Article / Tutorial Series / Research Report / Source Project / Quick Reference}
> **Difficulty**: {Beginner / Intermediate / Advanced}
> **content_id**: `{content_id}`

## Channel Overview

```text
Course canonical source
  State: To be written
  File: course-text.md
  Link: —
  Note: Member main version

Social channel
  State: To be written
  File: {business_root}/{brand}/{social_channel}/content/{unit_directory}/channel.md
  Link: —
  Note: Public lead-generation version

Member platform
  State: To be written
  File: {business_root}/{brand}/{member_platform}/content/{unit_directory}/membership.md
  Link: —
  Note: Member mirror version
```

## Resource Inventory

- Course text: `course-text.md`
- Delivery index: `delivery/CLAUDE.md`
- Deliverables: `delivery/`
- Resource index: `resources/CLAUDE.md`
- Materials: `resources/materials/materials.md`
- Cloud reference: `resources/cloud-reference/`
- Book materials: `resources/book-materials/`
- Local practice: `resources/local-practice/`
- Archive: `archive/`

## Authoring Boundaries

- {boundary 1}
- {boundary 2}

## Creation Log

- {YYYYMMDD}: {record}
````

## VI. State Machine

```text
draft      Course text or materials in draft, not published yet
ready      Course text complete, pending upload or channel derivatives
published  At least one channel published, link written
archived   Content retired, superseded, or materials moved to archive/
```

Units with `CLAUDE.md` record state at top, channel state in "Channel Overview." Units without `CLAUDE.md` reference channel state from `channel-mapping.md` status column.

Never express state in directory name.

## VII. New Unit Creation Steps

```bash
SHORTNAME="{unit_directory_name}"   # Format per "Naming Rules › Unit Naming"
DST="{business_root}/{brand}/{course_name}/content/{major_category}/${SHORTNAME}"

mkdir -p "$DST/delivery" "$DST/resources"/{materials,cloud-reference,book-materials,local-practice,visual-materials} "$DST/archive"
$EDITOR "$DST/course-text.md"
$EDITOR "$DST/channel-mapping.md"
$EDITOR "$DST/delivery/CLAUDE.md"
$EDITOR "$DST/resources/materials/materials.md"
$EDITOR "$DST/resources/CLAUDE.md"
$EDITOR "$DST/CLAUDE.md"
```

For multi-channel release, next create derivatives in channel directories:

```bash
SHORTNAME="{unit_directory_name}"
SOCIAL="{business_root}/{brand}/{social_channel}/content/${SHORTNAME}"
MEMBERSHIP="{business_root}/{brand}/{member_platform}/content/${SHORTNAME}"

mkdir -p "$SOCIAL" "$MEMBERSHIP"
$EDITOR "$SOCIAL/channel.md"
$EDITOR "$MEMBERSHIP/membership.md"
```

## VIII. Naming Rules

Segment count and separator rules defined by `../../naming/kb-naming-segment-convention.md`; this section defines specific semantics per slot.

### Distinguish Two Object Types

Course content has two directory types, different sorting and naming rules. Identify which before applying rules.

| Object | Where | Sort By | Rules |
|--------|-------|---------|-------|
| Unit | Under `{major_category}/` or `{major_category}/{subcategory}/` | Date | See "Unit Naming" |
| Chapter | Inside a multi-chapter unit | Series sequence | See "Chapter Naming" |

Judgment: **Is this directory its own course, or a specific lecture in a course?** If "specific lecture," it is a chapter. Sibling chapters in the same series, often generated together same day—date cannot sort; only sequence number can. That is the distinction.

### Unit Naming

```text
{YYYYMMDD}-{field1}[-{field2}][-{field3}][-{slug}]
```

Five hard rules (violation machine-checkable):

| # | Rule | Judgment |
|:-:|------|----------|
| 1 | Start with `{YYYYMMDD}-` | First 8 characters are valid date; 9th is `-` |
| 2 | At least one non-empty field after date | After removing `{YYYYMMDD}-`, not empty |
| 3 | Total length not over 80 characters | Exceeds: put full title in unit `CLAUDE.md`, shorten directory name |
| 4 | Name does not express state | No `draft`, `to-send`, `sent`, `obsolete`, `final`, `v2` etc.; state in `CLAUDE.md` or `channel-mapping.md` |
| 5 | Date uses compact format | Not hyphens-separated date |

Field guidance (author judgment, not machine-checked):

After date, write 1–3 fields **coarse to fine**—first "which batch," then "what," finally "from which angle." Write as many layers as title naturally splits; **do not invent missing layers**.

| Segments | When | Example |
|:--------:|------|---------|
| 1 | Standalone, no series | `20251210-{tool}generate-name-cards-and-posters` |
| 2 | Series, title is one complete sentence | `20260316-SEO-basics-01-how-search-results-appear` |
| 3 | Series, title naturally splits "what" and "how" | `20260316-SEO-basics-03-keywords-find-words-users-really-search` |

**Why not force four segments.** Above two examples are same series, same day, same batch: Lecture 03's topic "keywords" stands alone; Lecture 01 is one complete sentence, cannot cleanly split. Forcing Lecture 01 a fourth segment invents one—artificial and unhelpful. **Segment count follows title structure, not rule.**

Optional `{slug}` tail: if unit has external English identifier (command name, page ID), append at end, separated from the title by `-`.

```text
20251220-38.zero-foundation-programming-hands-on-code-push-cmd-git-push-code
                                                     └─ slug: cmd-{command}-{audience}
```

### Chapter Naming

```text
{series_name}[{NN}]{title}{content_id}
```

`{content_id}` is from content registry, format `{14-digit timestamp}-{domain}-{topic}-{angle}`.

Four hard rules:

| # | Rule | Judgment |
|:-:|------|----------|
| 1 | Name includes 14-digit timestamp; timestamp to end is valid `content_id` | Regex `\d{14}-[a-z0-9]+(-[a-z0-9]+)*$` matches to end |
| 2 | Non-empty before timestamp, starts with series name | Clear at a glance which series |
| 3 | Total length not over 80 characters | Per unit rule 3 |
| 4 | Ordered chapters get two-digit sequence `{NN}` right after series name | Start from `01`, continuous; supplements, extras not numbered |

Examples:

```text
{series_name}01{title}20260317132543-{domain}-{topic}-{angle}
└─series──┘└NN┘└── title ───┘└──────────── content_id ────────────┘
```

**Why chapters have no date, no `-` segment separator.** Same-batch chapters may differ only seconds in timestamp—date sorts nothing. Sequence sorts. Title and `content_id` need no separator: 14-digit timestamp itself is unambiguous boundary; regex cleanly splits. This form "clear to see, sortable, findable" hits all three.

`content_id` in directory name is chapter exception; units do not. Why: chapters lack date segment, need stable ID to match platform pages; units have date + title which suffice.

### Filename Naming

```text
Main text: course-text.md
Delivery index: delivery/AGENTS.md + delivery/CLAUDE.md
Delivery file: delivery/{purpose-Keyword}.md
Delivery dir: delivery/{asset-name}/
Resource index: resources/CLAUDE.md
Material file: resources/materials/materials.md
Cloud reference: resources/cloud-reference/
Book materials: resources/book-materials/
Local practice: resources/local-practice/
Visual materials: resources/visual-materials/
Social channel text: channel.md
Member platform text: membership.md
Website text: {site_slug}.md
```

`content_id` recorded in directory's `channel-mapping.md` and content registry. **Unit directory name and `course-text.md` filename never include `content_id`**; chapter directory name does—it is part of chapter form.

## IX. Antipatterns

- Writing course text as `distribution/course-text.md`.
- Putting channel derivatives back in course unit.
- Naming main text `course-text ({content_id}).md`.
- Writing state, `content_id`, usage methods, channel paths in top of `course-text.md`.
- Forming member-operable course text as lecture-only, no short prompt entry.
- Putting `materials.md` in unit root.
- Adding website platform header metadata to course materials.
- Putting member-usable source code, prompts, templates, CLI tools, capability packages in `resources/`.
- Naming single-file deliverable with only abstract terms, failing readability or retrieval.
- Pre-building type folders under `delivery/` (source, CLI, capability, prompts, templates).
- Scattering official verification, book excerpts, local practice in unit root.
- Scattering source code, templates, screenshots in unit root.
- Directly deleting obsolete materials; they go to `archive/`.
- Inventing nonexistent "angle" just to force four segments.
- Prefixing chapter directory with date—same-batch chapters all same date, cannot sort; need sequence.
- Encoding state in unit directory name.

## X. Restructuring Legacy Layout

When restructuring, do not delete—move content by type.

| Old Structure | New Location |
|---------------|--------------|
| `processing/*.md` | `resources/materials/processing/` |
| `original/*.md` | `resources/materials/original/` |
| `distribution/*.md` | Move by channel to respective channel directory; unclear: move to `archive/old-structure/` |
| `resources/source-code/`, `resources/prompts/`, `resources/templates/` single-file | Flat to `delivery/` |
| Same dirs' multi-file packages | Move by asset name to `delivery/{asset-name}/` |
| `resources/reference/` official docs, web snapshots | `resources/cloud-reference/` |
| `resources/reference/` book excerpts | `resources/book-materials/` |
| `resources/reference/` local config experience | `resources/local-practice/` |
| `delivery/` type subdirs (prompts, templates, source, CLI, capability) | Single-file to `delivery/` flat; empty dirs delete; multi-file retain but rename subdir to specific asset name |

## XI. Checklist

- [ ] Unit directory name meets five hard rules: date prefix, field non-empty, not over 80 char, no state words, date compact
- [ ] Fields coarse to fine, 1–3 segments, no forced-in missing layers
- [ ] Chapter directory name meets four hard rules: end is valid `content_id`, series name prefix, not over 80 char, ordered chapters have two-digit sequence
- [ ] Unit root has `course-text.md`
- [ ] Member-operable course has short prompt at `course-text.md` start; complete prompt in `delivery/` specialized file
- [ ] Self-executable deployment delivery dir has both `delivery/AGENTS.md` and `delivery/CLAUDE.md`
- [ ] Unit root has no `materials.md`
- [ ] Optional: unit root has `CLAUDE.md`
- [ ] Optional: `delivery/CLAUDE.md` documents member delivery flat rules
- [ ] Optional: `resources/CLAUDE.md` documents authoring material classification
- [ ] Optional: `resources/materials/materials.md` holds authoring input
- [ ] Cloud reference to `resources/cloud-reference/`
- [ ] Book materials to `resources/book-materials/`
- [ ] Local practice to `resources/local-practice/`
- [ ] Member single-file deliverable flat in `delivery/`
- [ ] Member single-file deliverable named "purpose + keyword"
- [ ] Deployment delivery dir: every file serves deployment chain, no mixed daily materials
- [ ] `delivery/` does not pre-build type empty folders
- [ ] Multi-file deliverable per specific asset name subdir
- [ ] Each channel derivative in respective channel directory
- [ ] Parent major category index already registered
- [ ] `channel-mapping.md` created, course canonical link filled
- [ ] Cross-channel registered to content registry

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Migrated from course materials spec and generalized |
