---
document_id: awp-knowledge-management-standard/naming/kb-file-structure-metadata
language: en
publication: public
title: "File Structure and Metadata Standard"
purpose: Universal structure, metadata, quality tiers, deprecation notes, and changelog constraints for all .md documents
category: General Standard
audit:
  group: Documentation and Language
  dimension: Changelog and Deprecation Notes Compliance
  check: "Files with a changelog or deprecation notes must follow ≤3 entries / ≤20 characters per entry, and end with the order deprecation notes → changelog"
  metric: "More than 3 entries = warn; a single entry over 20 characters = warn; wrong order = warn; missing changelog section = recommend"
---

# File Structure and Metadata Standard

> Scope: every `.md` document in the knowledge base (knowledge files + `CLAUDE.md` + best-practice tutorials + workflow documents + standard texts + business reports, etc.).
> Deliverable responsibility: defines the universal structure, metadata, quality tiers, lifecycle, and **deprecation-notes / changelog constraints** for documents.
> §1.1 changelog constraints and §1.2 deprecation-notes constraints = **the single master rule for the entire vault**; any file with a matching section must follow them.
> How file names and directory names are chosen, see `kb-naming-segment-convention.md`.

> ⚠️ **Layered applicability**: metadata, quality tiers, and lifecycle apply to knowledge files only (`CLAUDE.md` / best practices / business reports each have their own standards).
> But **§1.1 / §1.2** sit above every standard layer: as long as a file has `## Changelog` or `## Deprecation Notes`, it must follow ≤3 entries / ≤20 characters; the end-of-file order is fixed as deprecation notes → changelog.

---

## §0 Global Timestamp Rules

✅ **All timestamps in the knowledge base use 24-hour time in a single declared time zone.** The declared time zone of this vault is Beijing time (Asia/Shanghai, UTC+8); when a different vault adopts this rule, change only this declaration. The rules themselves stay unchanged.

Scope: every scenario that involves timestamps — directory names, file names, `run_id`, daily report dates, run records, scheduling records. Regardless of which machine runs the code and regardless of the host's local time zone, convert everything to the declared time zone before writing.

| Scenario | Format | Example |
|------|------|------|
| Time in directory / file names | `HHMMSS` or `YYYYMMDD-HHMMSS` | `183222`, `20260623-183222` |
| ISO 8601 timestamp | With time zone offset | `2026-06-23T18:32:22+08:00` |
| Date directory | `YYYYMMDD` (date in the declared time zone, compact, no dashes) | `20260623` |
| Month directory | `YYYYMM` (month in the declared time zone) | `202606` |

Python conversion example: `datetime.now(ZoneInfo('Asia/Shanghai')).strftime('%H%M%S')`

❌ Timestamps using "local machine time", "UTC", or no declared time zone are forbidden.

⚪ **Single exception**: scenarios where third-party protocols require UTC (for example, AWS SigV4 signing, OAuth timestamps, HTTP Date headers). These must use UTC, with a comment next to the code: `# protocol requires UTC, exempt from the global time zone rule`. Everything else uses the declared time zone.

---

## Design Philosophy

| Principle | Description |
|------|------|
| **Metadata is a contract** | Type / source / status decide how an Agent treats a file (load priority, editability, staleness detection) |
| **Explicit lifecycle** | Four stages — birth → growth → split → archive; every file has a clear current state and a next direction |
| **Quality tiers drive evolution** | L0–L4 is an evolution path, not a score — every file knows where it stands and how to level up |
| **Orthogonal responsibilities** | `CLAUDE.md` indexing has its own standard (see `../directory/kb-entry-authoring-standard.md`); this standard governs knowledge content files only |

---

## Organization Framework

| # | Question | Section | Core Content |
|---|------|------|---------|
| §1 | How is a file segmented? | Universal File Structure | Metadata + body + deprecation notes + changelog |
| §2 | How do I fill in metadata? | Metadata Standard | Required / optional field definitions |
| §3 | How do I mark the source? | Source Marking | Three sources: user / pack / imported |
| §4 | How many quality tiers are there? | Quality Tiers | L0–L4 promotion path + verifiable conditions |
| §5 | What is the lifecycle? | Lifecycle | Birth → growth → split → archive |

