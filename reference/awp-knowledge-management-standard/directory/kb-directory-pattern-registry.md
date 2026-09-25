---
document_id: awp-knowledge-management-standard/directory/kb-directory-pattern-registry
language: en
publication: public
title: "Directory Organization Pattern Registry"
purpose: Register all registered directory organization patterns in the knowledge base, and record which areas currently use which pattern
category: General Specification
audit:
  group: Directory System
  dimension: Directory Pattern Registration
  check: "Whether newly created directory areas select patterns from the registry; whether mapping table matches actual directory structure"
  metric: "Using unregistered pattern = warn; mapping table inconsistent with actual state = warn"
---

# Directory Organization Pattern Registry

> Scope: **What directory organization patterns are allowed in the knowledge base**, what each looks like, what scenario it applies to, and who is currently using it.
> Out of scope: How to choose among these patterns, whether they can be combined, which practices are forbidden (→ Directory Pattern Decision Tree and Composition Rules); also not file names (→ Naming Dimension).
> Before creating a new directory area, come here to select a pattern. If no match, follow the new pattern registration process at the end.

---

## Design Philosophy

| Principle | Explanation |
|------|------|
| **Pattern Registration System** | All directory organization methods must be registered in this document; new areas select from the registry, no inventing new patterns |
| **Purpose Determines Structure** | Directory structure serves retrieval and management purposes; same content in different purpose areas can use different structures |
| **Stackable** | One area can combine multiple patterns (e.g., "entity bucket + month bucket + date file"), stacking order is fixed |
| **Same Level Unified** | Only one pattern per level, no mixing |
| **Depth Restraint** | Registered patterns should stack to ≤4 layers; deep paths like `{workflows_root}.../references/`, `{business_root}.../product/`, standard reference libraries follow domain specifications, not mechanical 4 layers error |

---

## §1 Pattern Registry

### One. Time-Driven Type

#### T1 Month Bucket + Day Directory

```text
{YYYYMM}/{YYYYMMDD}/
```

**Use case**: Batch results by calendar day, with one independent directory per day containing all outputs for that day.
**Leaf naming**: Determined by domain specification (e.g. scheduling run reports use `{task_id}_{HHMMSS}_{short_title}`).
**Current users**: none. Timed leaves under the dashboard use T5 or T2.

#### T5 Month Bucket + Run Directory

```text
{YYYYMM}/{YYYYMMDDHHmmss}_{source}_{summary}/
```

**Use case**: Result of one run. Timestamp first, source is the workflow ID or a short token, flattened under the month.
**Leaf naming**: `{YYYYMMDDHHmmss}_{source}_{summary}`; same second + same source + same summary appends `-2`.
**Current users**: `{run_output_root}`.

#### T2 Month Bucket + Date-Prefixed Directory

```text
{YYYYMM}/{YYYYMMDD}-{description}/
```

**Use case**: Independently archived events or tasks by date, one directory per event, description distinguishes multiple same-day events.
**Description format**: semantic phrases connected with hyphens (e.g., `domain-object-purpose`), no segment limit but total length ≤30 characters.
**Current users**: `{dashboard_root}handoff/`, `{dashboard_root}research/`, `{inbox_root}archive/`, `{inbox_root}workstation-transit/{input,output}/`.

#### T3 Month Bucket + Date File

```text
{YYYYMM}/{YYYYMMDD}.md
```

**Use case**: One file per day for periodic output (daily reports, daily scan results). Multiple per day add sequence suffix `-01`, `-02`.
**Current users**: `{commerce_root}discovery/signal-listening/daily-scan/`, `{commerce_root}discovery/new-word-radar/daily-scan/`.

#### T4 Task ID Style

```text
T{YYYYMMDD}-{three-digit-seq}-{description}.md
```

**Use case**: Task files in scheduling system requiring globally unique IDs to track status.
**Current users**: none (scheduling moved to four-segment task directories on 2026-08-14; old ID-style files archived).

### Two. Entity Bucketing Type

#### E1 Brand × Dimension

```text
{brand}/{dimension}/
```

**Use case**: Multi-brand parallel operations, each brand branches by fixed dimensions. Dimension vocabulary defined by domain specification.
**Dimension vocabulary examples (brand four domains)**:

- Top level: `operations/`  -  `identity/`; (optional) `exploration/`
- Operations: `business-model/`  -  `audience/`  -  `competitors/`
- Identity: `strategy/`  -  `personality/`  -  `expression/`  -  `visual/`  -  `perception/`

