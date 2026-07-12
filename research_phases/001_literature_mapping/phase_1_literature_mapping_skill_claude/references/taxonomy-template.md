# Taxonomy Construction Template

Used in SKILL.md Step 3. Provides the structure for building a
Problem × Method hierarchical map.

---

## Document Structure

```markdown
# Research Taxonomy: [Research Area]

Generated: YYYY-MM-DD | Papers covered: N | Scope: [scope statement]

---

## 1. Problem Taxonomy

[Tree of problems the field addresses]

### Problem Category A: [Name]

**Definition**: [What class of challenge does this represent?]
**Why it matters**: [Why solving this is important to the field]

#### Sub-problem A1: [Name]
- **Description**: [One sentence]
- **Addressed by**: Method Family α, Method Family β (→ see Section 2)
- **Current best**: [Best known approach and its remaining limitation]

#### Sub-problem A2: [Name]
[same structure]

### Problem Category B: [Name]
[same structure]

---

## 2. Method Taxonomy

[For each problem node, the methods that address it]

### Methods for Problem Category A

#### Method Family α: [Name, e.g., "Attention-based approaches"]

| Paper | Year | Venue | Core Idea | Strength | Weakness |
|---|---|---|---|---|---|
| [Title](url) | YYYY | NeurIPS | [≤15 words] | [≤10 words] | [≤10 words] |
| [Title](url) | YYYY | ICML | ... | ... | ... |

**Family summary**: [2 sentences: what do these methods share, and what
collective limitation do they have?]

#### Method Family β: [Name]
[same structure]

### Methods for Problem Category B
[same structure]

---

## 3. Cross-Reference Index

Quick lookup: given a paper, find its place in the taxonomy.

| Paper | Problem node | Method family | Tier | Key citation |
|---|---|---|---|---|
| [Title] | A1 | α | T3-SOTA | vaswani2017 |
| [Title] | B2 | γ | T2-Foundation | lecun1998 |

---

## 4. Open Nodes

Problem nodes with NO satisfactory method family yet. These feed Step 7
(Problem Pool).

| Problem node | Why unsolved | Evidence papers |
|---|---|---|
| A1 sub-problem X | No method handles Y constraint | [Paper1], [Paper2] |
| B3 | Methods exist but only work in Z regime | [Paper3] |
```

---

## Construction Rules

### Rule 1: Problems before methods

Always define the problem tree first (Section 1), then attach methods
(Section 2). Never organize by method if the goal is understanding the field.

**Wrong**: "Transformer-based methods" → list of papers
**Right**: "Long-range dependency modeling" → Method Family: Transformers

### Rule 2: Leaf nodes must have evidence

Every leaf node (individual paper entry) must have:
- A URL or arXiv ID
- A one-sentence "Weakness" drawn from the paper or citing papers

Weakness entries without evidence are marked `[inferred]` and should be
verified in Step 4.

### Rule 3: Method family granularity

A method family should contain 2–8 papers. If you have 1, it is a single
paper, not a family. If you have 15+, split it.

Good family names describe the *mechanism*, not the paper lineage:
- "Sparse attention" (not "works after Longformer")
- "Reward shaping" (not "papers that cite PPO")
- "Contrastive pre-training" (not "CLIP and related")

### Rule 4: Strength/Weakness must be comparative

Strength: compared to what? ("Faster than Method A")
Weakness: in what condition? ("Fails when input > 2k tokens")

Absolute statements ("good results") are not useful in a taxonomy.

### Rule 5: Open Nodes are not failures

An Open Node means the field has an acknowledged unsolved problem. That is
valuable, not a gap in your taxonomy. Open Nodes are the primary input to
Step 7 (Problem Pool).

---

## Taxonomy Depth Guide

| Survey scope | Recommended depth |
|---|---|
| Broad (full field) | 2 levels of problems, 1 level of method families |
| Medium (sub-field) | 3 levels of problems, 2 levels of method families |
| Narrow (specific task) | 3+ levels of problems, 3+ levels of method families |

Do not go deeper than needed. Depth beyond the research scope wastes time
and obscures the map's navigability.

---

## Example Snippet: Object Detection

```markdown
### Problem Category A: Accurate Object Localization

#### Sub-problem A1: Two-stage detection accuracy-speed tradeoff

| Paper | Year | Venue | Core Idea | Strength | Weakness |
|---|---|---|---|---|---|
| [Faster R-CNN](https://arxiv.org/abs/1506.01497) | 2015 | NeurIPS | Region proposal network + RoI pooling | High accuracy on COCO | Slow inference (~5fps) |
| [Mask R-CNN](https://arxiv.org/abs/1703.06870) | 2017 | ICCV | Adds instance segmentation head | Multi-task, flexible | Even slower; memory heavy |

**Family summary**: Two-stage methods achieve high precision via decoupled
proposal + classification, but inference speed is bounded by the RPN step.

#### Sub-problem A2: One-stage detection anchor design

| Paper | Year | Venue | Core Idea | Strength | Weakness |
|---|---|---|---|---|---|
| [YOLO](https://arxiv.org/abs/1506.02640) | 2015 | CVPR | Single-pass grid prediction | Real-time (45fps) | Low accuracy on small objects |
| [SSD](https://arxiv.org/abs/1512.02325) | 2016 | ECCV | Multi-scale anchor boxes | Better small-object handling | Sensitive to anchor hyperparameters |
```
