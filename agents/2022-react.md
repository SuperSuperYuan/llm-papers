# ReAct: Synergizing Reasoning and Acting in Language Models

- **作者**：Shunyu Yao, Jeffrey Zhao, Dian Yu, Nan Du, Izhak Shafran, Karthik Narasimhan, Yuan Cao
- **机构**：Princeton University / Google Research (Brain team)
- **发表**：ICLR 2023 · arXiv:2210.03629（2022-10）
- **链接**：[arXiv](https://arxiv.org/abs/2210.03629)
- **主题标签**：`#agent` `#react` `#reasoning` `#tool-use` `#planning` `#prompting`

## 一句话总结

> 把**推理（reasoning）**与**行动（acting）**交替进行：让模型在「思考（thought）→ 行动（action）→ 观察（observation）」的循环里，一边用推理轨迹规划/追踪/更新计划，一边用行动调用外部工具（如 Wikipedia）获取信息——这是几乎所有现代 agent 的底层范式。

## 背景与动机

- 此前 LLM 的「推理」（如 CoT）与「行动」（如调用工具/与环境交互）被当作**两个独立课题**研究。
- 纯 CoT 在闭环内推理，无法获取外部知识、易**幻觉与错误传播**；纯 acting 又缺乏高层规划与抽象。
- ReAct 主张二者协同：推理指导该采取什么行动，行动返回的观察又反过来支撑推理。

## 核心方法

- **Thought–Action–Observation 循环**：
  - *Thought*：自由形式的推理，用于归纳、追踪、更新行动计划，分解目标。
  - *Action*：在动作空间内执行（如 `search[entity]`、`lookup[string]`、`finish[answer]`），与外部环境/知识源交互。
  - *Observation*：环境返回的结果，作为下一步推理的输入。
- **少样本提示**即可工作（in-context examples，无需微调），可与外部 API（Wikipedia 检索）结合。
- 与 CoT 的关键区别：CoT 是静态、闭环的推理链；ReAct 让推理与外部交互**动态交错**，可纠错、可获取最新事实。

## 实验与结论

- **知识密集型 QA / 事实核查**：HotpotQA、FEVER —— 相比纯 CoT 显著**降低幻觉**；CoT 与 ReAct 结合（互为补充）效果最佳。
- **交互式决策**：ALFWorld（文本家务）、WebShop（网购）——相比模仿学习 / 强化学习基线，成功率分别**绝对提升 34% / 10%**，且仅用极少 in-context 示例。
- **优势**：可解释（人能读懂思考轨迹）、可控、错误更易诊断与纠正。

## 个人评注

- 启发：这是 agent 范式的奠基工作——「LLM + 工具 + 循环」的最小可用闭环。后续 AutoGPT、LangChain agent、Tool-use、Plan-and-Execute 等几乎都是 ReAct 的扩展或变体。
- 关联 [[2022-chain-of-thought]]：ReAct 把 CoT 的「思考」从闭环搬进了带外部观察的交互循环；二者互补。
- 关联 [[2023-toolformer]]：Toolformer 用训练让模型「学会」调用工具，ReAct 用提示让模型「在循环中决定」调用工具——一个改权重、一个改流程。
- 关联 [[2012-mcts-survey]]：同属「test-time 推理/搜索」思路，但 ReAct 的搜索发生在真实外部环境而非模拟树中。
- 局限：依赖提示工程与动作空间设计；长程任务中观察噪声/上下文长度仍是瓶颈。
