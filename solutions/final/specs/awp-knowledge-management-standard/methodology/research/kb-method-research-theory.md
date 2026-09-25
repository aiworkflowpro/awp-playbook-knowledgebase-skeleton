---
document_id: awp-knowledge-management-standard/methodology/research/kb-method-research-theory
language: en
publication: public
title: "Theory Guides Practice Methodology"
---

# Theory Guides Practice Methodology

> Manages one thing: the full chain from thinking clearly to producing—theory → methodology → workflow → output.
> Covers the four-layer chain model, the four theory pillars, methodology build standards, and the four-step diagnosis and tracing method.
> Does not cover how to write a specific article, which tools to use, what an output looks like, or which directory an output goes to.

## 1. The Four-Layer Chain

### Core Claim

**Theory guides practice. Practice tests theory.**

- Every output is supported by a workflow
- Every workflow is guided by a methodology
- Every methodology is supported by classic theory
- When practice shows a theory is wrong, fix the theory—do not discard it

If any layer is missing, you have not thought it through.

### Scope: Every Task

This methodology is not limited to one field or to the inside of the knowledge base. Front-end design, product development, content creation, and investment decisions—any task that requires "making something" follows this chain. The methodology follows the task, and the output lands where the task needs it: a code repository, a directory in the knowledge base, or an external platform. The task context decides. This methodology does not fix the path in advance.

### Why the Four Layers Are Needed

A common failure mode: you start doing directly, the result is wrong, and when you look back you find you never even thought the problem through.

Another common failure mode: you think about a lot of theory and read a lot of books, but nothing lands—because the two bridge layers in the middle, methodology and workflow, are missing.

| Layer | Problem it solves | What happens without it |
|----|------------|--------------|
| Theory | Why do it this way | You do it without knowing why, and you cannot handle a new scenario |
| Methodology | What approach to follow | You start from zero every time, and experience cannot be reused |
| Workflow | What exactly to do in each step | The approach stays in one person's head, and no one else can run it |
| Output | What the result looks like | You finish but cannot tell whether it is done well |

### Four Design Principles

1. **Each layer does one thing only.** The theory layer handles only "why," the methodology layer handles only "what approach," the workflow layer handles only "what each step does," and the output layer handles only "what the result looks like." No layer oversteps, and no layers mix.
2. **Upper layers guide lower layers; lower layers never depend backward on upper layers.** A workflow can ignore the details of the theory layer as long as the methodology tells it what to do. But a methodology must know its own theory basis.
3. **The chain must be traceable.** Any output can be traced back along the chain to its workflow, methodology, and theory basis. If you cannot trace it, the chain is broken.
4. **Follow the task, not a fixed directory.** The four-layer chain is a thinking framework, not a file system. Which directory holds the methodology and where the output lands are decided by the task context.

### Converting Between Layers

```text
Theory ──[distill]──→ Methodology ──[operationalize]──→ Workflow ──[execute]──→ Output
  ↑                                                                              │
  └──────────────────────[feedback correction]────────────────────────────────────┘
```

#### Theory → Methodology (Distill)

| Requirement | Explanation |
|---------|------|
| Theory mapping | A new methodology must fill in the "classic theory reference" table, listing the theories it rests on and exactly which principle of each |
| Field scope | State clearly which field and scenario this methodology applies to |
| Negative example | List at least one real case showing what goes wrong without this methodology |

#### Methodology → Workflow (Operationalize)

| Requirement | Explanation |
|---------|------|
| Step breakdown | Every part of the methodology has a matching workflow step |
| Tool binding | Every step must name the tool it uses |
| Gate design | Key points have stage gates |

#### Workflow → Output (Execute)

| Requirement | Explanation |
|---------|------|
| Acceptance criteria | The workflow defines the output's acceptance conditions at its end |
| Quality gate | The output passes a checklist before release |
| File location | Output files go to an agreed location |

#### Output → Theory (Feedback Correction)

| Requirement | Explanation |
|---------|------|
| Practice verification | The output, used in real work, verifies whether the theory holds |
| Correction from failure | When output quality fails, trace back along the chain and fix the problem at the layer where it sits |
| Extracting new theory | When repeated practice reveals a new pattern, distill it into a new thinking model or principle |

### Core Rules for Each Layer

