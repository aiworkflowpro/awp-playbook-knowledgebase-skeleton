---
document_id: awp-knowledge-management-standard/methodology/tools/kb-method-practice-authoring
language: en
publication: public
title: "Best Practice Authoring Methodology"
---

# Best Practice Authoring Methodology

> Manage one thing: how to write tool-class tutorial documents — unified skeleton, chapter requirements, multi-carrier organization, version lifecycle, and maintenance rules.
> Applies to tutorial documents for tools, systems, or software in any industry.
> Doesn't manage how a specific tool is configured (that's written in each tool's own document), nor secret values and parsing (that's credential management methodology).

## Responsibility

Tutorial best practice is the tool's **reproducible deployment tutorial + complete runnable asset package** — a newcomer or a new machine follows it through once to fully deploy and understand why each step is done this way. At the same time it is a daily operation reference and the source material library for complete external tutorial output.

### Relationship with Specification

Best practice is the **operation tutorial layer**, constrained by the specification (upper layer constrains lower). Best practice writes hardcoded operation steps, config examples, and pitfall records for a specific tool or scenario; the specification writes cross-tool universal structural requirements and constraints.

- Best practice may write "universal rules are constrained by such-and-such specification" — acknowledging jurisdiction from the upper layer.
- Best practice **must not self-define universal normative rules** (cross-tool "must" / "must not" should be distilled into the specification).
- Best practice **must not restate specification content** — when citation is needed, only a pointer.

## Ten Design Principles

- **Reproducibility First** — the ultimate acceptance standard is: a new environment follows through and runs. Documents that fail this are unqualified.
- **One Tool One Folder** — regardless of file count, each tool occupies one exclusive folder; even with a single body file, reserve room to extend.
- **Dual-Layer Design** — scattered tool-class information (each tool independent) + concentrated comprehensive information (deployment overview centralized), single source, mutual references, no drift.
- **Complexity-Driven Skeleton** — don't force simple tools into long documents, don't allow complex platforms to be a single sentence.
- **Progressive Teaching** — tiered from novice to mastery, each tier has explicit goals and acceptance standards.
- **Each Step Verifiable** — every operation step must come with expected output; the reader can judge whether they did it right. A step without expected output is incomplete.
- **Pitfall as Asset** — pitfall records and novice misconceptions are the most valuable parts of the document; next time the same problem appears, look it up directly.
- **Multi-Carrier First-Class** — text, code, config, script, program, sample, media, and external links are equal; don't force everything into Markdown.
- **Truth Priority** — configs and scripts that can be preserved as-is must be preserved as-is (including comments, blank lines, indentation), **forbid describing config in prose**.
- **Credential Zero Drop** — best practice files forbid plaintext passwords, keys, or tokens; uniformly use the credential reference form.

## Three-Level Skeleton

Choose the skeleton by the count of body files. **The count counts body files only, not files under attachment subdirectories**:

| Level | Applicable scenario | Body count | Judgment standard |
|------|---------|:------:|---------|
| **Lightweight** | single config or command quick reference | 1 | 20 config items or fewer, no architecture explanation needed |
| **Standard** | complete tool with deployment, config, and operations | 1-2 | has a deployment flow, has running state to manage |
| **Complex** | platform-level tool where multiple aspects need independent documents | 3 or more | multiple subsystems, multiple config dimensions, needs separate files |

```text
# Lightweight
{four-segment tool directory}/
├── CLAUDE.md
└── {directory-id}-tutorial-{topic}-{scope}.md      ← single file contains everything

# Standard
{four-segment tool directory}/
├── CLAUDE.md
├── {directory-id}-tutorial-{topic}-{scope}.md      ← main tutorial
└── {directory-id}-{purpose}-{topic}-{scope}.md     ← optional: independent subtopic

# Complex
{four-segment tool directory}/
├── CLAUDE.md                              ← routing only
├── {directory-id}-{purpose}-{topic}-{scope}.md
├── {directory-id}-{purpose}-{topic}-{scope-or-date}.md
└── {subdirectory}/                        ← optional
```

The entry file is uniformly `CLAUDE.md` (routing + boundary + file index + change log); no alias entry created. Root-layer bodies uniformly use the four-segment name; headings continue to use natural language, not copying the filename structure.

