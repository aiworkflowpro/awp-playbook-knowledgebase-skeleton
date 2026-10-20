---
document_id: awp-knowledge-management-standard/directory/kb-entry-multiagent-compatibility
language: en
publication: public
title: "CLAUDE.md Multi-Framework Compatibility Specification"
---

# CLAUDE.md Multi-Framework Compatibility Specification

> Scope: How one library routing system distributes to all in-use Agent frameworks—source where, mirror use what mechanism, new framework how join.
> Out of scope: Layer structure itself (→ `kb-entry-authoring-standard.md` and `kb-entry-layer-levels.md`).
> This document is **sole source of truth** for multi-framework instruction-file topic—main spec and layer detail only point; not repeat.

---

## Positioning

Library read by multiple Agent framework simultaneously; each framework has own instruction-file name and discover mechanism. This spec answer: **How `CLAUDE.md` system let any framework read same routing; not maintain second content for any framework**.

Design two layers: **Principle Layer** (stable; not change with framework rotation) + **Framework Registry** (state register; add/drop framework only change table; principle not move).

---

## Design Philosophy

- **Single Source**: Library structure and rule per `CLAUDE.md` as source; other file distributed from source.
- **One Chain Multi-Use**: Shareable mirror absolutely not build per-framework separate—root one symlink serve all same-class framework.
- **Same-Content Soft-Link; Different-Content Independent**: Mirror and source identical must symlink (physically impossible drift); input-content framework-differ independent write; belong domain spec.
- **State and Rule Separate**: In-use framework checklist is registry not clause; spec hardcode framework name necessarily decay.
- **Compatibility Minimize**: Only patch file-map and load-difference; not backward-pollute layer spec with framework detail.

---

## Principle Layer

### ① Source Unique

✅ Library structure, rule, routing per `CLAUDE.md` system as sole source. Framework mirror state difference; source correct.
❌ Prohibit invent independent layer-system for any framework or second content.

### ② Root One Chain Multi-Use

✅ Library root maintain one symlink `AGENTS.md → CLAUDE.md`; serve all read `AGENTS.md` framework.
❌ Prohibit separate mirror for read-same-name multi-framework.
⚪ Framework native file-name not `AGENTS.md` and cannot configure compatible; only then at root add symlink (register to framework-registry).

### ③ Same-Content Soft-Link; Different-Content Independent

| Scenario | Mechanism | Why |
|------|------|------|
| Mirror and source identical | ✅ Symlink | Same inode; change once all-framework effect; not drift |
| Input-content framework-differ (e.g., workflow different framework thin-entry) | ✅ Independent write true-file | Soft-link can't express diff; same-diff boundary and sync-rule belong domain-spec |

❌ Prohibit "copy then manual-sync" maintain same-content mirror—will drift; two-legal-mechanism no-third.

### ④ Deep Entry Domain Spec Rule

For a deep library directory (e.g., `{workflows_root}*/`) and for a domain intake area outside the library (such as a `{tool_repository_root}` package or service), the domain standard decides whether a framework-exclusive entry file is needed, what goes in it, and how it stays in sync with `CLAUDE.md`. See `kb-entry-authoring-standard.md § Domain Intake Registration`; the source of truth for the workflow dual entry is the entry chapter of the Agent Workflow Authoring standard.

This spec only total principle: ✅ Deep entry is **thin entry** (point authority file not contain flow text); ❌ Unauthorized deep directory don't build framework-entry-file.

### ⑤ Global Layer Each Framework Autonomous

Each framework's global instruction-file (e.g., `~/.claude/CLAUDE.md`, `~/.codex/AGENTS.md`) per framework capability diff independent maintain; not force-unify.
⚪ Allow cross-framework soft-link reuse (one framework global-file link to another); condition content truly universal.

---

## Framework Registry

> **State register table**: records which frameworks are in use, what each one reads, and how it is wired in. Adding or dropping a framework changes this table only; the principles above do not move.