**Theory layer**: verified understanding and principles that apply across scenarios. Not one person's inspiration, but patterns tested by extensive practice.

| Admission condition | Explanation |
|---------|------|
| Has a classic source | Traces to a recognized academic work, or to a practice system verified widely |
| Applies across scenarios | Works in more than one scenario; verified in at least three different scenarios |
| Can be falsified | You can state clearly when this theory does not hold |
| No unverified ideas | Ideas go to the failure-mode library or the to-verify list first; promote them to theory only after verification |

**Methodology layer**: it turns theory into a structured approach that works in a specific field.

| Rule | Explanation |
|------|------|
| Must state its theory basis | Write which classic theories it rests on; cite, do not copy |
| Must have an operational path | Cannot stop at "in principle it should be this way"; must state exactly how to do it |
| Must bind an execution method | When it lands, bind it to a workflow or to clear manual steps |
| An approach without theory support is not a methodology | That is called experience |

A methodology has a lifecycle:

| Stage | Meaning | Requirement |
|------|------|------|
| Draft | First attempt, not yet fully verified | Theory basis + operating steps + labeled as draft |
| Official | At least one complete practice with passing output | Meets all admission conditions below |

Use it once before setting rules—do not wait until the methodology is perfect before you start.

**Workflow layer**: an executable implementation of a methodology.

| Methodology | Workflow |
|--------|-------|
| Says "what should be done" | Says "how to do it, what each step does" |
| A person can read it and understand the approach | An Agent can read it and run it directly |
| One methodology may match several workflow variants | One workflow implements one methodology only |
| Changes rarely (the approach is stable) | Changes often (tools and steps iterate) |

The workflow's entry file must state which methodology it implements. Every step has a clear input, action, and output. The end of the workflow must define the output's acceptance criteria.

**Output layer**: the end of the whole chain and the only standard for testing whether the chain is correct. Every output must be acceptable, traceable, and stored in a known place.

### Three Questions Before Creating Anything

Whether you create a methodology, a workflow, a standard, a product, or a page, answer these first:

1. **What is the theory basis?** Which verified principles exist in this field? If you cannot find one, search the field's classic books and top practitioners first.
2. **Where is the methodology?** Is there a structured approach? If not, pick the closest of the methodology prototypes and build a draft.
3. **What does the output look like?** Can you state, before you start, what will be in your hands when you finish?

If you cannot answer even one of the three questions, stop and fill the gap first. Do not start working directly.

---

## 2. The Four Theory Pillars

The theory layer is not a pile of loose knowledge points. It is organized around four pillars, one for each of four fundamental questions. Any new theory asset entering the knowledge base must fit into one of these four pillars. If it does not fit, either it does not belong to the theory layer (demote it to experience or inspiration), or the four pillars need extending.

### Why Four Pillars

Everything you do rests on four questions:

1. What is the problem I face? (**Problems**)
2. How do I make sure I think correctly? (**Cognition**)
3. What system does this problem sit in? (**Systems**)
4. How do I move from thinking to doing? (**Practice**)

These four questions map to four basic fields of philosophy: ontology, epistemology, systems theory, and practice theory.

- Three is not enough: without systems theory, you cannot see feedback loops or emergence, and you end up treating the part that hurts.
- Five is too many: further division enters specific fields (decision theory, game theory), which belongs to the methodology layer.
- Four covers the full loop: "understand the problem → think correctly → see the whole → take action."

### First Pillar: Problems (Ontology)

**Core question**: when you face a task, how do you understand and break it down?

| Classic source | Core contribution | In one sentence |
|---------|---------|-----------|
| Polya, *How to Solve It* (1945) | Four steps: understand → plan → carry out → review | The origin of all problem-solving frameworks |
| Altshuller, TRIZ (1946-1985) | Contradiction analysis, inventive principles | Contradictions exist to be resolved, not compromised |
| Newell and Simon, *Human Problem Solving* (1972) | Problem space theory, means-end analysis | Solving a problem is searching in the problem space |

**Core principles**:

1. **Problems have structure**—a well-defined problem (clear conditions and a clear goal) and a fuzzy problem (even the problem itself needs defining first) need completely different handling.
2. **Decomposition is the most basic strategy**—break a big problem into small ones and solve each small problem on its own.
3. **A contradiction is not a dead end**—when you need both A and B, do not pick one of the two; find a solution at a higher level that makes the contradiction disappear.

