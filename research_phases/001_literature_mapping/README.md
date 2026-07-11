# Phase 1：Literature Mapping（文献地图构建）

## 阶段定位

在完整科研流程中：

```
Phase 0 基础准备
        ↓
Phase 1 Literature Mapping
        ↓
Phase 2 Identify Research Gap
        ↓
Phase 3 Formulate Research Question
```

**Phase 1 的核心任务不是“读论文”，而是建立一个研究领域的结构化认知模型。**

对于计算机科学（CS）和人工智能（AI）领域，Phase 1 的本质是：

> 从“我知道一些论文”转变为“我知道这个领域的问题空间、方法空间、评价体系和发展方向”。

最终目标：

你应该能够回答：

> “这个方向过去解决了什么问题，现在有哪些路线，为什么这些路线有效或无效，未来可能在哪里突破？”

---

# 一、Phase 1 的主要工作内容

Phase 1 可以拆解为：

```
1. 界定研究空间（Research Scope Definition）
2. 构建文献集合（Literature Collection）
3. 文献分类与编码（Taxonomy Construction）
4. 方法演化分析（Method Evolution Analysis）
5. Benchmark与评价体系理解
6. 研究趋势分析（Trend Analysis）
7. 初步问题池建立（Problem Pool）
```

---

# 1. 界定研究空间（Research Scope Definition）

## 目标

确定：

> “我要绘制哪一块知识地图？”

---

## AI领域例子

假设兴趣：

> 大模型

太宽：

```
Artificial Intelligence
```

缩小：

```
Large Language Models
```

继续：

```
LLM Reasoning
```

继续：

```
Test-time Scaling for LLM Reasoning
```

最终：

```
How to improve reasoning ability of LLM during inference?
```

---

## 工作内容

定义：

### 研究对象（Object）

例如：

* Transformer
* CNN
* Diffusion Model
* Reinforcement Learning Agent

### 任务（Task）

例如：

* Classification
* Generation
* Retrieval
* Reasoning
* Planning

### 场景（Scenario）

例如：

* Medical
* Robotics
* Autonomous Driving

### 约束条件（Constraint）

例如：

* Low data
* Low compute
* Real-time
* Privacy

最终形成：

```
研究空间 =
对象 + 任务 + 场景 + 限制
```

---

# 2. 构建文献集合（Literature Collection）

## 目标

建立：

> 代表性论文集合，而不是论文堆积。

---

## 文献来源

AI/CS主要：

### 顶级会议

例如：

机器学习：

* NeurIPS
* ICML
* ICLR

计算机视觉：

* CVPR
* ICCV
* ECCV

自然语言：

* ACL
* EMNLP

人工智能：

* AAAI
* IJCAI

### 预印本

* arXiv

---

## 文献层级

不要随机搜索。

建议：

```
Level 1:
Survey / Review Paper

        ↓

Level 2:
Foundational Papers

        ↓

Level 3:
State-of-the-art Papers

        ↓

Level 4:
Recent Papers
```

---

例如研究RAG：

第一批：

* RAG综述

第二批：

* 原始RAG论文

第三批：

* Dense Retrieval
* Agentic RAG
* Graph RAG

第四批：

* 最近一年改进方法

---

# 3. 文献分类与编码（Taxonomy Construction）

这是Phase 1最核心工作。

很多新人：

> 看完100篇论文，但是不知道它们之间关系。

原因：

没有建立taxonomy。

---

## 目标

建立：

```
问题
 |
方法
 |
模型
 |
优缺点
 |
发展方向
```

---

## AI例子：目标检测

早期：

```
Traditional CV
 |
Feature Engineering
 |
HOG + SVM
```

↓

深度学习：

```
CNN detector

├── Two-stage
│     └── Faster R-CNN
│
└── One-stage
      ├── YOLO
      └── SSD
```

↓

Transformer：

```
DETR
 |
End-to-end Detection
```

---

最终不是记论文：

而是：

```
方法A解决问题X
但是存在限制Y

方法B改进Y
但是产生问题Z
```

---

# 4. 方法演化分析（Method Evolution）

## 核心问题：

为什么方法会发展？

---

AI研究通常：

不是：

旧方法 → 新方法

而是：

```
Problem
 ↓
Existing Solution
 ↓
Limitation
 ↓
New Idea
 ↓
New Solution
```

---

例如：

CNN：

解决：

> 图像空间特征提取

限制：

> 长距离依赖

Transformer：

解决：

> 全局建模

限制：

> 计算成本

新的研究：

> Efficient Transformer

---

Phase 1需要建立：

```
方法演化链
```

---

# 5. Benchmark与评价体系理解

AI领域特别重要。

很多新人只看模型。

但科研评价依赖：

```
Method
 +
Dataset
 +
Metric
 +
Baseline
```

---

例如：

研究LLM：

必须知道：

Benchmark：

* MMLU
* HumanEval
* GSM8K

指标：

* Accuracy
* Pass@k
* BLEU
* ROUGE

---

需要理解：

