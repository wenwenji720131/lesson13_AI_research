# Methodology Design Guide

Reference for Phase 5 SKILL.md Steps 2, 3, and 7.

---

## Section 1: Framework Design

A framework specification describes the overall system architecture — what
exists, what flows between components, and why each component is present.

### Design Principles

**One core problem → one core mechanism.**
Resist the temptation to add modules for completeness, robustness, or
generality. Each module must serve the method objective directly. If a
module's removal would not affect the core claim, remove it.

**The simplest framework that works is the best framework.**
Complexity adds implementation burden, ablation burden, and reviewer skepticism.
Start minimal; add only when a failure mode demands it.

**The framework diagram must be describable without running code.**
If you cannot describe the data flow in words, the framework is not
fully designed yet.

### Framework Specification Format

```
Input: [what enters the system — modality, shape, source]
Output: [what the system produces — prediction, embedding, action, etc.]

Modules:
  [Module A]: [one-line purpose]
  [Module B]: [one-line purpose]
  ...

Data flow:
  Input → [Module A] → [intermediate representation] → [Module B] → Output

Integration points:
  [how this connects to existing infrastructure or base models]
  [which components are new vs. reused from prior work]
```

### Module Necessity Test

For each module, answer:
1. What does the method do without this module?
2. If the answer is "works roughly the same," remove it.
3. If the answer is "fails on the specific case we designed for," keep it.

---

## Section 2: Core Mechanism Design

The mechanism is the design choice that makes the method work. It must be:
- Specific: "we replace standard cross-attention with locality-biased
  attention where weight decays exponentially with distance"
- Causal: the change must causally address the root cause, not correlate
  with better performance for an unrelated reason
- Justified: explain why the specific design choice works, not just that
  it works empirically

### Mechanism Specification Format

```
Mechanism name: [short descriptive name]
Existing approach it replaces or extends: [baseline operation, cited]
What changes: [the specific modification]
Why this change addresses the gap: [causal argument — 3–5 sentences]
What would happen without it: [expected behavior if removed — this becomes
  the ablation hypothesis in Phase 6]
```

### Anti-Patterns to Reject

| Anti-pattern | Why it fails |
|---|---|
| "Add a new module" | Module addition is architecture, not mechanism |
| "Use a larger network" | Resource, not mechanism |
| "Fine-tune on task-specific data" | Training recipe, not mechanism |
| "Apply attention" | Generic; applies everywhere; not a mechanism for THIS gap |
| "Use a better loss" | The mechanism IS the loss design; specify it |

### Causal Argument Structure

A valid causal argument has the form:

> [Current behavior] happens because [mechanism at play]. By changing
> [X] to [Y], we prevent [failure mode] from occurring because [causal chain].
> Without this change, we would expect [specific degradation].

If you cannot fill in this template with specific, testable claims, the
mechanism is not fully designed yet.

---

## Section 3: Evaluation Strategy Design

The evaluation strategy is a planning document — it specifies what evidence
would convince a reader that the method works.

### Baseline Selection Criteria

A baseline is appropriate if:
- It represents the current state of the art for this problem
- It is fairly compared (same data, same compute budget, published implementation)
- Its failure mode is the one the proposed method claims to fix

Inappropriate baselines:
- Methods known to be outdated for this setting (strawman)
- Methods the authors implement themselves without reporting implementation
  effort (risks subtle bugs that favor the proposed method)
- Methods tuned on a smaller hyperparameter budget than the proposed method

Include at least one "strong" baseline: a method tuned specifically for
this comparison, not a default configuration.

### Dataset Selection Criteria

Each dataset must test a specific claim. Do not include datasets for
coverage alone. For each dataset, state:

```
Dataset: [name]
Split used: [standard / custom — if custom, justify]
Why this dataset: [what property it tests that others do not]
Known limitations: [distribution shift, size, annotation quality]
```

### Ablation Design

An ablation study answers: "Is each design decision individually necessary?"

Each ablation variant removes or replaces exactly ONE component or design choice.
The variant serves as a hypothesis: "Component X is necessary because
removing it causes [specific degradation]."

Required ablations:
- One variant per key design decision from Phase 5 Step 3
- One variant replacing the proposed mechanism with the simplest baseline

Do NOT ablate hyperparameter values — that is a sensitivity experiment,
not an ablation.

### Metric Selection

```
Primary metric: [what to optimize — the one used to set hyperparameters]
Secondary metrics: [what to report additionally for completeness]
Efficiency metrics: [latency / memory / FLOPs — required if any efficiency claim]
```

Primary metric must directly measure the property the gap refers to.
If the gap is about generalization, the primary metric must measure OOD
performance, not in-distribution performance.
