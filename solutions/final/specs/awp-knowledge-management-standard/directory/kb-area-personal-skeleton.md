---
document_id: awp-knowledge-management-standard/directory/kb-area-personal-skeleton
language: en
publication: public
title: "Knowledge Base Personal/ Directory Skeleton"
---

# Personal/ Directory Skeleton

> Defines the subdirectory structure, organization patterns used, and customization interfaces of the `{personal_root}` root directory.

## Responsibilities

Stores facts and decisions from private life: documents, legal matters, health, growth, investments, home, leisure, personal business entities. Content here is private by default and does not enter any external output.

## Directory Structure

```text
{personal_root}
├── CLAUDE.md          ← Fixed; entry
├── credentials/       ← Optional; person-based subdirectories
│   └── {person_name}/
├── legal/             ← Optional; copyright and evidence two types
├── health/            ← Optional; sleep, exercise, diet, checkups
├── growth/            ← Optional; reading, learning, reflection
├── investment/        ← Optional; investments, insurance, major decisions
├── home/              ← Optional; equipment, smart home, maintenance
├── leisure/           ← Optional; film, travel, food, hobbies
└── business/          ← Optional; personally operated entities
```

- Path variable `{personal_root}` is declared in `{specs_root}layout.yaml`, resolved as `personal/`.
- Eight domains are peer-level, all optional: when empty, can contain only `CLAUDE.md`.
- Do not create empty shell files. When starting to write content in a domain, then add its required files.
- `documents/` has person-based subdirectories below; other domains do not have a third layer.

### Eight Domains Overview

| Dimension | Subdirectory | When to read |
|------|--------|-----------|
| Documents | `documents/` | Document lookup, visa application, identity verification |
| Legal | `legal/` | Copyright protection, consumer rights, evidence |
| Health | `health/` | Exercise guidance, checkup interpretation, sleep planning |
| Growth | `growth/` | Reading recommendations, learning plans, phase reflection |
| Finance | `investments/` | Investment decisions, insurance planning, major purchase retrospective |
| Home | `home/` | Equipment purchase, home renovation, maintenance reminders |
| Leisure | `leisure/` | Film recommendations, travel planning, hobby depth-building |
| Business | `business/` | Management of personally operated entities |

### Privacy Levels

Each active personal document must declare its privacy level in metadata. Only `CLAUDE.md` and empty domains without content are exempt.

| Level | Meaning | Handling |
|------|------|---------|
| Public | No sensitive personal information | Can be used by tools and full-text search |
| Internal | Personal preferences, unwilling to disclose but available within knowledge base | Can be used internally and full-text search |
| Sensitive | Involves specific numbers, health details, relationship details | Direct read only when task explicitly needs it, not proactively summarized |
| Restricted | Highly sensitive, legal or compliance risks | Not written to knowledge base, use encrypted notes instead |

Determination order: first check if content involves specific numbers, health details, financial amounts, relationship privacy. If not, it's public or internal. If so, then check if disclosure would cause legal, compliance, or major privacy risk. If not, it's sensitive; if so, it's restricted.

### External Publication Isolation

Agents must prohibit extracting or referencing content from `{personal_root}` when executing any external publication operation. External publication includes releasing toolkits, open-source repos, articles, social posts, tutorials, product docs, official website content.

Specific constraints:

- Do not reference internal-level or above content from this area in external output.
- Do not embed names, relationships, finance, health, addresses, document info in code, comments, sample data, or documentation.
- Do not hardcode paths to this area or file references in externally published prompts, workflows, or capability packages.
- Single exception: when person explicitly instructs referencing specific public-level content, can use one-off; no persistent reference forms.

### Three Content Types

| Type | Characteristic | Review Frequency |
|------|------|---------|
| Decision | Long-term validity, impacts multiple future behaviors | Quarterly review, update or archive when expired |
| Record | Snapshot of specific point in time | Periodic production, archive across years |
| Reference | Checklists, reminders, materials | Change only when content changes |

Within same domain, strategy and data should be separated: sleep, exercise, diet, home plans are decision type; checkups, medications, equipment inventory are record or reference type.

### Explicitly Out of Scope

| Content | Correct Location |
|------|---------|
| Creative materials | Research area or reference materials root |
| Published courses or product definitions | Brand and business areas |
| Interface keys and account credentials | `{tools_root}credentials/` |
| Home lab deployment technical details | `{tools_root}best-practice/` |
| Video production process files | `{business_root}` |
| Account ledgers | External accounting app, not knowledge base |
| Passwords, recovery codes, complete medical history | Encrypted notes, not any location in knowledge base |

## Organization Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → domain | **E3 Functional responsibility** | Short descriptive phrases, fixed structure |
| `documents/` → person | Person-based bucketing | One person per subdirectory |
| Domain → file | Flat layout | Record-type filenames include year or issue number |

Pattern definitions see `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{personal_root}` | Root path of this area | `personal/` (see `layout.yaml`) |
| Domain vocabulary | Which domain directories can exist under root | documents  -  legal  -  health  -  growth  -  investments  -  home  -  leisure  -  business |
| Each domain enabled | Build only when has content | All optional; empty domains contain only `CLAUDE.md` |
| Lifestyle type | single / partnered-cohabiting / nuclear-family / multigenerational / digital-nomad / phase-specific-special-state | Declared by user, can stack, determines which optional sections take effect |
| Privacy default level | Default privacy level for files in each domain | Health and investments default sensitive, others default internal |
| Document naming | Filenames under `documents/{person_name}/` | Defined by methodology |
| Review frequency | How often decision-type files are reviewed | Quarterly |

## Related Methodology

- `../methodology/personal/` — three types (decision, record, reference) file section skeletons; document, financial voucher, legal document naming conventions; required file lists for health and home domains; archive policy.

## Checklist

- [ ] Root directory contains only `CLAUDE.md` and declared domain directories
- [ ] Empty domains contain only `CLAUDE.md`, no artificially created empty shell files
- [ ] Each active content file has privacy level declared
- [ ] Restricted-level content is not in any location in knowledge base
- [ ] Sensitive-level content not proactively summarized
- [ ] External output contains no references to this area
- [ ] Decision-type files have review dates
- [ ] Record-type files are date-stamped annually, archived across years
- [ ] Creative materials, product definitions, deployment tech, credentials not in this area

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted skeleton from life specification |
