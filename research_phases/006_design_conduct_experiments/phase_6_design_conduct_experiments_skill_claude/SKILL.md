---
name: phase6-design-conduct-experiments
description: >
  Design and execute a rigorous experiment suite to validate a frozen
  methodology (Phase 6). Takes Phase 5 output (methodology documents,
  evaluation plan) as primary input. Produces Hypothesis Map, Experiment Plan,
  Reproducibility Record, Run Manifest, Experiment Log, Result Tables, and
  Integrity Check. Use when the user wants to map claims to experiments,
  design ablations, set up baselines, log runs, or audit result integrity.
  Triggers on: "设计实验", "实验方案", "experiment design", "run experiments",
  "ablation study", "baseline comparison", "实验结果记录".
  DO NOT use for: designing the methodology (Phase 5), interpreting results
  scientifically (Phase 7), writing the paper (Phase 8).
user-invocable: true
argument-hint: "<methodology_dir_or_phase5_dir> [--mode design|execute|analyze|all] [--depth quick|standard|deep]"
---

# Phase 6: Design and Conduct Experiments

Design claim-driven, reproducible experiments from a frozen methodology.
The core principle is: **Hypothesis → Experiment → Evidence → Conclusion**.
Every experiment must exist to test a specific claim.

## Phase Boundary (Hard Limits)

| Forbidden output | Belongs to |
|---|---|
| Modifying the core methodology design | Phase 5 |
| Scientific interpretation of results | Phase 7 |
| Drawing paper-level conclusions | Phase 7/8 |
| Writing paper sections | Phase 8 |
| Inventing or adjusting result values | Never |
| Stopping unfavorable runs without recording them | Never |

Phase 6 asks: "Does the method work, and under what conditions?"
Phase 7 asks: "What do these results mean scientifically?"

## Inputs

| File | Used in |
|---|---|
| Phase 5 `methodology-document.md` | All steps — method specification |
| Phase 5 `evaluation-plan.md` | Steps 1, 4–5 — baselines and metrics |
| Phase 5 `algorithm-spec.md` | Steps 2–3 — implementation reference |
| Phase 5 `risk-analysis.md` | Step 1 — failure modes to test |
| Phase 3 `candidate-rqs.md` | Step 1 — hypothesis alignment |

## Arguments

- **--mode**: `design` (Steps 1–3) | `execute` (Steps 4–6) | `analyze` (Steps 7–8) | `all`
- **--depth**: `quick` (core comparison + 1 ablation) | `standard` | `deep` (+ sensitivity + generalization)

---

## Workflow

### Step 1: Hypothesis and Claim Mapping

Convert the methodology claims into testable hypotheses.

Load `references/experiment-design-guide.md` Section 1.

For each claim in the methodology:
```
Claim ID: [C-N]
Claim: [exact statement from methodology-document.md]
Type: performance / efficiency / generalization / mechanism
Hypothesis: [falsifiable version — "Method X achieves Y > baseline Z on dataset D"]
Required evidence: [what experiment produces this evidence]
Failure mode: [what result would falsify the claim]
Risk (from Phase 5): [referenced risk from risk-analysis.md]
```

Every experiment in subsequent steps must trace back to a Claim ID.
Do not add experiments that don't test a specific claim.

---

### Step 2: Reproducibility Setup

Record the full environment before any run begins.

Produce `reproducibility.md`:
```
Hardware: [GPU model, memory, count]
Software: [framework + version, CUDA, key libraries with pinned versions]
OS: [OS version]
Seeds: [list of random seeds used]
Data provenance: [source URLs, download date, checksums if available]
Data licenses: [license and usage constraints]
Train/val/test split: [split sizes and split method]
Leakage safeguards: [how test set contamination was prevented]
```

This file is immutable once experiments begin. Changes require a new entry.

---

### Step 3: Run Manifest

Create `run-manifest.csv` before executing any run.

Required columns:
```
run_id | config_path | experiment_type | claim_id | dataset | baseline |
compute_budget | status | raw_result_path | notes
```

- `run_id`: immutable, format `R{YYYYMMDD}-{N:04d}`
- `status`: planned / running / completed / failed / cancelled
- Failed and cancelled runs must remain in the manifest — do not delete them

Run sanity checks first:
- Overfit on 10 examples → loss decreases: confirms training pipeline works
- Inference on one sample → non-trivial output: confirms eval pipeline works