### Second Pillar: Cognition (Epistemology)

**Core question**: what errors does human thinking make by nature, and how do you calibrate them?

| Classic source | Core contribution | In one sentence |
|---------|---------|-----------|
| Kahneman, *Thinking, Fast and Slow* (2011) | Dual-system theory, list of cognitive biases | People have two thinking systems; the fast one often errs |
| Taleb, the uncertainty series (2001-2018) | Black Swan, antifragility, asymmetric risk | The world is uncertain; surviving matters more than predicting accurately |
| Duke, *Thinking in Bets* (2018) | Probabilistic thinking, separating decisions from outcomes | A good decision is not the same as a good outcome |
| Galef, *The Scout Mindset* (2021) | The difference between the scout and soldier mindsets | The goal is to see the facts, not to win an argument |

**Core principles**:

1. **Human judgment is biased by nature**—confirmation bias, anchoring, availability bias, and hindsight bias. Knowing you make these errors is the first step to correcting them.
2. **Think in probabilities, not certainties**—most things are not "will happen" or "will not happen" but "how likely."
3. **Keep calibrating your beliefs**—when new evidence appears, update your probability. Do not look only at evidence that supports A because you think A is right.
4. **Judge decision quality and outcome quality separately**—a good decision can bring a bad outcome (bad luck), and a bad decision can bring a good outcome. Judge a decision by the quality of its process, not its outcome.

### Third Pillar: Systems (Systems Theory)

**Core question**: how do things interact? What chain reactions follow when you change one place?

| Classic source | Core contribution | In one sentence |
|---------|---------|-----------|
| Meadows, *Thinking in Systems* (2008) | Feedback loops, stocks and flows, leverage points | System behavior comes from structure, not intention |
| Senge, *The Fifth Discipline* (1990) | Learning organizations, system archetypes | See the whole, not the parts; see change, not a still picture |
| Taleb, *Antifragile* (2012) | Antifragility, convexity preference | The best system does not resist shocks; it benefits from them |

**Core principles**:

1. **Everything sits in feedback loops**—reinforcing loops (more makes more) and balancing loops (too much brings less). To understand a system, draw its feedback loops first.
2. **Leverage points**—the most effective way to change a system is not to push harder but to find the point with the greatest influence. The highest-level leverage point is to change the system's goal and paradigm.
3. **Emergence**—the behavior of the whole cannot be derived from its parts. The knowledge base itself is an emergent system.
4. **Delay**—time passes between an action and its result. Many wrong decisions come from missing the delay: you think an action is useless because its effect is not immediate, or you think all is well because the harm has not shown yet.

### Fourth Pillar: Practice (Practice Theory)

**Core question**: how do you move from "thinking" to "doing"?

| Classic source | Core contribution | In one sentence |
|---------|---------|-----------|
| Dewey, *How We Think* (1910) | Reflective thinking, learning by doing | Knowledge is not gained by watching; it is produced by action |
| The scientific method (Bacon to Popper) | Hypothesis → experiment → verify → correct | Every theory is temporary, waiting to be replaced by a better one |
| Ries, *The Lean Startup* (2011) | The Build-Measure-Learn loop | Build a minimum viable product and test assumptions fast |
| Wang Yangming, "unity of knowing and doing" (1508) | Knowing and doing cannot be separated | True knowing means you can do it; if you cannot do it, you do not truly know |

**Core principles**:

1. **Theory must be verified through practice**—a theory not tested by practice is only a hypothesis.
2. **Start small and iterate fast**—do not wait until the theory is perfect. Test the core hypothesis at the lowest cost first.
3. **Unity of knowing and doing**—if you know but cannot do it, you have not truly understood. The four-layer chain exists to connect knowing and doing.
4. **Failure fuels theory evolution**—failure in practice is the only reliable way to find a theory's flaws. When you fail, go back and fix the theory. Do not discard it.

---

## 3. Standards for Building a Methodology

### What Is Not a Methodology

Many things look like a methodology but are not:

| This is not a methodology | Difference from a methodology |
|------------|--------------|
| One experience | An experience says "it worked for me last time." A methodology says "under what conditions it usually works." |
| One idea | An idea says "I think this might work." A methodology says "this is verified to work." |
| A procedure | A procedure says "do it in this order." A methodology says "why this order, and when not to follow it." |
| A pile of tricks | Tricks are scattered operating shortcuts. A methodology is a structured, organized operating framework |

