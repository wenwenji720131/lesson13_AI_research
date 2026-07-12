# Deliverables and Validation Guide

Used in SKILL.md Step 7. Defines the required artifacts, scoring anchors,
validation checklist, and Phase 3 handoff criteria.

---

## Section 1: Required Artifacts

All five files must be created in `research-gap-analysis-YYYYMMDD-<slug>/`.

### Artifact 1: `research-gap-document.md`

One section per validated gap candidate. Each section must contain:

1. **Gap ID and title** — e.g., `GAP-001: Multi-hop reasoning failure in RAG`
2. **Research Gap Statement** — exact 4-sentence form (see Section 3)
3. **Supporting evidence summary** — brief reference to evidence-matrix entries
4. **Saturation status** — open / partially addressed, with date
5. **Score summary** — four dimension scores + composite

Do NOT include solution proposals or methodology suggestions.

### Artifact 2: `gap-matrix.csv`

Structured scoring table with one row per candidate.

Required columns:
```
Candidate_ID, Title, Source, Failure_Mode, Importance(1-5),
Novelty(1-5), Feasibility(1-5), Evaluability(1-5), Composite,
Saturation_Status, Promoted_to_Phase3
```

`Composite` = mean of four dimension scores, rounded to one decimal.
`Promoted_to_Phase3` = `yes` / `no` / `conditional`.

### Artifact 3: `failure-analysis.md`

Finalized output from Step 3. Must follow the output schema in
`failure-analysis-guide.md`. Do not modify the schema.

### Artifact 4: `candidate-rqs.md`

One Candidate Research Question per validated gap.

Required format (see Section 4 for exact form):
- One RQ per line block, numbered `RQ1`, `RQ2`, ...
- Each RQ includes: question text, gap traceability, saturation status

### Artifact 5: `phase2-validation.md`

Validation checklist (see Section 5) with pass/fail for each check,
plus Phase 3 handoff block.

---

## Section 2: Scoring Anchors

Score each surviving candidate on four dimensions (1–5).

### Dimension 1: Importance

> Does solving this gap unlock a high-value capability or remove a
> material bottleneck?

| Score | Anchor |
|---|---|
| 1 | Narrow inconvenience; affects only edge cases or paper-writing hygiene |
| 2 | Useful improvement but not blocking any current application |
| 3 | Meaningful field limitation; removing it would advance several applications |
| 4 | Blocks a concrete deployment or downstream research direction |
| 5 | Blocks a high-value, clearly named capability that cannot be approximated |

### Dimension 2: Novelty

> Is this gap genuinely unaddressed, or are there close solutions?

| Score | Anchor |
|---|---|
| 1 | Directly and adequately solved by an existing method |
| 2 | Substantially addressed; only minor residual gap |
| 3 | Partially addressed; a meaningful portion of the gap remains |
| 4 | Closely related work exists but does not address the specific bounded gap |
| 5 | Bounded and unaddressed after full saturation search |

### Dimension 3: Feasibility

> Is there a plausible path to investigate this within 12–18 months?

| Score | Anchor |
|---|---|
| 1 | Required data, compute, or expertise is unavailable and unlikely to become available |
| 2 | Significant resource barriers; would need large collaboration or grant |
| 3 | Plausible with constraints; some resources available, others need to be acquired |
| 4 | Feasible with standard resources; data and expertise accessible |
| 5 | Highly feasible; data, compute, expertise, and access all available |

### Dimension 4: Evaluability

> Can progress on this gap be measured with a credible outcome signal?

| Score | Anchor |
|---|---|
| 1 | No credible outcome measure exists; progress cannot be quantified |
| 2 | Proxy metric only; does not directly measure the gap |
| 3 | Existing benchmark partially captures the gap; a new sub-task could extend it |
| 4 | Existing benchmark captures the gap with known limitations |
| 5 | Clear, measurable outcome exists; standard benchmark or well-defined evaluation protocol |

### Composite and promotion threshold

```
Composite = (Importance + Novelty + Feasibility + Evaluability) / 4
```

| Composite | Decision |
|---|---|
| ≥ 4.0 | Promote to Phase 3 |
| 3.0–3.9 | Conditional — address stated uncertainty before promoting |
| < 3.0 | Hold; do not promote unless evidence strengthens |

**Note**: Write an uncertainty note for any dimension score below 3,
explaining what information would change the score. Low scores are not
disqualifying by themselves — they are signals to address.

---

## Section 3: Research Gap Statement Format

Every entry in `research-gap-document.md` must use this exact 4-sentence form.

```
Existing <methods / method family> address <problem X>.
However, they remain limited by <specific limitation Y>.
This limitation is material in <scenario Z>.
Evidence from <sources> indicates the bounded problem is <open | partially addressed>.
```

