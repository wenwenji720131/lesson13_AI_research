---
name: phase-2-identify-research-gaps-codex
description: Identify and validate evidence-backed research gaps from a Phase 1 literature map for AI or computer-science research. Use when Codex needs to examine method limitations, bottlenecks, failure cases, theoretical or application gaps, literature saturation, or gap value; produce a Research Gap Statement, gap matrix, failure analysis, and candidate research questions. Do not use to generate hypotheses, select a final topic, design a method, or plan experiments.
---

# Codex Phase 2 Research Gap Analysis

Find a defensible unresolved problem, not a solution. Read `../README.md`, then read `references/deliverables-and-validation.md`; read `references/evidence-and-saturation.md` before searching or classifying evidence.

## Inputs And Boundaries

Prefer the latest Phase 1 mapping folder with `scope.md`, `papers.csv`, `taxonomy.md`, `method-evolution.md`, `benchmark-summary.md`, `trend-analysis.md`, and `problem-pool.md`. If those artifacts are absent, request the paper corpus or mark the analysis provisional. Do not infer field-wide saturation from a small supplied paper set.

- Derive candidates from documented limitations, benchmark weaknesses, trends, and the Phase 1 problem pool. Do not promote one paper's future-work paragraph directly to a research gap.
- Narrow every candidate to an existing method family, concrete limitation, and material scenario. Split broad claims before evaluating them.
- Keep source-backed fact, observed result, and analyst inference distinct.
- Treat missing search results as a recall limitation, never as proof that a gap is open.
- Stop at gap statements and neutral candidate research questions. Do not create hypotheses, score a final thesis topic, propose an algorithm, choose a dataset, or prescribe an experiment.

## Evidence Discipline

Use approved browser, file, and terminal tools to retrieve sources. Prefer official proceedings, publisher pages, ACL Anthology, CVF, PMLR, OpenReview, arXiv, DBLP, Semantic Scholar, OpenAlex, Crossref, benchmark documentation, and project pages. Confirm quotations in the cited paper before retaining them; otherwise use a paraphrase labelled `indirect`.

Read the local `research-gap-finder` only for its limitation categories. Its hypothesis, prioritization, and method suggestions are out of scope. Read the local `gap-to-topic` only for its adversarial search, dead-end, and quote-verification principles; do not invoke its unavailable `research-hub` commands or DOCX workflow.

## Workflow

### 1. Register Candidates

Create `candidate-register.md`. Give each candidate a stable ID and record the affected method family, scenario, suspected mechanism, originating Phase 1 artifact, and initial uncertainty. Retain rejected candidates with a rejection reason.

### 2. Build Evidence And Failure Records

For each candidate, collect independent evidence where available:

1. an explicit limitation, theory contradiction, or stated assumption;
2. a benchmark bottleneck, error pattern, failure case, or deployment constraint;
3. a survey, recent paper, or measured trend showing the issue remains material.

Write `evidence-matrix.md` and `failure-analysis.md` using `references/evidence-and-saturation.md`. Do not turn an introduction's motivational claim into failure evidence when the same paper reports a successful remedy.

### 3. Test Literature Saturation

For each candidate, run the documented query families against more than one independent index when tools permit. Record queries, dates, source, retrieved count, deduplication rule, screening decision, stable URLs, and access limits in `search-log.md`.

Classify candidates as `open`, `partially addressed`, `occupied`, `dead-end`, or `inconclusive`. Reopen a stale dead-end only if retrieved evidence identifies both the previous blocker and an actual successor technology in the corpus. Never invent a successor.

### 4. Evaluate Research Value

For every surviving candidate, score importance, novelty, feasibility, and evaluability using the anchors in `references/deliverables-and-validation.md`. Explain evidence and uncertainty for each score. Scores support human judgement; they do not automatically select a topic.

### 5. Produce Phase 2 Artifacts

Create one dated output folder:

```text
research-gap-analysis-YYYYMMDD-<topic-slug>/
```

Write all required files listed in `references/deliverables-and-validation.md`. Use the prescribed Research Gap Statement exactly and omit any proposed solution.

### 6. Validate And Handoff

Complete `phase2-validation.md`. Promote only candidates that pass reality, saturation, clarity, evidence, value, boundary, and handoff checks. Hand Phase 3 the validated gap statement, evidence boundaries, unresolved uncertainties, and neutral candidate research questions.

## Tool Safety

Do not install packages, configure MCP servers, alter user configuration, or make a network request requiring new approval unless authorized. Preserve raw metadata, search logs, and original source links so conclusions can be audited or repeated.
