# Phase 8：Write Paper（论文撰写与学术表达）

## 阶段定位

在科研流程中：

```text
Phase 0  Foundation Preparation
        ↓
Phase 1  Literature Mapping
        ↓
Phase 2  Identify Research Gap
        ↓
Phase 3  Formulate Research Question
        ↓
Phase 4  Generate Research Ideas
        ↓
Phase 5  Refine Methodology
        ↓
Phase 6  Design & Conduct Experiments
        ↓
Phase 7  Analyze Results
        ↓
Phase 8  Write Paper
        ↓
Peer Review & Revision
```

**Phase 8 是将已经产生的科学发现转化为可被同行理解、评价和传播的学术成果。**

科研过程不是：

> 做出了方法 → 自动成为论文。

而是：

> 研究问题 + 方法 + 证据 + 解释 → 形成一个完整的科学论证故事。

---

对于计算机科学和人工智能领域：

> 论文不是实验报告，而是一种“科学论证结构”。

一篇优秀AI论文不是告诉别人：

> “我们训练了一个模型，结果比别人高。”

而是告诉同行：

> “现有方法在某类问题上存在根本限制，我们提出了一种针对该限制的新机制，并通过系统实验验证其有效性。”

---

# 一、Phase 8 的主要工作内容

Phase 8 可以拆解为：

```text
1. 确定论文核心故事（Research Story）
2. 提炼科学贡献（Contribution Extraction）
3. 构建论文结构（Paper Structure）
4. 撰写各章节内容
5. 设计图表与实验展示
6. 强化逻辑链
7. 调整学术表达
8. 准备投稿材料
```

---

# 1. 确定论文核心故事（Research Story）

这是写论文最重要的一步。

很多研究者的问题：

有大量实验结果，但没有故事。

---

论文故事应该回答：

```text
Why?
 ↓
What?
 ↓
How?
 ↓
Evidence?
 ↓
Impact?
```

---

典型AI论文故事：

## 问题：

当前LLM存在幻觉问题。

↓

## 缺口：

现有方法依赖外部检索，但无法验证生成内容。

↓

## 方法：

提出检索-生成-验证框架。

↓

## 证据：

多个benchmark提升。

↓

## 洞察：

验证机制提高事实可靠性。

---

这就是论文主线。

---

# 2. 提炼科学贡献（Contribution Extraction）

论文不是展示所有工作。

需要回答：

> 这篇论文对领域新增了什么？

---

AI论文贡献通常有4类：

---

## 贡献1：新方法（Method Contribution）

例如：

> 提出一种新的训练框架。

形式：

“We propose a novel framework for XXX.”

---

## 贡献2：新理论解释（Theoretical Contribution）

例如：

> 解释为什么某类模型有效。

---

## 贡献3：新数据/benchmark（Dataset Contribution）

例如：

> 构建新的评测体系。

---

## 贡献4：新发现（Empirical Discovery）

例如：

> 发现某种训练规律。

---

注意：

“模型更高分”本身不是贡献。

贡献应该是：

> 为什么这个提升具有普遍价值。

---

# 3. 构建论文结构（Paper Structure）

计算机科学和AI论文通常采用：

```text
Title

Abstract

1. Introduction

2. Related Work

3. Method

4. Experiments

5. Analysis

6. Conclusion
```

---

下面逐部分说明。

---

# 3.1 Title（标题）

目标：

一句话体现：

* 方法
* 问题
* 创新点

---

差：

> A New Deep Learning Model

太泛。

---

好：

> Improving Long-Context Reasoning in LLMs via Adaptive Retrieval Planning

包含：

* 问题：Long-context reasoning
* 方法：Adaptive Retrieval Planning

---

# 3.2 Abstract（摘要）

摘要不是简介。

它应该包含：

```text
Problem

↓

Gap

↓

Method

↓

Result

↓

Impact
```

---

典型结构：

## 第一句：

领域问题：

> Large language models suffer from...

## 第二句：

已有不足：

> Existing approaches fail because...

## 第三句：

你的方法：

> We propose...

## 第四句：

结果：

> Experiments show...

## 第五句：

意义：

> Our findings suggest...

---

# 3.3 Introduction（引言）

Introduction是论文最重要部分。

目标：

建立：

