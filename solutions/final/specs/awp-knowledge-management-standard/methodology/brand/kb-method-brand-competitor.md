---
document_id: awp-knowledge-management-standard/methodology/brand/kb-method-brand-competitor
language: en
publication: public
title: "Competitor Analysis Methodology"
---

# Competitor Analysis Methodology

> Managing how to build a competitor intelligence system: four-component model, eight dimensions, threat levels, time-series accumulation, and verification mechanism.
> Applicable to any business type (content creators / software services / e-commerce / education / offline services), shared skeleton for all brands.

---

## 1. Positioning

The competitor directory is a brand's **external perception layer**, answering "who are the concurrent competitors in the market, what did they do at each time point, and where is my differentiation."
The original is stored in `{brand_root}/{brand}/operations/competitors/`.

This methodology manages six types of outputs:

| Output | Answers | Location |
|--------|---------|----------|
| **Dimension Framework** | What dimensions to use? Where does data come from? | `dimension-framework.md` |
| **Single Competitor Profile** | What is this competitor like right now? | `competitors/{slug}/profile.md` |
| **Observation Logs and Synthesis Analysis** | What new discoveries were made at different time points? What cross-competitor insights? | `competitors/{slug}/observations/` and `synthesis-analysis/` |
| **Benchmarking** | Who are we competing with, who is worth learning from | `benchmarking/` |
| **Methodology** | What frameworks to use for analysis and creation | `methodologies/` |
| **Market** | What's the market size, what's the trend | `market/` |

Out of scope for this methodology:

| What's Not Managed | Goes Where |
|-------------------|------------|
| Product selection decisions, product copy optimization | Corresponding product location in business directory |
| Industry-wide market reports | Cross-brand research materials library |
| Own product definition | Corresponding product directory in business directory |
| Keyword libraries, search result scraping | Corresponding search optimization directory in business directory |

---

## 2. Design Philosophy

### 2.1 Shared dimensions across industries, zero business type branching

✅ All brands use the **same eight dimensions**.

Industry differences are not resolved by "picking different dimension sets," but by **what content you fill in**:

- Content creator brands write subscription tiers in "Pricing and Business Model"
- E-commerce brands write product prices and coupons in the same dimension

Consistent skeleton means lowest cost for cross-brand comparison, Agent routing, and future maintenance.

### 2.2 Time-series accumulation, never overwrite old observations

✅ Competitor analysis is **a growing notebook**, not a snapshot of one day.

- Main profile continuously updates current ground truth
- Observation logs preserve original increments from each discovery
- Synthesis analysis narrates by time point, old versions never deleted

❌ Do not "refresh main profile by directly overwriting old observations"—historical observations are raw material for pattern recognition.

### 2.3 Single competitor has own directory

✅ Each competitor gets its own slug directory, self-contained: profile, observations, materials.

❌ Do not put all competitors in one file. Once a single competitor accumulates sufficient depth (5+ observations plus screenshots plus raw scraped data), a single file becomes unmaintainable.

---

## 3. File Organization

### 3.1 Four-component model

Competitor intelligence serves one purpose: reduce uncertainty in strategic decisions. This requires four functional components, each corresponding to one or more fixed directory:

| Component | Answers | Directory | Nature |
|-----------|---------|-----------|--------|
| **① Coordinate System** | What dimensions to analyze competitors | `dimension-framework.md` | Fixed, one version |
| **② Profile** | What each competitor looks like now | `competitors/{slug}/` | Vertically accumulated |
| **③ Judgment** | What conclusions from cross-competitor comparison | `synthesis-analysis/` | Point-in-time narration |
| **④ Context** | Background knowledge supporting the above three | `benchmarking/`  -  `market/`  -  `methodologies/` | Three parts: who  -  field  -  method |

Context component splits into "who  -  field  -  method," each answering an irreplaceable question:

| Context Subdirectory | Shorthand | Answers | Contains |
|---------------------|-----------|---------|----------|
| `benchmarking/` | **who** | What players in the industry are worth watching | Benchmark account list, authority figures, glossaries, peer research |
| `market/` | **field** | What's the market size, what's the trend | Industry data, ecosystem data, pricing intelligence, technology trends, user voice |
| `methodologies/` | **method** | What methods to use for analysis and creation | Analysis frameworks, writing templates, methodologies |

### 3.2 Complete Skeleton (6 fixed directories)

✅ Competitor directory skeleton, universal for any brand:

```
{brand_root}/{brand}/operations/competitors/
├── CLAUDE.md                      # Overall index + triggers + business type + verification alarm
├── dimension-framework.md         # ① Coordinate system: eight dimensions instantiated for this brand
│
├── competitors/                   # ② Profile: look at one by one (vertically)
│   └── {slug}/
│       ├── profile.md            #    Eight dimensions ground truth
│       ├── observations/         #    Incremental observation logs
│       │   └── {YYYYMMDD}.md
│       └── materials/            #    Screenshots / scrapes / reports
│
├── synthesis-analysis/            # ③ Judgment: cross-competitor point-in-time narration
│   └── {YYYYMMDD}.md
│
├── benchmarking/                  # ④-who: what players in the industry
│   └── CLAUDE.md
│
├── market/                        # ④-field: market size and trends
│   └── CLAUDE.md
│
└── methodologies/                 # ④-method: analysis and creation frameworks
    └── CLAUDE.md
```

- ✅ When initializing a new brand, build all 6 directories with index files in each.
- ✅ Keep the three context directories flat (one level), no further nesting.
- ✅ Context directory indexes must explain: what question answered + file index + update cadence.
- ⚪ If a brand truly has no competitors to track, mark as "not yet activated" in the index with reason.
- ❌ Do not create new top-level subdirectories beyond these 6—all context goes into one of "who  -  field  -  method."

---

## 4. Universal Eight Dimensions

All brands share these; written at the top of each `dimension-framework.md`. ✅ Dimension names, order, and numbering are fixed, brands cannot customize.

| # | Dimension | Answers | What content creators fill | What e-commerce fills |
|---|-----------|---------|---------------------------|----------------------|
| 1 | **Identity and Positioning** | Who is this competitor? What's the unique selling point? | Brand name  -  persona  -  tagline | Seller name  -  brand story  -  registered entity |
| 2 | **Products and Services** | What's being sold? What format? | Content types  -  sections  -  subscription products | Products  -  specs  -  materials |
| 3 | **Pricing and Business Model** | How to monetize? Price tiers? | Subscription tiers  -  conversion path  -  free lead magnets | Product prices  -  coupons  -  bundle deals |
| 4 | **Channels and Distribution** | Where are they found? | Search  -  email newsletter  -  video platforms | E-commerce platforms  -  direct sites  -  offline  -  livestream |
| 5 | **Traffic and Influence** | How big is reach and impact? | Search rankings  -  subscribers  -  followers  -  monthly visits | Category rankings  -  review count  -  monthly sales  -  GMV |
| 6 | **Content and Assets** | What produced and accumulated? | Published articles / videos / emails | Product page quality  -  image details  -  brand flagship pages |
| 7 | **Users and Audiences** | Who are they serving? | Reader persona  -  comment section tone | Buyer persona  -  negative review signals |
| 8 | **Our Differentiation** | How we differentiate, how we compete head-on? | Content angle / audience segment / tool combination difference | Materials / tone / customer service / logistics |

- ✅ All eight required. When information is insufficient, write "pending" with planned collection date; cannot leave blank.
- ⚪ Inside `dimension-framework.md` can **add** brand-specific secondary granules (e.g., software services add "API completeness," education add "repeat purchase rate"), but **cannot delete or reorder the eight main dimensions**.

---

## 5. Single Competitor Profile Structure

`competitors/{slug}/profile.md` must have these sections:

### 5.1 Metadata