The essence of a methodology is: **a structured operating framework with theory support, verified through practice, and reusable in similar scenarios**.

**Fewer, but better.** A poor methodology is worse than no methodology—it gives you the false sense of security that "I have an approach" while the approach is actually wrong.

### Step Zero: Theory Discovery

When you enter an unfamiliar field, the first step is not to invent a methodology but to find the theory basis that already exists in the field.

| Path | How to do it | When it fits |
|------|-------|---------|
| Find classic books | Search for the 3-5 most-cited books in the field | Mature fields (design, management, engineering) |
| Find top practitioners | Find the 5-8 recognized best cases in the field, break down what they share, and extract the implied principles | Fields where practice leads and theory lags |
| Return to the four pillars | Start from ontology, epistemology, systems theory, and practice theory; see which general principles apply | Very new fields without their own classic theory |

Theory discovery does not need to be heavy—half an hour of searching and reading is enough. The goal is not to become a theory expert in the field but to find theory anchors strong enough to support a methodology.

### Gate One: Admission Conditions

For a methodology to enter the system, it must meet all four conditions at once:

| # | Condition | How to check | What to do if it fails |
|---|------|---------|------------|
| 1 | Has theory support | Points to at least one theory source—a classic book, a top practitioner's distilled principles, or a general principle from the four pillars | Run the three theory-discovery paths first |
| 2 | Has a clear scope | States clearly when to use it and when not to use it | Keep refining the scope; do not rush to create a methodology |
| 3 | Can be operationalized | Breaks into executable steps, not stopping at "in principle it should be this way" | Keep breaking it down until every step states its input, action, and output |
| 4 | Does not overlap existing methodologies | Not a reskin of an existing methodology | Merge it into an existing methodology, or state the dimension that makes it different |

A draft methodology needs conditions 1 and 3 only. After all four conditions pass, promote it to official.

### Gate Two: Required Structure

A methodology file must contain the following sections:

| # | Section | What to write | Anti-pattern |
|---|------|-------|--------|
| 1 | Core logic | The core idea, stated in no more than three sentences | Writing a long essay that leaves the reader unsure of the core |
| 2 | Classic theory reference | The classic theory it rests on, and exactly which principle it uses | Writing "based on such-and-such theory" without naming the principle |
| 3 | Scenarios where it applies | When to use it | Writing "applies to all scenarios"—that says nothing |
| 4 | Scenarios where it does not apply | When not to use it | Leaving this section out; every methodology has a boundary |
| 5 | Operating steps | How to do it: how many steps, and what each step does | Principles without steps |
| 6 | How it is executed | How to run it—a workflow, manual steps, or a mix | The methodology is written but no one knows how to run it |
| 7 | Verified cases | At least one real case where this methodology produced a successful output (may stay empty at the draft stage) | Making up a case, or writing "it succeeded once" |

### Gate Three: Verification and Promotion

**Conditions for promoting a draft to official**:

| Condition | Explanation |
|------|------|
| Complete at least one full practice | Run it from start to finish and produce a real result |
| The output meets acceptance criteria | The result of the practice stands up to review |
| Complete all required sections | Including the verified cases |
| Meet all four admission conditions | Especially the scope, which must be clear from practice |

**Three verification metrics after an official methodology goes live**:

| Metric | How to measure | What to do if it fails |
|------|---------|------------|
| Output hit rate | Of the outputs produced with this methodology, how many meet acceptance criteria | Below 50%: check whether the operating steps have problems |
| Reuse frequency | How many times it has been used since creation | Not used for more than 90 days: check whether this methodology is truly needed |
| Iteration count | How many times practice feedback corrected it | Never corrected: either it is too perfect (unlikely), or feedback was not collected seriously |

### Six Methodology Prototypes

Many methodologies share the same underlying pattern. When you meet a new field, first see whether one of these prototypes fits, then customize it to the field:

| Prototype | Pattern | Typical use |
|------|------|---------|
| Benchmarking | Find the benchmark → break it down by criteria → extract what they share → adopt it to your own situation | Design benchmarking, competitor analysis, writing-style research |
| Reverse engineering | Take a finished product → rebuild the production process → understand the logic behind it → rebuild your own version | Product teardown, technical-solution analysis |
| Iterative trial and error | Minimum viable plan → test → collect feedback → correct → test again | Product development, content strategy, pricing tests |
| First principles | Return to the most basic facts → derive from zero → free from existing solutions | Business-model design, technology selection |
| Matrix enumeration | List all dimensions → cross-combine them → evaluate each one → screen for the best | Direction scanning, keyword mining, audience segmentation |
| Expert interview | Find field experts → extract tacit knowledge → organize it into structure | New-field research, best-practice collection |

---

## 4. Diagnosis and Tracing

### The Symptom Sits Downstream, the Root Cause Sits Upstream

When an output fails, the instinct is to fix the output, but what really needs fixing is usually upstream:

| Symptom (seen at the output layer) | Real root cause | Layer where the cause sits |
|--------------------|-----------|-----------|
| The article you write gets no readers | The distribution step is missing from the writing workflow | Workflow layer |
| The article goes off in the wrong direction | The methodology defines the audience wrongly | Methodology layer |
| Several scan rounds in a row produce no output | The theory assumption behind the scan methodology is outdated | Theory layer |
| Output quality swings up and down | The workflow gates are too loose, with no consistent acceptance criteria | Workflow layer |

- **Check** in this order: output layer → workflow layer → methodology layer → theory layer. Start from the nearest layer and rule out each layer one by one.
- **Fix** in this order: fix the most upstream layer where the root cause sits, then let the correction flow down naturally.

### Five Steps

| # | Diagnostic step | Question it answers | Action after the verdict |
|---|---------|-----------|------------|
| 0 | Chain existence check | Does the four-layer chain exist in this field | A layer missing: build it first; complete: go to step 1 |
| 1 | Output layer check | Does the output meet acceptance criteria | Meets: no problem; does not meet: go to step 2 |
| 2 | Workflow layer check | Was the workflow executed correctly | Executed wrongly: fix the workflow or rerun; executed correctly: go to step 3 |
| 3 | Methodology layer check | Does the methodology fit this scenario | Does not fit: change or fix the methodology; fits: go to step 4 |
| 4 | Theory layer check | Does the theory behind the methodology still hold | Does not hold: correct the theory and rebuild the chain from the start |

### Step Zero: Chain Existence Check

Often the problem is not that one layer is broken but that **a complete chain was never built in this field**.

| Check item | How to check | What to do if missing |
|--------|-------|-----------|
| Is there a theory basis | Can you state the principle or classic source behind this work | Run the three theory-discovery paths |
| Is there a methodology | Is there a structured approach, or do you improvise every time | Pick one of the six prototypes and build a draft methodology |
| Is there a workflow | Is there an executable sequence of steps, or is everything improvised on the spot | Break the methodology into executable steps |
| Is there acceptance criteria | Can you judge whether the work is done well after it is done | Define what "good" means first, then start |

Enter the layer-by-layer check only when all four layers exist. If something is missing, build it first—do not debug a chain that is missing parts.

> Example: a product's interface looks bad. The check finds that the design field has no methodology at all. The root cause is not a broken layer; the methodology layer does not exist. Build the methodology first (use the benchmarking prototype), then come back to fix the design.

### Step One: Output Layer Check

| Check item | How to check | Common problems |
|--------|-------|---------|
| Do acceptance criteria exist | Check whether the workflow defines acceptance conditions at its end | None defined; no way to judge good or bad |
| Does the output meet the criteria | Compare the output against each acceptance condition | Some conditions pass, some do not |
| Are the criteria themselves reasonable | Show the output to real users | The standard is set too low or too high |

Verdict: no acceptance criteria means the problem is in the workflow layer; criteria exist but the output fails them, continue checking the workflow layer; the output passes but works poorly in use, the criteria themselves are wrong, so go back to the goal definition in the methodology layer.

### Step Two: Workflow Layer Check

| Check item | How to check | Common problems |
|--------|-------|---------|
| Were all steps executed | Compare against the workflow steps and look for skipped ones | Some steps were skipped (common in manual work) |
| Was the step order correct | Check whether any steps were swapped | Producing before researching (the order is reversed) |
| Did the tools work | Check whether the tools used in the steps reported errors | A tool reported an error but it was ignored |
| Did the gates work | Check whether the stage gates at key points ran their checks | A gate was set but its result was never checked |

