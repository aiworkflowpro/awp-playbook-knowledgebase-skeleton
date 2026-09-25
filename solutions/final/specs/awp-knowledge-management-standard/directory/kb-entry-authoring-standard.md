---
document_id: awp-knowledge-management-standard/directory/kb-entry-authoring-standard
language: en
publication: public
title: "CLAUDE.md Authoring Standard"
---

# CLAUDE.md Authoring Standard

> Scope: The definition, laws, legal chapters, templates, capacity, and machine checks for every `CLAUDE.md` index file in the knowledge base.
> Out of scope: Layer-by-layer details (→ CLAUDE.md Layer Levels Detailed Explanation); how to fix mistakes (→ CLAUDE.md Antipatterns and Archive Governance); multi-framework distribution (→ CLAUDE.md Multi-Framework Compatibility Specification).
> In the knowledge base, `CLAUDE.md` is a **router**, not a knowledge container—it tells Agent "go find it", not "here's the answer".
> Read this before creating or modifying any `CLAUDE.md`.

---

## Positioning

Knowledge bases are not code repositories. A code project's `CLAUDE.md` answers "how to build/test/deploy"; a knowledge base's `CLAUDE.md` answers **"what's here, where to find, when to read"**.

Knowledge base `CLAUDE.md` is essentially a **file system-level routing table**—Agent enters any directory, read `CLAUDE.md` for navigation map, then deep-dive into specific files by task need.

```text
Agent enters directory → Read CLAUDE.md → Get navigation map → Deep-dive to specific file by task
```

---

## Design Philosophy

- **Router not container**: `CLAUDE.md` only carries navigation and rule entry points; complete content always in independent files.
- **Criteria not enumeration**: Constrain each layer's function; don't lock-down specific content lists. Enumeration-style clauses are snapshot of state; snapshots go stale; criteria-style clauses remain valid as state evolves.
- **Template not description**: Each layer specifies one real-world template file as spec. Templates never drift from state; prose does.
- **Explanation near use**: One constraint appears in **one** place—can write into deliverable itself or give to machine check; don't repeat in spec.
- **State separate from rule**: Changes (in-use framework, domain intake area) go to registration table; add/delete only changes table, not clauses.

---

## Four Laws

| Law | Judgment Standard |
|------|---------|
| **Route not storage** | `CLAUDE.md` only index and navigation; not complete content |
| **Navigable** | Agent locates file in any directory without guessing. Satisfy one of three: ① this directory has `CLAUDE.md` index; ② domain spec declares inferrable naming convention; ③ parent index directly covers (when files few) |
| **Current state only** | No body-text narrative sidebar; short facts end `## Deprecation Note` (`naming/kb-file-structure-metadata.md` §1.2); long cases → `{inbox_root}archive/` (see `kb-entry-antipattern-archiving.md`) |
| **Load-on-demand** | Child `CLAUDE.md` loads only when Agent accesses; doesn't consume upper context |

**Navigable law exceptions**: Data corpora, batch outputs, `{inbox_root}archive/`, external embeds (cloned repos, third-party packages) don't build per-directory indexes—these areas navigate by naming convention; per-directory index only produces thousands of unmaintained shells. Knowledge navigation areas (brand / tools / specifications / business knowledge layers) build per-directory indexes.

---

## Core Criterion: One-Sentence Self-Check

After writing any content segment, ask:

> **If we delete this line, can Agent still find this content?**

| Answer | Action |
|------|------|
| Yes—`ls` finds it, `--help` runs it, adjacent file already has it | ❌ Delete |
| Yes but cost obvious higher (jump three levels, run five commands) | ⚪ Keep; this is shortcut lane |
| No—unguessable constraint, pitfall, or personal preference | ✅ Keep; this is most valuable content |

The third category is all the reason `CLAUDE.md` exists: **physical constraints** (sync delay, cross-machine fetch method), **security boundary** (which operations not auto), **personal preference** (don't correct what, don't proactively mention what). Never delete any of these three.