为什么这个benchmark重要？

它测量什么能力？

有什么缺陷？

---

# 6. 研究趋势分析（Trend Analysis）

目标：

判断：

> 哪些方向正在增长，哪些已经成熟。

---

分析：

## 时间趋势

例如：

2018：

CNN dominates

2020：

Transformer rise

2023：

LLM explosion

---

## 论文数量趋势

例如：

关键词：

```
"RAG"
"Agent"
"Multimodal LLM"
```

增长速度。

---

## 社区关注点

例如：

以前：

模型规模

现在：

* Efficiency
* Alignment
* Reasoning
* Reliability

---

# 7. 初步问题池建立（Problem Pool）

注意：

Phase 1不是找gap。

但是应该产生：

“问题候选”。

---

例如：

阅读100篇RAG论文后：

发现：

```
Problem Pool

P1:
Retrieval quality limitation

P2:
Long context inefficiency

P3:
Hallucination

P4:
Evaluation difficulty
```

---

区别：

Phase 1：

> 我发现有哪些问题。

Phase 2：

> 哪个问题值得解决？

---

# 二、Phase 1 的边界（Boundary）

非常重要。

---

# 不属于Phase 1的事情

## ❌ 1. 不追求创新方案

错误：

读20篇论文：

> 我要提出一个新模型。

原因：

知识地图还没完成。

---

## ❌ 2. 不大量调模型

例如：

下载代码：

改参数：

跑实验。

这属于：

Phase 5/6。

---

## ❌ 3. 不深入单篇论文细节

例如：

花两个月研究某篇论文数学证明。

可能浪费。

Phase 1关注：

全局结构。

---

## ❌ 4. 不追求发表

Phase 1产出：

不是paper。

而是：

research map。

---

# Phase 1结束时，你应该停止：

继续无限阅读。

典型陷阱：

```
我再读10篇论文
↓
再读50篇
↓
再读100篇
```

永远不会进入研究。

结束条件应该由能力决定。

---

# 三、Phase 1 验证目标（Validation Goals）

Phase 1的核心验证：

> 你是否已经拥有“研究领域地图”，可以开始寻找research gap？

---

## Validation 1：领域地图测试

要求：

画出：

```
Research Area

├── Problem Category A
│
├── Problem Category B
│
├── Method Family
│
├── Dataset
│
└── Open Challenges
```

---

例如：

LLM Agent：

```
LLM Agent

├── Planning
│
├── Tool Use
│
├── Memory
│
├── Reflection
│
├── Evaluation
```

---

通过标准：

别人问：

“这个方向有哪些路线？”

你能回答。

---

# Validation 2：论文定位能力

给你一篇新论文。

要求：

回答：

* 它属于哪个类别？
* 它解决什么问题？
* 它改进谁？
* 它相比已有方法创新在哪里？

---

# Validation 3：Method Comparison能力

能够制作：

| Method | Idea        | Strength | Weakness  |
| ------ | ----------- | -------- | --------- |
| A      | CNN         | Fast     | Local     |
| B      | Transformer | Global   | Expensive |
| C      | Hybrid      | Balance  | Complex   |

---

---

# Validation 4：复述领域发展历史

例如：

能够讲：

```
2015:
CNN-based methods

2018:
Attention mechanism

2020:
Transformer

2023:
Foundation Models
```

并解释：

为什么发生变化。

---

# Validation 5：提出Problem Pool

至少产生：

5~10个候选问题。

例如：

```
Problem 1:
Current models fail under low-resource conditions

Problem 2:
Evaluation is unreliable
```

---

# 四、Phase 1 最终交付物（Deliverables）

建议：

## 1. Literature Map

核心产物。

形式：

* 思维导图
* Markdown知识库
* Notion
* Obsidian

---

## 2. Paper Database

例如：

```
papers/

├── foundation
├── survey
├── method_A
├── method_B
├── benchmark
└── recent
```

---

## 3. Taxonomy Document

类似：

```
Research Landscape of XXX

1. Problem Definition

2. Existing Methods

3. Evolution

4. Limitations

5. Open Problems
```

---

## 4. Benchmark Summary

包括：

* Dataset
* Metric
* Baseline

---

## 5. Problem Pool

进入Phase 2。

---

# 五、Phase 1完成后的能力状态

进入Phase 0：

> 我会读论文。

进入Phase 1：

> 我知道论文在哪里。

完成Phase 1：

> 我知道这个领域的问题结构。

能力变化：

| 阶段        | 认知                |
| --------- | ----------------- |
| Phase 0   | 什么是AI研究           |
| Phase 1初期 | 有哪些论文             |
| Phase 1后期 | 有哪些方法、为什么发展、哪里有问题 |

---

## 一句话总结

**Phase 1 Literature Mapping 的本质不是“收集论文”，而是在大脑中建立一个可导航的研究地图。**

完成这一阶段后，你不应该成为某个方法的专家，而应该成为：

> 一个能够站在领域全局视角，判断“下一步应该研究什么”的初级研究者。
