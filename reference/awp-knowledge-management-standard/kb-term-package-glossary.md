---
document_id: awp-knowledge-management-standard/kb-term-package-glossary
language: en
publication: public
title: "Knowledge Base Management Specification  -  Glossary"
---

# Knowledge Base Management Specification  -  Glossary

> Sourced from all normative documents in this specification package. One concept, one term. A single word cannot serve two different meanings.
> **This table is term normalization only; normative rules follow their respective source documents.**
> Words with same names but different meanings (e.g., different L-level taxonomies, four dimensions, pending execution) have been renamed in this table to avoid conflicts.

---

## I. Naming System

> Source: `naming/kb-naming-segment-convention.md`, `naming/kb-naming-governance-migration.md`

| Term | English | Definition |
|------|---------|------------|
| Hyphen-count layering | hyphen-count layering | File and directory names follow patterns by hyphen count: hyphen count = semantic segment count − 1 |
| Zero-hyphen model | one-segment name | Single segment, no hyphens; used for fixed semantic names in files and directories |
| One-hyphen model | two-segment name | Two segments, one hyphen |
| Two-hyphen model | three-segment name | Three segments, two hyphens |
| Three-hyphen model | four-segment name | Four segments, three hyphens; the most structured pattern |
| Four-segment pattern | four-segment pattern | Generic term for three-hyphen model; each user registers their own field meanings within the four-segment formula |
| Segment separator | segment separator | Hyphen `-`, separates semantic segments at the same level |
| Level separator | level separator | Underscore `_`, used when concatenating identifiers from different levels |
| No hyphen inside segment | no hyphen inside a segment | A semantic segment cannot contain internal hyphens, otherwise the pattern cannot be counted |
| Compact date | compact date | Dates in file and directory names use `YYYYMMDD` / `YYYYMM`, not `YYYY-MM-DD` |
| Spec package ID | spec package ID | Specification package directory name, exactly four lowercase English segments when split by hyphens |
| Naming governance | naming governance | Four-step renaming process: directory research → mapping → execution → acceptance |

---

## II. Files and Metadata

> Source: `naming/kb-file-structure-metadata.md`, `naming/kb-document-identity-revision.md`

| Term | English | Definition |
|------|---------|------------|
| Knowledge file | knowledge file | `.md` files carrying facts or rules, excluding `CLAUDE.md` indices |
| Metadata | metadata | Field table at the start of a file containing status, dates, sources, etc. |
| Document ID | document_id | Cross-language, post-rename, post-move identifier for documents |
| Source revision | source_revision | Integer revision number tracking semantic content changes |
| Sync policy | sync_policy | Rules for when derived versions follow source updates |
| Quality level | quality level | Knowledge file quality tier, L0 to L4 |
| Lifecycle | lifecycle | How file state changes: draft → current → archived |
| Source annotation | source annotation | Mark file content provenance |
| Authoritative copy | authoritative copy | The unique file where a fact can be edited; all other places are pointers only |
| One fact, one source | one fact, one source | Facts like pricing, slogans, themes, audiences exist only in a single authoritative file |
| Cross-area reference | cross-area reference | Cross-region references use paths only, not full text duplication |
| Change log | change log | End-of-file rolling table recording recent changes to this document (≤3 entries / ≤20 characters each) |
| Deprecation notes | deprecation notes | Optional end-of-file section recording short facts about entity deprecation (≤3 entries / ≤20 characters); off by default, positioned before change log |
| Abandoned-plan aside | abandoned-plan aside | Writing deprecated practices in the middle of normal text (prohibited); short facts go in deprecation notes, long text goes to archive; time-stamped snapshots excepted |
| Current-state writing | current-state writing | Normal text documents only correct current practices |

---

## III. Directory Organization

> Source: `directory/kb-directory-pattern-registry.md`, `directory/kb-directory-decision-composition.md`

