---
document_id: awp-knowledge-management-standard/naming/kb-naming-segment-convention
language: en
publication: public
title: "File Naming Segment Specification"
purpose: Unified management across entire knowledge base of file and directory naming patterns by hyphen count
category: General Specification
audit:
  group: Documentation and Language
  dimension: Naming Compliance
  check: "Filename hyphen count matches registered pattern; spec package ID exactly four segments; date segment uses compact format"
  metric: "Unmatched registered pattern = warn; package ID not four segments = error; date contains YYYY-MM-DD = warn"
---

# File Naming Segment Specification

> What it governs: the naming patterns of every filename and directory name in the knowledge base. Layered by hyphen count—each of zero to three hyphens has one formula, and each implementer registers its own field definitions within the formula.
> This spec is the only place in the entire vault that defines naming patterns. Other specs and `CLAUDE.md` files reference this spec; they do not define patterns themselves.
> The **structural formula** of a name is defined here; what each segment **contains** is defined by the domain methodology spec (see `../methodology/`).

---

## Design Philosophy

| Principle | Explanation |
|-----------|------------|
| **Layered by Hyphen Count** | Hyphen count = semantic segment count − 1: zero hyphens one segment, one hyphen two segments, two hyphens three segments, three hyphens four segments |
| **Fixed Formula, Dynamic Fields** | The structure of each pattern (how many segments, what delimiter) stays fixed, but each implementer defines what each field contains |
| **Dates Do Not Use Hyphens** | Date segments always use the compact format (`YYYYMMDD` / `YYYYMM`), never `YYYY-MM-DD`, so the hyphen count never falls out of sync with the semantic segment count |
| **Registration System** | Which pattern each directory uses, and what each field contains, is registered centrally in the §6 registry |
| **Fixed Entries Untouched** | System filenames such as `CLAUDE.md`, `README.md`, and `manifest.json` are not bound by this spec |

---

## §1 Global Constraints

> This English distribution renders source-language filename examples as English semantic equivalents. The delimiter count, segment role, and naming decision remain the same as in the source authority.

### Delimiter System

The knowledge base uses two delimiters, each with a clear responsibility:

| Symbol | Name | Responsibility | Example |
|--------|------|----------------|---------|
| `-` | Hyphen | **Between segments**—between semantic segments at the same level | `report-book-review-overview-20260428` |
| `_` | Underscore | **Between layers**—when identifiers from different levels are joined | `awp-workflow-website-article_143022_ai-programming-introduction` (example) |

**Why two delimiters are needed**: when a filename must nest an identifier that itself contains hyphens, using hyphens between layers too makes the segment boundaries impossible to detect. The underscore separates identifiers from different levels, while the hyphen keeps its between-segments function inside each identifier.

**Where it applies**: the between-layers underscore is used only when nesting identifiers. Today only the workflow output directory uses this pattern across the entire vault—the workflow name is itself a three-hyphen, four-segment identifier, joined with the run time and topic by underscores:

```
{workflow_name}_{HHMMSS}_{topic_summary}
awp-workflow-website-article_143022_ai-programming-introduction
└── hyphens between segments ──┘ └─ underscore between layers ─┘
```

### Delimiter Constraints

| Rule | Explanation |
|------|-------------|
| ✅ Between-segment delimiter | Half-width hyphen `-` |
| ✅ Between-layers delimiter | Half-width underscore `_` (only for nested-identifier cases) |
| ❌ No hyphens inside a segment | A `-` must not appear inside one semantic segment (otherwise the pattern cannot be judged by hyphen count) |
| ❌ No spaces | Filenames and directory names must not contain spaces |
| ❌ No special characters | Only these are allowed: letters, digits, hyphen `-`, underscore `_`, dot `.` |
| ❌ No underscore abuse | When no nested identifier is needed, use hyphens between segments, not underscores |

### Joining Words Inside a Segment

When one semantic segment consists of several words:

| Language | Joining method | Example |
|----------|----------------|---------|
| Multi-word | Join directly or use underscore | `mental-model-books`, `publication-verification` |
| English | Underscore `_` or camelCase | `personal_auth`, `sharedApi` |

