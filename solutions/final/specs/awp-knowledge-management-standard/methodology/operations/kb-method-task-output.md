---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-task-output
language: en
publication: public
title: "Output Contract Methodology"
---

# Output Contract Methodology

> Manages one thing: when an automatically executed task completes, how the output content flows back into the knowledge base.
> Does not manage task naming and state transitions (those belong to task file methodology and state machine methodology).

## Core Rule

Any task executed automatically by an Agent must declare an `output_contract`. **Tasks without an output contract must not execute automatically**—without a contract there is no acceptance anchor; no one knows where outputs land after completion or whether the task is done.

## Field Structure

```yaml
output_contract:
  mode:
  target_paths: []
  report_path: {task_directory}/reports
  must_update_task_file: true
```

| Field | Description |
|------|------|
| `mode` | Output mode; valid values in table below |
| `target_paths` | Knowledge base target documents to write or update |
| `report_path` | Run report directory for this execution, defaulting to `reports/` inside the task directory |
| `must_update_task_file` | Whether task file must be written back |

## `mode` Values

| Value | Meaning |
|------|------|
| `update_existing` | Update existing knowledge base file |
| `create_new` | Create new knowledge base file |
| `append` | Append to specified section of existing file |
| `report_only` | Generate report only; do not modify formal KB files |
| `proposal` | Generate proposal awaiting manual review |

## Target Path Rules

- `target_paths` must use absolute paths.
- Target paths must be under knowledge base root directory.
- When touching formal business, brand, standards, or workflow files, must update corresponding directory's `CLAUDE.md` index.
- `report_only` tasks must also write run reports and output index.

## What Must Be Written After Completion

| Target | Write |
|------|--------|
| Target document | Each one listed in `output_contract.target_paths` |
| Task file | `status` / `output_paths` / `completed_by` / `completed_at` / completion summary |
| Run report | Directory pointed to by `output_contract.report_path` |

## Failure Handling

On failure, must also write run report. Report must include:

- Task identifier
- Failure phase
- Root cause assessment
- Modified files
- Whether manual intervention needed
- Recommended next action

**No report on failure means this run never happened**—next cycle will hit the same pit.

## Checklist

- [ ] Automatically executed tasks have `output_contract`
- [ ] `target_paths` point to real KB paths as absolute paths
- [ ] Both task file and target documents written after execution
- [ ] `CLAUDE.md` synchronized in directories with indexes
- [ ] On failure, run report written with all six items complete

## Change Log

> Rolling window; keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-14 | report_path defaults to task-dir reports/ |
| 2026-08-07 | Generalized from output contract specification |
