# Iteration Workflow

Use this when the user provides a previous prompt, generated image, generated-image description, or revision request.

## Inputs to Extract

- Previous target model and prompt, if provided.
- Generated-image observations: missing modules, wrong arrows, text errors, style drift, clutter, poor layout, hallucinated content, or mismatch with reference style.
- User optimization request: what to keep, change, remove, emphasize, simplify, or restyle.

## Revision Policy

- Preserve scientific facts and required modules before applying aesthetic changes.
- Keep the same target model unless the user explicitly asks to switch.
- Output a complete replacement prompt, not only a patch.
- Explain changes briefly unless the user asks for prompt only.
- If the user supplies an image and the current model can inspect it, diagnose directly from the image. If not, ask for a short description of the image issues.

## Output Template

```markdown
## 问题诊断
[3-6 bullets: what is wrong or likely to fail]

## 本轮修改策略
[3-6 bullets: concrete changes to layout, labels, arrows, style, or model adaptation]

## 保留与删除
保留：[scientific structure or visual strengths]
删除/抑制：[errors, hallucinations, clutter, style drift]

## 优化版最终绘图提示词
[complete replacement prompt]

## 简短审查提醒
生成后请重点审查科学结构、箭头关系、图中文字、数据边界和目标期刊要求。
```

## Common Failure Fixes

- Missing module: name it in the visible-text whitelist and assign it to a specific zone.
- Wrong arrow direction: describe source, target, path shape, and semantic meaning.
- Text errors: shorten labels, whitelist exact visible text, and forbid extra text.
- Over-simple draft: request final-candidate academic figure quality, multi-zone structure, refined hierarchy, and publication-ready finish.
- Too decorative: forbid marketing poster style, filler icons, unrelated metaphors, and cinematic lighting.
- Reference style copied too literally: preserve only palette, spacing, line style, and hierarchy; replace all scientific content with the user content.
