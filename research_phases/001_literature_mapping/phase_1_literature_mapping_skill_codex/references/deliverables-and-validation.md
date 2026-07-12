# Deliverables And Validation

## Required Artifacts

Create all artifacts below inside the dated literature-mapping folder.

| File | Required content |
| --- | --- |
| `scope.md` | Object, task, scenario, constraints, exclusions, date windows, and search boundary. |
| `search-log.md` | Queries, sources, dates, retrieval counts, inclusion/exclusion decisions, and known access limits. |
| `papers.csv` | One deduplicated record per paper using the schema in `artifact-templates.md`. |
| `references.bib` | Verified BibTeX entries for papers cited in the map. |
| `taxonomy.md` | Problem and method families, representative papers, assumptions, strengths, and limitations. |
| `method-evolution.md` | Evidence-backed evolution chains for every major method family. |
| `benchmark-summary.md` | Dataset, metric, baseline, protocol, and limitation summary. |
| `trend-analysis.md` | Explicit date range, query, observed trend, evidence, and uncertainty. |
| `problem-pool.md` | 5-10 evidence-backed problem candidates, without solution proposals or priority ranking. |
| `phase1-validation.md` | Completed acceptance checklist and Phase 2 handoff note. |

## Acceptance Checklist

Mark each item `pass`, `partial`, or `fail`, with a file reference.

1. The scope is specific enough to exclude irrelevant papers.
2. The corpus contains survey, foundational, representative, and recent layers, or records why a layer is unavailable.
3. Every retained paper has a stable URL, provenance, relevance rationale, and a classification.
4. The taxonomy explains relationships among methods, not merely a paper list.
5. Each method-evolution claim names the predecessor problem or limitation it addresses.
6. The benchmark summary distinguishes dataset, metric, baseline, protocol, and benchmark limitation.
7. Trend claims state query, source, date window, and uncertainty.
8. The problem pool contains observations supported by sources and does not select a research gap or method.
9. The map supports the five Phase 1 tests: field map, paper positioning, method comparison, development history, and problem pool.

Phase 1 is complete only when all items pass, or the user explicitly accepts documented partial items.
