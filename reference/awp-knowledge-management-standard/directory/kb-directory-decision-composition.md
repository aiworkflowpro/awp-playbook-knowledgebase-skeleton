---
document_id: awp-knowledge-management-standard/directory/kb-directory-decision-composition
language: en
publication: public
title: "Directory Pattern Decision Tree and Composition Rules"
purpose: Define how to select a pattern when creating a new directory area, how to combine multiple patterns, and which practices are prohibited
category: General Specification
audit:
  group: Directory System
  dimension: Directory System Compliance
  check: "Is the combination order following composition rules; are forbidden patterns hit"
  metric: "Inconsistent date formats in same level = error; nesting depth > 4 layers = warn; time layer contains entity layer = error"
---

# Directory Pattern Decision Tree and Composition Rules

> Scope: When creating a new directory area, **how to select one pattern from the registry**, how to **combine multiple patterns**, and **which practices are forbidden**.
> Out of scope: What patterns are available (→ Directory Organization Pattern Registry); file names (→ Naming Dimension).
> Prerequisite: Read Directory Organization Pattern Registry first; this document's branch nodes directly reference pattern numbers from there.

---

## This Document in Three Sections

| Section | Question | Content |
|---|------|------|
| §2 | How to choose? | Decision tree—judgment flow to select patterns by output characteristics |
| §3 | Can we combine? | Composition rules—combination order, forbidden combinations, depth limits |
| §5 | What's forbidden? | Taboos—no same-level mixing, format inconsistency, etc. hard prohibitions |

---

## §2 Decision Tree

When creating a new directory area, judge in this order:

```text
Q1: Will the content in this area grow continuously over time?
  ├─ Yes → Q2
  └─ No → Q5

Q2: What is the growth granularity?
  ├─ One file per day → T3 (month bucket + date file)
  ├─ Multiple independent directories per day → T1 (month bucket + day directory) or T2 (month bucket + date-prefixed directory)
  │   └─ Q3: Do outputs on the same day share a common parent?
  │       ├─ Yes (e.g., same day workflow outputs) → T1
  │       └─ No (independent events) → T2
  └─ Track by task ID → T4 (task ID style)

Q4: ⬆ After selecting the time layer above, does the parent of the time layer need to be bucketed by entity?
  ├─ Yes → Add E1/E2/E3 (see §3 Composition Rules)
  └─ No → Use time pattern directly

Q5: How is content organized by entity?
  ├─ By brand → E1 (brand × dimension)
  ├─ By person → E2 (person dimension)
  ├─ By responsibility/function → E3 (functional responsibility)
  ├─ By product development lifecycle → P1 (product development lifecycle nodes)
  ├─ By research partition + material accumulation → K1 (partition + material month bucket)
  ├─ By business scanning module (three-piece set) → K3
  └─ By workflow/best practice assets → A1/A3 (match registry)

Q6: Need dual machine index + human view layers?
  ├─ Yes → K2 (index + view hybrid)
  └─ No → Use the pattern selected above
```

⚠️ The decision tree covers common scenarios. For new scenarios that don't fit the classification, register a new pattern in the registry first, then use it. ❌ Do not skip registration and invent directly.

---

## §3 Composition Rules

### Stacking Order

One area can stack multiple patterns; stacking order from outside to inside:

```text
Layer 1: Entity bucket (E1/E2/E3)
Layer 2: Functional responsibility (E3)
Layer 3: Time bucket (T1/T2/T3/T4)
Layer 4: Leaf (files or domain-defined internal structure)
```

✅ Entity layer always wraps time layer.
✅ Use only one pattern per layer.

### Composition Examples

| Area | Stack | Actual Path |
|------|------|---------|
| Business brand articles | E1 + domain deep path | `{business_root}{brand}/website/content/{category}/{slug}/` (depth by business methodology, not mechanical 4 layers) |
| Run output | T5 | `{run_output_root}{YYYYMM}/{YYYYMMDDHHmmss}_{source}_{summary}/` |
| Research materials | K1 (includes month bucket) | `{research_root}topic/{topic}/materials/{YYYYMM}/{project}/` |

### Depth Limit

✅ After stacking, directory layers from area root to leaf file ≤ 4 layers (excluding the file itself).

```text
Good: {run_output_root}202606/20260625/                        → 3 layers ✅
Good: {research_root}topic/{topic}/materials/202606/            → 4 layers ✅
Bad: {business_root}{brand}/website/content/tutorials/{slug}/images/  → 6 layers ❌
```

⚠️ When exceeding 4 layers, prioritize checking if middle layers can be merged or leaf layers flattened.

### Forbidden Combinations

| Forbidden | Reason |
|------|------|
| Same-level mix of T1 and T3 | Searching becomes confused when one moment uses day directories and the next uses day files in the same level |
| Time layer nests entity layer inside time layer | e.g., `{YYYYMM}/{brand}/`, violates "entity outside time inside" principle |
| A1 and A3 stacking | Workflow directory and best practice directory naming systems are incompatible |

---

## §5 Taboos

| Number | Forbidden Practice | Reason |
|------|---------|------|
| X1 | ❌ Mixed date formats in the same level | e.g., `YYYYMMDD` and `YYYY-MM-DD` coexist in same level, sorting and retrieval become chaotic |
| X2 | ❌ Inventing unregistered directory patterns | Pattern sprawl fragments the overall knowledge base structure |
| X3 | ❌ Directory names containing spaces | Path references and script processing easily error |
| X4 | ❌ Stacking exceeds 4 directory layers | Over-deep nesting indicates layering design problems |
| X5 | ❌ Time layer contains entity layer | e.g., `202606/{brand}/`, violates "entity outside time inside" principle |
| X6 | ❌ Using directory depth to simulate versioning | e.g., `v1/` `v2/` subdirectories; for product versioning rules see the version and release chapter of the Product Development standard |
| X7 | ❌ Functional responsibility directory named with dates | Fixed structure areas should not be time-bucketed |

---

## Checklist

**Creating new directory area**:

- [ ] Completed judgment flow in §2 decision tree
- [ ] Total depth after stacking ≤ 4 layers
- [ ] Same level uses only one pattern
- [ ] Entity layer wraps time layer
- [ ] Directory names have no spaces, no special characters
- [ ] Date formats consistent with same-level existing directories

**Auditing existing area**:

- [ ] No §5 taboo practices
- [ ] No §3 forbidden combinations
