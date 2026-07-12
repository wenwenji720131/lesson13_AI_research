# Method Evolution Analysis Guide

Used in SKILL.md Step 4. Guides construction of method evolution chains
that explain *why* methods developed, not merely *when*.

---

## What an Evolution Chain Is

An evolution chain is a causal sequence connecting a recognized problem,
the existing solution, its failure mode, the insight that motivated a new
approach, and the new solution — together with its own residual limitation.

```
[Problem]
    ↓
[Solution A]  ←  Core idea of A
    ↓
[Limitation of A]  ←  Must be grounded in evidence
    ↓
[Insight / Motivation]  ←  Why did researchers think a new approach would work?
    ↓
[Solution B]  ←  Core idea of B
    ↓
[Residual limitation of B]  →  (Next chain link, or Open End)
```

The chain is not a timeline. Papers from the same year can form a chain if
one explicitly addresses a limitation of the other.

---

## Chain Construction Rules

### Rule 1: Ground every limitation

Each "Limitation of X" node must be supported by one of:
- The paper itself (explicit "limitations" section)
- A citing paper that frames its contribution as fixing X's limitation
- A benchmark result showing X fails on a specific condition

Do not insert inferred limitations. Mark them `[inferred — verify]`.

### Rule 2: Name the insight

The transition from Limitation → New Solution requires an insight: the
conceptual leap that made the new approach non-obvious. This is the most
important node in the chain.

Bad: "Researchers then proposed Method B."
Good: "Insight: if attention is computed globally, the quadratic cost is
the bottleneck → what if we sparsify attention patterns?"

### Rule 3: Mark open ends

A chain's last node whose residual limitation has no known solution yet is
an Open End. Mark it:

```
[Residual limitation of latest method]  →  *** OPEN END ***
```

Open Ends are direct candidates for Problem Pool (Step 7).

### Rule 4: Branches are valid

One limitation can motivate multiple independent solution families.
Draw branches when this happens:

```
[Limitation of A]
    ├── [Insight 1] → [Solution B]  →  [Limitation of B]
    └── [Insight 2] → [Solution C]  →  [Limitation of C]  →  *** OPEN END ***
```

### Rule 5: Minimum chain depth

A chain must have at least 3 links (Problem → Solution A → Solution B).
A single paper with a known limitation is not yet a chain — it is a
candidate for "to be mapped when more papers are collected."

---

## Document Format

```markdown
# Method Evolution Chains: [Research Area]

---

## Chain 1: [Method Family Name]

**Field**: [Which part of the taxonomy this chain belongs to]
**Time span**: [e.g., 2017–2024]
**Chain depth**: [number of links]

### Link 1

**Problem**: [What real-world or technical challenge motivates this?]

**Solution A**: [Paper title, Year, Venue]
Core idea: [One sentence]
Result: [Key benchmark number or qualitative achievement]

**Limitation of A**: [What does A fail at?]
Evidence: [cite paper(s) that show or acknowledge this limitation]

**Insight**: [Why did the next researcher think a different approach would work?]

---

### Link 2

**Solution B**: [Paper title, Year, Venue]
Core idea: [One sentence — must reference the Insight above]
Result: [Key benchmark number]

**Residual limitation of B**: [What does B fail at?]
Evidence: [cite]

**Insight**: [...]

---

### Link N (most recent)

**Solution N**: [...]

**Residual limitation of N**: [...]
Evidence: [...]

→ *** OPEN END *** — no published method fully addresses this as of [date].
Candidate for Problem Pool entry P-[N].

---

## Chain 2: [Next Method Family]
[same structure]
```

---

## Common Patterns in AI/CS Evolution

Recognizing these patterns speeds up chain construction:

### Pattern 1: Efficiency–Accuracy Tradeoff

A high-accuracy method is computationally expensive. A faster approximation
is proposed, sacrificing some accuracy. Then a method is proposed to recover
accuracy at the new speed level.

Example: Full attention → Sparse attention → Learned sparse attention

### Pattern 2: Inductive Bias Relaxation

A hand-designed bias (e.g., convolution locality) achieves good performance
on standard benchmarks but fails on out-of-distribution data. A more general
architecture removes the bias and learns it instead.

Example: CNN (locality bias) → ViT (no locality bias) → Hybrid architectures

### Pattern 3: Supervision Signal Expansion

A method trained on limited labels fails to generalize. Pre-training on
large unlabeled corpora provides better initialization.

Example: Supervised classification → Self-supervised pre-training →
Fine-tuning paradigm

### Pattern 4: Scale Law Discovery

A method works poorly at small scale. Increasing scale (data, model size,
compute) unexpectedly improves performance. Optimization then focuses on
making scaling more efficient.

Example: Small LMs → Scaling laws → Efficient architectures for large scale

### Pattern 5: Domain Gap

A method trained in one domain (e.g., simulation) fails in another (e.g.,
real-world). Techniques for domain adaptation or bridging are proposed.

Example: Sim-to-real gap in robotics, Lab-to-clinical gap in medical imaging

---

## Example: Attention Mechanism Evolution

```markdown
## Chain 1: Sequence Modeling Attention

Field: NLP → Vision → Multimodal
Time span: 2015–2024
Chain depth: 4

### Link 1

Problem: RNNs process sequences step-by-step, preventing parallelization
and losing long-range dependencies.

Solution A: Transformer (Vaswani et al., 2017, NeurIPS)
Core idea: Replace recurrence with full self-attention over all positions.
Result: BLEU +2 on WMT EN-DE; fully parallelizable.

Limitation of A: O(n²) memory and compute in sequence length.
Evidence: Vaswani et al. acknowledge quadratic cost; confirmed empirically
for n > 1024 (Child et al., 2019).

Insight: Not all token pairs need full attention — structure in data
suggests most attention mass is concentrated in local or sparse patterns.

---

### Link 2

Solution B: Sparse Transformer (Child et al., 2019, arXiv)
Core idea: Restrict attention to fixed local + strided global patterns.
Result: 30× memory reduction; comparable perplexity on enwiki8.

Residual limitation of B: Fixed sparsity pattern may miss task-relevant
non-local dependencies; not adaptive.
Evidence: Performance gap on tasks requiring irregular long-range context
(Tay et al., 2020, Long Range Arena).

Insight: Sparsity pattern should be learned from data, not hand-designed.

---

### Link 3

Solution C: Longformer / BigBird (Beltagy 2020; Zaheer 2020)
Core idea: Combine sliding window local attention + global tokens for
task-specific positions.
Result: Near-full-attention quality on document tasks at O(n) cost.

Residual limitation of C: Global tokens must be predefined; not suited
for tasks where important positions are not known in advance.
Evidence: Performance degrades when global token placement is wrong
(Xiong et al., 2021).

→ *** OPEN END *** — adaptive, content-aware sparse attention that
does not require predefined global positions remains an active research
problem as of 2024. Candidate for Problem Pool.
```