Do NOT start main runs until sanity checks pass.

---

### Step 4: Baseline Execution

Run all baselines under fair conditions.

Load `references/experiment-design-guide.md` Section 2.

Fairness requirements:
- Equal compute budget to the proposed method (same epochs or FLOPs)
- Use published hyperparameters from original papers where available
- If tuning is needed: tune on validation set only, no test access
- Implement from original code if available; document any deviations

For each baseline:
```
Baseline: [method name and citation]
Implementation source: [original code / reimplemented / framework built-in]
Hyperparameters: [values used and their source]
Validation score: [used for tuning]
Test score: [held until comparison]
```

---

### Step 5: Full Experiment Suite

Run experiments in this order: main comparison → ablation → sensitivity →
efficiency → generalization (add only if the claim exists).

Load `references/experiment-design-guide.md` Section 3.

**Main comparison**: proposed method vs. all baselines on all primary datasets.

**Ablation** (required — tests whether design decisions are necessary):
```
Ablation ID: [A-N]
Component removed/replaced: [exactly what changes]
Hypothesis: [what this tests]
Expected direction: [proposed > ablated? why?]
```
Every key design decision from Phase 5 must have an ablation.

**Sensitivity**: vary 1–2 key hyperparameters around the chosen value.
Report performance vs. hyperparameter value. Documents robustness.

**Efficiency**: wall-clock time, peak GPU memory, FLOPs vs. baselines.
Required if Phase 5 makes any efficiency claim.

**Failure cases**: document 3–5 examples where the method fails.
Required before Phase 7.

---

### Step 6: Execution Logging

Log every run in `experiment-log.md`.

For each completed run:
```
Run ID: [from manifest]
Start time / End time:
Config: [config file path or inline if small]
Key metrics: [validation and test values]
Artifacts: [checkpoint path, prediction files]
Anomalies: [anything unexpected during the run]
```

Rules:
- Never delete or overwrite a log entry
- Failed runs get a "FAILED" entry with the error message
- Do not report test metrics until all validation decisions are finalized

---

### Step 7: Failure Case Analysis

Before finalizing results, analyze where the method fails.

For 3–5 failure examples:
```
Example ID: [from dataset]
Input: [brief description or sample]
Prediction: [model output]
Ground truth: [correct output]
Failure type: [distributional / edge case / ambiguous / systematic]
Hypothesis for failure: [why this happened]
Frequency estimate: [isolated / common / systematic]
```

Systematic failures must be noted in limitations (Phase 7/8).

---

### Step 8: Result Validation

Audit results before handing off to Phase 7.

Load `references/validation-checklist.md`.

Produce `experiment-integrity-check.md`:
```
Check 1 — All claims covered: [list claim IDs and their evidence status]
Check 2 — Baselines are competitive: [confirm no strawman]
Check 3 — Ablations complete: [every Phase 5 decision tested]
Check 4 — No test leakage: [confirm split protocol]
Check 5 — Failed runs recorded: [count of failed/cancelled runs]
Check 6 — Reproducibility file current: [confirm no unlogged changes]
Check 7 — Result values are raw (not post-processed or selected): [confirm]
```

Phase 6 is complete only when all 7 checks pass.

---

## Output Package

```
phase6-experiments-YYYYMMDD-<slug>/
  experiment-plan.md          ← Step 1 (hypothesis-claim mapping)
  reproducibility.md          ← Step 2 (environment record)
  run-manifest.csv            ← Step 3 (all runs, including failed)
  experiment-log.md           ← Step 6 (per-run logs)
  result-tables.md            ← Steps 4–5 (main results, ablations, efficiency)
  failure-analysis.md         ← Step 7 (failure cases)
  experiment-integrity-check.md ← Step 8 (validation + Phase 7 handoff)
```

`result-tables.md` uses `TBD` for planned but not yet run experiments.
It must never contain fabricated values.

---

## Skill Linkage

- **Upstream**: `phase5-refine-methodology` → provides `evaluation-plan.md` and `methodology-document.md`
- **Downstream**: `phase7-analyze-results` → receives `result-tables.md`, `experiment-log.md`, `failure-analysis.md`
- **Support tools**:
  - `ccf-experiment-designer` — for extending the experiment plan (Step 5)
