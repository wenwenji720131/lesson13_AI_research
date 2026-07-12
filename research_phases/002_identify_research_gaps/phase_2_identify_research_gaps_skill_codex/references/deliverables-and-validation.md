# Deliverables And Validation

## Required Artifacts

| File | Required content |
| --- | --- |
| `candidate-register.md` | Candidate IDs, origin, method family, scenario, suspected mechanism, and rejection log. |
| `search-log.md` | Queries, dates, indexes, counts, deduplication, inclusion/exclusion decisions, and access limitations. |
| `evidence-matrix.md` | Source-backed limitation, failure, survey, and trend evidence. |
| `research-gap-document.md` | Problem, existing methods, limitation, scenario, evidence, saturation result, value scores, uncertainty, and Research Gap Statement. |
| `gap-matrix.csv` | `candidate_id,area,method_family,limitation,scenario,evidence_count,saturation_status,importance,novelty,feasibility,evaluability,validation_status`. |
| `failure-analysis.md` | Failure categories, affected settings, evidence locators, prevalence, and interpretation limits. |
| `candidate-rqs.md` | Neutral research questions for validated gaps only. |
| `phase2-validation.md` | Pass/partial/fail result and Phase 3 handoff for every candidate. |

## Value Score Anchors

Use 1-5 and record evidence plus uncertainty. Never average scores into an automatic decision.

| Dimension | 1 | 3 | 5 |
| --- | --- | --- | --- |
| Importance | Narrow inconvenience | Meaningful field limitation | Blocks a high-value capability or deployment setting |
| Novelty | Directly solved | Partial overlap or uncertain differentiation | Bounded issue remains unaddressed after logged screening |
| Feasibility | Needed resources unavailable | Plausible with constraints | Data, expertise, and access are available |
| Evaluability | No observable outcome | Partial benchmark or qualitative evidence | Clear measurable outcome and comparison context exist |

## Validation Checklist

Mark each condition `pass`, `partial`, or `fail` with artifact links.

1. **Reality:** recent literature, benchmark evidence, or a credible theory/deployment source supports the limitation.
2. **Saturation:** multiple query families and sources were logged; direct solutions were considered.
3. **Clarity:** one sentence names existing methods, limitation, and material scenario.
4. **Evidence:** at least one explicit or observed limitation/failure supports the candidate; inferences are labelled.
5. **Value:** importance, novelty, feasibility, and evaluability are justified.
6. **Boundary:** no hypothesis, solution, algorithm, experiment plan, or final topic-selection decision appears.
7. **Handoff:** candidate RQs remain neutral and traceable to a validated gap.

Validate a candidate only when every condition passes. Keep partial candidates as unresolved; do not hand them to Phase 3.

## Research Gap Statement

```text
Existing <methods> address <problem X>.
However, they remain limited by <specific limitation Y>.
This limitation is material in <scenario Z>.
Evidence from <sources / benchmark / failures> indicates that the bounded problem is <open or partially addressed>.
```

## Candidate Research Question

```text
RQ<n>: Under what conditions, and for what reason, do <existing methods> fail to achieve <required capability> in <scenario Z>?
```

Do not use solution-leading forms such as "How can we design/propose/build..." until a later phase.