**Business-side dimensions**: website, video channel, social accounts, products, code hosting platforms, etc. Product operations in `{business_root}.../product/`, not under brand.
**Current users**: `{brand_root}`, `{business_root}`.

#### E2 Person Dimension

```text
{dimension}/
```

**Use case**: Knowledge modeling centered on a person, organized by capability dimension. Use semantic words directly; files use four-segment names (see `naming/kb-naming-segment-convention.md`).
**Dimension vocabulary (current)**: `experience/`  -  `expertise/`  -  `vision/`  -  `decision/`  -  `collaboration/`.
**Current users**: `{owner_root}`.

#### E3 Functional Responsibility

```text
{responsibility_name}/
```

**Use case**: Areas divided by responsibility, content doesn't grow over time, structure is fixed. Pure semantic phrase naming.
**Current users**: `{dashboard_root}` top level, `{inbox_root}` top level, `{commerce_root}` top level, `{personal_root}` top level, `{tools_root}` top level.

### Three. Knowledge Organization Type

#### K1 Partition + Material Month Bucket

```text
{partition}/{name}/CLAUDE.md
{partition}/{name}/materials/{YYYYMM}/{YYYYMMDD}-{source_type_code}-{language_code}-{title_slug}/
```

**Use case**: Research material library. Two partition types—**topics** are general long-term directions, **subjects** are current focus, both structures identical. Partition root only stores `CLAUDE.md` and `materials/`; materials accumulate by month bucket; each material gets a four-segment project directory.
**Source type codes** (used in project directory names): `ar` (article), `bk` (book), `pp` (paper), `rp` (report), `gh` (code repository), etc.
**Language codes**: `en` (English), and other ISO 639-1 codes as needed.
**Project internal**: Must have unique raw (original) and std (standardized text), both four-segment file names; optional nav (navigation), card (interpretation), etc. whitelisted roles; interim products go in `process/`, role code `proc`. Role whitelist defined by `methodology/research/`.
❌ This pattern **has no knowledge layer**: Old layouts like `knowledge/`, `design/`, `progress/` are deprecated; simultaneously prohibited: type subdirectories, month-level `CLAUDE.md`, list sidebar md.
**Current users**: `{research_root}topic/`, `{research_root}subject/`.

#### K2 Index + View Hybrid

```text
master.json
topics/{topic}.json
indexes/{dimension}.json
views/{view_name}.md
```

