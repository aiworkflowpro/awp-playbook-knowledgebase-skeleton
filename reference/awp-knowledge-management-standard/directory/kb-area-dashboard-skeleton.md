---
document_id: awp-knowledge-management-standard/directory/kb-area-dashboard-skeleton
language: en
publication: public
title: "Knowledge Base Dashboard/ Directory Skeleton"
---

# Dashboard/ Directory Skeleton

> Defines the subdirectory structure under the `{dashboard_root}` root, the organizational patterns it uses, and its customization interface.

## Responsibilities

The dashboard holds the runtime state: who is working, what they are working on, how far they have gotten, and where their outputs land. Roles, projects, task scheduling, research planning, workflow outputs, process data, and session handoffs all live here.

## Directory Structure

```text
{dashboard_root}
├── CLAUDE.md              ← Fixed; entry point, the sole source of truth for the role list and the role count
├── roles/                 ← Fixed; all roles
│   ├── shared/            ← Fixed; runtime assets shared by all roles
│   └── {role_name}/       ← One directory per role
├── projects/              ← Fixed; long-term development projects
│   └── {product_name}/
├── output/                ← Fixed; = {run_output_root}, partitioned by month
├── scheduling/            ← Fixed; task hub
├── research/              ← Fixed; one-off research reports and in-flight proposals, partitioned by month
└── handoff/               ← Fixed; session handoff files, partitioned by month
```

- The path variables `{dashboard_root}` and `{run_output_root}` are declared in `{specs_root}layout.yaml`, resolved as `dashboard/` and `dashboard/output/`.
- The root directory holds only `CLAUDE.md` and the fixed subdirectories listed above.
- The role list and the role count are maintained in exactly one place, `{dashboard_root}CLAUDE.md`; no other file repeats them.

### Month-Subdivision Rules

Every subdirectory that carries a time dimension gets a `{YYYYMM}/` intermediate layer first. Date directories must not be flattened under the root.

| Subdirectory | Partition Depth | Path Template |
|--------|---------|---------|
| `output/` | Month | `{YYYYMM}/{YYYYMMDDHHmmss}_{source}_{summary}/` |
| `handoff/` | Month | `{YYYYMM}/{YYYYMMDDHHmm}-{action}-{object}-{detail}.md` |
| `research/` | Month | `{YYYYMM}/{YYYYMMDD}-{title}/` |

Trials, collections, intermediates, and formal runs all use a timestamp-first three-underscore name. Do not put a day layer under the month. `scheduling/` is not time-partitioned: task directories are four-segment and flat, structure defined by the task hub methodology.

### `roles/shared/`

Content shared by all roles is split between two places by its nature, and each piece has exactly one canonical copy. Each role's own `CLAUDE.md` only points to that copy:

| Nature | Canonical Location | What It Holds |
|------|---------|--------|
| Rules — still valid no matter which set of roles is in place | Role protocol files in the standards package | General behavior standards, self-review, closing notices, task management, task-assignment rules |
| Runtime state — must change whenever the current state changes | `{dashboard_root}roles/shared/` | Routing for finding people, stage direction, shared experience, delegation procedures |
| Private — used by one role only | That role's `operations-manual/` | Daily report templates, decision principles, pitfalls that role has hit |

`roles/shared/` sits at the same level as the role directories and belongs to no role. When you add something that everyone uses, judge its nature first; you must not lodge it under any single role's `operations-manual/`.

### `projects/` Boundary

`projects/{product_name}/` lives physically under the dashboard, but the product-development documents inside it are not governed by this skeleton.

| Governed By | Governs |
|------|--------|
| The product development spec | The project's internal phase directories, document framework, naming, versioning, and the flow of completed development back into the project |
| This skeleton | `projects/`'s place under the dashboard and its relationship to roles, scheduling, and handoffs |

### Write Boundary

| Operation | Inside the Dashboard | Outside the Dashboard |
|------|---------|---------|
| A tool in the dashboard writes | Allowed | Prohibited |
| A tool in the dashboard reads | Allowed | Allowed |
| Workflow-settled outputs | First landing spot | Second landing spot, copied by the workflow itself |

