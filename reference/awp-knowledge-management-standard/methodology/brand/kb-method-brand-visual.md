---
document_id: awp-knowledge-management-standard/methodology/brand/kb-method-brand-visual
language: en
publication: public
title: "Brand Visual Asset Management Methodology"
---

# Brand Visual Asset Management Methodology

> Managing organization, naming, sizing, and reuse rules of brand visual assets.
> Applicable to any industry, any brand's visual asset library.

---

## Positioning

Visual assets mean the brand's **visual media files**: logos, avatars, banners, product images, course covers, etc. They are the single source for any channel using images and any workflow fetching images.

Canonical copy lives in `{brand_root}/{brand}/identity/visual/`, split into two layers, same for all brands:

| Layer | Path | Holds |
|----|------|--------|
| **Rules** | `identity/visual/rules/` | Decision documents on color, fonts, tone, etc., named by four-segment scheme |
| **Assets** | `identity/visual/assets/` | Physical files, fully flat with zero subdirectories, `{category}-{object}-{variant}-{spec}.{ext}` |

**Why rules and assets separate**: text needs reading, citing, version evolution; images need fetching, finding by purpose. The two organization logics differ, mixing them in one layer makes both awkward. This is the only place in the brand directory allowed to split one more level.

This methodology manages two things:

1. Which visual assets a brand should complete, at what sizes
2. How to name a single file so the Agent can judge purpose and size from the name alone

Out of scope:

| Not managing | Where it goes |
|---------|------|
| In-content embedded images (article illustrations) | The corresponding project's material directory |
| Temporary material, drafts | Transit directory |
| Screenshots, reference images, benchmarking images | Reference material library or research directory |
| In-production material | The corresponding project directory |

---

## Design Philosophy

- **By purpose, not by format**: the first segment of a file name uses **purpose names** like "icon / avatar / banner," not **format names** like "png / jpg / svg." The Agent fetches images by purpose.
- **Name is metadata**: file name carries category, object, variant, spec; the Agent can judge without opening.
- **Directly citable**: asset paths are stable; any document, product page, or video script can cite them directly.
- **Multi-platform, one image source**: different platform sizes of the same asset lie flat in one layer, distinguished by the spec segment.
- **No empty shells in advance**: no placeholders without actual assets; don't generate unused files to fill a category table.

---

## Asset Layer Fully Flat

✅ The asset directory has **no subdirectories**—physical files all lie flat in one layer, classified by four-segment file names. Sorted by file name, same-kind items naturally cluster into one block (`icon-*` together, `avatar-*` together), no directory needed.

> **Why images are flat too**—counterexample: a brand's logo once had 46 subdirectories, four levels deep; fetching one favicon took four clicks. After flattening, 97 assets sit in one layer, grouped by file-name sorting, and finding things is faster.

✅ External platforms' or tools' official logos are isolated from the brand's own assets by the first segment, e.g., first segment writes `third-party`, never mixed with brand logos.

---

## Asset Category System

✅ Brand visual assets split into 17 types. **Types are a checklist, not a directory layer**—this table answers "which assets a brand should complete and at what sizes," not "which folder a file goes in." What a file is called is decided by this file's naming rules and that brand's asset directory index.

### The 17 Asset Types

| Category | Type | Holds | Required |
|------|------|--------|:----:|
| **Logo** | Lettermark | Brand abbreviation plus graphic | ✅ |
| | Wordmark | Brand full name, horizontal | ⚪ |
| | Brand icon | Pure graphic symbol, no text | ⚪ |
| **Avatar** | Video-platform avatar | Channel avatar, 800×800 recommended | ✅ |
| | Social main-site avatar | Personal avatar, 400×400 | ✅ |
| | Code-platform avatar | Avatar, 460×460 | ⚪ |
| | Generic social avatar | Includes small-size previews 40 / 48 / 98 / 134 | ⚪ |
| **Banner** | Video-platform banner | Channel banner 2560×1440, safe area 1546×423 | ⚪ |
| | Social main-site header | Personal page header 1500×500 | ⚪ |
| | Professional-social banner | Personal page banner 1584×396 | ⚪ |
| | Official-site hero | Official-site hero image | ⚪ |
| **Share card** | Social share card | Open-graph card 1200×630 | ✅ |
| | Platform article share card | Long-form article share card | ⚪ |
| **Icon** | Mobile app icon | Touch icon 180×180 | ✅ |
| | Progressive web app icon | 192 / 512 | ✅ |
| **Character** | Virtual persona | Brand character's multi-pose multi-scene variants | ⚪ |
| **Thumbnail** | Video thumbnail | Video thumbnail template | ⚪ |

