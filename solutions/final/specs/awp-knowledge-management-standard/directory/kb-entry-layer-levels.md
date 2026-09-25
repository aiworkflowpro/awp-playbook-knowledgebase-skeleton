---
document_id: awp-knowledge-management-standard/directory/kb-entry-layer-levels
language: en
publication: public
title: "CLAUDE.md Layer Levels Detailed Explanation"
---

# CLAUDE.md Layer Levels Detailed Explanation

> Scope: In the **six-layer system** of `CLAUDE.md`, how each layer writes itself—positioning, chapter framework, per-chapter requirements, layer division of labor.
> Out of scope: Laws, controlled chapter table, capacity references, template, machine checks (→ `kb-entry-authoring-standard.md` main spec); also how to fix mistakes (→ `kb-entry-antipattern-archiving.md`).
> How to use: Read main spec first to identify layer; then come here read that layer section.

---

## L0 Global CLAUDE.md

> `~/.claude/CLAUDE.md` is the **top layer** of the `CLAUDE.md` system (master compendium). Auto-load every session start; defines cross-all-project constant settings.

### L0 Positioning

L0 is Agent's **cross-project constant layer**. Loads on startup in any directory, so only holds "needed anywhere" content.

Project-specific content (identity, behavior rules, tools, library routing) in L1 (project `.claude/CLAUDE.md`) and L2 (library root `CLAUDE.md`).

```text
L0  ~/.claude/CLAUDE.md        ← Cross-project constant (all-project shared)
L1  .claude/CLAUDE.md          ← Identity + host-specific rules + @L2 (project entry)
L2  CLAUDE.md                  ← Main carrier (behavior+tool+navigation+shortcut)
```

### L0 Design Philosophy

- **Constant load minimized**: This file full-load every session; every line costs context. Shorter better.
- **Criteria admission**: Not enumerate "only can put what"; use admission criteria—criteria clauses stay valid content evolves.
- **Stability priority**: Should change very rarely.

### L0 Admission Criteria

Content wants entry L0 ✅ must satisfy all three:

| Criterion | Explanation |
|------|------|
| **Cross-project** | Needed in any directory startup (not depend some library or project exist) |
| **High-frequency** | Used most sessions |
| **Stable** | Expect unchanged months |

Any lack one → sink to L1 or L2.

#### Typical Legal Content

| Content | Explanation |
|------|------|
| Language rules | Think language + interact language + fault tolerance |
| Think mode | Deep think toggle etc. |
| Abbreviation table | High-frequency shorthand |
| Cross-project operation protocol | e.g., unified file preview command agreement |
| Design philosophy motto | ⚪ One sentence |

#### Prohibited (has dedicated layer)

| Info | Should Go |
|------|---------|
| Agent identity personality | L1 `.claude/CLAUDE.md` (no L1 embedded projects merge to L2) |
| Project behavior rules (tool / Skill / search) | L2 `CLAUDE.md` behavior rules |
| Design constraint (language coding rules) | L2 `CLAUDE.md` behavior rules |
| MCP list, tool route | L2 `CLAUDE.md` tool route |
| Library path | L1 `.claude/CLAUDE.md` (no L1 embedded projects merge to L2) |
| Host-specific rule (multi-machine fleet management) | L1 host-specific rule layer (no L1 embedded projects merge to L2; see below L1 optional layer) |

### L0 Capacity

Row budget see main spec §Capacity (L0 row; hard line).

---

## L1 Project CLAUDE.md

> `.claude/CLAUDE.md` is project-level instruction file. Auto-load on startup: define this library's identity; carry host-specific rules; @expand L2 via reference.

### L1 Positioning

L1 has two functions:

1. **Identity entry**: This project's Agent name; where find complete guide (@expand L2).
2. **Host-specific rule layer**: Only constrain current host (current Agent framework and compatible readers); rules not into shared multi-framework source.

Second function's origin: L2 via root `AGENTS.md → CLAUDE.md` symlink feeds all frameworks simultaneously (see `kb-entry-multiagent-compatibility.md`)—every rule in L2 read by all frameworks. Only want current-host to see (e.g., multi-machine fleet manage, context manage protocol) go L1 to not leak into other frameworks' context.

