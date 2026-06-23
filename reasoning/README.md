# 推理与思维链

> Chain-of-Thought、自一致性、推理时计算、数学与代码推理

## 论文清单

| 论文 | 年份 | 笔记 | 一句话总结 |
|------|------|------|-----------|
| [A Survey of Monte Carlo Tree Search Methods](https://doi.org/10.1109/TCIAIG.2012.2186810) | 2012 | [笔记](2012-mcts-survey.md) | MCTS 综述：树搜索精确性 + 随机采样通用性，用 UCT 平衡探索/利用 |
| [Chain-of-Thought Prompting Elicits Reasoning in LLMs](https://arxiv.org/abs/2201.11903) | 2022 | [笔记](2022-chain-of-thought.md) | 少样本示例中加入中间推理步骤，让大模型「一步步想」，推理能力随规模涌现 |
| [Plan-and-Solve Prompting](https://arxiv.org/abs/2305.04091) | 2023 | [笔记](2023-plan-and-solve.md) | zero-shot CoT 升级为「先制定计划再分步执行」（PS/PS+），缓解算错/漏步/理解偏差 |
| [Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651) | 2023 | [笔记](2023-self-refine.md) | 同一模型「生成→自我批评→修订」迭代精修，训练-free，平均 +20% 绝对提升 |
| [Tree of Thoughts](https://arxiv.org/abs/2305.10601) | 2023 | [笔记](2023-tree-of-thoughts.md) | 推理从链升级为可搜索的思维树，BFS/DFS 前瞻回溯（Game of 24：4%→74%） |
| [Graph of Thoughts](https://arxiv.org/abs/2308.09687) | 2023 | [笔记](2023-graph-of-thoughts.md) | 推理建模为任意图，支持思维聚合/合并与反馈环（排序较 ToT 质量 +62%、成本 −31%） |

---

返回 [仓库首页](../README.md)
