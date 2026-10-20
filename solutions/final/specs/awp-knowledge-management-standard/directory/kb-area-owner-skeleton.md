---
document_id: awp-knowledge-management-standard/directory/kb-area-owner-skeleton
language: en
publication: public
title: "Knowledge Base Owner/ Directory Skeleton"
---

# Owner/ Directory Skeleton

> Defines the subdirectory structure, organization patterns used, and customization interfaces of the `{owner_root}` root directory.

## Responsibilities

Stores facts about the project owner: what they've done, what they excel at, where they're headed, how they make judgments, how they collaborate. The single source of truth for the entire knowledge base, shared read by all brands, not replicated into brand directories.

## Directory Structure

```text
{owner_root}
├── CLAUDE.md       ← Fixed; entry index
├── experience/     ← Fixed; what they've done, milestones
├── expertise/      ← Fixed; what they excel at, capability boundaries
├── vision/         ← Fixed; where they're headed, long-term goals
├── decisions/      ← Fixed; what they believe in, judgment frameworks, values and red lines
└── collaboration/  ← Optional; output requirements for Agents, environment and habits
```

- Path variable `{owner_root}` is declared in `{specs_root}layout.yaml`, resolved as `owner/`.
- The five dimension directories are peer-level; no third-layer subdirectories below them.
- Each dimension directory must have `CLAUDE.md`; other files use four-segment names like `{type}-{dimension}-{topic}-{scope}.md`, e.g., `constraint-decision-values-and-redlines-general.md`.
- No duplication between dimensions: a single fact is written in one dimension only; other places only write pointers.

## Organization Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → dimension | **E2 Person dimension** | Directories by capability dimension, dimension words are short descriptive terms |
| Dimension → file | Four-segment flat layout | No time-based bucketing, no date directories |

Pattern definitions see `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{owner_root}` | Root path of this area | `owner/` (see `layout.yaml`) |
| Dimension vocabulary | Which dimension directories can exist under root | `experience`  -  `expertise`  -  `vision`  -  `decision`  -  `collaboration` |
| `collaboration/` enabled | Build only when need to write Agent collaboration preferences | Enabled |
| `{owner_key}` | Owner identifier in metadata fields | Declared by user |
| File naming pattern | Naming for content in dimension directories | `{type}-{dimension}-{topic}-{scope}.md` |

Before adding new dimensions, confirm the existing five cannot accommodate. After adding, register in `{owner_root}CLAUDE.md`.

## ⑦ Build Procedure

To build this area from scratch, an agent interviews the owner and writes files from the answers. No code needed — the owner speaks, the agent writes.

### Interview Questions (ask one at a time)

| # | Ask | Maps to |
|---|-----|---------|
| 1 | What is your name, and what do you do? (one sentence, not a resume) | `experience/` files |
| 2 | What are you best at — and where are the edges of your competence? | `expertise/` files |
| 3 | Where are you headed in the next one to three years? | `vision/` files |
| 4 | When you make a decision, do you lean fast or lean certain? Any hard preferences the agent must always respect? | `decisions/` files |
| 5 | How do you like agents to work with you — what format, what tone, what they must never do? (skip if the owner has no preference yet) | `collaboration/` files |

### Agent Rules

- Write in the owner's own words — never rewrite into template language.
- If an answer is too thin to fill a file, ask one follow-up, then write what you have.
- If question 5 gets "I don't know yet", skip `collaboration/` entirely and note it in `CLAUDE.md`.
- After writing, print the file tree and stop. Do not move on to the next area without the owner's go-ahead.
- Every file must use a four-segment name (see naming spec) and include frontmatter.

### Build Verification

- Print the full file tree of `{owner_root}`
- Have the Agent write a short introduction using only the profile — verify it uses the user's own words, not template language
- Check against § Checklist item by item

## Related Methodology

- `../methodology/brand/` — how to write identity files, boundary between owner layer and brand identity layer, load order, how to detect person layer leakage.
- Decision and record file universal shell in `../methodology/brand/` identity file methodology: metadata → one-sentence boundary → core content → change log.

## Checklist

- [ ] Root directory contains only `CLAUDE.md` and declared dimension directories, no loose files
- [ ] Each dimension directory has its own `CLAUDE.md`
- [ ] Content files use four-segment names, no hyphens within segments
- [ ] A single fact appears in only one dimension; other places only write pointers
- [ ] Directory contains no brand operational materials (positioning, audience, channel setup, visual rules)
- [ ] No workflow soft links or implicit loads pointing to this directory
- [ ] After adding or removing dimensions, `{owner_root}CLAUDE.md` has been updated

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted skeleton from brand specification |
