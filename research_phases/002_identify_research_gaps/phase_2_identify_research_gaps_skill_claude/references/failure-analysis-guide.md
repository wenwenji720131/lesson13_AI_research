# Failure Analysis Guide

Used in SKILL.md Step 3. Guides systematic analysis of when and why current
AI/CS methods fail, and how to convert failure patterns into research problems.

---

## Why Failure Analysis Matters

Many top-tier AI papers originate from a precise answer to:
> "When exactly does this model fail, and what does that failure reveal
> about an unresolved fundamental problem?"

Failure analysis differs from limitation analysis:
- **Limitations** — what authors acknowledge in their papers
- **Failure analysis** — what you discover by asking: under what specific
  conditions does performance degrade catastrophically, and why?

---

## Failure Analysis Pipeline

```
Step A: Identify failure scenarios
         ↓
Step B: Classify failure modes
         ↓
Step C: Root cause analysis
         ↓
Step D: Research problem formulation
```

---

## Step A: Identify Failure Scenarios

A failure scenario describes the **conditions** under which a method breaks,
not just that it "has limitations."

### Sources for finding failure scenarios

| Source | Evidence type | Where to look |
|---|---|---|
| Paper limitation sections | `explicit` | Last section or abstract |
| Error analysis appendices | `observed` | Tables breaking down error types |
| Benchmark per-category scores | `observed` | Leaderboard breakdowns, sub-task tables |
| Ablation studies | `observed` | Component removal causing large drops |
| Citing papers | `explicit` or `inferred` | Papers that frame their contribution as fixing method X |
| Challenge / stress-test datasets | `observed` | Papers designed to break existing methods |

### Scenario description format

```
Method: [Name]
Failure scenario: [Specific input condition or environment]
Evidence source: [Paper title, section/table/figure, URL]
Evidence type: explicit | observed | inferred
Performance drop: [Quantified if available — e.g., "89% → 61% under noise"]
```

### Common failure scenario patterns in AI/CS

| Type | Example |
|---|---|
| Input distribution shift | Model trained on clean images fails on noisy inputs |
| Domain transfer | Model trained on English fails on low-resource languages |
| Long-tail / rare cases | Autonomous driving fails on unusual traffic scenarios |
| Scale mismatch | Method works for short inputs, fails for long documents |
| Compositional inputs | Model handles A and B separately, fails on A+B |
| Temporal drift | Model trained in 2021 degrades on 2024 data patterns |
| Resource constraints | Method requires 80GB GPU, unavailable in deployment |
| Adversarial conditions | Small perturbation causes confident wrong prediction |

---

## Step B: Classify Failure Modes

Assign one or more labels from this taxonomy to each scenario.

| Label | Description | Typical research direction |
|---|---|---|
| `distribution-shift` | Train and test distributions differ | Representation learning, domain adaptation |
| `long-tail` | Rare events cause failure | Data augmentation, few-shot learning |
| `compositional` | Works on parts, fails on combinations | Compositional generalization, structured prediction |
| `adversarial` | Small perturbations cause large output changes | Adversarial robustness, certified defenses |
| `temporal` | Performance degrades without retraining | Continual learning, temporal alignment |
| `scale` | Fails beyond a size threshold | Efficient algorithms, approximation methods |
| `resource` | Correct result but cannot run in deployment | Model compression, efficient inference |
| `annotation` | Fails when labels are expensive or noisy | Weak supervision, label-efficient learning |
| `cross-domain` | Fails on different task domain | Transfer learning, domain generalization |
| `theory-gap` | Works empirically but no theoretical guarantee | Theoretical analysis, formal guarantees |
| `evaluation` | Benchmark saturates before real problem is solved | New benchmark design, evaluation methodology |

A scenario can carry multiple labels (e.g., `distribution-shift` + `long-tail`).

---

## Step C: Root Cause Analysis

For each failure scenario and mode, ask: **why does the model fail here
at a fundamental level?**

Root causes differ from symptoms:
- **Symptom**: "accuracy drops from 89% to 61% on noisy images"
- **Root cause**: "the model relies on high-frequency texture features
  destroyed by noise, rather than noise-invariant shape features"

### Root cause questions by failure mode

| Mode | Root cause questions |
|---|---|
| `distribution-shift` | What features does the model rely on that are unstable across distributions? Data problem or inductive bias problem? |
| `long-tail` | Does the model memorize frequent patterns or learn generalizable rules? How many examples per scenario does it need? |
| `compositional` | Are independent features or joint representations learned? Compositionality bottleneck: architecture, training, or data? |
| `adversarial` | What decision boundaries are exploited? Robust features or shortcut features? |
| `scale` | What operation has super-linear complexity? Why wasn't it approximated? |
| `theory-gap` | What theoretical property would explain the observation? What does current theory predict that contradicts the result? |
| `evaluation` | What does the benchmark measure that the real task doesn't? What does the real task require that the benchmark ignores? |

### Root cause statement format

```
Root cause: [One sentence — the fundamental reason for failure]
Evidence basis: [What the cause is inferred from]
Confidence: high | medium | low
Alternative explanations: [Other possible causes, if any]
```

---

## Step D: Research Problem Formulation

Convert each root cause into a **research problem** — a question about
what is not yet understood or achievable. Never a solution proposal.

### Formulation rules

**Rule 1: Question or need form only**
- ✅ "How can X be achieved under constraint Y?"
- ✅ "What mechanism explains the failure of Z in condition W?"
- ✅ "A method is needed that achieves P without requiring Q."
- ❌ "We will design a new architecture that..."
- ❌ "The solution is to add a regularization term..."

**Rule 2: Bounded and specific**
- ✅ "Multi-hop reasoning failure in RAG under 3+ hop questions"
- ❌ "LLMs sometimes hallucinate"

**Rule 3: Traceable to failure analysis**
- State which failure scenario and root cause this problem addresses

### Formulation template

```
Research problem: [Question or need statement — specific, bounded]
Failure scenario: [From Step A]
Root cause grounding: [From Step C]
Observable progress signal: [What would count as solving this — no method design]
```

---

## `failure-analysis.md` Output Schema

```markdown
# Failure Analysis: [Research Area / Method Family]

## Method Family: [Name]

### FA-[N]: [Short scenario name]

**Scenario**: [Condition under which the method fails]
**Evidence**: [Paper title, section, figure/table, URL]
**Evidence type**: explicit | observed | inferred
**Performance data**: [Quantified drop if available]

**Failure mode**: [label(s) from taxonomy]

**Root cause**:
[One sentence explaining WHY the method fails]
Evidence basis: [...]
Confidence: high | medium | low

**Research problem**:
[Question or need statement — Phase 2 boundary: no solution]
Traceability: FA-[N] → root cause → this problem

---

## Cross-family Patterns

[Failure modes or root causes appearing across multiple families —
strongest gap signals]

| Pattern | Families affected | Shared root cause | Candidate ID |
|---|---|---|---|
```

---

## Prioritizing Failure Scenarios for Gap Candidates

After completing the analysis, flag scenarios for the candidate register
using these signals:

| Priority signal | Explanation |
|---|---|
| Appears in multiple method families | Likely a deeper problem, not an implementation artifact |
| Performance drop > 15% | Material impact on capability |
| Core use case affected | Blocks a primary application, not an edge case |
| No existing workaround | Current practice has no effective mitigation |
| Acknowledged by surveys | Independent sources confirm the problem is open |
| Contradicts theoretical predictions | Reveals a theory-practice gap |

Add high-priority scenarios to the candidate register with `source=failure_analysis`.
