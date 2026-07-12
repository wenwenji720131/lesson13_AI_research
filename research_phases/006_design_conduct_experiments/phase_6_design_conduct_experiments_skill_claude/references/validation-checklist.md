# Validation Checklist

Reference for Phase 6 SKILL.md Step 8.
Run all 7 checks before handing off to Phase 7.

---

## Check 1: All Claims Covered

**Question**: Does every claim from `experiment-plan.md` have corresponding
evidence?

**Pass condition**:
- Every Claim ID has a status: `evidence-complete` / `TBD` / `refuted`
- No claim is `TBD` (pending) at handoff time
- Evidence is a real result, not a planned experiment

**Fail signals**:
- Any claim has status `TBD`
- A contribution claim from Phase 5 has no corresponding experiment

**Action if fail**: Run missing experiments or remove the corresponding claim.

---

## Check 2: Baselines Are Competitive

**Question**: Are the baselines state-of-the-art and fairly compared?

**Pass condition**:
- Every baseline uses the best-known hyperparameters for this setting
- Baselines were given comparable compute budget
- No published method that outperforms all baselines was excluded

**Fail signals**:
- A well-known strong baseline for this task is absent
- Baselines were tuned on fewer trials than the proposed method
- Baseline implementation is known to underperform the original paper

**Action if fail**: Add missing baselines or retune existing ones.

---

## Check 3: Ablations Complete

**Question**: Does the ablation study cover every key design decision?

**Pass condition**:
- Every component identified as "key" in Phase 5 methodology-document.md
  has a corresponding ablation variant
- The ablation table includes a variant replacing the core mechanism with
  the simplest baseline alternative

**Fail signals**:
- A key design decision has no ablation
- Ablations only test hyperparameter variations (not design decisions)

**Action if fail**: Add missing ablation runs.

---

## Check 4: No Test Set Leakage

**Question**: Were test set labels used for any tuning decision?

**Pass condition**:
- All hyperparameter decisions were made using validation set only
- Test evaluation was run exactly once per claim (after validation is final)
- No model selection was done based on test performance

**Fail signals**:
- Test metrics were reported at any intermediate tuning stage
- Model checkpoint selection used test metrics

**Action if fail**: Retrain and re-evaluate with a clean split protocol.
This is a critical integrity failure.

---

## Check 5: Failed Runs Recorded

**Question**: Is the record of failed and cancelled runs complete?

**Pass condition**:
- `run-manifest.csv` contains entries for every run, including failed/cancelled
- Every failed run has a root cause diagnosis and a follow-up run ID

**Fail signals**:
- Run IDs are non-sequential (suggests runs were deleted)
- No failed runs — unlikely for any non-trivial experiment suite

**Action if fail**: Reconstruct the run history from logs.

---

## Check 6: Reproducibility File Is Current

**Question**: Does `reproducibility.md` reflect the actual environment
used for the final runs?

**Pass condition**:
- All software versions, hardware specs, seeds, and data checksums are
  current (match the final runs)
- Any changes made after the initial setup are documented with a new entry

**Fail signals**:
- `reproducibility.md` was written at the start and not updated after
  environment changes (package upgrades, hardware migration)
- Seeds are missing for stochastic experiments

**Action if fail**: Update `reproducibility.md` to reflect actual conditions.

---

## Check 7: Result Values Are Raw

**Question**: Are all reported values raw measurements, not post-processed
selections?

**Pass condition**:
- Every number in `result-tables.md` traces to a run ID in `run-manifest.csv`
- Aggregate statistics (mean ± std) are computed from all runs, not cherry-picked
- No result was excluded without a documented, principled reason

**Fail signals**:
- A result is reported without a corresponding run ID
- The best run across multiple seeds is reported rather than the mean
- A run was excluded because it "didn't converge" but the non-convergence
  is not documented

**Action if fail**: Recompute from raw logs and document exclusion decisions.

---

## Phase 7 Handoff Statement

After all 7 checks pass, add this block to `experiment-integrity-check.md`:

```
Phase 6 Validation — [Date]
Checks passed: [list check numbers]
Checks failed: [list check numbers and blocking reason, if any]

Handoff to Phase 7:
  result-tables.md: [path]
  experiment-log.md: [path]
  failure-analysis.md: [path]
  reproducibility.md: [path]
  run-manifest.csv: [path — N runs total, M failed]

Claims with complete evidence: [list C-N]
Claims that were refuted: [list C-N with brief note]
Claims still pending: NONE (or list with explanation)

This experiment suite is ready for Phase 7 analysis.
```
