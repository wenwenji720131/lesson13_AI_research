---
name: phase9-revise-paper
description: >
  Revise an AI/CS paper in response to internal audit, peer review, or
  submission requirements (Phase 9). Takes Phase 8 manuscript and reviewer
  comments as input. Produces Revision Register, Change Log, revised sections,
  Response to Reviewers, and Submission Check. Use when the user wants to
  audit claims against evidence, triage reviewer comments, plan and execute
  revisions, write a point-by-point response letter, or run final compliance
  checks. Triggers on: "修改论文", "审稿意见", "revise paper", "reviewer comments",
  "response to reviewers", "camera-ready", "final submission check".
  DO NOT use for: fabricating new results, hiding negative findings, or
  generating new ideas (Phase 4).
user-invocable: true
argument-hint: "<manuscript_dir> [--source internal|peer-review|camera-ready] [--depth quick|standard|deep]"
---

# Phase 9: Revise Paper

Revise an AI/CS paper with evidence integrity and submission compliance.
Every change must be traceable. Every claim must survive an audit.

## Phase Boundary (Hard Limits)

| Forbidden output | Belongs to |
|---|---|
| Running new experiments to fill evidence gaps | Phase 6 |
| Inventing results, citations, or figures | Never |
| Concealing negative results or limitations | Never |
| Claiming a reviewer misunderstood without clarifying the manuscript | Never |
| Generating new research ideas or changing the core RQ | Phase 3/4 |

Phase 9 asks: "Is the paper correct, clear, and compliant?"
Phase 8 asked: "Does the paper tell the story?"

## Inputs

| File | Used in |
|---|---|
| Phase 8 `manuscript/` | All steps — current paper text |
| Phase 8 `draft-validation.md` | Step 1 — known issues from Phase 8 |
| Phase 8 `claim-evidence-section-map.md` | Steps 2–3 — claim audit |
| Phase 6 `result-tables.md` | Steps 2–3 — ground truth values |
| Phase 6 `experiment-integrity-check.md` | Step 3 — reproducibility |
| Reviewer comments (if any) | Steps 4–6 — revision priorities |

## Arguments

- **--source**: `internal` (self-audit before submission) | `peer-review` (responding to reviews) | `camera-ready` (post-acceptance final)
- **--depth**: `quick` (Steps 1, 4, 9) | `standard` (all steps) | `deep` (all + formal claim re-audit)

---

## Workflow

### Step 1: Version Control and Revision Register

Before any change, set up tracking.

Create a new version entry:
```
Version: [v1.0 / v1.1 / camera-ready-1 etc.]
Source: [internal-review / venue / reviewer initials]
Date: [YYYY-MM-DD]
Base manuscript: [file or commit reference]
```

Create `revision-register.md` with one row per issue:
```
| Issue ID | Source | Severity | Affected claim or section |
  Action | Evidence needed | Status |
```

- Source: `internal` / `R1` / `R2` / `AC` (associate chair)
- Severity: `critical` (claim wrong or unsupported) / `major` (affects
  understanding) / `minor` (clarity, format)

---

### Step 2: Claim-Evidence Audit

Before addressing any external feedback, verify the paper's own claims.

Load `references/claim-evidence-audit.md`.

For every central claim in the manuscript:
```
Claim: [exact text]
Section: [section and paragraph]
Evidence: [table/figure/result ID from Phase 6]
Verdict: supported / partially-supported / unsupported / overclaimed
Action: keep-as-is / qualify / strengthen / remove
```

Rules:
- "Unsupported" claims must be qualified or removed — not left as-is
- Overclaimed results must be rewritten with correct quantification
- If evidence is missing and Phase 6 is complete: flag as `DATA_NEEDED`,
  note as limitation, do not fabricate

---

### Step 3: Scientific Integrity Check

Verify reproducibility and ethical compliance.

Load `references/revision-checklist.md` Section 1.

```
Reproducibility:
- All result values match raw data in Phase 6 result-tables.md: [yes/no]
- Hyperparameters reported match reproducibility.md: [yes/no]
- Compute resources documented: [yes/no]
- Random seeds reported: [yes/no]

Ethics:
- Dataset licenses documented: [yes/no]
- Human subjects / crowdworker treatment stated (if applicable): [yes/no]
- Potential negative societal impacts addressed: [yes/no]

Citation integrity:
- All cited claims verified against source papers: [yes/no]
- No citation added without reading the source: [yes/no]
```

Flag failures as `INTEGRITY_ISSUE` in the revision register.

---

### Step 4: Reviewer Comment Triage

(Skip if --source is internal.)

Classify each reviewer comment:
```
Comment ID: [R1-1, R2-3, AC-2, etc.]
Comment: [exact quote]
Type: factual-correction / clarity / evidence-gap / design-concern /
      scope-extension / formatting / compliance
Validity: valid / partially-valid / misunderstanding (of text)
Priority: critical / major / minor
Action: revise-manuscript / add-experiment / clarify / decline-with-justification
```

