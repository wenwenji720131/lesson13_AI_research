# Experiment Design Guide

Reference for Phase 6 SKILL.md Steps 1, 4, and 5.

---

## Section 1: Hypothesis and Claim Mapping

Every experiment must exist to test a specific claim. An experiment without
a claim is a fishing expedition; a claim without an experiment is speculation.

### Claim Types and Their Experiments

| Claim type | Required experiment | Primary signal |
|---|---|---|
| Performance | Main comparison vs. baselines | Primary metric on test set |
| Efficiency | Benchmark latency, FLOPs, memory | Wall-clock time, peak GPU RAM |
| Generalization | Evaluate on OOD datasets | Performance gap train↔OOD |
| Mechanism | Ablation removing the component | Performance drop |
| Robustness | Sensitivity to hyperparameter k | Variance in metric |

### Claim-to-Experiment Mapping Format

```
Claim ID: C-N
Claim text: [exact claim from methodology-document.md]
Type: performance / efficiency / generalization / mechanism / robustness
Hypothesis: [falsifiable form — "Model A achieves X > Y on dataset D"]
Required experiment: [experiment type and dataset]
Stopping rule: [when to stop — n epochs / reaching criterion / fixed budget]
Failure mode: [what result would falsify this claim]
Risk reference: [Risk-N from phase5 risk-analysis.md]
```

### What Makes a Hypothesis Falsifiable

A hypothesis is falsifiable if:
1. It specifies a direction (better than, equal to, at least X%)
2. It specifies the comparison (against which baseline, on which dataset)
3. It specifies the metric
4. A single experiment can produce a result that contradicts it

"The method performs well" is not falsifiable.
"The method achieves BLEU > 35 on WMT14 En-De with comparable FLOPs
to the Transformer base" is falsifiable.

---

## Section 2: Baseline Execution Standards

Baselines are the most common source of unfair comparisons in AI papers.
The following standards prevent the most common failure modes.

### Implementation Priority

1. **Use the original authors' code** — if publicly available, always prefer
   this. Document the commit hash or version.
2. **Use a well-maintained framework reimplementation** — document the
   library, version, and any changes made.
3. **Reimplement** — document the implementation choices in `reproducibility.md`
   and note this is a reimplementation. Reimplementations may contain bugs.

### Hyperparameter Tuning Protocol

- Tune baselines on the validation set using the same number of trials
  as the proposed method (or document the budget used)
- Never tune baselines with access to test labels
- Use published hyperparameters from the original paper as the starting
  point; document any changes
- If the baseline has no published hyperparameters for this setting,
  document how you selected them

### Compute Budget Parity

Each baseline must receive comparable compute to the proposed method.
"Comparable" means:
- Same number of training epochs (adjusted for batch size)
- OR same total FLOPs
- OR same wall-clock time on the same hardware

Document which parity criterion was used. Deviations require justification.

### Baseline Result Recording Format

```
Baseline: [method name]
Citation: [paper + venue]
Implementation: [original-code / framework-builtin / reimplemented]
Code source: [URL + commit hash]
Hyperparameters: [key values used]
Tuning method: [grid / random / published defaults / manual]
Validation score: [metric value — used for tuning]
Test score: [metric value — held until all baselines are run]
Notes: [any known limitations of this run]
```

---

## Section 3: Full Experiment Suite Design

### Main Comparison

Purpose: show the proposed method outperforms baselines on the primary task.

Requirements:
- All baselines must be included in the same table
- All datasets claimed in contributions must be tested
- Statistical significance: report mean ± std across ≥ 3 runs for
  stochastic methods
- Do not report test results until validation tuning is complete

### Ablation Study

Purpose: show that each design decision is individually necessary.

Design rules:
- One change per ablation — do not combine changes
- Compare against the full proposed model (not against each other)
- Include a variant that replaces the core mechanism with the simplest
  possible baseline alternative
- Report on the same datasets as the main comparison

Ablation table format:
```
| Variant        | Component changed | Dataset-1 | Dataset-2 | Δ vs. full |
|----------------|-------------------|-----------|-----------|------------|
| Full model     | —                 |           |           | —          |
| w/o [A]        | remove module A   |           |           |            |
| w/o [B]        | replace mech B    |           |           |            |
```

### Sensitivity Analysis

Purpose: show that performance is stable across reasonable hyperparameter
settings.

Select 1–2 key hyperparameters (those introduced by the proposed method,
not shared with baselines). Vary each over 4–6 values around the chosen
setting. Report primary metric vs. hyperparameter value as a line plot.

A method is robust if performance degrades gracefully rather than
collapsing at nearby values.

### Efficiency Analysis

Required if ANY efficiency claim is made (latency, memory, FLOPs).

| Metric | How to measure | What to report |
|---|---|---|
| Wall-clock time | Time a fixed number of forward passes | ms/sample or samples/sec |
| Peak GPU memory | torch.cuda.max_memory_allocated() | GB |
| FLOPs | thop or fvcore | GFLOPs per sample |

Report efficiency on the same hardware for all methods. Measurements on
different hardware cannot be compared.

### Failure Case Analysis

Purpose: document where the method fails to inform limitations (Phase 7/8).

Collect 3–5 examples where the proposed method produces incorrect or
poor output. For each, note:
- Whether the same input also fails for baselines (shared failure) or
  is specific to the proposed method (targeted failure)
- Whether the failure is isolated or systematic

Systematic failures must be reported as limitations.
