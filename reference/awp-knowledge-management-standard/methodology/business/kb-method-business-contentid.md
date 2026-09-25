---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-contentid
language: en
publication: public
title: "Business Methodology  -  Content ID"
---

# Business Methodology  -  Content ID

> Manage unique identity of a piece of content across multiple channels: `content_id` format, display directory name, channel mapping, registry fields, rename gate.
> Inherits all constraints from `kb-method-business-general.md`.

`content_id` is not a platform's URL identifier (slug), nor is it a display title. It is an internal unique ID for a content unit that remains unchanged across channels.

## I. What We Manage

When identical content is reused across two or more channels, this file provides an invariant identity and logs each channel's location, state, link.

Content appearing in only one channel does not need `content_id`.

Single-channel directory structure is not managed here: website articles see `kb-method-business-article.md`, course materials see `kb-method-business-course.md`. This file manages cross-channel identity, display directory name, and registry fields.

## II. Two-Layer Naming

Cross-channel content uses two names:

```text
content_id         Machine unique identity, invariant across channels
Display Directory  Human-readable entry point, consistent across channels
```

Display directory name format:

```text
{YYYYMMDD}-{tool}-{topic}-{angle}
```

## III. `content_id` Format

```text
{timestamp}-{domain}-{topic}-{angle}
```

Must be four segments separated by three hyphens.

### Four-Segment Definition

| Segment | Meaning |
|---------|---------|
| `timestamp` | 14-digit creation time in format `YYYYMMDDHHMMSS` |
| `domain` | Content domain, product, or track; English lowercase continuous |
| `topic` | Topic cluster; English lowercase continuous |
| `angle` | Specific angle for this piece; English lowercase continuous; series can use three-digit numerical prefix |

### Eight Hard Rules

1. Global maximum of 3 hyphens.
2. Must split into exactly 4 segments.
3. No hyphens, underscores, spaces, non-ASCII characters, or punctuation within segments.
4. Only lowercase letters and digits allowed.
5. Do not include platform names.
6. Do not include version numbers (`v1`, `v2`, `new`, `final`).
7. Platform title, website URL identifier, or page title changes do not change `content_id`.
8. Once generated, `content_id` is permanent in principle. To change it, use mapping table and archiving.

Validation regex:

```text
^[0-9]{14}-[a-z0-9]{2,24}-[a-z0-9]{2,32}-[a-z0-9]{2,48}$
```

Hyphen count validation:

```text
content_id.count("-") == 3
```

## IV. How to Get `timestamp`

Take the first available from this order:

1. Content creation time: metadata in source file header, creation record, production run record.
2. Content first publication or registry time: platform-filled publication time, page creation time.
3. Explicit date in filename.
4. Legacy content migration when above three are unavailable: use migration registration time, mark `id_source: legacy_migration` in registry.

Prohibit three things:

- Generating separate sets of numbers per platform's publication time.
- Manually padding the same date with `000000` per day.
- Changing `timestamp` after republishing, editing, or retitling.

## V. `domain` Value Set

`domain` represents content domain, product, or track. Each organization maintains its own value set with uniform format. Examples:

```text
{product_abbreviation}   Specific product or tool
{track_abbreviation}     Content track
{method_domain}          Knowledge, methodology, thinking
{research_domain}        Deep research report
{production_step}        Content production and distribution
```

Rules for adding new `domain`:

1. Prefer existing value set.
2. New term must be 2–24 characters, lowercase English or digits continuous.
3. New term must be written into registry value set or this file.
4. Do not add `domain` due to channel changes.

## VI. `topic` Rules

`topic` represents topic cluster, grouping related content together.

Four rules:

1. `topic` should answer "what does this content group discuss."
2. Multiple pieces on the same topic must share the same `topic`.
3. `topic` does not represent this piece's angle, does not encode specific entry point.
4. `topic` does not encode platform name.