Prioritize in this order:
1. Repeated concerns across multiple reviewers
2. Claims that affect core credibility
3. Clarity and presentation issues
4. Scope extension requests

For declined requests: draft a respectful explanation of the scope constraint.
Do NOT argue that the reviewer is wrong without adding manuscript clarity.

---

### Step 5: Execute Revisions

Make changes in order: critical → major → minor.

For each revision, log in `change-log.md`:
```
Change ID: [C-N]
Issue ID: [from revision register]
Section and paragraph: [location before change]
Original text: [first 15 words or summary]
New text: [first 15 words or summary]
Rationale: [why this change addresses the issue]
Evidence used: [if claim was strengthened]
```

Load `references/academic-writing-guide.md` for style guidance.

After substantive changes (new claims, changed numbers, new figures):
- Re-run the claim-evidence audit for the changed section
- Update `claim-evidence-section-map.md`

After any methodology change: confirm with Phase 5/6 artifacts.

---

### Step 6: Write Response to Reviewers

(Skip if --source is internal.)

Load `references/response-letter-guide.md`.

Structure:
```
Dear Reviewers and Area Chair,

We thank the reviewers for [1 sentence of genuine acknowledgment].

[Reviewer 1]
Comment R1-1: [quote or paraphrase]
Response: [direct answer — what we did and why, or why we cannot]
Manuscript change: [section + line range, or "no change — see explanation"]
Evidence: [if applicable]

...
```

Rules:
- Address every comment, even if the answer is "we decline because..."
- Do not use passive-aggressive language or imply the reviewer is wrong
- If a request was not implemented: state the constraint plainly
  (out of scope, beyond compute budget, contradicts another reviewer)
- Changes in the paper must match what the response letter claims

---

### Step 7: Structure, Flow, and Expression Audit

Load `references/revision-checklist.md` Section 2.

For each section, verify:
```
Introduction: gap clearly stated before method, contribution list precise
Related work: organized by subtopic, differences stated not just similarities
Method: reads linearly without forward references to undefined terms
Experiments: every table/figure explained in body text, numbers match
Limitations: specific to this work, not generic hedges
Conclusion: no new claims, consistent with abstract
```

Verify figure and table quality:
- Captions are self-contained (readable without body text)
- All axes labeled with units
- Baselines included in every comparison figure/table
- Standard deviations or confidence intervals where stochastic

---

### Step 8: Format and Compliance Check

Load `references/revision-checklist.md` Section 3.

Produce `submission-check.md`:
```
PDF compiles without errors: [yes/no — note warnings]
Page limit respected: [yes/no — current page count vs. limit]
Blind review requirements:
  - Author names removed: [yes/no]
  - Institution removed from text: [yes/no]
  - Self-citations anonymized: [yes/no]
References: all cited in text, all in text cited in references
Figure/table count within venue limit: [yes/no]
Ethics statement included (if required): [yes/no]
Supplementary material organized: [yes/no]
Final filename matches venue convention: [yes/no]
```

Camera-ready only:
- Author list finalized and matches submission system
- Acknowledgments added
- De-anonymized: author names and institution restored

---

### Step 9: Final Pre-Submission Read

Read the full revised manuscript end-to-end as a reader (not author).

Check for:
- Claims in the abstract not supported by the experiments section
- Numbers in the body that differ from the tables
- Undefined acronyms on first use
- Broken cross-references (Figure X, Table Y)
- The word "novel" or "state-of-the-art" without a citation or result

Flag issues in `submission-check.md` and fix before submitting.

---

### Step 10: Archive Submission Version

After final submission:
```
Archive: submission-vN-YYYYMMDD/
  main-submitted.pdf
  supplementary-submitted.pdf (if applicable)
  response-to-reviewers.md (if applicable)
  change-log.md
  submission-check.md
  revision-register.md (final status column all "done")
```

Keep all previous versions — do not overwrite or delete prior drafts.

---

## Output Package

```
phase9-revision-YYYYMMDD-<slug>/
  revision-register.md          ← Step 1 (all issues tracked)
  change-log.md                 ← Step 5 (every text change)
  manuscript-revised/           ← Step 5 (revised LaTeX or Markdown)
  response-to-reviewers.md      ← Step 6 (point-by-point response)
  submission-check.md           ← Step 8–9 (compliance + pre-submit audit)
  archive/                      ← Step 10 (submitted version snapshot)
```

`submission-check.md` must state: "This version is ready for submission"
or list the checks that failed.

---

## Skill Linkage

- **Upstream**: `phase8-write-paper-draft` → provides `manuscript/` and `draft-validation.md`
- **Downstream**: submission system — receives `archive/` package
- **Support tools**:
  - Venue templates: `AAAI27_for_research/` or `AuthorKit27/` in repo root
  - LaTeX compilation: see `CLAUDE.md` for the `pdflatex` + `bibtex` sequence