### Attachment Extension Skeleton

On top of the three-level skeleton, any level may stack a fixed attachment subdirectory:

```text
{four-segment tool directory}/
├── CLAUDE.md
├── {directory-id}-tutorial-{topic}-{scope}.md  ← main document, must explicitly reference every attachment
├── configs/             ← config originals, container orchestration, system service units, database structures, interface contracts, templates
├── scripts/             ← executable scripts, patches in scripts/patches/
├── programs/            ← multi-file mini programs or plugins, one subdirectory per project + description file
├── samples/             ← sample data, test fixtures, request/response, log samples, error code tables
├── assets/              ← screenshots, diagrams, videos, audio, fonts, themes
├── projects/            ← hands-on project companion resources (code templates, starter files)
├── legacy/              ← old versions of documents + attachments
└── archive/             ← archived versions
```

- Subdirectory names are **fixed** to the eight above, inventing new ones is forbidden.
- The main document must explicitly reference every attachment (state purpose + when to use); unreferenced attachments are **orphans**.
- Attachments **do not count** toward the body file count.
- Forbid placing attachments anywhere outside the best practice directory.
- Forbid using attachments to replace mandatory chapters — attachments are supplements, not substitutes.

### Multi-Host and Multi-Environment

When the same tool deploys to multiple hosts or environments, choose one of two methods by scale, **forbid mixing**:

**① Suffix naming** (3 hosts or fewer): `{filename}.{environment}.{host alias}`

**② Host subdirectory** (more than 3 hosts, or big config differences): one subdirectory per host, and the root must have a host mapping table:

```markdown
| Host | Environment | Role | Address | Config directory |
|------|------|------|------|---------|
```

Host aliases match real host names, no invented codes. In suffix naming mode, the main document's "Basic Information" table must list all hosts.

## Content Carrier Tiering

Best practice is not just Markdown text; it is a **multi-carrier asset package**.

| Category | Subtype | Default destination | Extraction threshold |
|---|---|---|---|
| **① Text** | paragraphs, tables, lists, text diagrams | embedded in main document | — |
| **② Code snippet** | inline commands, short examples | embedded code block | 30 lines or fewer and no need for verbatim reuse |
| **③ Config file** | service config | `configs/` | 30+ lines, or verbatim reuse needed, or a real running file |
| | environment and credential templates | `configs/` + desensitized placeholders | any environment file with variables |
| | containers and orchestration | `configs/` | any |
| | system service units, scheduled configs | `configs/` | any |
| | database structures and migrations | `configs/` or `samples/` | any |
| | interface contracts | `configs/` | any |
| | non-secret certificates, render templates | `configs/` | any |
| **④ Scripts and programs** | shell scripts | `scripts/` + interpreter declaration + comment header | any executable |
| | single-file tools | `scripts/` | any |
| | multi-file mini programs | `programs/{project-name}/` | any multi-file program |
| | patches | `scripts/patches/` | any |
| | key mappings | `configs/` | any |
| | automation orchestration | `programs/` or `configs/` | any |
| **⑤ Sample data** | input/output, test fixtures, error code tables, packet captures | `samples/` | any real data needing reproduction |
| **⑥ Media** | text architecture diagrams | embedded in main document | **preferred** |
| | screenshots, diagrams | `assets/` + semantic filenames | when necessary |
| | video, screen recording, audio | `assets/` or external link | over 5 MB goes external link |
| **⑦ External link resources** | official docs, repos, images | link in main document | everything that can't be stored in the vault |
| | large files | external link + checksum | over 1 MB must go external link |

### Extraction Decision

```text
Is this content pure description or discussion?
├── Yes → embed in main document (text/table/list)
└── No → needs verbatim reuse (copy-paste and it runs)?
         ├── No → embedded code block
         └── Yes → is it a script or program?
                  ├── Yes → scripts/ or programs/
                  └── No → is it config?
                           ├── Yes → configs/
                           └── No → data → samples/  | media → assets/
```

### Config Snapshot Rhythm