---

## §1 Universal File Structure

Knowledge files assemble their structure according to the quality tier (aligned with §4; a draft need not be fully assembled from the start):

| Tier | Title | Metadata Table | Body | Deprecation Notes | Changelog |
|------|:----:|:--------:|:----:|:--------:|:--------:|
| L0 raw material | ✅ | ⚪ | ✅ | ⚪ none by default | ⚪ |
| L1+ structured and above | ✅ | ✅ required | ✅ | ⚪ none by default; create only when there are many asides | large ✅ / ≤200 lines ⚪ |

```markdown
# Title

## Metadata          ← L1+ ✅ required, the file's ID card; may be absent at L0
(metadata table)

---

(body)              ← ✅ required; write only the currently valid state

---

## Deprecation Notes ← ⚪ absent by default; create only when there are many asides (see §1.2)
| Date | Note |

## Changelog         ← large files ✅ required, small files ≤200 lines ⚪ optional; if present, it comes last
| Date | Change |
```

> Changelog details in §1.1; deprecation notes in §1.2 (**optional by default — do not add one to every file**).
> **Fixed end-of-file order**: body → `## Deprecation Notes` (optional) → `## Changelog` (if present, the last section).
> Knowledge files ❌ carry no version numbers — see the "Version Number Authoring Standard" for the versioning policy.
> **Aligned with current state**: journals, position drafts, clippings, etc. often exist at L0 (no metadata table); backfill the table when a file is promoted to L1 or is about to be formally referenced by a workflow / Skill.

| Good | Bad | Reason |
|----|-----|------|
| Metadata table directly after the title (L1+) | Metadata scattered through the body | An Agent can spot the former at a glance |
| Changelog as a date-descending table | Prose describing "what changed last time" | The former is machine-readable |
| Delete a half-sentence aside outright | Create a whole deprecation-notes section for every deleted half-sentence | The section shell weighs more than the aside; gilding the lily |
| Create deprecation notes after deleting multi-line tombstones | Leave `~~` / "already converged → archived" in the middle of the body | The body holds only the current state; a section is worth it only for many old names |

### §1.1 Changelog Constraints (the Single Master Rule for the Entire Vault)

> **Scope**: any `.md` document in the knowledge base that has a `## Changelog` section.
> Includes but is not limited to: knowledge files, `CLAUDE.md` at every level, best-practice tutorials, workflow documents, business reports, standard texts.
> This section is the **single master rule** for changelogs; other standards may only reference it and ❌ must not rewrite the numbers.
> **Not applicable**: `CHANGELOG.md` of code deliverables (CLI / MCP / Skill / Plugin). Those follow SemVer — see "Version Number Authoring Standard §3–§4".

A changelog consumes Agent context — this rule exists to save context, not to record history.
This table is only a quick-view window of recent evolution; it does not carry full history (full history lives in `git log`).

**Hard constraints**:

| Field | Constraint |
|------|------|
| Rolling window | ✅ at most **3** entries; beyond that, delete from the bottom (oldest) outright. ❌ no merging, no archiving. Uniform across the vault, no per-layer exceptions |
| Date | ✅ `YYYY-MM-DD`, fixed 10 characters, descending order |
| Length per entry | ✅ hard cap of ≤**20** characters (1 character = 1) |
| Format per entry | ✅ single line; ❌ no `<br>`, lists, code blocks, or line breaks |
| Column count | ✅ two columns `date + content`; ❌ three columns including a version number are forbidden |

**Core rule: neither knowledge files nor `CLAUDE.md` carry version numbers**

With no external consumer, a version number conveys no contract; it only degrades into a "modification counter". Full rationale → "Version Number Authoring Standard §1 tiering strategy".

**Blacklist / whitelist**:

| Content Type | Written? | Alternative Location |
|---------|:-------:|---------|
| Adding / removing sections, rules, or structure | ✅ | — |
| Major content rewrites | ✅ | — |
| Wording polish / typos / formatting | ❌ | git commit |
| Design rationale / trade-off explanations | ❌ | "Design Philosophy" section of the body |
| Migration guides / long explanations | ❌ | a separate file or `{inbox_root}archive/` |
| Entity renames / decommissions / path moves | ❌ | body writes only the new state; several entries → §1.2 (optional by default) |

