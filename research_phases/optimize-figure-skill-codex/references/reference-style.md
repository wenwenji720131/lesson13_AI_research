# Reference Style Extraction

Use this when the user provides a reference image, generated image, or image description.

## Readability Rule

If the current environment can inspect images, analyze the image directly. If the image is unavailable or unreadable, ask the user for a concise description covering layout, color, line style, text density, and what they want to imitate or avoid.

## Extract Only Transferable Style

Extract:
- Layout direction, panel structure, visual center, spacing, and hierarchy.
- Container shapes, line weight, arrow style, fills, borders, and depth.
- Palette, contrast, background, typography style, label density, and texture level.
- Overall academic finish: strict paper figure, graphical abstract, presentation overview, or clean vector schematic.

Do not copy:
- Scientific conclusions, labels, data values, axes, curves, microscopy evidence, logo, watermark, exact proprietary composition, or unique artwork.

## Style Patch Format

```markdown
## 参考图风格摘要
[5-8 concise bullets]

## 可迁移风格补丁
[one paragraph to merge into the final prompt]

## 不应复制的内容
[content, labels, data, logo, exact composition]

## 适用边界
[where this style helps and where it may hurt]
```

## Integration Rule

Reference style is a patch, not the main instruction. Domain, figure type, scientific facts, visible-text whitelist, and target-model adaptation always take priority.
