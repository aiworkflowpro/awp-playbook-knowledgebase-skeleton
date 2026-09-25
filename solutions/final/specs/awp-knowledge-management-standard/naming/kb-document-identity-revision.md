---
document_id: awp-knowledge-management-standard/naming/kb-document-identity-revision
language: en
publication: public
title: "Document Identity and Revision Specification"
purpose: Define cross-language ID, scope, source revision, and sync policy for specification documents
category: General Specification
---

# Document Identity and Revision Specification

> Scope: Each Markdown specification document in `{specs_root}` maintains an **identity** (ID that persists after renaming/moving), **publication scope**, **source revision number**, and **cross-language sync policy**. File naming is managed by `kb-naming-segment-convention.md`; file content is managed by `kb-file-structure-metadata.md`. This specification only manages identity fields.

---

## §1 Applicable Scope

This specification manages Markdown specification documents maintained by this knowledge base under `{specs_root}`. Third-party source texts, upstream data, and retained external code do not enter the document identity system.

Every managed document must declare the following fields in frontmatter:

| Field | Meaning |
|------|---------|
| `document_id` | Document ID that persists across language versions, renaming, and moving |
| `language` | Language code, e.g., `en` for English |
| `publication` | `public` for public documents, `private` for internal documents |
| `source_revision` | Positive integer revision number for semantic content changes |
| `sync_policy` | Sync policy for derived versions |
| `title` | Document title in current language |

`sync_policy` is optional. When present, `source_revision` indicates which source revision a derived document implements.

---

## §2 Document ID

The `document_id` uses the following structure:

```text
{four-segment-standard-package-id}/{document-key-within-package}
```

Examples:

```text
awp-knowledge-management-standard/naming/kb-naming-segment-convention
awp-knowledge-management-standard/directory/kb-area-brand-skeleton
awp-knowledge-management-standard/package-index
```

The document key within a package uses lowercase English, numbers, hyphens, and `/`. The root `CLAUDE.md` has a fixed document key of `package-index`. Subdirectory `CLAUDE.md` files have a fixed final segment of `directory-index`.

When a document is first registered, tools can generate an ID from the path. After registration, the path no longer determines the ID. When files are renamed, moved, or language paths are adjusted, the original ID must be preserved.

ID changes are permitted only in these cases:

- Original document splits into two or more independent documents.
- Multiple original documents merge into one new document.
- Original ID pointed to an incorrect specification entity.

When any of these occur, the relationship between old and new IDs must be recorded in `document-aliases.yaml`. Previously allocated old IDs cannot be reused.

---

## §3 Publication Scope

Public is the default. Use `publication: private` only when the document contains personal privacy, credentials, unpublished operational data, or non-generalizable internal operations. Example domains should use placeholders, relative paths, or directory variables declared in `layout.yaml` rather than personal hostnames, absolute paths, private credential directories, or unpublished services.

A single specification package may contain both public and internal documents, but publishing tools must exclude internal documents by field. If an entire package is internal, all documents within can be marked `private`.

---

## §4 Source Revision Number

`source_revision` starts at `1` and increments by 1 only when the document undergoes semantic changes.

Semantic changes include:

- Adding, removing, or modifying rules, thresholds, processes, fields, or boundary conditions.
- Changing what the document requires or allows readers to do.
- Correcting factual errors that change execution results.

Editorial changes do not increment the revision number. Editorial changes include typos, punctuation, formatting, equivalent rewording, and link fixes that don't change constraints.

After each document modification, a revision review must be performed to explicitly select `semantic` or `editorial`. The tool simultaneously records the source hash. When file content changes but revision review is incomplete, status must be `revision_review_required`; do not publish.

`source_revision` is not SemVer, does not represent public release versions, and does not replace git commits.

---

## §5 Sync Policy

`sync_policy` allows only these values:

| Value | Meaning |
|-------|---------|
| `release` | English can lag during development; must catch up before public release. Default value |
| `on_demand` | Sync English only when explicitly needed; must catch up if document enters one complete public release |
| `on_change` | Sync derived versions immediately after semantic changes. Use only for high-frequency external entry points |

Structure and identity are unaffected by sync policy. After additions, moves, or renames, mappings and target paths should update immediately; derived content can update later per policy.

---

## §6 Machine Indexes

`document-index.json` is generated by tools and not edited manually. The index records at minimum: document ID, specification package ID, document key, path, language, publication scope, title, source revision, and content hash.

`translation-state.json` is an internal sync ledger not included in public repositories. It records source revision, derived revision, source commit, source hash, derived hash, and review status.

---

## §7 Checklist

- [ ] Each managed document has a unique `document_id`.
- [ ] Counterpart documents in different languages use the same `document_id`.
- [ ] After renaming or moving files, original ID is retained.
- [ ] Semantic changes have incremented `source_revision`.
- [ ] Editorial changes have completed revision review without incrementing revision number.
- [ ] Publication scope and sync policy use controlled values.
- [ ] Public documents do not contain personal environment dependencies.

---

## Relationships with Other Specifications

| Related Specification | Relationship |
|----------------------|-------------|
| `kb-naming-segment-convention.md` | File name is storage location; `document_id` is permanent identity; renaming must preserve ID |
| `kb-naming-governance-migration.md` | During batch renaming, `document_id` is an identity field of the renamed object itself; must verify each one |
| `kb-file-structure-metadata.md` | Frontmatter fields in this specification are machine sync fields; do not replace the knowledge file metadata table |
| Translation and Cross-Language Specifications | Consume `source_revision` and `sync_policy` for sync gates |

---

## Change Log

> Rolling window, retain last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Merged into naming dimension and generalized |
