# How We Built Our Multi-Agent Research System（多 Agent 研究系统的工程实践）

- **作者**：Anthropic 工程团队
- **机构**：Anthropic
- **发表**：Anthropic 工程博客 · 2025-06-13
- **链接**：[原文](https://www.anthropic.com/engineering/built-multi-agent-research-system)
- **主题标签**：`#agent` `#multi-agent` `#orchestrator-worker` `#engineering` `#industry` `#anthropic` `#evaluation`

## 一句话总结

> Anthropic 把 Claude 的 Research 功能做成**编排者-工人（orchestrator-worker）** 多 agent 系统的真实落地复盘：lead agent 拆解问题、并行派发 subagent 各自探索再汇总；多 agent 比单 agent 在内部评测上提升 **90.2%**，但**约 15× token 消耗**——并给出 prompt 工程、评测、生产可靠性的一手教训。

## 背景与动机

- 研究类任务开放、不可预测，不适合固定 pipeline；需要动态、自适应的信息发现（区别于静态 RAG）。
- 多 agent 的价值：**并行探索**（subagent 各查一个方向，压缩海量信息）、**token 扩展**（给难题分配更多算力——token 用量解释了 80% 的网页检索性能方差）、**关注点分离**（独立上下文减少路径依赖）。

## 核心内容

**架构：Orchestrator-Worker**
- **Lead agent（编排者）**：分析查询、制定策略、派生多个专门 subagent。
- **Subagents（工人）**：各自独立搜索、用 extended thinking 评估信息、返回发现。
- Lead 综合所有 subagent 结果产出答案。

**Prompt 工程 8 条教训（节选）**：
1. 像 agent 一样逐步模拟以暴露失败模式；
2. 教会委派——给清晰的目标/输出格式/工具指引/任务边界；
3. 让投入匹配难度（按查询复杂度分配资源）；
4. **工具接口和人机接口一样关键**，糟糕的工具描述会带偏 agent；
5. 让 agent 自我改进（Claude 能诊断失败并改进 prompt）；
6. **先广后窄**——agent 默认查询过于具体，应先引导宽探索；
7. 用 extended thinking 作「可控的草稿纸」引导规划；
8. 并行化执行（subagent 并行用多工具，研究时间最多减 90%）。

**评测**：确定性路径假设对 agent 失效——用小样本（~20 例）早期快速迭代、用 LLM-as-judge 按 rubric（准确性/引用/完整性/来源质量/效率）打分、辅以人工测试发现边缘问题（如 agent 偏好 SEO 内容农场而非权威 PDF）。

**生产可靠性**：有状态的错误处理与断点续跑、全链路可观测性（监控决策模式而非对话内容）、彩虹部署（渐进切流量不打断运行中的 agent）；当前 lead 同步等待所有 subagent 是瓶颈。

**何时值得用多 agent**：高价值任务、可重并行、信息超单上下文、复杂工具生态——值得；需要全程共享上下文、agent 间强依赖（如多数编码任务）、低价值任务、实时协调——不值得。

## 个人评注

- 启发：把「多 agent 何时真正划算」量化了（15× token、80% 方差由 token 解释）——多 agent 的本质收益常常是「给难题砸更多 token/并行算力」，而非结构本身的魔力。
- 关联 [[2024-building-effective-agents]]：姊妹篇主张「别过早上多 agent」，本文给出「确实该上时」的工程细节，正反配套。
- 关联 [[2023-llm-compiler]]（并行执行的另一种工程化）、[[2023-survey-rise-of-agents]]（多 agent 协作的理论框架）。
- 关联 [[2026-onereason]] 等工业技术报告：同属「工程落地经验」一类，强调 prototype 到 production 的鸿沟与复合误差。
- 局限：经验性复盘、面向 Anthropic 自身系统；同步编排、成本高等限制仍未解。
