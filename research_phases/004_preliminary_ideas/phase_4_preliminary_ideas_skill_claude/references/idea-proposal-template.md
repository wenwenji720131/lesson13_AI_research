# Idea Proposal Template

Use for each surviving idea after Step 4 (Conceptual Validation).
Copy this template once per idea. File: `idea-proposals.md`.

---

## Idea Proposal: [P4-IDEA-N]

**Title**: [short name — 3–6 words, includes the key mechanism]

**Target mechanism**:
[Which specific failure mode from the mechanism map does this address?
Reference the failure mode label from Step 1, e.g., "FM-2: gradient
vanishes when sequence length > 512".]

**Core innovation**:
[2–3 sentences. What is the new design choice? Be specific about what
changes relative to the existing baseline. Avoid vague statements like
"we improve X" — describe the actual modification.]

**Causal argument**:
[Why does this change address the root cause? Trace the causal chain:
Existing behavior → failure mode → how the innovation breaks the chain.
Example: "Standard attention allocates uniform weight → distant tokens
dominate → we introduce distance-aware decay → tokens beyond k steps
receive < ε weight → failure mode cannot occur."]

**Assumptions**:
[What must hold for this to work? List 2–4 conditions. These become
the risk factors in Phase 5.]

- Assumption 1: [...]
- Assumption 2: [...]

**Expected evidence**:
[What does a positive result look like? Be specific:
- "Method outperforms baseline by ≥ 5% on benchmark X"
- "Ablation shows >10% drop when component Y is removed"
NOT: "method performs better".]

**Known risk**:
[The single most likely way this idea fails. This becomes Risk-1 in
Phase 5's risk register.]

**Closest prior work**:
[Name the most similar published method. Even if not read:
name the most obvious candidate from memory or a quick search.]
- Closest work: [paper title, authors, venue/year]
- Novelty status: unsearched / partial / searched
- Key difference (if searched): [what the proposal does that the
  closest work does not]

**Estimated complexity for Phase 5**:
low / medium / high

Justification: [what makes this high-complexity, if applicable —
e.g., requires custom CUDA kernel, new training loop, new dataset]

---

## Screening Result

| Dimension | Score (1–5) | Notes |
|---|---|---|
| Causal fit | | |
| Novelty | | |
| Feasibility | | |
| Evaluability | | |
| Risk | | |
| **Total** | | |

Decision: `recommended` / `viable` / `speculative` / `rejected`

Rejection reason (if rejected): [one sentence]