Website icons (16 / 32 / 48 / ICO) count inside the lettermark's transparent-background version, not a separate type.

⚪ Industry extensions—beyond the 17, append categories by brand business type, only when real assets exist:

| Brand type | Appended categories |
|---------|---------|
| Education and courses | Course material  -  chapter icons  -  certificate templates |
| E-commerce and physical goods | Product images  -  packaging images  -  scene images  -  size diagrams |
| Food and service | Dish images  -  store images  -  process diagrams |
| Software and tools | Interface screenshots  -  feature animations  -  comparison images |
| Personal brand | On-camera photos  -  event scenes |

✅ Every asset directory must have an index file stating the categories in use by this brand, each category's library status, and downstream citation rules.

### Background Variant Rules

Logo and character assets have three background variants, written in the file name's **variant segment**:

| Variant | Variant segment | Applicable scenario | Handling |
|------|--------|---------|---------|
| Dark background | `dark` | Dark-theme sites, videos, social cards | Original image (primary version for glow-type logos) |
| Transparent background | `transparent` | Website icons, app icons, overlay on light themes | Remove background or round-corner dark backing plate |
| White background | `white` | Light documents, business cards, email signatures | Regenerate a light version, not hard-cut the background |

✅ Types with background variants (lettermark, wordmark, brand icon, virtual persona) must produce a dark-background version. Transparent and white versions add as needed.

⚠️ A glow-type logo's white version can't just strip the background and lay it on white—the glow effect depends on the dark background. The white version should regenerate a graphic suited to light backgrounds, e.g., switch to solid gradients.

Avatar-type variant segments take style names (e.g., a certain illustration style name), not background colors.

### Multiple Design Lines Coexisting

One brand can have multiple design lines serving different types:

| Design line | Covered types | Coexistence |
|--------|---------|---------|
| Graphic-logo line | Lettermark, brand icon, icon types, share cards | Each type's file names don't overlap |
| Person-avatar line | Avatar types, virtual persona | Each type's file names don't overlap; avatars distinguished by variant segment style |

The two lines unify visually through brand colors and background colors.

---

## Naming Rules

✅ File name four segments, joined with `-`:

```
{category}-{object}-{variant}-{spec}.{extension}
```

| Segment | Required | Explanation | Value examples |
|---|:----:|------|---------|
| Category | ✅ | What purpose the asset serves | `icon`  -  `wordmark`  -  `avatar`  -  `banner`  -  `share-card`  -  `character`  -  `master`  -  `third-party` |
| Object | ✅ | Whose, for which platform | `brand`  -  `{product-name}`  -  `{platform-name}`  -  `{character-name}`  -  `universal` |
| Variant | ✅ | Background or style | `transparent`  -  `dark`  -  `white`  -  `{style-name}` |
| Spec | ✅ | Size or system identifier | `512`  -  `1200x630`  -  `vector`  -  `favicon` |
| Extension | ✅ | Priority: vector > lossless transparent > lossy | `.svg` > `.png` > `.jpg` / `.webp` |

The language of the four segments is decided by that brand's asset directory index; one brand doesn't mix languages. The values in use by this brand are also registered in that index. **Each segment itself must not carry `-`**, otherwise four segments inflate to five or six.

### Spec Segment Writing

| Case | Spec segment | Example |
|------|-------------|----|
| Square bitmap | Side length in pixels | `icon-brand-transparent-512.png` |
| Horizontal bitmap | `{width}x{height}` | `wordmark-brand-dark-906x177.png` |
| Vector source | `vector` | `icon-brand-transparent-vector.svg` |
| Files named by system identifiers | The identifier the system wants | `favicon`  -  `iOS180`  -  `PWA512` |