### Rules

- `<methods>` — name the specific method family, not "AI" or "deep learning"
- `<limitation Y>` — must be bounded and specific (see gap-classification-guide.md)
- `<scenario Z>` — name the condition, dataset, task, or deployment context
- `<sources>` — cite at least two sources from the evidence matrix
- The fourth sentence must state the saturation status with date

### Anti-patterns to reject

| Anti-pattern | Why rejected |
|---|---|
| "X is not well studied" | Not bounded; could mean anything |
| "Accuracy could be improved" | Every method has this; not a gap |
| "Future work suggests..." | Paraphrase of authors' hedging, not evidence of a gap |
| "We propose to..." | Solution proposal — Phase 2 boundary violation |
| "No one has tried Y" | Absence of paper ≠ absence of solution |

---

## Section 4: Candidate Research Question Format

Every entry in `candidate-rqs.md` must use this exact form.

```
RQ<n>: Under what conditions, and for what reason, do <existing methods>
fail to achieve <required capability> in <scenario Z>?

Gap traceability: GAP-<n> → FA-<n> (if from failure analysis) → root cause
Saturation status: open | partially addressed (as of YYYY-MM-DD)
```

### Rules

**Rule 1 — Question or need form only**
- Allowed: "Under what conditions...", "What mechanism explains...", "A method is needed that achieves P without requiring Q."
- Forbidden: "How can we design...", "We will build...", "The solution is..."

**Rule 2 — Bounded**
Name the method, the capability, and the scenario. Generic questions
like "Why do LLMs hallucinate?" are not allowed.

**Rule 3 — Traceable**
Every RQ must reference the gap ID and, where applicable, the failure
analysis entry that grounds it.

**Rule 4 — No methodology suggestions**
The RQ asks a question; it does not suggest experiments, architectures,
or techniques. Those belong to Phase 3 and Phase 4.

---

## Section 5: Validation Checklist (7 Checks)

Complete this checklist in `phase2-validation.md` before promoting any
candidate to Phase 3. A candidate is validated only when checks 1–7 all pass.

### Check 1 — Gap is bounded

> Can you name the specific method family, the specific condition of failure,
> and the specific required capability that is not met?

Pass: Yes — all three named explicitly.
Fail: Gap statement is broad (e.g., "LLMs cannot reason well").

### Check 2 — Evidence is sufficient

> Does the gap have at least two independent evidence items (explicit or
> observed), and does the evidence-matrix record them with sources?

Pass: ≥2 independent items, both with citations.
Fail: Only inferred evidence, or only one source.

### Check 3 — Saturation is complete

> Were all four query families run? Was the closest solution found and
> documented? Is the gap classified as open or partially addressed (not occupied)?

Pass: Four families run, result documented, status is not `occupied`.
Fail: Search not completed, or status is `occupied`.

### Check 4 — Research problem is in question form

> Does the RQ use the required form and avoid solution proposals?

Pass: Follows Section 4 format; no solution language.
Fail: Contains "we will", "we propose", "the approach is", or similar.

### Check 5 — Scores are justified

> Does each dimension score ≥3 have at least one sentence of evidence?
> Does each score < 3 have an uncertainty note?

Pass: All scores documented.
Fail: Bare scores with no justification.

### Check 6 — Phase boundary observed

> Does the output contain any forbidden content: algorithm designs,
> methodology suggestions, hypothesis framing, or experiment proposals?

Pass: No forbidden content found.
Fail: Any output from the forbidden list in SKILL.md is present.

### Check 7 — Phase 3 handoff ready

> Are `candidate-rqs.md` and `research-gap-document.md` complete, consistent,
> and cross-referenced? Can a Phase 3 agent start from these two files alone?

Pass: Both files exist, RQs reference gap IDs, gaps reference evidence.
Fail: Files are incomplete, inconsistent, or not cross-referenced.

---

## Section 6: Phase 3 Handoff Block

Include this block at the end of `phase2-validation.md`.

```markdown
## Phase 3 Handoff

Primary inputs for Phase 3:
- `candidate-rqs.md` — validated research questions
- `research-gap-document.md` — gap evidence and context

Promoted candidates:
| RQ | Gap ID | Composite Score | Saturation | Note |
|---|---|---|---|---|
| RQ1 | GAP-001 | 4.2 | open | ... |

Conditional candidates (address before Phase 3):
| RQ | Gap ID | Blocking issue |
|---|---|---|
| RQ2 | GAP-003 | Feasibility score 2 — GPU cluster access not confirmed |

Excluded candidates (reason):
| Candidate | Reason |
|---|---|
| C-005 | Occupied — addressed by [Paper] (2024) |
```
