---
document_id: awp-knowledge-management-standard/directory/kb-area-brand-skeleton
language: en
publication: public
title: "Knowledge Base Brand/ Directory Skeleton"
---

# Brand/ Directory Skeleton

> Defines the subdirectory structure of the `{brand_root}` root, the organizational modes it uses, and its customization interface.

## Responsibilities

Stores each brand's operating identity: who the brand is, where it is going, how it makes money, who it sells to, how it speaks, how it looks, and what it says. A brand does not represent the project owner as a person, and this area does not store product operations materials.

## Directory Structure

```text
{brand_root}
├── CLAUDE.md                  ← Fixed; cross-brand entry point
└── {brand_name}/              ← One directory per brand
    ├── CLAUDE.md              ← Fixed
    ├── strategy/              ← Fixed; positioning  -  boundary  -  direction  -  architecture  -  internal understanding
    ├── operations/            ← Fixed; settled business
    │   ├── business-model/    ← Fixed; product list  -  pricing  -  path  -  growth  -  measurement
    │   ├── audiences/         ← Fixed; who to sell to
    │   └── competitors/       ← Fixed; who we face
    ├── identity/              ← Fixed; how the brand is recognized and perceived
    │   ├── expression/        ← Fixed; how it speaks and the finalized external copy
    │   ├── visual/            ← Fixed; split into rules/ and assets/
    │   │   ├── rules/
    │   │   └── assets/
    │   ├── author/            ← Optional; byline and public attribution fields
    │   └── persona/           ← Optional; only for independent character brands
    ├── content/               ← Fixed; main line  -  framework  -  channel setup  -  craftsmanship
    ├── practice/              ← Optional; the brand's own lived-practice cases
    └── exploration/           ← Optional; only for experimental brands
```

- The path variable `{brand_root}` is declared in `{specs_root}layout.yaml`.
- The four domains `strategy/`, `operations/`, `identity/`, and `content/` sit at the same level, and every brand uses the same four.
- Only `identity/visual/` subdivides further into `rules/` and `assets/`; no other domain adds a similar layer.
- Do not build empty shell directories for domains with no content; build only the domains a task actually needs, and cover the rest with a one-line pointer in `CLAUDE.md`.

### What Each Domain Answers

| Directory | Answers What | Does Not Store |
|------|---------|---------|
| `strategy/` | What the brand should be, where it is going, where its boundaries are, how to judge internally | Product lists and pricing tables |
| `operations/` | How the settled business makes money, who it sells to, who its competitors are | Candidate directions still in the scanning stage |
| `identity/expression/` | How the brand speaks, what the finalized external copy is | The project owner's own tone |
| `identity/visual/` | How the brand looks | Finished assets used by business channels |
| `identity/author/` | Who signs, which public attribution fields channels require | Voice sources and persona settings |
| `identity/persona/` | How an independent character thinks and responds | A copy of the project owner's persona |
| `content/` | What to say, how to organize it, how to configure content for each channel | The current week's schedule and capacity |

### Explicitly Out of Scope for This Area

| Content | Correct Landing |
|------|---------|
| Product definitions, pricing, membership benefits, roadmap | `{business_root}{brand_name}/products/` |
| Product R&D documentation | `{dashboard_root}projects/{product_name}/` |
| Product source code | The code repository |
| Direction scans for opportunities still being sought | `{commerce_root}` |
| The project owner's own experience, expertise, vision, and decisions | `{owner_root}` |
| The current week's schedule and capacity | `{business_root}{brand_name}/` |

## Organizational Modes Used

| Layer | Mode | Description |
|----|------|------|
| Root → Brand → Domain | **E1 Brand × Dimension** | Bucket by brand first, then expand by the four domains |
| Domain → Subdimension | Fixed vocabulary | `operations/` has three subdimensions; `identity/` has two to four |
| Domain → File | Four-segment flat | `{type}-{dimension}-{topic}-{scope}.md` |

