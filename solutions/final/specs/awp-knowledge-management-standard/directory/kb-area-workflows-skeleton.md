---
document_id: awp-knowledge-management-standard/directory/kb-area-workflows-skeleton
language: en
publication: public
title: "Knowledge Base Workflows/ Directory Skeleton"
---

# Workflows/ Directory Skeleton

> Defines the subdirectory structure, organization patterns used, and customization interfaces of the `{workflows_root}` root directory.

## Responsibilities

Stores Agent workflow **definitions**: one workflow per directory, directory name is the workflow's identity. Run outputs go to `{run_output_root}`, not here.

## Directory Structure

```text
{workflows_root}
├── CLAUDE.md                              ← Fixed; entry, contains task routing
├── AGENTS.md                              ← Ecosystem fixed name; multi-framework instruction entry
├── document-index.json                    ← Machine generated; document identity index, rebuilt by tooling
├── translation-state.json                 ← Machine generated; zh-en translation state, rebuilt by tooling
└── {ns}-{domain}-{action}-{detail}/       ← One workflow per directory
```

- Path variable `{workflows_root}` is declared in `{specs_root}layout.yaml`, resolved as `workflows/`.
- Root directory contains only `CLAUDE.md` and workflow directories; workflow directories are flat, no further grouping by domain.
- Workflow directory names strictly four-segment, one English lowercase word per segment, segments separated by hyphens.

### Workflow Directory Name

```text
{ns}-{domain}-{action}-{detail}
```

| Segment | Description |
|------|------|
| `ns` | Project namespace |
| `domain` | Business domain |
| `action` | What to do with this domain |
| `detail` | Specific object or scenario |

Brand not in directory name—brands distinguish by run identity. Directory name and declared workflow identifier within package must be identical; changing one requires changing the other.

### Within-Package Structure

```text
{ns}-{domain}-{action}-{detail}/
├── AGENTS.md                  ← Ecosystem fixed name
├── CLAUDE.md                  ← Ecosystem fixed name
├── WORKFLOW.md                ← Master orchestration
├── ROUTER.md                  ← Routing
├── manifest.yaml              ← Machine-read declaration
├── workflows/                 ← Orchestration; sub-workflows
│   └── {phase_code}-{sub_id}/
│       ├── WORKFLOW.md
│       ├── steps/
│       │   └── step{NN}-{action}.md
│       └── {prompts,scripts,references,assets}/   ← Sub-workflow private resources
├── prompts/                   ← Package-level prompts
├── references/                ← Package-level knowledge
│   ├── contracts/
│   ├── methodology/
│   └── judging/
├── assets/                    ← Package-level materials
│   └── templates/
├── scripts/                   ← Package-level code
│   └── modules/
├── config/                    ← Configuration
│   ├── schemas/
│   ├── providers/
│   └── registries/
├── profiles/                  ← Run identity variants
│   └── {brand_key}/
│       ├── profile.yaml
│       ├── identity/
│       └── pad/
├── docs/                      ← Human-readable documentation
└── persistent/                ← Optional; continuous-operation workflows only
```

Eight top-level directory names fixed: `workflows`  -  `prompts`  -  `references`  -  `assets`  -  `scripts`  -  `config`  -  `profiles`  -  `docs`. Lightweight workflows without `workflows/` place steps directly at top-level `steps/`.

### Path Language Rule

**Any path segment containing non-ASCII characters in workflow package violates this rule**, machine-checkable; descriptive names not exempt.

Reason: entire package gets copied to other machines, passes through version control, URLs, different OS path rules, various pipelines; any non-ASCII segment may mismatch somewhere.

| Zone | Path Segments |
|----|--------|
| Definition zone (this area) | All English |
| Run output zone (`{run_output_root}`) | All English |

Instruction-type documents carry language suffix (`WORKFLOW.md`, `ROUTER.md`, `steps/step{NN}-{action}.md`); ecosystem fixed names, scripts, configs, templates not.

### Boundary with Run Output Zone

