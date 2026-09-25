---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-article
language: en
publication: public
title: "Business Methodology  -  Article Directory"
---

# Business Methodology  -  Article Directory

> Manage how the website content directory is organized: content root skeleton, single article structure, file naming, six-layer header metadata, lifecycle state machine.
> Inherits all constraints from `kb-method-business-general.md`.

Applies to the content root of any owned website, regardless of the underlying content management system. Other channels have their own rules; cross-channel identity follows `kb-method-business-contentid.md`.

Covers four states: published, scheduled, draft, static page.

## I. Six Design Principles

- **Content root archives only**: Local Markdown source of truth and cloud content correspond one-to-one. No machine files like export manifests, inventory tables, or seed ledgers in the content root.
- **Single source of truth**: One article equals one `{slug}.md`, with platform fields in the header metadata. State truth lives in header metadata, no second config file bolted on.
- **English site directories in English**: Top-level columns use industry English identifiers; body, title, description all in English.
- **Non-English site directories follow the site**: Non-English sites use existing column names; underscore prefixes not allowed.
- **Flat by default**: Default is `{YYYYMMDD}-{slug}/{slug}.md`. Lifecycle subdirectories (original / processing / publish / archive) are optional.
- **Second-level classification via tags**: Fine-grained directions go into `tags` in header metadata; no extra second-level folder layer.

## II. Content Root Skeleton

```text
{business_root}/{brand}/website/content/
├── CLAUDE.md                 ← human-readable index (optional but recommended)
├── {column}/                 ← top-level column (industry English identifiers)
│   └── {YYYYMMDD}-{slug}/
│       └── {slug}.md         ← the only body source of truth
├── drafts/                   ← local drafts (must not be written as _drafts)
├── pages/{page-slug}/        ← static pages
│   └── {page-slug}.md
├── tag/                      ← classification system plus icons (no machine-generated JSON)
└── archive/                  ← historical manual structure (read-only; no hidden name .archive)
```

### Forbidden in the Content Root

| Forbidden | Reason |
|------|------|
| Underscore-prefixed directories like `_drafts`, `_untagged` | Hard to recognize. Use `drafts/` uniformly, or file into the correct `{column}/` |
| Machine JSON like export manifests, inventory tables, seed ledgers | Machine audit and ledgers go into the tool's run directory, not the content root |
| Loose summary files under the business root | Cross-channel summaries go into the business root index file |
| Stacking CLI tool audit output in the content root | Same as above |

### Top-Level Columns

Top-level columns split by the site's main categories. English site uses industry English identifiers, examples:

| Column identifier | Industry tag |
|---------|---------|
| `technology` | Technology |
| `media` | Media |
| `commerce` | Commerce |
| `professions` | Professions |
| `care-learning` | Care & Learning |
| `operations` | Operations |
| `foundations` | Foundations |

The classification system source of truth lives in the content root's `tag/classification-system.md`. `tags[0]` must match the landing `{column}`; if the primary tag changes, change the directory or re-import.

## III. Single Article Structure

Only two things are required: the directory name format plus at least one body. Lifecycle subdirectories and root index files are both optional.

| Item | Required or optional | Description |
|---|:---:|------|
| Directory name `{YYYYMMDD}-{slug}/` | Required | Publish date plus URL identifier; the URL identifier itself has no date |
| Body `{slug}.md` (flat) or `publish/{platform}.md` | Required | Default flat `{slug}.md` |
| Original / processing / publish / archive / source / template / images | Optional | Only when the processing chain is long |

```text
{YYYYMMDD}-{slug}/
├── CLAUDE.md                 # optional, human-readable entry (no header metadata)
├── original/                 # optional, first-hand creation, native language, unprocessed
├── processing/               # optional, translation, refinement, expansion, review artifacts
├── publish/                  # optional, multi-platform final drafts, main file carries six-layer header metadata
├── archive/                  # optional, history and deprecated archives, keeps trace chain
├── source/                   # optional, code resources
├── template/                 # optional, template library
└── images/                   # optional, local image assets
```

