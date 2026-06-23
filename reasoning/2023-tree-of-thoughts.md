# Tree of Thoughts: Deliberate Problem Solving with Large Language Models

- **作者**：Shunyu Yao, Dian Yu, Jeffrey Zhao, Izhak Shafran, Thomas L. Griffiths, Yuan Cao, Karthik Narasimhan
- **机构**：Princeton University / Google DeepMind
- **发表**：NeurIPS 2023 · arXiv:2305.10601（2023-05）
- **链接**：[arXiv](https://arxiv.org/abs/2305.10601)
- **主题标签**：`#reasoning` `#tot` `#search` `#planning` `#test-time-compute` `#deliberate`

## 一句话总结

> 把推理从 CoT 的「一条左到右的链」升级为**一棵可探索的思维树**：每个节点是一个中间「想法（thought）」，模型生成多个候选、对各状态做价值评估，用 BFS/DFS **前瞻与回溯**——让 LLM 像下棋一样「深思熟虑」地解决需要规划的问题。

## 背景与动机

- CoT 把推理约束为 **token 级、从左到右**的单路径生成：一旦中途走错无法回头，也无法比较多条路径。
- 许多任务（需要规划、探索、试错的）需要「深思熟虑」式决策——考虑多条路径、前瞻、回溯。ToT 把经典 AI 的搜索引入 LLM 推理。

## 核心方法

四个要素：

1. **Thought Decomposition 思维分解**：把问题拆成连贯的中间思维单元（一步可评估的文本块）。
2. **Thought Generation 思维生成**：在每个状态生成多个候选下一步（采样或提议）。
3. **State Evaluation 状态评估**：用 LLM 自评每个状态离目标的进展（打分或投票），作为搜索启发。
4. **Search 搜索**：用 **BFS / DFS** 在思维树上探索，可前瞻、可回溯到更优分支。

## 实验与结论

- **任务**：Game of 24、Creative Writing（创意写作）、Mini Crosswords（迷你填字）。
- **关键结果**：Game of 24 上，GPT-4 标准提示成功率仅 **4%**，**ToT 达到 74%**——在规划密集型任务上巨幅提升。

## 个人评注

- 启发：把「搜索」正式接入 LLM 推理，是 CoT → 结构化推理的关键一跳；与 MCTS/经典搜索一脉相承，后续 LATS 直接用 MCTS 强化之。
- 关联 [[2022-chain-of-thought]]：ToT 是 CoT 的「多路径 + 评估 + 回溯」泛化（链 → 树）。
- 关联 [[2012-mcts-survey]]：ToT 的 BFS/DFS 是较朴素的搜索；[[2023-lats]] 进一步引入 MCTS 的探索-利用平衡与回传。
- 关联 [[2023-graph-of-thoughts]]：GoT 再把「树」泛化为「图」，支持思维的聚合/合并与反馈环。
- 局限：状态评估依赖 LLM 自评的可靠性；搜索带来大量 LLM 调用、成本高；分解方式需按任务设计。
