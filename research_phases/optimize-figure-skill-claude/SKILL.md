---
name: optimize-figure-skill-claude
description: Use when 用户想根据论文、科研文档、研究文本、图注、开题/答辩材料、图片描述或具备读图条件的参考图生成可复制的 AI 科研绘图提示词，目标模型为 Nano Banana Pro、Nano Banana 2 或 gpt-image-2；也用于用户已经用某一版提示词生成过图片、现在想基于图片效果和修改意见继续优化提示词的多轮迭代场景。触发场景包括论文配图、科研绘图、图形摘要、Graphical Abstract、机制图、技术路线图、实验装置图、模型架构图、多面板对比图、汇报总览图、参考图风格迁移、未知领域母版生成、优化已生成的绘图提示词、根据生成图片的问题调整 prompt，或上传/引用 PDF、Word、LaTeX、Markdown、摘要、方法段、图注、课题说明、研究方案、参考图片、已生成的图片。Also use when the user asks for scientific figure prompts, research illustration prompts, graphical abstract prompts, mechanism diagrams, technical roadmaps, experimental setup diagrams, model architecture diagrams, multi-panel scientific figures, paper/conference figures, or AI image prompts for Nano Banana Pro, Nano Banana 2, or gpt-image-2, based on papers, research documents, abstracts, methods sections, figure captions, proposals, reference images, PDFs, Word docs, LaTeX files, Markdown files, research plans, or a description of the target figure. Also use for iterating/refining an already-generated prompt based on a generated image and follow-up feedback.
---

# optimize-figure-skill-claude

这个 Skill 把论文、开题材料、实验方案、研究说明、图片描述，或具备读图条件的参考图，转换成可直接复制给 AI 绘图模型的科研绘图提示词，目标模型限定为 **Nano Banana Pro**、**Nano Banana 2**、**gpt-image-2** 三者之一。它只生成 prompt，不生成图片，不调用任何 API，不依赖任何 API Key，不推荐草图工具，不展开矢量化或后处理流程。它额外支持**多轮迭代优化**：用户拿着已生成的图片和修改意见回来时，本 Skill 基于结构化诊断对上一版 prompt 做最小改动修订，直到用户满意为止。最终 prompt 和图中文字使用中文还是英文，由论文语言、投稿场景和用户需求决定。

## 两条主路径

- **首轮生成路径**（Step 1-5）：输入是论文/研究内容/图片描述（可能附带风格参考图），产出第一版绘图提示词。
- **迭代优化路径**（Step 6）：输入是"上一版 prompt 生成的图片 + 本轮修改要求"，产出修订版提示词。两条路径共享同一套领域母版、图类型规则、模型卡和语言策略，只是触发条件和输出结构不同。

判断走哪条路径：如果当前对话里已经存在一版本 Skill 生成过的 prompt、且用户在针对它给反馈，走迭代路径（跳到 Step 6）；否则走首轮路径。

## 核心流程（首轮生成）

1. 解析用户提交的研究内容。
   - 用户可以直接用文字描述论文内容或想要的图片效果，不要求必须上传文件。
   - 如果用户给了文件路径，运行 `scripts/extract_research_doc.py`。
     - 支持 `.docx`、`.pdf`、`.tex`、`.latex`、`.md`、`.txt`。可以尝试解析 `.doc`，但旧版 Word 文件依赖本地转换工具；失败时要求用户转换为 `.docx` 或粘贴相关文本。
     - 提取标题、摘要、方法、结果、图注、结论和候选上下文片段。
     - 如果用户给的是 LaTeX 文件夹，要求用户指定主 `.tex` 文件，不要自行猜入口。
     - 如果 PDF 或 Word 解析质量不高，要明确说明，只基于已成功提取的文本生成提示词。
   - 如果用户只给了纯文字描述（论文核心内容、想画的图的效果描述），直接以这段描述作为研究内容，不必强制要求上传文件。

