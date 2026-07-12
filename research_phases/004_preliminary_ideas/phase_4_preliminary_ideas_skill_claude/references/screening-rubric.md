# Screening Rubric

Reference for Phase 4 SKILL.md Step 6 (Idea Screening).

Evaluate each idea on 5 dimensions using anchored 1–5 scores.
Total score range: 5–25. Decision thresholds at the bottom.

---

## Dimension 1: Causal Fit

Does the mechanism directly and causally address the root cause identified
in the mechanism map?

| Score | Anchor |
|---|---|
| 5 | Mechanism targets the exact intervention point; causal chain is explicit and complete |
| 4 | Mechanism addresses the root cause with one unstated assumption |
| 3 | Mechanism addresses a symptom of the root cause, not the cause itself |
| 2 | Mechanism has a tangential connection to the gap |
| 1 | Mechanism does not connect to the root cause |

---

## Dimension 2: Novelty

How likely is this to be genuinely new work?

| Score | Anchor |
|---|---|
| 5 | Targeted search done; no paper does this; specific difference documented |
| 4 | Partial search done; closest work differs in at least one key dimension |
| 3 | Unsearched; conceptually distinct from obvious prior art based on memory |
| 2 | Closely resembles known prior work; differentiation unclear |
| 1 | Effectively reproduces existing published method |

Note: score 3 (unsearched) is a ceiling — cannot score higher without a search.

---

## Dimension 3: Feasibility

Can this be implemented and tested with standard academic resources?

| Score | Anchor |
|---|---|
| 5 | Standard components, known frameworks, fits on ≤ 4 GPUs, public data |
| 4 | Mostly standard; one non-trivial engineering challenge |
| 3 | Significant engineering effort; may require 8–16 GPUs or dataset construction |
| 2 | Requires specialized infrastructure, proprietary data, or >100 GPU days |
| 1 | Requires unsolved sub-problem, unavailable data, or infeasible compute |

---

## Dimension 4: Evaluability

Can the idea be tested in a way that produces clear, convincing evidence?

| Score | Anchor |
|---|---|
| 5 | Standard benchmarks exist; metric directly measures the target property |
| 4 | Good benchmarks with minor adaptation; evidence chain is clear |
| 3 | Requires custom evaluation setup; interpretation may be indirect |
| 2 | Hard to isolate the mechanism; results are ambiguous about what is tested |
| 1 | No principled way to test whether the idea works |

---

## Dimension 5: Risk

How likely is this idea to fail despite correct implementation?

| Score | Anchor |
|---|---|
| 5 | Risk is low; failure modes are controllable or testable in early sanity checks |
| 4 | One moderate risk with a clear mitigation; failure is unlikely |
| 3 | 2–3 risks; at least one cannot be detected until late in Phase 6 |
| 2 | High probability of one critical failure; mitigation is unclear |
| 1 | Multiple critical failure modes; idea rests on untested assumptions |

---

## Decision Thresholds

| Total Score | Decision |
|---|---|
| 20–25 | `recommended` — prioritize for Phase 5 |
| 14–19 | `viable` — carry as alternative if recommended idea fails |
| 8–13 | `speculative` — hold pending novelty search or feasibility check |
| 5–7 | `rejected` — document reason and discard |

**Hard rejections** (regardless of total score):
- Causal fit score = 1: the idea does not address the problem
- Feasibility score = 1: cannot be done with available resources
- Novelty score = 1 (searched): effectively reproduces existing work

**Minimum for Phase 5 handoff**:
- At least 1 `recommended` idea, OR
- 2–3 `viable` ideas with a brief comparison note

Do NOT select a single winner. Phase 5 expects options.

---

## Comparison Matrix Template

```
| Idea ID | Title | Causal Fit | Novelty | Feasibility | Evaluability | Risk | Total | Decision |
|---------|-------|------------|---------|-------------|--------------|------|-------|----------|
| P4-IDEA-1 |     |            |         |             |              |      |       |          |
| P4-IDEA-2 |     |            |         |             |              |      |       |          |
```

Include a 1–2 sentence comparison note explaining tradeoffs between
`recommended` and `viable` ideas.
