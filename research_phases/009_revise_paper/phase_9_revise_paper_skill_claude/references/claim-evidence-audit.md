# Claim-Evidence Audit

Reference for Phase 9 SKILL.md Step 2.

Systematic procedure for auditing every claim in the manuscript against
its evidence source. Run before any revision to establish baseline state.

---

## Audit Procedure

### Step 1: Extract All Claims

Read the manuscript and extract every claim — a claim is any statement
that could be true or false and that a reviewer could challenge.

Types of claims:
- **Quantitative result**: "Method A achieves 85.2% on dataset X"
- **Comparative result**: "Method A outperforms baseline B by 3.2 points"
- **Mechanism claim**: "Component C is responsible for the gain"
- **Generalization claim**: "The method works across three domains"
- **Efficiency claim**: "The method is 2× faster than the baseline"
- **Theoretical claim**: "The loss function converges under assumption Z"

Do not audit: background statements about the field, citations to prior work,
or obvious definitional statements.

### Step 2: Map Each Claim to Evidence

For each claim, find the evidence source:

| Claim ID | Claim text (first 10 words) | Section | Evidence type | Evidence source | Verdict |
|---|---|---|---|---|---|
| CL-01 | "Method A achieves 85.2% on..." | §4.1 | experimental | Table 2, row 3 | supported |
| CL-02 | "Component C is responsible for..." | §4.3 | ablation | Table 3, row "w/o C" | supported |
| CL-03 | "The method generalizes to..." | §5 | experimental | Table 4 | partially-supported |

### Step 3: Assign Verdicts

| Verdict | Meaning |
|---|---|
| `supported` | Claim matches evidence directly and quantitatively |
| `partially-supported` | Evidence exists but is weaker or narrower than the claim states |
| `unsupported` | No evidence found in the manuscript |
| `overclaimed` | Evidence exists but the claim overstates its scope or magnitude |
| `needs-check` | Evidence exists but values need to be verified against raw data |

---

## Verdict-Specific Actions

### Supported

No action needed. Mark as checked.

### Partially Supported

Two options:
1. **Qualify the claim**: add a hedge ("in this setting", "for the tested
   datasets", "under the evaluated conditions")
2. **Add evidence**: run additional experiments to support the stronger claim

Do NOT leave the claim as-is with weaker evidence than stated.

### Unsupported

Three options:
1. **Add evidence**: run the experiment in Phase 6 and add to the paper
2. **Qualify to supported**: rewrite the claim to match what the evidence
   actually shows
3. **Remove the claim**: if no evidence is available or runnable

Do NOT keep an unsupported claim in the submitted paper.

### Overclaimed

Rewrite the claim to accurately state what the evidence shows:
- "state-of-the-art" → "outperforms [specific compared methods]"
- "always" → "in all tested cases" (and list the cases)
- "significantly better" → "better by X on Y (p < 0.05)"

### Needs-Check

Verify the number in the manuscript against:
1. `result-tables.md` (the ground truth for all experimental values)
2. The raw experiment log if the table value itself is uncertain

---

## Verification Against Raw Data

For quantitative claims, check three levels:

**Level 1 — Manuscript vs. Table**
Does the number in the body text exactly match the table?
Mismatch here is a manuscript error — update the text, not the table.

**Level 2 — Table vs. result-tables.md**
Does the table value match Phase 6 `result-tables.md`?
Mismatch here is a table error — update the table.

**Level 3 — result-tables.md vs. experiment log**
Does the value in `result-tables.md` match the raw run log?
Mismatch here is a computation error — trace back to the run and recompute.

The audit is complete when all three levels are consistent for every
`supported` claim.

---

## Audit Output Format

Produce one audit block per claim in `revision-register.md`:

```
CL-[N]
Claim: [exact text from manuscript]
Section: [section N, paragraph M]
Evidence type: [quantitative / comparative / mechanism / generalization /
  efficiency / theoretical]
Evidence source: [Table N row M / Figure N / Algorithm N / Theorem N]
Raw data verified: [yes / no — Level 1-3 check]
Verdict: [supported / partially-supported / unsupported / overclaimed / needs-check]
Action: [keep-as-is / qualify / strengthen / remove / rewrite]
Notes: [any discrepancy found during verification]
```

---

## Summary Metrics

After completing the audit, add this summary:

```
Audit completed: [YYYY-MM-DD]
Total claims audited: N
  Supported:           N  (N%)
  Partially supported: N  (N%)
  Unsupported:         N  (N%) ← must reach 0 before submission
  Overclaimed:         N  (N%) ← must reach 0 before submission
  Needs-check:         N  (N%) ← must reach 0 before submission
Raw data verified:     N / N claims
```

A paper is ready for submission only when `unsupported`, `overclaimed`,
and `needs-check` all reach 0.