2. 判断绘图上下文。
   - 识别研究主题、学科领域、候选图类型、最适合可视化的论文片段或用户描述的重点。
   - 如果明显属于计算机/机器学习、材料与化学、生物与医学，优先使用领域母版（`references/domain-masters.md`）。
   - 领域母版必须使用对应学科的发表语境：计算机类优先 ACM/IEEE/NeurIPS/ICML/CVPR/ACL/VLDB/KDD/WWW 等论文架构图的信息组织方式，不要套用 Nature/Science/Cell 的生物医学或材料科学视觉语言；材料化学、生物医学再使用各自对应期刊风格。
   - 对计算机/机器学习论文，不要把"领域会议风格"和"图面气质"混成一个选择；先分开判断两件事：**内容社区**（论文主题更接近哪个会议/期刊家族，决定信息组织方式）和 **视觉气质**（用户想要严格正文论文图、高级科研 graphical abstract、科研汇报/白皮书总览图，还是极简扁平矢量图）。
   - 如果用户未指定目标风格，不要直接锁死一个单一风格；先给出 2-3 个很短的"出图预期确认"候选，每个只写清"内容社区 + 视觉气质 + 适合什么结果"，并标注推荐项。目的是让用户在生图前确认大方向，不要写成长篇风格说明。
   - 如果用户提到"好看、质感、高级、出彩、精修、teaser、graphical abstract、海报、项目主页、展示图"等审美目标，优先推荐 **Premium Academic Graphical Abstract / 高级科研图形摘要** 视觉气质，而不是朴素的会议正文流程图；但内容社区仍然按论文主题选择。
   - 如果风格选择会显著改变最终 prompt，先让用户在候选风格中选择，此时不要同时输出最终绘图提示词；如果用户要求快速生成、"直接默认"或"只要 prompt"，才使用推荐项继续生成最终 prompt。
   - 图类型只作为表达任务规则，不替代领域母版。领域明确时，领域母版负责科学对象、学科语义和视觉语言；`references/figure-type-masters.md` 只作为适配层，约束表达目标、布局、区域、连接关系、可见文字和常见失败。
   - 只有当领域不明确、交叉学科明显或没有合适领域母版，且通用图类型结构不会丢失关键领域语义时，才单独使用图类型规则。
   - 如果现有领域母版无法覆盖用户学科，且直接使用通用图类型母版会丢失关键领域语义，读取 `references/adaptive-masters-and-reference-style.md`，使用 **模式 A：未知领域自适应母版**，先生成可复用的新领域母版草案，再基于草案生成本次最终绘图 prompt。
   - 如果用户提供参考图或要求"按这张图风格"，读取 `references/adaptive-masters-and-reference-style.md`，使用 **模式 B：参考图风格补丁**。风格补丁只能作为附加层，不能替代已选母版或新生成母版。注意区分：这里的参考图是"风格灵感来源"，不是"已生成图片的反馈对象"（后者走 Step 6）。
   - 只有当前模型具备读图能力时才分析参考图。若图片不可用或当前模型不能读图，要请用户补充参考图的简短描述，不要假装已经看过图片。
   - 如果多个选择都合理，先给推荐方案，只追问会显著改变最终 prompt 的问题。

3. 只追问必要信息。
   缺失信息会影响最终 prompt 时才问，尽量合并成一次追问：
   - 想画哪种图：技术路线图、实验装置图、机理示意图、多面板对比图、Graphical Abstract、开题/答辩/汇报总览图或其他。
   - 针对哪部分内容画：摘要、方法、结果、图注、全文、开题内容、用户描述的重点或用户指定片段。
   - 图中文字语言：中文、英文、中文提示词但英文标签、少文字。
   - **绘图模型**：本 Skill 只支持 Nano Banana Pro、Nano Banana 2、gpt-image-2 三选一。未指定时必须询问（不静默默认），推荐 Nano Banana Pro 或 gpt-image-2 作为学术级默认候选，仅在用户明确要快速草稿筛选时才提 Nano Banana 2；具体话术见 `references/model-cards.md` 的"模型选择不做静默默认"章节。如果用户要求快速生成/直接默认且未表态模型，按该章节的默认规则处理（默认 Nano Banana Pro）并在输出中明确说明这一选择。

4. 按需读取参考资料。
   - `references/domain-masters.md`：计算机/机器学习、材料与化学、生物与医学领域母版。
   - `references/figure-type-masters.md`：图类型融合规则，包括技术路线图、实验系统图、机制解释图、多面板比较图、图形摘要、汇报总览图和期刊封面图。
   - `references/model-cards.md`：Nano Banana Pro / Nano Banana 2 / gpt-image-2 三个模型的学术级适配规则和模型选择策略。
   - `references/language-strategy.md`：提示词语言与图中文字语言策略。
   - `references/prompt-quality-check.md`：最终检查与简短审查提醒（含首轮检查项和迭代轮次检查项）。
   - `references/adaptive-masters-and-reference-style.md`：未知领域母版生成、参考图风格补丁和保存为 Skill 母版的协议。
   - `references/iteration-critique.md`：多轮迭代优化流程，仅在 Step 6 使用。

