---
document_id: awp-knowledge-management-standard/methodology/personal/kb-method-personal-leisure
language: en
publication: public
title: "Personal Leisure Domain Methodology"
---

# Personal Leisure Domain Methodology

> Manage one thing: how to write files in personal leisure domain (film & TV, travel, food, hobbies).
> Inherits personal domain constraints (privacy classification, decision/record/reference three-output skeletons), this file only declares leisure-specific additions.

## Responsibility

Leisure domain records "joy" — film & TV, travel, food, hobbies. It answers background Agent needs when recommending films, planning trips, finding restaurants, deepening interests.

## Four Design Principles

- **Three-state grouping** — leisure files naturally have completed / in progress / want to do three states; organize all lists this way.
- **Personal viewpoint essential** — must have own rating or one-liner. Pure curated lists are platforms' job, not KB's.
- **Separate from creation materials** — personal viewing experience belongs here; creation quotes using media belong in reference materials or research.
- **Privacy defaults public or internal** — leisure info usually shareable.

## Required Files

| File | Type | Required Content |
|------|------|---------|
| `film-list.md` | Reference | Watched / Watching / Want to Watch three states + rating + one-liner |
| `travel-list.md` | Reference | Been / Planned / Want to Go three states + time + one-liner feeling |

## Recommended Files

| File | Type | Recommended Content |
|------|------|---------|
| `food-{city}.md` | Reference | Restaurants + rating + recommended dish + notes |
| `trip-{destination}.md` | Record | Single trip guide, diary, photo references |
| `hobby-{topic}.md` | Decision & Reference | Hobby deepening direction + resource or gear list |

## Add Per Status

| Status | Additional File | Privacy Level |
|------|---------|---------|
| Collections | `collection-{category}.md` | Internal or Sensitive |
| Car Owner | `car-maintenance.md` (model, maintenance, registration) | Internal |
| Sports Fan | `sport-tracking-{sport}.md` | Public |
| Reading | Go to growth domain book list, don't duplicate | — |
| Gaming | `game-library.md` (beat / playing / want to play) | Public |
| Photography or Crafts | `portfolio.md` | Internal |

## Three-State Grouping

All list-type files must organize by "completed / in progress / want to do":

```markdown
## Watched

| Title | Rating | One-liner |
|------|:----:|--------|

## Watching

| Title | Progress | Notes |
|------|------|------|

## Want to Watch

| Title | Recommended By | Priority |
|------|--------|--------|
```

Forbidden: mixing three states in one table — mixing makes quick decisions impossible, reverts to platform curation.

## Personal Viewpoint Hard Requirement

Each list entry must have at least one:

- Rating (number or star)
- One-liner evaluation
- Recommend or don't-recommend mark
- Tag

| Good | Bad | Reason |
|----|-----|------|
| `"Title" / 9 / Great visuals, slow pacing` | `"Title"` | Former has decision value |

Just listing title with zero viewpoint = not recorded.

## Privacy Defaults

| File | Default Level |
|------|---------|
| Film list, game library, sports tracking | **Public** |
| Travel list (places + dates) | **Internal** |
| Single trip diary (specific itinerary) | Internal or Sensitive |
| Food list | Public or Internal |
| Hobby notes | Public or Internal |

## Deduplication with Other Domains

| Content | Belongs To | Does Not Belong To |
|------|------|------|
| Reading book list | Growth domain book list | Leisure domain |
| Travel video production file | Business area video project | Leisure domain |
| Film/media creation reference | Reference materials or research | Leisure domain |
| Travel tool | Best practices | Leisure domain |
| Hobby commercialized (becomes product) | Brand product domain | Leisure domain |

## Checklist

- [ ] Metadata contains type, privacy level, update date
- [ ] List organized by three states
- [ ] Each entry contains rating or one-liner evaluation
- [ ] No duplication with growth domain book list
- [ ] No duplication with business video production
- [ ] Personal viewpoint explicitly present, not pure curation

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from leisure specification |