## VII. `angle` Rules

`angle` represents this piece's specific entry angle.

For regular content, write the angle directly. For series courses, add three-digit sequence before the angle word, like `001{angle}`, `002{angle}`.

Four rules:

1. Series numbering only in `angle` segment, three-digit numerical prefix.
2. Non-series content is not numbered.
3. `angle` only expresses this piece's angle, not channel or version.
4. When `angle` is too long, prefer deleting filler words instead of abbreviating to obscurity.

### Standard Examples

```text
20260414103022-{product_abbr}-{topic_cluster}-{angle}
20260415110008-{product_abbr}-{topic_cluster}-{another_angle}
20260426093000-{track_abbr}-{topic_cluster}-001{angle}
20260426094500-{track_abbr}-{topic_cluster}-002{angle}
20251208000000-{research_domain}-{source}-{report_topic}
```

## VIII. Display Directory Name

Display directory names apply to **channels where content is formed once at publication** (text subscription platforms, paid membership platforms). All four segments are fillable, so four segments are hard requirement.

```text
{YYYYMMDD}-{tool}-{topic}-{angle}
```

### Four-Segment Definition

| Segment | Answers | Char Count | Rules |
|---------|---------|:----------:|-------|
| Date | When published | 8 | `YYYYMMDD`, publication date. See `kb-method-business-article.md § Directory Name Date Extraction` for value order. Once set, never change |
| Tool | Which product or domain | 2–8 | Controlled vocabulary, add new tool per line |
| Topic | Which specific feature or concept | 2–6 | Freeform, use the most common name for this feature |
| Angle | What makes this piece unique | 2–8 | Freeform—specific effect, number, scenario, or method |

### Tool Segment Value Set

Each organization maintains its own tool segment controlled vocabulary, one abbreviation + full name per line. Requirements:

- Abbreviation 2–8 characters, recognizable at a glance.
- Add new tool per line, do not coin ad hoc terms.
- General topics also occupy one line (e.g., "AI" maps to "General AI Topics").

### Six Short-Name Rules

1. Four segments joined by `-`.
2. `content_id` does not go in directory name; record in directory's `channel-mapping.md`.
3. Short name once created is permanent—title can change, short name does not.
4. Same content across channels uses the same short name; website exception (keep English URL identifier).
5. Text social platforms retain sequence number before topic segment.
6. Video platforms retain episode number before topic segment.

### Main Text Filenames

Main text filenames are fixed per channel:

```text
{text_subscription_platform}/content/{YYYYMMDD}-{tool}-{topic}-{angle}/{platform}.md
{course_name}/content/{major_category}/{unit_directory}/course-text.md
{paid_membership_platform}/content/{YYYYMMDD}-{tool}-{topic}-{angle}/{platform}.md
```

Website article directory path and structure defined by `kb-method-business-article.md` separately; this file does not duplicate constraints to avoid two statements.

Course major category retains its aggregate classification name, does not convert to short-name format.

**Course units do not force four-dimensional hard requirement.** Course content includes both standalone units and series chapters; many titles cannot cleanly split into four segments. Forced splitting creates only artifice. Course-side rules and judgment per `kb-method-business-course.md § Naming Rules`; four-dimensional format here manages only channels where content forms once at publication.

## IX. `channel-mapping.md`

Every content directory root must have a `channel-mapping.md` recording this content's correspondence across channels. This file replaces the approach of "stuffing `content_id` into directory name."

### Location and Filename

```text
Location: Content directory root
Filename: channel-mapping.md (fixed, not changeable)
```

### Required Fields