| Framework | Native Instruction File | Library Intake | Note |
|------|-------------|---------------|------|
| Claude Code (all provider instances) | `CLAUDE.md` system | Native: L0→L2→load-on-demand | Main system; this library L1 merge-into root `CLAUDE.md` single-file manage; host-rule into shared-source |
| Codex | `AGENTS.md` (global + git root to cwd ancestor chain) | Root symlink `AGENTS.md → CLAUDE.md` | Workflow deep separate thin-entry (domain-spec rule) |
| Cursor | `AGENTS.md` + `.cursor/rules/` | Reuse root same-symlink | Rule directory per-need separate config |
| Grok | `~/.grok/` global; then git-repo walk root→cwd per-level; **non-git-repo only cwd one-level scan**. File-name recognize `AGENTS.md`/`AGENT.md`/`Agents.md`/`Claude.md`; single-file ≤10K char | Reuse root same-symlink; plus `~/.grok/AGENTS.md` global-rule | ⚠️ Neither library git-repo—Grok at subdirectory open-window read don't reach root; global-rule must write "read library-root `CLAUDE.md`" fill this hole |
| Antigravity | Global `~/.gemini/GEMINI.md` + workspace `.agents/rules/` | Global soft-link reuse Codex global-file | Workspace-rule per-need separate config |
| Cline | `.clinerules` file or `.clinerules/` directory at project root | Root add symlink `.clinerules → CLAUDE.md` | Native file name is not `AGENTS.md`; needs its own symlink under principle ② |
| Windsurf | `.windsurfrules` at project root; newer versions also read `.windsurf/rules/` | Root add symlink `.windsurfrules → CLAUDE.md` | Use the rules directory only when a directory needs its own extra rules |

**Maintain Rule**:

- ✅ To add a framework, follow the §New Framework Join Flow, then register one row here.
- ✅ When a framework is retired, delete its row and remove any symlink that served only that framework.
- ❌ Never hardcode a list of frameworks anywhere in this standard except this table.

### Language Style Distribute Point

Language style is the **one rule that must land in every framework's global layer**. It constrains every output, and the global layers do not see each other: a Claude Code output style is read by Claude Code alone, and no other framework reads a single character of it. The source is the language style rule in this knowledge base's authoring standard; the shared protocol is ASD-STE100 simplified technical English.

| Distribute Point | Serves | Carries |
|-------|---------|--------|
| `~/.claude/output-styles/{language-style-file}.md` | Every Claude Code instance | Always-on execution layer; the minimum executable rule set |
| `~/.claude/CLAUDE.md` | Claude Code, every project on this machine | Global user memory; one line stating the language rule |
| `~/.grok/AGENTS.md` | Every Grok window | Global rule; also contains "read the library root first" to close the cwd-scan hole |
| `~/.codex/AGENTS.md` (`~/.gemini/GEMINI.md` reuses it by symlink) | Codex and Antigravity | One line in the expression-constraint section |
| Library root `CLAUDE.md` (`AGENTS.md` symlink) | Shared source for every framework | The knowledge base protocol, written in STE style |

✅ When the language rule changes, change every distribution point in the same round, and keep the wording aligned with the source. ❌ Never change one point and assume it applies library-wide — no framework reads another framework's global layer.

---

## Layer Distribute Strategy

| Layer | Distribute | Explanation |
|:----:|---------|------|
| L0 Global | Each framework autonomous (⚪ can soft-link reuse) | Framework capability diff large; force-unify lose framework-unique config |
| L1 `.claude/` | Not distribute | Host-exclusive layer; should not other-framework (rare-framework active-read; careful content-boundary) |
| L2 Library Root | ✅ Symlink one-chain-multi-use | Only layer need mirror—multi-framework shared-source |
| L3–L5 Sub-Directory | Default not build | Exception: Domain-spec request deep thin-entry (principle ④) |

✅ Root true-source (via mirror read L2) must solo carry main-carrier job—not depend @expand-mechanism also provide complete-route (symlink straight to body; auto satisfy).

---

## New Framework Join Flow

```text
1. Find this framework's native-instruction file-name and discover-mechanism (global file? project root? ancestor chain? sub-dir scan?)
2. Native read AGENTS.md (or configurable compat)?
   → Yes: Zero action; existing root link direct work
   → No: Root add one {native_file_name} → CLAUDE.md symlink
3. Framework do deep sub-directory context scan?
   → Yes: Configure corresponding ignore (exclude node_modules/; cache; batch-output-area)
4. Global-layer per-need build this framework global-file (can soft-link reuse existing)
5. In §Framework Registry register one row; random sample-verify root-route readable
```

---

## Checklist

- [ ] `CLAUDE.md` is sole source; no framework hold split content
- [ ] Library root have `AGENTS.md → CLAUDE.md` symlink and point correct
- [ ] Same-content mirror all symlink; no "copy then manual-sync" true-file
- [ ] Differential input-entry (workflow dual-entry etc.) have domain-spec backup; and thin-entry
- [ ] Framework registry match real state (no exited-framework remaining-row; no unregister in-use-framework)
- [ ] Not hardcode framework-checklist outside registry in any clause
- [ ] Deep-scan-type framework already configure ignore-strategy
