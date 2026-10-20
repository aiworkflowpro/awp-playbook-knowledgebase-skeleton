---
document_id: awp-knowledge-management-standard/methodology/commerce/kb-method-commerce-dailyscan
language: en
publication: public
title: "Daily Scan Report Methodology"
---

# Daily Scan Report Methodology

> Managing what a daily scan report should look like—five fixed sections, each section's word-count floor, and required fields.
> Not managing file names and placement (that's in the direction-scanning methodology), nor which scoring system each scan module uses (each module decides its own).

## Responsibility

A daily scan report is one run's output of a scan module. Its value isn't listing results, but showing **what framework was used to think and why this conclusion was reached**.

A daily scan report must be self-sufficient: a reader gets all information from this one file alone, no need to look up paths elsewhere.

## Five-Section Skeleton

Every daily scan report must contain these five sections, order not adjustable:

| # | Section | Length | Answers what |
|---|------|------|---------|
| 1 | Run summary | ≤100 characters | Whether this run is worth a closer look |
| 2 | Thinking-framework section | ≥500 characters | What framework was used to think, how the conclusion was reached |
| 3 | Candidate directions | ≥200 characters each | What was found, what the evidence is |
| 4 | Three lists | Unlimited | Newly emerged / status refreshed / eliminated |
| 5 | Run metadata | Fixed fields | Machine-readable record of this run |

### 1. Run Summary

One sentence answering: what this round did, how many scanned, how many candidates found, how many passed blue-ocean checks. A decision maker reads this section and can judge whether to keep reading.

### 2. Thinking-Framework Section

This is the daily scan report's core value.

| Requirement | Explanation |
|------|------|
| ≥500 characters | Excluding titles and tables |
| Reflects the methodology's core logic | Walk the module's methodology framework fully, not generic analysis |
| Writes the reasoning process | Not just the conclusion—how evidence led to the conclusion |
| Data-supported | Search counts, hit rates, signal strength, etc. |

Which angles each scan module's thinking framework must cover is written in that module's own daily scan template. Modules without a separate definition follow "walk that methodology's core logic + blue-ocean checks + evidence," same 500-character floor.

### 3. Candidate Directions

Expand this round's found candidates one by one. Each candidate must include:

| Required field | Explanation |
|--------|------|
| Direction name + one-line positioning | What this is, who it serves |
| Score + grade | Per that module's scoring system |
| Evidence (≥3 items) | Real sources: links, posts, data sources |
| Competitor landscape | Top 2–3 players' positioning, pricing, weaknesses |
| Blue-ocean check results | Item-by-item results + overall verdict |
| Action recommendation | Into pending-review / keep tracking / eliminate, with reason |

### 4. Three Lists

| List | Content |
|------|------|
| Newly emerged | Directions appearing this round for the first time: identifier, name, score, recommended status |
| Status refreshed | Existing directions' score and status changes this round: identifier, old value → new value |
| Eliminated | Blocked directions: identifier, elimination reason |

When a list is empty this round, write "None this round," don't omit the heading. Omitting the heading makes readers unable to tell empty from forgotten.

### 5. Run Metadata

```text
run_id: {module-abbreviation}-{YYYYMMDD}-{sequence or pattern}
cadence: on-demand / automatic / manual
date: YYYY-MM-DD
duration: {minutes}
search_calls: {number of search calls}
candidates_generated: {total candidates}
candidates_survived: {number passing blue-ocean checks}
```

## Five Rules

1. **Report self-sufficiency**—one report holds all information, no external paths for readers to find themselves.
2. **Evidence from real searches**—no fabricating sources from impressions.
3. **Scoring system module-defined**—modules have different judgment dimensions, not unified here.
4. **File name unified** `{YYYYMMDD}{HHMM}-{description}.md`; `HHMM` is run time, automatic runs write `0000`.
5. **Update the index after writing**—after each daily scan, append or refresh that direction's entry in the module's `index.md`.

## Checklist

- [ ] All five sections present, order not adjusted
- [ ] Run summary ≤100 characters
- [ ] Thinking-framework section ≥500 characters, reasoning process written not just conclusion
- [ ] Each candidate ≥200 characters, all six required fields present
- [ ] Each candidate's evidence ≥3 items, all real sources
- [ ] Three lists all present, empty ones write "None this round"
- [ ] Run metadata all seven fields present
- [ ] `index.md` updated

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from daily-scan format spec |