Mode definitions: see `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{brand_root}` | The root path of this area | `brand/` (see `layout.yaml`) |
| Brand list | Which brand directories exist under the root | Declared by the user; when no brand is specified, route to the default brand |
| Default brand | Which brand to use when a workflow does not specify `profile` | Declared by the user in the root `CLAUDE.md` |
| `identity/author/` enabled | Build it only when channels need a byline or public bio fields | Off |
| `identity/persona/` enabled | Build it only for independent character brands | Off |
| `exploration/` enabled | Build it only for experimental brands | Off |
| Brand type | Personal identity brand / enterprise or media brand / product brand / service brand / sub-brand | Declared when building the brand; types can be combined |
| Image asset naming | Filename pattern under `identity/visual/assets/` | `{category}-{object}-{variant}-{spec}.{extension}` |

### Adding a New Brand

1. Create `{brand_root}{brand_name}/CLAUDE.md`.
2. Create the domains the task actually needs: `strategy/` + `operations/` + `identity/{expression,visual}` + `content/`.
3. Declare the brand type, then decide whether `identity/author/` and `identity/persona/` are needed.
4. The operations domain may start as an empty shell with a one-line pointer to the shared operations source of truth.
5. Register the brand in `{brand_root}CLAUDE.md`.

### Cross-Brand Isolation

| Rule | Description |
|------|------|
| Changes propagate within the brand only | Changing brand A does not trigger downstream checks for brand B |
| No cross-brand references | To reuse something, copy it; do not create cross-brand symlinks |
| Project owner facts are shared read-only | Read `{owner_root}` only; never copy them into any brand |
| Operations materials stay separate per brand | Audiences and competitors are not mixed in the same directory |

## ⑦ Build Procedure

To build a brand from scratch, an agent interviews the owner and writes files from the answers. The brand methodology files in `../methodology/brand/` define what each file must contain; this section defines how to get the answers.

### Interview Questions (ask one at a time)

| # | Ask | Maps to |
|---|-----|---------|
| 1 | What is this brand called? | Brand directory name |
| 2 | In one sentence, what does it do and for whom? | `strategy/` positioning file |
| 3 | Who is the audience — what hurts them, where do they gather? | `operations/audiences/` |
| 4 | How should the brand sound — technical, plain, playful, formal? Give an example sentence you like. | `identity/expression/` |
| 5 | Does this brand have a visual identity already — colors, logo, fonts? (skip if not) | `identity/visual/` |
| 6 | Does this brand sell anything right now? If yes: what, at what price, through what channel? | `operations/business-model/` |
| 7 | Who are the closest competitors? (skip if the owner doesn't know yet) | `operations/competitors/` |

### Agent Rules

- Build only the domains the answers actually fill. Empty domains stay unbuilt — never create shell directories.
- Write in the owner's voice. If the owner said "plain English, no hype", every file must reflect that.
- The brand methodology (see Related Methodologies) defines the internal structure of each file — follow it.
- After writing, generate a two-line brand-voice proof: draft a sample sentence using only what is in the base. Print it and ask the owner if it sounds right. Adjust the expression file if not.
- Print the file tree and stop.

### Build Verification

- Print the full file tree of `{brand_root}{brand_name}/`
- Have the Agent write a two-line introduction in the brand voice — verify it matches the expression file
- Check against § Checklist item by item

## Related Methodologies

- `../methodology/brand/` — Identity file shells, positioning, expression style, visual assets, audience profiles, competitor analysis, and the reference materials skeleton.
- For how to write `identity/persona/` for an independent character brand, see the persona-class methodology; this skeleton only governs whether the directory is built.

## Checklist

- [ ] The brand root contains only the four domains (plus the optional `exploration/`) and `CLAUDE.md`
- [ ] No empty shell domain directories were built
- [ ] `identity/visual/` has the two layers `rules/` and `assets/`, and no other domain has extra layers
- [ ] `identity/author/` contains only public attribution fields, no persona content
- [ ] `identity/persona/` appears only under independent character brands
- [ ] The directory holds no copies of the project owner's experience, expertise, or preferences
- [ ] The directory holds no product definitions, pricing, channel data, or deployment evidence
- [ ] Text files use four-segment names; image assets use a four-segment name plus extension
- [ ] After a brand is added, it is registered in `{brand_root}CLAUDE.md`

## Change Log

> Rolling window; keep the latest 3 entries, each ≤20 characters.

| Date | Change |
|------|---------|
| 2026-08-14 | practice/ added as optional domain |
| 2026-08-07 | Extracted skeleton from brand specification |