### Directory Name Date Value

`{YYYYMMDD}` is the **publish date**, not the creation date. Take the first value obtainable in the order below; stop once obtained:

| Order | Value source | When applicable |
|:---:|---------|---------|
| 1 | `published_at` in main file header metadata (publish time backfilled by platform) | Published articles |
| 2 | `date` in main file header metadata | Article has fixed publish date, not yet pushed |
| 3 | Earliest publish time of this article across channel mapping | Article published on other channels first, synced to website later |
| 4 | Earliest file modification time in the directory | Drafts, historical articles, when the first three are unobtainable |

Criterion: the first 8 characters of the directory name form a valid date, and it is the same day as the first obtainable source in the table above. The value source goes into the main file header metadata, not recorded in the directory name or a sidecar file.

**Why publish date, not creation date.** Directories sort by date to "review content by publish rhythm". Order by creation date does not match what readers see—an article written over three weeks would rank before an article written in one day but published earlier. Also creation date has no authoritative source: file-system creation time changes after cross-machine sync, while publish time is a definite value backfilled by the platform.

**Timezone**: Platform-backfilled publish time is usually UTC; convert to local timezone before taking the date, consistent with the library-wide date convention.

### Boundaries of the Four Lifecycle Subdirectories

Once created, use them accordingly.

| Subdirectory | Entry condition | Exit condition | What goes in | What stays out |
|--------|---------|---------|--------|--------|
| original/ | First-hand language draft done | Never leaves | `{language}-original.md`, `material-{description}.md`, `_history/` | Translated drafts, images, source |
| processing/ | Translation, refinement, or re-review starts | Processing done, content written into `publish/` | Translation first drafts, refined drafts, re-review evidence (report, state, pre-fix snapshot) | Images, final drafts, original drafts |
| publish/ | Re-review passed and images ready | Moved into `archive/` when wholly deprecated | `{platform}.md` main file, local images (when `images/` not standalone) | Process drafts, original drafts |
| archive/ | Article, version, or candidate deprecated | Never leaves, keeps trace chain | `pre-restructure-*.md`, `candidate-title-*.md`, `pre-release-*.md`, `deprecated-*.md` | Files currently in use |

### Trigger Conditions for Three Additional Subdirectories

| Subdirectory | Trigger condition | What goes in |
|--------|---------|--------|
| source/ | Article ships with executable code, config, scripts | Original project structure plus `source.zip` |
| template/ | Article ships with a template library | Template file tree, original structure |
| images/ | Image workflow produced local images, not pure external links | `cover.png` plus `intext-{NN}-{description}.png` |

## IV. File Naming

Segment count and separator rules defined by `../../naming/kb-naming-segment-convention.md`. This section defines slot semantics and scenario tag vocabulary.

```text
{category}-{subcategory-or-object}-{stage-or-description}-{time-or-scenario}.{ext}
```

### Three Core Rules

1. **Compact date**: write `YYYYMMDD`, no hyphenated form, avoid mixing internal hyphens with separators.
2. **Product names and compound words drop internal hyphens**: use camelCase or merged writing.
3. **Segment 4 writes a semantic scenario tag**, not a tool version number—tool versions are meaningless for content tracing.

### Re-Review Scenario Tag Vocabulary

| Tag | Applicable scenario |
|------|---------|
| `pre-publish` | Final check before pushing to platform |
| `post-translation` | First re-review after translation first draft done |
| `post-refinement` | Re-check after adding style and search optimization |
| `patch` | Re-review after minor revision of a published article |
| `post-rewrite` | Re-review after major content rewrite |
| `quarterly` | Quarterly unified self-check |
| `restructure-to-4-subdirs` | Article directory changed from flat to four subdirectories |
| `deprecated` | Final archive before article takedown |

### Naming Matrix

All subdirectories optional; this table constrains "how files are named once created".