⚪ L1 optional layer: Accept host-specific rules into shared source; trade single file for manage simple projects; can skip `.claude/CLAUDE.md`; merge identity + host-rule into root `CLAUDE.md`. `{source_vault_root}` currently this mode; adopt per `kb-entry-multiagent-compatibility.md § Framework Registry` state.

```text
L0  ~/.claude/CLAUDE.md        ← Cross-project constant (auto-load)
L1  .claude/CLAUDE.md          ← Identity + host-specific rules + @L2 (auto-load; current host only)
    └── @CLAUDE.md             ← L2 expand (multi-framework shared source)
```

### L1 Design Philosophy

- **Identity first**: Identity definition always front; @expand immediately follow.
- **Shared/host-specific split**: Which layer rule goes; whether other framework should read—should-share to L2; host-only to L1.
- **Project isolate**: Different libraries each own L1; no interfere.

### L1 Chapter Framework

| # | Chapter | Required | Explanation |
|---|------|:----:|------|
| ① | Identity Define | ✅ | Agent personality + library path |
| ② | @Expand L2 | ✅ | One line @reference to root `CLAUDE.md` |
| ③ | Host-Specific Rule | ⚪ | Only-current-host rule; per-function group `##` section |

#### ① Identity Define

✅ Must include:

| Element | Explanation |
|------|------|
| Personality statement | One sentence (e.g., "you serve {project_name}'s {personality}") |
| Library path | Point to root `CLAUDE.md` |

#### ② @Expand L2

✅ One line @reference; expand library's complete guide.

```markdown
@{library_absolute_path}/CLAUDE.md
```

❌ Prohibit multiple @references in L1. All resource route (spec, rule, etc.) manage in L2.

#### ③ Host-Specific Rule

⚪ Optional. Admission: **This rule only constrain current-host behavior; not apply to (or expose to) other frameworks entering via `AGENTS.md`**.

| Typical Content | Why L1 |
|---------|------------|
| Multi-machine fleet management (window control, task delegate) | Only current host do dispatch; other framework shouldn't fleet-op |
| Context manage protocol | Specific current host's session mechanism behavior rule |
| Host-exclusive role load note | Depend current host's session and window system |

