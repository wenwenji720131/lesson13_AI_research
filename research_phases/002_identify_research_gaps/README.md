# Phase 2：Identify Research Gap（识别研究空白）

## 阶段定位

在科研流程中：

```
Phase 0  Foundation Preparation
        ↓
Phase 1  Literature Mapping
        ↓
Phase 2  Identify Research Gap
        ↓
Phase 3  Formulate Research Question
        ↓
Phase 4  Generate Preliminary Ideas
```

**Phase 2 是从“理解已有知识”进入“发现未知问题”的关键阶段。**

如果说：

* Phase 1 的问题是：

> “这个领域已经知道什么？”

那么：

* Phase 2 的问题是：

> “这个领域还不知道什么？或者已有方法哪里不够？”

---

对于计算机科学和人工智能领域，Phase 2 的本质是：

> 在已有方法空间中寻找“性能瓶颈、理论缺陷、应用限制或评价空白”，形成值得研究的问题机会。

最终目标：

找到一个：

* 有价值（Important）
* 未解决（Unsolved）
* 可研究（Researchable）
* 可验证（Verifiable）

的问题。

---

# 一、Phase 2 的主要工作内容

Phase 2 可以拆解为：

```
1. 分析已有方法限制
2. 比较方法之间差异
3. 发现性能瓶颈
4. 分析失败案例
5. 寻找理论缺口
6. 发现应用场景缺口
7. 评估研究价值
8. 形成 Research Gap Statement
```

---

# 1. 分析已有方法限制（Method Limitation Analysis）

这是AI领域最常见的gap来源。

Phase 1已经建立：

```
方法A
方法B
方法C
```

Phase 2开始问：

> 为什么这些方法还不够？

---

## 示例1：计算机视觉

已有：

```
CNN
 ↓
ResNet
 ↓
Vision Transformer
```

发现：

CNN：

优势：

* 局部特征强
* 计算效率高

限制：

* 长距离依赖不足

Transformer：

解决：

* 全局建模

新限制：

* 数据需求大
* 计算成本高

于是产生gap：

> 如何设计一种同时具有CNN效率和Transformer全局建模能力的方法？

---

## 常见限制类型

### 1. 性能限制

例如：

准确率不够：

```
Current SOTA = 85%

Need:
>90%
```

---

### 2. 效率限制

例如：

LLM：

问题：

```
模型越来越大
↓
推理成本越来越高
```

Gap：

> 如何降低推理成本同时保持能力？

---

### 3. 泛化限制

例如：

模型：

训练数据：

```
ImageNet
```

现实：

```
Medical images
```

Gap：

> 如何提高domain generalization？

---

### 4. 鲁棒性限制

例如：

自动驾驶：

正常天气：

很好

极端天气：

失败

Gap：

> 如何提升模型在异常环境中的可靠性？

---

# 2. 方法间比较分析（Comparative Analysis）

很多gap不是单个论文发现，而是在比较中发现。

建立：

| Method      | 优势              | 不足                      |
| ----------- | --------------- | ----------------------- |
| CNN         | efficient       | limited receptive field |
| Transformer | global modeling | high cost               |
| Diffusion   | high quality    | slow generation         |

寻找：

```
A解决问题X
但是产生问题Y

B解决Y
但是产生问题Z
```

形成：

研究机会。

---

# 3. 发现性能瓶颈（Performance Bottleneck）

AI研究非常依赖benchmark。

不要只看：

```
Model A > Model B
```

而要问：

为什么？

---

例如：

LLM benchmark：

结果：

```
GPT-X:
MMLU 90%

Human:
95%
```

Gap：

不是：

“提高5%”

而是：

为什么：

* 推理失败？
* 知识不足？
* 长文本理解失败？
* 规划能力不足？

---

## 分析方法

看：

### Error Analysis

例如：

模型错误：

1000个case

分类：

```
30% reasoning failure
40% retrieval failure
20% hallucination
10% other
```

最大问题：

就是gap候选。

---

# 4. 分析失败案例（Failure Case Analysis）

这是AI科研非常重要的方法。

很多顶级论文来自：

> 模型什么时候失败？

---

例如：

自动驾驶模型：

正常：

99%

失败：

* 夜晚
* 雨天
* 遮挡

问题：

不是：

“再提高准确率”

而是：

> 为什么模型不能处理分布外情况？

---

典型流程：

```
Dataset
 ↓
Model
 ↓
Wrong Prediction
 ↓
Error Category
 ↓
Research Problem
```

---

# 5. 寻找理论缺口（Theoretical Gap）

计算机科学不仅是工程。

一些重要gap来自：

“我们不知道为什么有效”。

---

例如：

深度学习：

现象：

大模型泛化很好。

问题：

为什么？

---

产生：

* Scaling law
* Representation learning theory
* Optimization theory

---

理论gap形式：

```
Existing theory explains A

but cannot explain B
```

---

# 6. 应用场景缺口（Application Gap）

AI非常常见。

已有：

实验室有效。

现实：

无法部署。

例如：

医疗AI：

论文：

```
Accuracy 95%
```

但是医院：

问题：

* 数据隐私
* 标注成本
* 跨医院泛化

Gap：

> 如何构建实际可部署系统？

---

# 7. 判断Research Gap价值

不是所有gap值得研究。

需要评价：

---

## 重要性（Importance）