Settling is a copy, not a move: the output stays in the dashboard as evidence, and a copy is placed in the business or research directory.

## Organizational Patterns Used

| Layer | Pattern | Description |
|----|------|------|
| Root → Subdirectories | **E3 Functional Responsibility** | Structure is fixed; it does not grow over time |
| `output/` | **T5 Month Bucket + Run Directory** | Timestamp-first run directories under the month |
| `handoff/`, `research/` | **T2 Month Bucket + Date-Prefixed Directory** | Each entry is an independent event |
| `scheduling/` task directories | **Four-segment naming** | `{type}-{domain}-{purpose}-{qualifier}/` flat, defined by the task hub methodology |
| `projects/{product_name}/` | **P1 Product Development Lifecycle Node** | Defined by the product development spec |
| `roles/{role_name}/` | **E3 Functional Responsibility** | One directory per role |

Pattern definitions are in `kb-directory-pattern-registry.md`.

## Customization Interface

| Parameter | Description | Default |
|------|------|--------|
| `{dashboard_root}` | Root path of this area | `dashboard/` (see `layout.yaml`) |
| `{run_output_root}` | Root path for run output | `dashboard/output/` |
| Subdirectory list | Which fixed subdirectories exist under the root | `roles` · `projects` · `output` · `scheduling` · `research` · `handoff` |
| Role list | Which roles exist under `roles/` | Registered by the user in the root `CLAUDE.md` |
| Role layering | How many layers the roles are split into | A governance layer plus an execution layer; execution-layer roles are released once their work is done |
| Run directory naming | Leaf directory name under `output/` | `{YYYYMMDDHHmmss}_{source}_{summary}` |
| Retention policy | How long each data type is kept | Output is kept permanently; remove it manually once it is confirmed unused |
| Scheduling structure | Which functional directories exist under `scheduling/` | Defined by the task-hub methodology; this skeleton does not repeat it |

### Building a New Role

Four conditions must all hold before you create a new role directory: the responsibility boundary is clear, there is a stable source of input, there is a definite output, and no existing role can take on the work. After creating it, register the role in `{dashboard_root}CLAUDE.md`.

## ⑦ Build Procedure

The dashboard absorbs run results. Outputs pile up fast, items are unrelated, and they are looked up by recency — all three checks point to time partitions (month buckets).

### Setup (no interview needed — the structure is deterministic)

The agent creates the output directory with the current month folder and confirms the dashboard CLAUDE.md says: every future workflow run lands in the current month folder, one subfolder per run.

### Agent Rules

- Runs are never edited after the fact. A bad run gets a new run, not a fix-up.
- Each run subfolder is named by the naming standard with a timestamp prefix.
- This is why run outputs use date partitions: they grow without limit, items never relate to each other, and the only useful sort is most recent first.

### Build Verification

- Print the full file tree of `{dashboard_root}`
- Confirm `output/{current_month}/` exists
- Check against § Checklist item by item

## Related Methodologies

- `../methodology/operations/` — How role cards are written, the task file format and its state machine, the detailed naming rules for workflow-output directories, the double-landing rules, the four-layer correspondence for channel operations, and the daily report rules.

## Checklist

- [ ] The root directory contains only `CLAUDE.md` and the declared fixed subdirectories
- [ ] Every time-bearing subdirectory has a `{YYYYMM}/` intermediate layer
- [ ] Workflow outputs have a day layer; other subdirectories have no extra date layer
- [ ] The role list is maintained only in `{dashboard_root}CLAUDE.md`
- [ ] Runtime assets shared by everyone live in `roles/shared/` and are not lodged under any single role
- [ ] A tool in the dashboard has not written to any directory outside the dashboard
- [ ] Confirmed that no process is still writing to a run directory before renaming it
- [ ] Obsolete content goes to `{inbox_root}archive/`; no archive layer is built inside this area

## Change Log

> Rolling window; keep the last 3 entries, each ≤20 characters.

| Date | Change |
|------|--------|
| 2026-08-14 | Scheduling switched to four-segment flat; old drawer rows removed |
| 2026-08-07 | Extracted the skeleton from the dashboard specification |