| Change type | Handling |
|---------|---------|
| small change (tuning params, editing comments, adding rules) | overwrite the original file directly, update the "last verified date" in the header comment |
| big change (structural, incompatible, cross-major-version) | keep the old snapshot in `legacy/configs/` with a date suffix, new file goes to `configs/` |
| temporary debugging | don't commit to the vault; decide whether to distill after debugging |

Snapshot naming keeps the original filename plus the archive date suffix.

### Positive and Negative Comparison

| Good | Bad | Reason |
|---|---|---|
| 70-line config extracted to `configs/`, main document writes a one-line pointer | main document writes "the config roughly has three parts, first A then B......" | the former is copy-paste ready, the latter loses truth |
| start/stop script in `scripts/` with interpreter declaration and header comment | main document writes "start it with shell, the command is roughly......" | the former is reusable and auditable |
| multi-file mini tool in `programs/{project-name}/` with its own description | scattered source files dumped at the `configs/` root | the former is migratable and independently runnable |

### Script Directory Boundary

- Scripts under `scripts/` are the tool's **reference assets** — showing "how to use this tool", for copying to target hosts to run.
- They are **not** the knowledge base's runtime entry, not constrained by global script running rules.
- They will not be executed automatically by the knowledge base's continuous integration or maintenance tasks.

## Eight Mandatory Chapters

| Skeleton | Requirement |
|------|------|
| **Lightweight / Standard** | the main file must contain the eight chapters in the table below; order can be slightly adjusted, chapter responsibilities cannot be missing |
| **Complex** | the entry does routing only; each dimension document writes by its own responsibility, not forced to have all eight; **at least one** deployment or lifecycle document covers "can run + can self-test" |

| # | Chapter | Format | Description |
|---|------|------|------|
| 1 | title + one-sentence positioning + selection rationale | H1 + blockquote + bold paragraph | what the tool does + why it was chosen |
| 2 | status annotation + tutorial metadata | multi-line blockquote | status, version, date, credential + difficulty, duration, audience, prerequisites |
| 3 | basic information | table | access address, port, version, account, host and other core runtime parameters |
| 4 | prerequisites | table (with check command + expected output) | system, software, hardware, network requirements |
| 5 | deployment tutorial | progressive tiering | complete steps from zero to deployment, each step has expected output |
| 6 | complete config inventory | table + config directory reference | all config files list and their purposes |
| 7 | pitfalls and common misconceptions | two tables | ops pitfalls + novice misconceptions |
| 8 | self-test commands | code block + expected output | one-click verify the tool runs normally |

### ① Title + One-Sentence Positioning + Selection Rationale

- One sentence within 40 characters, stating "what this tool does".
- Selection rationale 1-3 sentences: what problem it solves + how it's better than alternatives + its position in your own system.
- Forbid omitting the one-sentence positioning — the Agent needs to quickly judge whether this is the target document.
- Forbid writing a selection thesis — the rationale is no more than 100 characters.

### ② Status Annotation + Tutorial Metadata

**Status fields**:

| Field | Mandatory | Meaning |
|------|:---:|------|
| Status | required | trial / current / legacy / archived |
| Version | required | the tool version described by the document |
| Last updated | required | the date of any text change in the document (writing dimension) |
| Last verified | required | the date a full run-through per the document confirmed it still works (runtime dimension) |
| Supersedes | conditionally required | which old version it replaced (when the current version has a predecessor) |
| Superseded by | conditionally required | what replaced it (legacy and archived must fill) |
| Related | optional | paths of related tools or alternatives |
| Credential | conditionally required | mandatory when sensitive info exists, points to the credential directory |
| Belonging deployment stack | optional | points to the collaboration document in the overview layer |

**Tutorial metadata fields**:

| Field | Mandatory | Meaning |
|------|:---:|------|
| Difficulty | required | five tiers: novice / intermediate / advanced / expert / master |
| Estimated duration | required | estimated total time to complete the whole tutorial from zero |
| Prerequisites | required | skills the reader needs in advance, specific to tool or concept |
| Target audience | required | one sentence describing who this tutorial is for |
| Course affiliation | optional | which paid course it belongs to; leave empty when not affiliated |

**Difficulty tiers**:

| Difficulty | Typical reader |
|------|---------|
| Novice | zero basics, first contact with the command line |
| Intermediate | knows the command line but hasn't used this tool |
| Advanced | has used similar tools, needs deep config |
| Expert | proficient user, needs advanced usage and tuning |
| Master | needs underlying understanding and custom development |

**"Last updated" and "Last verified" are two different things**:

| Date | When to update | Purpose |
|------|-----------|------|
| Last updated | any modification to the document text | track writing activity |
| Last verified | ran through the document and passed | trigger timeliness checks |

Fixing a typo and updating "last verified" resets the countdown for nothing.

### ③ Basic Information

A table, at least containing the tool's core runtime parameters. Common fields for different tool types:

| Type | Common fields |
|------|---------|
| Service | access address, port, account, version, host |
| Command line | install method, config file location, version |
| Desktop app | version, config path, shortcuts |
| Infrastructure | address, role, deployment path |

Sensitive info uses credential reference placeholders. In multi-host deployment, the table must list all hosts, or point to the host mapping table.

### ④ Prerequisites

All tools must state prerequisites. The table must include **check command** and **expected output**:

```markdown
| Item | Requirement | Check command | Expected output |
|----|------|----------|----------|
| System | {version requirement} | {command} | {what should be seen} |
```

- Every row must have a check command and expected output — the reader executes it and knows whether it's satisfied.
- Dependent tools point to the corresponding best practice document by path.
- Forbid vague descriptions like "need some basics" — be specific about which commands or concepts.

### ⑤ Deployment Tutorial

This is the **core chapter** of a tutorial best practice, organized by progressive tiers:

```markdown
## Deployment Tutorial

### Level 1  -  {topic}({estimated duration})

**Goal**: {one sentence on what the reader can do after this level}

**Steps**:

**1.1 {step name}**

{command or operation}

> **Expected**: {what should be seen after executing}

**1.2 {step name}**

...

**Level 1 Acceptance**:
- [ ] {acceptance item 1}
- [ ] {acceptance item 2}
```

**Tiering rules**:

| Level | Meaning | Positioning | Mandatory |
|------|------|------|:---:|
| Level 1 | novice | minimal usable path, just make it run | required |
| Level 2 | daily | full coverage of core daily operations | required |
| Level 3 | advanced | advanced usage, performance tuning, automation | optional |
| Level 4 and above | expert | hidden tricks, underlying principles, extreme scenarios | optional |

**Mandatory constraints**:

- Levels 1 and 2 are required; Level 3 and above are optional by tool complexity.
- Every Level must have four elements: **goal** (one sentence) + **steps** (numbered) + **expected output** (blockquote) + **acceptance checklist** (checkboxes).
- Each step is followed directly by an expected output blockquote.
- Step number format `{Level}.{Step}`.
- One Level is no more than 60 minutes — split into two if exceeded.
- Forbid skipping steps — Level 2 cannot assume the reader skipped a Level 1 step.
- Forbid giving commands without expected output.

Short expected output uses inline format, long expected output uses a code block.

### ⑥ Complete Config Inventory

List the complete inventory of all the tool's config files; these files live in the config directory and can be copied directly to the target host for deployment.

```markdown
| File | Purpose | Deployment path | Key config notes | Contains credentials |
|------|------|----------|-------------|:------:|
```

- Every config file is **saved in full as-is** in the config directory.
- The config file's top comment header writes: purpose / version / last verified date / related credential.
- Sensitive fields uniformly use credential reference placeholders.
- Use the "Contains credentials" column to mark which files need placeholder replacement.
- Tools without config files write "no external config files" in this chapter.

### ⑦ Pitfalls and Common Misconceptions

Two dimensions written separately:

```markdown
### Ops Pitfalls

| Problem | Cause | Solution |
|------|------|----------|

### Novice Misconceptions

| Misconception | Correct understanding | Why it matters |
|------|----------|-----------|
```

- Both use three-column tables; prose descriptions are forbidden — tables are scannable and appendable.
- When a reusable fix has been distilled into a script, reference the script path in the solution column.

### ⑧ Self-Test Commands

Every tool must provide self-test commands, one-click verify normal operation. Must include expected output — it directly supports re-checking the "last verified" field.

## Optional Chapters

"Conditionally required" ones upgrade to required when the trigger condition appears:

