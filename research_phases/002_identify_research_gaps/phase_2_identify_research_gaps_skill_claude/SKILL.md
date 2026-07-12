---
name: phase2-identify-research-gaps
description: >
  Systematically identify and validate research gaps for AI/CS research
  (Phase 2). Takes Phase 1 outputs (taxonomy, evolution chains, benchmark
  summary, problem pool) as primary input. Produces Research Gap Documents,
  Gap Matrix, Failure Analysis Report, and Candidate Research Questions.
  Use when the user wants to find research gaps, validate whether a problem
  is worth studying, or prepare for Phase 3. Triggers on: "识别研究空白",
  "找gap", "research gap", "what's missing in this field", "why do current
  methods fail", "is this worth studying".
  DO NOT use for: proposing solutions (Phase 4), designing experiments
  (Phase 6), writing papers (Phase 8), or standalone literature review
  (use phase1-literature-mapping instead).
user-invocable: true
argument-hint: "<topic_or_phase1_dir> [--mode discovery|validation|both] [--depth quick|standard|deep]"
---

# Phase 2: Identify Research Gaps

Identify a defensible unresolved problem — not a solution. Read
`references/deliverables-and-validation.md` before work and
`references/evidence-and-saturation.md` before screening candidates.

## Phase Boundary (Hard Limits)

This skill ends at Candidate Research Questions. These outputs are **forbidden**:

| Forbidden output | Belongs to |
|---|---|
| Algorithm or method designs | Phase 4 |
| Testable hypotheses with suggested methodology | Phase 3/4 |
| Large-scale baseline experiments | Phase 6 |
| "Improve accuracy by X%" framed as a gap | Not a research gap |
| Solution proposals or MVPs | Phase 4/5 |

If any output drifts toward solution design, stop and reframe as a question.

## Inputs

Preferred Phase 1 outputs (read all that exist):

| File | Used in |
|---|---|
| `taxonomy.md` | Steps 1–3 — method families and open nodes |
| `evolution_chains.md` | Steps 1–2 — open ends |
| `benchmark_summary.md` | Steps 1, 4 — blind spots and bottlenecks |
| `problem_pool.md` | Step 1 — initial candidates |
| `trend-analysis.md` | Step 1 — trend-based candidates |
| `papers_tiered.json` / `papers.csv` | Steps 2–4 — paper lookup |

If Phase 1 outputs are absent, request a paper corpus and note reduced
confidence throughout. Never treat a few papers as field-wide evidence.

## Arguments

- **--mode**: `discovery` (find gaps from Phase 1 map) | `validation`
  (validate 1–3 user-supplied candidates) | `both` (default)
- **--depth**: `quick` (Steps 1–4 + 7) | `standard` (all 7) |
  `deep` (all 7 + invoke `gap-to-topic` for top 3 candidates)

---

## Workflow

### Step 1: Build the Candidate Register

Create `candidate-register.md` from ALL Phase 1 sources:

1. **Problem pool entries** — import every High-severity entry from
   `problem_pool.md`; tag `source=problem_pool`
2. **Evolution open ends** — extract every `OPEN END` node from
   `evolution_chains.md`; tag `source=evolution_open_end`
3. **Taxonomy open nodes** — extract problem nodes with no satisfactory
   method family; tag `source=taxonomy_open_node`
4. **Benchmark blind spots** — extract "Missing coverage" from
   `benchmark_summary.md`; tag `source=benchmark_blind_spot`
5. **Trend signals** — extract shrinking-but-unsolved directions from
   `trend-analysis.md`; tag `source=trend`

For each candidate record: affected method family, task setting, and
suspected failure mechanism. Keep rejected candidates with rejection reason.

A broad statement like "LLMs hallucinate" must be decomposed by task,
setting, and failure mechanism before it enters the register.

---

### Step 2: Method Limitation and Comparative Analysis

Load `references/gap-classification-guide.md`.

#### 2a. Method Limitation Analysis

For each Method Family in `taxonomy.md`, assess limitations across four
dimensions and record evidence:

| Dimension | Key question | Evidence required |
|---|---|---|
| **Performance** | What accuracy ceiling does this method hit, and why? | Benchmark number + citation |
| **Efficiency** | What compute/latency cost prevents deployment? | Measured cost or author statement |
| **Generalization** | In what OOD conditions does performance degrade? | Benchmark or ablation result |
| **Robustness** | What inputs/environments cause catastrophic failure? | Failure case or adversarial result |

Add new limitations not already in the register with `source=method_limitation`.

#### 2b. Comparative Analysis

Build a comparison table for each Problem Category:

```markdown
| Method | Core Idea | Strength | Weakness | Gap exposed |
|---|---|---|---|---|
```

"Gap exposed" = one sentence stating the unsolved problem the weakness
reveals. Add new candidates with `source=comparative_analysis`.

Also flag **conflicting findings**: where two papers report contradictory
results on the same benchmark. Contradictions are strong gap signals.

---

### Step 3: Failure Case Analysis

Load `references/failure-analysis-guide.md`. This step is often the most
productive — many top-tier papers originate from a precise answer to
"when exactly does this model fail, and why?"

For each major Method Family, execute the failure analysis pipeline:

```
Identified method
      ↓
Failure scenarios (conditions where it breaks)
      ↓
Failure mode classification (distribution-shift / long-tail /
  compositional / adversarial / temporal / scale / resource /
  annotation / cross-domain / theory-gap / evaluation)
      ↓
Root cause analysis (why does it fail at a fundamental level?)
      ↓
Research problem formulation (question form — NO solution)
```

