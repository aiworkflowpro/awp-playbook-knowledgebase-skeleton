---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-task-file
language: en
publication: public
title: "Task File Methodology"
---

# Task File Methodology

> Manage one thing: "one file one task" path, naming, metadata fields, and body structure for task hub.
> Does not govern state enum (that is state machine methodology), nor output contract field semantics (that is output contract methodology).

## File Location

Task files by month:

```text
{dashboard_root}dispatch/pending/{YYYYMM}/
{dashboard_root}dispatch/completed/{YYYYMM}/
```

State directories must come from state machine methodology defined set. No custom states.

## File Naming

```text
{task_id}-{short_title}.md
```

| Constraint | Definition |
|------|------|
| Task ID | Recommend `T{YYYYMMDD}-{three_digit_sequence}` |
| Short title | Letters, digits, or short phrases |
| No spaces | — |
| No weak words | Words like "temp", "casual", "pending" mean task itself unclarified |

## Metadata Fields

```yaml
---
id:
title:
role: # Responsible role, single value
requester: # Requesting role (optional), fill only if different from responsible
status:
priority:
owner:
executor:
windows: []              # Windows list used
source:
created: # Archive time
dispatch_mode: # Dispatch way (optional), one sentence how it was sent
prompt: # Prompt file path (for long prompts saved to disk)
output: []                # Output directory or file path list
run_config: # Pipeline recipe path (batch tasks)
dedup_key:
source_context:
scheduled_for:
due:
cadence:
review_required:

claim_agent:
claim_started_at:

input_paths: []
locks: []                # Files this task modifies (optional), check conflict before dispatch
depends_on: []           # Prerequisite task IDs (optional), do not dispatch if pending

output_contract:
  mode:
  target_paths: []
  report_path:
  must_update_task_file: true

output_paths: []
completed_by:
completed_at:
---
```

Field definitions:

| Field | Definition |
|------|------|
| `id` | Task unique ID |
| `title` | Task title |
| `role` | Responsible role, single value, for role-based filtering |
| `requester` | Requesting role (optional) |
| `status` | State from state machine |
| `priority` | Priority bracket or blank |
| `owner` | Responsible party |
| `executor` | Executor ID, from registry in this library |
| `windows` | Windows list used |
| `source` | Task source (required): project owner direct / dispatch role delegation / automation trigger |
| `created` | Archive time (optional) |
| `dispatch_mode` | Dispatch way (optional), one sentence on how sent, which workflow |
| `prompt` | Prompt file path |
| `output` | Output directory or file paths |
| `run_config` | Batch task pipeline recipe path |
| `dedup_key` | Semantic dedup anchor (optional) |
| `source_context` | Context triggering this task (optional) |
| `scheduled_for` | Planned handle date |
| `due` | Due date |
| `cadence` | One-time / daily / weekly / monthly / custom |
| `review_required` | Human review required |
| `claim_agent` | Current claimant |
| `claim_started_at` | Claim time |
| `input_paths` | Input file absolute path list |
| `output_contract` | Output contract, see output contract methodology |
| `output_paths` | Actual output file absolute path list |
| `completed_by` | Completer |
| `completed_at` | Completion time |
| `locks` | Files this task modifies (optional). Check conflict before dispatch. |
| `depends_on` | Prerequisite task IDs (optional). Do not dispatch if pending. |

## How to Fill `role`

`role` is **single value role name**. One role only. Use name that actually exists in role directory. Filtering by `role` relies on exact string match. Putting flow description there breaks matching.

- Correct: `role: development_manager`
- Wrong: `role: content_manager (requesting) → development_manager (executing)`

When requester and responsible differ, responsible goes in `role`, requester in `requester`, windows in `windows`:

```yaml
role: development_manager
requester: content_manager
windows: [{window_name}]
```

Historical files do not backfill `role`. Scan treats as "no role".

## Body Structure

Must have two level-2 headings:

```markdown
## Acceptance Criteria

## Completion Summary
```

Five sections recommended below, take or leave per task complexity. Do not enforce:

```markdown
## Input

## Execution Requirements

## Output Requirements

## Execution Record

## Blocking
```

> Why shrink from seven mandatory to two: when all seven were required, most files padded five blank sections. Task files as narrative — sections following task itself — work better. One real "process slip" is more useful than one empty "blocking".

## Auto-Execution Gate

"Auto-execute" means **unattended** task pickup and execution. This gate stays dormant when no executor runs unattended. Executor goes to sleep, gate remains — it is prerequisite for resuming unattended execution.

To enable this gate, auto-executed task must meet all:

- `executor` is designated auto-executor in this library.
- `status` is `ready`.
- `output_contract.target_paths` non-empty.
- `review_required` explicitly `false`, or task only produces reviewable draft.
- Task does not need login, payment, delete, publish, authorize, or remote destructive action.

> `review_required` therefore optional — blank equals not meeting gate, therefore no auto-execute. Default is wanted. Manual dispatch ignores this field.

## Checklist

- [ ] Path under pending or completed monthly directory
- [ ] Filename is `{task_id}-{short_title}.md`
- [ ] Metadata has `id` / `status` / `executor` / `role`
- [ ] `role` is single value role name, matches role directory
- [ ] Body has "Acceptance Criteria" and "Completion Summary" level-2 headings
- [ ] Auto-execute task has `output_contract`

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from task file spec |
