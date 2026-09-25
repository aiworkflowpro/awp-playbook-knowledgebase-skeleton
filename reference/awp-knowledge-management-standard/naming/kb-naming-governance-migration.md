---
document_id: awp-knowledge-management-standard/naming/kb-naming-governance-migration
language: en
publication: public
title: "Naming Governance and Migration Specification"
purpose: Constrain investigation, mapping, execution, and acceptance flow for directory-level batch renaming
category: General Specification
---

# Naming Governance and Migration Specification

> Scope: For directory-level cleanup tasks, constrain how Agent establishes naming contracts for folders, documents, real assets, code files, and generated objects.  
> This specification doesn't prescribe single naming format; only process: discovery, consultation, mapping, execution, acceptance. Target format see `kb-naming-segment-convention.md`.

---

## Positioning

This specification solves the problem: when file/folder names and document names mix, how does Agent identify the directory context first, then deliver executable naming governance plan.

This specification is not a single filename template. Specific naming rules must come from these sources, loaded by priority:

1. Target directory and parent-level `CLAUDE.md`
2. From `{specs_root}CLAUDE.md` coverage matrix pointing domain-specific specification
3. Stable naming patterns in sibling directories
4. High-quality samples already in target directory
5. User-confirmed naming contract for this round

❌ Never hardcode one naming formula in workflow/script then apply uniformly across all directories.

---

## Applicable Scope

| Object | Applies? | Processing |
|--------|:--------:|------------|
| Folder | ✅ | Read folder responsibility first, then use short-semantic name or domain-spec-required structure name |
| Admin Document | ✅ | Can apply four-segment document naming by directory declaration |
| Knowledge `.md` Document | ✅ | Handle by domain specification and file structure spec |
| `.doc/.docx/.pdf/.txt/.csv/.json/.yaml/.xlsx` | ✅ | First determine if admin doc, source material, or tool output |
| Real Asset | ⚪ | Only rename when target directory rules explicitly require, e.g., book ID, image asset ID |
| Code File | ⚪ | Default follow project language and tool specs, not knowledge base document naming |
| Fixed Entry | ❌ | `CLAUDE.md`, `README.md`, `SKILL.md`, `manifest.json` fixed names don't change |
| Runtime Output | ⚪ | `runs/`, `logs/`, cache prioritize relocation, not renaming |

---

## Core Concept: Naming Contract

Naming contract is short document formed before directory cleanup and confirmed by user. It answers 6 questions:

| Question | Must Include |
|----------|------------|
| Governance Scope | Target directory, whether recursive, which extensions included |
| Classification Boundary | How to distinguish folders, admin docs, real assets, code files, runtime outputs |
| Rules Source | Which `CLAUDE.md`, specifications, sibling samples read |
| Naming Strategy | Which specification or contract each object type uses |
| Exempt Objects | Fixed entries, external names, unchangeable objects |
| Risk Handling | Conflicts, duplicates, link updates, rollback method |

✅ Must form naming contract as checklist before any real rename, present to user for confirmation.  
❌ Without user confirmation, only generate plan and dry-run, no `mv` execution.

---

## Sibling Sample Research

Naming proposal must reference sibling directories, not target directory alone.

Minimum research set:

1. Current level files and folders in target directory
2. 3-5 similar sibling directories
3. Parent-level `CLAUDE.md` directory responsibility and routing
4. Target directory's own `CLAUDE.md`, if exists
5. Naming chapter in domain specification

Research output must include:

```text
Sample Source | Observed Pattern | Adopt? | Why
```

---

## Classification Decision

Agent must classify before naming.

| Classification | Decision Basis | Common Strategy |
|--------|---------|----------|
| Fixed Entry | Filename hardcoded by tool or Agent | Keep original |
| Folder | Responsible for classification, phase, batch, archive | Short-semantic name; if needed per domain spec |
| Admin Document | Report, checklist, plan, index, cache, log | Can enable four-segment doc naming |
| Knowledge Document | Long-read reusable `.md` | Per domain spec and file structure spec |
| Real Asset | Book, image, video, data source, download | By asset ID or retain original identity |
| Code File | `.py/.ts/.sh` etc. | Per project code spec |
| Temporary Output | cache, tmp, runs, logs | Relocate, retain or clean needs separate confirmation |

