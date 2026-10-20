---
document_id: awp-knowledge-management-standard/methodology/brand/kb-method-brand-identity
language: en
publication: public
title: "Brand Identity Modeling Methodology"
---

# Brand Identity Modeling Methodology

> Managing how to layer brand identity, what each layer answers, how to name files, how to preserve decisions, and what to cross-check when changing one layer.
> Applicable to any industry and any brand. This methodology only defines "what questions should be answered," not "what the answers are."

---

## Path Placeholders

This methodology uses placeholders to indicate locations; substitute your own directory names when deploying.

| Placeholder | Means |
|-------------|-------|
| `{brand_root}/` | Root directory storing all brand materials |
| `{brand}` | Single brand's directory name |
| `{owner_root}/` | Directory storing the owner's personal facts |
| `{business_root}/` | Directory storing product deployment, channel operations, scheduling data |
| `{project_root}/` | Directory storing R&D project tracking docs |
| `{archive_root}/` | Directory storing archived files |
| `{workflows_root}/` | Directory storing content production workflows |

"Owner" means the person running these brands. One person can run multiple brands; owner layer is one copy shared by all; each brand has its own brand layer.

---

## What This Manages vs. What It Doesn't

| This Methodology Defines | This Methodology Doesn't Define |
|-------------------------|-------------------------------|
| Each file type's structural skeleton: section order, required fields, deduplication boundaries | Specific content: what values are, what red lines say, what products are called |
| Loading priority and cascade rules | Chapter-internal prose wording |
| How to stack industry-optional sections | Specific field values |
| Cross-file reference format and relationships | Standard answer for one dimension |

One phrase: "What questions must be answered," not "what the answers are."

---

## Design Philosophy

- **One dimension per file**: One fact exists in one place. Duplication is both maintenance burden and wastes Agent context budget.
- **Layered loading priority**: Not all files read every time. L0 guaranteed minimum knowledge; L1 and L2 control context cost.
- **Identity and expression separate**: Identity says "who I am," expression and platform samples say "how to write this time." Different sample set doesn't change person; different platform doesn't change voice.
- **Red lines non-negotiable**: Brand red lines are hard boundaries, not negotiable. Factual errors, position overreach, overpromising—all forbidden.
- **Framework universal, content private**: Answers differ by industry and brand naturally; methodology only prescribes what questions to answer.
- **Product files outside brand directory**: Pricing, transactions, ops data go in `{business_root}`; R&D goes in `{project_root}`; code goes in code repo. Brand directory keeps only strategy, operations, identity, and content.
- **Present state only**: Abandoned approaches don't linger as side comments; long backstories move to `{archive_root}`. Only current facts in main text.

---

## Knowledge Layering

| Layer | Answers | Location | Who Maintains |
|-------|---------|----------|---------------|
| **Owner Layer** | Person is who, thinks what, judges how | `{owner_root}/` | One master, all brands read |
| **Brand  -  Strategy Domain** | Brand is who? Goes where? Boundary where? Thinks how internally? | `{brand}/strategy/` | Each brand independent |
| **Brand  -  Operations Domain** | Fixed business: how to monetize, sell to whom, who's the competition | `{brand}/operations/` | Each brand independent |
| **Brand  -  Identity Domain** | Recognized how, speaks how, looks how | `{brand}/identity/` | Each brand independent |
| **Brand  -  Content Domain** | Says what, organizes how, what's the craftsmanship | `{brand}/content/` | Each brand independent |

Three boundaries:

1. **Owner layer doesn't copy into brand**. Brands read owner layer, don't duplicate their person's experience, skills, vision into brand directory.
2. **Character persona belongs only to independent character brands**. Cannot copy owner into brand persona; see `kb-method-brand-persona.md` details.
3. **Operations independent from strategy**. Strategy says "why and boundary," operations say "numbers and path"—change pricing once doesn't change positioning essay.

---

## Dimension Overview and Loading Priority