| Term | English | Definition |
|------|---------|------------|
| Directory pattern | directory pattern | Registered structure patterns: time-driven, entity bucketing, knowledge organization, asset naming, product R&D (five categories) |
| Pattern registration | pattern registration | New areas must select patterns from the registry, not invent new ones |
| Stackable | stackable | An area can combine multiple patterns; stacking order is fixed |
| Uniform within a level | uniform within a level | Only one pattern per hierarchy level; no mixing |
| Depth restraint | depth restraint | After stacking patterns, directories should not exceed 4 levels |
| Physical layout | physical layout | How directories are actually organized, e.g., by brand × product or channel |
| Mixed workspace | mixed workspace | Multiple primary categories at top level; subdirectories each declare their own type |

---

## IV. Entry Files (CLAUDE.md)

> Source: `directory/kb-entry-layer-levels.md`, `directory/kb-entry-authoring-standard.md`, `directory/kb-entry-multiagent-compatibility.md`

| Term | English | Definition |
|------|---------|------------|
| L0 global layer | global layer | `~/.claude/CLAUDE.md`, persistent across projects |
| L1 project layer | project layer | Project `.claude/CLAUDE.md`, declaring identity and machine-specific rules |
| L2 vault root layer | vault root layer | Knowledge base root `CLAUDE.md`, carries main responsibility and multi-framework sources |
| L3 domain layer | domain layer | Primary directory facade plus subdirectory index |
| L4 subdomain layer | subdomain layer | Secondary directory pure file index |
| L5+ leaf layer | leaf layer | Deeper leaf nodes, adapted by function into five categories |
| Domain override | domain override | Directory rules owned exclusively by domain specs, not fitted to generic templates |
| Controlled sections | controlled sections | Permitted section set; exceeding it violates compliance |
| Progressive disclosure | progressive disclosure | Upper layers provide thin entry points; details loaded from lower layers as needed |
| Size budget | size budget | Line or character count ceiling per layer, preventing context bloat |
| Multi-framework compatibility | multi-framework compatibility | Relationship between mirror files like `AGENTS.md` and `CLAUDE.md` source |
| Automated check | automated check | Full-library scan using `KB audit claude` |

---

## V. Brand and Persona

> Source: `directory/kb-area-brand-skeleton.md`, `methodology/brand/`

| Term | English | Definition |
|------|---------|------------|
| Brand | brand | Union of business domain and identity domain; path `{brand_root}{brand}/` |
| Business dimension | business dimension | Established business: business model, audience, competitors |
| Identity dimension | identity dimension | Who we are and how we are perceived: strategy, persona, expression, visual, cognition |
| Four dimensions | four dimensions | Four brand directory dimensions: strategy, business, identity, content |
| Project owner | project owner | Person-centered facts (expertise, vision, experience); shared across brands |
| Symlink | symlink | Workflows link only to brand authoritative copy, never maintain second edition |
| Persona | persona | Loadable inner narrative: values, thinking, emotion, memory, decision habits |
| Persona-driven | persona-driven | Derive sentences from "how this person would see it," not from sentence templates |
| Viewpoint loop | viewpoint loop | Inner steps before writing: establish stance → decide what to give → recall → intent → present and check |
| Stable layer | stable layer | Rarely-changed persona foundation: core, narrative arc, value conflicts |
| Living layer | living layer | Regularly-updated detail library, memory index, habit calibration |
| Minimal loading | minimal loading | Default to load only core settings during writing; add optional layers as needed, never read entire system |
| Detail library | detail library | Merged experiences and on-site material long-form, taking by section as needed |
| Persona instance | persona instance | Completed persona answers for a specific brand |
| Tone summary | tone summary | Short expression-layer description, not a pile of banned-word lists |
| Reference sample | reference sample | Workflow-side model text, borrowed for rhythm only, not stance-determining |

---

## VI. Commerce

> Source: `directory/kb-area-commerce-skeleton.md`, `methodology/commerce/`