| Subdirectory | File naming |
|--------|---------|
| original/ | `{language}-original.md`, `material-{description}.md`, `_history/{original-name}-{YYYYMMDD}.md` |
| processing/ | `translate-{language-pair}-{stage}.md`; `re-review-{type}-{YYYYMMDD}-{scenario}.{md or json}` |
| publish/ | `{platform}.md`; local images `cover.png`, `intext-{NN}-{description}.png` |
| archive/ | `pre-restructure-{original-structure}-{YYYYMMDD}-{goal}.md`; `candidate-title-{direction}-{draft-or-final}-{YYYYMMDD}.md`; `pre-release-{original-structure}-{YYYYMMDD}-with-platform-id.md`; `intermediate-{description}-{stage}-{YYYYMMDD}.md`; `deprecated-{reason}-{YYYYMMDD}-{platform}.md` |
| source/ | Original project structure plus optional `source.zip` |
| template/ | Template file tree, original structure |
| images/ | `cover.png`, `intext/{NN}-{description}.png`, `_source-files/{original-editing-file}.{extension}` |

## V. Six-Layer Header Metadata of the Main File

Main file location defaults to flat `{slug}.md`; with `publish/` created, it is `publish/{primary-platform}.md`.

The six layers follow strictly in the order below.

### Layer 1: Platform Fields

Platform fields follow the content management system's interface docs. Typical set:

```yaml
cms_id: null                        # backfilled after push, null at draft stage
cms_uuid: null                      # backfilled after push, null at draft stage
title: "..."
slug: "..."
status: draft                       # strict platform enum, example: draft / scheduled / published / sent
visibility: public                  # public / members / paid
featured: false
published_at: "2026-04-26"
updated_at: null
tags: [...]
custom_excerpt: "..."               # summary, length per platform limit
feature_image: "..."                # cover external link
feature_image_alt: "..."            # cover alt text, covers search and accessibility
feature_image_caption: null
meta_title: "..."                   # search result title
meta_description: "..."             # search result description
og_title: "..."                     # social share title
og_description: "..."
og_image: null
twitter_title: "..."
twitter_description: "..."
twitter_image: null
canonical_url: "..."
codeinjection_head: |               # structured data script
  <script type="application/ld+json"> ... </script>
codeinjection_foot: null
```

### Layer 2: Article-Level Metadata

```yaml
article:
  brand: {brand}                    # required
  primary_platform: {primary-platform}  # required
  source_language: zh               # required, original creation language
  source_file: original/{language}-original.md  # required; pure original may be null
  series: {series-identifier}       # optional
  series_index: 2                   # optional
  source_word_count: 12345          # optional, original character count
```

### Layer 3: Source Code Assets

```yaml
source_code:
  available: false                  # whether distributable source included
  path: null                        # source local path
  member_only: false                # whether member-only
  size: null                        # optional
  notes: null                       # optional
```

### Layer 4: Cross-Platform Sync State

```yaml
publish:
  {primary-platform}:
    enabled: true
    file: publish/{primary-platform}.md
    last_synced_at: '2026-04-26T03:40:00Z'   # null means not pushed yet
    word_count: 5722
  {other-platform}: { enabled: false }
```

### Layer 5: Re-Review State

```yaml
review:
  last_run: '2026-04-26'
  version: {process-version}        # machine-readable tracing, unrelated to file name
  scenario: post-translation        # scenario tag, see vocabulary above
  evidence:
    report: processing/re-review-report-2026-04-26-post-translation.md
    state: processing/re-review-state-2026-04-26-post-translation.json
    snapshot: null                  # pre-fix snapshot, only for auto-fix mode
```

### Layer 6: Lifecycle

```yaml
lifecycle: review_passed            # seven-state enum, see below
deprecated_at: null                 # only filled when lifecycle is deprecated
deprecated_reason: null
```

### Who Writes, Who Reads, Per Layer