> 为什么需要这项研究？

---

通常5段结构：

---

## 第一段：背景

说明领域重要性。

例如：

> LLMs have demonstrated remarkable capability...

---

## 第二段：已有方法

说明：

别人做了什么。

---

## 第三段：问题缺口

关键：

指出：

> 为什么已有方法还不够？

---

## 第四段：你的方法

说明：

> 我们提出什么？

---

## 第五段：贡献总结

通常：

```
Our contributions are:
1.
2.
3.
```

---

# 3.4 Related Work（相关工作）

目标：

证明：

你理解领域。

不是：

论文列表。

---

错误：

> A做了XX，B做了YY。

---

正确：

按照思想分类：

```text
Existing Methods

├── Retrieval-based Methods

├── Reasoning-based Methods

└── Verification-based Methods
```

然后说明：

你的方法位于哪里。

---

# 3.5 Method（方法）

这是AI论文核心。

需要回答：

> 你的方法具体是什么？

包括：

---

## Overall Framework

通常：

Figure 1。

展示：

输入 → 模块 → 输出。

---

## Component Details

解释：

每个模块：

* 为什么存在？
* 如何工作？
* 数学形式？

---

## Algorithm

例如：

伪代码。

---

## Complexity Analysis

例如：

计算成本。

---

# 3.6 Experiments（实验）

目标：

证明：

方法有效。

包括：

---

## Experimental Setup

说明：

* Dataset
* Baseline
* Metric
* Implementation

---

## Main Results

核心表格。

---

## Ablation Study

证明：

模块必要。

---

## Additional Analysis

例如：

* efficiency
* robustness
* case study

---

# 3.7 Analysis（分析）

这是高质量论文的重要区别。

不是只放结果。

需要：

解释：

为什么。

---

包括：

* Error analysis
* Visualization
* Mechanism analysis
* Scaling analysis

---

# 3.8 Conclusion（总结）

回答：

三个问题：

1. 做了什么？
2. 发现什么？
3. 意义是什么？

---

# 4. 设计图表与实验展示

AI论文中：

图表本身就是论证工具。

---

重要图：

## Figure 1：

方法框架图。

回答：

> 方法是什么？

---

## Table 1：

主结果。

回答：

> 是否有效？

---

## Figure 2：

机制分析。

回答：

> 为什么有效？

---

## Table 2：

消融。

回答：

> 每个设计是否必要？

---

# 5. 强化论文逻辑链（Scientific Argumentation）

优秀论文需要：

每句话服务于：

核心论点。

---

逻辑：

```text
Problem

↓

Limitation

↓

Need

↓

Method

↓

Evidence

↓

Conclusion
```

---

常见错误：

Method很强，但是：

不知道解决什么问题。

---

# 6. 学术表达优化（Academic Writing）

AI论文写作重点：

---

## 准确

避免：

> significantly improves

如果没有统计支持。

---

## 简洁

不要：

复杂表达。

---

## 可验证

避免：

> Obviously

科学论文没有“显然”。

---

# 7. 投稿材料准备

包括：

---

## Paper

论文主体。

---

## Supplementary Material

例如：

* 更多实验
* 参数
* 证明

---

## Code/Data Release

AI领域越来越重要。

---

## Cover Letter

说明：

* 为什么适合会议
* 贡献是什么

---

# 二、Phase 8 的边界（Boundary）

Phase 8非常容易出现错误。

---

# ❌ 不重新创造研究贡献

写论文阶段：

不要：

为了让故事更漂亮：

增加不存在的创新。

---

例如：

实验发现：

方法提高效率。

不要写：

> 方法解决了模型理解机制问题。

---

# ❌ 不修改数据迎合故事

禁止：

* 删除失败实验
* 选择性报告结果
* 修改实验条件

---

# ❌ 不无限补实验

写论文过程中：

发现缺实验：

可以补充。

但不要：

无限扩展研究。

---

# ❌ 不把论文写成代码说明书

AI论文不是：

“我们用了PyTorch实现”。

重点：

科学贡献。

---

# ❌ 不堆砌相关工作

Related Work不是综述。

目标：

定位自己的贡献。

---

# 三、Phase 8 验证目标（Validation Goals）

Phase 8结束，需要证明：

