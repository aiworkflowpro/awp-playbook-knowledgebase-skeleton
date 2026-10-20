---
document_id: awp-knowledge-management-standard/directory/kb-area-standards-skeleton
language: en
publication: public
title: "Knowledge Base Standards/ Directory Skeleton"
---

# Standards/ Directory Skeleton

> Defines the subdirectory structure, organization patterns used, and customization interfaces of the `{specs_root}` root directory.

## Responsibilities

Stores the rules layer: writing and development standards that Agents must follow. One standard package per directory; directory name is the package's identity.

Standards are the **rules layer**—generic, evolvable constraints, not hardcoding specific tools or cases. Operation tutorials for specific tools belong in best-practices under `{tools_root}best-practice/`.

## Directory Structure

```text
{specs_root}
├── CLAUDE.md                      ← Fixed; master entry, contains coverage matrix and quick lookup
├── layout.yaml                    ← Fixed; directory variable declaration
├── naming-map.yaml                ← Fixed; domain terms, target terms, package identity registry
├── document-index.json            ← Fixed; document index, machine-read
├── document-aliases.yaml          ← Fixed; document aliases
├── translation-state.json         ← Optional; translation status tracking
└── awp-{domain}-{target}-standard/  ← One standard package per directory
```

- Path variable `{specs_root}` is declared in `layout.yaml`, resolved as `specs/`.
- Standard package directories are flat under root, not further grouped by domain.
- Root directory contains only `CLAUDE.md` and the machine-read files listed above; no content files.

### Standard Package Directory Naming

```text
awp-{domain}-{target}-standard
```

Four segments: `awp` is fixed namespace, `{domain}` is registered domain, `{target}` is single target term, `standard` is package type. Each segment permits lowercase letters and digits only; no hyphens or underscores within segments.

Composite concepts must converge into a single clear target term; cannot stuff composite words into one slot. Domain terms, target terms, and package identities all register in `naming-map.yaml`.

Constraint nature (writing spec / development spec / reference manual / area spec) goes into the positioning one-liner in content, not directory name.

### Standard Package Internal Structure

Minimum two files:

```text
awp-{domain}-{target}-standard/
├── CLAUDE.md              ← Index, Agent entry point
└── {topic}.md             ← Rules content
```

Large standards split into multiple content files, two patterns:

| Pattern | Characteristic | Structure |
|------|------|------|
| Parallel multi-file | Each content independent, equal standing | `CLAUDE.md` + multiple `{topic}.md` |
| Master-slave multi-file | One master defines common framework, sub-files specialize by dimension | `CLAUDE.md` + master content + several sub-files |

In master-slave mode, master content must clarify division of labor with sub-files; sub-files do not repeat master's common rules, only reference.

Content files flat under package root—normal form, no need to create subdirectories just to fill space.

### Auxiliary Directories

Four optional standard subdirectories; name and content must match, do not build if no corresponding materials:

| Directory | Content | Maintenance |
|------|--------|---------|
| `reference/` | Ledgers, third-party source materials, quick-lookup cards | Living document; ledgers include review dates, periodic audit |
| `templates/` | Skeleton files, boilerplate outputs ready to copy | Update templates when main content changes |
| `assets/` | Case screenshots, reference samples, material records | Add-only, entries include source and capture date |
| `glossary/` | Term correspondence tables, vocabularies, enum ground-truth tables | New concepts enter dictionary before main content |

`reference/` and `assets/` have fixed internal form:

```text
{reference|assets}/
├── CLAUDE.md              ← Sole root entry point
└── {type_folder}/         ← Type folders only
```

Do not flat-lay business `.md` at root; all go into type folders.

Type-based sub-content directories for separate documents are rule content, not auxiliary materials, not subject to this convention.

### Out of Scope

| Content | Correct Location |
|------|---------|
| Specific tool operation tutorials, config examples, troubleshooting records | `{tools_root}best-practice/` |
| Product plans, architecture decisions | `{dashboard_root}projects/{product_name}/` |
| Business ledgers, repo inventories, operational reality | `{business_root}` |
| One-time research reports (selection analysis, competitor teardown, tech comparison) | `{dashboard_root}research/{YYYYMM}/` |
| Session drafts, abandoned plans, construction-phase plans | In-flight via `{dashboard_root}research/`, close to archive |
| Retired standards | `{inbox_root}archive/{YYYYMM}/` |

Do not create `research/` subdirectories within standard packages. Active reference ledgers go in each package's `reference/`; one-time research reports do not go in `reference/`—name-content mismatch is the start of auxiliary area corruption.

### File Naming

| File | Naming |
|------|------|
| Index file | Fixed `CLAUDE.md`, no language suffix |
| Content file | `{topic}.md`, topic name lowercase with hyphens |
| Machine-read auxiliary | `{name}.yaml` / `{name}.json`, single neutral copy, no language suffix |
| Third-party source materials | Preserve original name, no language suffix |