问：

如果解决：

有没有影响？

例如：

降低LLM成本50%

价值高。

---

## 新颖性（Novelty）

问：

别人有没有解决？

---

## 可行性（Feasibility）

问：

博士3年能否完成？

---

## 可验证性（Testability）

问：

有没有实验方法证明？

---

# 8. 形成Research Gap Statement

这是Phase 2最终目标。

格式：

```
Existing methods can solve X.

However, they still suffer from limitation Y.

This limitation becomes critical in scenario Z.

Therefore, a new approach is needed.
```

---

## AI例子

普通：

> 我想研究RAG。

不好。

Research Gap：

> Existing RAG systems improve factual accuracy by retrieving external knowledge, but they still suffer from retrieval errors when queries require multi-hop reasoning. Therefore, improving reasoning-aware retrieval remains an open problem.

---

# 二、Phase 2 的边界（Boundary）

Phase 2最容易犯错误。

---

# ❌ 不进入算法设计

错误：

发现gap：

> LLM幻觉严重。

马上：

设计新模型。

这是Phase 4。

Phase 2只回答：

```
问题是什么？
为什么重要？
为什么已有方法不够？
```

---

# ❌ 不做大规模实验

错误：

跑100个baseline。

Phase 2：

可以：

* 小规模验证

但不是正式实验。

---

# ❌ 不追求解决方案

不要：

```
Gap:
模型慢

Solution:
设计新Transformer
```

这里已经进入Phase 4。

---

# ❌ 不把“性能提升”当gap

错误：

> 当前模型准确率95%，我要提升96%。

这不是研究问题。

应该：

> 当前模型在哪类情况下失败？为什么失败？

---

# 三、Phase 2 验证目标（Validation Goals）

Phase 2结束时，需要证明：

> 我发现的问题是真实存在的，并且值得研究。

---

# Validation 1：Gap真实性验证

问题：

是不是假问题？

---

验证：

检查：

* 最新论文是否仍讨论这个问题？
* benchmark是否体现问题？
* 社区是否关注？

例如：

错误：

> CNN已经过时，所以我要改进CNN。

可能是假gap。

---

# Validation 2：Literature Saturation Test

测试：

是否已经有人解决？

方法：

搜索：

关键词组合：

```
problem + solution
problem + benchmark
problem + survey
```

---

结果：

如果：

已有10篇SOTA解决

gap消失。

---

# Validation 3：Gap明确性测试

一个好的gap：

应该一句话说清。

差：

> AI还有很多问题。

好：

> Current multimodal LLMs lack reliable visual reasoning under long-context scenarios.

---

# Validation 4：Evidence Test

必须有证据：

例如：

论文A：

> limitation

论文B：

> future work

实验：

> failure cases

形成：

```
Evidence → Gap
```

---

# Validation 5：Research Value Test

评分：

| 指标          | 问题       |
| ----------- | -------- |
| Importance  | 解决后影响大吗？ |
| Novelty     | 别人没解决吗？  |
| Feasibility | 能做吗？     |
| Evaluation  | 能验证吗？    |

---

# 四、Phase 2 最终交付物（Deliverables）

## 1. Research Gap Document

核心产物：

结构：

```
Problem:
Existing methods:

Limitation:

Evidence:

Why important:

Potential direction:
```

---

## 2. Gap Matrix

例如：

| Area   | Method | Limitation         | Gap                       |
| ------ | ------ | ------------------ | ------------------------- |
| LLM    | RAG    | Poor retrieval     | Reasoning-aware retrieval |
| Vision | ViT    | High cost          | Efficient attention       |
| RL     | PPO    | Sample inefficient | Better exploration        |

---

## 3. Failure Analysis Report

包括：

* 哪些case失败
* 为什么失败
* 哪类问题最多

---

## 4. Candidate Research Questions

不是方案。

例如：

```
RQ1:
Can retrieval improve multi-hop reasoning?

RQ2:
How can inference cost be reduced?
```

---

# 五、Phase 2完成后的能力状态

进入Phase 1：

> 我知道这个领域有什么。

完成Phase 2：

> 我知道这个领域缺什么。

能力变化：

| 阶段      | 研究者状态 |
| ------- | ----- |
| Phase 0 | 学习者   |
| Phase 1 | 领域观察者 |
| Phase 2 | 问题发现者 |
| Phase 3 | 问题定义者 |

---

# 六、Phase 2与Phase 3的核心区别

这是很多新人混淆的地方。

|    | Phase 2      | Phase 3                        |
| -- | ------------ | ------------------------------ |
| 目标 | 发现gap        | 定义问题                           |
| 回答 | 为什么需要研究？     | 具体研究什么？                        |
| 输出 | Research Gap | Research Question              |
| 关注 | 不足           | 目标                             |
| 例子 | RAG无法处理多跳推理  | 如何设计reasoning-aware retrieval？ |

---

## 一句话总结

**Phase 2 Identify Research Gap 的本质，是从已有知识中找到“值得投入科研资源的未知空间”。**

对于AI科研，优秀的研究者不是问：

> “我能设计什么新模型？”

而是先问：

> “现有模型为什么在某些情况下失败？这个失败背后隐藏着什么更深的问题？”

只有当这个问题被准确识别，后面的 Hypothesis、Idea、Experiment 才有真正的科研价值。
