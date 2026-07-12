---
name: phase-5-refine-methodology-codex
description: Refine a selected AI or computer-science research idea into a coherent, testable methodology. Use when Codex needs to define method objectives, framework modules, core mechanisms, algorithm flow, assumptions, risks, and an evaluation path before experiment design. Do not use to run experiments, fabricate results, or draft manuscript prose.
---

# Phase 5 Refine Methodology

Read `../README.md`. Accept one Phase 4 idea card plus its gap, research question, constraints, and prior-art uncertainty.

## Workflow

1. Freeze a one-sentence method objective linked to the gap and an observable success condition.
2. Write `method-blueprint.md`: inputs, outputs, modules, data flow, assumptions, and interfaces.
3. Explain each core mechanism as `limitation -> intervention -> expected effect -> failure mode`; remove modules without a causal role.
4. Specify algorithmic flow, training or inference decisions, complexity or resource implications, and alternatives considered.
5. Build a claim-to-evidence map with required baselines, ablations, robustness checks, and invalidating outcomes, but do not prescribe execution details.
6. Produce `method-spec.md`, `assumptions-and-risks.md`, `claim-evidence-map.md`, and `phase5-handoff.md`.

## Boundaries

Mark unverified theory and novelty as assumptions. Do not run models, report numbers, choose hyperparameters through test-set feedback, or write a paper. Hand Phase 6 a frozen method specification and evidence requirements.