> ⚠️ The underscore used to join words inside a segment and the underscore used between layers are the same symbol but different in meaning. How to tell them apart: the inside-a-segment underscore appears **inside one semantic segment** (e.g. `personal_auth` is one segment), the between-layers underscore appears **between two independent identifiers** (e.g. between `awp-workflow-website-article` and `143022`).

> Agent workflow directories do not use the inside-a-segment English joining rule from this section. They strictly use four segments, each segment one lowercase English word; details in the Agent Workflow Authoring Spec.

### Package Identity Formula

Spec packages, tool packages, and other same-family packages share one identity formula:

```text
{namespace}-{domain}-{target}-{kind}
```

`{namespace}` is the namespace the knowledge base registers in its layout declaration (`layout.yaml`). The entire vault has exactly one value. Examples below use `awp` for demonstration.

✅ After splitting a package ID by ASCII hyphens, it must be exactly four segments. Each segment must match `^[a-z][a-z0-9]*$`. With `awp` as the namespace, the full ID must match `^awp-[a-z][a-z0-9]*-[a-z][a-z0-9]*-[a-z][a-z0-9]*$`.

✅ The `kind` of a spec package is fixed at `spec`. The `kind` of a tool package corresponds to `manifest.json.form`; its values are managed by the Agent Tool Authoring Spec.

❌ No segment of a package ID may contain a hyphen or an underscore. The inside-a-segment joining rules allowed for general filenames do not apply to package identity.

### Date Formats

✅ Dates in filenames and directory names always use the compact format, without hyphens:

| Precision | Format | Example | Hyphen count used |
|-----------|--------|---------|-------------------|
| Month | `YYYYMM` | `202606` | 0 |
| Day | `YYYYMMDD` | `20260428` | 0 |
| Graded | `YYYYMMDDHHmm` | `202607041530` | 0 |
| Timestamp | `HHMMSS` | `183222` | 0 |
| Full | `YYYYMMDD-HHMMSS` | `20260628-183222` | 1 (between date and time) |

❌ The `YYYY-MM-DD` format is forbidden in filenames and directory names (it consumes two extra hyphens and makes the hyphen count fall out of sync with the semantic segment count). **No exceptions—always use the compact `YYYYMMDD` format.**

✅ Timestamps follow `kb-file-structure-metadata.md §0 global timestamp rules` and use the single timezone declared by the knowledge base.

### Length Limits

| Object | Limit | Explanation |
|--------|-------|-------------|
| ✅ Directory name | ≤ 80 characters | If a description title was stuffed into the directory name, shorten it or put the full title in `CLAUDE.md` |
| ⚪ Filename | ≤ 80 characters recommended | No hard limit, but brevity is encouraged |

### Language

| Rule | Explanation |
|------|-------------|
| ✅ Knowledge files use descriptive naming | `positioning.md`, `report-book-review-overview-20260428.md` |
| ⚪ Necessary English allowed | Proper names, abbreviations (e.g. `SEO`), technical identifiers |
| ✅ Credentials/code/tools all lowercase English | `account-gmail-personal-auth.md` |

### Basic Character Principles

Three minimum requirements sit above all naming patterns, and no pattern may violate them:

| Rule | Good | Bad |
|------|------|-----|
| ✅ Knowledge files use descriptive naming | `positioning.md` | `brand-positioning-v2.md` |
| ❌ No spaces | `source-code-course.md` | `source-code course-production.md` |
| ❌ No special characters | Only letters, digits, `-`, `_`, `.` allowed | `course(v2).md` |

---

## §2 Zero-Hyphen Pattern

```
{semantic_name}.ext
```

One segment, zero hyphens. The filename itself is one complete semantic noun.

| Field | Explanation |
|-------|-------------|
| Semantic name | A short, plain noun or phrase |

### Registered Instances