```yaml
slug: <competitor-slug>
name: <competitor display name>
official_domain: <URL>
threat_level: S | A | B | C | D       # see § 5.3
current_status: active | monitoring | misaligned-ignore | exited | acquired
first_profiled: YYYYMMDD
last_updated: YYYYMMDD
next_review: YYYYMMDD                # default = last_updated + 90 days
```

### 5.2 Eight Dimensions (one section each)

✅ Follow the order in § 4, each as a level-two heading (`## 1. Identity and Positioning` ... `## 8. Our Differentiation`).

Each section contains three things:

- Current ground truth (factual statement)
- Data source (URL / scrape date / tool)
- Key changes since last update (recommended)

### 5.3 Threat Level Dictionary

```
S Misaligned     —— Completely non-competing (different scale / industry / model)
A Differentiated —— Same track but different strategy, frontal conflict costly
B Frontal        —— Direct competitor, same track same approach, must position
C Monitoring     —— Small scale now but potential threat, quarterly review
D Learning       —— No current competition but learnable approach
```

- ✅ Write in the metadata "Threat Level" field, **no separate summary file**.
- ✅ Dictionary consistent across brands, brands cannot customize letter meanings.

### 5.4 Our Differentiation

✅ Section 8 "Our Differentiation" must give at least **one executable differentiation judgment**, such as concrete process handling or specific automation pipeline.

❌ Forbid vague assertions like "better quality control" or "better content" without anchors.

⚪ If judgment is immature, write "differentiation undefined → pending {signal} for backfill" with backfill conditions; cannot leave empty.

---

## 6. Observation Logs (Time-Series Accumulation)

### 6.1 Trigger Conditions

✅ Create `competitors/{slug}/observations/{YYYYMMDD}.md` when any of these happen:

- Competitor launches new product, section, subscription tier
- Pricing or business model adjustment
- Traffic data significantly changes (search rank jump, subscribers double, category rank swings)
- Major company action (funding, acquisition, personnel change, crisis event)
- Our strategy needs adjustment due to their moves

### 6.2 File Naming

```
{YYYYMMDD}.md                    # default
{YYYYMMDD}-{event_suffix}.md     # multiple observations same day
```

### 6.3 Section Skeleton

```markdown
# {Competitor} Observation  -  YYYYMMDD

## Trigger
<what event prompted this observation>

## Facts
<traceable fact statement + URL / screenshot / scrape date>

## Dimension Impact
<which of the eight dimensions affected  -  direction of impact>

## Todos
<need to update main profile? rerun synthesis analysis? adjust our strategy?>
```

### 6.4 Backflow to Main Profile

✅ When observations accumulate enough to "change a dimension's ground truth," backflow to main profile:

- Update corresponding dimension in main profile with new ground truth
- Update metadata "last_updated" to today
- Update "next_review" to today + 90 days
- ❌ Keep the merged observation logs **undeletd**, as timeline evidence

---

## 7. Synthesis Analysis (Point-in-Time Narration)

### 7.1 Trigger Conditions

✅ Create `synthesis-analysis/{YYYYMMDD}.md` when any of these happen:

- Quarterly review (90 days)
- Our strategy shift (positioning / business model / channel structure change)
- Multiple competitors signal coordination, e.g., three simultaneously cut prices or enter a vertical

### 7.2 Section Skeleton

```markdown
# {Brand} Competitor Synthesis  -  YYYYMMDD

## Trigger
## Cross-Competitor Posture (cut horizontally by the eight dimensions)
## Threat Map (S/A/B/C/D distribution + changes)
## Our Differentiation Recalibration
## Action Recommendations (90 days)
## Next Synthesis Review: YYYYMMDD
```

### 7.3 Archiving Rules

- ✅ Old synthesis analyses **never deleted**—stacking them is a timeline of brand competitive understanding evolution.
- ❌ Do not merge historical synthesis analyses into one final version—each version is a fossil of judgment at that time point.

