---
name: phase5-refine-methodology
description: >
  Transform a selected research idea into a complete, executable, and
  verifiable methodology (Phase 5). Takes Phase 4 output (top idea proposal)
  as primary input. Produces Methodology Document, Framework Design,
  Algorithm Description, Experimental Plan, and Risk Analysis.
  Use when the user wants to design a method, formalize an algorithm,
  plan training strategy, or prepare a methodology before experiments.
  Triggers on: "设计方法", "方法设计", "refine methodology", "method design",
  "algorithm formulation", "实验方案设计", "如何实现这个想法".
  DO NOT use for: running actual experiments (Phase 6), writing the paper (Phase 8),
  or generating new ideas (Phase 4).
user-invocable: true
argument-hint: "<idea_proposal_or_phase4_dir> [--depth quick|standard|deep]"
---

# Phase 5: Refine Methodology

Transform a validated research idea into a logically closed, implementable,
and verifiable method. The output is NOT code — it is a design specification
precise enough that someone could implement it.

## Phase Boundary (Hard Limits)

| Forbidden output | Belongs to |
|---|---|
| Running experiments or training models | Phase 6 |
| Large-scale hyperparameter search | Phase 6 |
| Writing paper sections | Phase 8 |
| Generating new ideas or pivoting the research question | Phase 4/3 |
| Claiming experimental results | Phase 6/7 |

Phase 5 asks: "How exactly should this be designed and why?"
Phase 6 asks: "Does it actually work?"

## Inputs

| File | Used in |
|---|---|
| Phase 4 `phase4-handoff.md` | All steps — idea and mechanism |
| Phase 3 `candidate-rqs.md` | Step 1 — alignment check with RQ |
| Phase 2 `research-gap-document.md` | Step 1 — gap context |
| Phase 1 `taxonomy.md` | Steps 2–3 — architectural baselines |

## Arguments

- **--depth**: `quick` (Steps 1–3 + 7) | `standard` (all 8 steps) | `deep` (all + formal complexity analysis)

---

## Workflow

### Step 1: Method Objective Formulation

Convert the Research Question into a precise optimization target.

The method objective must be:
- Bounded: specifies what to improve, not just "improve performance"
- Measurable: corresponds to a metric
- Tied to the gap: directly addresses the root cause from Phase 2/4

Format:
```
Research Question: [from Phase 3]
Core gap: [the root cause the method must address]
Method objective: [formal statement — Minimize X / Maximize Y / Achieve P without Q]
Success criterion: [what counts as solving the problem]
Out-of-scope: [what the method is NOT trying to do]
```

If the method objective contradicts the gap (e.g., gap is efficiency but
objective adds computation), stop and reframe before proceeding.

---

### Step 2: Framework Design

Design the overall system architecture.

Load `references/methodology-design-guide.md` Section 1.

Produce a framework specification:
```
Input: [what the system receives]
Output: [what the system produces]
Modules: [list of components with one-line purpose each]
Data flow: [Input → Module A → Module B → ... → Output]
Integration points: [how this connects to existing infrastructure]
```

Principles:
- One core problem → one core mechanism. Do not add modules for "completeness."
- Each module must serve the method objective. Remove modules that don't.
- The framework diagram (Figure 1 in the future paper) should be describable
  in this step.

---

### Step 3: Core Mechanism Design

This is the creative and critical step. Design the mechanism that makes the
method work — not just what it does, but WHY it solves the gap.

Load `references/methodology-design-guide.md` Section 2.

For the main module(s), specify:
```
Mechanism name: [short descriptive name]
Existing approach it replaces or extends: [name the baseline operation]
What changes: [the specific modification — mathematically or procedurally]
Why this change addresses the gap: [the causal argument]
What would happen without it: [expected behavior if this module is removed]
```

Anti-patterns to reject:
- "Add a new module" without explaining the causal mechanism
- "Use a larger network" — this is resource, not mechanism
- Mechanisms that add complexity without addressing the root cause

---

### Step 4: Algorithm Formulation

Convert the mechanism into a precise, implementable specification.
Load `references/algorithm-template.md`.

Required outputs:
1. **Algorithm pseudocode** — structured procedure with named inputs/outputs
2. **Mathematical formulation** — key equations for the core operations
3. **Complexity analysis** — time and space complexity vs. baseline

Format:
```
Algorithm: [Name]
Input: [variables with types/shapes]
Output: [variables with types/shapes]
Parameters: [hyperparameters and their ranges]

Step 1: ...
Step 2: ...
...

Key equations:
[equation block]

Complexity:
Time: O(...) vs baseline O(...)
Space: O(...) vs baseline O(...)
```