| Chapter | Applicable scenario |
|------|---------|
| Architecture | systems with multiple components or devices, use text architecture diagrams |
| Uninstall and rollback | **mandatory for tools with deployment steps**: cleanup commands + residue checks |
| Device and node inventory | systems deployed on multiple devices |
| Subsystems and modules | tools with multiple independent sub-features |
| Integration and linkage | has linkage relationships with other tools |
| Migration records | has undergone migration or upgrades |
| Version history | old and new versions coexist |
| Interface operations | tools with programmable interfaces |
| Related tools | substitute or complementary relationships with other best practices |
| Hands-on projects | needs to string multiple knowledge points into a complete task |
| Learning path | needs to string together a course system |
| Companion resources | **mandatory when any attachment subdirectory exists**: table listing all attachments |

**Hands-on projects** each must have: difficulty + duration + what's learned + steps + final effect; companion resources go in `projects/`, 1-3 items, don't be greedy.

**Learning path** presents in both text diagram and table form; subsequent recommendations must point to concrete document paths.

**Companion resources** unified format:

```markdown
| Path | Category | Purpose | When to use |
|------|------|------|---------|
```

## Attachment File Rules

**Config files**: keep the original extension; the top comment header writes source, version, last verified date, related credential; multiple files of the same type use environment and host suffixes in naming; sensitive fields use credential reference placeholders; forbid writing real keys.

**Script files**: must have an interpreter declaration; the header comment includes purpose, prerequisites, example invocation, last verified date; shell scripts must start in strict mode; patches uniformly go to the patch subdirectory.

**Multi-file programs**: each project occupies one subdirectory with its own description file (purpose, installation, usage); those with dependencies write a dependency list; over 5 MB goes external link.

**Hands-on projects**: each project occupies one subdirectory with its own description file (goal, starter code description, completed code comparison), containing starter code and completed code; **forbid credentials**, use environment templates with placeholders.

**Sample data**: must be desensitized (personal info, tokens, real domains replaced); the file header or a sibling description file marks collection time, source, purpose; over 1 MB goes external link.

**Media files**: architecture diagrams prefer text diagrams embedded in the main document; image filenames are semantic and include the date; the main document references by relative path; videos over 5 MB go external link.

**External link resources**: give the full address + purpose + last reachable date; key external links attach a checksum or commit hash against drift.

**Forbid replacing text architecture diagrams with images** — the Agent can't read images.

## Credential Separation

Uniformly use the reference form defined by the credential management methodology:

```text
<see credentials/{credential file}.md §Authentication Info  -  {field}>
```

Application across carriers:

| Carrier | Writing form |
|------|------|
| main document command | embed the reference form directly in the command |
| config file | `KEY=<see credentials/...>` |
| script | `export TOKEN="<see credentials/...>"` |
| environment template | `PASSWORD=<see credentials/...>` |

**Iron laws**:

- All carriers use the same reference form, same source as the credential management methodology.
- The "Complete Config Inventory" table uses the "Contains credentials" column to mark which files need replacement.
- Forbid any real key, token, or password in any file.
- Forbid non-standard placeholders like `xxx`, `your-token`, `<REDACTED>` — they can't be replaced automatically.
- Commands involving credentials in deployment tutorial steps use the standard placeholder too, and the step description prompts to get the real value from the credential directory.

## Version and Lifecycle

### Four Statuses

| Status | Meaning | Usage scenario |
|------|------|---------|
| **Trial** | exploring, not yet verified production-ready | new tool tryout, new solution comparison |
| **Current** | in service, the default recommended solution | in production (default status) |
| **Legacy** | was in service, replaced by a newer version, kept for reference and rollback | new/old coexistence period, old machines still running |
| **Archived** | fully retired, no longer maintained, history only | tool decommissioned, solution fully abandoned |

```text
trial → current → legacy → archived
        ↑       │
        └───────┘  (when a newer version demotes to legacy)
```

- Any status change must update the status annotation and append one line to the change log.
- Forbid skipping legacy and going straight to archived (unless the solution never reached production).
- The current version may exceptionally fall back to trial (big changes need re-verification); must note the deviation reason.

### Change Log Applicability Matrix

