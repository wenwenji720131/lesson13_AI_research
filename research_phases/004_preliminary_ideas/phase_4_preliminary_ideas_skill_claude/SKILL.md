---
name: phase4-generate-research-ideas
description: >
  Systematically generate and screen candidate research ideas for AI/CS
  research (Phase 4). Takes Phase 3 output (validated RQ + gap) as primary
  input. Produces Mechanism Map, Idea Pool, Idea Proposals, Comparison Matrix,
  and Handoff document. Use when the user wants to explore methods, generate
  innovations, map solution spaces, or produce candidate ideas before
  methodology design. Triggers on: "生成想法", "idea generation", "研究思路",
  "how to address this gap", "solution exploration", "brainstorm methods".
  DO NOT use for: designing a final method (Phase 5), running experiments
  (Phase 6), writing the paper (Phase 8).
user-invocable: true
argument-hint: "<research_question_or_phase3_dir> [--mode explore|screen|both] [--depth quick|standard|deep]"
---

# Phase 4: Generate Research Ideas

Systematically explore solution space and generate candidate research ideas
from a validated research question and gap. Output is a set of CANDIDATE
ideas — not a final methodology or algorithm.

## Phase Boundary (Hard Limits)

| Forbidden output | Belongs to |
|---|---|
| Final method selection or design | Phase 5 |
| Algorithm pseudocode or loss functions | Phase 5 |
| Experiment design or execution | Phase 6 |
| Novelty claims stated as proven | Phase 5/7 |
| Pilot results or benchmarking | Phase 6 |
| Paper writing or contribution framing | Phase 8 |

Phase 4 asks: "What are the plausible approaches and why might each work?"
Phase 5 asks: "How exactly should the chosen approach be designed?"

## Inputs

| File | Used in |
|---|---|
| Phase 3 `candidate-rqs.md` | All steps — primary RQ and constraints |
| Phase 2 `research-gap-document.md` | Step 1 — gap structure and root cause |
| Phase 2 `gap-matrix.csv` | Step 1 — gap classification |
| Phase 1 `taxonomy.md` | Steps 2–3 — baseline methods and design space |

## Arguments

- **--mode**: `explore` (Steps 1–3) | `screen` (Steps 4–6) | `both` (all steps)
- **--depth**: `quick` (Steps 1, 5, 6) | `standard` (all 6 steps) | `deep` (all + extended validation)

---

## Workflow

### Step 1: Problem Mechanism Analysis

Before generating ideas, understand WHY the gap exists.

Load `references/idea-generation-guide.md` Section 1.

Produce a mechanism map:
```
Research Question: [from Phase 3]
Root cause of gap: [why existing methods fail — the causal mechanism]
Failure mode 1: [specific failure — e.g., "distributional shift breaks X"]
Failure mode 2: ...
Key assumptions the gap rests on: [what must change for the gap to be addressable]
Intervention points: [where in the pipeline or formulation change is possible]
```

Do not proceed to idea generation until the root cause is identified.
"Existing methods perform poorly" is not a root cause.

---

### Step 2: Innovation Source Exploration

Explore four or more lenses for where solutions could come from.

Load `references/idea-generation-guide.md` Section 2.

For each applicable lens, produce 1–3 candidate directions:

```
Lens: [Method Transfer / Method Combination / Mechanism Redesign /
       Problem Reformulation / Data or Benchmark Reframing / Theory-Driven]

Direction: [what the transferred/combined/redesigned approach would do]
Why this lens applies: [connection to the root cause from Step 1]
Key assumption: [what must hold for this to work]
Prior evidence: [papers that support this direction, if any]
```

At least 2 lenses must be explored. If only one lens applies, document why
the others were rejected.

---

### Step 3: Solution Space Exploration

Expand the candidate directions into 5–10 distinct idea sketches.

Each idea sketch (2–4 lines):
```
Idea [N]: [name]
Mechanism: [what it does differently from baseline]
Gap connection: [which failure mode it directly addresses]
Closest prior work: [most similar published method — searched or inferred]
```

Keep ideas conceptually distinct — variants of the same mechanism count as one.
Aim for diversity across lenses, not depth on one direction.

---

### Step 4: Conceptual Validation

Screen each idea for internal consistency before writing full proposals.

Load `references/idea-generation-guide.md` Section 3.

For each idea sketch, check:
```
Causal fit: Does the mechanism directly address the root cause? [yes/partial/no]
Internal consistency: Are the components compatible? [yes/no]
Feasibility boundary: Can this be done in a standard compute budget? [yes/risky/no]
Likely prior-art overlap: [unsearched / partial / searched — cite if searched]
Falsifying observation: [what single experiment would kill this idea]
```

Drop ideas that fail causal fit or internal consistency.
Keep at least 3 ideas with potential.

---

### Step 5: Full Idea Proposals

Write a structured proposal for each surviving idea.

Load `references/idea-proposal-template.md`.

Each proposal must include:
```
Idea ID: [P4-IDEA-N]
Title: [short name]
Target mechanism: [the specific failure mode this addresses]
Core innovation: [the new design choice, 2–3 sentences]
Why it addresses the gap: [causal argument — must be specific]
Assumptions: [what must hold for this to work]
Expected evidence: [what a positive result would look like]
Known risk: [the main way this could fail]
Closest work uncertainty: [novelty status: unsearched / partial / searched]
Estimated complexity: low / medium / high (for Phase 5 implementation)
```

Do NOT claim novelty is proven unless a literature search was done.
Do NOT write algorithms, loss functions, or training procedures here.

---

### Step 6: Idea Screening and Handoff

Compare ideas and select candidates for Phase 5.

Load `references/screening-rubric.md`.

Produce a comparison matrix:
```
| Idea | Causal Fit | Novelty | Feasibility | Evaluability | Risk |
|------|------------|---------|-------------|--------------|------|
| ...  |            |         |             |              |      |
```

Scoring: 1–5 per dimension. Document the reasoning, not just the score.

**Do NOT select a single winner.** Phase 5 expects 1–3 candidates.
Label each surviving idea: `recommended` / `viable` / `speculative`.

Rejected ideas go to `rejected-ideas.md` with one-line reason each.

---

## Output Package

```
phase4-ideas-YYYYMMDD-<slug>/
  mechanism-map.md          ← Step 1 (root cause analysis)
  idea-pool.md              ← Steps 2–3 (sketches and directions)
  idea-proposals.md         ← Step 5 (full proposals for survivors)
  idea-comparison-matrix.md ← Step 6 (scored comparison)
  rejected-ideas.md         ← Step 6 (rejected with reasons)
  phase4-handoff.md         ← Step 6 (recommended candidates for Phase 5)
```

`phase4-handoff.md` must list 1–3 ideas, their novelty status, and the
mechanism map. It must NOT declare a winner or include algorithm details.

---

## Skill Linkage

- **Upstream**: `phase3-formulate-research-hypotheses` → provides `candidate-rqs.md`
- **Downstream**: `phase5-refine-methodology` → receives `phase4-handoff.md`
- **Support tools**:
  - `research-gap-finder` — for validating gap connection in Step 1
  - `ccf-idea-reviewer` — for scoring individual ideas against CCF-A criteria