❌ Criterion unsatisfied rules (apply all frameworks' behavior; tool route) → L2.
❌ Prohibit repeat L2 content in L1—L1 and L2 load same-screen via @expand; repeat double.

### L1 Capacity

Row budget see main spec §Capacity (L1 row).

### L1 Template

```markdown
## Identity Define

You serve {project_name}'s {personality}. Prefix each interaction with "{personality}".

- Library: `{library_absolute_path}` (main carrier → `CLAUDE.md`)

@{library_absolute_path}/CLAUDE.md

## {Host-Specific Function One} (⚪)

{rule}

## {Host-Specific Function Two} (⚪)

{rule}
```

### L1 Multi-Library Parallel

Different terminal switch different library directory start Agent; each load own L1:

```text
Terminal 1: cd {library_A_path} && {agent_command}
  → L0 + {A}/.claude/CLAUDE.md + @{A}/CLAUDE.md

Terminal 2: cd {library_B_path} && {agent_command}
  → L0 + {B}/.claude/CLAUDE.md + @{B}/CLAUDE.md
```

Identity and tool route auto-switch by directory.

---

## L2 Library Root CLAUDE.md

> Library root directory `CLAUDE.md` authoring spec. Library's **main carrier**; Agent's complete work map; simultaneously **sole shared source** across frameworks.

### L2 Positioning

L2 is library's **sole main carrier**. Agent via L1's @expand enter L2; get behavior rules, tool route, library navigation, shortcut guide—all runtime needed info in one file.

L2 is also **multi-framework shared source**: root `AGENTS.md → CLAUDE.md` symlink feeds all frameworks (see `kb-entry-multiagent-compatibility.md`). Every content in L2 reaches all frameworks—host-only rule keep L1; not here.

L2 answer core question: **How to work, use what tool, go find where**.

### L2 Design Philosophy

- **Main carrier**: L2 is L1's @expand target; carry all library runtime guide.
- **One-page overview**: After read L2; Agent should form complete library cognition.
- **Shared source awareness**: Content apply all frameworks becomes L2; only-one-host rules belong L1.
- **Shortcut lane**: High-frequency scenario give shortcut guide; skip layered route less hop.
- **Rule inline**: Behavior rule write direct in behavior rule function area; not via extra @expand.
- **Detail over brief**: L2 must-load file; prefer detailed; don't make Agent extra Read.

### L2 Organization: Mandatory Function + Open Extend

L2 by **function** organize; ✅ must cover five mandatory functions; chapter name and number (## level or ## both) not lock; function coverage key:

| Function | Required | Content |
|------|:----:|------|
| Header positioning | ✅ | Title + base path + CLI shorthand (`>` quote) |
| Behavior rule | ✅ | Scenario-grouped behavior principle (tool / content / code / delivery etc.) |
| Tool route | ✅ | MCP table + local tool route (+ crosscut shorthand) |
| Navigate + shortcut | ✅ | Directory overview + trigger word → path |
| Changelog | ✅ | Follow `naming/kb-file-structure-metadata.md` §1.1 |

⚪ **Extend function area**: Standard function cover not all real need (e.g., runtime environment and sync topology; role trigger route) per need add dedicated chapter; one function one chapter; per-function name. Criterion: Content useful all frameworks' Agent (shared source awareness); not belong existing function.

> Not set "always-load" section: Behavior rule inline. If really need immediate-load file; after header positioning use `@absolute-path` one line inject; not new chapter.
> Not set "memory" section: After and recovery rule belong behavior rule "delivery" group; not new chapter.

### L2 Per-Function Detail

#### Header Positioning

✅ Title, base path, CLI shorthand. Use `>` quote block.

```markdown
# {library_name}

> Base path: `{absolute_path}`
> Shorthand `KB` = `{CLI entry command}`
```

❌ Prohibit write history; quantity statistic (decay).

#### Behavior Rule

✅ Group by scenario use `###`; typical grouping:

| Group | Content |
|------|------|
| Tool and content | Tool priority, workflow route, read spec before change, index sync |
| Code | Language and package manage constraint, start-stop spec |
| Delivery | Self-verify, task output format |

⚪ Library-unique rule group (e.g., cognition discipline, language style) per need add. Each rule use **bold keyword** + unambiguous condition→action.

#### Tool Route

✅ Two parts: MCP table + local tool route.

**MCP table**: Columns `MCP | Purpose | Note`. No special note fill `—`.

**Local tool route**: Per intent per line; header note call and dynamic-discover command. ⚪ Can add crosscut shorthand.

❌ Prohibit write each tool detail usage—belong tool's own `CLAUDE.md`.

#### Navigate and Shortcut

✅ Directory overview table: Columns `Directory | Responsibility | Trigger`; per first-level directory one line.

✅ Shortcut guide: Trigger→path shortcut. 

- ✅ Can cross-level reference (L2 direct→L5 file); intentional shortcut.
- ✅ Can use template path (e.g., `{run_output_root}{YYYYMM}/{YYYYMMDD}/`) merge same kind.
- Many entries group by domain; not split 10+ title.

⚪ Command quick-lookup: Per type ≤3 high-frequency; point complete list; can merge tool route.

#### Changelog

✅ Required. See main spec §Changelog Convention.

### L2 ↔ L1 Division

| Content | Where | Criterion |
|------|------|------|
| Behavior rule, tool route, navigate apply all framework | L2 | Shared source |
| Rule only constrain current host (fleet, context) | L1 | Host-only; not shared |
| Identity define | L1 | Project entry |

### L2 ↔ L3 Division

| Dimension | L2 (Main Carrier) | L3 (Domain Index) |
|------|------------|--------------|
| Behavior rule | ✅ Complete rule | Domain-specific rule |
| Tool route | ✅ MCP + route | Tool dependency subset (⚪) |
| Trigger route | ✅ Complete map | Not repeat |
| Directory structure | First-level overview | Subdirectory expand |
| Command quick-lookup | High-frequency | Not repeat |

### L2 Capacity

Row budget see main spec §Capacity (L2 row).

---

## L3 Domain CLAUDE.md

> All first-level directory `CLAUDE.md` under library root; authoring spec. Don't hardcode directory checklist—when new first-level directory added auto-apply.

### L3 Positioning

L3 is each first-level directory's **domain facade index**. Agent jump L2 to certain first-level directory; read L3 get complete domain navigation—subdirectory structure, file checklist, operation entry, domain-specific rule.

L3 answer core question: **This domain has what, how organize, when read which subdirectory**.

### L3 Design Philosophy

- **Domain autonomous**: L3 is domain's authority index; domain's structure, rule, operation all define here.
- **Not overflow**: L3 manage own domain content; not repeat L2 global info; not invade other domain.
- **Detail layering**: Subdirectory use table overview; detail leave L4; file use index; content leave file itself.
- **Domain rule sink**: Only domain-apply operation rule go L3; not float to L2.

### L3 Organization Framework

L3 ✅ must organize per order:

| # | Chapter | Required | Explanation |
|---|------|:----:|------|
| ① | One-line position | ✅ | `>` quote; one sentence (≤30 char or one nature sentence) |
| ② | Subdirectory Index | ✅ | List all subdirectories in table |
| ③ | File Index | ⚪ | This directory's direct file (no subdirectory when ✅) |
| ④ | Operation Guide | ⚪ | Quick start, command example, usage flow |
| ⑤ | Tool Dependency | ⚪ | Domain task frequent tool (scenario→tool→form→example) |
| ⑥ | Domain Rule | ⚪ | Only-this-domain behavior rule |
| ⑦ | Changelog | ⚪ | Follow `naming/kb-file-structure-metadata.md` §1.1 |

### L3 Per-Chapter Detail

#### ① One-Line Positioning

✅ Use `>` quote; one sentence what domain manages. Naming convention, split criterion, spec pointer don't go positioning—each belong own chapter.

```markdown
# {tools_root}

> CODE+AUTH: source+credential+index.
```

| Good | Bad | Why |
|----|-----|------|
| `> WHO: who am I, write whom, what tone.` | Three-line pile naming convention and criterion | Positioning only answer "what here" one question |

#### ② Subdirectory Index

✅ Structured index cover all subdirectory. Chapter name unified **`## Subdirectory Index`**—whole library same concept one name; ❌ no more "brand index" "directory index" variants.

Two format both ok:

- **Table** (recommend): Three column (directory/content/trigger) or adjust by domain.
- **Code-block tree**: Hierarchy clearer for level; but ❌ only expand to second—deeper level by that directory's own `CLAUDE.md` carry.

```markdown
## Subdirectory Index

| Directory | Define | Trigger |
|------|------|--------|
| app/ | CLI tool flat register | Tool, script |
| best-practice/ | One-tool-one-folder tutorial | Best practice, pitfall |
| credential/ | API Key and Token | Credential, secret |
```

| Rule | Constraint |
|------|------|
| Per subdirectory one line | ✅ Miss none |
| Trigger column | ⚪ If subdirectory clear trigger scene add |
| Structure count | ❌ Prohibit "N total" exact count (see `kb-entry-antipattern-archiving.md` § antipattern - structure-count)—use nature description |

❌ Prohibit expand subdirectory **file structure** in subdirectory index—L4 job.

#### ③ File Index

⚪ When L3 direct contain file (not subdirectory file) use.

```markdown
## File Index

| File | Explanation |
|------|------|
| position.md | Brand value + red line + persona base |
```

⚠️ Default not list subdirectory internal file—those by subdirectory's own `CLAUDE.md` index. But high-frequency access subdirectory can list key file (≤5) via "shortcut guide" as shortcut not complete file index.

#### ④ Operation Guide

⚪ Tool and workflow type L3 recommend have; brand / spec / business usually not.

**Operation guide boundary**:

| Info Type | L3 Put What | Not Put |
|---------|----------|---------|
| Tool / resource checklist | ✅ Complete route table (name+one-line) | Each tool detail param (belong tool's `CLAUDE.md`) |
| Quick start example | Represent example (per type 1-2) | All tool complete usage |
| Quick lookup | One merged task→entry table | Repeat table (quick lookup and task route separate) |

**Key distinction**: Complete route table (Agent per-it locate resource) ≠ detailed usage tutorial (Agent find resource after need). Route table L3 core job ✅ complete; detailed belong L4+.

#### ⑤ Tool Dependency

⚪ When domain task call external tool add. Format: scenario→tool→form→example four column; ≤15 line; tail point back `{tools_root}CLAUDE.md`; chapter name see main spec §Controlled Chapter.

❌ Prohibit copy `{tools_root}CLAUDE.md` complete route—only domain high-freq subset.
❌ Domain itself is tool register center (e.g., `{tools_root}`) don't need—own route already cover.

#### ⑥ Domain Rule

⚪ Only-this-domain apply rule put L3.

**Rule belong judge**:

| Rule Apply Range | Go Where |
|------------|-------|
| Global apply (all domain) | L2 behavior rule |
| Single domain apply | This domain L3's domain rule chapter |
| Single tool/scenario apply | L3 or leaf `CLAUDE.md` |

#### ⑦ Changelog

⚪ Optional. See main spec §Changelog Convention.

**Audit/health-check large report** ❌ prohibited inline L3. Archive independent file; L3 changelog leave one-line summary.

### L3 Route-Hub-Type Exception

Few L3's core job **library-level route** (e.g., spec area entry coverage matrix + quick-find; workflow area task-route total). This type L3 follow adjust:

| Constraint | Normal L3 | Route-Hub Type |
|------|---------|-----------|
| Total reference line | Main spec §Capacity L3 row | Not apply—by route complete decide |
| Single table >80 row | Split to independent route file | **Split two choices**: Group multi `###` sub-group table; or sink independent route file pointer |
| Content boundary | Same normal L3 | **Not relax**—still pure route (intent→entry); operation manual, SOP, directory tree full expand all violate |

**Judge**: This L3 by L2 or multi-domain as intent-distribute total entry; route entry naturally cover whole library → route-hub type. Common domain long table not—first review content overflow.

### L3 De-Duplication Principle

L3 above-below info boundary:

| Info Type | L2 Have | L3 Put What | L4 Put What |
|------|--------|----------|----------|
| Directory structure | First-level name | Second-level expand | Third-level expand |
| Trigger word | Domain-level | Subdirectory-level | File-level |
| Tool dependency | Not put (L2 only manage route entry) | Domain high-freq subset | Not repeat (point L3) |

**Judge standard**: If table already complete exist subdirectory's `CLAUDE.md`; L3 only put one-line pointer; not copy.

### L3 Cross-Reference

When Agent complete task need read two different domain info (e.g., operation guide in A domain; credential in B domain); primary domain ✅ must pointer to cooperate domain.

```markdown
| Scenario | Path | Relation |
|------|------|------|
| {operation} | `{primary_domain_path}` | → {cooperate_domain}: `{related_file_path}` |
```

❌ Prohibit copy another domain complete content in L3—only pointer.

### L3 Shared Mapping Table

Mapping cross-multi L3 use (e.g., name↔directory map); ✅ must be findable in each use L3.

| Method | Use |
|------|---------|
| **Inline** | Map table ≤10 row |
| **Pointer** | Map table >10 row or other file maintain; e.g., `> Platform map → {workflows_root}CLAUDE.md §Platform directory map` |

### L3 Capacity

Row reference see main spec §Capacity (L3 row); route-hub type see exception. Over when judge overflow: route-table swell → group or split; content surface → sink fix.

### L3 Domain Extension Area

⚪ Optional. Standard chapter not all domain-specific content put here.

- ✅ Must after all standard chapter; use `---` separate.
- ✅ Must use `## Domain Extension` title; below free organize.
- ❌ Prohibit put global rule, other domain info, implementation.
- ⚪ Can include: domain-only map, category, flow, pattern quick-lookup etc.

---

## L4 Subdomain CLAUDE.md

> Second-level directory (first-level down first layer sub-directory) `CLAUDE.md` authoring spec.

### L4 Positioning

L4 is library's **subdomain index**. Agent jump L3 to certain second-level directory; read L4 get that subdomain file checklist or deeper subdirectory navigate.

L4 answer core question: **This subdomain what file or subdirectory; each what**.

### L4 Design Philosophy

- **Concise priority**: L4 one-two hop from leaf; content should more concise L3.
- **Pure index**: L4 core job list file + subdirectory; not add operation guide; not add tutorial.
- **Trigger complete**: L4 Agent decide read which concrete file final route hop; trigger need precise cover.
- **Not repeat parent**: L3 already introduce domain position; L4 not repeat.

### L4 Organization Framework

L4 ✅ must organize per order:

| # | Chapter | Required | Explanation |
|---|------|:----:|------|
| ① | One-line position | ✅ | `>` quote |
| ② | Subdirectory Index | ⚪ | When has ✅ |
| ③ | File Index | ⚪ | Direct contain file when ✅ |
| ④ | Shortcut Guide | ⚪ | Only file ≥10 and high-freq scenario |
| ⑤ | Agent Behavior | ⚪ | Only Agent need special behavior |
| ⑥ | Changelog | ⚪ | Follow `naming/kb-file-structure-metadata.md` §1.1 |

### L4 Per-Chapter Detail

#### ① One-Line Position

✅ Use `>` quote. More specific than L3—say this subdomain in parent domain what role.

```markdown
# identity/

> Brand core identity element: position, voice, expertise, experience, vision, role, business model.
```

#### ② Subdirectory Index

⚪ Has ✅ must. Format L3 same but more concise—usually two column (directory/content) ok. ❌ Prohibit structure count (see `kb-entry-antipattern-archiving.md` § antipattern - structure-count).

```markdown
## Subdirectory Index

| Directory | Content |
|------|------|
| {tool_A}/ | Config  -  instruction  -  agent  -  hook  -  MCP  -  optimize |
| {tool_B}/ | Architect  -  debug  -  benchmark |
```

⚪ Trigger column: if subdirectory clear trigger scene add; else skip.

#### ③ File Index

⚪ Directory direct contain file ✅ must. Standard two column:

```markdown
## File Index

| File | Explanation |
|------|------|
| position.md | Value + red line + persona base |
| expression-style.md | Voice define + catchphrase + ban word (must read before create) |
```

⚪ Can note load timing in explanation (e.g., "must read before create"); help Agent judge immediate-read need.

#### ④ Shortcut Guide

⚪ Only file ≥10 and high-freq scenario need. Most L4 not—file index enough.

#### ⑤ Agent Behavior Directive

⚪ When Agent in subdomain need special behavior use.

```markdown
## Agent Behavior Directive

- **When directly create**: Must read position.md + expression-style.md + platform style
- **When create via Skill**: Skill load own context; Agent only pass param
```

❌ Prohibit put global behavior rule—belong L2.

#### ⑥ Changelog

⚪ Subdomain significant change add. See main spec §Changelog Convention.

### L4 Dual-Identity Exception (Operations Asset Type)

⚪ When L4 subdomain **itself operations asset** (e.g., `{business_root}{brand}/{business_type}/`—video channel, website, course workspace etc.); its `CLAUDE.md` allow dual role:

| Role | Content | Place |
|------|------|------|
| **L4 Subdomain Index** (primary) | Subdirectory/file index + trigger | Body |
| **Operations Asset Archive** (attach) | 6 Facet metadata + source mutual-refer + key attribute | Top |

#### Compliance Boundary

- ✅ Top metadata + source mutual-refer ≤30 row.
- ✅ Body maintain L4 index job (subdirectory/file/trigger).
- ✅ Total capacity per main spec §Capacity dual-identity budget.
- ❌ Over-budget long-tail (operations fact, schedule, log, tech detail) sink independent file.
- ❌ Prohibit copy spec body—spec rule only one-line pointer.

#### Judge Standard

| Scenario | Use Dual-Identity | Use Pure L4 + Independent Asset |
|------|:-------:|:--------------------:|
| Directory is asset; subdirectory ≤10 | ✅ | ❌ |
| Directory is asset; subdirectory >10 and maintain log frequent | ❌ | ✅ |
| Directory not asset | ❌ (use pure L4) | ❌ |

### L4 Over-Large Index Exception

When subdirectory quantity large (about ≥50; e.g., tool register center, best-practice collection); pure directory list self exceed L4 reference.

| Constraint | Value |
|------|-----|
| Capacity | Per need break; but content must pure index—per-line only directory name + one-line explanation |
| Operation Guide | ❌ Not allow—volume already large; operation leave L3 |

### L4 Domain Intake Area

Workflow entry, spec directory entry etc. domain-intake L4; chapter and capacity per intake spec—intake relation see main spec §Domain Intake Registration; this don't repeat enumerate.

### L4 Level Choose

Count from first-level down:

| Directory Depth | Use Layer |
|---------|---------|
| First level | L3 |
| Second level | **L4** |
| Third+ level | L5+ |

Not by file content quantity; by directory depth.

### L4 De-Duplication Principle

| Info Type | L3 Have | L4 Put What |
|------|--------|----------|
| Subdirectory overview | One-line description | Expand to file-checklist or sub-subdirectory |
| Trigger | Subdomain level | File level (more granular) |
| Usage note | Operation guide/quick-start | Not repeat; if need point back |
| Domain rule | L3 domain rule chapter | Not repeat |

**Judge standard**: L4 only put L3 not expand detail. If L3 already list some info; L4 use pointer not copy.

### L4 Build or Not

| Condition | Build or Not |
|------|-------|
| Directory has 3+ file | ✅ Build |
| Directory has subdirectory | ✅ Build |
| Directory only 1-2 file | ❌ Not build; L3 file index cover |
| Directory only one `CLAUDE.md` (self-ref) | ❌ Not build |

### L4 Domain Extension Area

⚪ Optional. L4 extend lighter L3—only subdomain-unique, can't go file-index reference info.

- ✅ Must after file index; use `---` separate.
- ✅ Must use `## Domain Extension` title.
- ❌ Prohibit put operation guide or flow (belong L3).

---

## L5+ Deep CLAUDE.md

> Third+ level directory `CLAUDE.md` authoring spec. No fixed depth limit—directory any deep; long as need index apply.

### L5+ Positioning

L5+ cover third+ all directory. Not "last hop"—**recursively apply** rule: regardless directory level 4 or 12; long as not L3 (first level) or L4 (second level); use this section.

L5+ answer core question: **What file or subdirectory here; each what**.

### Why Not L6/L7/L8

Directory depth not decide write method; layer number not bind depth:

1. **Depth not format**—same deep competitor analyze directory and source directory; write complete different. Decide `CLAUDE.md` how write is directory **functional type**; not it which level.
2. **Fixed number decay**—per-level add one L number; spec itself swell fail. 
3. **Recurse better enumerate**—L5+ rule recursively use all deep directory. Type need diff when; per **functional classify** not layer number distinguish.

### L5+ Functional Classify (By Directory Type Dynamic Adapt)

L5+ directory per function classify. Different type follow different rule. Judge way: look directory **hold what**; not it which level.

| Type | Judge Standard | `CLAUDE.md` Rule | Typical Scenario |
|------|---------|---------------|---------|
| **Index Type** | Directory hold knowledge file or sub-directory; need route navigate | Minimal: position + file/sub-index | Most knowledge directory, competitor-analyze tree, topic resource layer, style platform index |
| **Functional Type** | Directory core job define one entity; `CLAUDE.md` carry entity-define | Allow expand: position + entity-define (capacity see main spec §Capacity) | Role define, brand dimension (version), style package define, operations territory job-declare, project function map |
| **Archive Type** | Directory with single delivery or operation instance one-one correspond; `CLAUDE.md` carry structure-state metadata | State table-head + file index (capacity see main spec §Capacity) | Article directory card, course unit card, batch snapshot, run-data entry |
| **Project Type** | Directory code project or contain engineering config; `CLAUDE.md` from project-self | Follow project-self spec; this spec not intervene | Source directory, repo-clone |
| **Template Type** | 10+ same-structure sibling directory; workflow batch-generate; content one-write then mostly immutable | Minimal: position + file index; prohibit stuff data-summary | Collect data-card, auto-generate directory-index, date-partition run-record |
| *(Exclude)* | External-embed—locate `raw/`, `node_modules/`, or `.archive/` in outside repo-clone `CLAUDE.md` | Not classify; Agent shouldn't treat knowledge-spec | Research material capture outside repo; third-party package |

#### Archive Type Detail

Archive type middle-state between index and template: like template batch-exist; like index each instance metadata value differ and lifecycle-change.

**Allow content**:

- Structure state table-head—publish state, brand, slug, wordcount etc. key-value
- Platform sync full-view table—per-row one platform; state/file/link column
- Subdirectory and file index-table
- Key-file pointer section—main-file, raw, recheck-report etc. shortcut
- Metadata truth-source declare—mark source-of-truth where

**Prohibit**:

- >10 line analysis narrative—put independent `.md`
- Data-table—ranking, traffic-statistic put independent data-file
- Operation guide—flow put parent or workflow

#### Judge Flow

```text
Locate in raw/ / node_modules/ / .archive/ inside external repo-clone?
  → Yes: Exclude; not classify

Directory contain package.json / pyproject.toml / setup.py / Cargo.toml?
  → Yes: Project type; follow project-self spec

`CLAUDE.md` body mainly entity-define (role/brand-dimension/style-pkg/asset-lib/product-spec)?
  → Yes: Functional type (capacity see main spec §Capacity)

`CLAUDE.md` contain structure-state table-head (publish-state/platform-sync-view/metadata-source-declare one)?
  → Yes: Archive type (capacity see main spec §Capacity)

10+ same-structure sibling directory; content one-generate mostly not-change?
  → Yes: Template type; minimal + prohibit data-summary

Match above none → Index type (default); minimal
```

### L5+ Design Philosophy

- **Minimal default**: Index and template only position + file-list.
- **Per-need relax**: Functional allow carry entity-define; archive allow state metadata; project follow self-spec.
- **External exclude**: Non-library produce `CLAUDE.md` (outside repo, third-party package) not classify.
- **Build threshold**: Not every directory need `CLAUDE.md`; file ≤2 not build; data-corpus and batch-output area use naming-navigate (main spec §Four Law - exception).
- **Recursively apply**: This section rule apply level 3 to any-depth directory.

### L5+ Organization Framework

L5+ ✅ must organize; **only these chapter**:

| # | Chapter | Required | Explanation |
|---|------|:----:|------|
| ① | One-line position | ✅ | `>` quote |
| ② | File Index | ✅ | All this-directory file-list |

⚪ If directory still have sub-directory; add sub-directory index. But review whether depth too deep—exceed 4 usually means need reorganize.

#### Changelog: Default Prohibit + Domain Special License

❌ L5+ default prohibit `## Changelog` section—leaf pure-list; file-level change walk version-control log.

✅ **Special License**: Directory hit main spec §Domain Intake Registration; and domain-spec explicit allow or request changelog (e.g., tool best-practice entry, dashboard role, commerce-output directory) → follow domain-spec.

### L5+ Per-Chapter Detail

#### ① One-Line Position

✅ One line explain what-type content this directory hold.

```markdown
# {tool_name}/

> {tool_name}'s config, instruction-file, agent, hook, MCP, optimize best-practice.
```

#### ② File Index

✅ List all file; per-file one-line explain. Standard two-column:

```markdown
## File Index

| File | Explanation |
|------|------|
| case-001.md | Tutorial tweet example |
| case-002.md | Real-world share example |
```

**Large directory (20+ file)**: ⚪ Can group per sub-topic (`###` sub-section; per-group one two-column table).

❌ Prohibit >one-line description per-file. If need detail; belong file self content.

### L5+ Build or Not

| Condition | Build or Not |
|------|-------|
| Knowledge-navigate-area directory 3+ file | ✅ Build |
| Directory contain subdirectory need route | ✅ Build |
| Directory only 1-2 file | ❌ Not build; parent index cover |
| Data-corpus/batch-output-area (name-navigate) | ❌ Not build (main spec §Four Law - exception) |
| Directory depth ≥5 layer | ⚠️ Review if need-reorganize |

### L5+ Functional Type Exception

When directory core job **define one entity** (role, project, product) not index-file; that `CLAUDE.md` not L5+ minimal constraint.

**Judge**: `CLAUDE.md` body mainly entity-define (role-persona, project-target, product-spec) not file-list → functional type.

| Handle Method | When-Use |
|---------|---------|
| Write per L3 standard | Directory only one `CLAUDE.md` carry all-define; no other file separate |
| Split `CLAUDE.md` (index) + independent `.md` (define) | Directory simultaneously contain define + other-file—**recommend** |

Functional type capacity hard-line see main spec §Capacity. Over line when pull separatable content (operations-handbook, tool-chain detail) split independent file.

### L5+ Domain Extension Area

⚪ Optional. L5+ rarely need extend.

- ✅ Must after file-index; use `---` separate.
- ✅ Extend ≤10 line.
- ✅ Only gather meta, stat summary, traceability (symlink-source, internal-copy source-truth-path, core-stance declare).
- ❌ Prohibit put rule, tutorial, operation, tech-doc—all migrate independent `.md`.
- ❌ Prohibit put data-table (ranking-type)—belong independent data-file.
