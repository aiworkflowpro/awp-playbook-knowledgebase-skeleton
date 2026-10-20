---
document_id: awp-knowledge-management-standard/directory/kb-entry-antipattern-archiving
language: en
publication: public
title: "CLAUDE.md Antipatterns and Archive Governance"
---

# CLAUDE.md Antipatterns and Archive Governance

> Scope: Dictionary of incorrect forms in the `CLAUDE.md` system, and handling rules for index references that remain after directories are merged, retired, or archived.
> Out of scope: How to write normally (→ `kb-entry-authoring-standard.md` and `kb-entry-layer-levels.md`).
> **When to read**: When fixing a malformed `CLAUDE.md`; when a directory is merged, retired, or archived. No need for daily new creation.

---

## Antipatterns

| Antipattern | Problem | Fix |
|--------|------|------|
| **Knowledge Container** | Complete tutorial / report / operation manual shoved into `CLAUDE.md` | Extract content to independent files, `CLAUDE.md` only leave index |
| **No Index Navigation Area** | Directory with 3+ files but has neither `CLAUDE.md` nor naming convention; Agent guesses | Add index or domain specification declares naming convention |
| **Cross-Level Index** | L2 directly indexes L5 file path | Each layer only references the next layer (L2 direct read exception) |
| **Information Redundancy** | Same table repeated in parent and child `CLAUDE.md` | Parent only lists directory name + one-line description; detailed table in child |
| **Multiple Views of Same Thing** | Coverage matrix, hierarchy tree, quick lookup, subdirectory index four tables describe same mapping | Define one as source of truth; others deleted or compressed to pointer |
| **Stale State** | Progress / status data outdated, not updated | Update corresponding `CLAUDE.md` immediately when file changes |
| **Role Confusion** | Index file mixed with operation guides or tutorials | Classify by layer responsibility; operation guides go in independent files |
| **No Trigger Words** | Agent doesn't know what scenario needs this directory | Subdirectory table add trigger word column |
| **Self-Evident Index** | Directory with only 1-2 files still builds `CLAUDE.md` | Don't build; parent file index covers |
| **Structure Count** | Index hardcodes "N total" exact count | Use nature description replacing count; let `ls` handle quantity |
| **Changelog Bloat** | Exceeds row count, character count, inline accident details | Compress per `naming/kb-file-structure-metadata.md` §1.1; detailed info goes to version control logs |
| **Changelog External** | Splits changelog into independent file to save load cost | Don't split—thousands of `CLAUDE.md` means thousands of new files. If compressing, compress row count |
| **`CLAUDE.md` as README** | Installation guide / run instructions / architecture docs in `CLAUDE.md` | Technical docs go to independent `README.md`; `CLAUDE.md` only points to it in file index |
| **`CLAUDE.md` as Data Summary** | Batch-generated `CLAUDE.md` stuffed with stats (rankings, account overview) | Data summaries go to independent data files; `CLAUDE.md` only leave positioning + file list |
| **Hardcoded Instance List** | Spec or index hardcodes "current N directories" specific list | Use dynamic description (e.g., "all first-level directories"); new directories auto-apply |
| **Zombie Archive Entries** | Strikethrough entries or links to non-existent directories remain in index | Handle per archive governance rules below |
| **Narrative Sidebar** | Long paragraphs in body about "decommissioned path / old mapping / ~~strikethrough~~ / historical don't use" for Agent to load every time | Body only current state; short facts write end `## Deprecation Note` (≤3 items / ≤20 chars, before changelog); long cases migrate to `{inbox_root}archive/`; ledger max status column one word |
| **Implementation Detail Surfacing** | L3 describes Skill or tool internal flow logic | Sink to corresponding development spec or source code |
| **Runtime State Surfacing** | Version numbers, operational data snapshots in L3 | Sink to independent ledger file; L3 leave pointer |
| **Global Rules Sinking** | Global principles placed in some L3 | Surface to L2 behavior rules |
| **Island Domain** | Task needs two domains working together but no cross-reference | Add pointer in primary domain L3 to related domain |
| **Peer Information Duplication** | Same mapping table written in two L3s | Define one as source of truth; other use pointer |
| **Overlong File Index** | 5+ lines description per file | File index table one line per file explanation |
| **Repeated Parent Positioning** | Child layer re-explains what parent domain is | One-line positioning only says role in this layer |
| **Over-Nesting** | 5+ layers every level has `CLAUDE.md` | Reorganize directory structure, reduce levels |

