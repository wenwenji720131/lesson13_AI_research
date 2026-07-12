# Evidence and Saturation Guide

Used in SKILL.md Steps 5–6. Defines the evidence collection schema,
saturation query protocol, and classification rules.

---

## Section 1: Evidence Matrix Schema

The `evidence-matrix.md` file records all evidence collected for
each candidate. Use one row per evidence item.

### Column definitions

| Column | Content |
|---|---|
| `Candidate_ID` | ID from `candidate-register.md` (e.g., `C-001`) |
| `Evidence_type` | `explicit` / `observed` / `inferred` (see definitions below) |
| `Claim` | One sentence — what the evidence says about the gap |
| `Source` | Author (Year), paper title, venue |
| `Location` | Section / Table / Figure number |
| `URL` | DOI, arXiv, or ACL Anthology URL |
| `Status` | `supports` / `weakens` / `contradicts` / `neutral` |
| `Interpretation` | One sentence — what this means for the candidate's validity |

### Evidence type definitions

| Type | Definition | Use |
|---|---|---|
| `explicit` | Authors directly state the limitation or gap in their paper | Strongest support |
| `observed` | You measure or read a performance result that implies the gap | Strong support |
| `inferred` | You reason that the gap exists from indirect signals | Weakest — must be corroborated |

**Rule**: A candidate supported only by `inferred` evidence cannot be
classified as `open`. It requires at minimum one `explicit` or `observed`
piece of corroborating evidence.

### Minimum evidence requirement

Each surviving candidate must have at least **two independent** evidence
items from **different sources** before Step 6. Independent means:
- Different papers
- Different authors or research groups
- Different evidence types preferred (e.g., one `explicit` + one `observed`)

### `evidence-matrix.md` template

```markdown
# Evidence Matrix

| Candidate_ID | Evidence_type | Claim | Source | Location | URL | Status | Interpretation |
|---|---|---|---|---|---|---|---|
| C-001 | explicit | ... | Author et al. (2024), "Title", Venue | Sec 5.3 | https://... | supports | ... |
| C-001 | observed | ... | Author et al. (2023), "Title", Venue | Table 4 | https://... | supports | ... |
| C-002 | inferred | ... | Author et al. (2024), "Title", Venue | Sec 6 | https://... | weakens | ... |
```

---

## Section 2: Saturation Protocol

Saturation testing determines whether a candidate gap is genuinely open
or already addressed by existing work.

### Purpose

A gap candidate is "open" only if a thorough search for solutions
finds none. Saturation means: "we searched and found no adequate solution."
It does NOT mean "we could not find a paper." Absence of paper ≠ open gap.

### Query families

Run ALL four query families for each candidate. Record results.

#### Family 1 — Direct solution search

```
"<core problem> solution" OR "<core problem> method" AFTER:2022
"<core problem> <constraint>" AFTER:2022
"<problem keyword> addressed" OR "<problem keyword> resolved"
```

**Target**: Papers that directly claim to solve the problem.

#### Family 2 — Benchmark and evaluation search

```
"<problem> benchmark" OR "<problem> evaluation" OR "<problem> dataset"
"<problem> metric" OR "<problem> leaderboard"
```

**Target**: Whether a standard evaluation protocol exists.
If the benchmark does not exist, the gap may be an **evaluation gap** itself.

#### Family 3 — Survey and review search

```
"<topic area> survey" OR "<topic area> review" AFTER:2022
"<problem> open problems" OR "<problem> future directions"
"<method family> limitations" OR "<method family> challenges"
```

**Target**: Whether the community acknowledges the problem as open.
Survey papers that list the problem as future work are strong evidence.

#### Family 4 — Failure and limitation search

```
"<method> failure" OR "<method> fails" OR "<method> limitation"
"<method> cannot" OR "<method> breaks down"
"<method> adversarial" OR "<method> distribution shift" (if applicable)
```

**Target**: Papers that characterize when and why the method fails —
useful for root cause corroboration.

---

## Section 3: Saturation Classification

After running query families, classify each candidate.

### Classification labels

| Label | Definition | Required evidence |
|---|---|---|
| `open` | No adequate solution found after thorough search | Thorough search across all 4 families with no solution found; at least one source acknowledging the problem |
| `partially addressed` | Solutions exist but leave a meaningful residual gap | At least one paper addressing part of the problem + evidence of the residual |
| `occupied` | A published method already solves this problem adequately | At least one paper with benchmark results showing the problem is solved |
| `dead-end` | A fundamental blocking constraint makes the problem unsolvable or not worth pursuing | Evidence of a theoretical lower bound, resource impossibility, or domain consensus that the problem is abandoned |
| `inconclusive` | Evidence is insufficient to classify | Use when evidence is contradictory or sparse — triggers additional search, not rejection |

### Classification rules

**Rule 1 — No vacancy-by-absence**
Never classify a candidate as `open` solely because the search returned
few papers. Low search density could mean: new topic, poor keyword choice,
problem named differently. Investigate before concluding "open."

**Rule 2 — Dead-end requires positive evidence**
`dead-end` requires naming the blocking constraint with a citation.
Do not invent reasons why something cannot be done.

**Rule 3 — Partial ≠ open**
A `partially addressed` gap is a gap — but the research problem must be
reframed to target the residual, not the part already solved.

**Rule 4 — Reopen stale dead-ends only with successor technology**
If a prior dead-end existed because of constraint C, and new technology
T potentially removes C, reopen only if the evidence names both C and T.

### Saturation record format (in `candidate-register.md`)

```
Candidate_ID: C-001
Saturation status: open | partially addressed | occupied | dead-end | inconclusive
Search date: YYYY-MM-DD
Queries run: [list query strings used]
Closest solution found: [Paper title + why it does NOT solve the gap, or "none"]
Residual gap (if partially addressed): [What remains unsolved]
Classification rationale: [2–3 sentences]
```

---

## Section 4: Evidence Strength Assessment

When multiple candidates compete for inclusion in the final output,
use this rubric to rank by evidence strength.

| Score | Evidence profile |
|---|---|
| 5 | ≥2 explicit sources + saturation search found no solution + acknowledged in survey |
| 4 | 1 explicit + 1 observed + saturation found only partial solution |
| 3 | 1 explicit or 2 observed + saturation inconclusive |
| 2 | 1 observed + 1 inferred + no saturation completed |
| 1 | Only inferred evidence |

Candidates scoring 1–2 should be held in reserve; only score 3–5
candidates proceed to artifact writing in Step 7.
