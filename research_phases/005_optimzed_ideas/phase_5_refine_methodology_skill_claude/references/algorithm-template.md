# Algorithm Template

Reference for Phase 5 SKILL.md Step 4.

This template defines the expected format for algorithm pseudocode,
mathematical formulation, and complexity analysis.

---

## Algorithm Pseudocode Format

```
Algorithm [N]: [Name]
─────────────────────────────────────────────────
Input:
  [variable]: [type / shape / description]
  [variable]: ...

Output:
  [variable]: [type / shape / description]

Parameters (hyperparameters, set before training):
  [param]: [description, typical range]
  [param]: ...

Require: [any preconditions — e.g., "encoder E is pretrained"]
─────────────────────────────────────────────────
1:  [step]
2:  for [iteration condition] do
3:    [step]
4:    if [condition] then
5:      [step]
6:    end if
7:  end for
8:  return [output]
─────────────────────────────────────────────────
```

### Pseudocode Conventions

- Use mathematical notation for variable names: bold lowercase for vectors
  (**x**, **h**), uppercase for matrices (**W**, **X**), subscripts for
  indices (x_t, h_i)
- Number every line — reviewers reference line numbers
- Name operations explicitly: "Softmax", "LayerNorm", "Cross-Attention"
  not "normalize" or "attend"
- Mark the KEY STEP — the line that implements the core mechanism —
  with a comment: `// Core mechanism: [mechanism name]`
- Keep implementation details out of pseudocode (no CUDA kernels,
  batching tricks, or framework-specific ops)

---

## Mathematical Formulation

Present key equations in a numbered block.

### Notation Table (fill in for the paper)

| Symbol | Meaning | Dimensions |
|---|---|---|
| T | sequence length | scalar |
| d | hidden dimension | scalar |
| **x**_t | input token at position t | ℝ^d |
| **h**_t | hidden state at step t | ℝ^d |

### Equation Block Format

```
Core operation:
(1)  ẑ = f(x; θ)                  [one-line description]

(2)  L = L_main + λ · L_aux       [if composite loss]

(3)  [key equation for the mechanism]
```

Each equation must appear in the paper's Method section with a brief
explanation of each term. Never present an equation without a sentence
interpreting each variable.

---

## Complexity Analysis

Compare to the baseline method. Both should be O-notation with the same
variables for a fair comparison.

### Template

```
Variables:
  n: [what n refers to — e.g., sequence length, graph nodes]
  d: hidden dimension
  k: [other relevant variable — e.g., number of neighbors]

          | Time Complexity | Space Complexity
Baseline  | O(n²d)          | O(n²)
Proposed  | O(nkd)          | O(nk)
Ratio     | k/n reduction   | k/n reduction
```

### When Complexity Is Worse Than Baseline

If the proposed method has higher time or space complexity, provide one
of these justifications:

1. **Bounded overhead**: the overhead is O(c) where c is small and bounded
   (e.g., an extra linear layer with fixed size d × d)
2. **Asymptotic win at scale**: complexity looks worse at small n but
   dominates at the n values used in practice
3. **Explicit tradeoff**: "We accept O(nk) vs O(n) because this provides
   the k-hop context that eliminates the failure mode; without it the
   method cannot work"

If you cannot provide justification (3), redesign the mechanism to reduce
overhead. Reviewers will ask.

---

## Implementation Notes (not in the paper — for Phase 6 reference)

Record implementation-level details here so Phase 6 can implement
faithfully without inventing them:

```
Framework: [PyTorch / JAX / etc.]
Key library functions: [e.g., torch.nn.MultiheadAttention]
Initialization: [how weights are initialized — Xavier, kaiming, etc.]
Numerical stability: [any log-softmax vs softmax considerations]
Gradient flow: [any stop-gradient or detach operations]
Memory optimization: [gradient checkpointing, mixed precision]
```
