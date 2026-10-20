---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-dashboard-role
language: en
publication: public
title: "Role Protocol Methodology"
---

# Role Protocol Methodology

> Manage one thing: when multiple Agent roles work together, shared behavioral standards, reporting agreements, and task delegation rules.
> All roles read one copy. Each role's own files only point to this, without embedding copies. Changing this file takes effect for everyone.

## Governance Layer Variants

Governance layer roles differ from execution layer in reporting chain. Sections listed below should be written by these roles in their own files, not using this methodology:

| Role Type | Variant Section | Reason |
|---------|---------|------|
| Highest decision representative | Completion notification  -  task management | Takes project owner delegation only, not role dispatch. Case log uses own inspection record. |
| Main dispatch role | Completion notification | Already in dispatch window, does not report back to dispatch window |
| Independent review role | Completion notification | Conclusion goes directly to project owner, not through any role filter |

All sections outside the table follow this file only. Do not maintain copies in role files.

## Common Behavioral Standards

1. **Project owner decides** — Roles can analyze and suggest, but decision authority rests with project owner. Do not make major changes on own initiative then expect acceptance.
2. **Continuous consolidation** — Distill modifications from project owner into general rules, write into experience library or operations handbook. Improve workflow source files directly when they need refinement. Each debug round makes roles closer to project owner standards.
3. **Workflow is authoritative** — Tasks with corresponding workflow follow steps strictly, do not skip or substitute based on feeling. Workflow is deep experience sediment.
4. **Trust records, not memory** — Look up numbers in ledger, style in style library, rules in spec files. Memory fails, files do not.
5. **Fix tools on error** — When command line tools or scripts error, fix the tool itself first. Do not manually work around it.
6. **Credential security** — Real secrets only via credential files, never in logs, output, or chat.
7. **Fix problems directly** — When detecting factual errors, stale info, format issues, fix them immediately. Detection exists to fix.
8. **Stay in lane** — Each role has clear "do not do" list, respect it strictly. Ask project owner when unsure.
9. **Review requires translation + context** — When requesting project owner review of foreign-language output, show both original and translated version. For replies or quotes, also show quoted original text (bilingual), so they see full context.
10. **Rate-limited model windows limit concurrency** — Some third-party model APIs have rate limits. When running workflow in these windows, do not exceed 3 sub-agents total. For more items, execute in batches, report between batches.

## Self-Reflection

Reflect on each sub-task immediately upon completion. Record only lessons anchored in concrete results, not feelings.

- **In-role stumbles** → Write to this role's operations handbook case studies.
- **Cross-role lessons** → Write to shared experience file in public role directory.
- **Accidental success does not become rule** — Confirm 2-3 times before formalizing as experience.

## Completion Notification: One Call Convention

**When assigning task, write completion report sentence on last line of prompt. After executor completes, they run that line.** No service, no ledger, no code involved — assigner confirms own window name first, writes **originating window** into prompt as constant. That is the entire mechanism.

| Task Source | Report To |
|---------|--------|
| Any window or role assignment (including peer) | Report to **originating window** — whoever sent it gets it back |
| Main dispatch role assignment | Report to dispatch window (still reporting to originator, originator is dispatch) |
| Project owner direct statement in this window | **Report to project owner in person**, no report sentence, no window notification |

**Never default to report to dispatch window.** Dispatch window is special only when "originator happens to be it", not the command chain for peer delegation.

**Executor side has one rule only: run the report sentence in the prompt, do not use fixed template from own handbook.** When prompt has no report sentence, report based on task nature — return result for result task, conclusion for judgment task, findings for problem identification task. Still do not initiate message to dispatch window.

> **This is a call convention, not a notification system.** Assigning equals pushing to stack (writing return address), completing equals popping (returning to address). **Only assigner at assignment time knows who is waiting**, so they write the address. Do not rely on anything to guess at completion time.
>
> **Report may not come, and that is the known cost.** Assigner forgot to write, executor crashed and cleared, or did not run the instruction, means no echo — no mechanism covers all cases. If no action after expected time, check status yourself, do not wait indefinitely.
>
> History shows two tries to "let machine decide who to notify" (global mailbox, multi-layer routing plus model fallback). Both failed at the same place: **machine does not know who is waiting.** Before building a third system, read the retirement records of the first two.

## Task Management

- **Board**: Active task list in dispatch directory, filter by role.
- **Task directory**: `{dashboard_root}scheduling/{type}-{domain}-{purpose}-{qualifier}/`, with `role` in the metadata of `task.yaml` (or `task.md` for one-off tasks).
- **Dispatch prompt**: If over 10 lines, save to prompt partition in dispatch directory.
- **Output**: Write to run data directory or business directory, task file output field records path. After completion, change status and delete from active board; the directory never moves.
- **Before context cleanup**: Refresh active board progress, write context snapshot at bottom. Next load reads it to restore, then delete snapshot.

## Task Delegation Rules

### First Rule: Analysis belongs to assigner, execution belongs to executor

**Assigner is commander, executor is hands.** This governs all delegation, whether to temp window, standing window, or remote.

| Who | Responsible For |
|----|---------|
| **Assigner** | Clarify current state  -  identify problem source  -  define solution  -  break into concrete checklist down to file and step  -  **accept delivery** |
| **Executor** | Execute checklist  -  collect facts  -  report truthfully (including incomplete parts) |

**Never pass judgment to executor.** "Research it first, then decide how to change" means passing command authority — executor only sees their piece, their judgment lacks full picture, result likely needs rework.

When executor must collect facts first (e.g., clarify difference between two directories), task must explicitly state: **report facts only, no conclusions, no suggestions, no prioritization**. Bring facts back, assigner judges, then dispatch second round of concrete steps.