| Category | Content | Location | Answers | Loading Level |
|----------|---------|----------|---------|------|
| Strategy | Positioning  -  Red lines  -  Direction  -  Architecture | `{brand}/strategy/` | Who is this brand? Where going? | L0 required (positioning + red lines) |
| Strategy | Internal understanding | `{brand}/strategy/` cognition files | What is this brand for the owner? | L1 as needed |
| Operations | Business model  -  SKU  -  Pricing  -  Path narrative | `{brand}/operations/business-model/` | How to monetize? Product system? | L2 low frequency |
| Operations | Audiences | `{brand}/operations/audiences/` | Sell to whom? | L1 as needed |
| Operations | Competitors | `{brand}/operations/competitors/` | Who's the competition? | L1 as needed |
| Identity | Expression  -  Taglines  -  Medium slices | `{brand}/identity/expression/` | How does this brand speak? | L0 required |
| Identity | Author public fields | `{brand}/identity/author/` | Who signs? What attribution fields do channels need? | Only when signing or brief needed |
| Identity | Independent character persona | `{brand}/identity/persona/` | How does a character brand think and respond? | Only for character type, explicitly declared |
| Identity | Visual rules and assets | `{brand}/identity/visual/` | Look how? | L1 as needed |
| Content | Main line  -  framework  -  channel setup  -  craftsmanship | `{brand}/content/` | Says what? Organizes how? | L1 as needed |
| Owner | Expertise  -  Experience  -  Vision  -  Judgment  -  Values | `{owner_root}/` | What's the person skilled at, done, heading toward, believe in? | L2 low frequency |

Three-level loading rules:

| Level | Read | When |
|-------|------|------|
| **L0 Required** | Target brand's positioning, audiences, content setup, expression and platform hard limits | Regular content work |
| **L1 As Needed** | Brand visual, operations, author public fields or character data | Visual work, pricing, signing, character tasks |
| **L2 Low Frequency** | Owner's vision, judgment, experience, expertise | Comprehensive planning, cross-brand trade-off, review, fact verification |

### Workflows Load by Brand Contract

Workflows only describe target brand's operating contract. Can reference or internalize brand positioning, audiences, content setup, expression, platform differences; **does not ingest owner layer**.

- Person's experience, expertise, vision, judgment, bias must not be soft-linked, copied, or implicitly injected into regular workflows.
- Brand original stays at `{brand_root}/{brand}/`. When workflows internalize platform variants, must clarify boundary from original.
- Owner identification only appears in signature, reviewer, or operator fields, not as workflow's target brand.
- Author public fields only read when output format requires signature, brief, or about section. Signing itself doesn't authorize first-person writing.
- Character brand only reads persona file when workflow explicitly declares character; regular workflows don't load character.

---

## Brand Type Layering

Each brand declares type at creation for choosing whether to enable industry-optional sections. Types can stack.

| Type | Definition | Typical Optional Extensions |
|------|-----------|--------------------------|
| **Personal Brand** | Public identity is the person | Expertise boundary, person facts, video explanation style |
| **Enterprise or Media Brand** | Run by organization, media, or methodology name | Category definition, visual identity, brand story, brand relationships |
| **Product Brand** | Core on single product, emphasizes selling point and scenario | Core selling point, scenario matrix, competitor benchmarking, packaging specs |
| **Service Brand** | Core on service process | Service process, SLA promises, touchpoint map, customer journey |
| **Sub-Brand** | Branch of parent brand | Parent relationship, brand boundary, shared asset list |

- ✅ One brand can be multiple types simultaneously, e.g. "personal brand + product brand." Enable corresponding type extensions.
- ❌ Cannot use industry-optional sections without declaring type.

When enterprise brand scales to multi-brand or organization stage, can add:

- Category definition—what category? key terms?
- Visual identity—colors, fonts, logo usage rules
- Brand story—origin, turning point, highlight moment
- Org structure—team composition, division, decision mechanism
- Brand relationships—parent, sub, partnership hierarchy

Create only if real asset exists; no stub files.

---

## Three-Layer Optional Skeleton

Identity, audiences, visual, competitors files default to three-layer sections:

| Layer | Means | Missing Consequence |
|-------|-------|------------------|
| ① Required Sections | All industries, all types must fill | File deemed incomplete |
| ② Recommended Sections | Fits most brands | Missing needs reason statement |
| ③ Industry-Optional Sections | Stack by brand type | Skip if not enabled |

Each spec must explicitly declare three-layer boundary. Undeclared defaults to all required.

Industry-optional section stacking rules:

| Principle | Explanation |
|-----------|------------|
| Add not replace | Only append to end of existing sections, cannot replace required |
| No duplicate skeleton | Cannot repeat required or recommended section content |
| Enable by type | Select per "Brand Type Layering" above |

---

## Medium Slices

Medium slice is expression style's deployment in specific medium, not independent persona dimension. Files live in `{brand}/identity/expression/`, by four-segment naming, extending by brand output form:

- Long video and screen recording
- Livestream and conversation
- Pure audio podcast
- Vertical short video

Each medium slice uses the same skeleton, only swaps medium-specific part.

---

## File Naming: Four-Segment, All Flat

Brand directory stays flat; filenames do classification, not directory structure.

> Universal four-segment naming rules see `../../naming/`. This section only prescribes brand zone value dictionaries and hard requirements.

### Documents: `{type}-{dimension}-{topic}-{scope}.md`

| Segment | Fill | Values |
|---------|------|--------|
| **Type** | This file's nature | `blueprint` (decisions & design)  -  `constraint` (red lines & forbids)  -  `data` (facts & materials)  -  `guide` (how to execute)  -  `cognition` (internal judgment) |
| **Dimension** | Which brand dimension | `positioning`  -  `business`  -  `direction`  -  `persona`  -  `expression`  -  `tagline`  -  `naming`  -  `content`  -  `channel`  -  `visual`  -  `brand` |
| **Topic** | Specifically what | E.g., `brand-red-lines`  -  `character-traits`  -  `language-features` |
| **Scope** | Applies to whom | `universal` (brand-level)  -  `{channel_name}`  -  `{product_name}`  -  `{character_name}` |

Examples (placeholders mean specific names):

```
strategy/blueprint-positioning-{positioning-claim}-universal.md
strategy/constraint-boundary-brand-red-lines-universal.md
strategy/data-direction-next-steps-universal.md
author/data-author-public-fields-{author_name}.md
persona/data-persona-core-setting-{character_name}.md
expression/constraint-expression-language-features-universal.md
visual/rules/blueprint-visual-color-universal.md
```

### Image Assets: `{category}-{object}-{variant}-{spec}.{extension}`

Images also stay flat; same self-sorting when sorted—file naming does what directories used to do.

| Segment | Values |
|---------|--------|
| **Category** | `icon`  -  `wordmark`  -  `logotype`  -  `avatar`  -  `banner`  -  `share-card`  -  `character`  -  `master` |
| **Object** | `brand`  -  `{site_name}`  -  `{platform_name}`  -  `{character_name}`  -  `universal` |
| **Variant** | `transparent`  -  `dark`  -  `white`  -  `{style_name}`  -  `{color_name}` |
| **Spec** | Pixel count (`512`)  -  dimensions (`1200x630`)  -  `vector`  -  system ID (`favicon`  -  `iOS180`  -  `PWA512`) |

Details see `kb-method-brand-visual.md`.

### Four Hard Requirements

1. **No hyphens in segments.** Hyphen is segment separator; hyphen inside segment makes four become five or six. English IDs with hyphens use underscore or concatenate: `plain-english` write `plain_english`, hyphenated brand names concatenate no-space.
2. **No "current" type words.** After old version archives, remaining files in brand directory are all current version anyway; marking is information-empty and waste segment. Scope segment must hold real info.
3. **No subdirectories**; documents and images both. Only exception: visual directory's `rules/` and `assets/` split.
4. **Filename self-explanatory**—without path you know which brand, which dimension, what type. If not, naming picked wrong.

### Version Replacement Five Steps