✅ One event per entry, starting with the verb or the subject, telegraphic summary
❌ Forbidden: a `version` column, `vX.Y.Z` markers, listing multiple ① ② ③ sub-items

**Writing examples**:

| Good (≤20 characters) | Bad (>20 characters or several events in one entry) |
|------|------|
| `domain-cli v1.3 RDAP+proxy pool` | `domain tool v1.3.0: ① primary path switched to RDAP over HTTPS ② batch loads the proxy pool by default ③ added --no-proxy ...` |
| `7 hosts aliases unified, cd knowledge base` | `claude + codex aliases on all 7 hosts fully aligned, ~/.zshrc on every machine unified to cd <knowledge base> &&...` |
| `added vendor 4-option matrix` | `added vendor directory: unified vendor management. Integrated 4 options...` |

**Template (standard hint line ✅ required, fixed wording)**:

```markdown
## Changelog

> Rolling window: keep the latest 3 entries, each ≤20 characters.

| Date | Change |
|------|---------|
| YYYY-MM-DD | telegraphic summary ≤20 characters |
```

✅ **The hint line must directly follow the heading** — the wording is fixed as `> Rolling window: keep the latest 3 entries, each ≤20 characters.`, not one character off:

- Purpose: the rule travels with the deliverable; when an Agent edits the record, it sees the constraint at first glance, no need to look up the standard
- ❌ Rewording, changing the numbers, or deleting the hint line are forbidden
- Exception: when only the `## Changelog` section is absent (small files ≤200 lines ⚪ optional), no hint line is needed
- Exception: if a sub-document of a large standard family has its changelog maintained centrally by its owning `CLAUDE.md`, the sub-document does not set up its own `## Changelog`

**Hard ceiling**: heading 1 + hint line 1 + blank line 1 + table header 2 + ≤3 data rows = ≤8 lines total, never exceeded.

**Over-limit repair**: when more than 3 entries or entries over 20 characters are found, keep the latest 3 and delete the rest; for over-length entries, compress — take the essence of the bold prefix or the part before the colon, cut to 18 characters and append `...`.

❌ No exemption markers. When over the limit, compress the content until it is actually compliant — the character cap is the entire meaning of this rule; bypassing it cancels it.

> ⚠️ Exception: code deliverables (CLI / MCP / Skill) are not governed by this standard; they use their own `CHANGELOG.md` — see "Version Number Authoring Standard §3–§4".

### §1.2 Deprecation Notes Constraints (the Single Master Rule for the Entire Vault  -  Off by Default)

> **English anchor**: Deprecation notes (Deprecated / Removed / Superseded).
> **Scope**: `.md` files in the knowledge base that **already have** a `## Deprecation Notes` section — if present, it must comply; **the vast majority of files should not have this section**.
> This section is the **single master rule** for deprecation notes; other standards may only reference it and ❌ must not rewrite the numbers.
> **Purpose**: the body and live indexes forbid "no longer in use" statements; only when multiple short memories must be kept does this section absorb them — **not a tax every file must pay**.

Deprecation notes record **the fate of a subject entity leaving the scene**, not "what this document changed" (the latter → §1.1 changelog).

**When to create the section (dynamic  -  not created by default)**:

| Judgment | Action |
|------|------|
| Half-sentence aside, strikethrough in a cell, `~~` inside a fixed pitfall | **delete / rewrite as current state only**; ❌ do not create this section |
| "No longer used" short facts to keep in the same file **≤1** | **delete from the body only**; generally do not create the section (the section shell is longer than that one fact) |
| Clearing **multi-line tombstones** in one pass (for example, several `~~` lines in an index, a whole "merged source / already archived" block) or keeping **≥2** short facts | ⚪ **create this section**, write ≤3 entries |
| Long process narratives | delete from the body; move to `{inbox_root}archive/`; this section does not carry them |

❌ Forbidden: "cleared one aside, so casually add an empty deprecation-notes shell". The section shell plus hint line is about a hundred characters; deleting the half-sentence aside is enough — adding the section is gilding the lily.

**End-of-file order (when this section exists)**:

