# Model Cards

Use model cards as light adaptation only. Do not replace the selected master prompt. This skill targets **academic/publication-grade** output — every card below is tuned to push the model toward complex, precise, journal/conference-ready structure, not toward casual sketches or quick drafts.

## Supported models

Only these three models are supported. Do not generate prompts for any other image model unless the user explicitly asks and accepts that it falls outside this skill's tuned model cards.

| Model | Academic role | Adaptation |
| --- | --- | --- |
| **Nano Banana Pro** | **Default candidate #1.** Complex multi-region structure, stable redraws across iterations, final publication/submission-candidate diagrams. Best when the figure has many zones, feedback loops, or hierarchical layout. | Use explicit zone/module/position language, precise arrow and connection descriptions, and an explicit forbidden-content list. Avoid vague or conflicting style words — Nano Banana Pro rewards literal, structured instructions over loose adjectives. Keep labels moderate-to-rich but grouped by zone so the model does not blur regions together. |
| **gpt-image-2** | **Default candidate #2.** Strongest text-rendering fidelity among the three; best for label-dense system diagrams, method pipelines, and graphical abstracts where many short labels must render legibly. | Constrain scientific structure clearly, but allow richer controlled labels and short explanatory phrases when they clarify the workflow — do not force minimal-text mode purely because the label count exceeds 10. Composition/whitespace can stay moderately flexible since text renders reliably. |
| **Nano Banana 2** | **Not a default.** Positioned as a fast-draft / multi-version screening model, not a final academic candidate. Use only when the user explicitly asks for quick drafts, rapid iteration screening, or many cheap variants before committing to a final model. | Emphasize short, readable labels and exact text over dense labeling. If the user later wants a polished/final version, recommend switching to Nano Banana Pro or gpt-image-2 rather than continuing to iterate on Nano Banana 2 output. |

## Model selection is not silently defaulted

Because this skill targets rigorous academic figures (not quick sketches), do not silently pick a model when the user hasn't stated one. Ask once, as part of the same clarifying-question batch used for figure type / content scope (see `SKILL.md` Step 3), and frame it as a choice between the two academic-grade defaults:

```text
用于生成图片的模型：
1. Nano Banana Pro（推荐）——复杂结构、多区域、可稳定多轮重绘，适合投稿正文图/最终候选图。
2. gpt-image-2（推荐）——文字渲染能力最强，适合标签密集的系统图/图形摘要。
（如需快速草稿筛选多个版本，也可以选 Nano Banana 2，但后续建议切换到以上两者之一定稿。）
```

If the user says "直接默认" / "快速生成" / "quick default" without picking, default to **Nano Banana Pro** (the more literal, structure-first model is the safer unstated default for academic diagrams) and state that choice explicitly in the output so the user can correct it before spending a generation call.

## Output is single-model, not multi-model

This skill always produces **one** complete prompt for **one** confirmed model per turn, not three parallel prompt variants. This is deliberate: multi-round iteration (see `iteration-critique.md`) binds each round's feedback to a specific generated image, and that image was produced by exactly one model. Producing three prompts per turn would make it ambiguous which model a later "the arrows are wrong" comment refers to. If the user wants to switch models mid-project, treat it as a new explicit request — regenerate a fresh prompt for the new model from the same Figure Brief, and reset the iteration round counter for that model.

## Common constraints

Chinese:

```text
请严格遵守指定的科学结构，不要新增、删除、合并、重排或改写任何科学模块。不要编造数据、数值、曲线、图例、色标、公式、实验结果或测量标签。不要营销海报风，不要装饰图标，不要水印。
```

English:

```text
Strictly follow the specified scientific structure. Do not add, remove, merge, reorder, or reinterpret any scientific module. Do not invent quantitative data, values, curves, legends, color bars, equations, experimental results, or measurement labels. No marketing poster style, no decorative icons, no watermark.
```

## When to use a Visual Schema first

Use a two-stage Visual Schema when the figure has more than four regions, parallel flows, feedback loops, multi-level hierarchy, many labels, or strict layout requirements. Otherwise, a figure-type master can be used directly. For academic-grade output, the two-stage Visual Schema is the common case, not the exception — prefer it whenever the paper's method has more than one logical stage.
