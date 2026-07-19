# Language Strategy

Choose visible text based on paper language, target venue, and user request.

## Chinese User, No Venue Specified

Use Chinese explanations to the user. For the prompt itself, use Chinese or bilingual wording if the target generation model handles it well. Keep visible figure labels concise.

Visible text rule:

```text
图中所有可见文字只能使用以下内容：[列出精确标签]。不要生成任何其他标题、段落、脚注、水印、公式、编号或占位文字。`ZONE`、`LAYOUT`、`CONNECTIONS` 等提示词内部结构词不能出现在图中。
```

## English Paper or International Submission

Use English labels unless the user asks otherwise.

Visible text rule:

```text
All visible text in the figure must be limited to the following exact labels: [list exact labels]. Do not render any other titles, paragraphs, footnotes, watermarks, equations, numbering, or placeholder text. Internal prompt headings such as ZONE, LAYOUT, and CONNECTIONS must not appear in the figure.
```

## Label Density

- Nano Banana Pro: moderate labels, all important modules named.
- Nano Banana 2: fewer labels, shorter exact words.
- gpt-image-2: can use more labels if they are controlled and scientifically necessary.

Never use long explanatory sentences inside the figure unless the user explicitly requests a presentation-style graphic.
