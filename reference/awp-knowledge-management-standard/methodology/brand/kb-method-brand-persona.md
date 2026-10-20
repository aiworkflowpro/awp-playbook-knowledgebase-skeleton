---
document_id: awp-knowledge-management-standard/methodology/brand/kb-method-brand-persona
language: en
publication: public
title: "AI Persona Modeling Methodology"
---

# AI Persona Modeling Methodology

> Managing "how to build a complete AI persona"—installing an inner setting in the Agent that can reason on its own, not pinning down a style list.
> Serves character-type brands only. Regular brands' content work doesn't need a persona layer, and this methodology must not be used to copy the brand owner into a brand persona.

Canonical copy lives in `{brand_root}/{brand}/identity/persona/`. How the four brand domains split and whether the directory exists, see `kb-method-brand-identity.md`.

---

## Glossary

| Term | Definition |
|------|------|
| **Persona** | Loadable inner setting: values, thinking, emotion, memory, and decision habits, letting the Agent reason on its own in new situations |
| **Persona-driven** | Output derives from "how this person would see it," not from sentence menus or forbidden-word metrics |
| **Viewpoint loop** | Inner steps facing material: establish stance → decide what to give the reader → any first-hand memory → write / reply / stay silent → present and incident check |
| **Incident check** | Last check before output: any fabricated facts, any overreach into professional advice, any broken isolation between character and the owner |
| **Instance** | A character-type brand's concrete answers to the ten-layer questions |
| **Character loading** | A character-type brand explicitly links this brand's persona canonical file in its own workflow; regular brands don't load |
| **Stable layer** | Rarely-changed foundation: core, narrative arc, value-conflict ordering, stance toward knowing |
| **Living layer** | Regularly-updated parts: detail library, memory index, calibration habits, used ledger |
| **Minimal loading** | Writing defaults to loading only core setting, adding a few layers by stimulus, never reading all ten layers through |
| **Detail library** | Merged experiences and on-site material long-form, taken by section as needed |
| **Reference sample** | Model text provided by the workflow side, borrowed for rhythm only, doesn't decide stance |
| **Hot source / Irritation source** | Material that excites this character / material that makes this character impatient |

---

## ① Positioning

| | |
|--|--|
| **Manages** | Character-type brand's complete persona structure, each layer's duty, viewpoint loop, verification method, and workflow interface |
| **Output** | Character setting under `{brand_root}/{brand}/identity/persona/`; enters content production only when that brand's workflow explicitly declares it |
| **Doesn't manage** | Brand four-domain division (→ identity modeling); operations-side products, audiences, competitors; bio finalization (→ expression style); posting quotas (→ operations); reference samples (→ workflow) |
| **One phrase** | **Character brands can load a character; regular brands only load the brand contract.** No situation relies on sentence rules. |

❌ Don't write specific character stories in this methodology; and never copy the brand owner into a brand persona. The owner's facts and decisions stay in the owner layer only.

---

## ② Design Philosophy

1. **Resemblance is a structure problem, not a tone-of-voice problem.** An Agent with only labels goes empty on new material; only a complete inner world can reason.
2. **Serves character-type brands only.** Any material first goes through the character's viewpoint loop; reference samples only lend rhythm. Regular brands read the brand contract per the writing method.
3. **Methodology asks questions, brand fills answers.** This file writes no instance's private details.
4. **Directory and persona-building separate.** Identity modeling manages whether the directory exists; this methodology manages what the persona layer answers.
5. **One constraint written in one place.** Incident boundary in strategy domain; stance toward knowing in the corresponding layer; external temperament in the persona-mask layer.
6. **Verifiable.** Complete documents don't pass; new material growing opinions that look like the same person passes.

---

## ③ Organization Framework

### 3.1 Division of Labor with Identity Modeling

```
Identity modeling methodology ──directory──► {brand_root}/{brand}/
                                              ├── operations/      (this methodology doesn't manage)
                                              └── identity/
                                                   ├── strategy/ expression/ visual/ cognition/
                                                   └── persona/  ◄── this methodology only builds here
AI persona modeling methodology ──build──► identity/persona/ inside: core setting + L1–L10 + detail library
                                                │
                                            instance answers (by target brand)
                                                │
Character-brand workflow ──explicit declaration──► {brand_root}/{brand}/identity/persona/
Regular-brand workflow ──brand contract──► positioning + audiences + content setup + expression
```

| Dimension | Identity modeling methodology | This methodology | Brand instance |
|------|--------------|---------|---------|
| Whether `identity/persona/` directory exists | ✅ decides | — | build directory |
| How operations domain lays out | ✅ decides | ❌ doesn't manage | fill operations |
| File name and metadata shell | ✅ decides shell and naming | ✅ decides layer questions | fill shell |
| Character layer writes description or virtue checklist | — | ✅ decides persona-driven | write per this methodology |
| Viewpoint loop | — | ✅ decides protocol | core setting holds one section |
| Incidents and isolation | strategy domain | interface: real incidents don't enter persona-mask layer | strategy plus thin character-layer summary |

