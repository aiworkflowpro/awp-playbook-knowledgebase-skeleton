---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-planning
language: en
publication: public
title: "Business Methodology  -  Project Planning"
---

# Business Methodology  -  Project Planning

> Manage complete planning from 0 to 1 for new directions, new tracks, new products: five-stage pipeline, four evidence hard gates, plan document skeleton.
> Inherits all constraints from `kb-method-business-general.md`; this file only adds project-planning-specific sections.

## One. What to Manage

Complete project launch from 0 to 1: theory building, market research, track validation, business model design, brand planning, execution plan, tool planning, knowledge base filling.

Output is a **executable planning document**.

This file manages "how to create a good planning proposal", not "the specific business content in the proposal".

### Landing Point

The planning proposal itself is in-flight; lands in the research area per `{research_root}/{YYYYMM}/{YYYYMMDD}-plan-{object}-{status}/` structure. Directory naming and placement follow research area rules; this file only manages "what should a proposal look like", no duplication.

After planning runs successfully, the resulting business entity lands under business root.

### Handoff with Other Classifications

```text
Project Planning (this file) → Strategy Decisions (record key decisions) → Project Archive (record execution) → Operational Assets (launch resources) → Operational Metrics (periodic reports)
```

## Two. Seven Principles

- **Research first**: Research without methodology is blindfold exploration. Build theory first, then analyze markets with methods.
- **Data-driven**: Every decision needs data support, no pure intuition.
- **Evidence hard gates**: Research, proposal, launch, revenue verification each have clear pass criteria. Hard gates check evidence only, not product phasing.
- **Reuse first**: Don't rebuild tools, content, processes that can be reused. Inventory existing assets first, then decide on new builds.
- **Don't hardcode**: Don't hardcode specific platforms, tools, prices in proposals; use role names, fill concrete values at execution time.
- **Sync knowledge base**: Update knowledge base as far as execution goes; sync brand and business directories.
- **Plans and business separate**: Don't build directories under business root until proposal launches; avoid empty shells.

### Positive vs. Negative Contrast

| Good | Bad | Reason |
|----|-----|------|
| Keyword data table + difficulty score, decide track accordingly | "Feel like this direction is good" | Former data-driven, latter pure intuition |
| Read 5 books for theory first, then research | Just search keywords | Unstructured research misses dimensions |
| List existing tools first, decide new build | "Need a new tool here" | Avoid wheel reinvention |
| Proposal in research area, directory name with status word | Build "planning" directory under business root | Former status flows; latter is empty shell |
| Evidence hard gates fail → pivot or stop | Research bad but continue anyway | Hard gates prevent sunk-cost trap |

## Three. Five-Stage Pipeline

```text
Stage 0 Theory Building → Stage 1 Research Validation → Stage 2 Plan Design → Stage 3 Infrastructure Launch → Stage 4 Operations Growth
                                       ↑                              ↑                              ↑
                                Evidence Hard Gate 1         Evidence Hard Gate 2         Evidence Hard Gate 3
```

Here "stage" is proposal material area and evidence checkpoint, not product development phase. When product development involved, development itself follows one-time dev / one-time refactor / one-time launch.

### Overview

| Stage | Name | Core Question | Evidence Hard Gate |
|------|------|---------|---------|
| 0 | Theory Building | What method do we use to analyze? | None |
| 1 | Research Validation | Is this direction worth pursuing? | Do / Pivot / Don't |
| 2 | Plan Design | How specifically do we do it? | Proposal approval |
| 3 | Infrastructure Launch | Can the complete link verify? | End-to-end validated |
| 4 | Operations Growth | Made money yet? | Revenue verified / Replication decision |

## Four. Stage 0: Theory Building

> Stand on giants' shoulders. Find the right method first, then analyze using the method.

Required modules:

| Module | Content | Output |
|------|------|------|
| Book Search and Download | 5–10 core books in domain | Research library topic books directory (cross-brand shared) |
| Online Best Practices Collection | Industry leading blogs, official docs, success cases, method tutorials | Proposal directory `theory/{topic}.md` |
| Method Extraction | Extract applicable methods from books and best practices | Proposal directory `theory/{method_name}.md` |

