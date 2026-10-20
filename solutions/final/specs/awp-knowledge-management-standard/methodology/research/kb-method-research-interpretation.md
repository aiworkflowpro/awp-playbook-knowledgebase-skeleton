---
document_id: awp-knowledge-management-standard/methodology/research/kb-method-research-interpretation
language: en
publication: public
title: "Interpretation Card Methodology"
---

# Interpretation Card Methodology

> Manage One Thing: After read one source, write into what form—seven required chapters, depth standard by source-type, quality tier.
> Doesn't manage source collection in-repo, doesn't manage cross-source synthesis cognition (that's cognition-layer methodology).

## Responsibility

Interpretation card answer one question: **This source teach us what, how we use it.**

Difference with adjacent output:

| Adjacent | Difference |
|----------|-----------|
| Navigation | Navigation say "thing where" (chapter line-index supply per-excerpt source-text); interpretation say "thing use-what" |
| Raw & standard piece | Two are source-itself, interpretation is after-digest cognition |
| Cross-item synthesize | Synthesize consolidate multi-item, interpretation manage single-item |

One source one interpretation card, mutual-not-replace.

## Why Write This Deep

**Run once not-easy, output must match cost.**

Process one source need model read-full, input often ten-thousand token, this cost not-negligible. Interpretation card must squeeze-out all read value—core framework, operation step, case, quote, misconception, limit. Rather over-write then-delete, than under-write then-retry: retry mean re-read full-text.

**Deep standard core criterion**: Person never-read this source, only see interpretation-card, can-use it-core-method in self-work? Can—depth enough; can't—continue add.

## Seven Required Chapter

| # | Chapter | Answer What |
|---|--------|-----------|
| 1 | Frontmatter | Metadata |
| 2 | One-Line Position | What-is this source, for-who |
| 3 | Core Opinion | Author most-important claim what-is |
| 4 | Core Framework | Author propose what methodology, model, flow |
| 5 | Operation Step | Follow this-methodology how-exactly do |
| 6 | Insight for-Us | Relate-to own-business what-use |
| 7 | Quote Extract | Worth direct-quote from-source original-text |

Not hand-maintain "related source" section. Source-between relationship Agent establish by full-text search, topic-index, context-auto; single-card hand-maintain link only generate low-quality dead-link.

### By Source-Type Add Optional Chapter

| Chapter | When-Add |
|---------|----------|
| Key-Concept | Source introduce important-proprietary concept or-terminology |
| Case Parse | Source contain worth-separate-parse case |
| Common Misconception | Author explicit-point common wrong-do |
| Dispute & Limit | Author opinion have-dispute, or clear-applicable boundary |

## Chapter Title Only One Write-Way

**Required chapter use level-2 title, title text strict-follow above table, no-number, no-rephrase, no-level-1 title.** Write `## Core Framework`, not `## Framework Method`, `## 3. Core Framework` or `# Core Framework`.

Not pure-format-OCD. Interpretation-card machine and human read-together: complete-check rely chapter-title judge full-not-full, cognition extract rely locate which-segment read. Title rephrase machine judge missing-chapter, one-well-write card become calc-broken. Batch in-library most-easy three-format coexist—same meaning three-title-way, content all-there, pure-wording uneven, machine report-out massive "missing-chapter". Unify method build old-write mapping table, seen-write method all-change standard-name:

| Old Type | Unify-To |
|---------|-------|
| `source-position` this-kind position-describe | `one-line-position` |
| `framework-method` `method-framework` | `core-framework` |
| `inspiration` `relate-X-transfer` | `insight-for-us` |
| `key-sentence` `quote` `transferable-source` | `quote-extract` |
| `step-SOP` | `operation-step` |
| `reverse-antipattern-list` | `common-misconception` |
| `chapter-close-reading` `full-book-close-reading` | `case-parse` |

Long-card over-3-4 ten-thousand-word, put fine-title lower-into respective level-2 chapter, not-flat level-2.

## Line-by-Line Requirement

### 1. Frontmatter

```yaml
---
type: interpretation
source: {entry-dir-name-full}
topic: {entry-container-dir-name}
subtopic: {fine-direction}
created: YYYY-MM-DD
depth: {depth-value}
---
```

| Field | Explain |
|------|------|
| `type` | Fix `interpretation`, no-variant |
| `source` | Entry dir-name full, disk dir-name byte-exact. Not-truncate, not-already-remove-from-dir-name-char |
| `topic` | Equal entry container dir-name, path-match disk |
| `subtopic` | Fine direction; old-topic-name-before-reorganize can-put here tag |
| `created` | Create date |
| `depth` | Interpretation depth, value must fall below white-list, no-quote |

`source` and `topic` mismatch disk is most-common machine-check fail reason—tool rely these-two map card to entry, write-wrong report-fake-break.

#### `depth` Whitelist

By source-type abbreviate value, each-type have default:

| Type-Abbrev | Allow Value | Default |
|---------|---------|------|
| Book | `full-book`  -  `core-chapter`  -  `single-chapter` | `full-book` |
| Article | `full-text` | `full-text` |
| Video | `video` | `video` |
| Code-Repo | `repo-full-overview` | `repo-full-overview` |
| Report | `report` | `report` |
| Paper | `paper` | `paper` |
| Course | `course` | `course` |
| Case | `case` | `case` |
| Interview | `interview` | `interview` |
| Podcast | `podcast` | `podcast` |
| Dataset | `dataset` | `dataset` |

Free-style (standard / quick / extend this-kind) all-per-type default. 

### 2. One-Line Position

One-sentence say-clear this source what, for-who, not-exceed 50 char.

> **Criterion**: One-sentence clear it-solve what-problem, suit-who read, not-give classify-label.

| Good | Bad |
|----|-----|
| Product-position operation manual—teach step-by-step do positioning, not-only-theory | One-good-book about-positioning |
| Authority reference-book say-technical-detail, suit already-understand basic person lookup | Relevant-domain book |

### 3. Core Opinion

Author most important 1-3 claim. Each expand 3-5 sentence—not-only "author think X", say-clear "why author think X, support-X evidence what".

Word-require: 500-1000 char.

### 4. Core Framework

Most-important interpretation-card section. Source propose methodology, model, process time, must complete-parse:

- Framework every component or step must-list
- Each component explain meaning, operate-point, common-pit
- Component-between relationship (sequence-depend, parallel, hierarchy) say-clear
- Use table present structure-info

Word-require: Book 1500-3000, short-video or-article 500-1000.

> **Criterion**: Framework expand-to direct-do grain, reader not-must back-flip original.

| Good | Bad |
|----|-----|
| List all component, each one-line meaning, one-line operate-point, one-line pit | "Author propose five-step framework" one-sentence |
| Ten-step process use table list, each-step have do-what, key-detail two column | "Author give ten-step" then-only list title |

### 5. Operation Step

Transform core-framework into executable-sequence. Different-from "core framework": framework explain "what-is", operation explain "exactly how-do".

Must concrete-to "get new-project, step-one do-what, step-two do-what" grade.

Word-require: Book 800-1500, short-video or-article 300-600.

### 6. Insight for-Us

Must hook-to actual-business. Not "this method very-good", but concrete-say:

- Which business part can-use this method
- Which product or course can-learn
- Content create, search tuning, course-design which-scenario fit
- Pricing, brand, acquire which-decide can-refer

Each insight need 2-3 develop, not-only title-one-row.

Word-require: Book 800-1500, short-video or-article 300-600.

### 7. Quote Extract

Extract from source worth direct-quote original-text, each-attach one-sentence explanation.

Quantity-require: Book 5-15, short-video or-article 2-5.

> **Criterion**: Each extract-text attach one-sentence "why-this-matter", extract must-be true insight-sentence, not universal-phrase.

| Good | Bad |
|----|-----|
| Original + one-sentence say why-important | Only list original-text no-explain |
| Choose true-insight sentence | Choose "hard-work succeed" this-waste |

## By Source-Type Depth Standard

### Book

| Dimension | Standard |
|-----------|----------|
| Total word | Min 10000; long-book by-body-size tier-increase |
| Core framework | Each component or step all-expand, include operate-point & pit |
| Operation step | Executable—read complete can-direct do |
| Case | At-least extract 3 actual-case in-book |
| Quote | 5-15 |
| Depth criterion | Never-read book person, only see card, can-use book core-method |

### Video

| Dimension | Standard |
|-----------|----------|
| Total word | Long-video (>20min) 1500-3000; short-video (<5min) 800-1500 |
| Core framework | Extract video main-opinion & structure |
| Operation step | Video teach methodology time, transform executable-step |
| Quote | 2-5 |
| Depth criterion | Don't watch video, only see card, know video-what, how-use |
| No Transcript When | First transcript or-extract key-frame then-write card; card not-long-empty shell |

### Article

| Dimension | Standard |
|-----------|----------|
| Total word | Long (original >3000) 1000-2000; short 500-1000 |
| Core framework | Extract core-opinion & support-evidence |
| Quote | 2-5 |

### Paper

| Dimension | Standard |
|-----------|----------|
| Total word | 2000-4000 |
| Core framework | Research-question + method + core-find + limit |
| Operation step | Paper have practical-meaning time, transform usable-step |
| Data | Extract key-data & chart-conclusion |

### Code-Repo

| Dimension | Standard |
|-----------|----------|
| Total word | Min 2500 |
| Core framework | Capability-map, architecture, workflow, vs similar-item differ, use table-parse-component |
| Operation step | From pull-code to smoke-test executable-step |
| Quote | 2-5, can-extract project-description position-sentence |

### Report, Course & Other

Reference book standard 60% word-count, core-chapter no-cut; `depth` use type default.

## Quality Tier

| Level | Criterion | Apply-Case |
|------|---------|----------|
| **A  -  Deep Interpretation** | Satisfy all word and structure require, core-framework complete-parse, operation-step executable, insight concrete-to-business-scene | Main-battle topic core-source |
| **B  -  Standard Interpretation** | Satisfy structure-require but word lower-limit, some chapter brief | Normal source |
| **C  -  Quick Card** | Only one-line position + core-opinion, other-chapter empty | Low-priority source, initial-scan |

Batch-goal B-tier. Main-battle source later hand-upgrade A.

## Checklist

- [ ] Frontmatter six-field complete: `type` / `source` / `topic` / `subtopic` / `created` / `depth`
- [ ] `type` fix `interpretation`
- [ ] `source` equal entry-dir-name, byte-exact
- [ ] `topic` equal container-dir-name, path-match disk
- [ ] `depth` fall-in type-whitelist, value no-quote
- [ ] Seven required-chapter all-have content, level-2 title exact-standard-name
- [ ] Total word reach correspond-source-type minimum
- [ ] Core framework not-one-sentence—each-component expand
- [ ] Operation step concrete-to executable
- [ ] "Insight for-Us" hook-to actual-business-scene
- [ ] Quote count meet-require, each-attach explain

## Change Log

> Rolling window, retain last 3 entries, ≤20 characters each.

| Date | Content |
|------|---------|
| 2026-08-07 | Generalized from interpretation-spec |