```text
(body, current state only)
## Deprecation Notes ← ⚪ absent by default; if present, directly above the changelog
## Changelog     ← if present, the last section
```

❌ Putting `## Deprecation Notes` after `## Changelog` is forbidden.
❌ Writing deprecation-style sentences in the middle of the body ("was originally", "deprecated", "formerly used", `~~old name~~`, etc.) is forbidden.

**Hard constraints** (only when this section exists; same numbers as §1.1):

| Field | Constraint |
|------|------|
| Rolling window | ✅ at most **3** entries; beyond that, delete from the bottom (oldest) outright. ❌ no merging, no archiving |
| Date | ✅ `YYYY-MM-DD`, fixed 10 characters, descending order |
| Length per entry | ✅ hard cap of ≤**20** characters (1 character = 1) |
| Format per entry | ✅ single line; ❌ no `<br>`, lists, code blocks, or line breaks |
| Column count | ✅ two columns `date + note`; ❌ comparison multi-column tables or a version column are forbidden |

**Division of labor with the changelog**:

| | Deprecation Notes (optional) | Changelog |
|--|----------|----------|
| Object | Subject entity (path, field, module, command, directory name) | This file's own section / rule operations |
| Sentence pattern | "X decommissioned / renamed / moved" | "added a rule / changed a table / fixed a link" |
| Example | `field agent renamed to executor` | `deleted index tombstone lines` |

The same change may produce one line in each; ❌ merging the two into one sentence and cramming it into a single section is forbidden.

**Blacklist / whitelist** ("written" = written into this table; precondition is **the decision to create the section**):

| Content Type | Written? | Alternative Location |
|---------|:-------:|---------|
| Entity decommission / whole package removal | ✅ | create the section only for ≥2 entries or large cleanups; otherwise delete from the body only |
| Renames / field or command renames | ✅ | same as above |
| Path moves (old path merged into a new path) | ✅ | same as above |
| Merged / superseded / converged entries | ✅ | after deleting `~~` from the body; create the section when there are several lines |
| Discredited positions / old approaches no longer used | ✅ | after deleting the narrative from the body; create the section when there are several entries |
| Offhand historical half-sentence ("replaces the deprecated X") | ❌ | **delete the half-sentence only**; no section by default |
| Long migration guides / multi-step causality / process narratives | ❌ | `{inbox_root}archive/{YYYYMM}/` or a separate file |
| Strikethrough old names embedded in the body | ❌ | delete cleanly from the body; consider this table only for several lines |
| Which sections of this file changed | ❌ | → §1.1 changelog |
| Status columns (credentials expired / deprecated, etc., current status) | ❌ | keep in the body as a current-state field |
| Links / accounts no longer sold but still kept | ❌ | keep in the body; remove the strikethrough, mark status = no longer sold |
| Looks old but is actually a term / current rule / book excerpt / point-in-time snapshot | ❌ | leave untouched |
| Version comparisons inside point-in-time snapshots | ❌ | see `../directory/kb-entry-antipattern-archiving.md § exception: dated point-in-time snapshots` |

✅ Note style: who is gone, who it became. ❌ Not a big old-vs-new comparison table, not a long migration essay.

**Procedure (when hitting a "no longer in use" sentence in the body)**:

1. **Delete** the sentence / line from the body or live index (including `~~`) — **this step is always done**
2. Judge per "when to create the section": default **stop here**; create the section only for multi-line / ≥2 short facts
3. If creating the section: compress to ≤20 characters and write; fixed hint line; delete the oldest when over 3 entries
4. Long text → archive; this table's content **is not an execution entry point**; routing trusts only live tables

**Writing examples** (only when the section has been created):

| Good (≤20 characters) | Bad |
|------|------|
| `field agent renamed to executor` | `We used to use agent, then to align with runtime we changed it to executor...` |
| `old path shared/ merged into tools/` | `~~shared/~~ → tools/` still written in the body |
| `module foo fully decommissioned` | deleted the half-sentence aside but added a whole deprecation-notes section |

**Template (only when creating the section; hint line wording fixed)**:

```markdown
## Deprecation Notes

> Rolling window of 3, each ≤20 characters: short notes on anything no longer in use (decommissioned, deprecated, renamed, moved, merged, superseded, old names, old paths) go here only; do not write them into the body.

| Date | Note |
|------|------|
| YYYY-MM-DD | telegraphic note ≤20 characters |
```