Filenames must reflect what they constrain; Agents must route without reading content. Prohibit name-content mismatch, prohibit Pinyin and made-up abbreviations.

Each package's `CLAUDE.md` documentation table must include a human-readable name column for quick identification.

## Organization Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → standard package | Strict four-segment package identity | `awp-{domain}-{target}-standard` |
| Within-package content | Flat layout | Root layer holds `*.md` |
| Within-package auxiliary | Fixed subdirectory names | `reference`  -  `templates`  -  `assets`  -  `glossary` |
| Within auxiliary | Type folders | Root contains only `CLAUDE.md` plus type folders |

Pattern definitions see `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{specs_root}` | Root path of this area | `specs/` (see `layout.yaml`) |
| Namespace | First segment of package directory name | Single namespace |
| Domain vocabulary | Second segment of package directory name | Registered in `naming-map.yaml` |
| Target vocabulary | Third segment of package directory name | Registered in `naming-map.yaml` |
| Package type suffix | Fourth segment of package directory name | Fixed |
| Machine-read file list | Non-package files under root | `layout.yaml`  -  `naming-map.yaml`  -  `document-index.json`  -  `document-aliases.yaml`; translation-state file source language library only |
| Auxiliary subdirectory list | Which subdirectories packages may have | `reference`  -  `templates`  -  `assets`  -  `glossary` (closed set, all optional) |
| Source language | Content language | English |
| Document identity | Cross-language identity field for each standard file | Document number in frontmatter metadata |

### Creating New Standard Package

1. Register domain and target terms in `naming-map.yaml`.
2. Create the `awp-{domain}-{target}-standard/` directory.
3. Write `CLAUDE.md` index and at least one content file.
4. Add one row to coverage matrix and subdirectory index in `{specs_root}CLAUDE.md`.
5. Build auxiliary subdirectories only when auxiliary materials exist.

### Priority Chain

When standards conflict, resolve in this order:

```text
Standard-writing standard > Domain standard > General standard > Product self-declaration
```

## ⑦ Build Procedure

Build modes: `interview` → `research` → `verify`

Standards are grown from mistakes, not planned in advance. The first session builds exactly one rule; future mistakes become future rules.

### Interview (interview)

Information to collect:

| # | Information | Required | Ask | Maps to |
|---|------------|:--------:|-----|---------|
| 1 | Naming preference | Required | How do you like files named — language, date position, separators? (show options if unsure) | `naming` standard file |
| 2 | Format rules | Optional | Any format rules for documents — headings, length, front matter? | `format` standard file (skip if no opinion) |
| 3 | Hard prohibitions | Required | What should an agent never do in this base? | House rules in root `CLAUDE.md` |

### Information Gathering (research)

| # | Search for | Sources | Output |
|---|-----------|---------|--------|
| 1 | Naming conventions in the owner's industry | Web search, open-source projects | Reference examples for the naming standard |
| 2 | Document format best practices | Industry articles, style guides | Supplement format rules if the owner was unsure |

### Live Verification (verify)

- Verification task: create the same test note twice — once named the old way the agent would have guessed, once by the new rule
- Success criteria: ① names are visibly different ② the new name follows the standard ③ the old one is deleted

### Agent Rules

- Write at most two standard files in the first session. More rules come later, from real mistakes.
- Each standard must include three concrete correct examples so the agent and the owner can verify compliance.
- From this moment, apply these standards to every file in the base, in this session and every future one.
- Add one line to the root `CLAUDE.md` house rules pointing to the standards area.
- Print the file tree and stop.

### Build Verification

- Print the full file tree of `{specs_root}`
- Confirm the verification task was run and the correct file kept
- Check against § Checklist item by item

## Related Methodology

- How standards themselves should be written—unified skeleton, section rules, lifecycle, governance, language style, library-wide alignment standards—is defined by the standard-writing standard. This skeleton only addresses what `{specs_root}` directory looks like.

## Checklist

- [ ] Root directory contains only `CLAUDE.md`, declared machine-read files, and standard package directories
- [ ] Each package directory name matches strict four-segment format
- [ ] Domain and target terms registered in `naming-map.yaml`
- [ ] Each package has `CLAUDE.md` and at least one content file
- [ ] Package `CLAUDE.md` documentation table includes human-readable name column
- [ ] Auxiliary subdirectory names in closed set, name-content match
- [ ] `reference/` and `assets/` root contains only `CLAUDE.md` plus type folders
- [ ] No `research/` subdirectory in packages
- [ ] Directory contains no tool tutorials, product plans, business ledgers
- [ ] Retired standards moved to `{inbox_root}archive/`, not remaining as active rules
- [ ] After adding or retiring packages, `{specs_root}CLAUDE.md` updated

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted skeleton from standard-writing specification |