| Implementer | What the semantic name holds | Example |
|-------------|------------------------------|---------|
| {dashboard_root}scheduling/ | Functional purpose | `active.md`, `model-selection.md`, `common-tasks.md` |
| {research_root}discovery/ | Vault-wide index and views | `library-book-list.md`, `term-inverted-index.md` |
| {personal_root} | Domain noun | `transaction-log.md`, `current-holdings.md`, `watch-list.md` |
| {commerce_root}*/ | Fixed triple-set names | `index.md`, `pending-decision.md`, `pending-action.md` |
| Some spec package texts | Spec topic | `authoring.md`, `glossary.md` |
| All directories | System entries | `CLAUDE.md`, `README.md`, `manifest.json` |

### When to Use

- Files with stable content and no version iteration
- Fixed system entries
- An index or master table that exists only once per directory

---

## §3 One-Hyphen Pattern

```
{A}-{B}.ext
```

Two segments, one hyphen.

| Field slot | Allowed semantic types |
|------------|------------------------|
| A | Classifier / date (`YYYYMM`) / number (`NN`) / dimension |
| B | Topic / object / attribute / code name |

### Registered Instances

| Implementer | What A holds | What B holds | Example |
|-------------|--------------|--------------|---------|
| {brand_root} visual version directory | `YYYYMM` | Topic name | `202604-three-arrow-geometry/` (example) |
| {specs_root} glossary | `term-glossary` | Domain | `term-glossary-zh-to-en.md`, `term-glossary-SEOand-marketing.md` |
| {research_root} theoretical frameworks | Framework name | Number or abbreviation | `trust-formula-7114.md`, `brand-story-framework-SB7.md` |
| {personal_root} notes | `notes` | Topic | `notes-financial-statement-reading.md`, `notes-valuation-method.md` |
| {commerce_root} daily scan short sequence | `YYYYMMDD` | Sequence number | `20260710-1.md` (common in discovery module daily scans) |
| Numbered sequences | `NN` (two-digit number) | Title | `01-tool-directory.md`, `03-search-and-discovery.md` |

### When to Use

- Files in the same directory classified along one dimension
- Monthly version snapshots (`YYYYMM-{code_name}`)
- Numbered ordered sequences

---

## §4 Two-Hyphen Pattern

```
{A}-{B}-{C}.ext
```

Three segments, two hyphens.

| Field slot | Allowed semantic types |
|------------|------------------------|
| A | Classifier / date (`YYYYMM`) / number |
| B | Object / subcategory / stage |
| C | Attribute / topic / scenario |

### Registered Instances

| Implementer | A | B | C | Example |
|-------------|---|---|---|---------|
| {brand_root} competitor research | `YYYYMM` | Research topic (e.g. `competitor`) | Dimension | — |
| {brand_root} industry regularities | `YYYYMM` | Category (e.g. `technology-channel`) | Dimension | — |
| {research_root} reference documents | Type (`reference`/`case`) | Source | Topic | `reference-dialogue-analysis-work-pattern.md` |
| Article workflow / translation | Action (`translation`) | Language pair | Stage | `translation-zh-en-draft.md` |
| {commerce_root} business models | `YYYYMM` | `business-model` | Stage | — |

### When to Use

- Files that need three dimensions to be uniquely identified
- Classifier + object + attribute combinations

> ⚠️ If the A segment uses a `YYYYMM` date and B and C together express only one topic, consider whether this is really a one-hyphen pattern (`YYYYMM-topic`). Use two hyphens only when three genuinely independent semantic segments are needed.

---

## §5 Three-Hyphen Pattern

```
{A}-{B}-{C}-{D}.ext
```

Four segments, three hyphens. This is the most structured pattern, for administrative documents and work tasks that need precise positioning.

| Field slot | Allowed semantic types |
|------------|------------------------|
| A | Type word / date (`YYYYMMDD` or `YYYYMMDDHHmm`) / namespace / category |
| B | Object / service / domain / action |
| C | Stage / scope / action / object |
| D | Date (`YYYYMMDD`) / scenario / purpose / status / subdivision |

### Registered Instances

