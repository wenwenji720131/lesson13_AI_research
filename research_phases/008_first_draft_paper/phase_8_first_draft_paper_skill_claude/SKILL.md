---
name: phase8-write-paper-draft
description: >
  Write a complete, evidence-backed first draft of an AI/CS paper from
  validated research artifacts (Phase 8). Takes Phase 5 methodology, Phase 6
  results, and Phase 7 analyses as input. Produces Research Story, Claim-
  Evidence Map, full paper sections, and a Submission Package. Use when the
  user wants to build the paper narrative, draft sections, connect figures to
  claims, or prepare a submission-ready draft. Triggers on: "写论文", "写paper",
  "paper writing", "draft paper", "write introduction", "write abstract",
  "投稿准备". DO NOT use for: running experiments (Phase 6), interpreting
  results (Phase 7), responding to peer review (Phase 9).
user-invocable: true
argument-hint: "<phase7_dir_or_results_dir> [--venue <venue_name>] [--depth quick|standard|deep]"
---

# Phase 8: Write Paper Draft

Transform validated research artifacts into a complete, evidence-backed paper
draft. Every claim in the draft must link to evidence produced in Phase 6/7.

## Phase Boundary (Hard Limits)

| Forbidden output | Belongs to |
|---|---|
| Running new experiments or re-running baselines | Phase 6 |
| Scientific interpretation of new results | Phase 7 |
| Inventing citations, results, or figures | Never |
| Responding to peer review or revision | Phase 9 |
| Claiming final readiness without validation checks | Phase 9 |

Phase 8 asks: "How do we tell this research story clearly and completely?"
Phase 9 asks: "Does the submitted paper hold up to scrutiny?"

## Inputs

| File | Used in |
|---|---|
| Phase 7 `interpretation-report.md` | Steps 1–2 — story and claims |
| Phase 6 `result-tables.md` | Steps 2, 5 — evidence for claims |
| Phase 6 `failure-analysis.md` | Step 3 (limitations section) |
| Phase 5 `methodology-document.md` | Steps 3–4 — method section |
| Phase 5 `algorithm-spec.md` | Step 4 — algorithm presentation |
| Phase 5 `theoretical-basis.md` | Step 4 — theoretical justification |
| Phase 2 `research-gap-document.md` | Steps 3 — introduction/related work |
| Phase 1 `taxonomy.md` | Step 3 — related work structure |
| Venue template | Step 6 — formatting constraints |

## Arguments

- **--venue**: target venue name for format and length constraints (e.g., `AAAI27`, `NeurIPS`, `ICML`)
- **--depth**: `quick` (Steps 1–3, 6) | `standard` (all 8 steps) | `deep` (all + extended logic audit)

---

## Workflow

### Step 1: Research Story Construction

Build the narrative spine before writing any section.

Load `references/paper-structure-guide.md` Section 1.

Produce `paper-story.md`:
```
Problem: [what is broken or missing — for practitioners or the field]
Gap: [why existing solutions fail — tied to Phase 2 root cause]
Method: [what we do differently — the core mechanism in one sentence]
Evidence: [what results we have and what they show]
Impact: [who benefits and how — claim scope]

Contribution 1: [specific, falsifiable claim] → Evidence: [table/figure ID]
Contribution 2: ...
Contribution 3: ...
```

Rules:
- Each contribution must link directly to evidence from Phase 6/7
- No contribution may appear in the paper if it has no linked evidence
- Mark missing evidence as `DATA_NEEDED` — do not fabricate

---

### Step 2: Claim-Evidence-Section Map

Assign every claim, figure, table, and citation to a paper section.

Produce `claim-evidence-section-map.md`:
```
| Claim | Evidence | Section | Figure/Table | Limitation noted? |
|-------|----------|---------|--------------|-------------------|
| ...   |          |         |              |                   |
```

- Every row in `result-tables.md` should appear in at least one row here
- Claims without evidence are `DATA_NEEDED` — do not draft that claim
- Limitations must reference `failure-analysis.md`

---

### Step 3: Paper Structure and Section Drafting

Draft each section in this order. Load `references/paper-structure-guide.md` Section 2
for the required elements of each section.

**Title**: precise, mentions the key mechanism or contribution. Avoid
vague words ("novel", "effective", "improved").

**Abstract** (venue word limit): problem → gap → method → result → impact.
One number per contribution. No citations.

**Introduction**: problem motivation → gap → limitations of prior work →
our approach (high level) → contribution list → paper organization.
Do NOT put the method details here.