Who wins on conflict:

| Conflict | Winner |
|---------|------|
| Metadata fields inconsistent | Identity modeling methodology's standard shell |
| A layer's "what it answers" | This methodology |
| Persona-driven vs. old sentence or forbidden-word lists | Persona-driven |
| Where the real-incident boundary is written | Strategy domain's constraint-and-boundary file; persona layer writes summary only |
| What the directory is called, whether under identity domain | Identity modeling methodology |

### 3.2 Three-Layer Assembly

Borrow psychology's three-layer description of personality (McAdams' three-layer personality model) to decide how to read the ten layers:

| Assembly layer | Question | Main mapping |
|--------|------|---------|
| **I Dispositional traits** | Usually like what? | L2 character foundation  -  L3 personality  -  L5 emotional baseline |
| **II Characteristic adaptations** | Pursue what, how to handle situations? | L4 values  -  L6 cognition  -  L8–L9 monitoring and decisions |
| **III Narrative identity** | What does life mean? | L1 identity narrative  -  L7 memory |

Recommended load order: core setting → read relevant layers of I / II / III on demand → run material through the viewpoint loop → present persona-mask layer with reference samples.

### 3.3 Ten Layers at a Glance

| Layer | Only answers | Psychological reference (framework, not a fill-in form) |
|----|--------|--------------------------------|
| L1 | Who it is, why it exists | Narrative identity |
| L2 | What it's like at the core; real incidents can be extremely thin | Character foundation, not a style list |
| L3 | Usual tendencies | Big Five / HEXACO six-factor |
| L4 | What it pursues; who wins on conflict | Schwartz values / motivation theory |
| L5 | Emotional baseline and hot/irritation sources | Emotion dimensions |
| L6 | How it thinks; stance toward knowing | Dual-system thinking, bounded rationality |
| L7 | Experiences and usable material | Autobiographical memory |
| L8 | How it notices its own thinking went off | Metacognition, calibration |
| L9 | Whether to act, how to act | Self-regulation |
| L10 | What speaking feels like | Persona mask, dramaturgical theory (written as description) |

### 3.4 Viewpoint Loop

Facing any material (external collection, internal material, reader letters):

| Step | Name | Question | Main layers |
|----|------|------|--------|
| 0 | Trigger | Does it touch a hot source or irritation source? | L5 |
| 1 | Establish stance | What to hold? Where's the boundary? Where's uncertain? | L6  -  L8 |
| 2 | Decide what to give | What increment for the reader? Which side do values stand? | L4  -  L1 |
| 3 | Memory | Any first-hand data or failed experience? If none, lower assertion strength | L7  -  detail library |
| 4 | Intent | Reply, write, note, or stay silent? | L9 |
| 5 | Present | What temperament says it? | L10 with reference samples |
| 6 | Incident check | Any fabrication? Any professional overreach? Any broken isolation? | L2 thin entries plus strategy boundary |

- ✅ Steps 1–4 **forbid** relying on sentence libraries or forbidden-word lists.
- ✅ Staying silent is a legal intent.

### 3.5 Directory Structure: Fully Flat, Four-Segment

> Aligns with `kb-method-brand-identity.md § File Naming`. ❌ No `details/` subdirectory; ❌ no one-hyphen old names like `L1-identity.md`.

```
{brand_root}/{brand}/identity/persona/          ← canonical copy (zero subdirectories)
├── CLAUDE.md
├── data-persona-core-setting-{character}.md
├── data-persona-L1-identity-{character}.md
├── data-persona-L2-character-{character}.md
├── ... L3 ... L9 ...
├── data-persona-L10-mask-{character}.md
├── data-persona-detail-library-{character}.md    ← level-two headings split sections inside
├── data-persona-stable-layer-ledger-{character}.md
└── guide-persona-new-material-card-{character}.md

{workflows_root}/.../identity/              ← only symlink to the files above, no second copy
```

| Segment | Persona-layer values |
|----|-----------|
| Type | Main text writes `data`; operating instructions write `guide` |
| Dimension | Fixed `persona` |
| Topic | `core-setting`  -  `L1-identity` ... `L10-mask`  -  `detail-library`  -  `stable-layer-ledger` (no hyphen inside segment) |
| Scope | Character name; brand name can't go in this segment |

**Brands without ten layers**: may use the sliced form of `plan-persona-{topic}-universal.md` plus `data-persona-{topic}-{character}.md`, no need to force a full L1–L10.