```markdown
# Channel Mapping

- content_id: {14-digit timestamp}-{domain}-{topic}-{angle}
- Short name: {tool}-{topic}-{angle}
- Updated: {date_time}

| Channel | Status | Published | Title | Link | Local Path |
|---------|--------|-----------|-------|------|-----------|
| {text_subscription_platform} | Published / Draft / Not Sent | YYYY-MM-DD | ... | {complete_link} | This directory/{platform}.md |
| {paid_course_platform} | Published / Not Sent | YYYY-MM-DD | ... | {complete_link} | {course_name}/content/.../course-text.md |
| {paid_membership_platform} | Published / Not Sent | ... | ... | {complete_link} | This directory/{platform}.md |
| Website | Published / Draft / Not Sent | ... | ... | {complete_link} | website/content/{column}/{YYYYMMDD}-{slug}/{slug}.md |
| {text_social_platform} | Published / Not Sent | ... | ... | {complete_link or blank} | {platform}/content/{directory}/ |
```

### Six Rules

1. `Updated` changes every time channel mapping is modified, using ISO 8601 format.
2. `Status` uses only three values: `Published` / `Draft` / `Not Sent`.
3. `Link` published: fill complete URL; not sent: fill `-`.
4. `Local Path` relative to {business_root}.
5. After publishing to a new channel, backfill this table.
6. Early content without assigned `content_id`: mark "pending assignment."

## X. Relation to Platform Fields

| Field | Owned By | Will It Change |
|-------|----------|----------------|
| `content_id` | Internal unique identity | Unchanged across channels |
| `legacy_id` | Pre-migration old directory name or old URL identifier | Compatibility and traceability only |
| `{website}.slug` | Website URL identifier | Website only |
| `{channel}.title` | Each channel display title | Variable |
| `canonical_title` | Internal master title, generates display directory name | Variable, but keep history |

Four core principles:

- `content_id` can derive from website URL identifier but is not equal to it.
- Platform title not directly equal directory name; must converge to `canonical_title` first.
- Display directory name serves human maintenance; `content_id` serves machine correspondence.
- Directory name can shift due to `canonical_title` changes, but `content_id` is permanent in principle.

## XI. Registry Fields

Brand-level registry in `{business_root}/{brand}/content-registry/content-registry.yml`.

Each content entry includes:

```yaml
- content_id: 20260414103022-{domain}-{topic}-{angle}
  legacy_ids:
    - {old_identifier}
  id_source: source_created_at
  timestamp: "2026-04-14T10:30:22"
  domain: {domain}
  topic: {topic}
  angle: {angle}
  canonical_title: "{internal_master_title}"
  content_type: article
  source:
    path: "{business_root}/{brand}/{course_name}/content/{major_category}/{unit_directory}"
  channels:
    {website}:
      status: published
      slug: {url_identifier}
      title: "{title}"
      path: "{business_root}/{brand}/website/content/{column}/{YYYYMMDD}-{slug}/{slug}.md"
    {text_subscription_platform}:
      status: published
      title: "{title}"
      path: "{business_root}/{brand}/{text_subscription_platform}/content/{display_directory_name}/{platform}.md"
    {paid_course_platform}:
      status: published
      title: "{title}"
      path: "{business_root}/{brand}/{course_name}/content/{major_category}/{unit_directory}/course-text.md"
    {paid_membership_platform}:
      status: ignored
```

## XII. Rename Gate

Before truly renaming cross-channel content, complete these seven steps:

1. Generate `content-registry.yml`.
2. Generate temporary mapping table with fields: `old_path`, `new_path`, `channel`, `legacy_id`, `content_id`, `risk`.
3. Dry run, check conflicts, case collisions, target already exists, cross-channel inconsistency.
4. Migrate one `content_id` as sample, review references and indexes.
5. Batch migrate, then sync index files and registry.
6. Do not hard-delete old paths. Retain per archiving process or keep `legacy_ids` in registry.
7. One-off migration mapping table and migration ledger go to archive area after use.

Four prohibitions:

- No rename without registry.
- Do not generate separate `content_id` per channel.
- Do not rename directory without index.
- Do not change path without retaining `legacy_ids`.

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Migrated from content ID spec and generalized |