5. 生成一段最终绘图提示词。
   - 不要把领域母版和图类型规则逐段拼接。
   - 领域已覆盖时，以领域母版作为主要科学视觉语言。
   - 图类型规则只作为适配层，用来约束表达目标、布局、区域、连接关系、可见文字、科学边界和常见失败。
   - 写最终 prompt 前，先在内部形成 Figure Brief：图像目标、领域对象、图类型结构、区域/模块、连接关系、可见文字、科学边界和模型适配。**这份 Figure Brief 需要在对话上下文中完整保留**，它是后续多轮迭代（Step 6）的修订基准。
   - 如果领域与图类型发生冲突，优先级为：科学事实 > 用户明确要求 > 领域母版 > 图类型结构 > 模型适配 > 审美词。
   - 模型适配只能轻量补充，不覆盖领域视觉语言或科学约束；三个模型的适配规则详见 `references/model-cards.md`。
   - 必须把"图中所有可见文字只能使用以下内容..."写进最终绘图提示词内部。
   - 将 `{VISIBLE_TEXT_RULE}` 替换为 `references/language-strategy.md` 中与语言场景匹配的可见文字规则；面向用户的最终 prompt 中不要留下 `{VISIBLE_TEXT_RULE}` 或任何未填占位符。
   - Stage 1 Visual Schema 只作为内部规划。最终 prompt 仍然可以使用 `ZONE 1`、`ZONE 2`、`CONNECTIONS` 这类结构标题来组织绘图指令，但不能包含 `[Paste the full Visual Schema here]`、`[Insert extracted research context]`、`---BEGIN PROMPT---`、`---END PROMPT---` 或未替换的 `[Label ...]` 半成品脚手架。
   - 如果最终 prompt 使用 `ZONE` 这类结构标题，要通过可见文字规则说明这些只是提示词内部结构，除非显式列入可见标签清单，否则不能被画成图中文字。
   - 如果生成了自适应领域母版，要把新母版草案和本次最终 prompt 分开输出；只有当用户确认满意后，才询问是否保存为可复用 skill 母版。
   - 如果用户明确同意保存自适应领域母版，将其追加到 `references/domain-masters.md`，并在 Stage 2 保留 `{VISIBLE_TEXT_RULE}` 占位符。
   - 不要把"图中可出现的文字"做成用户需要额外复制的独立步骤。
   - 生成前，用 `references/prompt-quality-check.md` 的首轮检查项过一遍。
   - 输出前，明确标注本次确认使用的模型名称（例如"最终绘图提示词（Nano Banana Pro）"），为后续可能的迭代轮次做好标记基础。

## 多轮迭代优化（Step 6）

当用户带着"上一版 prompt 生成的图片"和修改意见回来时，切换到本流程，不要重新走 Step 1-5 的完整领域判断。

1. 判断是否满足迭代前提：当前对话里存在一份本 Skill 已生成的 Figure Brief + 已确认模型 + 完整 prompt。若不满足，说明需要先有一版基准 prompt，引导用户提供或走首轮流程。
2. 读取 `references/iteration-critique.md`，按其定义的读图判断、结构化诊断维度（结构保真度/领域语义/可见文字/科学边界/模型特定常见失败/用户本轮问题）和修订优先级执行。
3. 严格遵守"最小改动修订"：只改用户反馈涉及的部分，其余保持上一版不变。
4. 涉及图类型/领域重新判断或模型切换的反馈，先按 `iteration-critique.md` 的规则向用户确认，不直接静默处理。
5. 输出使用 `iteration-critique.md` 定义的"变更摘要 + 优化后的绘图提示词（第 N 轮 · 模型名）"格式，并用 `references/prompt-quality-check.md` 的迭代轮次检查项过一遍再返回。
6. 用户表示满意即结束，无需额外确认步骤。

## 输出格式

