---
document_id: awp-knowledge-management-standard/methodology/operations/kb-method-engagement-strategy
language: en
publication: public
title: "Operational Engagement Strategy Methodology"
---

# Operational Engagement Strategy Methodology

> Manage one thing: after proactively engaging on others' content (reply, comment, private message), how to learn from historical data and feed conclusions back into selection and writing.
> Does not govern account quota and scheduling (those are in operational role handbook), platform character limits and review policies (those are platform facts), nor writing style (that is writing methodology).

Applies to: replying or commenting on others' content, community private messages, cross-platform active engagement. Workflows with publish-only (no engagement) do not apply.

## Terminology

| Term | Definition |
|----|------|
| Engagement strategy | Selection and writing close-loop for replies, comments, private messages |
| Record | Leave engagement log and fields |
| Collect | Retrieve engagement data |
| Attribution | Slice-compare to identify which factor drove results |
| Feedback | Write conclusion back to selection strategy or reply style |
| Selection | Decide whose content to reply to |
| Four dimensions | Attribution cuts at least four ways: audience scale, timing, content style, topic |
| Object snapshot | Record other party's scale, topic, engagement count at time of action. Do not rewrite later. |
| Benchmark | Instance self-fills immediate, accumulation, long-tail threshold. |

## Four Design Principles

- **Close-loop** — Conclusion must flow back to selection and writing, else it is accounting, not strategy.
- **Strategy numbers are live** — After attribution stabilizes, overwrite old values directly. No backward compatibility, no historical branch.
- **Insufficient sample means no conclusion** — Only conclude after 20+ single-dimension samples. Rare signals can relax to 10, but mark "trend pending verification".
- **Framework generic, values in instances** — This methodology does not hard-code any numbers (follower sweet spot, reply window). Values live in each account strategy instance.

## Four Stages

```text
Record → Collect → Attribution → Feedback
```

| Stage | Responsibility |
|------|------|
| Record | Every engagement immediately to structured record + object snapshot |
| Collect | Fill result fields into same record at fixed times |
| Attribution | Slice-compare → update effect attribution |
| Feedback | Change selection strategy and reply style, record feedback entry |

### Record Format

Append each engagement to monthly reply log (`reply_log/{YYYYMM}.json`).

**Required fields**: engagement ID, engagement link, engagement text, expression template, publish time (ISO 8601), object snapshot, score, and result fields for each collection point (null if not yet collected).

**Object snapshot must record values at time of action**: other party ID and author, audience scale bracket, topic, crowding, timeliness, engagement count snapshot. Rewriting snapshot after fact pollutes attribution independent variable.

**Optional fields**: images, links, tags, notes.

### Collection

| Time | Action |
|------|------|
| Immediately after publish | Write record, result fields as `null` |
| 24h / 72h / 7d | Fill back into same record |

Slow-moving platforms can shift to 7d / 14d / 30d. Fill back **to same record**, do not create parallel record — two records double sample size and distort.

### Attribution

Three steps: **slice → compare → update**.

Attribution cuts at least these four dimensions:

| Dimension | Means | Field Example |
|------|------|---------|
| Audience scale | Other party's follower or subscriber bracket | `author_followers_tier` |
| Timing | Time since other party's content publish | `hours_after_source` |
| Content style | This reply's expression template | `reply_style` |
| Topic | Other party's content category | `topic_category` |

Write conclusion to strategy instance's attribution file. Keep separate dated snapshot copy.

Trigger: 20 items reached, or once per week, whichever first.

### Feedback

- Conclusion flows to selection strategy (change thresholds)
- Conclusion flows to reply style (change priority)
- Record one line in attribution file feedback table

Overwrite old strategy directly, do not keep branch — next person will not know which version to run.

### Benchmark

Each account instance self-fills three brackets (immediate / accumulation / long-tail) for key metrics. "Other party responded to me" gets its own column — it differs from exposure metrics and mixing them masks true engagement.

### Minimum Sample Size

Conclude only after 20+ single-dimension samples. If short, mark "insufficient sample". Rare but high-value signals can mark "trend pending verification" at 10, but cannot drive threshold changes.

## Instance Directory

```text
{business_root}{brand}/{channel}/operations/
├── CLAUDE.md
├── strategy/          # Selection, reply style, pacing, benchmark, attribution
├── data/          # Content performance, reply log, attribution snapshot
└── positioning/          # Account original
```

Workflow resource library does **not** stack full strategy text. Steps reference business strategy path.

## Coordination with Adjacent Layers

- Single account quota, scheduling, north star metric → **operational role handbook** priority.
- Workflow resource library holds creation and engagement craft (reference materials, identity loading, guardrails).
- Platform facts → platform rules. Writing style and format → writing methodology plus workflow materials. This methodology does not prescribe sentences.
- Where feedback lands → channel operations four-layer matching methodology.

## Checklist

- [ ] Workflow with engagement has interaction record skeleton
- [ ] Each engagement has complete required fields and object snapshot
- [ ] Collection points filled in, no parallel records created
- [ ] Attribution meets sample size before strategy change, feedback recorded
- [ ] Account-level rules follow operational role handbook
- [ ] Strategy values in instances, not hard-coded in this methodology

## Change Log

> Rolling window, keep last 3 entries, each ≤20 words.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from operations strategy spec |