---

## Migration Process

1. Load directory context: read current and parent-level `CLAUDE.md`.
2. Locate domain specification: find corresponding spec from `{specs_root}CLAUDE.md`.
3. Inventory filesystem: generate target directory inventory.
4. Sibling research: summarize neighboring directory patterns.
5. Classify objects: mark fixed entries, folders, admin docs, real assets.
6. Generate naming contract: provide each object type naming strategy and exemptions.
7. User confirmation: get explicit confirmation before renaming.
8. Generate rename mapping: include old path, new path, classification, rule source, reason.
9. Dry-run: check conflicts, overwrites, case collisions, link impact.
10. Execute rename: prioritize reversible, re-verifiable commands.
11. Sync references: update `CLAUDE.md`, indexes, reports, cross-references, then scan "Seven Post-Rename Locations" once per type.
12. Acceptance: check old-name residuals, link validity, count consistency, encoding and format anomalies; output generator runs once after fixes, confirm old directory won't auto-recreate.

---

## Rename Mapping Table

Mapping table fields:

```text
Old Path | New Path | Object Class | Rule Source | Rename Reason | Risk Level | Execute?
```

✅ Mapping table must exist before rename.  
✅ Save mapping to target directory admin area or this run's `{run_output_root}/{run_id}/output/`.  
❌ Never batch rename without mapping table.

---

## Seven Locations to Scan After Rename

`grep` with backtick-wrapped paths covers only small part of references. Below seven types are "miss = break", scan each type after rename, **leave record for each type: "scanned, hit N entries"**—writing "globally replaced" doesn't count.

| # | Type | Specific Locations | Miss Consequence |
|:-:|------|---------|-----------|
| 1 | Path string constant in code | `"{top-level}/..."` format literal, path-concat function, path dictionary | Runtime writes output to wrong location, **no error** |
| 2 | Document title self-reference | File one-level title, `WORKFLOW.md:1`, step-file title with old number | Reader follows title to find, can't |
| 3 | Function docstring and code comment | Module/function docstring (docstring), `#` comment with path | Next person editing code follows comment wrong |
| 4 | Metadata field | `manifest.yaml` `provenance`, audit script exemption list, registry `path` field | Exemption list exempts old path, doesn't exempt new, check backwards |
| 5 | Renamed object's own identity field | `SKILL.md` `name`, `manifest.yaml` `id`, `package.json` `name`, `settings.json` keys named by it | Directory renamed but identity unchanged, misaligned |
| 6 | Runtime-loaded config | `config/*.yaml`, `argparse` `default=`, env var default | Same as 1, silent wrong place |
| 7 | Renamed directory **internal** self-reference | Directory-internal `.json` / `.md` with its absolute path | External reference scan won't find—it's inside renamed dir |

**Common trait matters more than individual form**: These seven all unquoted, not in Markdown body, machine-check doesn't catch them, **silent failure—wrong action, not stop**. Classic case: path constant guard check `parent.exists()` passes, so it quietly creates wrong file next to correct one.

**Reusable Query**: Extract all `"{top-level}/..."` string constants from code check each `Path.exists()`. False positives only three types—easy to exclude: error message, template placeholder, test fixture.

### Rename Triple-Check

Rename impact spreads three directions; skip any one and it recurs:

1. **Check External References**—paths outside pointing to renamed object. This is only direction regular `grep` covers
2. **Check Internal Self-Reference**—renamed directory-internal files with their pre-rename paths (Type 7)
3. **Check Output-Generation Code**—who generates these names. See next section

### Only Rename Document, Not Output Generator; Fix Gets Auto-Reverted

**Criterion: This round rename "directory structure" or "filenames"? If yes, must find output generator simultaneously.** Output generator has four types: script  -  workflow step file  -  scheduled task prompt  -  audit script exemption list. Document rename alone is manual docstring update; output generator unchanged still produces old-style. 