| Implementer | A | B | C | D | Example |
|-------------|---|---|---|---|---------|
| Administrative documents | Type word | Object | Stage | `YYYYMMDD` | `report-mental-model-books-publication-verification-20260428.md` |
| {owner_root} | Type | Dimension | Topic | Scope | `plan-expertise-industry-priority-general.md` |
| Agent workflows | Namespace | Domain | Action | Subdivision | `awp-workflow-x-tweet` (example); each segment one English word |
| {brand_root} identity | Type | Dimension | Topic | Scope | `plan-positioning-industry-agent-workflow-general.md` |
| {brand_root} persona | Type | Dimension | Topic | Scope | `data-persona-L1identity-{persona_key}.md` |
| {tools_root}credentials/ | Category | Service | Scope | Purpose | `cloud-cloudflare-shared-api.md` |
| {dashboard_root}handoff/ | `YYYYMMDDHHmm` | Action | Object | Detail | `202606051430-handoff-presentation-slides-acceptance-trial` |
| {dashboard_root}output/ | `YYYYMMDDHHmmss` | Source | Summary | — | `20260601143000_research-agent_intelligence-brief` |
| {inbox_root}archive/ | `YYYYMMDD` | Type | Object | Disposition | `20260430-book-excerpt-midas-touch-secrets-sealed` |
| {research_root}topic/{topic}/material/{YYYYMM}/ | `YYYYMMDD` | Type abbreviation | Language | Title | `20260607-bk-en-data_feminism` |
| {research_root}subject/{subject}/material/{YYYYMM}/ | `YYYYMMDD` | Material type | Language | Title | `20260807-an-zh-spoken-video-editing-automation-boundary.md` |
| {workflows_root} directory names | Namespace | Domain | Action | Subdivision | `awp-workflow-website-article/` (example) |
| {specs_root} standard packages | Namespace | Domain | Target | `standard` | `awp-knowledge-management-standard/` (example) |
| CLI entry names (commands) | Namespace | Major category | Name | Form | `{prefix}-fetch`, `{prefix}-sync cloud` (examples) |
| {tools_root}best-practice/ directory names | Domain | Tool | Level | Status | `infra-ssh-base-live/` |
| {tools_root}best-practice/ root-level texts | Directory identifier | Purpose | Topic | Scope or date | `claudecode-configuration-base-settings-general.md` |
| Article workflow / recheck | Action | Dimension | `YYYYMMDD` | Scenario | `recheck-report-20260426-prepublication.md` |
| {commerce_root} deep-analysis daily scan | `YYYYMMDDHHmm` | Direction (multi-word segments may join words) | — | — | `202606131106-flywheel-multi-source-intelligence-engine.md` (after the date more than two segments are allowed, see `../methodology/commerce/`) |
| VPS four-segment names (SSH aliases) | Region | Provider | Spec | Sequence number | `us-rn-6c8g-01`, `hk-zgo-4c4g-01` |
| {tools_root}credentials/ VPS files | `infra` | VPS identifier (joined by underscores) | `cloud` | `config` | `infra-us_rn_6c8g_01-cloud-config.md` |

### About "Which Segment Holds the Date"

In the three-hyphen pattern, the position of the date segment depends on the implementer's need:

| Date position | When to use | Reason |
|---------------|-------------|--------|
| **A segment (front)** | Dashboard, inbox, research entries | Sorting by time is the primary need |
| **D segment (back)** | Administrative documents | Type and object are the primary retrieval dimensions; the date is auxiliary |

Both are compliant; just state which one in the registry.

### Type Word Dictionary (for administrative documents)

When the A segment holds a "type word", use these controlled words:

| Type word | Purpose |
|-----------|---------|
| `report` | Analysis, verification, audit results |
| `list` | Candidate, todo, resource lists |
| `master-table` | Summary table, master data table |
| `plan` | Rename plans, collection plans |
| `cache` | API cache, temporary computation |
| `index` | Directory entry, navigation index |
| `backup` | Pre-migration state, rollback-capable copy |
| `excerpt` | Chapter excerpt, fragment excerpt |
| `log` | Run logs, processing logs |

⚪ Type words may be extended, but must stay consistent within one directory.

### Status Word Dictionary (for dashboard / inbox)

When the D segment holds "status / disposition", use these controlled words:

| Status word | Meaning |
|-------------|---------|
| `in-progress` | In progress |
| `pending-schedule` | Waiting to be scheduled |
| `review` | Waiting for review |
| `continuation` | Continuation of the previous stage |
| `acceptance` | Pending acceptance |
| `sealed` | Cold storage |
| `archived` | Formally archived |
| `deprecated` | Deprecation marker |
| `replaced` | Replaced by a newer version |
| `preserved` | Kept for reference |

### Forbidden Words in the Fourth Segment

❌ Relative time words and vague version numbers are forbidden:

```
today  -  latest-version  -  final  -  new  -  final  -  v2  -  latest  -  latest
```

---

## §6 Registry

> Vault-wide index summarizing which pattern each implementer chose. **What each slot holds is defined by the implementer's domain spec**; this table is only a pointer—it records the pattern, an example, and the spec where field definitions live.

### File Naming

| Implementer | Pattern | Slot summary | Example | Field definitions in |
|-------------|---------|--------------|---------|----------------------|
| This spec package's own texts | §5 three hyphens | `kb`-dimension-topic-subdivision | `kb-naming-segment-convention.md` | This spec §5 |
| Other spec package texts | §2 zero hyphens | Semantic name | `authoring.md` | — |
| {owner_root} | §5 three hyphens | type-dimension-topic-scope | `plan-expertise-industry-priority-general.md` | `../methodology/brand/` |
| {dashboard_root}scheduling/ | §2 zero hyphens | Function name | `active.md`, `common-tasks.md` | — |
| {brand_root} identity (`plan` - `data` - `guide` - `constraint`) | §5 three hyphens | type-dimension-topic-scope | `plan-positioning-industry-agent-workflow-general.md` | `../methodology/brand/` |
| {brand_root} persona (incl. L-layer  -  detail library) | §5 three hyphens | type-dimension-topic-scope | `data-persona-L1identity-{persona_key}.md` | `../methodology/brand/` |
| {brand_root}{brand}/operations/audience/ | §5 three hyphens | type-audience-persona-scope | `persona-audience-beginner-student-general.md` | `../methodology/brand/kb-method-brand-audience.md` |
| {brand_root} visual version directory | §3 one hyphen | `YYYYMM`-topic | `202604-three-arrow-geometry/` | `../methodology/brand/` |
| {personal_root} | §2+§3 | Mixed | `current-holdings.md`, `notes-valuation-method.md` | `../methodology/personal/` |
| Prompt files | §4 two hyphens | A-B-C | See Prompt Authoring Spec | Prompt Authoring Spec |
| Article workflow / translation | §4 two hyphens | A-B-C | `translation-zh-en-draft.md` | `../methodology/business/` |
| Article workflow / recheck | §5 three hyphens | A-B-C-D | `recheck-report-20260426-prepublication.md` | `../methodology/business/` |
| Administrative documents (general) | §5 three hyphens | A-B-C-D | `report-book-review-overview-20260428.md` | This spec §5 |
| {tools_root}credentials/ | §5 three hyphens | A-B-C-D | `cloud-cloudflare-shared-api.md` | `../methodology/tools/` |
| {tools_root}best-practice/*/*.md (except fixed entries) | §5 three hyphens | dir-identifier-purpose-topic-scope or date | `claudecode-configuration-base-settings-general.md` | `../methodology/tools/` |
| CLI entry names (entries under `~/.local/bin/`, code in {tool_repository_root}) | §5 three hyphens | A-B-C-D | `{prefix}-fetch` (example) | Agent Tool Authoring standard |
| {dashboard_root}handoff/ | §5 three hyphens | A-B-C-D | `202606051430-handoff-presentation-slides-acceptance-trial` | `../methodology/operations/` |
| {dashboard_root}projects/{product_name}/01-05 nodes | §5 three hyphens | A-B-C-D | `202607061430-V02-test-full-production-smoke-test.md` | Product Development Spec |
| {dashboard_root}output/ | T5 run directory | `{YYYYMMDDHHmmss}_{source}_{summary}` | `20260601143000_research-agent_intelligence-brief` | `../directory/kb-area-dashboard-skeleton.md` |
| roles/*/operations-handbook/ | §5 three hyphens | type-domain-action-subdivision | `method-content-planning-closed-loop.md` | `../methodology/operations/` |
| {inbox_root}archive/ | §5 three hyphens | A-B-C-D | `20260430-book-excerpt-midas-touch-secrets-sealed` | `../methodology/operations/` |
| {research_root}topic/{topic}/material/{YYYYMM}/ | §5 three hyphens | date-type-language-title | `20260607-bk-en-data_feminism` | `../methodology/research/` |
| {research_root}subject/{subject}/material/{YYYYMM}/ | §5 three hyphens | date-type-language-title | `20260807-an-zh-spoken-video-editing-automation-boundary.md` | `../methodology/research/` |
| {business_root} project archives | §5 three hyphens | A-B-C-D | `{seq}-{type}-{title}/` | `../methodology/business/` |
| {business_root}{brand}/official-site/01-08 | §5 three hyphens | type-dimension-topic-scope | `status-SEO-technical-traffic-general.md` | `../methodology/business/kb-method-business-operations.md` |
| {commerce_root}judgment/decision/ | §5 three hyphens | A-B-C-D | `202606251430-agent-cost-control-layer-Go.md` | `../methodology/commerce/` |
| {business_root} strategic decisions | §3 one hyphen | A-B | `decision-{topic}.md` | `../methodology/business/` |
| {business_root} operating data | §3 one hyphen | A-B | `{report_type}-{year_month}.md` | `../methodology/business/` |
| {dashboard_root}research/{YYYYMM}/ | §3+ | date prefix + description | `202607-dashboard-scheduling-unified-task-management-plan.md` | `../methodology/operations/` |
| {commerce_root}discovery/*/ daily scans | §3 one hyphen as the main pattern | date-sequence number or summary | `20260710-1.md`, `202606131106-flywheel-multi-source-intelligence-engine.md` | `../methodology/commerce/` |
| {commerce_root}market-perspective/ | §3+ topic buckets | topic directory / point-in-time file | `discovery-industry-updates/`, `judgment-cognitive-difference/` | `../methodology/commerce/` |
| {commerce_root}*/ fixed triple-set names | §2 zero hyphens | Fixed semantic names | `index.md`, `pending-decision.md`, `pending-action.md` | `../methodology/commerce/` |
| {brand_root}{brand}/operations/ | Domain-defined | Short names of operating texts | `data-business-product-and-pricing-general.md` | `../methodology/brand/` |
| {brand_root}{brand}/operations/competitor/{benchmarks · market · methodology}/ | §2 zero hyphens | Short semantic name | `term-glossary.md`, `authority-figures.md` | `../methodology/brand/kb-method-brand-competitor.md § 3.2` |
| {commerce_root}discovery/new-word-radar/ | §2+§3 | Mixed | `index.md`, `202606251430-01.md` | `../methodology/commerce/` |
| {dashboard_root}scheduling/ tasks | T numbering (T4) | `T`+date-sequence-description | `T20260626-001-website-frontend-update.md` | `../methodology/operations/` |
| {workflows_root}daily/ | §2 zero hyphens | `YYYYMMDD` | `20260623.md` | Agent Workflow Authoring Spec |