✅ **If the section is created, the standard hint line must directly follow the heading** — the wording is fixed as:

`> Rolling window of 3, each ≤20 characters: short notes on anything no longer in use (decommissioned, deprecated, renamed, moved, merged, superseded, old names, old paths) go here only; do not write them into the body.`

Not one character off.

- **Default**: no such section
- Section exists but has no lines left to write: ❌ do not leave an empty table — **delete the whole section**
- Long obsolete texts still go to `{inbox_root}archive/{YYYYMM}/`

**Hard ceiling** (when this section exists): heading 1 + hint line 1 + blank line 1 + table header 2 + ≤3 data rows = ≤8 lines total.

**Over-limit repair**: same as §1.1 — keep the latest 3 entries; cut over-length entries to 18 characters and append `...`.

---

## §2 Metadata Standard

> The metadata table in this section **constrains knowledge files only** (see the layered applicability at the top). Standard texts themselves are not bound by this table: their status and dates are carried by their owning `CLAUDE.md`, and the body may omit the metadata table; if a body uses frontmatter purely as machine annotation, that is not a violation — the ruling is in "Standard Authoring Standard § two-file system".

### ✅ Required Fields

| Field | Description | Values |
|------|------|------|
| Type | Nature of the file | identity / style / business / profile / process / template / reference / work / industry / standard / experience |
| Source | Who created it | see §3 source marking |
| Status | Current life stage | draft / active / archived |
| Updated | Last modification date | `YYYY-MM-DD` |

### ⚪ Optional Fields

| Field | When Applicable |
|------|---------|
| Created | When creation and update times need to be distinguished |
| Tier | L0–L4 knowledge quality tier |
| Review cycle | Periodic review frequency |
| Validity | Re-validation date for experience-type files |

> ❌ A `version` field is forbidden in knowledge-file metadata tables. See the "Version Number Authoring Standard" for the versioning policy.

### Metadata Table Format

```markdown
## Metadata

| Field | Value |
|------|---|
| Type | business |
| Source | user |
| Status | active |
| Updated | 2026-03-24 |
```

| Good | Bad | Reason |
|----|-----|------|
| `Updated: 2026-03-24` | `Updated: yesterday` | The former is an absolute date, unambiguous across sessions |
| `Type: business` | `Type: I think it is business-related` | The former is an enum value, verifiable |

> The `document_id`, `publication`, `source_revision`, and `sync_policy` fields in the frontmatter of standard documents are managed by `kb-document-identity-revision.md`. They are machine sync fields; they do not replace the knowledge-file metadata table of this section.

---

## §3 Source Marking

| Source Value | Meaning | Permissions |
|--------|------|--------|
| user | Created or confirmed manually by the user | ✅ editable, ❌ not deletable (change to archived) |
| `pack:{industry}` | Injected by an industry pack | ❌ read-only, not modifiable |
| imported | Triaged and placed from the inbox | ✅ editable; after confirmation ✅ change to "user" |

Industry-pack sources carry the industry name, e.g. `pack:education`, `pack:medical-aesthetics`; multiple industries stack without interfering with each other.

| Good | Bad | Reason |
|----|-----|------|
| `Source: pack:education` | `Source: found it online` | The former is an enum value; an Agent can determine permissions |
| `Source: imported` → changed to `user` after confirmation | stays `imported` forever | after confirmation, the source should be upgraded |

---

## §4 Knowledge Quality Tiers

| Tier | Name | Promotion Condition (✅ verifiable) | Example |
|------|------|---------------------|------|
| L0 | Raw material | The file exists | Clipped articles, screenshots, voice-transcribed text |
| L1 | Structured | Has a complete metadata table (type + source + status + updated) | A product intro written from the template |
| L2 | Validated | Referenced ≥1 time by a Skill or workflow (verifiable via `grep`) | A template used 5 times with good results |
| L3 | Distilled | Patterns extracted from ≥3 L2 materials, confirmed by the user | 5 patterns distilled from 20 experience entries |
| L4 | Propagable | Published to an external platform or included in a course | Published articles, course materials |

