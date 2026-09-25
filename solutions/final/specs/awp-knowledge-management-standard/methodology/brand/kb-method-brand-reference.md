---
document_id: awp-knowledge-management-standard/methodology/brand/kb-method-brand-reference
language: en
publication: public
title: "Reference Materials Methodology"
---

# Reference Materials Methodology

> Managing collection, organization, and maintenance of brand context knowledge: file skeletons and shared rules for 6 reference types.
> Applicable to any industry, any brand.

---

## Positioning

Reference materials are the brand's ammunition depot—the Agent calls frameworks, data, cases, viral patterns, term definitions, and authoritative citations on demand when writing content.

This methodology manages two things:

1. Each of the 6 reference types' file skeleton
2. Collection, maintenance, and citation rules shared by all reference materials

**Landing spot**: the 6 types enter corresponding context directories per the competitor-analysis four-component model—benchmarking types into `benchmarking/`, data types into `market/`, framework and template types into `methodology/`. This methodology only defines type skeletons; exact paths follow each context directory's index. The four-component model see `kb-method-brand-competitor.md`.

---

## Design Philosophy

- **Classify by function, not by medium**: organize by "what it's used for" (framework / data / viral / case / term / citation), not by "where it came from" (book / report / article).
- **Citable is the floor**: every reference item must have a source; the Agent can name the origin when citing.
- **Collection and distillation separate**: raw material may be redundant, but distilled reference items must be structured and machine-readable.
- **Extend on demand**: the 6 types are not a closed set. When new reference needs appear, create new types per the shared rules.

---

## The 6 Reference Types at a Glance

| # | Type | Directory | When to call | Content unit |
|---|------|------|------------|---------|
| 1 | Framework | `framework/` | When a thinking model is needed | One book or methodology → one file |
| 2 | Data | `data/` | When data support is needed | A set of reports → clustered by topic |
| 3 | Viral | `viral/` | When content benchmarking is needed | One platform → multiple accounts → single items |
| 4 | Case | `case/` | When real examples are needed | One business scenario → one file |
| 5 | Term | `term/` | When term unification is needed | One domain → one file |
| 6 | Citation | `citation/` | When authoritative backing is needed | One person or source → one file |

✅ Every type's root directory must have an index file.

---

## Type by Type

### ① Framework

**Positioning**: reusable thinking models distilled from books, content products, methodologies, etc.

**Directory structure**:

```
framework/
├── CLAUDE.md           ← index: categories + bibliography + usage
├── {category A}/
│   └── {book or methodology name}.md
└── {category B}/
```

**Single-file skeleton** (✅ required sections):

| # | Section | Content |
|---|------|------|
| 1 | Title plus one-line summary | `# {book name}` + `> {author}|{original title}` + `> **One line**: {core thesis}` |
| 2 | Core model | The book or methodology's key model, structured with diagrams plus lists |
| 3 | Citable quotes | Original quotes with quotation marks |
| 4 | Call scenarios | Which scenarios call this framework |

⚪ Optional sections: pros-and-cons comparison, relationships with other frameworks.

❌ No full book excerpts—framework files hold distilled reusable models only, not reading notes.

| Good | Bad | Why |
|----|-----|------|
| Core model structured with tables and diagrams | Large blocks of original text copied | The former the Agent can call directly |

---

### ② Data

**Positioning**: citable data and trend insights extracted from institutional reports, surveys.

**Directory structure**:

```
data/
├── CLAUDE.md           ← index: categories + report count + usage
└── {topic category}/
    └── CLAUDE.md       ← that topic's clustered data file
```

**Topic data file skeleton** (✅ required sections):

| # | Section | Content |
|---|------|------|
| 1 | Title plus positioning | One line on what this topic covers |
| 2 | Report index | Table: number / report name / institution / sample / publish date / core viewpoint |
| 3 | Key data | Clustered by subtopic, each item annotated with source report number |
| 4 | Trend insights | Conclusions from cross-validating multiple reports |

⚪ Optional sections:

| Section | When it fits |
|------|---------|
| Citation guide | Brands with external content needs, scenario-based citation script templates |
| Data usage notes | When data has metric-definition differences or sample bias |
| Full citation | Formal citation format of the report |

**Key data format**—✅ every item must have a source annotation:

```markdown
| Metric | Value | Source |
|------|------|------|
| {metric name} | **{value}** | R1 {institution name} |
```

❌ No unsourced data—data without a source can't be cited.

---

### ③ Viral

**Positioning**: full-text collection plus pattern breakdown of peers' or competitors' high-reach content.

**Directory structure**:

```
viral/
├── CLAUDE.md           ← index: platform + accounts + usage
└── {platform}/
    ├── CLAUDE.md       ← platform index: account list + viral-formula quick reference
    ├── viral-formula/  ← that platform's pattern breakdown
    │   ├── 01-structure-and-hook.md
    │   ├── 02-language-and-style.md
    │   └── 03-rhythm-and-psychology.md
    └── {account name}/
        ├── CLAUDE.md   ← account metadata: positioning / style / viral traits
        └── {content}.md   ← single item full text
```

**Three-layer structure rules**:

| Level | Index must contain |
|------|---------|
| Root | Platform list plus usage |
| Platform | Account list plus viral-formula quick reference table |
| Account | Positioning, style traits, follower scale |

**Viral-formula file skeleton** (⚪ optional but recommended)—✅ if present, split by three dimensions:

1. Structure and hook: patterns of opening, title, call to action
2. Language and style: patterns of word choice, sentence shape, emotional expression
3. Rhythm and psychology: information density, emotion curve, completion and watch-through strategy

**Single content item file**:

- ✅ Keep the original full text
- ⚪ May append metadata: publish time, performance, platform
- ❌ Never modify the original text—its reference value is the authentic original

---

### ④ Case

**Positioning**: real business cases for teaching or argumentation—who solved what problem with what tool, and what results.

**Directory structure**:

```
case/
├── CLAUDE.md           ← index: classified by industry or scenario
└── {case name}.md
```

⚪ When cases are many, subdirectories by industry or scenario are allowed.

**Single-file skeleton** (✅ required sections):

| # | Section | Content |
|---|------|------|
| 1 | One-line summary | who + with what + solved what + results |
| 2 | Background | Who the case subject is, what problem it faced (2–5 sentences) |
| 3 | Solution | What tool or method was used, how it was done |
| 4 | Results | Quantifiable outcomes, data first |
| 5 | Source | Case origin: URL, report name, or interview source |

⚪ Optional sections: takeaways, limitations.

| Good | Bad | Why |
|----|-----|------|
| "A restaurant used automation tools to handle orders, saving 40 hours a month" | "Automation can improve efficiency in the restaurant industry" | The former is a concrete case, the latter empty talk |

❌ No fabricated cases—every case must have a traceable source.

---

### ⑤ Term

**Positioning**: standard definitions of core concepts, ensuring term consistency when the Agent writes.

**Directory structure**:

```
term/
├── CLAUDE.md           ← index: domain categories + term quick reference
└── {domain}.md           ← terms organized by domain
```

**Single-file skeleton** (✅ required format)—every term uses a unified table:

```markdown
### {term name}

| Field | Content |
|------|------|
| English | {English term} |
| One line | {standard definition ≤30 characters} |
| Detail | {2–3 sentence expansion} |
| Easily confused with | {similar terms and the difference} |
```

⚪ May append "Example usage" field.

- ❌ No term files becoming encyclopedias—each term's detail explanation ≤100 characters
- ❌ No duplicate definitions of the same term across multiple domain files

---

### ⑥ Citation

**Positioning**: high-frequency cited authoritative people or sources, called when content needs endorsement.

**Directory structure**:

```
citation/
├── CLAUDE.md           ← index: people and sources list + topic quick reference
└── {person or source name}.md
```

**Single-file skeleton** (✅ required sections):

| # | Section | Content |
|---|------|------|
| 1 | Person or source intro | One sentence on why authoritative: identity plus achievement |
| 2 | Citation list | Original text plus source plus applicable scenario, in a table |

**Citation list format**:

```markdown
| Original text | Source | Applicable scenario |
|------|------|---------|
| "{original}" | {book/speech/article}, {year} | {which argument needs this citation} |
```

- ✅ Every citation must have a source
- ❌ No fabricated citations or misattribution

---

## Shared Rules

The following rules apply to all 6 reference types.

### Source Rules

- ✅ Every reference item must be traceable to a source
- ✅ Source format: `{author or institution}, {work name}, {year}. {URL}`, attach URL when present
- ❌ No unsourced data, citations, or cases

### Index Rules

- ✅ Every type's root directory must have an index file
- ✅ Index contains: type positioning + file and directory list + usage
- ✅ New content must sync the index update

### Timeliness Rules

- ⚠️ Data-type references (data, cases) over 1 year old should be annotated "as of {year}"
- ⚪ Framework-type references (framework, term) are less time-sensitive, no mandatory annotation
- ✅ Viral-type account metadata (follower counts etc.) updates annotated with date

### New-Type Rules

When a new reference type is needed:

1. Determine which context directory it belongs to (benchmarking / market / methodology)
2. Confirm functional naming, named by "what it's used for"
3. Define single-file skeleton, at least summary, core content, source three sections
4. Update the corresponding context directory's index
5. Update this methodology's type overview table

### Relationship with Other Brand Dimensions

| Reference type | Related dimension |
|---------|---------|
| Framework | Called on demand in content creation, doesn't directly affect brand definition |
| Data | Provides argumentation support for content, cross-validates with positioning's industry judgments |
| Viral | Provides benchmarking reference for writing style, complements expression style |
| Case | Provides material for content production, relates to product catalog |
| Term | Echoes the expression style's forbidden words and professional terms |
| Citation | Adds authority to content, consistent with positioning's values |

---

## Checklist

**New reference item**:
- [ ] Type determined (one of 6)
- [ ] File structure matches that type's skeleton
- [ ] Traceable source present
- [ ] Index file updated

**New reference type**:
- [ ] Functional naming, by "what it's used for"
- [ ] Directory and index file created
- [ ] Single-file skeleton defined
- [ ] Corresponding context directory's index updated
- [ ] This methodology's type overview table updated

**Periodic maintenance**:
- [ ] Any data-type references over 1 year without timeliness annotation
- [ ] Whether viral account metadata needs updates
- [ ] Each type's index file matches actual files

---

## Related Methodologies

| Topic | File |
|------|------|
| Context directory three-way split and four-component model | `kb-method-brand-competitor.md` |
| Identity layering and cascade impact | `kb-method-brand-identity.md` |

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted generic methodology from brand spec |