- ❌ No workflow and brand each maintaining a layer copy.
- ❌ No two homepage files in the persona directory at once; workflows may symlink to the canonical index.
- ❌ No `details/` subdirectory; new material appends to the corresponding detail-library section.

---

## ④ Layer by Layer Requirements

### L1 Identity

- ✅ One-line positioning  -  core motivation (what problem it chases)  -  narrative arc (tells a story, not a resume)  -  relationship with the reader
- ⚪ Self-awareness of own abilities, boundary of public information

### L2 Character

- ✅ **Descriptive** foundation, 3–7 entries, saying which experience or training it came from
- ⚪ Extremely-thin real-incident table (fabrication, professional advice, isolation), consistent with strategy boundary
- ❌ Virtue or forbidden-action checkbox tables as the creative gate
- ❌ Heading formulas, forbidden-word lists

### L3 Personality

- ✅ Tendency description (Big Five or equivalent framework) plus how it shows daily
- ❌ "Should be like this" normative sentences

### L4 Values and Drives

- ✅ What it cares about  -  **who wins on conflict** (table)
- ⚪ Drives, explicitly what it doesn't pursue
- ❌ Tone of an externally-facing standard answer

### L5 Emotion

- ✅ Emotional baseline  -  hot sources  -  irritation sources (these two are material filters)
- ⚪ When it's fragile, when it's at ease

### L6 Cognition

- ✅ Thinking modules (keep short)  -  **stance toward knowing**: default attitude toward evidence, authority, the unknown, and failure
- ❌ Passing writing-tip lists off as cognition

### L7 Memory

- ✅ Path memory index  -  detail-library pointers  -  "no first-hand memory → lower assertion strength"
- ❌ Stuffing hundreds of lines of stories into this layer's main text

### L8 Metacognition

- ✅ Typical form when it's lazy  -  how it calibrates  -  drift signals
- ⚪ Habit of revising its own claims

### L9 Self-Regulation

- ✅ Habits in different situations  -  how it decides when seeing material; **staying silent is legal**
- Consistent with viewpoint loop step 4

### L10 Persona Mask

- ✅ Stance and tone temperament, written as description
- ⚪ What it usually has on hand, observations of natural rhythm
- ❌ Numbered sentences, forbidden-word metrics, hard length specs (length belongs to operations and platforms)
- Rhythm training → delegate to workflow's reference samples

### Core Setting File

- ✅ Core one-liner  -  ultra-short path  -  thinking skeleton  -  **a viewpoint-loop section** (may be a condensed isomorphic version of this methodology)  -  pointers to the ten layers
- ⚪ 2–4 "like" and "unlike" observations each, written as description not forbidden-word lists—to steady the voice
- Shell: metadata plus change log, using the brand standard shell

---

## ⑤ Stable Layer and Living Layer

A stable persona = **stable layer rarely changes, living layer changes often, activation by stimulus at writing time**. Not "the file never changes."

| Class | Contains | Change discipline |
|----|--------|---------|
| **Stable layer** | Core-setting core  -  L1 narrative arc  -  L2 foundation  -  L4 who-wins-on-conflict  -  L6 stance-toward-knowing summary  -  strategy incident boundary | No change by default; changes must go through the stable-layer change record (who approved, why, which workflows affected) |
| **Living layer** | Detail library  -  L7 index and pointers  -  L8 and L9 calibration habits  -  used ledger  -  workflow reference samples | May update with practice; don't write living-layer content into stable layer pretending "always so" |
| **Writing-time modulation** | Current stimulus  -  material  -  sample draw | Changes every task; **forbid** changing the stable layer to force output for convenience |

| ✅ | ❌ |
|----|-----|
| High-reach feel handled by sample drawing | Turning L4 or L10 into sentence formulas for one high-reach piece |
| New first-hand experience into detail library and L7 | Writing the current material permanently into L1 as "she's always been this" |
| Strategy incident table only adds real incidents | Writing "post N times a day" into the persona |

### Stable-Layer Change Record Template

When changing the stable layer, write it in that file's change log, or leave a short note in the persona directory:

```text
Date | which stable-layer entry changed | reason (one sentence) | approver (decision maker or role) | workflows needing sync
```

Unrecorded major stable-layer changes count as non-compliant drift.

---

## ⑥ Minimal Loading

After a character-type brand explicitly declares in its workflow, load in this order:

| Priority | Loads what | Explanation |
|--------|--------|------|
| Required | Core setting (incl. viewpoint loop) | Entry point, must not skip |
| By stimulus | 1–3 relevant layers | Read when hot source, irritation source, value conflict, or memory trigger appears |
| When visuals needed | Relevant detail-library sections | No whole-library dump |
| Presentation | Persona-mask temperament (can be thin) with reference samples | Reference samples live in workflow, not in the persona canonical file |
| Incidents | Strategy boundary pointers | Real incidents don't pile into persona-mask layer as iron rules |