Optional modules:

| Module | Applicable Scenario |
|------|---------|
| Video & Podcast Learning | Domain has high-quality video tutorials or podcast interviews |
| Paid Courses & Communities | Need to understand competitor paid product forms |

Output directory is `theory/` under proposal directory.

Stage 0 has no evidence hard gate — theory building is basis for subsequent stages; completion moves to stage 1.

## Five. Stage 1: Research Validation

> Use data to answer: is this direction worth pursuing?

Required modules:

| Module | Core Question | Output |
|------|---------|------|
| Market Capacity Analysis | How big is this market? Growing or shrinking? | Market size data (total, serviceable, addressable, or search volume + trend) |
| Needs & Keyword Research | What are target users searching for, asking, lacking? | Need list or keyword data table (volume, competition, clusters) |
| Deep Competitor Analysis | Who's doing it? How well? How do they make money? | Competitor matrix (top N breakdown: scale, content, pricing, channels, weaknesses) |
| Content & Product Gap Analysis | What do competitors cover? What's missing? | Gap opportunity list |
| Track Comparison & Selection | Multiple optional tracks, which has highest ROI? | Track comparison table, data-driven ranking |
| Differentiation Validation | Why do we win? Is differentiation viable? | Unique value props + differentiation matrix, dimension-by-dimension vs. competitors |
| Feasibility Assessment | Resources enough? Time enough? Risks manageable? | Feasibility table, covering resources, cost, time, risk |

Optional modules:

| Module | Applicable Scenario |
|------|---------|
| User Interviews & Surveys | Reachable target user group available |
| Technology Feasibility Validation | New tech stack or unvalidated technology approach |
| Legal & Compliance Research | Cross-border, payment, privacy, copyright risks |

### Evidence Hard Gate 1

| Decision | Condition |
|------|------|
| Do | Market capacity sufficient, differentiation viable, feasibility passes → enter stage 2 |
| Pivot | Data shows need to adjust track, positioning or business model; revise and re-validate |
| Don't | Market too small, competition insurmountable, resources insufficient; pause and document reason, archive |

Evidence hard gate requires clear data support. No "feels good" pass allowed.

## Six. Stage 2: Plan Design

> Design specific approach after research validation.

Required modules:

| Module | Core Question | Output |
|------|---------|------|
| Business Model Design | How do we make money? Pricing? Cost structure? | Business model canvas or revenue model |
| Brand Design | Brand name? Persona? Tone? | Brand positioning + persona doc + visual direction |
| Target Audience Definition | Sell to whom? User persona? | 2–3 core audience personas |
| Content or Product Strategy | What content? In what order? | Content pillars + topic ranking + content calendar |
| Revenue Strategy | Short-term revenue source and long-term growth source? | Dual-engine strategy + revenue timeline estimate |
| Technology & Platform Approach | What platform? How deploy? | Tech selection + architecture + config checklist |
| Tool Planning | Existing tools reusable? Gaps? | Tool mapping table: task → existing tool → gap → new build plan |
| Knowledge Base Filling Checklist | Brand and business directories to create/update? | File checklist + content source + execution phase |
| Timeline & Milestones | How many weeks/months? Weekly deliverables? | Weekly execution plan + weekly deliverables list |
| Risk & Mitigation | What could go wrong? How to respond? | Risk matrix: probability × impact × mitigation |
| Success Metrics | How measure success? | First complete link metrics + long-term validation metrics |

Optional modules:

| Module | Applicable Scenario |
|------|---------|
| Template Replication Framework | This project positioned as replicable template |
| Alliance & Partnership Strategy | Involves external partners or alliance marketing |
| Mid-term Growth Planning | 6–12 month roadmap after first launch cycle |

### Evidence Hard Gate 2

Proposal approval — stakeholder confirms approach is executable, enters execution.

## Seven. Stage 3: Infrastructure Launch