**Related Work**: organize by subtopic, not by paper. For each subtopic:
what existing methods do, where they fall short, and how our work differs.

**Method**: reference the method sections from Phase 5. Structure:
Overview → Core Mechanism (with algorithm) → Training Strategy → Inference.

**Experiments**: setup → main results → ablation → efficiency →
analysis / qualitative. Every table and figure must have a body paragraph
explaining what it shows and why the result matters.

**Limitations**: honest, specific — based on `failure-analysis.md`.
Scope limitations and failure modes, not generic hedges.

**Conclusion**: brief restatement of contributions, main result, and
one forward-looking sentence. No new claims.

---

### Step 4: Algorithm and Figure Presentation

Convert Phase 5 artifacts into paper-ready format.

Load `references/paper-structure-guide.md` Section 3.

For each algorithm box:
- Include only the steps visible in the paper (hide implementation details)
- Inputs and outputs must match the text description

For each figure:
```
Figure [N]: [caption — describes what is shown and the key takeaway]
Data source: [experiment ID from run-manifest.csv]
Placement: [Section X, after paragraph Y]
Self-contained: [yes / no — missing labels, units, or baseline reference]
```

For each table:
```
Table [N]: [caption with metric names and dataset]
Columns: [method, dataset, primary metric ± std, secondary metric]
Bold convention: [best result per column / per row]
Baseline included: [yes — if no, justify]
```

---

### Step 5: Academic Writing and Style

Load `references/academic-writing-guide.md`.

Apply to the full draft:
- Precision: every claim quantified where possible ("+3.2% on X")
- Tense: past for experiments, present for general facts and claims
- Voice: active where possible, passive for describing results
- Hedging: use "suggests" / "indicates" for generalization claims;
  "demonstrates" / "shows" for direct results

Audit for:
- Overclaiming: "solves", "always", "significantly" without numbers
- Underclaiming: contribution buried or qualified to meaninglessness
- Circular reasoning: claim restated as its own evidence

---

### Step 6: Draft Validation

Run all 7 checks before calling the draft ready for submission.

Load `references/validation-checklist.md`.

Produce `draft-validation.md`:
```
Check 1 — Story completeness: problem → gap → method → evidence chain holds
Check 2 — Claim-evidence coverage: every claim has a data source
Check 3 — Figure/table completeness: captions, units, baselines present
Check 4 — Related work coverage: key baselines cited
Check 5 — Limitations section: failure modes from Phase 6 addressed
Check 6 — Format compliance: venue page limit, anonymization, template used
Check 7 — Bibliography: all keys exist and match citation text
```

Mark each check `pass` / `fail` / `DATA_NEEDED`.
A draft with any `fail` is NOT submission-ready.

---

### Step 7: Submission Materials

Prepare all files required for submission.

```
Submission checklist:
- Main paper PDF (compiled from venue template)
- Supplementary material (if applicable)
- Code and data release plan (if venue requires)
- Authorship confirmation
- Ethics statement (if venue requires)
- Anonymization: author names and institution references removed
```

Record compilation warnings and unresolved references in `draft-validation.md`.

---

### Step 8: Logic Chain Audit

Re-read the full draft for internal consistency.

For each section transition, verify:
```
Introduction → Method: gap stated in intro ↔ mechanism in method
Method → Experiments: design choices in method ↔ ablation targets in experiments
Experiments → Analysis: result values in tables ↔ numbers in body text
Analysis → Conclusion: conclusion claims ↔ evidence actually shown
```

Flag any disconnect as `LOGIC_GAP` in `draft-validation.md`.

---

## Output Package

```
phase8-paper-YYYYMMDD-<slug>/
  paper-story.md              ← Step 1 (narrative spine)
  claim-evidence-section-map.md ← Step 2 (claim→evidence→section links)
  manuscript/                 ← Step 3–7 (LaTeX or Markdown draft)
    main.tex (or main.md)
    figures/
    references.bib
  draft-validation.md         ← Step 6–8 (7 checks + logic audit)
```

`draft-validation.md` must state: "Draft is ready for Phase 9 review" or
list the checks that failed.

---

## Skill Linkage

- **Upstream**: `phase7-analyze-results` → provides `interpretation-report.md`
- **Downstream**: `phase9-revise-paper` → receives `manuscript/` and `draft-validation.md`
- **Support tools**:
  - Venue templates: `AAAI27_for_research/` or `AuthorKit27/` in repo root
  - `ccf-idea-optimizer` — for sharpening contribution framing in Step 1
