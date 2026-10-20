---
document_id: awp-knowledge-management-standard/methodology/commerce/kb-method-commerce-scanning
language: en
publication: public
title: "Business Direction Scanning Methodology"
---

# Business Direction Scanning Methodology

> Manage one thing: continuously find new business opportunities in the knowledge base and judge whether a candidate deserves continued attention investment.
> Not managing already-committed business (that belongs to brand management), nor actual execution (that belongs to business implementation).

## Responsibility

Business direction scanning answers two questions:

1. What opportunities exist online right now?
2. Should we continue investing attention in this candidate?

It does not answer: existing product lists, confirmed target audiences, established competitor ecosystems. These three belong to brand management.

## Three Stages

```text
Discovery (find) → Evaluation (select) → Review (verify)
```

| Stage | What to do | Output to |
|-------|-----------|-----------|
| Discovery | Scan candidate directions from various signal sources | Pass to Evaluation |
| Evaluation | Deep analysis of candidates, make continue-or-abandon decisions | Pass to brand management or business implementation |
| Review | Look back at completed directions, verify initial judgment | Can feed back to Discovery |

### Why only three stages

No execution stage. Committed business lives in brand management, actual implementation in business implementation. Adding execution to the scanning pipeline would create three copies of the same thing.

### Why stages aren't numbered

Numbering (1-Discovery, 2-Evaluation, 3-Review) suggests a pipeline where every candidate must travel through all stages. That's not true—most candidates get eliminated at Discovery, a few jump straight to implementation. The names themselves clarify semantics; numbering only adds confusion.

## Three-Part Correspondence

Every scanning module consists of three aligned parts, growing and shrinking together:

```text
Methodology ↔ Workflow ↔ Output directory
```

| Component | Answers what | Example |
|-----------|------------|---------|
| Methodology | According to what process do we scan | One file under `{commerce_root}methodology/` |
| Workflow | What are the concrete steps | One workflow under `{workflows_root}` |
| Output directory | Where do scanned items go | `{commerce_root}{stage}/{module_name}/` |

When building a new scanning module, all three must be created together; if any is missing, the module won't run. When deleting, delete all three together.

## Three-Part Kit

Every scanning module's output directory holds three fixed components:

```text
{stage}/{module_name}/
├── daily_scan/        ← Single-run reports, one file per run
├── index.md           ← Full aggregation, conclusions from all rounds concentrated here
├── pending_{next_stage}.md  ← Handoff to next stage
└── CLAUDE.md          ← Says which workflow this module maps to
```

| File | Responsibility | Criterion |
|------|----------------|-----------|
| `daily_scan/` | Single-run report | One file per run, don't append to old files |
| `index.md` | Full aggregation | Refresh relevant entries after each round |
| `pending_*.md` | Handoff list | Filename clarifies next stage (`pending_evaluation.md` / `pending_implementation.md`) |
| `CLAUDE.md` | Routing | Only state which workflow it maps to, not rule text |

When a module needs additional resources (e.g., long-maintained candidate list), note in the module's `CLAUDE.md` what it is and why it's separate, but it doesn't replace any of the three parts.

## Handoff Relationships

Each stage has a clear next stop; handoff happens via `pending_*.md`:

| Output source | Handoff file | Recipient |
|---------------|-------------|-----------|
| `discovery/{module}/` | `pending_evaluation.md` | Evaluation stage deep analysis |
| `judgment/deep_analysis/` | `pending_implementation.md` | Brand management or business implementation |
| Brand management business model directory | `pending_review.md` | Review stage |
| `review/retrospective/` | `index.md` | Can feed back to Discovery stage |

## Where decisions belong

Scanning decisions and brand management are different; putting them in the wrong place creates duplicate records:

| Content | Goes to | Criterion |
|---------|---------|-----------|
| Continue or abandon candidate direction | `{commerce_root}judgment/decision/` | Not yet decided, it's a ruling on a candidate |
| Product lists, pricing | `{brand_root}{brand}/management/business_model/` | Already decided, it's management fact |
| Target audience | `{brand_root}{brand}/management/audience/` | Already decided |
| Competitor landscape | `{brand_root}{brand}/management/competitors/` | Already decided |

One-sentence criterion: **Things still being decided go to scanning decisions; things already decided go to brand management.**

## Run on demand, not scheduled batches

Scanning modules trigger on-demand—run when you have questions, not all modules together daily.

- Stopping a module's scheduler doesn't mean it's offline.
- Scanning modules have no permanent staff.
- Discovery stage can select lines on demand; cheaper modules can run in parallel.

## Blue ocean gate

Candidates must pass blue ocean check before entering `pending_evaluation.md`. Red ocean candidates stay in daily scan reports as records, don't enter evaluation—evaluation costs much more than discovery, wasting it on red ocean is inefficient.

Each scanning module's methodology defines specific check items; this methodology only mandates that this gate exists.

## External intelligence

`{commerce_root}market_perspective/` holds intelligence collected externally, not self-scanned candidates:

| Subdirectory | Holds what |
|--------------|-----------|
| `discovery-industry_trends/` | What's happening in the industry |
| `evaluation-perception_gaps/` | How others see it, how our view differs |
| `best_practices/` | Proven approaches others have tested |

## Boundaries

```text
Direction scanning (find opportunities) ⇄ Brand management (people + committed business) → Business implementation (actually do it)
```

- Scanning decisions can harden into brand management; brand management conclusions flow back to scanning periodically.
- Don't create management state directories in scanning (business model, audience, competitors).

## Checklist

**Starting a new scanning module**

- [ ] Output directory path is `{commerce_root}discovery|evaluation|review/{name}/`, no number prefix
- [ ] Methodology, workflow, output directory all three present
- [ ] Added one line to `{commerce_root}CLAUDE.md`
- [ ] Workflow's top states it's on-demand trigger
- [ ] Three-part kit complete: `daily_scan/` + `index.md` + `pending_*.md`
- [ ] Blue ocean gate defined in this module's methodology

**Business model or product list changes**

- [ ] Only modify brand management, don't touch scanning pipeline directories

## Changelog

> Rolling window, keep last 3 entries, ≤20 chars each.

| Date | Change |
|------|--------|
| 2026-08-07 | Extracted methodology from business specs |
