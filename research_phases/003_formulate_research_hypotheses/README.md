# Phase 3：Formulate Research Question（构建研究问题）

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
Phase 4  Generate Preliminary Ideas
        ↓
Phase 5  Optimize Ideas
```

**Phase 3 是从“发现问题”到“定义科学问题”的转换阶段。**

Phase 2回答：

> 现有研究哪里不足？

Phase 3回答：

> 我具体要研究哪个问题？我要证明什么？研究边界在哪里？

---

对于计算机科学和人工智能领域：

> Research Question（RQ）是连接“研究空白”和“技术方案”的桥梁。

很多AI论文失败，不是因为模型设计不好，而是因为：

* 问题定义模糊；
* 研究目标不清；
* 实验无法验证核心贡献。

优秀研究的问题通常不是：

> “我想设计一个新的Transformer。”

而是：

> “当前Transformer在长序列建模中存在二次复杂度问题，能否设计一种保持表达能力同时降低计算复杂度的方法？”

---

# 一、Phase 3 的主要工作内容

Phase 3 可以拆解为：

```text
1. 明确研究对象（What）
2. 定义研究目标（Goal）
3. 建立问题假设（Hypothesis）
4. 界定研究范围（Scope）
5. 确定变量关系（Variables）
6. 设计可验证问题（Testability）
7. 构建Research Question体系
```

---

# 1. 明确研究对象（Define Research Object）

## 目标

回答：

> 我要研究的“东西”到底是什么？

---

AI领域一个问题通常包含：

```
对象(Object)
+
任务(Task)
+
环境(Context)
+
限制(Constraint)
+
目标(Objective)
```

---

例如：

模糊：

> 研究大模型推理能力。

明确：

> 研究大型语言模型在多步数学推理任务中的错误来源，以及如何通过推理增强机制提高可靠性。

拆解：

| 元素 | 内容    |
| -- | ----- |
| 对象 | LLM   |
| 任务 | 数学推理  |
| 场景 | 多步推理  |
| 问题 | 错误    |
| 目标 | 提高可靠性 |

---

# 2. 定义研究目标（Research Objective）

研究问题必须明确：

> 解决什么？

---

常见AI研究目标：

## 提升性能

例如：

> 如何提高小样本分类准确率？

---

## 降低成本

例如：

> 如何减少LLM推理计算成本？

---

## 增强可靠性

例如：

> 如何降低模型幻觉？

---

## 提升理解

例如：

> 为什么Transformer具有强泛化能力？

---

## 扩展能力

例如：

> 如何让模型适应新的领域？

---

注意：

目标不是：

> 做一个更大的模型。

而是：

> 解决某个明确限制。

---

# 3. 建立研究假设（Research Hypothesis）

这是Phase 3的核心。

一个好的研究问题背后应该有：

> 可验证的预测。

---

## AI例子

Gap：

> RAG在多跳问题中效果差。

普通问题：

> 如何改进RAG？

研究问题：

> 是否可以通过显式规划检索路径提高LLM多跳问答能力？

对应假设：

> 如果模型能够提前规划检索步骤，则多跳任务准确率会提高。

形式：

```
如果引入X，
那么Y会改善，
因为机制Z。
```

---

# 4. 界定研究范围（Research Scope）

这是博士科研中特别重要的能力。

很多问题失败：

不是没有价值，而是太大。

---

例如：

错误：

> 如何解决人工智能安全问题？

范围过大。

---

缩小：

> 如何检测LLM生成文本中的事实性错误？

进一步：

> 如何利用外部知识验证减少LLM在开放域问答中的幻觉？

---

范围限定：

包括：

## 数据范围

例如：

只研究：

* English QA datasets

---

## 模型范围

例如：

只研究：

* Decoder-only LLM

---

## 场景范围

例如：

只研究：

* Medical QA

---

## 指标范围

例如：

关注：

* factual accuracy

而不是：

* all capability

---

# 5. 确定变量关系（Variables Definition）

理工科尤其AI，需要明确：

---

## Independent Variable（自变量）

你改变什么？

例如：

* 模型结构
* 训练方法
* 数据策略

---

## Dependent Variable（因变量）

观察什么？

例如：

* accuracy
* latency
* robustness

---

## Control Variable（控制变量）

保持什么？

例如：

* dataset
* training budget
* model size

---

例：

研究：

> Prompt optimization是否提高LLM推理能力？

变量：

```
Input:
Prompt strategy

Output:
Reasoning accuracy

Control:
Model, Dataset
```

---

# 6. 构建可验证问题（Make It Testable）

科研问题必须能够被实验或理论验证。

---

## 不好的问题

> 如何让AI更聪明？

无法验证。

---

## 好的问题

> Chain-of-thought prompting是否能够提升小模型在数学推理任务中的表现？

可以设计：

```
Baseline:
normal prompting

Method:
CoT prompting