| Term | English | Definition |
|------|---------|------------|
| Stage | stage | Three stages: discovery / judgment / retrospective, not numbered |
| Module | module | One concrete scan line within a stage, e.g., new-term radar |
| Commerce method doc | commerce method doc | Method files under `{commerce_root}methodology/`, filename may include stage classifiers |
| Three-part set | three-part set | Daily scan + `index.md` + `pending-{next}.md` |
| Daily scan | daily scan | Scan output entries written by day |
| Scan verdict | scan verdict | Decision: continue investing or abandon candidate direction |
| Go/Kill | Go/Kill | Two scan verdict outcomes: continue or abandon |
| Blue ocean | blue ocean | Five checks to pass before entering pending-judgment |
| Red ocean | red ocean | Directions failing blue-ocean checks; daily-scan only, no deep review |
| Pending review | pending review | Candidate list from discovery module for deep analysis |
| Pending handoff | pending handoff | Handoff file from judgment module to brand operations or business area |
| Market view | market view | Slice of external intelligence and industry dynamics |
| On demand | on demand | Runs only when needed; not triggered periodically by default |
| Three-way correspondence | three-way correspondence | Methods, workflows, output directories grow and shrink together |

---

## VII. Business

> Source: `directory/kb-area-business-skeleton.md`, `methodology/business/`

| Term | English | Definition |
|------|---------|------------|
| Primary category | primary category | One of seven asset types; single-select, written in asset metadata |
| Facet | facet | Seven multi-select label dimensions for retrieval and filtering |
| Two-axis structure | two-axis structure | Primary category as backbone, facets as tags; use both together |
| Controlled vocabulary | controlled vocabulary | Facet allowed values defined uniformly in main spec |
| Operating asset | operating asset | Continuously maintained in-use resource; includes website product catalog |
| Project record | project record | One-time deliverable with definite start and end |
| Project plan | project plan | Zero-to-one proposal; plan files go in dashboard research |
| Content ID | content ID | Cross-channel content unit stable identifier, four segments with three hyphens |
| Content registry | content registry | Registration of `content-registry` and display directory names |
| Four-part short name | four-part short name | Content naming format for some channels, e.g., `{tool}-{theme}-{angle}` |
| Three product layers | three product layers | Operations material in business area, projects in dashboard, code in repo |
| Handoff rule | handoff rule | Boundary between business area and brand, dashboard, workflow, credential areas |

---

## VIII. Research

> Source: `directory/kb-area-research-skeleton.md`, `methodology/research/`

| Term | English | Definition |
|------|---------|------------|
| Topic | topic | Generic long-term partition, path `topics/{name}/` |
| Focus area | focus area | Current priority partition, path `focus-areas/{name}/` |
| Research project | research project | Four-segment directory under `materials/{YYYYMM}/`, minimum research unit |
| Research four-segment | research four-segment | `{YYYYMMDD}-{kind}-{lang}-{title}[.{ext}]` |
| kind | kind | Second segment of four-segment: primary type or role code, must be whitelisted |
| Raw | raw | Unique `*-raw-*` file, unmodified; when no raw exists write `...raw.pending.md` |
| Std | std | Unique `*-std-*.md`, research project authoritative copy |
| Nav | nav | `kind=nav`, filename `*-nav-*-nav.md`, records chapter row-number indices |
| Excerpt | excerpt | Action: extract one segment from standardized copy by nav coordinate |
| Line-based excerpt | line-based excerpt | Complete excerpt description when coordinate is row number |
| Card | card | `kind=card`, filename `*-card-*-interpretation.md`; interpretation and card are equivalent |
| Proc | proc | `kind=proc` intermediate file, must live in `processes/` directory |
| Term correction | term correction | Edit standardized copy and subtitles, never raw |
| Research quality level | research quality level | L0 archived, L1 excerpt-ready, L2 citable |
| Discovery layer | discovery layer | `discovery/` directory, machine-readable index |

---

## IX. Operations

### 9.1 Dashboard and Roles

> Source: `directory/kb-area-dashboard-skeleton.md`, `methodology/operations/kb-method-dashboard-role.md`

