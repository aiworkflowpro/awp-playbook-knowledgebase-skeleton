---
document_id: awp-knowledge-management-standard/directory/kb-area-tools-skeleton
language: en
publication: public
title: "Knowledge Base Tools/ Directory Skeleton"
---

# Tools/ Directory Skeleton

> Defines the subdirectory structure, organization patterns used, and customization interfaces of the `{tools_root}` root directory.

## Responsibilities

Stores tool **content**, not tool code: interface keys and account credentials, operation tutorials and troubleshooting records for specific tools, test fixtures used by tools.

**Knowledge base stores no code.** Command-line tools, external service wrappers, resident services all live in separate code repositories with three machines pulling same commit. Knowledge base root uses one declaration file to tell tools "credentials here, output there"; tools recognize the library by reading this declaration.

## Directory Structure

```text
{tools_root}
├── CLAUDE.md              ← Fixed; entry
├── credentials/           ← Fixed; interface keys and accounts, all flat
│   ├── CLAUDE.md
│   └── {category}-{object}-{owner}-{purpose}.md
├── best-practice/         ← Fixed; specific tool tutorials
│   ├── CLAUDE.md
│   └── {domain}-{tool}-{level}-{status}/
└── {test_fixtures}/       ← Optional; materials for tool testing
```

- Path variable `{tools_root}` is declared in `{specs_root}layout.yaml`, resolved as `tools/`.
- Root directory contains only `CLAUDE.md` and subdirectories listed above.
- Test fixtures follow tools, not in business brand directories.

### `credentials/`

```text
credentials/
├── CLAUDE.md
├── account-{object}-{owner}-{purpose}.md
├── cloud-{object}-{owner}-{purpose}.md
└── ...
```

Three hard constraints:

- **All flat**, no subdirectories.
- **Only `.md`**, one credential per file.
- Ground truth only here; distributed tools or capability packages contain templates or declarations only, not actual values.

After credential expires, move entire file to `{inbox_root}archive/{YYYYMM}/`, not delete in-place.

### `best-practice/`

One tool per directory, four-segment directory name:

```text
{domain}-{tool}-{level}-{status}/
```

Example: `agent-claudecode-app-live`. Entry short-names (like `overview/`) may omit hyphens.

Internal structure splits by main document count into three skeleton levels:

| Level | Main Docs | Structure |
|------|---------|------|
| Single-file | One | `CLAUDE.md` + one tutorial |
| Standard | Two | `CLAUDE.md` + main tutorial + independent sub-topic |
| Complex | Three+ | `CLAUDE.md` + multiple content + optional subdirectories |

Main document count is root-level `.md` only; attachments don't count. Root-level content uniformly uses four-segment naming `{dir-id}-{purpose}-{topic}-{scope}.md`; entry file fixed as `CLAUDE.md`, no renaming.

Any level can stack fixed auxiliary subdirectories; names are closed set, no custom creation:

| Subdirectory | Content |
|--------|--------|
| `configs/` | Config originals, container orchestration, service definitions, database schemas, API contracts, templates |
| `scripts/` | Executable scripts; patches go in `scripts/patches/` |
| `programs/` | Multi-file small programs or plugins, one project per subdirectory plus explanation file |
| `samples/` | Sample data, requests and responses, log samples, error code tables |
| `assets/` | Screenshots, charts, screen recordings, audio, fonts, themes |
| `projects/` | Supplementary resources for hands-on projects |
| `legacy/` | Old docs and attachments |
| `archive/` | Archived versions |

Main documents must explicitly reference each auxiliary item, explaining what it is and when to use it. Unreferenced attachments are orphans to be cleaned up. Attachments cannot be placed outside `best-practice/` or substitute for required sections.

### Boundary Between Standards and Best-Practices

| | Standards (`{specs_root}`) | Best-Practices (`{tools_root}best-practice/`) |
|---|---|---|
| Nature | Rules, constraints, checklists, not bound to specific tools | Operation tutorials, config examples, troubleshooting records, bound to specific tools |
| Criterion | Swap machine or tool, rule still applies | Only applies to specific tool or version |
| Level | Upper, constraints best-practices | Lower, constrained by standards |

Best-practices can say "general rules constrained by some standard," but don't define general rules themselves. Standards don't reference specific best-practice paths as ground truth.

## Organization Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → subdirectory | **E3 Functional responsibility** | Fixed structure, not time-driven growth |
| `credentials/` | Flat layout | One credential per `.md`, no subdirectories |
| `best-practice/` | **A3 Best-practices four-segment** | `{domain}-{tool}-{level}-{status}/` |
| Best-practices auxiliary | Fixed subdirectory names | Closed set, no custom creation |

Pattern definitions see `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{tools_root}` | Root path of this area | `tools/` (see `layout.yaml`) |
| Subdirectory list | Which subdirectories under root | `credentials`  -  `best-practices` required; test fixtures as needed |
| Credential file naming | Filenames under `credentials/` | `{category}-{object}-{owner}-{purpose}.md` |
| Credential category vocabulary | First segment of filename | Defined and registered by user in `credentials/CLAUDE.md` |
| Best-practices four-segment vocabulary | Domain, tool, level, status values | Controlled vocabularies defined by best-practices methodology |
| Auxiliary subdirectory list | Allowed subdirectories in tutorial package | `configs`  -  `scripts`  -  `programs`  -  `samples`  -  `assets`  -  `projects`  -  `legacy`  -  `archive` (closed set) |
| Library declaration file | Which file tools use to recognize library | Declaration file at knowledge base root, specifies credentials directory and output directory |
| Sync surface | Which machines participate in sync | Declared by user; adding public network node equals handing over entire credential set |

## Related Methodology

- `../methodology/tools/` — credential file section skeleton and parse contract, best-practices tutorial three-level skeleton and required sections, auxiliary extraction threshold, multi-host organization, versions and lifecycle.

## Checklist

- [ ] Root directory contains only `CLAUDE.md` and declared subdirectories
- [ ] Directory contains no code repositories
- [ ] `credentials/` entirely flat, no subdirectories, only `.md`
- [ ] Expired credentials moved to `{inbox_root}archive/`, not in-place deleted
- [ ] Each best-practices directory name matches four-segment format
- [ ] Tutorial package entry file named `CLAUDE.md`, root-level content uses four-segment naming
- [ ] Auxiliary subdirectory names in closed set
- [ ] Each auxiliary explicitly referenced by main document, no orphans
- [ ] Tutorials contain no custom general rules, only reference standards
- [ ] Test fixtures in `{tools_root}`, not in business area

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted skeleton from tools and credentials specification |
