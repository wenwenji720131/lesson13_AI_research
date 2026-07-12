# Academic Writing Guide

Reference for Phase 8 SKILL.md Step 5.

---

## Precision and Quantification

Every claim in a paper must be as precise as possible.

| Imprecise | Precise |
|---|---|
| "significantly improves" | "improves by 3.2 BLEU points (p < 0.05)" |
| "our method is faster" | "reduces inference time by 40% (12ms vs. 20ms)" |
| "achieves state-of-the-art" | "outperforms the previous best by 1.8% on benchmark X" |
| "the model struggles with long sequences" | "accuracy drops from 82% to 61% at length > 512" |

When you cannot quantify a claim: either measure it, or remove the claim.

---

## Hedging and Certainty

Match the hedge level to the evidence strength.

| Evidence | Appropriate hedge | Example |
|---|---|---|
| Direct experimental result | "shows", "demonstrates", "achieves" | "Method A achieves 85.2% accuracy" |
| Pattern observed in results | "suggests", "indicates" | "Results suggest that X improves with scale" |
| Theoretical argument without empirical test | "argues", "implies" | "This formulation implies convergence" |
| Speculation about future work | "may", "could", "might" | "Future work might explore..." |

Avoid:
- "proves" (reserved for formal mathematical proofs)
- "solves" (implies the problem is fully resolved)
- "always" (unless you have an exhaustive test)
- "novel" as a freestanding adjective (every reviewer will check)

---

## Tense Conventions

| Context | Tense | Example |
|---|---|---|
| General facts and principles | Present | "Transformers use self-attention" |
| Describing the proposed method | Present | "Our encoder computes..." |
| Describing experiments you ran | Past | "We trained the model for 100 epochs" |
| Describing results | Past | "The model achieved 85.2% accuracy" |
| Describing what a figure shows | Present | "Figure 2 shows the ablation results" |
| Related work | Past | "Vaswani et al. introduced..." |

---

## Voice

**Active voice is preferred** when the subject is the method or the paper.

| Passive (avoid) | Active (prefer) |
|---|---|
| "A loss is computed by the model" | "The model computes a loss" |
| "Experiments were conducted" | "We conducted experiments" |
| "It can be seen that..." | "Figure 3 shows that..." |

Use passive voice when: the action is more important than the actor,
or when avoiding "we" sounds more natural for a specific sentence.

---

## Common Overclaiming Patterns

These phrases trigger reviewer skepticism. Replace with precise language.

| Pattern | Problem | Fix |
|---|---|---|
| "Our novel method" | Every method is "novel" by definition of submission | Remove "novel" |
| "state-of-the-art results" | Must cite what was state-of-the-art and by how much | "outperforms [X] by 2.1 points" |
| "significantly better" | "Significantly" has a statistical meaning | Report p-value or effect size |
| "demonstrates the effectiveness" | Vague — effectiveness at what? | "demonstrates that X reduces Y by Z" |
| "can handle various tasks" | Which tasks? With what performance? | List tasks and metrics |
| "our approach generalizes well" | Generalizes to what? | "achieves 79% on [OOD dataset]" |

---

## Structural Anti-Patterns

### Introduction Too Long

If the introduction runs more than 1.5 pages, it is likely:
- Describing the method (belongs in Method section)
- Reviewing related work (belongs in Related Work section)
- Presenting results (belongs in Experiments section)

### Related Work as a List

A related work section that summarizes each paper in isolation without
stating how the proposed work differs is not useful. Each subtopic should
end with a 1–2 sentence positioning statement.

### Experiments Section as a Data Dump

If every row in a table has only "the proposed method outperforms", the
section provides no insight. The analysis must explain WHY the results
look the way they do, connecting back to the mechanism from the Method section.

### Limitations as a Generic Disclaimer

"The model may fail on out-of-distribution inputs" is true of every model.
A limitations section must be specific: "The model degrades on sequences
longer than 1024 tokens because [mechanism], as shown in Figure X."

---

## Self-Review Checklist

Before finalizing a section, read it as a skeptical reviewer:

- [ ] Can every claim be traced to a table, figure, or citation?
- [ ] Does every number in the body match the tables exactly?
- [ ] Is any sentence longer than 3 lines? (If yes: split it)
- [ ] Does each paragraph have a clear topic sentence?
- [ ] Are all acronyms defined on first use?
- [ ] Are all symbols defined before use in equations?
- [ ] Is any related work summarized without stating how it differs?
- [ ] Are any results presented in the introduction that aren't in the
  experiments section?