✅ **Write "what changed from last version" as this version's conclusion, not backstory.** Position swaps, benchmark competitors becoming obsolete, old profiles deprecated—these must be explained; delete them and readers cannot tell why this round rescanned. Point-in-time snapshots with date stamps are exempt from "only state current" rule.

---

## 8. Verification Mechanism

| Level | Review Cycle | Trigger |
|-------|--------------|---------|
| Single competitor profile | 90 days | Profile metadata "next_review" expires |
| Synthesis analysis | 90 days | Last version's "next synthesis review" expires |
| Dimension framework itself | Strategy upgrade | Brand positioning, business model, or channel structure changes |
| Index top-level "last_review_date" | Any level updates | — |

⚠️ Profile "next_review" overdue >30 days must be flagged in index; >90 days marks profile as unreliable, must re-scrape before citing.

---

## 9. Naming Contract

### 9.1 Slug rules

✅ Competitor slugs meet three conditions:

- All lowercase English plus digits plus hyphens
- Prefer competitor's official brand name in English lowercase
- Max 32 characters

Examples: `context7`  -  `cursor-com`

❌ Not allowed: non-ASCII slugs, spaces, underscores, version number tails.

### 9.2 Directory and File Naming

```
competitors/{slug}/profile.md
competitors/{slug}/observations/{YYYYMMDD}.md
competitors/{slug}/observations/{YYYYMMDD}-{event_suffix}.md
competitors/{slug}/materials/{any_name}.{ext}
synthesis-analysis/{YYYYMMDD}.md
synthesis-analysis/{YYYYMMDD}-{topic}.md
```

✅ Fixed entry names: index file  -  `dimension-framework.md`  -  `profile.md`, cannot rename.

---

## 10. Data Authenticity

- ✅ All numbers must be traceable to concrete source (URL / scrape date / tool)
- ✅ Screenshots and scrapes marked with date, e.g. "scraped 2026-03-31"
- ✅ Data >90 days without update must be marked as possibly outdated
- ❌ Forbid "approximately" "heard" "should be" language without sources
- ❌ Forbid fabricating negative review keywords or user comments—must come from real scraping
- ❌ Forbid unsourced hype about competitors or unsourced disparagement

---

## 11. Checklist

**New or modified `dimension-framework.md`**:
- [ ] Eight dimensions per § 4 fully listed, order fixed
- [ ] Current brand type instantiated each dimension with explanation
- [ ] Industry-specific secondary granules (if any) are additions, not deletions from main dimensions
- [ ] Metadata and change log complete

**New or modified single competitor `profile.md`**:
- [ ] Metadata all fields complete (slug / threat level / last update / next review)
- [ ] All eight dimensions answered; insufficient info marked as "pending" with date
- [ ] "Our Differentiation" gives executable judgment
- [ ] All data has URL, scrape date, or tool
- [ ] Data >90 days marked with note

**New observation log**:
- [ ] Four sections complete (trigger / facts / dimension impact / todos)
- [ ] Facts are traceable
- [ ] "Dimension Impact" explicitly refers to which of the eight dimensions

**New synthesis analysis**:
- [ ] Six sections complete (trigger / cross-competitor / threat map / recalibration / recommendations / next review)
- [ ] Old analyses not merged or deleted
- [ ] Recommendations have 90-day window

**Directory health check (quarterly)**:
- [ ] Index top "last_review_date" matches profile layer
- [ ] Overdue >30 days already flagged in index
- [ ] Competitor exited/acquired, "current_status" updated, profile not archived (kept as timeline evidence)

---

## Related Methodologies

| Topic | File |
|-------|------|
| What types of materials go in context directories | `kb-method-brand-reference.md` |
| Identity layering and cascade impacts | `kb-method-brand-identity.md` |
| Audience persona | `kb-method-brand-audience.md` |

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|--------|
| 2026-08-07 | Extracted from brand standards into reusable methodology |