> Build skeleton, make system run.

Required modules:

| Module | Content |
|------|------|
| Infrastructure Setup | Site, payment, domain, CDN, email, and other tech foundation |
| Brand Asset Creation | Avatar, logo, pages, social accounts |
| Tool Configuration | Existing tools + credentials and endpoints, plus new builds |
| Knowledge Base Brand Directory Filling | Identity, style, audience, product, competitor, reference directories |
| End-to-End Validation | Users complete core path: read → subscribe → pay |

### Evidence Hard Gate 3

End-to-end validated — core path fully verifiable, can begin content filling.

## Eight. Stage 4: Operations Growth

> Run it, make money.

Required modules:

| Module | Content |
|------|------|
| Content Production | Produce, translate, publish per content calendar |
| Multi-Channel Promotion | Search, social, community, email, alliance |
| Data Post-mortem | Weekly and monthly reports tracking success metrics |
| Iterative Optimization | Adjust content, pricing, channel strategy per data |

Optional modules:

| Module | Applicable Scenario |
|------|---------|
| Template Sedimentation & Replication Assessment | Batch-build model: can we replicate to next track? |
| Channel Expansion | Add new acquisition channels |
| Community Operations | Build user community |

### Evidence Hard Gate 4

Revenue verification — hit preset revenue target, decide whether to expand or replicate.

## Nine. Plan Document Skeleton

Each proposal follows this structure. Sections adjustable per project, but order fixed.

```markdown
# {project_name} {period} Planning

> Version: vX.Y | Date: YYYYMMDD | Status: Awaiting Approval / Approved / Executing / Completed
> {One-line project summary}

## Zero. Current Progress & Pending Work
{Complete snapshot of completed, in-progress, pending tasks plus dependency diagram}

## One. Strategic Positioning
{Positioning, differentiation, target audience, business model}

## Two. Research Outcomes
{Keyword, competitor, track validation core conclusions — reference research docs, don't repeat}

## Three. Product & Technology Approach
{Platform selection, config approach, membership and pricing system}

## Four. Brand Approach
{Brand positioning, persona, visual, social channels}

## Five. Content Strategy
{Content pillars, topic ranking, production pipeline, resource production standards}

## Six. Execution Plan
{Weekly timeline, weekly tasks, deliverables list, evidence hard gates}

## Seven. Revenue Strategy
{Short-term engine, long-term engine, revenue timeline estimate}

## Eight. Tool Planning
{Existing reuse, new build plan, config changes}

## Nine. Knowledge Base Filling Checklist
{Brand and business directory file list, content source, execution phase}

## Ten. Growth Planning
{Months 2–6 and month 12 growth arrangements}

## Eleven. Risk & Mitigation
{Risk matrix}

## Twelve. Success Metrics
{First complete link, long-term validation}

## Appendix
{Research report index, decision log, change log}
```

Simple projects can merge similar sections, but must not omit "Execution Plan" and "Success Metrics".

## Ten. Proposal Directory Structure

```text
{research_area}/{YYYYMM}/{YYYYMMDD}-plan-{object}-{status}/
├── README.md              ← Continuation entry (required)
├── decision-log.md        ← Key judgments + timestamp (required)
├── {plan_name}-proposal.md ← Main proposal doc, per twelve-section skeleton above
└── theory/                ← Stage 0 output
    ├── books/             ← Downloaded reference books
    └── {topic}.md         ← Best practices & method notes
```

Stage 1 research reports don't go in proposal directory; they stay as single files in same-month directory, proposal main doc only references, doesn't copy.

After proposal runs successfully and business truly starts, output falls under business root per business methodology; proposal directory status changes to `implemented`, stays in research area for traceability.

## Eleven. Sharing Rules

### Tool Planning

- List existing tools first, output "task → existing tool" mapping.
- Only list new builds for gaps existing tools can't cover.
- Don't list unnecessary tools just to make proposal "look complete".
- New tool code lands in unified code repo, not separate KB directory.

### Knowledge Base Sync

