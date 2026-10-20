---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-event
language: en
publication: public
title: "Business Methodology  -  Event Archive"
---

# Business Methodology  -  Event Archive

> Manage complete record of one-time major events: planning, execution, retrospective—three phases.
> Inherits all constraints from `kb-method-business-general.md`, this file adds only what applies to event archive specifically.

## I. What We Manage

One-time major events: product launch, conference, promotion, IPO, anniversary, crisis, keynote speech, partnership signing, industry summit.

Difference from adjacent classes:

| Compared To | Difference |
|-------------|-----------|
| Project Record | Events organize by **time point or time range**; projects by **deliverable** |
| Operations Data | Events are **discrete occurrence**; operations data **periodic output** |

## II. Four Core Principles

- **Three-phase structure**: Every event has before (planning), during (execution), after (retrospective).
- **Event data traceable**: Data, photos, videos, feedback from the event must be archived.
- **Retrospective priority**: Event itself passes; retrospective has long-term value.
- **Materials sediment**: Reusable materials from the event should sediment to visual asset library or research library.

## III. Three-Phase Skeleton

```text
{event_directory}/
├── event.md              # Metadata + Facet + Overview
├── planning/             # Pre-event planning files
├── execution/            # Event-day or event-week records
└── retrospective/        # Post-event retrospective and material sedimentation
```

### `event.md` Extra Required Fields

Beyond nine universal fields, add:

| Field | Explanation |
|-------|-------------|
| Event Type | Launch / Conference / Promotion / Crisis / Keynote / Signing / Ceremony / Other |
| Event Date | `YYYYMMDD` (single day) or `YYYYMMDD to YYYYMMDD` (multi-day) |
| Event Location | Online or offline venue; sensitive locations can be de-identified |
| Scale and Budget | Participant count, budget; use range or magnitude, not exact |
| Host and Partners | Host + partners; cross-reference customer relationships |

## IV. Planning Phase Required

| Section | Content |
|---------|---------|
| Objectives | What should this event achieve, quantifiable preferred |
| Timeline | Key milestone timeline |
| Materials Checklist | Materials to prepare; cross-reference visual asset library or mark new-build |
| Workplan | Who does what; cross-reference customer relationship or team |
| Budget | Budget line items; range or magnitude, avoid exact |
| Risks | Main identified risks and response |

## V. Execution Phase Required

| Section | Content |
|---------|---------|
| Event Record | Rolling time-ordered record of what happened |
| Attendance and Participation | Actual attendees or participants, demographics; can de-identify |
| Immediate Feedback | Key feedback captured on-site |
| Anomalies | Items differing from plan |

Recommend attaching photo, video, screenshot references; actual files stay in project production directory or visual asset library.

## VI. Retrospective Phase Required

| Section | Content |
|---------|---------|
| Objective Achievement | Evaluate each objective from planning |
| Data Summary | Attendance, conversion, reach, media coverage and other quantifiable metrics |
| What Went Right | Replicable practices |
| What Went Wrong | Pitfalls to avoid next time |
| Material Sedimentation | Index of reusable material output, cross-reference visual asset library or research library |
| Follow-up Actions | Action items arising from event |

## VII. Recommended Sections

| Section | Explanation |
|---------|------------|
| Media and Public Statement | Outbound communication text; mandatory for crisis events |
| Compliance Record | Items requiring compliance/approval |
| Budget Settlement | Comparison with planned budget; range or magnitude |
| Photo/Video Inventory | Archive index of multimedia |

## VIII. Industry-Specific Optional Sections

| Event Type | Add Recommended |
|------------|-----------------|
| Product Launch | Media list, propagation data, market response |
| Conference, Trade Show | Booth, logistics, lead list |
| Promotion | Rules, sales breakdown, customer persona |
| Crisis | Timeline, public statement, legal consultation, subsequent impact |
| Keynote, Lecture | Slides, recording, audience feedback |
| Partnership Signing | Contract key points, effective conditions (full contract in credential library) |
| Ceremony (opening, anniversary) | Program flow, guest list, remarks |
| Academic Conference | Papers, reports, collaboration intent |

Industry-optional sections add structure internal to three phases only; do not create new top-level structure.

## IX. Naming

`{event_name}-{YYYY-MM}.md`, or directory `{event_name}-{YYYY-MM}/`.

```text
Good:
  {launch_name}-2026-04/
  {promotion_name}-2026-11/
  {crisis_shorthand}-2026-03/

Bad:
  2026-04-{event}/     ← Date prefix prohibited
  event1/              ← No semantics
  {vague_shorthand}/   ← No time
```

## X. Deduplication Boundaries

| Content | Goes To | Does Not Go To |
|---------|---------|----------------|
| Recurring event | Operations Data or Operating Asset | Event Archive |
| Ongoing project work | Project Record | Event Archive |
| Product launched in event | Project records product; this section records launch | Both |
| Event-generated operations data | Operations Data | Cross-reference |
| Event planning process | Workflow Library | Event Archive |
| Reusable event material output | Visual Asset Library | Material Sedimentation |
| Private celebration | Personal Area | Business Event Archive |

## XI. Checklist

**Planning Phase**

- [ ] `event.md` contains nine fields + five event-required fields
- [ ] Objectives quantifiable or evaluable
- [ ] Timeline includes key milestones
- [ ] Risk inventory at least 3 items
- [ ] Budget uses range or magnitude

**Execution Phase**

- [ ] Event record time-ordered rolling
- [ ] Anomalies recorded
- [ ] Multimedia files in place

**Retrospective Phase**

- [ ] Objective achievement evaluated per item
- [ ] "Went right" and "went wrong" each at least 3 items
- [ ] Material sedimentation index cross-references visual asset library
- [ ] Follow-up actions listed
- [ ] `event.md` state set to "archived"

## Change Record

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Migrated from event archive spec and generalized |
