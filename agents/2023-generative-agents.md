# Generative Agents: Interactive Simulacra of Human Behavior

- **作者**：Joon Sung Park, Joseph C. O'Brien, Carrie J. Cai, Meredith Ringel Morris, Percy Liang, Michael S. Bernstein
- **机构**：Stanford University / Google DeepMind（Google Research）
- **发表**：UIST 2023 · arXiv:2304.03442（2023-04）
- **链接**：[arXiv](https://arxiv.org/abs/2304.03442)
- **主题标签**：`#agent` `#memory` `#memory-stream` `#reflection` `#planning` `#simulation` `#multi-agent`

## 一句话总结

> 「斯坦福小镇」：用 LLM 驱动 25 个可信的拟人 agent，核心是**记忆流（memory stream）+ 检索（按时近性/重要性/相关性）+ 反思（reflection）+ 规划（planning）** 的架构，使 agent 能记住经历、提炼洞见、规划日程，并在沙盒里**涌现**出传播聚会邀请、自发约会、协同赴会等社会行为。

## 背景与动机

- 要让 agent 长期、可信地模拟人类，需要解决：如何**记住**大量经历、如何把零散记忆**提炼**成高层理解、如何据此**连贯地规划**未来行为——单靠 LLM 上下文窗口做不到。
- 目标：构建能长时间运行、行为可信、可交互的生成式 agent，并研究其社会涌现。

## 核心方法

**记忆-反思-规划架构**：

1. **Memory Stream 记忆流**：以自然语言完整记录 agent 的所有经历（observation），按时间排列。
2. **Retrieval 检索**：取记忆时综合三个维度打分——**recency（时近性）、importance（重要性）、relevance（与当前情境的相关性）**，挑出最相关的记忆喂给 LLM。
3. **Reflection 反思**：周期性地把底层观察**综合成更高层的抽象洞见**（如「我对某人/某事的看法」），反思本身也作为记忆存入流中，可层层递进。
4. **Planning 规划**：把高层日程**递归细化**为具体行动，并随环境变化重规划；行动结果又回写记忆流。

**评测环境 Smallville**：受《模拟人生》启发的交互沙盒，25 个 agent 自主生活、用自然语言交互。

## 实验与结论

- **涌现社会行为**：仅给一个 agent「办情人节派对」的初始意图，agent 们便自发**传播邀请、建立新关系、相约结伴、协同到场**——无脚本编排。
- **消融研究**：去掉 observation / planning / reflection 任一组件，行为可信度都显著下降——三者各自重要。

## 个人评注

- 启发：memory 研究最经典的奠基工作，确立了「记忆流 + recency/importance/relevance 检索 + 反思」这套被后续大量 agent/记忆系统沿用的范式。
- 关联 [[2023-reflexion]]：都把「反思」作为核心，但 Reflexion 面向任务试错改进，Generative Agents 面向长期拟人模拟与社会涌现。
- 关联 [[2023-memgpt]]：二者都在攻克「LLM 记忆/长期性」，本文偏认知架构（记忆怎么组织/提炼），MemGPT 偏系统机制（上下文怎么分层调度）。
- 关联 [[2022-react]]：可视为带长期记忆与社会环境的 agent，行动-观察循环之上加了记忆与反思层。
- 局限：成本高（大量 LLM 调用）；评测偏定性/可信度，缺乏严格任务指标；长期记忆的真实性与一致性仍有限。
