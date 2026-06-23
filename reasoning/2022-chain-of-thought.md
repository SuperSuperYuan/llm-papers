# Chain-of-Thought Prompting Elicits Reasoning in Large Language Models

- **作者**：Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten Bosma, Brian Ichter, Fei Xia, Ed Chi, Quoc Le, Denny Zhou
- **机构**：Google Research (Brain team)
- **发表**：NeurIPS 2022 · arXiv:2201.11903（2022-01）
- **链接**：[arXiv](https://arxiv.org/abs/2201.11903)
- **主题标签**：`#cot` `#reasoning` `#prompting` `#emergent-ability` `#few-shot`

## 一句话总结

> 在少样本提示里给出带**中间推理步骤**的示例（chain-of-thought 范例），就能让大模型在回答前先「一步步想」，从而在算术、常识、符号推理等复杂任务上大幅提升——而且这种能力**随模型规模涌现（emergent）**，无需任何额外训练。

## 背景与动机

- 标准少样本提示（直接「问题→答案」）在需要多步推理的任务上表现很差，且单纯扩大模型也难以解决。
- 直觉：人类解复杂问题会分解成中间步骤。能否让模型也显式生成这些中间步骤？

## 核心方法

- **Chain-of-Thought Prompting**：在 few-shot 示例中，把每个范例的答案替换为「中间推理过程 + 最终答案」。模型据此模仿，在新问题上也先输出推理链再给答案。
- **零额外训练**：纯提示技巧，不改权重；只需 ~8 个示例。
- 与标准提示的关键区别：把「一步到位」变成「显式分解推理」，使模型把计算/逻辑分摊到多个生成步。

## 实验与结论

- **模型**：在 PaLM 540B、GPT、LaMDA 等多个大模型上测试。
- **基准**：GSM8K（数学应用题）、SVAMP、算术、常识推理、符号推理等。
- **关键结果**：
  - PaLM 540B 仅用 8 个 CoT 示例即在 GSM8K 上达到 SOTA，**超过当时经过微调的基线**。
  - **涌现性**：CoT 的收益只在足够大的模型上才显著出现；小模型用 CoT 反而可能更差。

## 个人评注

- 启发：这是「推理时计算 / test-time reasoning」的标志性起点之一——后续 self-consistency、ToT、o1/R1 式长思维链、推理 RL 都建立在「让模型显式生成中间步骤」之上。
- 关联 [[2022-react]]：ReAct 把 CoT 的「思考」嵌入带外部观察的行动循环；CoT 是 agent 推理能力的底座。
- 关联 [[2012-mcts-survey]]、[[2019-the-bitter-lesson]]：同属「用更多推理/搜索算力换性能」的思路；Bitter Lesson 视角下，CoT 是让计算在推理时可扩展的通用手段。
- 关联 [[2026-onereason]]：OneReason 正是想把 CoT 范式迁移到生成式推荐，却发现物品 token 构不成有意义的推理链——反衬出 CoT 依赖语言 token 语义这一前提。
- 局限：依赖模型规模（涌现）；推理链可能「看似合理实则错误」（不忠实）；纯闭环、无法获取外部事实（→ 催生 ReAct/检索增强）。
