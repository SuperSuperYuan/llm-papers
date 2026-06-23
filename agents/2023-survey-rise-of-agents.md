# The Rise and Potential of Large Language Model Based Agents: A Survey

- **作者**：Zhiheng Xi, Wenxiang Chen, Xin Guo, Wei He 等（共 28 位作者）
- **机构**：复旦大学 NLP 组（Fudan NLP）等
- **发表**：arXiv:2309.07864（2023-09）· 综述（~86 页）
- **链接**：[arXiv](https://arxiv.org/abs/2309.07864)
- **主题标签**：`#agent` `#survey` `#multi-agent` `#agent-society` `#overview`

## 一句话总结

> 一篇约 86 页的 LLM agent 全景综述：提出「**脑（brain）— 感知（perception）— 行动（action）**」的统一 agent 框架，系统梳理单 agent、多 agent、人-agent 协作三类应用场景，并探讨「agent 社会」中的行为模式与社会涌现现象。

## 背景与动机

- LLM agent 研究爆发式增长但散乱，需要一个统一的概念框架与全局地图。
- 把 LLM 视为通向 AGI 的「火花」，从哲学渊源（agent 的定义）讲到工程实现，建立系统性认知。

## 核心内容（框架）

**统一框架：Brain – Perception – Action**

- **Brain（脑）**：以 LLM 为核心，负责记忆、知识、推理、规划、决策。
- **Perception（感知）**：把多模态环境输入（文本/视觉/听觉）转化为 agent 可理解的表示，扩展感知空间。
- **Action（行动）**：通过文本、工具调用、具身行动等影响环境，扩展行动空间。

**三类应用场景**：

1. **单 agent**：自主完成任务。
2. **多 agent**：协作（合作/竞争/辩论）完成复杂任务。
3. **人-agent 协作**：人在回路，bridging 人类与 AI。

**Agent 社会**：模拟社会中 agent 的行为、人格、社会涌现现象及其对人类社会的启示，以及随之而来的风险。

## 个人评注

- 启发：建立全局观的最佳入口之一，brain-perception-action 框架清晰，适合作为 agent 领域的「地图」对照具体工作定位。
- 关联：本仓库 agents/ 下的 [[2022-react]]、[[2023-reflexion]]、[[2023-generative-agents]] 等都可对号入座到此框架的不同模块；多 agent 部分与 [[2025-anthropic-multi-agent-research]] 的工程实践互为印证。
- 关联 [[2023-survey-autonomous-agents]]：两篇综述视角互补——本文偏「能力框架 + 社会」，另一篇偏「构建模块 + 评测」。
- 局限：综述时点为 2023 年中，未覆盖此后的推理模型、computer-use、大规模工业落地等进展。