---

## Archive Governance

After a directory is merged, retired, or archived, `CLAUDE.md` leaves residual references. If not cleaned up they become zombies—Agent reads an entry pointing to non-existent directory, cannot route nor decide to ignore.

### Must Do When Archive Occurs

| Action | Explanation |
|------|------|
| **Delete index entries** | Remove the directory row from parent `CLAUDE.md` subdirectory index |
| **Delete task route entries** | Remove routes pointing to this directory from operation guide / task route tables |
| **Delete strikethrough entries** | `~~old_name~~ → merged into new_name` writing style forbidden to keep. Merge relationship noted in new directory `CLAUDE.md`, not parent sidebar |

### Three Legitimate Archive References

| Type | Example | Keep Where |
|------|------|---------|
| **Historical Mapping Source of Truth** | Old brand → new attribution mapping | Unique library source of truth; streamline to brand name + new attribution + archive month; don't expand narrative |
| **Retirement Declaration** | Old spec retired; judgments internalized to workflow | `{specs_root}` retired spec section; mark "don't reference as active spec" |
| **Reference Pointer** | Some feature implementation logic can reference archived version | Active workflow task route one-line pointer; mark "reference" not "entry" |

### Prohibited Archive Writing

- ❌ **Strikethrough Sidebar**: `| ~~old_workflow~~ | → archived | — |`—delete, don't keep.
- ❌ **Narrative Sidebar**: In active index start or mid-body pile "was X → retired → full archive path → don't use"—Agent loads noise every time; short facts go to `## Deprecation Note`, long docs migrate to archive, body only shows current state.
- ❌ **Archive Narrative**: 3-5 lines describing archive circumstances—compress to deprecation note one line (≤20 chars) or migrate to archive.
- ❌ **Archive Full Path in Multiple Places**: At most in **single** ledger or archive explanation write `{inbox_root}archive/{YYYYMM}/...`; active `CLAUDE.md` don't repeat for everyone.
- ❌ **Multiple Repetition**: Same archive mapping table in two L3s—define one source of truth; others use pointer.

> **Term**: **Narrative Sidebar** = discarded passages, old paths, strikethrough archaeology mid-body (prohibited). Legal landing: `## Deprecation Note` (short facts) or `{inbox_root}archive/` (long text). ≠ ledger "status column" write decommissioned or discontinued (that's current-state field). ≠ `## Changelog` (only this file operations).

### Exception: Date-Stamped Point Snapshots

One class of file has date stamp in name; content records "how it looked that day"; written once then immutable; versions stack into timeline. These files writing "what changed in this version vs. last" is analysis conclusion itself, not sidebar—delete would falsify history.

One-sentence criterion: **Is this file "today's rule" or "observation from that day"?** Observation, keep version comparison.

| | Original includes history (❌ prohibited) | Snapshot does version comparison (✅ allowed) |
|--|--------------------------|---------------------------|
| File nature | Live document; changeable; library only has one | Point snapshot; immutable; stacks one-version-per-file timeline |
| What's this sentence saying | How this file became today's state | What observation subject changed in this period |
| If deleted | One less noise | Conclusion lost evidence |
| Example | `archive.md` writes "originally called X, renamed Y" | `20260728-comprehensive-analysis.md` writes "last round's entire pool completely invalid" |

Scope: Competitor comprehensive analysis (see `methodology/brand/` competitor analysis spec)  -  Research report  -  Handoff document  -  Changelog. These never merge/rewrite anyway.

⚠️ Exception only covers **this snapshot vs. previous snapshot comparison**. Snapshot plus "some directory deprecated, don't look there" still narrative sidebar.

### Judgment Criteria

Does the referenced target directory still exist?

- Exists → Normal index entry; keep.
- Doesn't exist and no route value → Delete.
- Doesn't exist but has historical traceability value (where did old brand go; what replaced old spec) → Keep condensed in sole source of truth location.
