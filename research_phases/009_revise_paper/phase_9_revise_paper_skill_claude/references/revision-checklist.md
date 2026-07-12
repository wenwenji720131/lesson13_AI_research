# Revision Checklist

Reference for Phase 9 SKILL.md Steps 3, 7, and 8.

---

## Section 1: Scientific Integrity Checks

Run before making any revision — establishes what the paper currently
claims and whether it can be defended.

### 1.1 Result-Manuscript Consistency

For every number in the manuscript body and abstract:

| Check | Source of truth |
|---|---|
| Matches table/figure value | `result-tables.md` or raw logs |
| Aggregate is computed correctly | All seeds included, not cherry-picked |
| Metric direction stated correctly | ↑/↓ consistent throughout |
| Baseline numbers match cited paper | Check cited paper's Table N |

Any discrepancy is an integrity issue — fix before revision, not during.

### 1.2 Reproducibility Requirements

```
Hardware documented: [yes / no]
Software versions pinned: [yes / no]
Random seeds reported: [yes / no]
Data processing steps described: [yes / no]
Code or checkpoint available (if claimed): [yes / no / URL]
Data licenses documented: [yes / no]
```

Missing items must be added in the revision, not deferred.

### 1.3 Citation Integrity

- Every citation was read before being cited: [yes / flag any exceptions]
- No citation supports a claim stronger than what the paper actually shows
- No self-citation added that does not directly support the text
- Newly added citations in revision are verified against source

### 1.4 Ethics and Compliance

- Dataset collection method ethical (if applicable): [documented / N/A]
- Human subjects or crowdworkers: [IRB status / N/A]
- Potential negative societal impacts: [addressed in paper / N/A]
- Venue-specific ethics requirements: [met / list outstanding items]

---

## Section 2: Structure, Flow, and Expression

Run on the revised manuscript after making substantive changes.

### 2.1 Section-Level Checks

```
Introduction:
  [ ] Gap clearly stated before method is introduced
  [ ] Contribution list precise and falsifiable (not vague descriptions)
  [ ] No method details leaked into introduction

Related Work:
  [ ] Organized by subtopic, not chronologically
  [ ] Each subtopic ends with a positioning statement
  [ ] All baselines from experiments cited

Method:
  [ ] Overview paragraph precedes component descriptions
  [ ] Algorithm box inputs/outputs match text
  [ ] Self-contained: implementable from this section alone
  [ ] No forward references to undefined terms

Experiments:
  [ ] Setup subsection describes baselines, datasets, metrics
  [ ] Every table/figure has a body paragraph with explicit takeaway
  [ ] Body text numbers match table values exactly
  [ ] Ablation table covers all key design decisions

Limitations:
  [ ] Specific to this work (not generic)
  [ ] At least 3 failure modes from Phase 6 failure-analysis.md

Conclusion:
  [ ] No new claims
  [ ] Consistent with abstract
  [ ] Forward-looking sentence present
```

### 2.2 Figure and Table Quality

```
Figures:
  [ ] All axes labeled with units
  [ ] Font size readable at print (≥ 8pt)
  [ ] Baseline included in every comparison figure
  [ ] Caption: describes content AND states key takeaway
  [ ] Accessible in grayscale

Tables:
  [ ] Caption includes metric + dataset + directionality indicator
  [ ] Best result bold per column
  [ ] Uncertainty reported (± std) for stochastic methods
  [ ] All competing methods in same table
```

### 2.3 Expression Checks

```
[ ] No sentence longer than 4 printed lines (split if so)
[ ] No overclaiming terms without quantification:
    "significantly", "always", "solves", "novel", "state-of-the-art"
[ ] Tense consistent (past for experiments, present for claims/principles)
[ ] All acronyms defined on first use
[ ] All symbols defined before use in equations
```

---

## Section 3: Format and Compliance Checks

Run immediately before submission.

### 3.1 Submission Package

```
[ ] PDF compiles without errors (pdflatex output clean)
[ ] Page count: [N] pages ≤ venue limit of [M] pages
[ ] Supplementary: [included / not included] (within venue limit if applicable)
[ ] All figures and tables appear in the compiled PDF
[ ] No overfull \hbox warnings causing text to overflow margins
```

### 3.2 Anonymization (for blind review)

```
[ ] Author names removed from title page
[ ] Institution affiliation removed
[ ] Acknowledgments removed
[ ] Self-citations anonymized: "we showed in [ANON]" not "[Author et al., 2024]"
[ ] No identifying metadata in PDF properties
[ ] No GitHub links that identify authors
```

### 3.3 Camera-Ready (post-acceptance)

```
[ ] Author names and affiliations restored and finalized
[ ] Acknowledgments section added (funding, compute resources)
[ ] Camera-ready template applied (may differ from submission template)
[ ] Supplemental material packaged per venue instructions
[ ] Code/data release URL added (if committed to)
[ ] Final PDF + source submitted to venue system
```

### 3.4 References

```
[ ] All \cite{} keys resolve (no "?" in PDF)
[ ] All bibliography entries cited in text
[ ] Venue citation format applied consistently
[ ] No arXiv-only citations for published papers (use published venue)
```
