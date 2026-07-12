# Idea Generation Guide

Reference for Phase 4 SKILL.md Steps 1–4.

---

## Section 1: Problem Mechanism Analysis

The goal is to identify WHY existing methods fail, not just THAT they fail.
A root cause is a mechanistic explanation at the level of computation, data,
objective, or architecture — not a performance observation.

### Root Cause Identification

Ask iteratively: "Why does this method fail on this problem?"

| Level | Example root cause |
|---|---|
| Data | Training distribution does not cover the test scenario |
| Representation | Features collapse distinct concepts into the same embedding |
| Objective | Loss function optimizes a proxy that diverges from the true goal |
| Architecture | Inductive bias prevents learning the target relation |
| Optimization | Gradient vanishes or explodes in the target regime |
| Evaluation | Metric does not capture the property the task requires |

### Intervention Points

An intervention point is a specific location in the pipeline where a
change could address the root cause. Common locations:

- Input representation or preprocessing
- Model architecture or attention mechanism
- Loss function or training objective
- Inference or decoding procedure
- Training data selection or augmentation
- Evaluation protocol

### Output Format

```
Root cause: [1–2 sentences — the mechanism, not the symptom]
Failure mode 1: [specific failure — context where it manifests]
Failure mode 2: ...
Key assumption: [what must be true for the root cause to be addressable]
Intervention points: [ranked list — most direct first]
```

---

## Section 2: Innovation Source Lenses

Use at least 2 lenses per idea generation session. Not all lenses apply
to every problem — document which were considered and why some were skipped.

### Lens 1: Method Transfer

Take a mechanism from a different domain or task and apply it here.

Questions to ask:
- What methods solve a structurally similar problem in a different field?
- Is there a mechanism from NLP, CV, RL, or classical ML that addresses
  the same root cause in a related setting?
- What adaptation is needed to bridge the gap?

Key risk: the structural similarity may be superficial. Verify that the
root cause is genuinely the same, not just the surface problem statement.

### Lens 2: Method Combination

Combine two existing methods that each address part of the problem.

Questions to ask:
- Method A addresses failure mode X; method B addresses failure mode Y.
  Can they be integrated without conflict?
- Where is the integration point (data pipeline, loss, architecture, training)?
- Do the methods make conflicting assumptions?

Key risk: integration overhead may exceed the benefit. Each component
must be individually necessary.

### Lens 3: Mechanism Redesign

Redesign a specific component of an existing method.

Questions to ask:
- Which module in the existing baseline is closest to the failure point?
- What is the minimal change that addresses the root cause?
- What would a "theoretically ideal" version of this module look like?

Key risk: redesign may be incremental rather than novel. The change must
address the root cause causally, not just improve a proxy metric.

### Lens 4: Problem Reformulation

Reframe the problem to make it easier to solve.

Questions to ask:
- Is the current problem formulation introducing unnecessary difficulty?
- Can the task be decomposed into simpler sub-problems?
- Is there an equivalent formulation that admits a known solution?

Key risk: reformulation may change what is actually being solved.
Verify that the reformulated problem still addresses the original gap.

### Lens 5: Data or Benchmark Reframing

Change what data is used or how evaluation is structured.

Questions to ask:
- Does the existing benchmark actually test the property of interest?
- Is there a data source or augmentation strategy that directly
  represents the distribution the gap refers to?
- Can a new synthetic setting make the problem tractable?

Key risk: this changes the evaluation target, which may not be accepted
by the community. Requires strong justification.

### Lens 6: Theory-Driven

Start from a theoretical result and derive a mechanism.

Questions to ask:
- Is there a theoretical guarantee that applies to the gap structure?
- What inductive bias would a theory of generalization predict is needed?
- Are there information-theoretic bounds that suggest the direction?

Key risk: theory and practice diverge often in deep learning. Theoretical
motivation is valuable but does not substitute for empirical validation.

---

## Section 3: Conceptual Validation

Apply these checks to every idea before writing a full proposal.
An idea that fails check 1 or 2 should be dropped immediately.

### Check 1: Causal Fit (Required)

Does the mechanism directly address the root cause from Section 1?

- YES: the mechanism modifies the exact intervention point identified
- PARTIAL: the mechanism addresses a symptom, not the root cause
- NO: the mechanism does not connect to the root cause

An idea with causal fit = NO or PARTIAL without justification is not
worth developing further.

### Check 2: Internal Consistency (Required)

Are the components of the proposed idea compatible?

Incompatibility patterns to look for:
- The mechanism requires information not available at the identified
  intervention point
- Two components make contradictory assumptions
- The mechanism addresses a failure mode that only occurs because of
  a different mechanism the idea also relies on

### Check 3: Feasibility Boundary

Can this be done with standard resources?

| Feasibility | Indicators |
|---|---|
| Feasible | Training on 1–8 GPUs, standard datasets, known frameworks |
| Risky | Requires proprietary data, 100+ GPU days, novel hardware |
| Infeasible | Requires exponential compute, unavailable data, or unsolved sub-problems |

Document the specific constraint if risky or infeasible.

### Check 4: Novelty Assessment

| Status | Meaning |
|---|---|
| `unsearched` | No literature check done — could be prior art |
| `partial` | Quick search found adjacent work — differences not verified |
| `searched` | Targeted search done — differences from closest work documented |

Never upgrade to `searched` without actually reading the closest paper.
Never claim `novel` as a status — novelty is an outcome, not a self-assessment.

### Check 5: Falsifying Observation

State one result that would immediately kill this idea.

A good falsifying observation:
- Is a single, runnable experiment
- Would be produced early in Phase 6 (e.g., an ablation or sanity check)
- Would prevent wasting effort on a Phase 5 methodology that cannot work

Example: "If removing the proposed component does not degrade performance
on the core failure case, the mechanism is not causally necessary."
