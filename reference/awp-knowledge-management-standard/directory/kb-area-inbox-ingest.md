---
document_id: awp-knowledge-management-standard/directory/kb-area-inbox-ingest
language: en
publication: public
title: "Document Ingestion Specification"
---

# Document Ingestion Specification

> Governs one thing: when documents arrive in `inbox/`, how to process them one by one — place or extract — then archive the originals.
> This specification defines hard rules. For determining which directory a document belongs to, reference the Placement Analysis Methodology (`kb-method-inbox-placement`). For file naming, reference the Naming Segment Convention (`kb-naming-segment-convention`).

---

## § 1 · Scope and Trigger Conditions

### In scope

- After the user places a batch of external documents into `inbox/`, the agent processes each one into the correct location within the knowledge base.
- External documents include but are not limited to: old notes, downloaded articles, exported chat logs, strategy documents, deliverable backups, files received from others.

### Trigger

- The user explicitly says "process the files in inbox," "ingest these documents," or "sort the inbox."
- Or the agent discovers unprocessed files in `inbox/` during another task and proposes to process them.

### Out of scope

- Files whose destination can be determined before entering `inbox/` — route them directly to the target directory. (See `kb-area-inbox-skeleton` processing pipeline.)
- Code files — code goes to code repositories, not the knowledge base. Only usage documentation and credentials stay. (See `kb-method-inbox-placement § Code stays out of the knowledge base`.)

---

## § 2 · Per-Document Analysis Flow

Each document is processed independently. No batch guessing.

### Steps

1. **Read the full document.** Understand its topic, structure, and information density.
2. **Determine top-level destination.** Which of the 11 top-level directories does this document belong to? Use the four-dimension analysis: content type → consumer → subdomain → create or append. (Details in `kb-method-inbox-placement § Four-Dimension Analysis`.)
3. **Read the target directory's `CLAUDE.md`.** Determine the subdirectory. This step cannot be skipped — subdirectory boundaries are defined in each directory's own entry file.
4. **Determine processing mode.** Place or extract? See § 3.
5. **Generate a proposal.** Include: source file path, processing mode, target path, confidence level, operation summary.
6. **Wait for user confirmation.** Execute only after the user approves.

---

## § 3 · Processing Mode Determination

Each document takes exactly one mode. The decision is based on the document's nature, not user preference.

### Place Mode (Copy & Place)

Copy the entire document as-is to the target directory, renamed per the naming convention.

| When to use | Example |
|-------------|---------|
| The document is independent and complete — usable on its own | Published articles, standalone research reports, complete tutorials |
| The document is an atomic unit — splitting it destroys its value | Contracts, invoices, certificates, resumes |
| All content in the document belongs to a single target directory | An article about AI video tools → `research/ai-video-tools/material/{YYYYMM}/` |

### Extract Mode (Extract & Update)

Pull valuable information from the document and merge it into existing files in target directories. The original document is not copied to any target directory.

| When to use | Example |
|-------------|---------|
| The document contains scattered info belonging to different directories | A strategy doc mentions brand positioning (→ `brand/identity.md`), audience (→ `brand/audience.md`), business model (→ `brand/businessmodel.md`) |
| The information should be merged into existing files, not create new ones | Meeting notes about decision preferences → append to `owner/decisions.md` |
| The document itself has no standalone value; its value is in the information it contains | An email mentioning a new competitor → update the relevant file in `research/competitor-channels/` |

### Decision Table

| Question | Yes | No |
|----------|-----|----|
| Is the document an independent, complete work? | → Lean toward Place | → Lean toward Extract |
| Does all content point to a single target directory? | → Place | → Extract (info spans multiple directories) |
| Does the target directory already have a file covering the same topic? | → Extract (merge into existing) | → Place (create new file) |
| Does the document have standalone reference value outside the KB context? | → Place (preserve the complete original) | → Extract (only the information matters) |

When both modes are defensible, default to Place — the cost of preserving a complete original is lower than the risk of losing information.

---

## § 4 · Confidence Scoring and User Confirmation

The agent assigns a confidence level to each document, which determines the interaction style.

| Confidence | Meaning | Interaction |
|------------|---------|-------------|
| **HIGH** | Target directory is clear, processing mode is unambiguous | One-line proposal summary; user may batch-confirm |
| **MEDIUM** | Target directory is likely correct, but both processing modes are plausible | Show full proposal details; wait for per-document confirmation |
| **LOW** | Destination uncertain, or content spans multiple domains without a clear primary | Show full-text analysis and multiple candidate plans; wait for user to decide |

### Confidence Assignment Rules

- Document title or content clearly matches a top-level directory's stated responsibility → HIGH
- Must read the full document to determine destination → MEDIUM
- Full reading still leaves multiple plausible candidates → LOW
- Document content has no obvious correspondence to any existing KB structure → LOW

### Proposal Format

Each document's proposal contains:

```
Source:     inbox/old-strategy-doc.md
Confidence: MEDIUM
Mode:       Extract
Targets:
  - brand/identity.md ← extract brand positioning paragraphs
  - brand/audience.md ← extract audience description
Summary:    This document is a 2024 brand strategy review. Its brand positioning
            and audience descriptions are more detailed than current files.
            Recommend extracting and updating.
```

---

## § 5 · Place Mode Execution

After user confirmation, execute in this order:

1. **Copy the file to the target directory.** Do not move — the source file stays in `inbox/` until archiving.
2. **Rename.** Follow the Naming Segment Convention (`kb-naming-segment-convention`). Common four-segment pattern: `{date}-{type}-{language}-{title}.md`.
3. **Update the target directory's `CLAUDE.md`.** If the new file opens a new subtopic, register it in the parent `CLAUDE.md` index. If the file simply joins an existing subdirectory, no `CLAUDE.md` update is needed.
4. **Log the operation.** Write one record in the batch's metadata log (see § 10).