**Common root is second level.** Example case: directory renamed, six path locations fixed; six minutes later directory recreates by code's `mkdir(parents=True, exist_ok=True)`. First level: five hardcoded paths; second level: root cause `mkdir` inside path-calculation function, and nine callers all import-time call it, **running `--help` rebuilds directory**. Fix method: remove `mkdir`, pure path calc, actual write-point each builds. 

**Check completion: after fix, run named module's any command once, watch directory/file auto-return**. Returns = incomplete.

### Batch Replace Safe Posture

| Method | Why |
|--------|-----|
| Use full context string, not bare keyword | Entire vault may have multiple same-name different-meaning values; bare replace kills unrelated ones |
| Line-start anchor + full-line exact match + scope limit | `sed 's/^status: done$/status: completed/'` scoped to dir won't kill shell loop's `done` terminator |
| Replace complete filename string, not pattern | Fullname unique across vault, meaning consistent in-out |
| Placeholder replace use whitelist, not pattern match | Pattern match kills template syntax (e.g. `{{range .Mounts}}`) |
| Multiple regex merge match at once, not serial | Serial later consumes former's output, generates corrupt string |
| Pre-rename distinguish "path" and "same-name config value" | One word maybe both directory name and sync tool's folder ID; misreplace needs rollback |

**Code Fence** (``` wrapped block) **skip behavior differs**: detector & replacer not same. Link **detection** must skip fence, else teaching example path falsely reported; **replace** using "verified old → new exact string" fence safe both ways. Fences often just layout (directory tree, diagram, evidence block) but hold real reference not example.

### "Don't Alter History Area" Really Means Content, Not Path

Same month-partitioned directory may hold true history (`.log`, complete run dir) and **executable pending instruction**. Path judgment makes live executable look dead; skip.

**Judge by content, not path**: Same directory contain `.sh` / `.py` / Agent-consumable instruction file?—Yes = live must rename together. Conversely, only `.md` record, no run script, no external reference, all vault import none = completion record don't touch.

### Concurrent Rename Dependency Conflict

Multiple parties editing same area simultaneously: A moves file, B scan-by-startup-snapshot, file not in old spot—both think covered, actually middle batch uncovered.

**Rule**: Batch rename sync range must include **this round's other executor-moved directory**, not just starting-snapshot. Before starting, confirm no other party moving same area this round.

---

## User Confirmation Template

```markdown
This round's naming contract below; confirm before real rename:

1. Governance Scope: {target_path}
2. Folder Strategy: {folder_strategy}
3. Document Strategy: {document_strategy}
4. Real Asset Strategy: {asset_strategy}
5. Fixed Entry Exemptions: {fixed_entry_exemptions}
6. Predicted Renames: {rename_count} items
7. Risk: {risk_summary}

Reply "Confirm execute" to continue; unconfirmed stays plan-only.
```

---

## Acceptance Checklist

- [ ] Target directory and parent `CLAUDE.md` read
- [ ] Domain specification located and referenced
- [ ] Sibling samples researched
- [ ] Object classification complete
- [ ] Naming contract confirmed by user
- [ ] Rename mapping table saved
- [ ] Dry-run no conflicts
- [ ] Real rename complete; indexes and cross-references synced
- [ ] Seven location types scanned each, hit count recorded (including 0)
- [ ] Internal self-reference checked (directory internal to itself)
- [ ] Output generator located and fixed; run once, old directory/file didn't auto-recreate
- [ ] History area judged by content not path
- [ ] Old-path residuals exist only in mapping table or history report
- [ ] File count and classification stats match before-after

---

## Relationships with Other Specifications

| Related Specification | Relationship |
|----------------------|-------------|
| `kb-naming-segment-convention.md` | Complementary—that manages "filename should look like", this manages "how to migrate" |
| `kb-file-structure-metadata.md` | File internal structure and metadata constraints after rename |
| `kb-document-identity-revision.md` | Specification doc rename/move must preserve `document_id` |
| `../directory/kb-directory-decision-composition.md` | Structural adjustment first by directory pattern decision tree, then this migration spec |
| `../directory/kb-directory-pattern-registry.md` | Look up registered list of directory organization patterns |

---

## Change Log

> Rolling window, retain last 3 entries, ≤20 characters each.

| Date | Content |
|------|---------|
| 2026-08-07 | Merged into naming dimension and generalized |