| Content | Location |
|------|------|
| Workflow definition, prompts, scripts, templates | `{workflows_root}{workflow_name}/` |
| Each run's outputs, state, evidence | `{run_output_root}{YYYYMM}/{YYYYMMDDHHmmss}_{source}_{summary}/` |

Package files do not write knowledge base top-level directory paths. External material locations write in run-identity file; run root derives from run contract; neither hardcoded in package.

If run-output-zone skeleton directories appear under workflow root, executor's working directory base is wrong—delete and investigate, don't leave in place.

## Organization Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → workflow | **A1 Four-segment hyphenated** | Directory name is both path and workflow identity |
| Package top-level | Fixed English directory names | Eight items, closed set |
| Sub-workflows | `{phase_code}-{sub_id}/` | Phase code is digit plus uppercase letter |
| Step files | `step{NN}-{action}.md` | Two-digit sequence number |

Pattern definitions see `kb-directory-pattern-registry.md`. Workflow packages deeper than four layers follow this skeleton, not hard depth limit.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{workflows_root}` | Root path of this area | `workflows/` (see `layout.yaml`) |
| `{run_output_root}` | Root path for run outputs | `dashboard/output/` |
| Namespace vocabulary | Directory name first segment | Single namespace; machine ground-truth in workflow-spec package constant file |
| Domain vocabulary | Directory name second segment | English controlled vocabulary, defined by workflow methodology |
| Action vocabulary | Directory name third segment | English controlled vocabulary, defined by workflow methodology |
| Top-level directory list | Package top-level allowed directories | Eight fixed; add `persistent/` for continuous-operation type |
| Run-identity key | Directory name under `profiles/` | Lowercase English with hyphens; template fixed as `_example/` |
| Language suffix | Instruction document filename suffix | Source library uses `.md`, English library uses `.md` |
| Step location | Presence of `workflows/` middle layer | Complete workflows have it; lightweight workflows place steps at top-level `steps/` |

## ⑦ Build Procedure

A workflow is a repeatable step list the agent can run end to end, checking its own work against the standards. The first session builds one workflow from a task the owner already repeats.

### Interview Questions (ask one at a time)

| # | Ask | Maps to |
|---|-----|--------|
| 1 | What task do you repeat every week or every day? | Workflow name and trigger |
| 2 | Walk me through it — what are the steps, in order? (reflect them back until confirmed) | Steps section |
| 3 | How do you check the result is good? | Check section (must reference applicable standards) |

### Agent Rules

- The workflow file has four sections: When to run (trigger), Steps (numbered, each doable without asking), Check (verification, including names follow the naming standard), Where it lands (which business arena or dashboard month folder receives the result).
- After writing the workflow, run it once for real, start to finish. Show the result and where it landed.
- The check step must reference at least one standard. This is how rules and workflows interlock.
- Print the file tree and stop.

### Build Verification

- Print the full file tree of `{workflows_root}`
- Run the workflow once end to end — verify the output lands in the correct location and the file name follows the naming standard
- Check against § Checklist item by item

## Related Methodology

- Orchestration patterns, document skeletons, evaluation methods, phase gates, run contracts, state models for Agent workflows defined by Agent Workflow Specification; this skeleton only addresses directory appearance.

## Checklist

- [ ] Root directory contains only `CLAUDE.md` and workflow directories, flat layout
- [ ] Workflow directory name strictly four-segment, each segment one English lowercase word
- [ ] Directory name identical to declared workflow identifier within package
- [ ] No path segment in package contains non-ASCII characters
- [ ] Top-level directory names in closed set
- [ ] Instruction documents carry language suffix, ecosystem fixed names and scripts/configs do not
- [ ] Package contains no hardcoded knowledge-base top-level directory paths
- [ ] Workflow root has no run-output-zone skeleton directories
- [ ] Sub-workflow private resources not directly referenced by other sub-workflows

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-14 | Root machine indexes declared |
| 2026-08-07 | Extracted skeleton from workflow specification |