---

## § 6 · Extract Mode Execution

After user confirmation, execute in this order:

1. **Read the target file's current content.** This step cannot be skipped — writing directly risks overwriting or duplicating existing content.
2. **Locate the insertion point.** Find the relevant section or paragraph in the target file.
3. **Merge information.** Write the source document's information into the target file. Follow these rules:
   - Do not copy raw paragraphs — rewrite in the knowledge base's language style.
   - Preserve the target file's existing structure and formatting.
   - Annotate the source of new information. Format: add a line at the end of the new section: `(Source: inbox/{original-filename}, {date})`.
   - If the target file has a `source_revision` in its frontmatter, increment it by one.
4. **Check for duplication.** Confirm no existing information was written again.
5. **Log the operation.** Write one record in the metadata log (see § 10).

---

## § 7 · Naming Normalization

All files produced by Place mode must comply with the Naming Segment Convention.

### Common Naming Patterns

| Target Area | Naming Pattern | Example |
|-------------|---------------|---------|
| `research/{topic}/material/{YYYYMM}/` | Four-segment: date-type-language-title | `20260823-ar-en-runway-gen4-update.md` |
| `business/{arena}/` | Per that arena's naming rules | Defined by the arena's `CLAUDE.md` |
| `owner/` · `brand/` | Dimension-type, named by function | `profile.md` · `decisions.md` · `identity.md` |
| `specs/` | Standards naming pattern | Defined by the standards skeleton |

### Original Filename Preservation

- The placed file uses the normalized name.
- If the source file's original name has reference value (e.g., contains a version number or source identifier), record it in the file's frontmatter as `original_filename`.

---

## § 8 · Archiving

After all files in a batch have been processed and the user has confirmed, execute archiving.

### Steps

1. Move all processed source files from `inbox/` to `inbox/archive/{YYYYMM}/` (the archive directory).
2. Archive directory naming: `{YYYYMMDD}-import-batch-archive/` (per the inbox skeleton's archive naming convention).
3. Source files inside the archive directory keep their original names — the original name is evidence for traceability.
4. Unprocessed files (skipped by user, or low-confidence without confirmation) stay in `inbox/`.

### Hard Rules

- **Never delete.** Source files are only moved to the archive, never deleted.
- **Never leave processed files in inbox/.** inbox is a processing pipeline, not a warehouse.
- **Always retrievable.** Anyone can find the original document in `archive/{YYYYMM}/` at any time.

---

## § 9 · Batch Processing Rhythm

### Single-Document Loop

```text
Read document → Analyze destination → Determine mode → Generate proposal → User confirms → Execute → Next
```

Each document completes the full cycle independently. No predicting, no skipping steps, no accumulating a batch before asking.

### Batch Summary

After all files in a batch are processed, output a summary report:

```text
Batch processed: 12 documents
  Placed: 8 (research/ 4, business/ 2, owner/ 1, brand/ 1)
  Extracted: 3 (brand/identity.md updated 2x, owner/decisions.md updated 1x)
  Skipped: 1 (user decided to handle later)
Archive location: inbox/archive/202608/20260823-import-batch-archive/
```

### Interruption and Resumption

If processing is interrupted (user leaves, session disconnects), on resumption:
- Continue with the files still in `inbox/`.
- For files already placed/extracted but not yet archived, verify the operation completed at the target location, then proceed to archiving.

---

## § 10 · Metadata and Audit Trail

Record the following metadata for every processed document. Metadata is written in an `import-log.md` file inside the batch archive directory.

| Field | Description | Example |
|-------|-------------|---------|
| Source file | Original path in `inbox/` | `inbox/old-brand-strategy.md` |
| Processing mode | Place or Extract | `Extract` |
| Confidence | HIGH / MEDIUM / LOW | `MEDIUM` |
| Target path | Place: full target file path. Extract: which files were updated | `brand/identity.md`, `brand/audience.md` |
| Operation summary | One sentence describing what was done | `Extracted brand positioning and audience description, updated two files in brand/` |
| Processed at | ISO 8601 | `2026-08-23T22:00:00+08:00` |
| Confirmation type | Per-document / Batch | `Per-document` |

---

## § 11 · References

| Referenced Document | What This Specification Uses It For |
|--------------------|--------------------------------------|
| `kb-method-inbox-placement` | Four-Dimension Analysis — determining which top-level directory a document belongs to |
| `kb-naming-segment-convention` | Naming Segment Convention — how to rename placed files |
| `kb-area-inbox-skeleton` | Inbox Directory Skeleton — the directory structure of inbox/ and archive |
| `kb-method-inbox-archive` | Archive Methodology — archive directory naming and lifecycle |
| Each area's `kb-area-*-skeleton § ⑦` | Build Procedure for each directory — determining subdirectories and file formats |

---

## Checklist

- [ ] Every document was read in full, not just the title
- [ ] Every document has a determined top-level directory destination, and the target `CLAUDE.md` was read
- [ ] Every document has a clear processing mode (Place or Extract), not a vague treatment
- [ ] In Extract mode, the target file's current content was read before writing
- [ ] In Extract mode, new information is annotated with its source
- [ ] In Place mode, the file was renamed per the naming convention
- [ ] Every document has a proposal that was confirmed by the user before execution
- [ ] All processed source files have been moved to the `archive/{YYYYMM}/` archive directory
- [ ] The archive directory contains `import-log.md` with one record per document
- [ ] No processed files remain in inbox/

---

## Change Log

> Rolling window, keep the latest 3 entries, each ≤ 20 words.

| Date | Change |
|------|--------|
| 2026-08-23 | Created. Defines two-mode ingestion process |