**Promotion path**: L0 → fill in metadata → L1 → referenced → L2 → user-confirmed distillation → L3 → published → L4

---

## §5 File Lifecycle

### Birth

| Method | Source Marking | Entry Point |
|------|---------|------|
| Generated by an initialization Skill | user | Auto-created when the vault is built |
| Injected by an industry pack | `pack:{industry}` | Injection step |
| Created manually by the user | user | Filled in from the template |
| Imported from the inbox | imported | AI triage and placement |

### Growth

| File Type | Growth Method | Frequency |
|---------|---------|------|
| identity / style | Occasional adjustments | Quarterly review |
| business / profile | Updated when business changes | On demand |
| process | Append experience on every execution | Most active |
| template | Append validation data on every use | Data-driven |
| industry | Append when new rules are discovered | When hitting pitfalls |

### Split

✅ Files over 500 lines must be split:

| File Type | Split Method |
|---------|---------|
| Business files | Promote to a subdirectory (intro.md + accompanying files) |
| Term files | Split by category (terms-project.md + terms-operations.md) |
| Process files | Split by stage |
| Experience records | When over 20 entries, distill patterns then archive old records |

> ⚠️ Deviation condition: a file over 500 lines whose content cannot be split (for example, a complete API reference) must be marked `⚠️ deviation: 500-line split | reason: {reason}`.

### Archive

| Trigger Condition | Action |
|---------|------|
| Business decommissioned | Change status to "archived"; the file stays in place, not moved |
| Expired rules | Delete, or mark "expired" |
| Old process versions | Write one line in the changelog; hand the historical details to git |

---

## Checklist

**Creating a knowledge file**:

- [ ] L0 may have no metadata; when promoted to L1+, include the metadata table (✅ type + source + status + updated)
- [ ] Source marked with an enum value (user / `pack:{industry}` / imported)
- [ ] File name follows the naming standard (no spaces, no special characters; patterns in `kb-naming-segment-convention.md`)
- [ ] Placed under the correct top-level directory
- [ ] ❌ did not delete a file whose source is "user"
- [ ] ❌ did not modify a file whose source is `pack:*`

**Quality promotion**:

- [ ] L0→L1: has a complete metadata table (type + source + status + updated)
- [ ] L1→L2: referenced ≥1 time by a Skill or workflow (`grep` verifies the reference relationship)
- [ ] L2→L3: patterns distilled from ≥3 L2 materials, confirmed by the user
- [ ] L3→L4: published to an external platform or included in a course

**File maintenance**:

- [ ] Files over 500 lines have been split (or carry a deviation note)
- [ ] Files with source "imported" have been changed to "user" after confirmation
- [ ] Updated date is the actual last modification date

**Deprecation notes** (⚪ no such section by default; create only when there are many asides):

- [ ] ❌ did not create a section for a half-sentence aside (default: delete from the body only)
- [ ] If the section exists: located **before** `## Changelog`; an empty table means deleting the whole section
- [ ] Two columns `| Date | Note |`; hint line verbatim (see §1.2 template)
- [ ] ≤**3** entries, each ≤**20** characters; entity exits only, no this-file operations
- [ ] Body has no "was originally" / "deprecated" / "formerly used" / `~~old name~~` obsolete asides

**Changelog**:

- [ ] Two-column format `| Date | Change |`; ❌ no version column
- [ ] Metadata table ❌ has no `version` field
- [ ] **✅ standard hint line directly after the heading: `> Rolling window: keep the latest 3 entries, each ≤20 characters.`** (verbatim)
- [ ] Changelog ≤**3** entries (delete the oldest when over)
- [ ] Each entry ≤**20** characters, single line, no `<br>` / lists / code blocks / listed sub-items
- [ ] Section / rule changes only; no wording / typos / rationale; entity exits do not go into this table (several entries → deprecation notes, optional by default)
- [ ] One event per entry, date descending
- [ ] If present, it is the last section at the end of the file
- [ ] `CLAUDE.md` also follows this rule (§1.1 / §1.2 are the single master rule for the entire vault)

---

## Changelog

> Rolling window: keep the latest 3 entries, each ≤20 characters.

| Date | Change |
|------|---------|
| 2026-08-07 | Merged into the naming dimension and generalized |