---

## Controlled Chapter Table

`CLAUDE.md` legal chapters **only these**. Chapter name is semantic—name already says what it holds; no extra explanation needed. ❌ Prohibit custom chapter name variants.

| Chapter Name | Holds | Apply to |
|--------|-------|--------|
| (one-line positioning) | `>` quote block; one sentence says what this directory manages | All levels ✅ |
| `## Subdirectory Index` | Per subdirectory one line: directory / content / trigger words | When has subdirectories ✅ |
| `## File Index` | Files directly in this directory; one line per file explanation | When has files ✅ |
| `## Behavior Rules` | Behavior principles grouped by scenario | L2 ✅; L3 ⚪ (domain-specific only) |
| `## Tool Route` | MCP table + local tool route table | L2 ✅ |
| `## Tool Dependencies` | High-frequency tools in this domain: scenario / tool / form / example | L3 ⚪ |
| `## Direct Read Guide` | Trigger-word→path shortcuts; can cross levels | L2 ✅; L4 ⚪ |
| `## Operation Guide` | Quick start, command examples, usage flow | L3 ⚪ |
| `## Domain Extension` | Non-standard-chapter domain-specific content; end | L3 / L4 ⚪ |
| `## Changelog` | See §Changelog Convention below | See that section |

❌ **Index files don't write `## Metadata` table.** Metadata constraints knowledge files (see `naming/kb-file-structure-metadata.md` document header "Apply To"); not routing files. Index state and date shown by content itself and changelog; separate "dimension / brand / type / state / update" table only adds one more place to decay. Directory real status (skeleton incomplete, maintained, accumulating) goes in one-line positioning.

---

## Six-Layer System

| Layer | Location | Responsibility | Layer Details |
|:----:|------|------|---------|
| **L0** | `~/.claude/CLAUDE.md` | Cross-project constant layer (criteria-based admit) | `kb-entry-layer-levels.md § L0` |
| **L1** | `.claude/CLAUDE.md` | Identity entry + host-specific rules + @expand L2 | `kb-entry-layer-levels.md § L1` |
| **L2** | `CLAUDE.md` | Main carrier + multi-framework shared source | `kb-entry-layer-levels.md § L2` |
| **L3** | `{first-level}/CLAUDE.md` | Domain facade + subdirectory index | `kb-entry-layer-levels.md § L3` |
| **L4** | `{second-level}/CLAUDE.md` | Subdomain checklist + file index | `kb-entry-layer-levels.md § L4` |
| **L5+** | `{third+-level}/CLAUDE.md` | Deep index; functionally classify dynamic adapt | `kb-entry-layer-levels.md § L5+` |

```text
L0  Cross-project constant (auto-load)
L1  Identity + host-specific rules → @expand L2 (auto-load)
  L2 Main carrier → behavior+tool+navigation+shortcut (@expand load, multi-framework shared)
    L3 Domain index → first-level facade+navigation (load-on-demand)
      L4 Subdomain index → second-level file checklist (load-on-demand)
        L5+ Deep index → third+ level; recurse; functionally classify (load-on-demand)
```

**L5+ not numbered by depth** (no L6/L7/L8); by directory **functional type** dynamically adapt—index, functional, archive, project, template five categories plus external embed exclusion. Details see layer detail § L5+ functional classification.

**Detail level**: L2 detailed (must-load, prefer detailed); L3–L5 concise (load-on-demand).
Each layer only guides next level; don't skip levels to index—L2 direct read shortcuts exception; that's intentional shortcut.

---

## Template Files

Before writing any layer, open corresponding template; write following it. **Template takes precedence over this spec prose**: when conflict, template is correct; revise this spec.