| Layer | Namespace | Who writes | Who reads |
|:--:|---------|------|------|
| 1 | Top-level no prefix | Platform tools, re-review flow | Platform push tool |
| 2 | `article.*` | Creator, translation flow | Knowledge base retrieval |
| 3 | `source_code.*` | Creator, re-review flow | Member distribution flow, image flow |
| 4 | `publish.*` | Multi-platform publishing flow | Multi-channel publishing tool, scheduling |
| 5 | `review.*` | Re-review flow | State reports |
| 6 | `lifecycle`, `deprecated_*` | Lifecycle flow | Retrieval, scheduling |

Key: platform tools only read layer-1 top-level fields. New `article`, `source_code`, `publish`, `review`, `lifecycle` are treated as unknown fields and ignored; no conflict.

## VI. Relationship Between Platform `status` and `lifecycle`

The two are decoupled, each managing its own:

| Field | Who defines | Enum | Meaning |
|------|--------|------|------|
| Layer 1 `status` | Strictly defined by platform | `draft` / `scheduled` / `published` / `sent` | Publish state shown in platform backend |
| Layer 6 `lifecycle` | Extended by this methodology | `draft` / `translated` / `review_passed` / `ready` / `scheduled` / `published` / `deprecated` | Internal content lifecycle in the knowledge base |

Mapping rule (derive `status` from `lifecycle`):

| `lifecycle` | Recommended `status` | Description |
|-------------|:------------:|------|
| `draft` | `draft` | Original draft exists, no translation |
| `translated` | `draft` | Translation done, awaiting re-review, still platform draft |
| `review_passed` | `draft` | Re-review passed, awaiting images, still platform draft |
| `ready` | `draft` | Images ready, awaiting push, still platform draft |
| `scheduled` | `scheduled` | Pushed to platform, publish time in future, waiting for auto-publish |
| `published` | `published` | Live |
| `deprecated` | `draft` | Taken down |

Red line: writing `lifecycle` extended state values (e.g. `review_passed`) into layer-1 `status` is forbidden. Platform API rejects them; push fails or bounces back to draft.

## VII. `lifecycle` State Machine (Seven States)

```text
draft ──translate──> translated ──re-review──> review_passed ──images──> ready ──schedule──> scheduled ──auto──> published
                                                                                                    │
                                                                                                    ├─ update ──> published (keep platform ID)
                                                                                                    └─ deprecate ──> deprecated
```

| Stage | `lifecycle` | `status` | File location | Platform ID |
|------|:---:|:---:|---------|:---:|
| Drafting | `draft` | `draft` | Original saved, main file placeholder | null |
| Translated, awaiting re-review | `translated` | `draft` | Translation first draft exists | null |
| Re-review passed, awaiting images | `review_passed` | `draft` | Re-review report exists, main file has review block | null |
| Images ready, awaiting push | `ready` | `draft` | Cover is a real external link, not placeholder | null |
| Uploaded, awaiting auto-publish | `scheduled` | `scheduled` | Publish time in future, scheduled on platform side | has value |
| Published | `published` | `published` | Main file has platform ID, live on platform side | has value |
| Deprecated | `deprecated` | `draft` | Main file moved to `archive/deprecated-{date}-{reason}.md` | keep old value |

### Two Rules for the Scheduled State

- When pushing, create directly in "scheduled" state with the publish time; do not push a draft first and change to scheduled afterward.
- Once the platform accepts the schedule and returns success, **immediately** change both local layer-1 `status` and layer-6 `lifecycle` to `scheduled`.

Core principle: state is expressed twice—**file location plus `lifecycle`**—and layer-1 `status` aligns with the platform, avoiding "field says re-review passed but platform push failed".

## VIII. Header Metadata of Satellite Files

Non-main-file header metadata only carries that file's own specific fields; **no duplicate cross-platform or cross-file state**, avoiding inconsistency from writing state in multiple places.

First-hand original draft:

```yaml
parent: publish/{primary-platform}.md   # reverse pointer to main file
language: zh
title: "{original-title}"
word_count: 12345
created_at: 2026-04-21
```

