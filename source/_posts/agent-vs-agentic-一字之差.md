---
title: 一字之差：Agent 和 Agentic 到底有什么区别？
date: 2026-04-24 22:45:00
tags: [AI, Agent, Agentic, LLM]
categories: [技术思考]
---

# 一字之差：Agent 和 Agentic 到底有什么区别？

如果你最近在看 AI 圈的内容，肯定遇到过这两个词：

- "Claude Code 是一个 **Agent**"
- "GPT-5 的 **Agentic** 能力大幅提升"
- "我们在做一个 **Agentic** workflow"
- "DeepSeek V4 是开源最强 **Agent** 模型"

听上去差不多，**但混着用会出大问题**。最近就看到一个真实场景：同事看到"DeepSeek V4 Agent 能力提升"的发布说明，第一反应是："它出 CLI 了？没出怎么提升 Agent 能力？"

这个困惑的根源就是没分清这两个词。今天用最少的废话讲清楚。

## 一、定义先放出来

**Agent**（名词）：一个完整的**系统/产品**
- 模型 + 工具 + 调度逻辑 + 用户界面
- 你可以"用"一个 Agent，因为它是个东西
- 例子：Claude Code、Cursor、Devin、AutoGPT、Cline

**Agentic**（形容词）：描述某个事物的**"能动性"程度**
- 形容词，修饰属性
- 你不能"用一个 Agentic"，但可以说"这个模型很 Agentic"
- 例子：Agentic capability（能动能力）、Agentic workflow（能动工作流）、Agentic benchmark（能动评测）

一个是**实体**，一个是**形容词**。语法上的区别其实最关键。

## 二、用一个具体的例子拆开

假设你看到这句话：

> "Claude Opus 4.7 在 SWE-bench 上达到 SOTA，agentic 能力领先 GPT-5。"

正确解读：

- **Claude Opus 4.7** 是个**模型**（不是 Agent）
- **SWE-bench** 是测**模型**在 agent 场景下表现的 benchmark
- **agentic 能力**是说这个**模型**有多擅长"自主多步操作"

这里**没有任何一个 Agent 出现**。整句话讨论的全是**模型属性**。

再看另一句：

> "Claude Code 是 Anthropic 出的 coding agent，背后跑的是 Claude 模型。"

正确解读：

- **Claude Code** 是 **Agent**（系统/产品）
- 它**封装**了 Claude 模型 + 工具 + UI
- 它的"能力强"由两部分决定：模型 agentic 能力 + 工程封装质量

**Agent 是容器，Agentic 是容器里那个核心驱动力的描述。**

## 三、为什么容易混

三个原因。

**第一：词根相同。** Agent 和 Agentic 来自同一个词，中文翻译又重叠 —— 都跟"代理/智能体"有关。

**第二：英文新闻稿混着写。** 连 Anthropic、OpenAI 自己的 blog 也经常混用。比如 "agent capability" 和 "agentic capability" 在很多文档里被当同义词。严格说，"agent capability" 应该指系统能力，"agentic capability" 才是模型能力，但实际语料里混了。

**第三：中文语境放大了混乱。** 中文里"智能体"既可以翻 Agent 也可以翻 Agentic。"智能体能力" 这种说法天然歧义 —— 是说一个智能体（Agent）的能力？还是说"智能体性的"（Agentic）能力？分不清。

## 四、一个能记一辈子的类比

把 AI Agent 系统想成一辆**自动驾驶汽车**：

| | 对应 | 解释 |
|---|---|---|
| **Agent**（系统） | 整辆车 | 包含底盘、传感器、控制软件、屏幕 |
| **Model**（核心） | 决策算法/AI 芯片 | 这辆车的"大脑" |
| **Agentic 能力** | 那块芯片的"自主决策水平" | 能不能在复杂路况下自己做对决定 |

- "我买了辆 Tesla" = 我有了个 **Agent**（系统）
- "Tesla 的 FSD 算法 agentic 能力很强" = 它的**核心模型**自主决策能力强
- "Tesla 的 agentic 能力提升" = 算法升级了（不是车壳子重做了）

Tesla 升级 FSD 算法的时候，**不会顺便重新发布一辆车**。同理，DeepSeek 升级模型的 agentic 能力，**不需要顺便发个 CLI**。

## 五、为什么必须分清：评测和选型场景

混淆这两个词，会在两个场景出大问题。

### 场景 1：看 benchmark

下面两种 benchmark 完全不同：

| Benchmark 类型 | 测什么 | 例子 |
|---|---|---|
| **Agentic benchmark**（模型评测） | 单一模型在标准 harness 下的能动能力 | SWE-bench、TAU-bench、METR、Terminal-bench |
| **Agent benchmark**（系统评测） | 一个完整产品的端到端用户体验 | 各种 leaderboard、用户主观评分、A/B 测试 |

**Agentic benchmark 控制变量是模型** —— 所有模型套同一个 harness，比的是模型本身。

**Agent benchmark 测的是产品** —— Claude Code 和 Cursor 都用 Claude Opus，但用户体验可能完全不同，因为工程实现、UI、上下文管理策略都不一样。

如果你看 SWE-bench 分数选模型，但拿这个分数评 Cursor 好不好用，就南辕北辙了。

### 场景 2：技术选型

假设你公司要做一个内部 AI coding 工具：

- **如果 Agent 不行**（产品体验差）：换 harness 或自研
- **如果模型 agentic 不行**（再好的工具也救不回来）：换底层模型

这两个决策路径完全不一样。混淆了就会做错动作 —— 比如"产品不好用 → 决定换个模型"，结果新模型 agentic 能力一样，啥也没改善。

正确思路：**先定位是哪一层的问题**。同样的模型在另一个 Agent 里好用吗？同样的 Agent 换个模型能改善吗？两个对照实验做完，问题就锁定了。

## 六、对照表：以后看到这两个词怎么读

| 句子 | 正确解读 |
|---|---|
| "我们在做一个 **agent**" | 我们在做一个产品/系统 |
| "我们在做 **agentic** workflow" | 我们在设计一种自主多步执行的工作流 |
| "这个模型 **agent** 能力强" | 表述不严谨，应该是 "agentic 能力强"，意思是模型自主执行能力强 |
| "Claude Code 是个 coding **agent**" | 一个 coding 产品/系统 |
| "Opus 4.7 **agentic** SOTA" | 这个模型在能动评测上排第一 |
| "**Agent** = Model × Harness" | 系统 = 模型 × 工程封装 |
| "**Agentic** capability is trainable" | 能动能力是可以训练出来的（指模型层面） |

## 七、一句话总结

**Agent 是名词，是产品；Agentic 是形容词，是属性。**

- 你**用** Agent
- 你**评估** Agentic 能力
- Agent 由模型 + 工程组成
- 模型的 agentic 能力是 Agent 整体表现的**上限**

下次再看到这两个词，先问自己：**这句话在讨论一个完整系统，还是在讨论模型的某个属性？** 区分清楚了，AI 圈一半的发布说明就能看懂了。

---

## 附：常用术语速查

- **Agent / AI Agent**：智能体系统、AI 应用
- **Agentic**：能动的、自主的（形容词）
- **Agentic capability / agentic ability**：模型的自主执行能力
- **Agentic workflow**：能动工作流（多步自主决策的工作流）
- **Agentic benchmark**：能动评测（测模型自主能力）
- **Agent framework**：Agent 框架（构建 Agent 的工程脚手架，如 LangChain、CrewAI）
- **Harness**：外壳/壳子（指 Agent 系统中模型外的所有工程部分）