| Layer | Template | Why Chosen |
|:----:|------|-----------|
| L0 | `~/.claude/CLAUDE.md` | Only instance; is baseline |
| L2 | `{source_vault_root}/CLAUDE.md` | Five functions complete; constraint vs. route clear |
| L3 | `{personal_root}CLAUDE.md` | Pure index; no content surfacing |
| L4 | `{tools_root}best-practice/CLAUDE.md` | File index + trigger words standard |
| L5+ | Any tool package `CLAUDE.md` in code repo | Tool entry functional pattern (in repo not library) |

Table updates after template changes—refers to path not snapshot.

---

## Domain Intake Registration Table

Some `CLAUDE.md` managed by domain-specific spec—chapters, capacity, entry file, changelog per domain spec; this spec family defers. Intake relationships **only listed here**; new domain intake = add row; no clause changes.

| Directory Pattern | Intake Spec | Intake Scope |
|---------|---------|---------|
| `{workflows_root}*/` (all sub-levels) | Agent Workflow Authoring standard | Entry chapters, capacity, `CLAUDE.md` and `AGENTS.md` dual entry, changelog |
| `{specs_root}*/` | Standard Authoring standard | Index four elements, metadata, changelog |
| `{tools_root}best-practice/*/` | `methodology/tools/` | Chapters, capacity, changelog special license |
| `{tool_repository_root}/` (CLI repo `packages/` and `services/`; outside library) | Agent Tool Authoring standard | Tool `CLAUDE.md` content, entry file, changelog special license |
| `{tools_root}credentials/` | `methodology/tools/` | Credential index structure, capacity |
| `{dashboard_root}*/` (role, project, operations, scheduling all) | `methodology/operations/` (project archives additionally follow the Product Development standard) | Each area `CLAUDE.md` structure, capacity, changelog special license |
| `{commerce_root}` (phase-output directory family) | `methodology/commerce/` | Output directory three-piece set, changelog special license |
| `{research_root}` (topic, material, discovery layer) | `methodology/research/` | Topic structure, material convention, auto-generate index, changelog special license |
| `{brand_root}{brand}/` (identity dimension directory) | `methodology/brand/` | Dimension define and version, changelog special license |
| `{business_root}{brand}/` (operations asset and archive level) | `methodology/business/` | Operations asset archive, 6 Facet metadata, changelog special license |
| Project-type directory (contains `package.json` / `pyproject.toml` etc. engineering config) | Project's own spec | All |

**Decision order**: Directory hit intake table → domain spec takes priority; miss → this spec family layer detail applies.

---

## Capacity

Row count not compliance standard; **complexity recovery trigger**. Use core criterion above to judge capacity; not row count.

| Object | Reference Line | Nature |
|------|-------|------|
| L0 | ≤15 rows | **Hard line**—every session fully load; cost real |
| L1 | ≤60 rows | Reference |
| L2 | ≤250 rows | Reference |
| L3 | ≤150 rows | Reference |
| L4 | ≤100 rows | Reference |
| L5+ functional / archive | ≤200 rows | Reference |
| L5+ index / template | Positioning + Checklist | Principle |
| Domain intake area | Defined by domain spec | Transfer |

**Over reference line what to do**: First judge content overflow vs. role naturally needs. Overflow → extract independent file; `CLAUDE.md` only pointer. Natural need (e.g., library-level routing hub) → record reason; no fix.

---

## Changelog Convention

Changelog format, row count, character count, etc. common constraints defined in `naming/kb-file-structure-metadata.md` §1.1. **Spec body doesn't repeat numbers**—constraints follow output-object; Agent sees them first-line when editing.

| Layer | Changelog |
|------|---------|
| L0 / L1 | ❌ None |
| L2 | ✅ Required; **rolling window ≤3 entries**—unified whole-library in `naming/kb-file-structure-metadata.md` §1.1 |
| L3 / L4 | ⚪ Optional |
| L5+ | ❌ Default prohibited; domain intake area per domain spec special license |

❌ **Don't externalize changelog to independent file.** One changelog swaps one new file; across thousand-plus `CLAUDE.md` trees becomes thousand-plus new files—savings lost to multi-level structure cost. Compress row count if needed.

