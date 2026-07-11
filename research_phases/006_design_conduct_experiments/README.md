# Phase 6：Design & Conduct Experiments（实验设计与执行）

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
```

**Phase 6 是把“方法设计”转化为“科学证据”的阶段。**

前面的阶段解决：

* 为什么研究？（Why）
* 研究什么？（What）
* 怎么解决？（How）

Phase 6解决：

> 我的方法是否真的有效？为什么有效？在哪些情况下有效或失败？

---

对于计算机科学和人工智能领域：

> Phase 6 不等于“跑代码得到一个数字”，而是设计一套能够支撑科学结论的验证体系。

优秀实验不是证明：

> 我的模型准确率最高。

而是证明：

> 我的核心假设成立，并且提升来自提出的方法机制，而不是偶然因素。

---

# 一、Phase 6 的主要工作内容

Phase 6 可以拆解为：

```text
1. 实验目标定义（Experiment Objective）
2. 实验环境准备（Experimental Setup）
3. Benchmark与数据设计
4. Baseline选择
5. 实验方案设计
6. 模型训练与运行
7. 超参数与公平性控制
8. Ablation实验
9. 敏感性分析
10. 失败案例分析
```

---

# 1. 实验目标定义（Experiment Objective）

## 目标

首先明确：

> 这个实验要证明什么？

---

很多初学者错误：

```text
训练模型
↓
看结果
↓
寻找解释
```

这是工程试错。

科研应该：

```text
Hypothesis
↓
Experiment
↓
Evidence
↓
Conclusion
```

---

例如：

Phase 5提出：

方法：

> 引入动态检索机制提升LLM推理能力。

实验目标不是：

> 看准确率。

而是：

验证三个假设：

### H1：

动态检索提高推理准确率。

### H2：

提升来自更好的信息选择。

### H3：

动态检索比固定检索更有效。

---

对应：

| 假设 | 实验                     |
| -- | ---------------------- |
| H1 | Performance comparison |
| H2 | Retrieval analysis     |
| H3 | Ablation               |

---

# 2. 实验环境准备（Experimental Setup）

## 目标

建立可重复实验条件。

---

包括：

## 硬件

AI领域：

* GPU型号
* 显存
* CPU
* RAM

例如：

```text
8 × NVIDIA A100
```

---

## 软件环境

包括：

* Python版本
* PyTorch版本
* CUDA版本
* Framework

---

## 随机性控制

AI非常重要：

设置：

* random seed
* multiple runs

原因：

一次实验结果可能只是随机波动。

---

# 3. Benchmark与数据设计

这是AI科研核心。

---

## 3.1 Dataset选择

需要回答：

> 为什么选择这个数据集？

---

例如：

研究LLM数学推理：

选择：

* GSM8K
* MATH

原因：

测试：

multi-step reasoning。

---

## 3.2 数据划分

通常：

```text
Dataset

├── Training set
├── Validation set
└── Test set
```

---

避免：

test数据泄漏。

---

## 3.3 数据规模

需要说明：

* 使用多少数据？
* 为什么？

---

例如：

小样本研究：

重点：

不是数据越多越好。

而是：

验证：

方法在低资源情况下有效。

---

# 4. Baseline选择

这是论文可信度的重要来源。

---

实验不能只比较：

```text
Your Method
vs
Old Method
```

需要：

代表性baseline。

---

通常：

## Baseline 1：传统方法

证明：

超过经典方法。

---

## Baseline 2：当前SOTA

证明：

达到竞争水平。

---

## Baseline 3：最近相关方法

证明：

相比直接竞争者优势。

---

例如：

研究Transformer优化：

需要：

| 方法          | 作用   |
| ----------- | ---- |
| Transformer | 原始基线 |
| Longformer  | 相关方法 |
| BigBird     | SOTA |
| Your method | 提出方法 |

---

# 5. 实验方案设计（Experimental Design）

这是Phase 6核心。

---

## 5.1 主实验（Main Experiment）

回答：

> 方法有没有效果？

形式：

```text
Method       Accuracy

Baseline A      80

Baseline B      82

Ours            86
```

---

但是：

只有主实验通常不足。

---

# 5.2 对比实验（Comparison Experiment）

目的：

证明：

不是简单堆资源。

---

控制：

* 参数量
* 数据量
* 训练时间

---

例如：

错误：

你的模型：

70B参数

baseline：

7B参数

提升没有意义。

---

# 5.3 Ablation实验（消融实验）

AI论文最重要实验之一。

回答：

> 每个设计是否必要？

---

例如：

方法：

```text
Full Model