Required output in `failure-analysis.md`:
- Failure scenario with evidence locator (paper, section, table/figure)
- Evidence type: `explicit` | `observed` | `inferred`
- Failure mode label
- Root cause statement (grounded in evidence, not inferred)
- Research problem as a question
- Sample size or qualitative prevalence

Add new candidates with `source=failure_analysis`.

---

### Step 4: Performance Bottleneck and Theoretical/Application Gap Discovery

#### 4a. Benchmark Bottleneck

From `benchmark_summary.md`, for each benchmark where SOTA is below
a meaningful threshold:
- Identify which error categories account for the remaining gap
- For saturated benchmarks: "solved" vs "benchmark no longer discriminates"
  — the latter is an **evaluation gap**

Error analysis framing:
```
Wrong predictions → error category distribution → dominant category → research problem
```

#### 4b. Theoretical Gaps

Look for: a method works empirically but has no theoretical explanation;
theory explains A but not B; two theoretical results contradict each other
in practice. Record: phenomenon, what existing theory cannot explain,
and evidence. Tag `source=theoretical`.

#### 4c. Application Gaps

Look for: strong lab results that cannot be deployed due to privacy,
latency, annotation cost, or regulation; real-world user populations not
covered by existing evaluations. Record: lab achievement, deployment
blocker, why current methods do not address it. Tag `source=application`.

---

### Step 5: Assemble Evidence Chains

For every candidate still in the register, collect independent evidence
from at least two sources using schemas in
`references/evidence-and-saturation.md`:

1. An explicit limitation, section quote, or theory contradiction
2. A benchmark result, failure case, or deployment constraint
3. A survey or recent paper showing the issue remains material

Populate `evidence-matrix.md`. Distinguish `explicit`, `observed`, and
`inferred` evidence. An `inferred`-only entry cannot be the sole support
for a gap.

---

### Step 6: Saturation Test

For each candidate, run the query families from
`references/evidence-and-saturation.md` and classify as:
`open` | `partially addressed` | `occupied` | `dead-end` | `inconclusive`

Rules:
- Never call a candidate `open` because the corpus lacks a paper
- `dead-end` requires evidence of a fundamental blocking constraint;
  do not invent the blocker
- Reopen a stale dead-end only when evidence names both the old blocker
  and a credible successor technology

---

### Step 7: Score, Write Artifacts, and Validate

#### 7a. Score Each Candidate

Use `references/deliverables-and-validation.md` score anchors. For each
surviving candidate score all four dimensions (1–5) and write an
uncertainty note for any score below high confidence:

| Dimension | 1 | 3 | 5 |
|---|---|---|---|
| Importance | Narrow inconvenience | Meaningful field limitation | Blocks a high-value capability |
| Novelty | Directly solved | Partial overlap | Bounded and unaddressed after screening |
| Feasibility | Resources unavailable | Plausible with constraints | Data/expertise/access available |
| Evaluability | No credible outcome | Partial benchmark | Clear measurable outcome exists |

For `--depth deep`, invoke `gap-to-topic` for adversarial 3-gate
validation of top 3 candidates.

#### 7b. Write Artifacts

Create all five artifacts in `research-gap-analysis-YYYYMMDD-<slug>/`:

```text
research-gap-document.md    ← one section per validated candidate
gap-matrix.csv              ← structured scoring table
failure-analysis.md         ← from Step 3 (finalized)
candidate-rqs.md            ← neutral research questions
phase2-validation.md        ← checklist + Phase 3 handoff
```

**Research Gap Statement** — exact form required in `research-gap-document.md`:
```
Existing <methods> address <problem X>.
However, they remain limited by <specific limitation Y>.
This limitation is material in <scenario Z>.
Evidence from <sources> indicates the bounded problem is <open|partially addressed>.
```

**Candidate Research Question** — exact form in `candidate-rqs.md`:
```
RQ<n>: Under what conditions, and for what reason, do <existing methods>
fail to achieve <required capability> in <scenario Z>?
```

Do NOT write "How can we design/build/propose..." — Phase 3 does that.

#### 7c. Validate and Hand Off

Complete `phase2-validation.md` per `references/deliverables-and-validation.md`
checklist (7 checks). A candidate is validated only when checks 1–5 pass
AND checks 6–7 (boundary and handoff) pass. Promote only validated
candidates to Phase 3.

---

## Output Package

```
research-gap-analysis-YYYYMMDD-<slug>/
  candidate-register.md       ← Step 1 working list
  evidence-matrix.md          ← Step 5
  failure-analysis.md         ← Step 3 (Deliverable 3)
  research-gap-document.md    ← Deliverable 1
  gap-matrix.csv              ← Deliverable 2
  candidate-rqs.md            ← Deliverable 4
  phase2-validation.md        ← exit validation + Phase 3 handoff
```

---

## Skill Linkage

- **Upstream**: `phase1-literature-mapping` → provides `taxonomy.md`,
  `evolution_chains.md`, `benchmark_summary.md`, `problem_pool.md`
- **Downstream**: `phase3-formulate-research-question` → receives
  `candidate-rqs.md` and `research-gap-document.md`
- **Support tools**:
  - `gap-to-topic` — adversarial retrieval and dead-end reasoning only
    (`--depth deep`); ignore its DOCX generator and `research-hub` commands
  - `research-gap-finder` — limitation-category reference only; ignore
    its Phase 3 hypothesis generation and methodology suggestions
  - `ccf-literature-searcher` — targeted saturation search in Step 6
