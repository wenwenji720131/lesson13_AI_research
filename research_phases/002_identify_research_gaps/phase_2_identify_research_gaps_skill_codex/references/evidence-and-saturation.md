# Evidence And Saturation Protocol

## Evidence Matrix

| Candidate ID | Evidence type | Claim | Source | Stable URL / locator | Status | Interpretation |
| --- | --- | --- | --- | --- | --- | --- |
| G-01 | Explicit limitation | Author-stated limitation | Paper | URL, section, page | verified | Direct support |
| G-01 | Failure result | Error pattern or benchmark result | Paper / benchmark | URL, table, figure | verified | Direct support |
| G-01 | Trend / survey | Issue remains active | Survey / recent paper | URL, section | verified | Context support |

Set `Status` to `explicit`, `observed`, or `inferred`. An inferred record must not be the only support for a candidate gap.

## Query Families

Log all query strings and date windows. Begin with these families and adapt terminology to the field:

```text
<problem> <common solution>
<problem> benchmark evaluation
<problem> survey review
<problem> limitations failure cases
<method family> <scenario> robustness efficiency generalization
```

Screen every candidate as `on-topic`, `near-miss`, or `off-topic`; retain the decision and rationale. Deduplicate by DOI, arXiv identifier, then normalized title.

## Saturation Statuses

| Status | Meaning |
| --- | --- |
| `open` | No retrieved work directly resolves the bounded problem; always retain a recall caveat. |
| `partially addressed` | Work addresses part of the issue but leaves a documented mechanism, setting, or evaluation boundary. |
| `occupied` | Current retrieved work directly addresses the same bounded problem with adequate evidence. |
| `dead-end` | Credible evidence shows a fundamental or still-binding blocker after prior attempts. |
| `inconclusive` | Retrieval, access, or evidence is too weak to support another status. |

## Failure Analysis

For empirical AI work, group failures by task difficulty, input condition, distribution shift, resource budget, model component, and error category. State the evidence source and sample size. For theory or deployment work, group evidence by contradiction, missing assumption, policy constraint, or operational limitation.

Failure-language false-positive rule: a paper that says "X fails" only to motivate and then demonstrate a remedy is an attempt, not evidence that the field abandoned X. Use reported results, Limitations/Future Work, or independent surveys to establish a standing failure.