| Document type | Needs change log? | Reason |
|---------|:--------------:|------|
| Main tutorial document | **required** | tutorials keep evolving, need to track major changes |
| Config guides and deployment manuals | **required** | equivalent to the tutorial type |
| Research and planning documents, dated snapshots | may omit | one-off outputs, the point in time is already expressed by filename or metadata |
| Evaluation test papers and results | not needed | data snapshots, archived once written, don't evolve themselves |
| One-off attachments or incident records | may omit | covered by the main document's change log |

Judgment decision tree:

```text
Will this document keep being modified or get new sections in the future?
├── Yes → must have a change log
└── No → is it a snapshot of a point in time?
         ├── Yes → not needed
         └── No → may omit
```

### Multi-Version Coexistence

```text
# New and old coexist
{four-segment tool directory}/
├── CLAUDE.md            ← default entry
├── {body four-segment name}.md      ← current version
├── configs/             ← current version attachments
└── legacy/
    ├── {body four-segment name}.v1.md  ← old version complete document
    └── configs/            ← old version attachments archived in the same directory

# Multi-version archived
{four-segment tool directory}/
├── CLAUDE.md            ← version overview + recommended path
├── {body four-segment name}.md      ← current version
├── legacy/
│   ├── {body four-segment name}.v2.md
│   └── {body four-segment name}.v1.md
└── archive/
    └── {body four-segment name}.{year}.md
```

- The current version always sits at the tool directory root with the body four-segment name; old versions move down to `legacy/`.
- Old version documents must state in the first paragraph "why it was replaced" + "scenarios still worth reading".
- Forbid `new`, `old`, `latest`, `final` as filename segments.
- `legacy/` holds what may still be looked up, `archive/` holds what is fully sealed.
- With 3 or more versions, the entry file must have a version quick-reference table:

```markdown
| Version | Status | Path | Applicable scenario | Last verified |
|------|------|------|---------|---------|
```

### Migration Trigger Conditions

**current → legacy**:

| Trigger condition | Action |
|---------|------|
| new solution passed production verification for two full weeks | old solution demoted to legacy, new solution enters the root-layer body |
| tool officially incompatible major version and already upgraded | old version sinks to `legacy/` |
| tool completely replaced by another tool | whole directory demoted to legacy, pointing to the new tool |

**legacy → archived**:

| Trigger condition | Action |
|---------|------|
| no machine runs the solution | move to `archive/` |
| "last verified" over 365 days | same as above |
| tool officially stops maintenance | same as above |
| solution has a serious flaw | archive immediately and add a warning |

## Directory and File Naming

### Folder Four-Segment Format

```text
{domain}-{tool}-{tier}-{status}/
```

| Segment | Answers what | Value range |
|---|---------|---------|
| **domain** | what field | shared domain term list with credentials |
| **tool** | which tool | official tool name, run together within the segment, no hyphens |
| **tier** | which layer of the tech stack | `base` (infrastructure layer, other tools depend on it) / `app` (application layer, the main tool used directly) / `platform` (platform layer, external or third-party service) / `util` (auxiliary layer, ops, monitoring, troubleshooting) |
| **status** | lifecycle | `live` (in use) / `eval` (evaluating) / `idle` (low maintenance or replaced but kept) / `stub` (migration stub, content moved away) |

| Rule | Level |
|------|:----:|
| exactly three hyphens separating four segments | required |
| lowercase letters + hyphens between segments | required |
| run together within the segment, no hyphens | required |
| all four segments present, none missing | required |
| domain from the controlled term list, new domains must be registered | required |
| tier and status each from their four values | required |
| Non-ASCII directory names | forbidden |
| numeric prefix | forbidden |

Multi-tool collaboration overview directories keep their original names, no four-segment prefix — they are not single-tool tutorials.

### Body File Four-Segment Format

```text
{directory-id}-{purpose}-{topic}-{scope-or-date}.md
```

| Segment | Content to fill | Rule |
|----|---------|------|
| directory-id | second segment of the parent directory | use the existing lowercase English identifier |
| purpose | what the document is responsible for | choose only from the controlled term list |
| topic | concrete object or problem | short descriptive phrase or necessary proper name, no hyphens within the segment |
| scope-or-date | applicable environment, object, or time | long-lived documents write scope; time snapshots write `YYYYMMDD` |

