# Gap Classification Guide

Used in SKILL.md Steps 2–4. Provides a systematic framework for classifying
research gaps in AI/CS, with how to find each type.

---

## Section 1: Method Limitation Analysis Framework

Analyse every major Method Family across four limitation dimensions.

### Dimension 1: Performance Limitations

**Definition**: The method achieves acceptable results on standard
benchmarks but hits a ceiling that matters for the target application.

**How to find**:
- Look at benchmark leaderboards: what is the gap between SOTA and
  human-level or application requirement?
- Identify sub-tasks or sub-populations where the method underperforms
  relative to overall score (disparate performance)
- Check if the method degrades gracefully or catastrophically as task
  difficulty increases

**Evidence template**:
```
Method: [Name]
Performance ceiling: [Benchmark, score, year]
Required level: [Application requirement or human baseline]
Gap magnitude: [Quantified difference]
Where the gap concentrates: [Sub-task, input type, or condition]
```

**Gap signal**: Performance gap is concentrated in a specific, nameable
condition → that condition is the bounded research problem.

---

### Dimension 2: Efficiency Limitations

**Definition**: The method is accurate but too slow, too large, or too
expensive for real deployment.

**How to find**:
- Check training compute (GPU-hours, parameters) vs deployment budget
- Check inference latency vs real-time requirement
- Check memory footprint vs edge device or API cost constraint
- Find the scaling law: does the method need 10× more compute for 1%
  more accuracy?

**Evidence template**:
```
Method: [Name]
Resource requirement: [FLOPs / latency / memory / cost at deployment]
Deployment constraint: [Real-world budget or SLA]
Gap: [What cannot be done under constraint]
```

**Gap signal**: A method is accurate but cannot be deployed in a
high-value scenario due to resource cost → efficiency-deployment gap.

---

### Dimension 3: Generalization Limitations

**Definition**: The method performs well on training-similar distributions
but degrades on novel inputs.

**How to find**:
- Check cross-dataset transfer results (trained on A, tested on B)
- Check ablation studies that vary data domain or input style
- Look for "domain adaptation" papers citing this method — they often
  contain quantified generalization gaps

**Evidence template**:
```
Method: [Name]
In-distribution performance: [Benchmark, score]
Out-of-distribution condition: [What changes — domain, style, language, etc.]
OOD performance: [Score or qualitative assessment]
Degradation: [Magnitude and nature of failure]
```

**Gap signal**: Degradation is consistent across multiple OOD conditions
→ fundamental generalization failure, not a dataset artifact.

---

### Dimension 4: Robustness Limitations

**Definition**: The method fails unexpectedly on edge cases, adversarial
inputs, or rare-but-important scenarios.

**How to find**:
- Check adversarial robustness benchmarks (AutoAttack, RobustBench, etc.)
- Look for challenge datasets designed to stress-test specific methods
- Search for papers explicitly testing failure cases of this method
- Check deployment incident reports or real-world usage analyses

**Evidence template**:
```
Method: [Name]
Nominal performance: [Clean benchmark]
Stress condition: [Adversarial / rare / extreme input]
Robustness performance: [Score under stress]
```

**Gap signal**: Robust performance is significantly worse than nominal
performance in a scenario relevant to safe deployment → robustness gap.

---

## Section 2: Comparative Analysis Framework

Gap signals that only appear when methods are compared side-by-side.

### The A→B→C Chain Pattern

The most productive comparative pattern:

```
Method A: solves problem P1, but creates problem P2
      ↓
Method B: solves P2, but creates problem P3
      ↓
Method C: solves P3, but creates problem P4   ← OPEN END
```

Where P4 has no known solution → research gap.

**How to construct**:
1. Start from the evolution chain in `evolution_chains.md`
2. For each chain, identify the last "residual limitation"
3. Confirm the residual limitation is not solved by any method in the taxonomy

### The Tradeoff Pattern

Two methods each sacrifice something different:

```
Method A: high accuracy, high cost
Method B: low cost, low accuracy
```

Gap: no method achieves high accuracy at low cost. But be specific —
not all tradeoffs are researchable. The gap is only valid if:
- The tradeoff region is theoretically non-empty (it should be possible)
- No existing method occupies that region
- A method occupying that region would be valuable

### The Contradiction Pattern

Two papers report contradictory results on the same benchmark or claim:

```
Paper A: "Method X achieves Y on benchmark Z"
Paper B: "Method X fails on benchmark Z in condition C"
```

This contradiction signals either a **scope limitation** (X works only
in specific conditions) or a **measurement problem** (the benchmark
measures different things in different setups). Both are gaps.

**Evidence requirement**: quote both papers' specific claims with citations.
Do not infer contradictions — they must be explicit in the text or data.

---

## Section 3: Theoretical and Application Gap Framework

### Theoretical Gaps

**Type T1 — Unexplained Success**
A method works significantly better than theory predicts.

```
Observation: Method X achieves Y, but theory says Y should be impossible
             or should require much more data/compute.
Theoretical gap: No theoretical account of why X works.
```

Example: Neural networks generalize well despite being heavily over-parameterized,
contradicting classical bias-variance theory.

**Type T2 — Theory Does Not Transfer**
Theory explains behavior in setting A but fails to predict behavior in setting B.

```
Theory: Framework F correctly models phenomenon in setting A.
Observed failure: Framework F predicts wrong outcome in setting B.
Gap: Theory needs extension or revision to cover setting B.
```

**Type T3 — Fundamental Bound Not Known**
The field does not know whether a capability is achievable in principle.

```
Open question: Is it possible to achieve P under constraint C?
Current state: Neither a proof nor a disproof exists.
```

**Evidence requirement for theoretical gaps**: cite at least one paper
acknowledging the theoretical gap explicitly, or two papers whose results
jointly imply it.

---

### Application Gaps

**Type A1 — Lab-to-Real Transfer Failure**

```
Lab result: Method achieves X on benchmark under controlled conditions.
Deployment blocker: [Privacy regulation / latency / annotation cost /
                     hardware unavailability / safety requirement]
Why current methods do not address it: [one sentence]
```

Example: Medical image analysis achieves 95% accuracy in lab but cannot
be deployed because it requires 100k annotated examples per hospital,
which is unavailable in practice.

**Type A2 — Coverage Gap**

```
Target population: [Who the system should serve]
Current coverage: [Who current benchmarks and evaluations actually cover]
Missing: [What population, language, setting, or edge case is absent]
```

Example: NLP systems evaluated only on English perform poorly on
morphologically rich languages with limited training data.

**Type A3 — System Integration Gap**

```
Component performance: Method X achieves high performance in isolation.
System failure: When integrated into system Y, performance degrades
                or the method is incompatible.
```

---

## Gap Candidate Quality Criteria

Before adding a candidate to the register, verify:

| Criterion | Check |
|---|---|
| Bounded | Can you name the specific method, condition, and failure? |
| Evidence-backed | Is there at least one explicit or observed source? |
| Non-trivial | Is this a known limitation that everyone acknowledges and ignores, or a real open problem? |
| Researchable | Is there a plausible line of investigation (even if unknown)? |
| Not already solved | Quick check: does a 2024 paper already directly address this? |

Reject candidates that fail the "Bounded" or "Researchable" checks.
Keep candidates that pass all five for the saturation test in Step 6.