**Acceptance is assigner's job, not executor self-certification.** Review delivery: did I actually run what was supposed to run, are self-check conclusions trustworthy, was "structure verified" confused with "execution verified". Return if substandard for rework. Do not pass incomplete work upstream.

### Checks Before Delegating to Standing Window

1. Check window status — must be idle or completed, do not interrupt active work.
2. Confirm previous task is done — check final output and current task field.
3. Judge if new task relates to previous:
   - **Related** (same project, sequential dependency, need shared context) → Dispatch directly, do not clear.
   - **Unrelated** (completely different task) → Clear context first, then dispatch.
4. Write prompt, add completion report sentence on last line.
5. Add to prompt: "Execute directly, do not wait for confirmation". This works for all models.

### One Message One Task

When messaging a window running a long task, **it follows its own to-do list, will not change priority because you casually mention something in a long message**.

| Do Not Do This | Result |
|--------|------|
| Acceptance + ruling + new task in one message | New task treated as background info, read but not done |
| "While you are at it, also do X" in second paragraph | It finishes current round, X still waiting |
| One task continued in two separate messages | Misses both rounds. You think it is rebelling, actually a formatting issue. |

**For a new task, send separate message, title it clearly as new round.** Send acceptance and ruling separately.

Delivery itself has lag: adding message to busy window is **queuing**. Stack a few, it arrives proportionally later. Tool return of "no immediate execution observed" means it did not start right away, text already in queue. **Do not re-send** — re-send makes it read the same content twice.

For urgent corrections of parameters, use queue-jump mode: it reads in current round. Cost is current round gets interrupted, so **use only to fix current task**. New tasks still send separately, do not queue-jump.

### How to Write Completion Report Sentence

All three slots are dynamic. **Forbid "self / this window / user window" as vague addresses**:

| Slot | Means |
|------|------|
| `{executor_window}` | Who to assign to |
| `{originating_window}` | Who to report to, equals assigner's window name |
| `{what_to_report}` | Mirror of assignment requirement |

#### Prompt Structure

**Confirm executor window exists before assigning.** When project owner did not name window, use tools to resolve by capability and repo state, not memory. Check which machine you are on before cross-machine assignment — wrong machine sends task to someone else's window. Before cross-machine work, confirm own identity.

Write metadata before long task body to avoid executor guessing addresses:

```text
[Assignment Metadata]
- Executor window: {executor_window}
- Originating window: {originating_window}
- Report window: {originating_window}
```

**Cross-machine assignment must include host parameter, otherwise report does not reach.** When executor on machine A, assigner on machine B, executor without host parameter looks for assigner's window on machine A, finds nothing, report cuts off halfway.

Check own identity once before assigning. Tool gives exact command to paste into completion report sentence. Current machine to current machine: host parameter optional, but **get in habit of always including** — same prompt deployed to remote later needs no change.

Tail sentence template (send target always originating window, never default dispatch window):

```text
Send to {executor_window}: "{task content}. Execute directly, do not wait for confirmation.
Upon completion, execute: Send to {originating_window} \"[{executor_window}→{originating_window} - summary]{what_to_report}\""
```

Two hard constraints for cross-machine delegation:

- **Build window and wait for ready** — Do not rush to send when startup shows not ready. Message drops into startup banner and disappears. Check where it is stuck first.
- **Delivery requires verification** — Return showing "execution not verified" **fails**. "Sent" only means it left, not that far end started. Check status yourself.

Suggest report prefix as `[{executor_window}→{originating_window} - summary]`, easy to scan the chain.

#### What to Report: Mirror Assignment Requirement

**Completion report sentence mirrors what assignment asked for.** Report what you asked — "clarify root cause" goes back as `cause: {what}`, not `done: {one sentence}`. The latter tells nothing, assigner must read through anyway, that report wasted itself.

| Assignment Asked For | Report Sentence Asks |
|---------------|-----------------|
| Result | `done: {one sentence result}` |
| Process, how to | `done: {key steps + files changed}` |
| Judgment, suggestion | `conclusion: {judgment} + {one sentence reason}` |
| Problem, risk | `found: {problem list, or "none"}` |
| Numbers, list | `result: {numbers or list itself}` — bring the numbers back, do not just say "counted" |
| Root cause trace | `cause: {what} / stuck_at: {which step unresolvable}` |
| Multi-round one round | `this_round: {what completed} + next: {suggestion}` |

**Report even if it did not work.** Report sentence only saying "done: ..." makes executor skip report if failed — they think it is not "done". Either leave failure exit in report sentence, or tell task "report even if stuck, write where you got stuck". **No report and failure are different things, mixing them makes tracing hardest.**

#### Five Constraints

- **Report window equals originating window** — Fill in assigner's name, check once before assigning. If unsure do not write report sentence, let assigner check themselves. Do not guess a window name and send.
- **No vague reference** — Prompt must not have "this window / user window / current session / own window" as address, must be concrete tag.
- **Write full command, not local shorthand** — Shorthand is project command-line convention, executor without loaded project cannot expand it.
- **Do not write if no report needed** — Pipeline entries (engine has own acceptance criteria), single shell commands, self-supervising after dispatch, casual tasks, project owner face-to-face directive.
- **Do not nest report in report sentence** — Command executor runs has no further reporting requirement. Chain ends there.

#### Pre-Dispatch Three Questions

1. What is my window name? Written in "originating window" yet?
2. Is completion report target **equal to originating window**?
3. Anything left in prompt like "this window / user window / default dispatch window"?

If question 2 is no or question 3 is yes, fix first, then dispatch.

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|---------|
| 2026-08-14 | Task path points at four-segment task directories |
| 2026-08-07 | Generalized from role procedures |
