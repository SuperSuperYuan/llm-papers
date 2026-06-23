# 智能体与工具使用

> ReAct、工具调用、规划、多智能体、自主任务执行

## 论文清单

| 论文 | 年份 | 笔记 | 一句话总结 |
|------|------|------|-----------|
| [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) | 2022 | [笔记](2022-react.md) | 推理与行动交替（思考→行动→观察循环），LLM 调用外部工具的底层 agent 范式 |
| [Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761) | 2023 | [笔记](2023-toolformer.md) | 自监督让模型自学调用工具：采样 API 调用、按「是否降低预测损失」筛选后微调 |
| [An LLM Compiler for Parallel Function Calling](https://arxiv.org/abs/2312.04511) | 2023 | [笔记](2023-llm-compiler.md) | 编译器思想编排工具调用：Planner 生成可并行 DAG，并发执行，较 ReAct 最高 3.7× 加速、6.7× 降本 |
| [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) | 2023 | [笔记](2023-reflexion.md) | 语言化反思 + 情景记忆替代权重更新，跨 trial 积累经验自我改进（HumanEval 91% pass@1） |
| [Language Agent Tree Search (LATS)](https://arxiv.org/abs/2310.04406) | 2023 | [笔记](2023-lats.md) | 把 MCTS 引入 language agent，统一推理/行动/规划，LLM 兼任行动者与价值评估 |

---

返回 [仓库首页](../README.md)
