# Prompt Quality Check

Run this final pass before returning any prompt.

## Required Checks

- The target model is one of Nano Banana Pro, Nano Banana 2, or gpt-image-2.
- Default output is Nano Banana Pro unless the user selected another model or requested comparison mode.
- The prompt asks for publication-quality academic figure output, not a rough draft or simple sketch.
- Domain style matches the research field.
- Figure type and layout are explicit.
- Zones, modules, arrows, relations, labels, and forbidden content are concrete.
- The visible-text whitelist appears inside the final prompt.
- Internal structure words are forbidden as visible figure text unless whitelisted.
- No unsupported data, results, microscopy, charts, equations, or claims are invented.
- Reference-image style is used only as a transferable style patch.
- For iterative optimization, the response includes diagnosis, modification strategy, and a complete replacement prompt unless the user asked for prompt only.
- No API key, provider setup, paid command, or direct image-generation step is requested.

## Short Reminder

Use this after the prompt unless the user asked for prompt only:

```text
生成后请重点审查科学结构、箭头关系、图中文字、数据边界和目标期刊要求。
```
