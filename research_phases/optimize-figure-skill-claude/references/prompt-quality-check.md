# Prompt Quality Check

Use this as a final pass before returning the prompt. Apply the full checklist for a first-round (new) prompt. For an iteration-round prompt (round 2+), also apply the extra "Iteration round checks" section.

## Check the prompt

- The selected master structure is preserved.
- The field style matches the detected discipline. For CS/ML prompts, check both Content Community and Visual Treatment: the content community should match the paper topic, and any Premium Academic Graphical Abstract treatment should still preserve CS system-diagram logic rather than drifting into biomedical, materials-science, or generic journal visual language.
- The target figure type is explicit.
- The research object and content focus come from the provided document or the user's description.
- The layout, modules, arrows, and relationships are concrete.
- The prompt does not ask the drawing model to invent data, curves, measurements, experimental results, microscopy content, or photo evidence.
- The phrase `图中所有可见文字只能使用以下内容` or the English equivalent appears inside the final prompt.
- The final prompt does not contain unresolved scaffolding or placeholders such as `{VISIBLE_TEXT_RULE}`, `[Paste the full Visual Schema here]`, `[Insert extracted research context]`, `[Label ...]`, `---BEGIN PROMPT---`, or `---END PROMPT---`.
- The visible text list contains only concise labels.
- The prompt includes forbidden-content constraints and does not request forbidden content.
- Model adaptation matches one of the three supported models (Nano Banana Pro, Nano Banana 2, gpt-image-2) and is short; it does not override the master prompt.
- No unrelated toolchain suggestions appear.

## Iteration round checks (round 2+)

- The prompt is a **minimal-diff revision** of the previous round's prompt, not a full rewrite. Unrelated zones/labels/structure that the user did not flag should be byte-for-byte or near-identical to the prior round.
- The revision addresses every specific issue named in the user's feedback for this round, and does not silently address issues the user did not raise.
- The model identity is unchanged from the previous round unless the user explicitly asked to switch models.
- The visible-text list is unchanged unless the feedback explicitly requested a label change.
- The output is labeled with the correct round number and model name in its heading.
- If the user's feedback implies a change to the figure type or domain classification itself (not just a rendering detail), flag this explicitly rather than quietly reclassifying — ask for confirmation before discarding the existing Figure Brief.

## Short review reminder

Use one concise sentence outside the final prompt:

```text
生成后请重点审查科学结构、箭头关系、图中文字、数据边界和目标期刊要求。
```

For real data charts, microscopy images, experimental photos, or factual image repair requests, use:

```text
涉及真实数据或实证图像时，请不要让绘图模型编造、修补或改写事实证据；生成结果只能作为示意构图参考，并需作者审查。
```