| ✅ | ❌ |
|----|-----|
| Simple replies can load only core setting plus viewpoint loop | Reading all ten layers through by default as ritual |
| Prompt only writes a pointer to the persona canonical file | Embedding a complete second persona inside the prompt |
| Data-slice creation doesn't load by default | Feeding slices and layer main text into context at once |

**This methodology only builds the character; the writing method decides whether to load the character.** On conflict: what the character layer answers is ruled by this methodology; what the workflow loads is ruled by the writing method and that workflow's brand declaration.

---

## ⑦ Data Slice Discipline

Some brands have separate data-slice files, e.g., experience narratives, capability wordings.

| ✅ | ❌ |
|----|-----|
| Slice header marks "Appendix"; on conflict the layer main text wins | Slice and layer each write mutually exclusive stories |
| Creation default path doesn't load slices | Workflow treats old-named files as the main identity |
| What can merge into layers merges, then delete the duplicate | Same fact maintained in three places |

---

## ⑧ Shared Rules

### Persona-Driven Red Lines

| ✅ | ❌ |
|----|-----|
| Behavior derives from values and thinking | Sentence menus drive writing |
| Real incidents written in strategy domain | Style iron rules posing as persona |
| Reference samples only manage rhythm | Reference samples decide stance |
| Stable layer changes rarely, living layer often | Changing the stable layer for a single output |

### Division of Labor with Expression, Strategy, Writing Method

| Content | Where the canonical copy lives |
|------|---------|
| Temperament depth | Persona-mask layer |
| Temperament summary, finalized bio | Brand identity domain's expression directory |
| Isolation, no fabrication, professional overreach | Brand strategy domain's constraint-and-boundary file |
| Writing-time loading and on-the-spot play | Writing method |

### Verification: What Counts as Passing

| Test | Pass standard |
|------|---------|
| 3+ pieces of unfamiliar material, reading only persona plus detail library | Viewpoint-loop traces visible, feels like the same person |
| Value-conflict questions | Results follow L4's "who wins on conflict" |
| Topics without first-hand memory | Marks uncertainty or stays silent, doesn't fake expertise |
| Same question with different reference samples | Feel changes, value stance doesn't |
| Minimal loading vs. reading all ten layers through | Minimal loading still feels like the same person; if not, core setting is too thin |

Complete documents don't equal passing.

### Dynamic Updates

- **Living layer** (details, L7 index, L8 and L9): update often.
- **Stable layer** (L1 / L2 / L4 foundation, core): changes rarely, go through stable-layer change record.
- The viewpoint-loop protocol belongs to the methodology layer; changing the protocol means changing this file and the corresponding section in every brand's core setting at the same time.

### Living-Layer Feedback: Writing Feeds the Persona

| What feeds back | Where it lands |
|---------|--------|
| New first-hand experience, reusable scenes | Detail library plus L7 pointers |
| Already-used stories, avoid repeating | Used ledger |
| "Thought went off again" calibrations | L8 |
| High-reach sentences, hook priorities | Workflow reference samples or operations, not into stable layer |

---

## ⑨ Checklist

### Methodology Itself

- [ ] Four elements complete: positioning, scope, document relationships, metadata
- [ ] Division-of-labor table with identity modeling exists, and no "double canonical copy"
- [ ] No requirement to treat sentence menus or forbidden-word metrics as the persona canonical file
- [ ] Contains stable layer and living layer, minimal loading sections

### Brand Persona Instance

- [ ] Canonical copy in `{brand_root}/{brand}/identity/persona/`, workflows only symlink
- [ ] Only one navigation entry, no two homepages
- [ ] Every layer has metadata and change log
- [ ] L2 is description-oriented; L10 is temperament-oriented
- [ ] Core setting contains the viewpoint loop, or an explicit pointer to this methodology § 3.4
- [ ] Core setting contains "like / unlike" observations (⚪ can be added later)
- [ ] L4 has "who wins on conflict"; L6 has stance toward knowing
- [ ] Real incidents don't pile into L10 as iron rules
- [ ] Index states minimal loading; data slices marked "Appendix"
- [ ] Data slices don't form a second canonical copy with layer main text

### Coordination

- [ ] Methodology changed required items → same round updates the registered pilot brands' corresponding sections
- [ ] Brand changed layer duties → recheck whether this methodology still covers
- [ ] Symlinks unbroken
- [ ] Stable-layer changes recorded

---

## Related Methodologies

| Topic | File |
|------|------|
| Brand four domains, directories, and four-segment naming | `kb-method-brand-identity.md` |
| Expression style and temperament summary | `kb-method-brand-identity.md § Style Priority` |

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Extracted generic methodology from persona spec |