### Directory Naming

| Implementer | Pattern | Slot summary | Example | Field definitions in |
|-------------|---------|--------------|---------|----------------------|
| {workflows_root} | §5 three hyphens | A-B-C-D | `awp-workflow-website-article/` (example) | Agent Workflow Authoring Spec |
| {specs_root} | §5 three hyphens, strictly four physical segments | `{namespace}`-domain-target-`standard` | `awp-knowledge-management-standard/` (example) | `{specs_root}naming-map.yaml`  -  Standard Authoring standard |
| Course material units | §3-§5 (1-3 segments) | date-1 to 3 segments from coarse to fine | `20260316-seo-basics-tutorial03-keyword-find-real-user-queries/` | `../methodology/business/` |
| Course material chapters | Dedicated system | series name + number + title + `content_id` | `ClaudeCode01what-is-claude-code20260317132543-claudecode-intro-concept/` | `../methodology/business/` |
| {dashboard_root} monthly partitions | §2 zero hyphens | `YYYYMM` | `202606/` | `../methodology/operations/` |
| {dashboard_root}scheduling/ task directories | §5 three hyphens | `{type}-{domain}-{purpose}-{qualifier}` | `task-brand-operate-relaunch/` | `../methodology/operations/kb-method-task-file.md` |
| {inbox_root}archive/ monthly partitions | §2 zero hyphens | `YYYYMM` | `202606/` | `../methodology/operations/` |
| {brand_root} design version directory | §3 one hyphen | A-B | `202606-workbench/` | `../methodology/brand/` |
| {research_root}topic/{topic}/materials/ monthly partitions | §2 zero hyphens | `YYYYMM` | `202606/` | `../methodology/research/` |
| {research_root}subject/{subject}/materials/ monthly partitions | §2 zero hyphens | `YYYYMM` | `202608/` | `../methodology/research/` |
| {run_output_root} | Nested (between-layers `_`) | workflow_name_`HHMMSS`_topic | `awp-workflow-website-article_143022_ai-programming-introduction/` | `../methodology/operations/` |
| {dashboard_root}research/ | §5 three hyphens | A-B-C-D | `20260605-plan-visual-analysis-cli-continuation/` | `../methodology/operations/` |
| {commerce_root}judgment/decision/ | §5 three hyphens | A-B-C-D | `20260625-agent-cost-control-layer-Go/` | `../methodology/commerce/` |
| Object storage paths | Dedicated system | three layers | `x/20260607/agent-hype-a3f7-cover.webp` | `../methodology/tools/` |