Verdict: executed wrongly, fix the execution and rerun; the workflow is missing a step, add it; the workflow ran correctly but the output still fails, the problem is in the methodology layer.

### Step Three: Methodology Layer Check

| Check item | How to check | Common problems |
|--------|-------|---------|
| Scenario match | Compare against the methodology's applicable and inapplicable scenarios | Forcing it into a scenario where it does not apply |
| Operating steps are feasible | Check whether the steps work under current conditions | The conditions the methodology assumes do not hold |
| Theory mapping is complete | Check for a classic theory reference | The methodology is a pile of experience with no theory support |
| Compare with similar methodologies | Check whether a better fit exists for the same scenario | A second-best methodology was used |

Verdict: the scenario does not match, change the methodology; the methodology itself has flaws, fix it against the required structure; the methodology is sound but the output still fails, the problem is in the theory layer.

### Step Four: Theory Layer Check

This is the deepest problem and the least common one.

| Check item | How to check | Common problems |
|--------|-------|---------|
| Is the theory outdated | Check the source's publication date and look for newer research that overturns it | The theory it relies on has been rejected by newer research |
| Was the theory misunderstood | Go back to the original source, reread it, and compare with your own understanding | You read the author's meaning wrong |
| Have the conditions changed | Check whether the conditions the theory assumes still hold in the current environment | The environment changed but the theory was not updated |
| Is there a better theory | Search for the latest progress in the relevant field | A better theory exists but has not been brought in |

Verdict: the theory is outdated, bring in a new theory and rebuild the chain from the theory layer; the theory was misunderstood, fix the understanding and adjust the methodology; the conditions changed, assess how far the impact reaches, then decide whether to correct the theory or mark a new scope.

### Four Symptoms of a Missing Layer

| Missing layer | Symptom | How to fix |
|---------|------|---------|
| No theory layer | The methodology cannot explain "why do it this way" | Find the theory basis first |
| No methodology layer | The workflow exists but no one knows what approach it rests on | Extract the methodology first, then attach the workflow under it |
| No workflow layer | The methodology is known but every run is improvised on the spot | Operationalize the methodology into an executable workflow |
| No acceptance criteria | The work is done but no one knows whether it is done well | Define acceptance criteria at the end of the workflow |

---

## Checklist

### Creating a Methodology

- [ ] Theory basis: you found the field's classic theory or top practitioners' experience
- [ ] Field scope: you stated the scenarios where it applies and does not apply
- [ ] Methodology prototype: you picked the closest of the six prototypes as the skeleton
- [ ] Operational path: there is a breakdown from the methodology to executable steps
- [ ] Lifecycle label: you marked it draft or official
- [ ] All seven required sections are written
- [ ] Core logic is stated in no more than three sentences
- [ ] The theory reference names the exact principle used, not a vague "based on such-and-such theory"

### Creating a Workflow

- [ ] Methodology binding: the entry file states which methodology it implements
- [ ] Steps are executable: every step has input, action, and output
- [ ] Output spec: acceptance criteria are defined at the end
- [ ] Gate design: key points have stage gates

### Adding a Theory Asset

- [ ] Fits into one of the four pillars (if not, assess whether the pillars need extending)
- [ ] Has a classic source
- [ ] Applies across scenarios (verified in at least three different scenarios)
- [ ] Can be falsified (you can state when it does not hold)
- [ ] Does not duplicate existing theory assets (reference existing assets; do not start from scratch)

### Chain Completeness Self-Check

- [ ] An output traces back to a workflow
- [ ] A workflow traces back to a methodology
- [ ] A methodology traces back to a theory basis
- [ ] The chain has no gap—no layer is skipped to connect directly

### Diagnosis Process Self-Check

- [ ] The chain existence check ran first
- [ ] Checking started from the output layer, not an intuitive jump to some layer
- [ ] Every layer ended with a clear verdict
- [ ] After finding the root-cause layer, the fix started there and flowed downstream
- [ ] After the fix, the full chain ran again and the output met the criteria
- [ ] The fix is recorded in the change log of the corresponding file

## Change Log

> Rolling window: keep the 3 most recent entries, each no more than 20 words.

| Date | Change |
|------|---------|
| 2026-08-07 | Merged the four theory-guides-practice files |