Metric:
accuracy
```

---

# 7. 建立Research Question体系

复杂研究通常不是一个RQ。

通常：

## Main Research Question（主问题）

*

## Sub Research Questions（子问题）

---

例如：

主题：

> Efficient LLM inference

主问题：

RQ:

> How can inference efficiency be improved without sacrificing model capability?

子问题：

RQ1:

> Which components dominate inference cost?

RQ2:

> Can KV cache be optimized?

RQ3:

> What accuracy-efficiency tradeoff exists?

---

# 二、Phase 3 的边界（Boundary）

Phase 3 非常容易越界。

---

# ❌ 不设计具体算法

错误：

RQ阶段：

> 我要使用Graph Neural Network解决问题。

这是Phase 4。

---

正确：

> 如何利用结构信息提高模型泛化能力？

---

# ❌ 不展开实验

Phase 3 不应该：

* 下载数据集
* 调模型
* 跑benchmark

实验属于Phase 6。

---

# ❌ 不追求最终答案

Phase 3不是：

> 找解决方案。

而是：

> 精确定义问题。

---

# ❌ 不把工程需求当科研问题

例如：

工程：

> 我要开发一个聊天机器人。

科研：

> 当前对话模型在长期记忆保持方面存在什么机制限制？

---

# 三、Phase 3 验证目标（Validation Goals）

Phase 3结束，需要证明：

> 我的研究问题是清晰、重要、可研究、可验证的。

---

# Validation 1：Problem Clarity Test（问题清晰性）

测试：

能否一句话描述？

---

差：

> 研究AI效率。

好：

> 研究如何降低Transformer长序列推理中的计算复杂度。

---

标准：

别人听完知道：

* 研究对象
* 问题
* 目标

---

# Validation 2：Research Gap Alignment Test

RQ必须来自gap。

检查：

```
Research Gap
      ↓
Research Question
```

是否一致。

---

例：

Gap：

> LLM hallucination

RQ：

> 如何提高LLM训练速度？

失败。

因为：

没有对应关系。

---

# Validation 3：Novelty Test（新颖性）

检查：

已有论文是否已经回答？

搜索：

关键词：

```
Research Question keywords
+
survey
+
benchmark
+
review
```

---

如果已有：

完整解决。

需要重新定义。

---

# Validation 4：Feasibility Test（可行性）

考虑：

## 时间

博士：

3-5年。

硕士：

半年-两年。

---

## 资源

是否需要：

* 百万美元GPU？
* 大规模数据？
* 特殊设备？

---

## 技术能力

是否具备：

* 数学基础？
* 编程能力？
* 实验条件？

---

# Validation 5：Falsifiability Test（可证伪性）

这是科学问题核心。

好的RQ：

允许：

“你的假设可能错误。”

---

例如：

好：

> Method X是否提高LLM reasoning accuracy？

结果：

可能：

提高 / 不提高。

---

坏：

> 如何证明我的方法有效？

因为：

预设答案。

---

# Validation 6：Contribution Test（贡献潜力）

问：

如果解决：

贡献是什么？

可能贡献：

## 方法贡献

提出新算法。

## 理论贡献

解释机制。

## 数据贡献

新benchmark。

## 系统贡献

提升部署能力。

---

# 四、Phase 3 最终交付物（Deliverables）

---

## 1. Research Question Document

模板：

```
Title:

Background:

Existing limitation:

Research Gap:

Main Research Question:

Sub Questions:

Hypothesis:

Expected Contribution:

Evaluation Plan:
```

---

## 2. Problem Definition

明确：

```
Input:
Output:
Objective:
Constraint:
Evaluation:
```

---

## 3. Research Hypothesis

例如：

```
H1:
Introducing retrieval planning improves multi-hop QA accuracy.

H2:
The improvement comes from better evidence selection.
```

---

## 4. Scope Statement

明确：

```
This work focuses on...

This work does not address...
```

---

# 五、Phase 3 完成后的能力状态

阶段变化：

| 阶段      | 研究者状态 |
| ------- | ----- |
| Phase 0 | 学习者   |
| Phase 1 | 领域观察者 |
| Phase 2 | 问题发现者 |
| Phase 3 | 问题定义者 |
| Phase 4 | 方案设计者 |

---

# 六、Phase 2 与 Phase 3 的核心区别

这是科研训练中最关键的区别：

|      | Phase 2      | Phase 3           |
| ---- | ------------ | ----------------- |
| 核心问题 | 哪里有不足？       | 我要研究哪个不足？         |
| 输出   | Research Gap | Research Question |
| 形式   | 描述缺陷         | 提出问题              |
| 例子   | LLM存在幻觉      | 如何降低LLM幻觉？        |
| 关注   | Why?         | What exactly?     |

---

# 一句话总结

**Phase 3 Formulate Research Question 的本质，是把“领域中的模糊不足”转化为一个可以被科学验证的问题。**

对于AI科研：

低水平研究：

> 我有一个模型想法，然后找问题。

高水平研究：

> 我发现一个重要问题，定义它，然后寻找最合适的方法解决它。

Phase 3 做得越好，后面的 Idea、Experiment、Paper 成功率越高。