### Registration Rules

✅ **When adding an implementer**: define the concrete semantics and controlled word lists of each slot in the domain methodology spec, then add one index row to this table.
✅ **This table is only a pointer**—it does not redefine field meanings. The single source of truth for field meanings is the domain spec pointed to by the "Field definitions in" column.
❌ **Never define a naming pattern in a domain spec without registering it here**—every pattern must be discoverable from this table.

---

## §7 Applicability Boundary

This spec governs **every filename and directory name produced by the knowledge base**. The four patterns (§2-§5) plus the nested pattern (between-layers `_`) cover the vast majority of cases.

A few objects have names that must carry information a hyphen split cannot express (embedded identifiers, path shapes required by external systems). Register these as **dedicated systems**: mark `dedicated system` in the §6 registry, let the domain spec give the full format and criteria, and this spec keeps only two global constraints—the length limit and the compact date format. **A dedicated system is valid only when registered**—unregistered ones violate the four patterns by default. Two exist today: object storage paths and course material chapters.

**CLI entry names are the only object that lives outside the knowledge base yet is still governed by this spec**: the code lives in the tool repository ({tool_repository_root}), the entry points are installed under `~/.local/bin/`, but these names appear daily in the knowledge base's routing tables and workflows, so the formula must stay the same as inside the vault. Package directory names inside the repository are not governed—those are language-layer package names and follow the language spec.

The following objects are **not knowledge base products**; their names are decided by external systems and are not governed by this spec:

- Source code files (`.py` / `.ts` / `.js` etc.) follow the corresponding language spec
- External downloads keep their source identity until standardized
- Language runtime directories (`__pycache__` / `node_modules`)

The following objects **are knowledge base products**, fixed instances of the §2 zero-hyphen pattern, not exemptions:

- `CLAUDE.md` / `README.md` / `SKILL.md` / `AGENTS.md` (system entries)
- `manifest.json` / `manifest.yaml` (tool / workflow manifests)
- Fixed names of platform release files (e.g. `ghost.md` / `wechat.md`)

### Subdirectory Depth

Subdirectory nesting depth is constrained uniformly by the directory dimension composition rules; see `../directory/kb-directory-decision-composition.md §3 depth limit`.

---

## §8 Enabling and Migration

### How to Enable

An implementer declares the enabled scope in its own directory's `CLAUDE.md` and references this spec:

```markdown
## Naming Rules

This directory enables "File Naming Segment Specification §5 three-hyphen pattern" for administrative documents:

`{type}-{object}-{stage}-{YYYYMMDD}.{ext}`

Applies to: administrative documents such as reports/checklists/plans/indexes/caches/logs.
Does not apply to: CLAUDE.md, real asset files, external downloads.

See: {specs_root}awp-knowledge-management-standard/naming/kb-naming-segment-convention.md
```

✅ State clearly what applies and what does not.
❌ Never just say "follow the naming spec" without saying which pattern and what each segment holds.

### Migration Process

The investigation, mapping, execution, and acceptance flow for batch renaming is detailed in `kb-naming-governance-migration.md`. The two specs complement each other:

- **This spec** answers "what should a filename look like"
- **The governance spec** answers "how to change existing filenames"

---

## §9 Checklist

**When creating a new file**:

- [ ] Confirm this directory has a registered naming pattern in the registry (§6)
- [ ] Filename hyphen count matches the registered pattern
- [ ] Date segment uses the compact format (`YYYYMMDD` or `YYYYMM`), no `YYYY-MM-DD`
- [ ] No hyphen `-` inside a segment, no spaces
- [ ] The fourth segment (if any) does not use forbidden words (`latest`/`final`/`v2` etc.)

**When registering a new pattern**:

- [ ] Declare the concrete field definitions in the implementer's `CLAUDE.md`
- [ ] Add an entry to the §6 registry of this spec
- [ ] State the language and special constraints
- [ ] Package ID passed the strict four-segment regex; no hyphens or underscores inside segments

**When organizing a directory**:

- [ ] First read this spec to decide the target pattern
- [ ] Then run the migration following the flow in `kb-naming-governance-migration.md`
- [ ] After migration, verify hyphen count consistency

---

## Relationship to Other Specs

This spec defines the **structural formula** of a name (how many hyphens, date format, delimiters). Domain specs define **slot semantics** (what each segment holds, controlled word lists). The two layers work together; neither can be missing.

A file path is a storage location, not a permanent identity for a spec document. After a spec document is first registered, renaming or moving it must keep the `document_id`. The generation, preservation, and alias rules for document IDs are in `kb-document-identity-revision.md`.

| Related spec | Relationship | Pattern |
|--------------|--------------|---------|
| `kb-file-structure-metadata.md` | File structure and metadata; this spec is the deepening of its naming part | — |
| `kb-naming-governance-migration.md` | Complementary—this spec governs "what it looks like", the governance spec governs "how to change it" | — |
| `../directory/kb-directory-pattern-registry.md` | Complementary—this spec governs "the name", the directory spec governs "how directories are layered" | — |
| Agent Workflow Authoring Spec | Defines the field semantics and controlled word lists of the four segments of workflow directory names | §5 |
| Agent Tool Authoring Spec | Defines the field semantics and controlled word lists of the four segments of CLI entry names | §5 |
| `../methodology/tools/` | Defines field semantics for credentials, best-practice texts, and object storage paths | §5  -  dedicated |
| `../methodology/research/` | Defines the four-segment semantics of research entries and topic analysis materials | §5 |
| `../methodology/operations/` | Defines field semantics for handoffs, run data, workflow outputs, and role operation handbooks | §5 |
| `../methodology/brand/` | Defines field semantics for identity, persona, and visual asset directories | §3  -  §5 |
| `../methodology/business/` | Defines field semantics for six types of business files, articles, and course materials | §2-§5 |
| `../methodology/commerce/` | Defines field semantics for outputs of each stage of the scan pipeline | §2-§5 |
| `../methodology/personal/` | Defines field semantics for personal files and the yearly/object subdivision rules | §2-§3 |
| Prompt Authoring Spec | Defines the field semantics of the three segments of prompt filenames | §4 |

---

## Changelog

> Rolling window, keep the latest 3 entries, each ≤20 characters.

| Date | Change |
|------|--------|
| 2026-08-15 | Add audience·research paths·competitor row |
| 2026-08-15 | Add site-ops four-seg row |
| 2026-08-14 | Task dir changed to four-seg |