Purpose controlled term list:

```text
overview tutorial deployment configuration extension architecture operations security troubleshooting
plan research evaluation checklist template reference
```

- The filename only expresses retrieval identity; the H1 continues to use natural language.
- "general" is only for long-lived documents truly not limited by host, environment, and date.
- Official proper names with hyphens use compact or camelCase writing.
- The third segment doesn't write redundant words like "best practice", "usage guide", "main document".
- The fourth segment doesn't write relative statuses like "latest", "final", "v2".
- Don't copy the parent directory's domain, tier, and status into the body filename.
- The fixed entry file doesn't get renamed.
- Attachment directories keep their real identity, named by each attachment rule.

### Entry File

Every four-segment tool directory must have an entry file, no exemption by body count. The entry only indexes, holds no body content.

| Chapter | Mandatory | Content |
|------|:----:|------|
| One-line positioning | required | blockquote, one sentence stating what this directory is |
| File index | required | main document + each dimension body, one file per line |
| Trigger words | optional | tool name + aliases + core function keywords |
| Boundary | optional | division of labor with adjacent tools or specs |
| Change log | optional | special allowance |

- Capacity 40-80 lines, indexing and routing only.
- The chapter name is uniformly "File Index", no synonym titles.
- The file index uniformly uses the two-column table "file, description"; the first column uses a backtick relative path or a link pointing to the same path, no unordered lists, no plain-text filenames without paths.
- Every root-layer body file must appear **exactly once** in the file index, and the target file must actually exist.
- Subdirectories must be registered in the subdirectory index or companion resources; the index must not keep directories that don't exist.

### Top-Level Index

The top-level entry must contain:

| Section | Content |
|------|------|
| category directory table | grouped by category, each item lists tool name + one sentence + directory path |
| directory routing table | mapping from trigger words to directories |
| archive zone index | mandatory when an archive directory exists |

- The category directory table must cover all current tool directories, each directory appears exactly once.
- The directory routing table must cover all current tool directories; trigger words at least include the directory identifier and body topic words.
- Don't keep deleted, renamed, or history-only directories in the current index.

### Flow for Adding a New Tool

1. create the tool directory in four-segment format; tools in use use `live`, evaluating use `eval`
2. choose the lightweight, standard, or complex skeleton by complexity
3. create the entry file, register boundary and all body files
4. take the directory identifier from the parent directory's second segment
5. name root-layer bodies in body four-segment format, purpose must come from the controlled term list
6. write the eight mandatory chapters
7. tools with deployment steps add "Uninstall and Rollback"
8. enable attachment subdirectories as needed
9. when attachments exist, add the "Companion Resources" chapter
10. add optional chapters like hands-on projects and learning paths as needed
11. update the top-level index (category directory + trigger words)

## Timeliness

Timeliness checks use the "last verified" date:

| Trigger | Action |
|------|------|
| tool changes, migration, pitfall fixes | re-verify on the spot and update "last verified" |
| quarterly inspection | scan documents over 180 days, schedule re-verification |
| annual cleanup | over 365 days and no re-verification planned, evaluate demotion |

- After each full run-through per the document passes, update "last verified".
- Attachment header comments' "last verified date" syncs with the main document.
- External links' "last reachable date" over 180 days should be re-confirmed.

## Anti-Patterns

| Anti-pattern | Manifestation | Why wrong |
|--------|---------|------|
| **Vague generality** | "roughly three steps, first do A then B......" | the tutorial must give complete commands and expected output per step |
| **Skipping steps** | Level 2 assumes the reader skipped a Level 1 step | every level must be self-contained, reproducible in order |
| **No expected output** | gives commands but doesn't say what to see after executing | the reader can't judge whether they did it right |
| **Diary-style** | "today I ran into a problem......" | pitfalls must distill into tables, not running narratives |
| **Pasting official site** | copying official text wholesale | best practice is "my usage + my pitfalls", not an official doc mirror |
| **Encyclopedia-ization** | main document over 500 lines still not split | over the threshold must upgrade to the complex skeleton |
| **Describing config in prose** | describing what the config file looks like in text | truth priority — extract to the config directory, keep as-is |
| **No status annotation** | no status, version, last verified at the top | can't judge whether outdated |
| **Relative naming** | filenames with "latest", "final" | current documents write real scope or date, old versions go to `legacy/` |
| **Hiding failed solutions** | deleting the document directly when a solution is abandoned | failed solutions are assets, should demote to legacy or archive |
| **Orphan attachments** | attachment directory has files but the main document doesn't reference them | attachments must have explicit references |
| **Text-only change resetting countdown** | updating "last verified" for a typo fix | last verified can only update after a real run-through |
| **Non-standard credential placeholders** | non-standard placeholders instead of the standard reference form | can't be replaced automatically, easy to miss during deployment |