If complexity is significantly worse than the baseline, justify why the
tradeoff is acceptable OR redesign in Step 3.

---

### Step 5: Theoretical Justification

Explain WHY the method works at a principled level. This does NOT require
formal proofs for most AI/CS papers but requires a clear causal argument.

Provide one or more of:

**a) Mechanism explanation**: why does the design choice address the root cause?
Use analogies to existing theoretical results if available.

**b) Complexity analysis**: if the contribution is efficiency, provide the
comparison table (Before: O(n²), After: O(n log n)).

**c) Convergence / stability argument**: for optimization-based methods,
why does training converge? What guarantees does the loss design provide?

**d) Generalization argument**: for out-of-distribution claims, what inductive
bias does the method introduce that should improve generalization?

Document as:
```
Theoretical claim: [what property is argued]
Argument type: mechanism-explanation | complexity | convergence | generalization
Argument: [the reasoning]
Evidence basis: [prior results this builds on]
Confidence: high | medium | low
What would invalidate this: [the key assumption that must hold]
```

---

### Step 6: Optimization Strategy

Specify how the method is trained / optimized.

| Component | Specification |
|---|---|
| Loss function | What is minimized? If composite: L = L_main + λ·L_aux |
| Training procedure | Pretraining / fine-tuning / RL / etc. |
| Data strategy | Standard / augmentation / curriculum / synthetic |
| Inference strategy | Greedy / beam search / sampling / prompting |

Document the training configuration:
```
Training objective: [loss formula]
Data: [source, size, preprocessing]
Optimization: [optimizer, lr schedule, batch size range]
Inference: [how the model is used at test time]
```

Note: this step specifies the strategy; hyperparameter values are found in Phase 6.

---

### Step 7: Evaluation Strategy

Design the experiment plan — this is a planning document, not execution.
Load `references/methodology-design-guide.md` Section 3.

Required elements:
```
Baselines:
  - [Method 1]: [why this is an appropriate comparison]
  - [Method 2]: ...

Datasets/Benchmarks:
  - [Dataset 1]: [what property it tests]
  - [Dataset 2]: ...

Primary metrics: [what to optimize for]
Secondary metrics: [what to report additionally]

Ablation plan:
  - Remove [component A]: tests whether A is necessary
  - Remove [component B]: tests whether B is necessary
  - Replace [mechanism] with [baseline mechanism]: tests mechanism superiority

Efficiency evaluation: [latency / memory / FLOPs comparison]
```

Validation criteria for the experiment plan:
- Every claim in the future paper must have a corresponding experiment
- Baselines must be competitive — no strawman comparisons
- Ablation must cover every key design decision

---

### Step 8: Risk Analysis and Validation

Identify the ways the method could fail and design mitigations.
Load `references/validation-checklist.md`.

**Risk register**:
```
Risk: [what could go wrong]
Probability: high | medium | low
Impact: blocks-all | major | minor
Mitigation: [design change or experimental precaution]
Detection: [what experiment would reveal this risk has materialized]
```

**Run the 7 validation checks** from `references/validation-checklist.md`:
1. Method-Gap Alignment Test
2. Mechanism Justification Test
3. Component Necessity Test
4. Novelty Test
5. Experimental Testability Test
6. Complexity / Resource Test
7. Failure Prediction Test

A method is ready for Phase 6 only when all 7 checks pass.

---

## Output Package

```
phase5-methodology-YYYYMMDD-<slug>/
  methodology-document.md   ← Steps 1–3 (objective, framework, mechanism)
  algorithm-spec.md         ← Step 4 (pseudocode, equations, complexity)
  theoretical-basis.md      ← Step 5 (justification arguments)
  training-strategy.md      ← Step 6 (optimization and training plan)
  evaluation-plan.md        ← Step 7 (baselines, datasets, ablations)
  risk-analysis.md          ← Step 8 (risks and mitigations)
  phase5-validation.md      ← 7-check checklist + Phase 6 handoff
```

`phase5-validation.md` must state explicitly: "This methodology is
ready for Phase 6 experiments" or list the checks that failed.

---

## Skill Linkage

- **Upstream**: `phase4-generate-research-ideas` → provides `phase4-handoff.md`
- **Downstream**: `phase6-design-conduct-experiments` → receives `evaluation-plan.md`
  and `methodology-document.md`
- **Support tools**:
  - `ccf-idea-optimizer` — for sharpening the innovation framing only
  - `ccf-experiment-designer` — for extending the evaluation plan (Step 7)
