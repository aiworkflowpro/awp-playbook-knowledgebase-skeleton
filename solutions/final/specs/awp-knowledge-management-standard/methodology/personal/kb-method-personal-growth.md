---
document_id: awp-knowledge-management-standard/methodology/personal/kb-method-personal-growth
language: en
publication: public
title: "Personal Growth Domain Methodology"
---

# Personal Growth Domain Methodology

> Manage one thing: how to write files in personal growth domain (reading, learning, reflection, skills).
> Inherits personal domain constraints (privacy classification, decision/record/reference three-output skeletons), this file only declares growth-specific additions.

## Responsibility

Growth domain records "heart" — non-work skills, reading, reflection, personal evolution. It answers background Agent needs when recommending books, planning learning, citing past reflection.

## Three Design Principles

- **Learning and reflection separated** — book lists and courses are **reference** (continuously append), reflection is **record** (time snapshot), skill progress is **decision** (long-term goal). Three types have completely different update rhythms; mixing interferes.
- **Quality over quantity** — don't record "read 100 books" vanity; only record what truly influences you.
- **Separate from work skills** — work-related technical learning belongs in best practices; this domain only manages "non-work" or "beyond-work" growth.

## Required Files

| File | Type | Required Content |
|------|------|---------|
| `book-list.md` | Reference | Read / Reading / Want to Read three states + rating + impact level |
| `reflection-{year}.md` or `reflection-{year}-Q{quarter}.md` | Record | Phase review and insights; archive cross-year |

## Recommended Files

| File | Type | Recommended Content |
|------|------|---------|
| `course-list.md` | Reference | In Progress / Completed + evaluation |
| `skill-{name}.md` | Decision | Skill learning goal, path, progress, review |
| `annual-review.md` | Record | Annual overall review; continuously append |

## Add Per Phase

| Phase | Additional File | Notes |
|------|---------|------|
| Language Learning | `language-{language}.md` (goals, resources, progress) | Decision & Reference mixed |
| Certification Prep | `certification-{name}.md` (registration, materials, practice test, result) | Phase records |
| Study Abroad or Immigration | `application-{school or country}.md` | Sensitive |
| Writing Practice | `writing-log-{year}.md` | Separate from brand creation |
| Meditation or Spirituality | `inner-record.md` | **Prefer not to store** |

## Privacy Defaults

| File | Default Level | Notes |
|------|---------|------|
| Book list, course list | **Public** | Usually shareable |
| Phase reflection | Internal; drops to Sensitive if contains personal vulnerability | — |
| Study abroad / immigration | Sensitive | Contains personal materials |
| Inner records, spirituality | **Prefer not to record** | Highly sensitive; hesitate before KB entry |

## Deduplication with Other Domains

| Content | Belongs To | Does Not Belong To |
|------|------|------|
| Work technical learning notes | Best practices | Growth domain |
| Own brand course definition | Brand product domain | Growth domain (own courses don't count as "in learning") |
| Quotes from creation references | Reference materials or research area | Growth domain |
| Personal certificates and credentials | Certificate archive or business area | Growth domain |

## Checklist

- [ ] Metadata contains type, privacy level, update date
- [ ] Book list organized by three states
- [ ] Reflection organized by year or quarter as independent files
- [ ] Work technical content moved to best practices
- [ ] High-sensitivity content (spirituality, inner records) not in knowledge base

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from growth specification |