| Term | English | Definition |
|------|---------|------------|
| Dashboard | dashboard | Operations headquarters directory `{dashboard_root}` |
| Governance roles | governance roles | Permanent governance: chairman, CEO, auditor, etc. |
| Execution roles | execution roles | Optional manager roles as needed |
| Shared role assets | shared role assets | `{dashboard_root}roles/shared/`, reusable real assets for all |
| Role protocol | role protocol | Normative-side universal behavior guidelines |
| Role handbook | role handbook | Single-role private templates and decision principles |
| Four-way alignment | four-way alignment | Correspondence between brand, role, workflow, business |
| Write boundary | write boundary | Who can write which directories; crossing prohibited |
| Task assignment rule | task assignment rule | Cross-role delegation and reporting agreements |
| Temporary window | temporary window | Dynamically built execution window and task line code |
| Workflow output | workflow output | Workflow run results, partitioned monthly then daily |

### 9.2 Task Hub

> Source: `methodology/operations/kb-method-task-*.md`

| Term | English | Definition |
|------|---------|------------|
| Task hub | task hub | `{dashboard_root}schedule/`, task and reporting system |
| Task file | task file | One file per task, containing frontmatter and body |
| State machine | state machine | Six task states and allowed transitions |
| Output contract | output_contract | Delivery agreement for automated task execution |
| Waiting user | waiting_user | High-risk task state, requires human judgment |
| Executor | executor | Tool or window type that actually runs the task |
| Automation record | automation record | Mirror registry of timed task in knowledge base |
| Run report | run report | Flat report from each audit run, or directory report from workflow |
| Pending tasks | pending tasks | Unfinished tasks, partitioned monthly |
| Completed tasks | completed tasks | Archive directory for finished tasks |
| Write-back | write-back | Update execution results to task file and contract fields |
| Task ownership | task ownership | File and state are source of truth; ownership stays with knowledge base, not window session |

### 9.3 Inbox

> Source: `directory/kb-area-inbox-skeleton.md`, `methodology/operations/kb-method-inbox-*.md`

| Term | English | Definition |
|------|---------|------------|
| Inbox | inbox | Transit area, not a permanent repository |
| Placement | placement | Move transit file to its true destination |
| Four placement dimensions | four placement dimensions | Four judgment dimensions during placement |
| Archive | archive | `{inbox_root}archive/{YYYYMM}/`, soft-delete and archival endpoint |
| Soft delete | soft delete | Move to archive area, not direct physical deletion |
| Screenshot staging | screenshot staging | Landing point for temporary screenshots |
| Workstation staging | workstation staging | Landing point for cross-machine temp files |
| Root discipline | root discipline | Only spec-declared subdirectories allowed at inbox root |
| Run-data pointer | run-data pointer | Inbox holds pointers to dashboard run data, not the original text |

### 9.4 Engagement Strategy

> Source: `methodology/operations/kb-method-engagement-strategy.md`

| Term | English | Definition |
|------|---------|------------|
| Engagement strategy | engagement strategy | Complete flow from target selection through reply to feedback loop |
| Target selection | target selection | Decide whose posts to reply to |
| Logging | logging | Keep engagement log and fields when acting |
| Data retrieval | data retrieval | Retrieve engagement data |
| Attribution | attribution | Determine which factors drove results via slice comparison |
| Four attribution dimensions | four attribution dimensions | Minimum four slices: audience scale, timing, content style, topic |
| Feedback to strategy | feedback to strategy | Write attribution conclusions back to target selection or reply style |
| Target snapshot | target snapshot | Record counterparty scale, topic, engagement data when acting; never rewrite post-hoc |
| Attribution report | attribution report | Instance-level attribution conclusion file `effect-attribution.md` |
| Threshold | threshold | Instance-defined immediate, cumulative, long-tail metric ceilings |
| Reply log | reply log | Monthly JSON record `reply-logs/{YYYYMM}.json` |
| Strategy instance | strategy instance | Specific values and clauses of operational strategy for one brand-channel |

