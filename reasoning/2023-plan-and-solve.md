# Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning by Large Language Models

- **作者**：Lei Wang, Wanyu Xu, Yihuai Lan, Zhiqiang Hu, Yunshi Lan, Roy Ka-Wei Lee, Ee-Peng Lim
- **机构**：Singapore Management University / 华东师范大学 / SUTD 等
- **发表**：ACL 2023 · arXiv:2305.04091（2023-05）
- **链接**：[arXiv](https://arxiv.org/abs/2305.04091)
- **主题标签**：`#cot` `#reasoning` `#prompting` `#zero-shot` `#planning`

## 一句话总结

> 把 zero-shot CoT 的「Let's think step by step」升级为「**先制定计划、再按计划分步执行**」：用 PS / PS+ 提示让模型先把问题分解成子任务再逐一求解，零样本下显著优于 Zero-shot-CoT，数学推理上甚至逼近 8-shot CoT。

## 背景与动机

- Zero-shot-CoT（Kojima 等的「Let's think step by step」）虽简单有效，但存在三类典型错误：
  1. **计算错误**（calculation errors）；
  2. **步骤缺失**（missing-step / 推理链不完整）；
  3. **语义理解偏差**（semantic misunderstanding）。
- 目标：在**不引入人工示例（仍是 zero-shot）** 的前提下缓解上述问题。

## 核心方法

- **PS（Plan-and-Solve）提示**：两阶段——
  1. 引导模型「先理解问题、制定解决计划（把任务拆成子任务）」；
  2. 再「按计划执行子任务」得出答案。
  - 即把触发语从「一步步想」改为「先列计划、再逐步执行」。
- **PS+ 提示**：在 PS 基础上加入**更详细的指令**（如「提取相关变量并算出中间结果」「注意计算」），针对性减少计算错误、补全步骤。
- 关键区别：相比 Zero-shot-CoT 的单一触发句，PS 显式引入**规划阶段**，结构化推理过程。

## 实验与结论

- **10 个数据集 / 3 类推理任务**（算术、常识、符号推理）。
- **结果**：
  - 大幅超越 Zero-shot-CoT；
  - 持平或超过 Zero-shot Program-of-Thought（PoT）；
  - 数学推理上与 **8-shot CoT** 表现相当——即用 zero-shot 逼近 few-shot。

## 个人评注

- 启发：用「规划 → 执行」结构化 zero-shot 推理，是 CoT 与「agent 式 planning」之间的桥梁——后续 agent 的 plan-then-execute 思路与此一脉相承。
- 关联 [[2022-chain-of-thought]]：本文是 CoT 的 zero-shot 改进版，直击 CoT 推理链不完整/算错的痛点。
- 关联 [[2022-react]]、[[2023-llm-compiler]]：ReAct/LLMCompiler 在「带工具的行动空间」里做规划与执行；Plan-and-Solve 在「纯文本推理」里做规划与执行——同一思想的不同载体。
- 局限：仍是提示工程，依赖模型本身能力；复杂多跳问题的规划质量不稳定；无外部工具/事实获取。
