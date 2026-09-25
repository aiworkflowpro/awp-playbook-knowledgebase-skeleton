---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-task-statemachine
language: en
publication: public
title: "Task State Machine Methodology"
---

# Task State Machine Methodology

> Manages one thing: task hub's state set and permissible transitions.
> Does not manage same-named states in other systems—see below "Do not change the other two state sets together".

## Six States

```text
State           Meaning
ready           Executable, awaiting pickup
running         Executing
waiting_user    Mid-execution needs decision (requirements unclear / needs login / high risk), returns to ready after decision
blocked         Blocked—dependency unsatisfied or needs long manual processing; directory stays in place, set back to ready after handling
completed       Completed
cancelled       Cancelled
```

These six states are the task hub's only state set, aligned with directory layout.

**State only describes task location, not executor.** Executor written in `executor` and `completed_by` fields.

## Terminal State is `completed`, not `done`

Any `done` appearing in task files, or any informal equivalent of `completed`, must be rewritten to `completed`. `done` is not retained as alias.

### Do not change the other two state sets together

A knowledge base often has three unrelated state machines both using the word `done`; this methodology only manages the first set. Before batch replace check which set:

| Which State Set | Shape | Managed By | Change? |
|-----------|---------|--------|--------|
| **Task hub task status** | `status` in task file metadata | This methodology | **Yes**, rewrite all to `completed` |
| **Window management backend window state** | `idle` / `working` / `done` / `blocked` | Window management backend protocol; dispatch tool judges window can take work by it | **No**, change breaks dispatch tool completely |
| **Workflow step status** | Step status field in step file | Workflow authoring spec enum | **No**, that is another spec's enum |

No unconditional KB-wide replace of `done`. Criterion: **is this `done` describing a task file's `status`**—if not, do not touch.

## Standard Transitions

```text
ready -> running
running -> completed
running -> cancelled
running -> waiting_user
waiting_user -> ready
running -> blocked
blocked -> ready
ready -> cancelled
```

## Executor Acknowledgment Rules

- Dispatch role scans upon inspection pickup tasks in executable partition with `status: ready`, routes by `executor` field to execution window.
- After pickup immediately change state from `ready` to `running`, write executor and start time, task stays in place.
- Same scan round must not re-dispatch tasks already entered `running`.

## Timeout Handling

```text
State          Handling
running        Over 6 hours no update, transition to waiting_user for decision
waiting_user   Over task declared deadline no decision, retain and highlight in view
blocked        After dependency or manual handling complete, set status back to ready
```

## Exception Transitions

| Situation | Transition |
|------|------|
| Requirements unclear | `running -> waiting_user` |
| Needs login | `running -> waiting_user` |
| High-risk action | `running -> waiting_user` |
| External API unavailable | `running -> blocked` (await external recovery or manual handling) |
| Output contract missing | Must not enter `running`, change directly to `waiting_user` |

## Checklist

- [ ] Task `status` only uses these six enum values
- [ ] Terminal state uses `completed`, not `done`
- [ ] No accidental changes to window state or workflow step status `done`
- [ ] State directory matches state set, no custom directories

## Change Log

> Rolling window; keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-14 | Removed old partition wording |
| 2026-08-07 | Generalized from state machine specification |