1. Archive old file to `{archive_root}/{YYYYMM}/{YYYYMMDD}-brand-{brand}-old-version-archive/{dimension}/`
2. Write new file in dimension directory with four-segment naming
3. Update dimension index: add evolution table row, mark old version archived with archive path
4. **Evolution main line must stay**—why switch from last version beats last version itself
5. Check soft links before moving

> ⚠️ **Soft links are this structure's weakest point.** If workflow uses symlink to read brand original, path change breaks silently—link remains, target gone, reads empty.
>
> Before moving: list all symlinks pointing to this brand. After: verify target file exists.

### Batch Renaming Pitfall

Script batch rename: **substring match will hit unintended files**. Real case: "is this a share card?" written as "filename contains og" matched `logo-1024.png` too—`logo` has letters `og`. Fix to "filename starts with og."

Before batch rename: **three mandatory steps: generate complete mapping table → check duplicates → sample human verify**, then execute.

### Process Drafts Must Archive

Design candidates, abandoned approaches, preview pages stay out of brand directory. **One test: "will this file be used now?"** No means archive.

Example: brand's logo design process drafts filled half the visual directory but none were usable—move all to archive directory.

---

## Decision Trail: Keeping "Why We Changed"

### Why Keep It

Brand decisions upgrade repeatedly. Keep only current conclusion, three months later nobody remembers **why the last version shifted**; same mistake gets walked again.

Example: brand positioning changed four times. The most valuable isn't any version—it's "why version N didn't work"—when written into internal cognition file, beats all four old versions combined.

### Lives in Three Places

| What | Where | Form |
|-----|-------|------|
| **Current Conclusion** | `{dimension}/{four-segment-file}.md` | Brand directory keeps one copy |
| **Version Evolution Table** | `{dimension}/` index file | Per version: effective date  -  code  -  status  -  one-line  -  archive path |
| **Old Full Text** | `{archive_root}/{YYYYMM}/{YYYYMMDD}-brand-{brand}-old-version-archive/` | Entire directory moves with explanation of why obsolete |

### Dimension Index Must Have Four Parts

1. **File Table**—what files in this dimension, what each answers
2. **Current Quick Look**—one glance at current conclusion, no need to click into blueprint file
3. **Version Evolution Table**—complete history, old marked archived with path
4. **Agent Behavior Directive**—this dimension's hard constraint, e.g., "ship must pass red lines," "forbid inventing background"

### Decision Basis Traceable

Blueprint file must have "decision basis" section, citing the **research report's file name and chapter**:

```markdown
> Basis: `{research_report_filename}` § {chapter_name}
```

**Cite theory together with its limits**—frameworks in brand directory are reference not absolute law; final call with owner. 

### File Two Natures: Decision vs. State

Files in identity layers split two natures. Structure same (all flat), distinction in change discipline.

| Nature | Test | When Changed | Examples |
|--------|------|--------------|----------|
| **Decision** | Has "why define this way" trail, upgrades need history | Archive old version + add evolution table row | Positioning  -  Business  -  Persona  -  Expression  -  Tagline  -  Naming  -  Content  -  Channel  -  Visual rules |
| **State** | Records "what is now," rewrites anytime | Direct change, no old version | Current direction  -  Four internal cognition files |

### Internal Cognition Layer (all brands required)

Internal cognition holds **what this brand means to owner**, not external talking points. Boundary:

| Write What | Answers What | For Whom |
|-----------|-------------|---------|
| Positioning blueprint and red lines | What brand **externally is** | Readers and executors |
| Current direction | What brand **now does** | Executors (including Agent) |
| **Internal Cognition** | What brand **means to owner** | Owner self |

One-phrase split: direction says "do what," cognition says "why do, worth it, when stop."

Four fixed files:

| File | Answers |
|------|---------|
| Essence | What is this brand fundamentally  -  why exist  -  what it's not |
| Position | In whole portfolio where, relationships with others, resource split |
| Input-Output | Real input  -  real output  -  what counts  -  **exit criteria** |
| Assumptions | Betting what  -  most uncertain  -  **record of wrong bets** |