A模块
B模块
C模块
```

实验：

| 模型     | 结果 |
| ------ | -- |
| Base   | 80 |
| +A     | 83 |
| +A+B   | 85 |
| +A+B+C | 87 |

证明：

每个组件贡献。

---

# 5.4 Sensitivity Analysis（敏感性分析）

研究：

参数变化影响。

---

例如：

LLM：

temperature：

```text
0.1
0.5
1.0
```

观察：

稳定性。

---

模型：

embedding size：

```text
128
256
512
```

观察：

性能变化。

---

# 5.5 Efficiency Evaluation（效率实验）

AI越来越重要。

不仅看：

accuracy。

还看：

* training cost
* inference latency
* memory usage
* FLOPs

---

例如：

方法A：

Accuracy:
90%

Cost:
100 GPU hours

方法B：

Accuracy:
89%

Cost:
10 GPU hours

实际价值可能更高。

---

# 6. 模型训练与运行（Execution）

正式执行：

包括：

---

## Training

例如：

* pre-training
* fine-tuning

---

## Validation

调整：

* learning rate
* batch size
* epochs

---

## Testing

最终：

固定模型。

在test set评价。

---

# 7. 超参数与公平性控制

AI实验容易被质疑：

> 你的提升是不是因为调参？

---

需要：

说明：

* hyperparameter search范围
* 使用相同预算
* 相同数据

---

例如：

公平：

```text
All methods:
Same training data
Same compute budget
Same evaluation metric
```

---

# 8. 失败案例分析（Failure Case Analysis）

优秀论文不仅展示成功。

还分析：

失败在哪里。

---

例如：

模型：

总体：

90% accuracy

失败：

100个case：

分类：

```text
30 reasoning error
40 retrieval error
30 ambiguity
```

发现：

未来改进方向。

---

# 二、Phase 6 的边界（Boundary）

Phase 6 是科研流程中最容易失控的阶段。

---

# ❌ 不无限调参

错误：

> 再调100组参数，总能提高。

问题：

可能过拟合benchmark。

---

正确：

有限调参。

记录：

实验过程。

---

# ❌ 不修改研究问题迎合结果

危险：

实验失败：

于是改变目标：

> 本来研究性能，现在研究效率。

这是研究漂移。

---

# ❌ 不只追求最高数字

错误：

> 我的模型+0.2%，所以成功。

科研需要：

解释：

为什么提升。

---

# ❌ 不隐藏负结果

失败实验也是信息。

例如：

发现：

方法只适用于小模型。

这是重要发现。

---

# ❌ 不引入未经设计的新模块

实验过程中：

发现效果不好：

加入：

* 新loss
* 新模块
* 新数据

如果改变核心方法：

需要重新经过Phase 4/5。

---

# 三、Phase 6 验证目标（Validation Goals）

Phase 6结束需要证明：

> 方法有效，并且实验结果可信。

---

# Validation 1：Hypothesis Validation

核心。

检查：

```text
Hypothesis

↓

Experiment Result

↓

Support / Reject
```

---

例如：

假设：

> 动态检索提升推理。

结果：

准确率提高。

支持。

---

# Validation 2：Fair Comparison Test

验证：

比较公平。

检查：

* 数据一致？
* 参数规模一致？
* 训练预算一致？
* 指标一致？

---

# Validation 3：Statistical Reliability Test

AI越来越重视。

包括：

## 多次运行

例如：

5 runs。

报告：

mean ± std。

---

## 显著性分析

例如：

判断提升是否只是随机。

---

# Validation 4：Ablation Validation

证明：

核心机制有效。

问题：

如果删除核心模块：

性能是否下降？

如果：

没有下降。

说明：

模块可能没用。

---

# Validation 5：Generalization Test

验证：

是否只适合一个数据集。

---

例如：

训练：

ImageNet

测试：

CIFAR

Medical dataset

---

优秀方法：

不是：

只在一个benchmark赢。

---

# Validation 6：Robustness Test

测试：

异常情况。

例如：

* noisy data
* distribution shift
* adversarial examples

---

# Validation 7：Efficiency Test

尤其AI。

证明：

性能提升是否值得成本。

---

# 四、Phase 6 最终交付物（Deliverables）

---

# 1. Experimental Protocol

实验设计文档：

包括：

```text
Research Question:

Hypothesis:

Dataset:

Baseline:

Metric:

Experiment:

Expected Result:
```

---

# 2. Experimental Results

包括：

## Main Table

核心结果。

## Ablation Table

组件贡献。

## Efficiency Table

资源消耗。

## Case Study

失败/成功案例。

---

# 3. Experiment Log

非常重要。

记录：

* code version
* configuration
* random seed
* results

保证：

可复现。

---

# 4. Analysis Report

不是：

“我们的模型最好”。

而是：

解释：

为什么。

---

# 五、Phase 6 完成后的能力状态

研究者角色变化：

| 阶段      | 角色    |
| ------- | ----- |
| Phase 0 | 学习者   |
| Phase 1 | 领域观察者 |
| Phase 2 | 问题发现者 |
| Phase 3 | 问题定义者 |
| Phase 4 | 方案创造者 |
| Phase 5 | 方法设计者 |
| Phase 6 | 证据生产者 |

---

# 六、Phase 5 与 Phase 6 的核心区别

|      | Phase 5 | Phase 6  |
| ---- | ------- | -------- |
| 核心问题 | 方法怎么设计？ | 方法是否有效？  |
| 输出   | Method  | Evidence |
| 活动   | 设计      | 执行       |
| 代码   | 原型      | 正式实验     |
| 结果   | 预期      | 真实数据     |

---

# 七、AI科研完整例子串联

## Phase 2 Gap

发现：

> LLM在多跳推理中容易失败。

---

## Phase 3 RQ

> 如何提高LLM多跳推理可靠性？

---

## Phase 4 Idea

> 引入规划机制。

---

## Phase 5 Method

设计：

Planning + Retrieval + Verification框架。

---

## Phase 6 Experiment

实验：

### Dataset：

* HotpotQA
* MuSiQue

### Baseline：

* GPT-4
* Standard RAG

### Metrics：

* Accuracy
* Evidence correctness

### Ablation：

去掉：

* Planning
* Verification

### Analysis：

发现：

提升主要来自：

更准确的信息选择。

---

# 一句话总结

**Phase 6 Design & Conduct Experiments 的本质，是把“我认为这个方法有效”转化为“我有严格证据证明这个方法为什么有效”。**

对于AI科研：

低水平实验：

> 跑一个benchmark，得到一个更高数字。

高水平实验：

> 设计一套证据链，证明研究假设、方法机制和实际价值之间存在因果关系。

Phase 6 做得好，论文才真正从“一个想法”变成“科学贡献”。
