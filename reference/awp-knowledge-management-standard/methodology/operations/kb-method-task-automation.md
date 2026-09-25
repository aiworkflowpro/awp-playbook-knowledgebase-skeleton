---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-task-automation
language: en
publication: public
title: "Automation Registration Methodology"
---

# Automation Registration Methodology

> Manage one thing: how timed dispatch tasks register a mirror in the knowledge base.
> Does not govern actual dispatch itself — true dispatch lives in system-level scheduler. Knowledge base keeps mirror only.

## Why Register Mirror

System-level scheduler is true source. Knowledge base keeps registration mirror for three things: **audit** (who ran what when), **migration** (rebuild on new machine following record), **reproduction** (know configuration at time of issue).

Registration file:

```text
{dashboard_root}dispatch/automation/registry.md
```

## When to Register

| Action | Registration Need |
|------|---------|
| After creating timed task | Must register in knowledge base |
| After changing frequency, prompt, workflow, run method | Must sync registration |
| After deleting timed task | Must mark stopped in registry, or migrate to history section |

Forgetting to register after deletion is most common slip — leftover entry makes people think task still runs.

## Required Fields

```yaml
name:
type:
status:
host:
cadence:
schedule_cron:
prompt:
output_root:
created_at:
updated_at:
notes:
```

Which workflow and which run method: write in `notes`. No need separate field — separate field sits empty long-term.

## Type

| Type | Scenario |
|------|------|
| Timed task | System-level scheduler triggers, unattended |
| Scan loop | Agent in standing window periodically scans task queue |
| Manual trigger | User manually runs dispatch job |

## Security Requirements

- Unattended tasks use headless mode. Permissions limited by task's declared allowed tool list.
- Tasks needing outside account, login state, payment, publish, or delete: mark only as awaiting decision. Must not run unattended.

## Checklist

- [ ] After new, change, or stop timed task, registry synced
- [ ] Registry has `name` / `status` / `cadence` / `prompt` required fields
- [ ] Stopped tasks marked stopped status, not left in active section
- [ ] Unattended task permissions declared and limited, no high-risk actions

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from automation registration spec |
