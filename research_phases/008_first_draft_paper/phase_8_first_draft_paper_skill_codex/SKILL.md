---
name: phase-8-paper-drafting-codex
description: Draft an evidence-backed AI or computer-science paper from validated research artifacts. Use when Codex needs to build a paper story, extract contributions, draft structured Markdown or LaTeX sections, connect figures and tables to claims, and prepare a submission draft. Do not use to invent citations, results, or reviewer responses.
---

# Phase 8 Paper Drafting

Read `../README.md` and the target venue template. Require Phase 2 gap, Phase 5 method, Phase 6 provenance, and Phase 7 analyses.

## Workflow

1. Create `paper-story.md` with `problem -> gap -> method -> evidence -> impact`; every contribution must link to evidence.
2. Build `claim-evidence-section-map.md` assigning each claim, citation, figure, table, limitation, and section owner.
3. Draft title, abstract, introduction, related work, method, experiments, analysis, limitations, and conclusion in the venue structure.
4. Use only verified bibliography keys and real result artifacts. Label missing evidence `DATA_NEEDED`; never fabricate text, numbers, citations, or figures.
5. Check that figures/tables have captions, units, baselines, uncertainty where applicable, and an explanatory paragraph in the body.
6. Compile or render when the toolchain is available; record warnings, unresolved references, page limits, and anonymization status in `draft-validation.md`.

## Boundaries

Do not claim final readiness or silently repair evidence gaps. Phase 9 owns peer-review response, final compliance, and substantive revision.
