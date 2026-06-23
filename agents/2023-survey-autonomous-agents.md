# A Survey on Large Language Model based Autonomous Agents

- **作者**：Lei Wang, Chen Ma, Xueyang Feng 等（中国人民大学高瓴人工智能学院团队）
- **机构**：Renmin University of China (Gaoling School of AI) 等
- **发表**：Frontiers of Computer Science (FCS) · arXiv:2308.11432（2023-08，2025 修订）
- **链接**：[arXiv](https://arxiv.org/abs/2308.11432) · [配套仓库](https://github.com/Paitesanshi/LLM-Agent-Survey)
- **主题标签**：`#agent` `#survey` `#agent-architecture` `#evaluation` `#overview`

## 一句话总结

> 从「如何构建、如何应用、如何评测」三问题出发的 LLM 自主 agent 综述：提出统一的 agent 构建框架——**Profile（人设）/ Memory（记忆）/ Planning（规划）/ Action（行动）** 四模块，并系统梳理其在社会科学、自然科学、工程领域的应用与评测方法。

## 背景与动机

- LLM 让 agent 首次具备接近人类水平的知识与决策能力，相关工作激增但缺乏统一的构建与评测视角。
- 目标：用一个模块化框架统一描述各种 agent 设计，并整理应用与评测，给研究者一张可操作的蓝图。

## 核心内容（框架）

**统一构建框架（四模块）**：

1. **Profiling（人设模块）**：定义 agent 的角色/身份（手工指定、LLM 生成或数据集对齐）。
2. **Memory（记忆模块）**：结构、格式、读写与反思机制，支撑长期行为。
3. **Planning（规划模块）**：有/无反馈的规划，任务分解与策略制定。
4. **Action（行动模块）**：把决策落为具体行动（含工具使用），影响环境。

**应用领域**：社会科学、自然科学、工程三大类。

**评测**：系统梳理主观（人评/LLM 评）与客观（指标/benchmark）的 agent 评测策略，并维护配套仓库持续追踪。

## 个人评注

- 启发：Profile/Memory/Planning/Action 四模块是设计/拆解一个 agent 的实用 checklist；评测章节尤其有价值，agent 评测一直是难点。
- 关联 [[2023-survey-rise-of-agents]]：两篇并读最佳——本文给「构建模块 + 评测」的工程蓝图，另一篇给「能力框架 + 社会」的全景。
- 关联 [[2023-generative-agents]]（Memory 模块的范例）、[[2023-plan-and-solve]] / [[2023-tree-of-thoughts]]（Planning 模块的范例）、[[2022-react]] / [[2023-toolformer]]（Action 模块的范例）。
- 局限：综述本质是快照；agent 领域演进极快，需结合最新工作与工业实践（如 Anthropic 的 [[2024-building-effective-agents]]）补充。
