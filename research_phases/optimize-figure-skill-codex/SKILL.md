---
name: optimize-figure-skill-codex
description: Generate and iteratively optimize high-quality structured prompts for academic scientific figures without calling any image API. Use when the user provides a paper, method section, figure caption, research-plan text, generated-image feedback, or reference-image description and wants a publication-quality prompt adapted by research domain, figure type, and target image model. Supports Nano Banana Pro, Nano Banana 2, and gpt-image-2; also use for multi-round prompt refinement from a generated image until the user is satisfied.
---

# Optimize Figure Skill Codex

## Overview

Convert research content or figure feedback into a copy-ready prompt for publication-quality scientific illustration. This skill is prompt-only: do not call image APIs, do not require API keys, and do not generate images directly.

## Core Rules

- Default to **single-model mode** with **Nano Banana Pro** unless the user names another supported model.
- Output prompts for `Nano Banana Pro`, `Nano Banana 2`, and `gpt-image-2` only when the user explicitly asks for comparison, all versions, or model migration.
- Prioritize complex structure, academic style, scientific accuracy, and final-candidate quality. Do not write prompts for rough sketches, simple drafts, or casual diagrams unless the user explicitly asks.
- Support image inputs only as available context. If the current environment can inspect the image, analyze it; otherwise ask the user for a concise description of the generated/reference image.
- Never invent scientific facts, data values, curves, microscopy evidence, sample names, or results not provided by the user.

## Workflow

1. Parse intent: identify whether this is first-pass prompt generation, prompt optimization from feedback, model migration, or reference-style extraction.
2. Build a Figure Brief: research topic, domain, figure type, target model, visual treatment, visible text language, required modules, arrows, and forbidden content.
3. Load only the references needed:
   - `references/domain-masters.md` for CS/ML, materials/chemistry, biology/medicine, or unknown fields.
   - `references/figure-type-masters.md` for layout and task-specific constraints.
   - `references/model-cards.md` for Nano Banana Pro, Nano Banana 2, or gpt-image-2 adaptation.
   - `references/reference-style.md` when the user supplies a reference image or style description.
   - `references/iteration-workflow.md` for second or later prompt revisions.
   - `references/language-strategy.md` for visible-text rules.
   - `references/prompt-quality-check.md` before final output.
4. Generate one complete replacement prompt. For iterative requests, include concise diagnosis and changes before the prompt.

## Output Modes

- **First pass:** output `文档理解`, optional `出图方案`, `最终绘图提示词`, and `简短审查提醒`.
- **Optimization pass:** output `问题诊断`, `本轮修改策略`, `保留与删除`, `优化版最终绘图提示词`, and `简短审查提醒`.
- **Compare mode:** output three concise prompts, ordered `Nano Banana Pro`, `gpt-image-2`, then `Nano Banana 2`, with one-line usage notes for each.
- **Prompt-only request:** if the user says "只要 prompt" or equivalent, output only the final prompt section.

## Final Prompt Requirements

- Include the target model and visual treatment inside the prompt.
- Use concrete zones, modules, arrows, relations, panel structure, label list, and forbidden content.
- Include this sentence or its English equivalent inside the prompt: `图中所有可见文字只能使用以下内容`.
- State that internal prompt headings such as `ZONE`, `LAYOUT`, or `CONNECTIONS` must not be rendered as figure text unless listed in the visible-text whitelist.
- End with constraints against marketing poster style, decorative filler icons, watermarks, fake data, and unsupported scientific claims.
