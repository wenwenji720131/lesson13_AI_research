# Research Scope Definition Guide

Used in SKILL.md Step 1. Guides the narrowing from broad interest to a
precise, bounded research space.

---

## The Four-Dimension Framework

Every research scope can be described by four axes:

| Dimension | Question | Example values |
|---|---|---|
| **Object** | What system/model/algorithm is being studied? | Transformer, Diffusion Model, RL Agent, GNN, VLM |
| **Task** | What capability or behavior is being improved? | Reasoning, Planning, Detection, Generation, Retrieval |
| **Scenario** | In what real-world context or domain? | Autonomous Driving, Medical Imaging, Robotics, Code |
| **Constraint** | Under what practical limitation? | Low compute, Few-shot, Real-time, Privacy, Safety |

**Research space formula**:
> How to improve [Task] of [Object] in [Scenario] under [Constraint]?

---

## Narrowing Process

Work top-down. Start from the user's raw topic and apply each step.

### Level 0 → Level 1: Identify the Object

| Too broad | Narrowed |
|---|---|
| Artificial Intelligence | Large Language Models |
| Computer Vision | Vision-Language Models |
| Reinforcement Learning | Offline RL |

Rule: the Object should be nameable as a model family or algorithm class,
not a research field.

### Level 1 → Level 2: Identify the Task

| Object | Task options | Choose based on… |
|---|---|---|
| LLM | Reasoning / Alignment / Efficiency | User's stated interest |
| VLM | Grounding / Generation / Understanding | Prior papers user has read |
| RL Agent | Planning / Exploration / Transfer | Application domain |

Rule: the Task should be a specific capability, not a general goal like
"improve performance".

### Level 2 → Level 3: Identify the Scenario (if applicable)

Some research is scenario-agnostic (e.g., general LLM reasoning). Only add
a Scenario dimension if:
- The user has a specific application domain in mind, OR
- The field itself is scenario-specific (e.g., autonomous driving, medical)

Leaving Scenario open is valid for broad surveys.

### Level 3 → Level 4: Identify the Constraint (if applicable)

Constraints sharpen the research question. Common constraints in AI/CS:

- **Data**: low-resource, few-shot, zero-shot, domain shift
- **Compute**: inference efficiency, model compression, edge deployment
- **Time**: online/real-time, streaming, latency-bound
- **Privacy/Safety**: federated, differential privacy, adversarial robustness
- **Interpretability**: explainability required

Constraints are optional for broad surveys but required for narrow scope.

---

## Scope Statement Format

After narrowing, produce one paragraph:

```
Research Scope: [One-sentence statement using the formula above]

IN scope:
- [Method families, tasks, scenarios explicitly covered]
- [Paper types to include: surveys, benchmarks, methods, systems]

OUT of scope:
- [Adjacent fields or sub-problems explicitly excluded]
- [Why they are excluded — to justify boundary decisions]

Boundary cases:
- [Topics that are partially related — include at lower tier or note but do not map deeply]
```

---

## Common Mistakes

**Too broad**: "I want to map all of deep learning."
→ No useful taxonomy can be built. Narrow to one Object + Task minimum.

**Too narrow too early**: "I want to map sparse attention for 4-bit quantized
LLM inference on mobile."
→ Literature will be too sparse for a useful map. Start one level up.

**Scope creep during Step 2**: Finding interesting adjacent papers and
expanding scope mid-collection.
→ Add boundary cases to the scope statement instead of expanding the core.

**Task = problem statement**: "Improve accuracy" is not a Task.
→ Task must be a concrete capability: Classification, Reasoning, Planning, etc.

---

## Examples

### Example 1: VLA for Autonomous Driving

Raw topic: "VLA models in autonomous driving"

- Object: Vision-Language-Action Models (VLA)
- Task: Action Reasoning / Decision Making
- Scenario: Autonomous Driving
- Constraint: Real-time, Safety-critical

Scope statement:
> How to improve action reasoning of VLA models in autonomous driving under
> real-time and safety constraints?

IN scope: VLA architectures, action prediction, scene understanding for
driving, driving benchmarks (nuScenes, CARLA, etc.)

OUT of scope: General VLMs without action output, non-driving robotics,
speech/audio modalities

### Example 2: LLM Reasoning

Raw topic: "LLM reasoning"

- Object: Large Language Models
- Task: Multi-step Reasoning
- Scenario: General (no specific domain constraint)
- Constraint: Test-time compute efficiency (optional, for narrow)

Scope statement (broad):
> What methods improve multi-step reasoning ability of LLMs?

IN scope: Chain-of-thought prompting, process reward models, self-consistency,
reasoning benchmarks (GSM8K, MATH, BBH)

OUT of scope: LLM alignment/RLHF (separate field), retrieval-augmented
generation (separate task)