**Use case**: Machine-facing JSON database + human-facing Markdown views coexist.
**Current users**: `{research_root}discovery/` (research library global machine index, parallel to K1's two partitions).

#### K3 Business Scanning Three-Piece Set

```text
{module_name}/
├── daily-scan/                    ← Time-point output (file naming see methodology/commerce/)
├── index.md                       ← Aggregation
└── to-judge.md | to-execute.md   ← Handoff to next station
```

**Use case**: Business direction scanning discovery/judgment modules, fixed structure as "daily-scan + index + to_{next_station}", not creating dimension subdirectories by project full name.
**Leaf naming**: Discovery daily-scan commonly `{YYYYMMDD}-{seq_or_summary}.md` or with time; deep analysis daily-scan `{YYYYMMDDHHmm}-{direction}.md` (field definitions see `methodology/commerce/`).
**Current users**: `{commerce_root}discovery/*/`, `{commerce_root}judgment/deep-analysis/`, `{commerce_root}judgment/decision/` (isomorphic three-piece set, handoff file names vary by stage).

### Four. Asset Naming Type

#### A1 Four-Segment Hyphen (brand-domain-action-facet)

```text
{brand}-{domain}-{action}-{facet}/
```

**Use case**: Workflow directories; four-segment naming serves as both directory name and workflow identity.
**Internal standard subdirectories**: `workflows/`, `library/`, `shared/`, `docs/` (defined by the Agent Workflow Authoring standard).
**Step subdirectory naming**: `{digit}{uppercase_letter}-{description}`, e.g., `1P-prepare-calibrate`, `4Q-static-qa`.
**Current users**: `{workflows_root}`.

#### A3 Best Practice Four-Segment (domain-tool-level-state)

```text
{domain}-{tool}-{level}-{state}/
```

**Use case**: `{tools_root}best-practice/` tutorial directory; four-segment controlled vocabulary see `methodology/tools/` (e.g., `agent-claudecode-app-live`).
**Exceptions**: `overview/` etc. entry short names can be zero hyphens.
**Current users**: `{tools_root}best-practice/`.

### Five. Product Development Type

#### P1 Product Development Lifecycle Node

```text
CLAUDE.md
01-research/
02-solution/
03-launch-deployment/
04-testing-retrospective/
05-attachments/
```

**Use case**: Long-term development product documentation directory.
**Rules source**: the lifecycle stages and the document naming and evidence chapters of the Product Development standard.
**Current users**: `{dashboard_root}projects/{product_name}/`.

---

## §4 Current Mapping Table

| Area | Pattern | Path Template |
|------|------|---------|
| `{run_output_root}` | T5 | `{YYYYMM}/{YYYYMMDDHHmmss}_{source}_{summary}/` |
| `{dashboard_root}scheduling/` task directories | Four-segment flat | `{type}-{domain}-{purpose}-{qualifier}/` (defined in the task file methodology) |
| `{dashboard_root}handoff/` | T2 | `{YYYYMM}/{YYYYMMDDHHmm}-{description}.md` |
| `{dashboard_root}research/` | T2 | `{YYYYMM}/{YYYYMMDD}-{type}-{description}-{state}/` |
| `{dashboard_root}projects/{product_name}/` | P1 | `CLAUDE.md` + `01-research/` + `02-solution/` + `03-launch-deployment/` + `04-testing-retrospective/` + `05-attachments/` |
| `{dashboard_root}` top level | E3 | `{responsibility_name}/` (scheduling, output, research, handoff...) |
| `{inbox_root}archive/` | T2 | `{YYYYMM}/{YYYYMMDD}-{type}-{object}-{operation}/` |
| `{inbox_root}workstation-transit/{input,output}/` | T2 | `{YYYYMM}/{YYYYMMDDHHmm}-{model}-{topic}-{nature}/` |
| `{inbox_root}` top level | E3 | `{responsibility_name}/` (screenshots, archive, workstation transit...) |
| `{brand_root}` | E1 | `{brand}/{dimension}/` |
| `{business_root}` | E1 | `{brand}/{platform_or_product}/` |
| `{owner_root}` | E2 | `{dimension}/{subdimension}/` |
| `{commerce_root}` top level | E3 | `{responsibility_name}/` (discovery, judgment, retrospective, methodology, market perspective) |
| `{commerce_root}discovery/*/` | K3 | `daily-scan/` + `index.md` + `to-judge.md` |
| `{commerce_root}discovery/*/daily-scan/` | T3 variant | `{YYYYMMDD}-{seq_or_summary}.md` (optional time) |
| `{commerce_root}judgment/deep-analysis/` | K3 | `daily-scan/` + `index.md` + `to-execute.md` |
| `{commerce_root}judgment/decision/` | K3 isomorphic | Three-piece set; ruling file naming see `methodology/commerce/` |
| `{research_root}topic/` | K1 | `{topic}/CLAUDE.md` + `{topic}/materials/{YYYYMM}/{project}/` |
| `{research_root}subject/` | K1 isomorphic | `{subject}/CLAUDE.md` + `{subject}/materials/{YYYYMM}/{project}/` |
| `{research_root}discovery/` | K2 | `master.json` + `topics/` + `indexes/` + `views/` |
| `{workflows_root}` | A1 | `{brand}-{domain}-{action}-{facet}/` |
| `{tools_root}best-practice/` | A3 | `{domain}-{tool}-{level}-{state}/` (controlled vocabulary see `methodology/tools/`; `overview/` etc. can be zero hyphens) |
| `{personal_root}` top level | E3 | `{responsibility_name}/` (health, investment, growth...) |
| `{specs_root}` | Strict four-segment package | `{prefix}-{domain}-{target}-standard/` |

---

## New Pattern Registration Process

When existing patterns cannot cover a new scenario:

1. Add new pattern entry at the end of §1 registry, write template, use case, and current users clearly.
2. Update Directory Pattern Decision Tree, add new pattern at appropriate branch node.
3. Update §4 mapping table, note the first user.
4. Check composition rules, confirm new pattern stacking relationships with existing patterns.
5. Check taboo table, add new forbidden combinations if any.

✅ Register first then use. ❌ Cannot use first then register later.

---

## Checklist

- [ ] Selected pattern from §1 registry (or registered new pattern following new pattern registration process)
- [ ] §4 mapping table consistent with actual directory structure
- [ ] No self-invented unregistered directory patterns in use