- ❌ No redundant `-512x512.png` dual-dimension writing for squares.
- ❌ No `@2x` scale suffixes—write actual pixels directly.

### Naming Taboos

- ❌ Date prefixes (`2026-04-banner.png`)—dates belong to version control records
- ❌ Not enough segments (`logo.png`  -  `icon-brand.png`)—four segments, none missing
- ❌ Mixed case (`Logo.PNG`)—extensions always lowercase; proper nouns inside segments keep as-is
- ❌ Spaces (`my logo.png`)—use `-`
- ❌ Unclear abbreviations (`bg-1.png`)—at least state category and object

| Good | Bad | Why |
|----|-----|------|
| `icon-brand-transparent-512.png` | `logo2.png` | "2" means nothing; each of four segments means something |
| `avatar-{platform}-{style-name}-400.png` | `thumb.png` | Whose, what style, what size—judge at a glance |
| `banner-{platform}-banner01-universal.png` | `banner_new.png` / `banner_final.png` | Clear sequence numbers, batch-citable |

---

## Size Matrix

✅ When the same asset distributes across multiple platforms and specs, the brand must declare **the platforms and specs it actually uses**, written into the asset directory's index file. No separate size-matrix file—one more file is one more place to go stale.

The matrix structure is fixed, specific rows filled by brand business type:

```markdown
| Platform or scenario | Type | Size (W×H) | Purpose |
|-----------|------|-------------|------|
| {platform} | {banner/cover/avatar/hero} | {W×H} | {description} |
```

❌ This methodology hard-codes no platform names or sizes—different brand types use completely different platforms.

⚪ Reference by brand type:

| Brand type | Common platform dimensions |
|---------|------------|
| Content creators and personal brands | Video-platform covers and banners, image-social covers, vertical short-video images, blog headers |
| E-commerce and physical goods | Product hero images, image details, mobile hero images, package spread diagrams |
| Software and tools | Official-site hero, social share cards, app-store screenshots, feature comparison images |
| Food and offline | Review-platform hero images, delivery covers, menu images, store photos |
| B2B | Official-site banners, whitepaper covers, presentation masters, event materials |

---

## Reuse and Citation Rules

- ✅ Any document cites assets by relative or absolute path, either works
- ✅ Same asset used across multiple channels **stored once only**, channel directories don't copy
- ✅ Citing logos always goes through the asset directory's current primary file, never draft versions
- ⚠️ Before modifying an asset, full-text search the file path to back-query citing parties, avoid broken links
- ❌ No copying files that already exist in the asset directory to other locations like business directories

**Drafts must archive**: design candidates, abandoned schemes, preview pages don't stay in the brand directory. The criterion is "will this file still be fetched now"; if not, archive it.

---

## Relationship with Other Directories

| Directory | Relationship |
|------|------|
| Reference material library | Reference materials are others' material (for benchmarking); visual assets are your own assets |
| Project material directory | Project-embedded temporary images, promoted to brand asset directory once finalized |
| Product catalog | Product definitions cite assets, but don't store them |
| Workflow directory | Workflows read asset paths, don't store assets |

---

## Checklist

**New visual asset**:
- [ ] File lands in the asset directory (physical) or rules directory (decision document)
- [ ] Included in the visual directory or asset directory's index

**New single file**:
- [ ] File name is complete four segments `category-object-variant-spec`, no segment carries `-`
- [ ] No date prefix, no spaces, lowercase extension
- [ ] Spec segment per spec writing: squares write single side length, no dual dimensions
- [ ] No new subdirectory created for it
- [ ] No same-name file duplicated in other directories

**Modify or delete file**:
- [ ] Back-queried reverse citations
- [ ] Modified the original file, not created `_new` / `_v2` copies

---

## Related Methodologies

| Topic | File |
|------|------|
| Four-segment naming general rules and identity layering | `kb-method-brand-identity.md` |
| Generic four-segment naming | `../../naming/` |

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted generic methodology from brand spec |