Three Writing Disciplines:

1. **No external pitch**—this is self-judgment, not reader-facing copy
2. **Numbers are real**—only 11 subscribers write 11, not "early growth stage"
3. **Dare say bad news**—write no bad news means not really thinking

> "Record of wrong bets" is this layer's most valuable: **marking where judgment missed beats changing it.** Most expensive lesson.

---

## Style Priority

Three-layer style from specific to universal:

```
Platform style > Medium slice > Global expression style
```

| Layer | Defines | Master Location |
|-------|---------|-----------------|
| Global expression style | Brand's baseline text voice: self-reference, connectors, sentence shape, quantification, emotion intensity, interaction method | `{brand}/identity/expression/` |
| Medium slice | Spoken and visual storytelling traits for this medium | `{brand}/identity/expression/` |
| Platform style | Channel-specific text differences | Corresponding workflow's methods directory, not brand directory |

Conflict: more specific layer wins; higher layer as fallback.

---

## Cascade Impact

Change upstream, assess downstream. Dependencies:

```
Strategy (positioning  -  red lines  -  business  -  direction)
  ├── Affects → Workflow writing method and samples (tone)
  ├── Affects → Audiences (target people)
  ├── Affects → Products (product line)
  ├── Affects → Reference materials (benchmark objects)
  └── Affects → Competitors (differentiation)

Expression
  ├── Affects → Medium slices (video / livestream / podcast)
  └── Affects → Workflow writing method and samples

Author fields → Signature, brief, platform account
Independent persona → Only that character brand's response method
Visual → All references (full-text search to back-query)
Internal cognition → Input-output and exit-related decisions
Audiences → Content depth and word choice
Competitor differentiation → Product definition's "differentiation" field
```

### Modification Checklist

| Changed | Must Recheck |
|---------|------------|
| Strategy (positioning  -  red lines  -  direction  -  business) | Writing methods and samples, audiences, products, competitor differentiation |
| Expression | Medium slices, air of narrative |
| Author fields | Signature, brief, platform account fields |
| Persona | Only character brand's character data and workflow declaration |
| Visual | All reference points (full-text search file path) |
| Internal cognition | Input-output and exit-related decisions |
| Audiences | Corresponding product definition |
| Competitor profile | Product definition's differentiation field |

---

## Checklist

**Identity and brand-layer files**:
- [ ] Strategy has positioning blueprint + brand red lines + current direction
- [ ] Expression has defined language traits, covers self-reference, common words, sentence shape, emotion at least four types
- [ ] Brands needing signature keep author field only with public attribution, not owner's writing style
- [ ] Persona only for explicit independent character brands, declared by workflow
- [ ] Medium slices live in expression directory with complete skeleton
- [ ] Files at same layer have no contradictions

**Writing methods and samples**:
- [ ] Samples in corresponding creation or publishing workflow, not brand directory
- [ ] Samples indexed; master protocol in writing method, brand directory makes no extra style directory

**Naming and archiving**:
- [ ] Filename complete four segments, no segment has internal hyphen
- [ ] Scope segment has no "current" type empty-info words
- [ ] Except visual's rules/assets split, no new subdirectories made
- [ ] Old version archived, dimension index evolution table added
- [ ] Symlinks verified before and after moving

**Boundaries**:
- [ ] Brand directory has no product operations files
- [ ] Product definition, pricing, promotion, channel data all in `{business_root}`
- [ ] Owner layer not copied into brand directory

---

## Related Methodologies

| Topic | File |
|-------|------|
| Audience persona | `kb-method-brand-audience.md` |
| Competitor analysis | `kb-method-brand-competitor.md` |
| Visual assets | `kb-method-brand-visual.md` |
| Reference materials | `kb-method-brand-reference.md` |
| Business model | `kb-method-brand-businessmodel.md` |
| AI persona modeling | `kb-method-brand-persona.md` |
| Universal four-segment naming | `../../naming/` |
| Directory structure | `../../directory/` |

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|--------|
| 2026-08-07 | Extracted from brand standards into reusable methodology |