Channel material draft:

```yaml
parent: publish/{primary-platform}.md
language: zh
platform_origin: {platform}
title: "{platform-version-title}"
```

Other-platform final draft:

```yaml
parent: publish/{primary-platform}.md
platform: {platform}
title: "{platform-version-title}"
{platform-specific-field}: ...
```

Re-review state file is pure machine-readable JSON, no header metadata:

```json
{
  "slug": "...",
  "scenario": "pre-publish",
  "version": "...",
  "before": { "words": 4778, "schema": 3, "bans": 0 },
  "after": { "words": 4989, "schema": 3, "bans": 0 },
  "weighted_score": 95.7,
  "verdict": "PASS"
}
```

## IX. Article Root Index File

Root index file is optional—the source of truth for machine-readable metadata is the main file header metadata; this one only serves human-readable navigation. If written, follow the skeleton below: no header metadata (so it is not mistaken for a machine-readable source of truth), five sections.

```markdown
# {article-title}

> **State**: `{lifecycle}`  -  Last re-review {YYYYMMDD} {scenario}  -  {state-note}
> **Brand**: {brand}  -  **Primary platform**: {primary-platform}  -  **URL identifier**: `{slug}`  -  **Words**: {word_count}

## Platform Sync Overview

| Platform | State | File | Note |
|------|------|------|------|

## Subdirectory Navigation

| Subdirectory | Purpose | Main content |
|--------|---------|------|

## Key Files

- Main file: {path} — source of truth for header metadata
- First-hand original draft: {path}
- Last re-review report: {path}

## Metadata Source of Truth

This file only serves human-readable navigation. All machine-readable metadata follows the main file header metadata. This file being stale does not affect the publishing flow.
```

## X. Upper-Level Directory Conventions

### `tag/` Classification System

```text
content/tag/
├── classification-system.md ← primary and secondary classifications plus tagging rules (human-readable source of truth)
├── CLAUDE.md       ← icon description
├── *.svg           ← active tag icons
└── archive-old-icons/   ← old system icons (optional archive)
```

- `tags` ordered per classification system; primary tag maps one-to-one to `{column}/`.
- Secondary directions are tags only; no second-level folders.

### `pages/` Static Pages

Path is `pages/{page-slug}/{page-slug}.md`. Legal pages, about pages, contact pages do not go through the article re-review flow. Scattered `pages/*.md` forbidden; must enter subdirectories.

### `drafts/` Local Drafts

Only local drafts not yet published or not exported on the cloud. After publishing, move into the corresponding `{column}/`. Writing `_drafts` forbidden.

### `archive/` Historical Structure

Read-only. Using hidden name `.archive` as a live staging area forbidden.

## XI. Anti-Patterns

| Mistake | Correct approach |
|------|---------|
| Export manifests, inventory tables, seed ledgers in content root | Delete; audit output into tool run directory |
| Underscore prefix `_drafts/` | Use `drafts/` |
| Directory name only URL identifier, no date | Use `{YYYYMMDD}-{slug}/` |
| Directory name date is creation date | Use publish date |
| Sidecar `meta.yaml` | Write into header metadata |
| Second-level detail direction folders under top-level columns | Detail directions as tags only |
| Non-English column names on English site | Use industry English identifiers |
| Scattered `pages/about.md` | Use `pages/about/about.md` |

## XII. Checklist

- [ ] Choose `{column}`, consistent with `tags[0]`
- [ ] Create `{column}/{YYYYMMDD}-{slug}/`
- [ ] Write `{slug}.md` with platform header metadata (default flat)
- [ ] Confirm no machine JSON in content root, no underscore-prefixed staging directory
- [ ] After publishing to a second channel, register in content registry
- [ ] Create original, processing, source, image subdirectories as needed

## Change Record

> Rolling window, keep latest 3 entries, each ≤20 chars.

| Date | Change |
|------|---------|
| 2026-08-07 | Migrated from article directory spec and generalized |