默认跟随用户交流语言输出：用户用中文提问时，使用中文交流；用户用英文提问时，使用英文交流。最终绘图 prompt 和图中文字语言不简单跟随交流语言，而是按论文语言、投稿场景、用户要求和 `references/language-strategy.md` 的规则决定。

当需要用户先确认出图预期或绘图模型时，只输出 `## 文档理解`、`## 出图预期确认` 和必要的 `## 选用依据`，等待用户选择后再输出最终绘图提示词。只有在用户要求快速生成、直接默认或只要 prompt 时，才跳过等待并使用推荐项输出最终 prompt。

### 首轮生成输出

```markdown
## 文档理解
[3-6 条：研究主题、领域判断、选用片段、图类型、绘图模型、图中文字语言]

## 出图预期确认
[当用户未指定目标风格和/或绘图模型，且选择会显著影响生图结果时列出候选。风格候选 2-3 个，每项不超过 2 行，包含：内容社区 + 视觉气质 + 适合什么结果；模型候选见 model-cards.md 的确认话术。标注推荐项。让用户快速选方向，不写长篇解释。]

## 选用依据
[简要列出使用了哪些摘要、方法、结果、图注、用户描述或候选片段]

## 自适应领域母版草案
[仅当现有领域母版无法覆盖并生成了新领域母版时输出。包含适合场景、领域图示特征、Stage 1 Visual Schema、Stage 2 Rendering Prompt、可替换变量、稳定约束和质检清单。]

## 参考图风格补充
[仅当使用参考图或参考风格时输出。包含可迁移风格摘要、可添加到最终 prompt 的风格补充、不应复制内容和适用边界。]

## 最终绘图提示词（[模型名]）
[一段可以直接复制给绘图模型的完整 prompt。必须在这段 prompt 内部包含"图中所有可见文字只能使用以下内容..."。输出前必须替换所有占位符和内部 schema 交接标记。]

## 图中文字核对清单
[默认不输出。只有当图中文字较多、用户要求检查标签，或需要额外核对术语时才输出；必须与最终 prompt 内嵌文字清单一致。]

## 简短审查提醒
[一句话提醒用户审查科学结构、箭头关系、图中文字、数据边界和期刊要求；如果未指定模型或默认使用丰富标签，可顺带说明需要时可再提供少文字标签版]
```

如果用户明确说"只要 prompt"，只输出 `## 最终绘图提示词（[模型名]）`。

### 迭代优化输出（第 2 轮起）

```markdown
## 变更摘要（第 N 轮）
[3-6 条：本轮反馈的问题定位、对应的修改动作；哪些部分保持不变。]

## 优化后的绘图提示词（第 N 轮 · [模型名]）
[完整可复制 prompt，基于上一版最小改动修订而来。]

## 简短审查提醒
[沿用首轮的一句话提醒，可省略如果上一轮已经提示过且本轮无新增风险点。]
```

如果用户明确说"只要 prompt"，只输出 `## 优化后的绘图提示词（第 N 轮 · [模型名]）`。

## 期刊正文图与事实内容

不要阻止用户生成期刊投稿正文图提示词。正文科研示意图、机制图、图形摘要和方法图都可以生成 prompt。

如果用户提到投稿、正文图、SCI、期刊图，只做简短审查提醒：生成后需要作者检查科学准确性、标签、数据边界和期刊要求。

如果用户要求真实数据图、显微图、实验照片、事实性图像修补或数据结果图，要提醒：不要让绘图模型编造、修补或改写事实证据；但主输出仍然聚焦于提示词生成。

## 不做的事

- 除非用户明确要求，不要推荐或解释 Excalidraw、draw.io、Figma、Illustrator、Vectorizer、Edit-Banana、Paper2Any、视频教程、去水印或矢量化流程。这个 Skill 的边界就是"从科研内容生成/优化绘图提示词"。
- 不生成 Nano Banana Pro、Nano Banana 2、gpt-image-2 之外的其他模型专属 prompt，除非用户明确要求且接受这超出本 Skill 调优范围。
- 不在一次响应中输出多个模型的完整 prompt（见 `references/model-cards.md`）；一次只产出一个确认模型的版本。
- 不做跨会话的迭代历史持久化；多轮迭代仅在当前对话上下文内有效，不写入任何本地文件。
- 不调用任何图像生成 API 或外部服务；`scripts/extract_research_doc.py` 只做本地文本抽取，不联网、不调用 LLM。