**Large audit/health-check reports** ❌ prohibited inline. Archive to independent file; changelog leave one-line summary.

---

## Multi-Framework Instruction Files

Distribution principles and in-use framework registry defined by `kb-entry-multiagent-compatibility.md`; that sole source of truth.

One-line: `CLAUDE.md` sole source; identical content mirrors use symlinks (library `AGENTS.md → CLAUDE.md`); differential content entry (e.g., workflow dual entry) independent write; belong domain spec.

---

## Progressive Disclosure

```text
CLAUDE.md (map) → Agent pick route by task → Read specific file (territory)
```

Knowledge base naturally suits progressive disclosure—`CLAUDE.md` forms routing network chain; each hop only loads that layer index; don't pre-load below content.

**Applies not just directory tree but also single-file interior**: Detail needed only at actual use (some tool full command table, some handoff debug record), sink to independent file leave one-line pointer; better than stay original.

### @Reference Loading Behavior

`@file.md` re-read from disk (eager load) on session startup and every context compression; not lazy. This library **only use for L1 → L2 main expand**. ❌ Don't use to inject rule files—rules all inline in L2 behavior section.

Load-on-demand content use "read time" text guide; Agent decide when:

```markdown
### Database Schema — `docs/schema.md`
**Read when**: Modify data model
```

---

## Agent-Facing Authoring Technique

### Give Criteria; Not Hard Numbers

Model judgment enough; hard rules' misfire exceeds benefit. When criteria can self-check with rules; don't hardcode numbers.

```text
❌ Default don't write comments; at most one line
✅ Wrote code should read like surrounding code
```

Exception: Security boundary and physical constraint still hardcode—that's permission not taste; delete wrong once irreversible.

### Positive Directive Better than Negative

Agent follow "do X" higher rate than "don't do Y".

```text
❌ Don't use Redux
✅ State manage with Zustand; not Redux
```

### Trigger Words Cover Synonyms

Agent via keyword match decides load which directory; trigger words cover multiple ways users might express.

Write "persona, identity, voice, brand positioning, values" not just "identity".

### Use Interface Design Replace Examples

Examples box model in example-drawn space. Rather than three usage example; encode intent into naming and structure—`status` only `pending` / `in_progress` / `completed` three values; see enum know lifecycle.

---

## Antipatterns and Archive Governance

→ `kb-entry-antipattern-archiving.md` (read when hit)

---

## Machine Enforce Layer

Below machine-enforced by `{kb_cli} audit claude` script. Run after modify `CLAUDE.md` system.

| Check Item | Level |
|--------|------|
| Changelog row count / character / hint line | Violation |
| L5+ unauthorized changelog | Violation |
| Library root `AGENTS.md` symlink | Violation |
| L0 over hard line | Violation |
| L1–L5 over reference line | Warning (review content overflow) |
| Index suspected zombie entry | Warning |
| Knowledge navigation area index gap | Warning |
| Empty shell index | Warning |
| Index segment name not `subdirectory index` / `file index` | Warning |
| Structure count and tag cloud | Warning |
| Index cover gap (L2/L3/L4 direct child uncovered) | Warning |

❌ No per-line exception mark. Machine error report → fix content until really compliant—don't give "mark and skip" door. Machine misreport fix machine itself.

Prose clause conflicts machine check; prose takes precedence; revise machine—machine execute means not second source.

---

## Checklist

Spec family single checklist. Machine handles objective items; here only machine-unjudgeable:

- [ ] Hit §Domain Intake Registration Table; read domain spec first
- [ ] Wrote following §Template Files that layer
- [ ] Each paragraph pass §Core Criterion—no "delete and still find" content
- [ ] Chapter names all from §Controlled Chapter Table; no self-invented
- [ ] No complete content inline (route not storage)
- [ ] Three undeletable categories (physical / security / personal) not mistakenly deleted
- [ ] Parent `CLAUDE.md` updated reference
- [ ] Run `{kb_cli} audit claude`; no new violation this edit