## Checklist

**Tutorial completeness**

- [ ] title contains one-sentence positioning (within 40 characters) + selection rationale (within 100 characters)
- [ ] status annotation contains the tutorial five fields (difficulty, duration, prerequisites, audience, course affiliation)
- [ ] prerequisites table every row has check command and expected output
- [ ] deployment tutorial contains at least Level 1 and Level 2
- [ ] every step has number, complete command, expected output blockquote
- [ ] every level has goal and acceptance checklist
- [ ] single level no more than 60 minutes
- [ ] complete config inventory lists all config files and deployment paths
- [ ] self-test commands cover core functions, with expected output
- [ ] both ops pitfalls and novice misconceptions present

**Credential separation**

- [ ] all sensitive fields use the standard credential reference form
- [ ] no non-standard placeholders
- [ ] sensitive fields in the config directory and script directory use the standard placeholder too
- [ ] complete config inventory marks relevant files with the "Contains credentials" column

**Reproducibility**

- [ ] a new environment following the document end-to-end can complete deployment
- [ ] prerequisites without omission (all check commands verified)
- [ ] no skipped steps
- [ ] config files directly copy-usable (run after placeholder replacement)

**Structure compliance**

- [ ] tool directory conforms to the four-segment format, all four segments from controlled values
- [ ] every tool directory has an entry file
- [ ] root-layer body exactly four segments, first segment equals the parent directory's second segment
- [ ] body second segment from the purpose controlled term list
- [ ] body fourth segment is a clear scope or compact date
- [ ] skeleton level correct (lightweight / standard / complex)
- [ ] eight mandatory chapters complete
- [ ] attachment subdirectory naming compliant
- [ ] main document explicitly references all attachments (no orphan files)
- [ ] top-level index updated

**Attachment assets**

- [ ] configs and scripts preserved as-is, not "described in prose"
- [ ] config and script header comments contain source, last verified date, related credential
- [ ] multi-file programs have their own description file and dependency list
- [ ] hands-on projects have description file, starter code, completed code
- [ ] sample data desensitized with collection time marked
- [ ] large files via external link

**Multi-host**

- [ ] chose suffix naming or host subdirectory mode, no mixing
- [ ] host mapping table present in host subdirectory mode
- [ ] host aliases match real host names

**Version and lifecycle**

- [ ] main document top has a complete status annotation block
- [ ] status matches directory organization
- [ ] legacy and archived documents state "why replaced"
- [ ] when new and old coexist, old version in `legacy/` subdirectory
- [ ] 3+ versions: entry has a version quick-reference table
- [ ] status changes appended to the change log
- [ ] change log judged by the applicability matrix

**Periodic maintenance**

- [ ] version number, address, port match reality
- [ ] trigger words cover common aliases
- [ ] "last verified" not over 180 days
- [ ] attachment "last verified date" syncs with the main document
- [ ] external links "last reachable date" not over 180 days
- [ ] no orphan attachments
- [ ] legacy over 365 days and no machine running it: evaluate archiving
- [ ] archived tools removed from the directory routing table
- [ ] top-level index and actual tool directories consistent both ways
- [ ] every tool entry has a file index covering all root-layer body files
- [ ] file index uses the two-column table, first column is a resolvable relative path
- [ ] all index targets exist

## Change Log

> Rolling window, retain the last 3 entries, each ≤20 characters.

| Date | Content |
|------|---------|
| 2026-08-07 | Generalized from the best-practice spec |