> 研究成果已经被组织成一个清晰、可信、可评价的科学论证。

---

# Validation 1：Story Coherence Test（故事完整性）

检查：

论文是否形成：

```text
Problem
 ↓
Gap
 ↓
Question
 ↓
Method
 ↓
Evidence
 ↓
Contribution
```

---

如果：

Introduction讲A。

Method解决B。

Experiment证明C。

论文失败。

---

# Validation 2：Contribution Clarity Test

读完摘要和引言：

别人能回答：

> 这篇论文贡献是什么？

---

标准：

3句话以内。

---

# Validation 3：Evidence Support Test

每个claim是否有证据。

例如：

Claim：

> 方法提高鲁棒性。

Evidence：

多个domain测试。

---

不能：

没有实验支撑。

---

# Validation 4：Novelty Test

检查：

与已有论文区别。

---

回答：

> 如果去掉你的方法，领域损失什么？

---

# Validation 5：Reproducibility Test

AI领域特别重要。

检查：

别人是否能复现？

包括：

* 数据
* 代码
* 参数
* 实验设置

---

# Validation 6：Reviewer Perspective Test

模拟审稿人：

可能问：

---

## Q1：

为什么这个问题重要？

## Q2：

为什么已有方法不行？

## Q3：

你的方法为什么有效？

## Q4：

实验是否充分？

## Q5：

贡献是否足够？

---

# Validation 7：Venue Fit Test

检查：

投稿目标是否匹配。

例如：

NeurIPS：

偏：

* 方法创新
* 理论

ICLR：

偏：

* 学习机制

CVPR：

偏：

* 视觉任务

---

# 四、Phase 8 最终交付物（Deliverables）

---

## 1. Manuscript（论文初稿）

完整：

* Abstract
* Introduction
* Method
* Experiment
* Conclusion

---

## 2. Contribution Statement

明确：

```
Contribution 1:

Contribution 2:

Contribution 3:
```

---

## 3. Figure/Table Package

包括：

* 主图
* 实验表
* 分析图

---

## 4. Supplementary Material

包括：

* 额外实验
* 参数
* 证明

---

## 5. Submission Package

包括：

* Paper
* Code
* Dataset
* Appendix

---

# 五、Phase 8 完成后的能力状态

研究者角色变化：

| 阶段      | 角色    |
| ------- | ----- |
| Phase 0 | 学习者   |
| Phase 1 | 领域观察者 |
| Phase 2 | 问题发现者 |
| Phase 3 | 问题定义者 |
| Phase 4 | 方案创造者 |
| Phase 5 | 方法设计者 |
| Phase 6 | 实验执行者 |
| Phase 7 | 科学解释者 |
| Phase 8 | 知识传播者 |

---

# 六、Phase 7 与 Phase 8 的核心区别

|      | Phase 7            | Phase 8                  |
| ---- | ------------------ | ------------------------ |
| 核心问题 | 结果意味着什么？           | 如何告诉别人？                  |
| 输出   | Scientific Insight | Scientific Communication |
| 重点   | 解释                 | 表达                       |
| 对象   | 自己理解               | 同行理解                     |
| 产物   | 结论                 | 论文                       |

---

# 七、AI科研完整流程串联

例如：

## Phase 2

发现：

> RAG在复杂推理中失败。

↓

## Phase 3

RQ：

> 如何提高RAG多跳推理能力？

↓

## Phase 4

Idea：

> 引入规划机制。

↓

## Phase 5

Method：

> Planning-based RAG。

↓

## Phase 6

实验：

多个benchmark提升。

↓

## Phase 7

分析：

发现：

规划改善检索路径。

↓

## Phase 8

论文：

标题：

> Improving Multi-hop Reasoning in LLMs via Retrieval Planning

核心故事：

> 现有RAG缺少推理规划，我们提出规划增强机制并验证其有效性。

---

# 一句话总结

**Phase 8 Write Paper 的本质，是把“个人完成的一项研究工作”转化为“整个学术共同体可以理解、评价、引用的知识贡献”。**

对于AI科研：

Phase 4决定有没有想法；
Phase 5决定想法是否成为方法；
Phase 6决定是否有证据；
Phase 7决定是否理解自己的发现；
Phase 8决定这个发现能否进入科学共同体。
