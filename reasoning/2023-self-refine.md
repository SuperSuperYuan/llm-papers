# Self-Refine: Iterative Refinement with Self-Feedback

- **作者**：Aman Madaan, Niket Tandon, Prakhar Gupta, Skyler Hallinan, Luyu Gao, Sarah Wiegreffe, Uri Alon, Nouha Dziri, Shrimai Prabhumoye, Yiming Yang, Shashank Gupta, Bodhisattwa Prasad Majumder, Katherine Hermann, Sean Welleck, Amir Yazdanbakhsh, Peter Clark
- **机构**：CMU / Allen Institute for AI (AI2) / University of Washington / NVIDIA / Google DeepMind 等
- **发表**：NeurIPS 2023 · arXiv:2303.17651（2023-03）
- **链接**：[arXiv](https://arxiv.org/abs/2303.17651)
- **主题标签**：`#reasoning` `#self-refine` `#self-feedback` `#iterative` `#prompting` `#test-time`

## 一句话总结

> 同一个模型「自己产出 → 自己批评 → 据此修改」反复迭代：无需额外训练或 RL，仅靠 **generate → feedback → refine** 的推理时循环，就能让 GPT-3.5/GPT-4 等模型的输出平均提升约 20% 绝对分。

## 背景与动机

- 人类写作/解题往往是先出草稿、再自我审阅修改的迭代过程。
- 现有 LLM 多是「一次性生成」，缺少这种自我精修；而引入外部评判器或训练成本高。能否**只用模型自身**完成反馈与改进？

## 核心方法

- **三步循环（同一个 LLM 扮演三个角色）**：
  1. **Generate**：先产出初始输出；
  2. **Feedback**：对自己的输出生成**具体、可操作**的批评/建议；
  3. **Refine**：根据反馈修订输出。
  - 反复迭代直到满足停止条件（收敛或达到轮数上限）。
- **训练-free**：纯提示，无需标注、无需微调、无需额外模型；反馈是自然语言而非标量分数。

## 实验与结论

- **模型**：GPT-3.5、ChatGPT、GPT-4。
- **任务**：7 类多样任务，从对话回复生成到数学推理、代码优化等。
- **结果**：相比一次性生成，**平均约 +20% 绝对提升**，人类偏好与自动指标均验证。

## 个人评注

- 启发：把「迭代自我反馈」确立为推理时通用增益手段；关键洞见是反馈必须**具体可执行**，否则 refine 无从下手。
- 关联 [[2023-reflexion]]：同为自我反馈，但 Self-Refine 在**单个任务的单次输出内**精修，Reflexion 跨**多个 episode**用外部反馈 + 记忆积累。
- 关联 [[2022-chain-of-thought]]、[[2023-plan-and-solve]]：同属推理时计算路线，但本文增益来自「修订」而非「分步/规划」。
- 局限：弱模型的自我反馈质量有限（自评天花板）；某些任务自我批评不可靠，可能越改越差；迭代带来额外 token 成本。
