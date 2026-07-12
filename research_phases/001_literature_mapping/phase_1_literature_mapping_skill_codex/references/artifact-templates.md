# Artifact Templates

## `papers.csv` Schema

```text
paper_id,title,year,authors,venue,paper_type,layer,stable_url,doi_or_arxiv_id,discovery_source,query,relevance_rationale,problem_category,method_family,dataset_metric_notes,stated_limitation,evidence_status
```

Use `evidence_status` as `verified`, `metadata-only`, or `inferred`. Preserve missing values as empty cells; never infer them from title alone.

## Taxonomy Entry

```markdown
## <Method Family>

**Problem addressed:**
**Core mechanism:**
**Assumptions / operating regime:**
**Representative papers:**
**Strengths:**
**Limitations:**
**Relation to other families:**
```

## Method Evolution Entry

```markdown
## <Transition or Method Family>

1. **Problem:**
2. **Prior solution:**
3. **Prior limitation:**
4. **Subsequent response:**
5. **Evidence:** stable paper links and exact supporting sections when available.
6. **Remaining limitation:**
```

## Benchmark Row

| Dataset / benchmark | Capability measured | Metric | Standard baselines | Protocol notes | Known limitation | Evidence |
| --- | --- | --- | --- | --- | --- | --- |

## Problem-Pool Entry

```markdown
### P<n>: <Observed problem>

**Observed setting:**
**Evidence:**
**Affected method or benchmark families:**
**Why it remains unresolved or under-tested:**
**Uncertainty / counterevidence:**
**Phase 2 handoff question:**
```