---

## X. Personal

> Source: `directory/kb-area-personal-skeleton.md`, `methodology/personal/`

| Term | English | Definition |
|------|---------|------------|
| Eight life domains | eight life domains | credential, law, body, mind, finance, home, leisure, business |
| Privacy level | privacy level | L0 to L3; L3 prohibited from logging |
| Decision type | decision type | Long-term retrospective life file |
| Record type | record type | Snapshot archive life file |
| Reference type | reference type | Continuous-append life file |
| Three-tier skeleton | three-tier skeleton | Sections divided into required, recommended, lifestyle-optional three tiers |
| Privacy first | privacy first | Minimal metadata, lower recording burden |
| Empty domain | empty domain | Can keep index only; build body text when truly activated |

---

## XI. Tools

> Source: `directory/kb-area-tools-skeleton.md`, `methodology/tools/`

| Term | English | Definition |
|------|---------|------------|
| Credential file | credential file | Markdown file recording API keys, account info, etc. |
| Machine-readable section | machine-readable section | Fields or section zones in credential file readable by machines |
| Parsing contract | parsing contract | Agreement for tools to extract fields from Markdown |
| Three-level fallback | three-level fallback | Three fallback value-fetch methods if parsing fails |
| Flat layout | flat layout | `{tools_root}credentials/` without subdirectories, only `.md` files |
| Placeholder credential | placeholder credential | Placeholder in skill or CLI, not real machine values |
| Purpose vocabulary | purpose vocabulary | Permitted use-case enum for credentials |
| Section whitelist | section whitelist | Set of standard sections allowed in credential files |
| Ledger style | ledger style | Multi-entry registration-style credential format |
| Expiry handling | expiry handling | Process when credential expires: move to inbox archive, etc. |
| See credential | see credential | Reference style when pointing to credential file from text |
| Credential separation | credential separation | Normal text uses "see credential" only, never real values |
| Tutorial-style practice | tutorial-style practice | Reproducible deployment tutorial plus complete runnable asset package |
| Runnable asset bundle | runnable asset bundle | Config, scripts, and other directly-runnable attached files |
| Entry CLAUDE | entry CLAUDE.md | Only human and agent entry point for tool folder |
| Skeleton sections | skeleton sections | Required and recommended section set |
| Directory tag | directory tag | Second segment of tool directory four-segment name; `overview/` always uses `overview` |
| Body four-segment name | body four-segment name | `{directory-tag}-{purpose}-{theme}-{scope-or-date}.md` |
| Purpose word | purpose word | Controlled term in body four-segment second segment, declaring this document's work |
| Scope or date | scope or date | Body four-segment fourth segment: long-term docs specify scope, time snapshots use compact date |

---

## XII. Methodology Four-Layer

> Source: `methodology/research/kb-method-research-theory.md`

| Term | English | Definition |
|------|---------|------------|
| Theory layer | theory layer | Why do it: classical theory and problem definition |
| Methodology layer | methodology layer | How to do it: reusable method system |
| Workflow layer | workflow layer | What to do each step: executable steps |
| Output layer | output layer | What result looks like: acceptance criteria |
| Four-layer chain | four-layer chain | Theory → methodology → workflow → output |
| Traceability | traceability | Any output can trace back to its workflow, methodology, theory |
| Methodology admission | methodology admission | Conditions that must be met before upgrading to formal method |
| Diagnostic tracing | diagnostic tracing | When output falls short, reverse-trace which layer broke |
| Six archetypes | six archetypes | Six common prototypes in methodology building |
| Task-driven | task-driven | Four layers are thinking framework, not fixed to directory paths |
| Top-down guidance | top-down guidance | Lower layers do not reverse-depend on upper-layer details |

---

| Date | Change |
|------|--------|
| 2026-08-07 | Merged 15 prior glossaries, de-duplicated and unified same-name words |
