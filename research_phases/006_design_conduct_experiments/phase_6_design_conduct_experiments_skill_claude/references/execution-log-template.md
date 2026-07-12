# Execution Log Template

Reference for Phase 6 SKILL.md Step 6.
Use one entry per completed or failed run. Never delete entries.

---

## Log Entry Format

```
═══════════════════════════════════════════════════════════
Run ID:       [R{YYYYMMDD}-{N:04d}]
Status:       [completed / failed / cancelled]
Experiment:   [main-comparison / ablation / sensitivity / efficiency / sanity]
Claim ID:     [C-N — from experiment-plan.md]
─────────────────────────────────────────────────────────
Config file:  [path to config file, or inline if small]
Dataset:      [dataset name + split]
Model:        [model name + checkpoint if fine-tuned]
─────────────────────────────────────────────────────────
Start time:   [YYYY-MM-DD HH:MM UTC]
End time:     [YYYY-MM-DD HH:MM UTC]
Duration:     [HH:MM]
Hardware:     [GPU model × count, RAM]
─────────────────────────────────────────────────────────
Key metrics:
  Validation: [metric name] = [value]
  Test:       [metric name] = [value]    ← only if validation is finalized
  Secondary:  [metric name] = [value]
─────────────────────────────────────────────────────────
Artifacts:
  Checkpoint: [path]
  Predictions: [path]
  TensorBoard/logs: [path]
─────────────────────────────────────────────────────────
Anomalies:  [anything unexpected during the run — loss spikes, OOM, NaN]
Notes:      [any deviation from the config, manual interventions]
═══════════════════════════════════════════════════════════
```

---

## Failed Run Entry

```
═══════════════════════════════════════════════════════════
Run ID:       [R{YYYYMMDD}-{N:04d}]
Status:       FAILED
─────────────────────────────────────────────────────────
Failure time: [YYYY-MM-DD HH:MM UTC]
Error type:   [OOM / NaN loss / assertion error / timeout / other]
Error message: [first 3 lines of the error traceback]
─────────────────────────────────────────────────────────
Steps completed before failure: [N steps / N epochs]
Partial results (if any): [checkpoint path if saved]
─────────────────────────────────────────────────────────
Root cause (diagnosed): [what caused the failure]
Fix applied: [config change or code fix — reference commit if applicable]
Follow-up run ID: [R{YYYYMMDD}-{M:04d} — the run that replaced this one]
═══════════════════════════════════════════════════════════
```

Do NOT delete failed run entries. They are part of the record.

---

## Sanity Check Log

Record before any main run. A main run must not start until both pass.

```
Sanity Check 1: Overfit on 10 examples
  Run ID:    [R{YYYYMMDD}-{N:04d}]
  Result:    [loss at step 0] → [loss at step 100]
  Expected:  loss decreases monotonically to near-zero
  Verdict:   PASS / FAIL
  Notes:     ...

Sanity Check 2: Single-sample inference
  Run ID:    [R{YYYYMMDD}-{N:04d}]
  Input:     [brief description of the sample]
  Output:    [model output]
  Expected:  non-trivial output with correct format
  Verdict:   PASS / FAIL
  Notes:     ...
```

---

## Reporting Protocol

- **Validation metric**: may be reported at any time
- **Test metric**: report ONLY after all validation tuning decisions are
  final — no going back to tune after seeing test results
- Mark test scores with `[FINAL]` in the log when reported

When all runs for a claim are complete:
```
Claim C-N — EVIDENCE COMPLETE
Runs included: [R001, R003, R005]
Aggregate result: [mean ± std of primary metric]
Verdict: [claim supported / partially supported / refuted]
```
