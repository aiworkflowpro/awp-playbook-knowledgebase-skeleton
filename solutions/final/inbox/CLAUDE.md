# Inbox

> Staging area — new files land here first, then get sorted into the right folder. Nothing stays here forever.

Quick captures, drafts, and imported notes arrive here. From this area the agent decides where each item belongs and moves it to the matching folder.

The step 7 import batch has been processed: four documents went to their targets and the originals are in `archive/202608/20260824-import-batch-archive/` with an `import-log.md` recording every decision. Read that log to see what "place" and "extract" look like on real files.

## File Index

| File | Where it came from | Status |
|------|--------------------|--------|
| `20260824-video-script-youtube.md` | Step 4 naming demo | Not import material. Kept as a live example of the date-first filename form that time-sorted folders use |

## Subdirectory Index

| Directory | Content |
|-----------|---------|
| `archive/` | Processed originals, by month — `archive/{YYYYMM}/{YYYYMMDD}-import-batch-archive/`. Each batch folder keeps the source files under their original names plus an `import-log.md` |

## Processed in the 2026-08-24 batch

| Original | Mode | Went to |
|----------|------|---------|
| `about-me-draft.md` | Extract | `owner/profile.md`, `owner/decisions.md` |
| `competitor-notes-aug-2026.md` | Place | `research/topics/competitor-channels/materials/202608/` |
| `my-first-blog-post.md` | Place | `business/x/post-lessons-x-20260824.md` |
| `old-naming-rules.md` | Extract | `specs/naming-convention.md` |

## Rules

- Read an item fully before deciding where it goes.
- **Place** if the document is complete on its own; **extract** if it should update an existing file.
- In extract mode, read the target file before writing, merge without repeating what is already there, and mark the new information with `(Source: inbox/{original-filename}, {date})`.
- If the source contradicts a file already in the knowledge base, do not silently overwrite. Decide which one the rest of the knowledge base depends on, reconcile, and write down why in the batch log.
- Never delete an original. Once processed, it moves to `archive/{YYYYMM}/{YYYYMMDD}-import-batch-archive/`, keeping its original filename, with an `import-log.md` recording source, target, and mode.
- Register every placed or updated file in its target folder's CLAUDE.md index.
