---
name: phase-6-experiment-design-codex
description: Design and conduct claim-driven, reproducible AI or computer-science experiments from a frozen methodology. Use when Codex needs to map claims to datasets, baselines, metrics, ablations, robustness checks, run manifests, and result logs. Do not use to fabricate results or interpret final scientific conclusions.
---

# Phase 6 Experiments

Read `../README.md`. Require a Phase 5 method specification and claim-evidence map.

## Workflow

1. Create `experiment-plan.md` mapping every claim to a dataset, split, baseline, metric, control, expected failure mode, and stopping rule.
2. Record environment, software versions, hardware, seeds, data provenance, licenses, and leakage safeguards in `reproducibility.md`.
3. Build `run-manifest.csv` with immutable run IDs, config paths, budgets, status, and raw-result paths; run sanity checks before main runs.
4. Execute fairly: give comparable baselines equivalent budgets, tune without test leakage, preserve failed runs, and repeat stochastic runs where variance matters.
5. Require main comparison, ablation, robustness/sensitivity, efficiency, and failure-case evidence only when each supports a specific claim.
6. Produce `experiment-log.md`, raw result links, `result-tables.md` with real values or `TBD`, and `experiment-integrity-check.md`.

## Boundaries

Never invent values, normalize against model outputs, delete unfavorable results, or turn results into broad conclusions. Phase 7 owns scientific interpretation; hand it raw artifacts, provenance, and claim-to-result links.
