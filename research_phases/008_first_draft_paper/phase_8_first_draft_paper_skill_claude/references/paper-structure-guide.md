# Paper Structure Guide

Reference for Phase 8 SKILL.md Steps 1, 3, and 4.

---

## Section 1: Research Story Construction

A paper is not a report of what you did — it is an argument for why the
research matters and what should change because of it.

### The Five-Element Story

```
Problem → Gap → Method → Evidence → Impact
```

| Element | Question it answers | Common failure |
|---|---|---|
| Problem | Why should a reader care? | Too narrow ("our model") or too broad ("AI is important") |
| Gap | What is missing that this work provides? | Vague: "existing methods are limited" |
| Method | What exactly is new? | Mechanism buried in a paragraph of related work |
| Evidence | What results back up the claim? | Metrics that don't measure what the gap refers to |
| Impact | Who benefits and how? | Overclaimed scope or no connection back to the problem |

### Contribution List Rules

- 3 contributions maximum in a typical venue paper
- Each contribution is one falsifiable claim, not a description of a module
- Format: "We propose [mechanism] that [does X], which [achieves Y]
  on [benchmark Z]"
- Never write: "We present a novel framework for..." — this is a description,
  not a claim

### DATA_NEEDED Policy

If a contribution lacks evidence at draft time, mark it `DATA_NEEDED` in
`claim-evidence-section-map.md`. Do NOT:
- Draft the claim anyway with vague language
- Invent or approximate results
- Write "we expect that..."

Either run the missing experiment (Phase 6) or remove the claim.

---

## Section 2: Required Elements per Section

### Abstract

- Length: venue limit (typically 150–250 words)
- Structure: problem (1–2 sentences) → gap (1 sentence) → method
  (1–2 sentences) → key result with number (1 sentence) → impact (1 sentence)
- Must include at least one concrete metric result
- Must not include citations

### Introduction

| Paragraph | Content | Length |
|---|---|---|
| 1 | Problem motivation — why it matters in practice | 4–6 sentences |
| 2–3 | Gap analysis — what existing methods do, where they fail | 1 paragraph per subtopic |
| 4 | Our approach — what we do differently (high level only) | 3–4 sentences |
| 5 | Contributions — bulleted list of 2–3 claims with evidence pointers | — |
| 6 | Paper organization (optional for short papers) | 2–3 sentences |

Do NOT include method details in the introduction.
Do NOT present results in the introduction (except as a teaser with a figure).

### Related Work

- Organize by subtopic or approach, not chronologically
- For each subtopic: what existing methods do → their limitation → how
  our work relates
- Never summarize a paper without stating how it differs from the proposed work
- Position related work after the introduction or after the method section
  depending on venue convention

### Method

- Start with an overview paragraph that describes the full system in 3–5
  sentences before diving into components
- For each component: motivation → design → formulation
- Include the algorithm box for the core mechanism
- The method section must be self-contained: a reader should be able to
  implement the method from this section alone

### Experiments

Required structure:
1. **Setup**: datasets, splits, metrics, baselines, implementation details
   (optimizer, batch size, hardware) — in a subsection or a table
2. **Main Results**: full comparison table with all baselines and all
   datasets; body text explains what the table shows and why
3. **Ablation Study**: table with all ablation variants
4. **Analysis** (optional but expected): efficiency comparison, qualitative
   examples, failure cases
5. **Discussion / Limitations**: specific failure modes, not generic hedges

Every table and figure must have:
- A body paragraph that explicitly states the main takeaway
- Numbers from the body that match the table exactly

### Limitations

- 3–5 specific limitations derived from `failure-analysis.md`
- Each limitation states: what breaks, under what conditions, what future
  work could address it
- Never write "the model sometimes fails" — specify when and why

### Conclusion

- 3–4 sentences maximum
- Restate the problem, the core mechanism, and the key result
- One forward-looking sentence about future work
- No new claims

---

## Section 3: Algorithm and Figure Presentation

### Algorithm Box Rules

- Present only the steps a reader needs to understand the method
- Suppress batching, padding, and implementation tricks
- Input/Output lines must match the text description exactly
- The key step (core mechanism) should be visually distinguishable
  (e.g., a comment or shaded box in LaTeX)
- Algorithm boxes go in the Method section, immediately after the
  first description of that procedure

### Figure Checklist

Every figure must satisfy ALL of:
- [ ] Caption describes what is shown AND the key takeaway (not just a label)
- [ ] All axes labeled with units
- [ ] Baseline included in every comparison figure
- [ ] Font size readable at print size (≥ 8pt)
- [ ] Colors distinguishable in grayscale
- [ ] Caption is self-contained (readable without body text)
- [ ] Figure referenced at least once in the body, immediately before or after

### Table Checklist

Every table must satisfy ALL of:
- [ ] Caption includes metric name, dataset name, and directionality
  (↑ = higher is better)
- [ ] Best result per column in bold
- [ ] Second-best result underlined (if space)
- [ ] Standard deviation or error bars included for stochastic methods
- [ ] All compared methods in the same table (no split across tables for
  the same metric)
- [ ] Table referenced in the body with a specific claim stated

### Figures vs. Tables

Use a figure when: showing a trend, a distribution, a qualitative example,
or a comparison where the shape of a curve matters.

Use a table when: comparing specific values precisely, where exact numbers
matter more than trends.