- Proposal must include knowledge base filling checklist, stating which directories/files to create/update.
- List per-file, matching existing brand directory structure.
- Each file: note source (new write / rewrite / research output) and execution phase.
- Forbidden to skip KB update after execution — update to where you've progressed.

### Data & Decisions

- Stage 1 each conclusion must cite data source.
- Evidence hard gate must have clear pass/fail criteria.
- Forbidden to skip evidence hard gates, go directly to later stages/execution status.
- Evidence hard gate pass criteria adjustable per project scale, but must declare upfront.

### Timeline

- Execution plan detail to weekly, not month-level vagueness.
- Each week has explicit deliverables list.
- Task dependencies explicitly annotated.
- Optional to draw dependency diagram in text format for critical path.

### Don't Hardcode

- Forbidden to hardcode specific platform names, tool names, prices, domain in methodology.
- Use role names, e.g., "content management system" not a specific product, "keyword tool" not specific service.
- Concrete values fill in proposal instances; methodology only defines what to fill.

## Twelve. Metadata

Proposal metadata inherits common nine fields, plus proposal-specific:

```markdown
| Field | Value |
|------|---|
| Classification | Project Planning |
| Status | Planned / Executing / Completed / Archived |
| Brand | {brand} |
| Industry | {controlled vocabulary value} |
| Owner | {person / team role} |
| Created | YYYYMMDD |
| Planning Period | {N days / N weeks / N months} |
| Current Material Area | Stage 0 / 1 / 2 / 3 / 4 |
| Budget | {amount, or "zero-cost"} |
| Related Decision | → Strategy Decisions/{decision_file}, or "none" |
```

## Thirteen. Checklist

**Stage 0 Theory Building**

- [ ] Retrieved and downloaded domain core books, at least 5
- [ ] Collected online best practices, at least 5
- [ ] Extracted method notes
- [ ] Theory files stored in proposal directory `theory/`

**Stage 1 Research Validation**

- [ ] Market capacity has data support
- [ ] Need & keyword research complete
- [ ] Competitor analysis covers top 10+
- [ ] Content & product gap list output
- [ ] Track comparison quantitatively ranked
- [ ] Differentiation matrix dimension-by-dimension vs. competitors
- [ ] Feasibility assessment covers resources, cost, time, risk four dimensions
- [ ] Evidence hard gate 1 has clear data-supported do / pivot / don't conclusion

**Stage 2 Plan Design**

- [ ] Business model has revenue model and cost structure
- [ ] Brand has positioning and persona doc
- [ ] Target audience has 2+ personas
- [ ] Content strategy has pillars + topic ranking
- [ ] Revenue strategy has short-term engine + long-term engine
- [ ] Technology approach has selection and config checklist
- [ ] Tool planning inventoried existing first, then lists new builds
- [ ] Knowledge base filling checklist aligns with existing brand structure
- [ ] Timeline detailed to weekly, each week has deliverables
- [ ] Risk matrix has probability, impact, mitigation
- [ ] Success metrics have first complete link + long-term validation

**Stage 3 Infrastructure Launch**

- [ ] Infrastructure setup complete
- [ ] Brand assets created
- [ ] Tool configuration and development complete
- [ ] Knowledge base brand directory filled
- [ ] End-to-end validation passed

**Stage 4 Operations Growth**

- [ ] Content produced per calendar
- [ ] Multi-channel promotion executing
- [ ] Data post-mortem conducted regularly
- [ ] Success metrics tracked

**Proposal Document Self-Check**

- [ ] Version and status correctly marked
- [ ] Current progress section reflects real status
- [ ] All decisions have data support citations
- [ ] Tool planning has no redundant new builds
- [ ] Knowledge base checklist aligns with brand directory structure
- [ ] Timeline dependencies explicitly marked
- [ ] Methodology template contains no hardcoded values (proposal instances can)
- [ ] Proposal directory in research area, directory name has status word, `README.md` and `decision-log.md` complete

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Migrated from project planning specification and generalized |
