---
document_id: awp-knowledge-management-standard/methodology/brand/kb-method-brand-audience
language: en
publication: public
title: "Audience Persona Methodology"
---

# Audience Persona Methodology

> Managing how to write audience persona files: identifying target groups, their needs, and conversion paths.
> Applicable to any industry, any brand. Identity layering and loading priority see `kb-method-brand-identity.md`.

---

## Positioning

An audience persona answers "who I write to, who I sell to." Each persona is one independent Markdown file. Before writing content, the Agent reads the matching persona and matches language depth, pain points, and conversion strategy accordingly.

This methodology manages two things:

1. The section skeleton and writing requirements of each persona file
2. The differentiation boundary between personas

Canonical copy lives in `{brand_root}/{brand}/operations/audiences/`.

---

## Design Philosophy

- **One persona, one file**: Each group gets an independent file, no mixing—the Agent loads a single persona per scenario.
- **Decidable difference**: Every two personas must have a clear distinction criterion, no blurry overlap.
- **User's viewpoint**: A persona describes "what kind of people they are," not "what I want them to become."
- **Action-oriented**: A persona is not a demographics table; it's a decision tool guiding content strategy and conversion paths.

---

## Persona File Skeleton

✅ Each persona file organizes in this order:

```
① Metadata → ② Who They Are → ③ Trigger Scenarios → ④ Core Needs → ⑤ Information Behavior → ⑥ Common Questions → ⑦ Conversion Barriers → ⑧ Who It Doesn't Fit → ⑨ Change Log
```

| # | Section | Required | Question it answers |
|---|---------|:----:|-----------|
| ① | Metadata | ✅ | File management info |
| ② | Who They Are | ✅ | Basic traits of this group? |
| ③ | Trigger Scenarios | ✅ | When do they come to me? |
| ④ | Core Needs | ✅ | What do they really want? |
| ⑤ | Information Behavior | ✅ | How do they get information and make decisions? |
| ⑥ | Common Questions | ✅ | What do they ask? What's the standard answer? |
| ⑦ | Conversion Barriers | ✅ | What stops them from acting? What alternatives exist? |
| ⑧ | Who It Doesn't Fit | ✅ | Who is the opposite of this persona? |
| ⑨ | Change Log | ✅ | Date plus change content, no version numbers |

---

## Section by Section

### ① Metadata

✅ Fields and order fixed:

```markdown
## Metadata

| Field | Value |
|------|---|
| Persona | {persona name, same as file name} |
| Status | Active / Draft / Deprecated |
| Created | YYYYMMDD |
| Updated | YYYYMMDD |
```

### ② Who They Are

✅ Use a list to describe basic traits across 3–5 dimensions.

Required dimensions:

| Dimension | Description |
|------|------|
| Identity or occupation | The role they identify with |
| Spending power or budget | Willingness and range to pay |
| Personality keywords | 3–5 traits relevant to decision-making |

⚪ Optional dimensions, pick by industry:

| Dimension | When it fits |
|------|---------|
| Age range | Consumer products, education |
| Region | Services with regional differences |
| Technical level | Tech products, education |
| Company size | B2B products and services |
| Industry | Vertical-industry services |

❌ No piling up demographic stats—keep only dimensions that affect content strategy and conversion decisions.

| Good | Bad | Why |
|----|-----|------|
| "Identity: working professional wanting to transition" | "Gender ratio 6:4" | The former affects content strategy |
| "Spending power: has team training budget" | "Household income 200K–500K" | The former relates directly to purchase decisions |

### ③ Trigger Scenarios

✅ Numbered list, 2–5 scenarios.
✅ One sentence per scenario describing "what event or state makes them start looking for a solution."
✅ Scenarios must be concrete and imaginable, not abstract.

| Good | Bad | Why |
|----|-----|------|
| "Saw a peer get results, anxiety kicked in" | "Interested in this field" | The former has a scene |
| "Boss asked: competitors already use it, what about us" | "The company has transformation needs" | The former is a concrete trigger event |

### ④ Core Needs

✅ Organized in three layers:

| Layer | Question it answers | Example |
|------|-----------|------|
| Functional need | What task do they need to complete? | "Learn to automate daily work" |
| Emotional need | What do they want to feel after completing it? | "Feel they're keeping up with the times" |
| Social need | What do they want to look like in others' eyes? | "Appear technically capable among peers" |

✅ All three layers required. Functional need drives product design, emotional need drives content tone, social need drives distribution strategy.

### ⑤ Information Behavior

✅ Three sub-dimensions:

| Sub-dimension | Content |
|--------|------|
| Information channels | Where they get information; list main channels |
| Trust factors | What makes them trust you; list 2–4 trust triggers |
| Decision process | Typical path from knowing to paying |

✅ Decision process uses `→` arrow chains to show conversion steps clearly.

### ⑥ Common Questions

✅ Two-column table: question / standard answer.
✅ 3–8 high-frequency questions.
✅ Standard answers are reference scripts for the Agent when facing users of this persona.

❌ No generic Q&A—every question must be a doubt specific to this persona.

| Good | Bad | Why |
|----|-----|------|
| "Can I learn it without programming?" (unique to zero-beginners) | "Is your product good?" (everyone asks) | The former is persona-specific |

### ⑦ Conversion Barriers

✅ Two parts:

- **Hesitation points** (numbered list, 2–4 items): what psychological factors stop them from acting.
- **Alternatives** (numbered list, 2–3 items): if they don't choose you, what do they choose.

✅ Alternatives must be real—the Agent needs to know who the competitors are to respond implicitly in content.

### ⑧ Who It Doesn't Fit

✅ Numbered list, 2–4 items.
✅ Describe the opposite of this persona—who looks like this persona but actually isn't a fit.

The value of this section:

- The Agent can filter implicitly in content, e.g., "if you want a quick win, this isn't for you"
- Avoid attracting wrong users, which causes bad reviews or refunds

---

## Shared Rules

### Persona Count

- ✅ 3–8 personas cover the main groups
- ❌ No more than 8—too many personas mean over-segmentation; the Agent can't match effectively
- ❌ No fewer than 2—one persona equals no persona

**Exception: single-audience brand.** When brand positioning itself converges paying groups into one class, ✅ exactly 1 persona is allowed, plus some distribution-surface or non-audience notes (these don't count toward the persona count). The count lower bound doesn't apply then, but the audience directory's index file must state two things:

1. **Why only one class**—which positioning criterion converged the groups into one, pointing to the positioning canonical file
2. **Who looks like it but isn't**—why each distribution surface and adjacent group doesn't enter the persona

❌ Don't split a second persona just to reach 2. If positioning says serve one class but the audience directory lists two, you're denying your own positioning with the file structure.

### Persona Differentiation

- ✅ Every two personas must have at least one decidable distinction criterion
- ⚪ Recommended: a difference matrix summarizing all personas, placed in the audience directory's index file

### File Naming

- ✅ Four-segment: `{type}-audience-{persona-name}-{scope}.md`—type is `persona` or `decision`, scope defaults to `general`
- ✅ Persona name uses labels users understand, not internal codes; analysis groupings (AI value approach · revenue model · purchase intent) are registered in the directory index, not in the filename
- ❌ No numbered names, e.g., `persona-01.md`; no brand name as the last segment (the path already encodes the brand)

### Index File

The audience directory's index file ✅ must contain a quick-reference table of all personas:

```markdown
| File | Group | Core traits |
|------|------|---------|
| {persona-name}.md | {one-line group description} | {most critical trait} |
```

### Relationship with Other Brand Dimensions

| Related dimension | Relationship |
|---------|------|
| Positioning file's "who I serve" | Positioning summarizes in one line; audience personas expand |
| Expression style file | Different personas may need different language depth |
| Business model | Different personas map to different products or pricing tiers |

After modifying an audience persona, check whether the related dimensions above need syncing.

---

## Checklist

**New persona file**:
- [ ] All 9 sections present (Metadata → Who They Are → Trigger Scenarios → Core Needs → Information Behavior → Common Questions → Conversion Barriers → Who It Doesn't Fit → Change Log)
- [ ] Metadata fields complete
- [ ] "Who They Are" has the three required dimensions: identity, spending power, personality keywords
- [ ] 2–5 trigger scenarios, each concrete and imaginable
- [ ] Core needs all three layers filled (functional / emotional / social)
- [ ] Information behavior all three dimensions filled (channels / trust / decision process)
- [ ] Common questions are persona-specific, not generic Q&A
- [ ] Conversion barriers have hesitation points plus alternatives
- [ ] "Who It Doesn't Fit" has 2–4 items

**Persona system check**:
- [ ] Total personas 3–8; single-audience brand has 1, and the index states why only one class and who looks like it but isn't
- [ ] Every two personas have decidable differences
- [ ] Index quick-reference table updated
- [ ] No persona contradicts the positioning file's "who I serve"

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-15 | Naming to four-seg · groupings to index |
| 2026-08-07 | Extracted generic methodology from brand spec |
