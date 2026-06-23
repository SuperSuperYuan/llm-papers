# Building Effective Agents（构建高效的 Agent）

- **作者**：Erik Schluntz, Barry Zhang（Anthropic）
- **机构**：Anthropic
- **发表**：Anthropic 工程博客 · 2024-12-19
- **链接**：[原文](https://www.anthropic.com/research/building-effective-agents)
- **主题标签**：`#agent` `#engineering` `#workflow` `#best-practice` `#industry` `#anthropic`

## 一句话总结

> Anthropic 的实战工程指南：先把 **workflow（预定义代码路径编排 LLM/工具）** 与 **agent（LLM 自主决定流程与工具）** 区分开；强调**从简单做起、只在确有收益时才加复杂度**，别过早上框架、别过早上多 agent——并给出 5 种可组合的 workflow 模式与 3 条核心原则。

## 背景与动机

- 业界一谈 agent 就堆叠复杂框架与多 agent，常常得不偿失。
- Anthropic 基于大量客户落地经验总结：多数场景**优化好的单次 LLM 调用或简单 workflow 就够了**，真正需要自主 agent 的场景有限。

## 核心内容

**基础构件：Augmented LLM（增强型 LLM）**——LLM + 检索 + 工具 + 记忆，是一切 agentic 模式的基本单元。

**Workflow（确定性编排）vs Agent（动态自主）**：关键区分。workflow 路径由代码预定义；agent 由 LLM 动态决定流程和工具使用。

**5 种 workflow 模式**（按复杂度递增、可组合）：

1. **Prompt chaining 提示链**：把任务拆成固定的顺序步骤，逐步 LLM 调用。
2. **Routing 路由**：先分类输入，再分发给专门的处理器。
3. **Parallelization 并行化**：并行子任务，或多次采样投票（sectioning / voting）。
4. **Orchestrator-workers 编排者-工人**：中心 LLM 动态拆分并委派给 worker LLM。
5. **Evaluator-optimizer 评估-优化**：生成 → 评估 → 反馈迭代精修的闭环。

**何时该用 agent**：仅用于**开放式、解题路径不可预测、需长程自主**的问题；且必须在沙盒中充分测试、配好 guardrails。

**3 条核心原则**：
1. 保持设计**简单（simplicity）**；
2. 通过**显式规划步骤**保证**透明（transparency）**；
3. 精心设计并测试 **agent-computer 接口（ACI）/ 工具文档**。

## 个人评注

- 启发：对抗「为了 agent 而 agent」的最佳清醒剂——「只在确有收益时才加复杂度」「workflow 往往就够」应作为 agent 工程的默认心态。ACI（工具接口设计与人机接口同等重要）的提法很实用。
- 关联 [[2025-anthropic-multi-agent-research]]：本文主张「别过早上多 agent」，姊妹篇则给出**真正值得上多 agent 时**的落地经验，二者互为正反面、配套阅读。
- 关联 [[2023-self-refine]]（evaluator-optimizer 的思想源）、[[2022-react]]（agent 自主循环的范式基础）、[[2023-llm-compiler]]（parallelization 的工程化）。
- 局限：是工程经验/方法论而非实证论文，无量化基准；具体模式选择仍需按场景权衡。
