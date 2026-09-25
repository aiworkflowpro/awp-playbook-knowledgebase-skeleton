---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-task-runreport
language: en
publication: public
title: "Run Report Methodology"
---

# Run Report Methodology

> Manages one thing: what a flat report must look like after each task hub run.
> Does not manage directory-style output from workflow runs—that is a separate shape; see division table below.

## Two Forms Each in Place

Two form types exist; choose by output nature:

| Form | Shape | When to Use | Managed By |
|------|---------|-----------|--------|
| **Flat file** | `{YYYYMMDD}-{type}.md` single file | Inspection report—scan task queue once, record results once | `{dashboard_root}scheduling/scan-dispatch-health-core/reports/` |
| **Directory style** | One run directory with run info and results | Workflow run output | `{run_output_root}{YYYYMM}/` (see the dashboard skeleton) |

Decision criterion: **Did this run follow a workflow**? If yes, use directory style into the output area; if no, just scanned queue, use a flat file into the inspection task directory. Run reports of a specific task go to `reports/` inside that task directory.

## Report Location and Naming

```text
{dashboard_root}scheduling/scan-dispatch-health-core/reports/{YYYYMMDD}-{type}.md
```

Run reports of a specific task go to `reports/` inside that task directory.

Timestamps use KB-standard local timezone, 24-hour format.

Type values:

```text
scan           Regular scan
daily          Daily review
weekly         Weekly review
monthly        Monthly archive
no_tasks       No executable tasks
failure        Failure report
```

## Report Structure

```markdown
# Task Hub Run Report

## Run Information

## Scan Scope

## This Round's Processing

## Output Files

## Manual

## Exceptions and Root Causes

## Next Steps
```

## Required Content

- Run time
- Trigger source
- Prompt file used
- Task count scanned
- Task identifiers processed
- State changes
- Absolute paths actually written
- Explanation when no tasks

Trigger source values registered in this KB library; deprecated trigger channels leave one archived record in automation registry, not as active value in trigger source enum.

"Explanation when no tasks" cannot be omitted—writing "no executable tasks this round" and writing nothing are two different things: first proves scan ran, second leaves it unclear whether scan ran or just had no results.

## Checklist

- [ ] Inspection report uses flat naming `{YYYYMMDD}-{type}.md`
- [ ] Workflow runs use directory style, do not apply this methodology in full
- [ ] All seven sections present
- [ ] All eight required items filled
- [ ] Write paths are absolute paths

## Change Log

> Rolling window; keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-14 | Reports land in the scan task dir; date-only naming |
| 2026-08-07 | Generalized from run report specification |
