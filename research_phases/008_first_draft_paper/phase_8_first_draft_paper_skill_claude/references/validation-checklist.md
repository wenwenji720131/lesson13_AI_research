# Validation Checklist

Reference for Phase 8 SKILL.md Step 6.
Run all 7 checks before calling the draft ready for Phase 9.

---

## Check 1: Story Completeness

**Question**: Does the paper tell a complete and coherent story?

**Pass condition**:
- `paper-story.md` has all five elements: problem → gap → method →
  evidence → impact
- The gap stated in the introduction matches the root cause from Phase 2
- The method description matches `methodology-document.md`
- Each contribution in the introduction is backed by a result in Experiments

**Fail signals**:
- The gap is stated but not connected to the method's mechanism
- A contribution claim appears in the introduction but not in Experiments
- The conclusion introduces a claim not made in the main body

**Action if fail**: Revise `paper-story.md` and then revise the affected sections.

---

## Check 2: Claim-Evidence Coverage

**Question**: Does every claim have a direct evidence source?

**Pass condition**:
- Every row in `claim-evidence-section-map.md` has a non-null evidence field
- No `DATA_NEEDED` markers remain in the draft
- Every number stated in the body text matches the corresponding table/figure

**Fail signals**:
- `DATA_NEEDED` markers present — missing evidence
- A body sentence states a number not found in any table
- A figure is referenced in the body but does not exist

**Action if fail**: Either run missing experiments (Phase 6) or remove the
unsupported claim.

---

## Check 3: Figure and Table Completeness

**Question**: Are all figures and tables self-contained and accurate?

**Pass condition**:
- Every figure: caption, axis labels with units, baseline in comparison plots
- Every table: caption with metric + dataset, bold for best, header row
- Every table/figure referenced and explained in the body

**Fail signals**:
- Axes unlabeled or missing units
- A table row missing a baseline comparison
- A figure exists but is never referenced in the body

**Action if fail**: Fix figure/table formatting and add missing body text.

---

## Check 4: Related Work Coverage

**Question**: Are the key baselines and prior works cited and positioned?

**Pass condition**:
- All methods in the comparison table are cited in related work
- For each subtopic in related work, the proposed method's differences are stated
- No method that significantly outperforms all baselines is omitted

**Fail signals**:
- A method in the experiments table is not mentioned in related work
- Related work describes prior methods without positioning the proposed work
- A stronger published baseline was missed

**Action if fail**: Add missing citations and positioning statements.

---

## Check 5: Limitations Section

**Question**: Does the limitations section honestly reflect failure cases?

**Pass condition**:
- Limitations are specific to this work (not generic AI disclaimers)
- At least 3 specific limitations derived from `failure-analysis.md`
- Each limitation states: what breaks, when, and why

**Fail signals**:
- Limitations section is absent or is a single generic sentence
- Known failure modes from Phase 6 `failure-analysis.md` are not mentioned

**Action if fail**: Rewrite limitations using `failure-analysis.md` directly.

---

## Check 6: Format Compliance

**Question**: Does the draft meet venue formatting requirements?

**Pass condition**:
- Page count within the venue limit (check compiled PDF, not source)
- Template used matches the target venue
- For blind review: author names, institution, acknowledgments removed
- Bibliography format matches venue style

**Fail signals**:
- PDF page count exceeds limit
- Author names appear in the text or metadata
- References use the wrong citation format

**Action if fail**: Remove content to meet page limit (prioritize: cut related
work, appendix, or qualitative examples before cutting results or method).

---

## Check 7: Bibliography Integrity

**Question**: Are all citations real, present, and accurately rendered?

**Pass condition**:
- Every `\cite{}` key resolves (no "?" in the compiled PDF)
- Every reference in the bibliography is cited in the text
- Author names and year in the text match the bibliography entry
- No citation was added without reading the source

**Fail signals**:
- Undefined reference warnings in pdflatex output
- A citation key appears in the text but not in the .bib file
- A citation is used for a claim that is not in the cited paper

**Action if fail**: Fix .bib entries and remove any citations added without
verification.

---

## Phase 9 Handoff Statement

After all 7 checks pass, write in `draft-validation.md`:

```
Phase 8 Validation — [Date]
Checks passed: [list check numbers]
Checks failed: [list check numbers and blocking reason, if any]

Draft is ready for Phase 9 review.

Manuscript: [path to main.tex or main.md]
Compiled PDF: [path]
Page count: [N] / [venue limit]
Blind review: [yes / no]
DATA_NEEDED markers remaining: 0 (or N — see list)
Known issues for Phase 9: [list if any]
```
