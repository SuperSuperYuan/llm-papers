# Graph of Thoughts: Solving Elaborate Problems with Large Language Models

- **作者**：Maciej Besta, Nils Blach, Ales Kubicek, Robert Gerstenberger, Michal Podstawski, Lukas Gianinazzi, Joanna Gajda, Tomasz Lehmann, Hubert Niewiadomski, Piotr Nyczyk, Torsten Hoefler
- **机构**：ETH Zurich / Cledar / Warsaw University of Technology
- **发表**：AAAI 2024 · arXiv:2308.09687（2023-08）
- **链接**：[arXiv](https://arxiv.org/abs/2308.09687)
- **主题标签**：`#reasoning` `#got` `#graph` `#prompting` `#aggregation` `#test-time-compute`

## 一句话总结

> 把 LLM 推理建模为一张**任意图**：思维（thought）是顶点、依赖是边，从而支持把多条思维**聚合/合并（aggregate）**成更优结果、**蒸馏**整张思维网络的精华、以及用**反馈环（feedback loop）** 增强思维——比 CoT（链）和 ToT（树）表达力更强。

## 背景与动机

- CoT 是链、ToT 是树，二者都**无法表达「把多条独立思路合并」或「带循环的反馈精修」**。
- 很多复杂问题（如排序、集合运算、聚合类任务）天然需要分解后再合并子结果。GoT 用图结构统一表达这些推理拓扑。

## 核心方法

- **图抽象**：顶点 = 一个 LLM 思维（中间解/子结果），有向边 = 依赖关系。
- **思维变换（thought transformations）** 作为图操作：
  - **Generate**：从已有思维生成新思维（扩展）；
  - **Aggregate**：把多个思维**合并**成一个（CoT/ToT 做不到的关键操作）；
  - **Refine**：对思维做自我精修（可形成反馈环/循环）。
- 通过组合这些操作灵活构建与编辑推理图；框架可扩展以容纳未来的新提示范式。

## 实验与结论

- **任务**：排序（sorting）、集合运算（set operations）等可分解-合并的任务。
- **关键结果**：在排序任务上相比 ToT **质量提升 62%**，同时**成本降低 >31%**——既更好又更省。

## 个人评注

- 启发：「聚合多条思维」是 GoT 相对 ToT 的核心增量，特别契合 divide-and-conquer 类问题；也提示推理拓扑本身是可设计的维度。
- 关联 [[2022-chain-of-thought]]、[[2023-tree-of-thoughts]]：推理拓扑的演进链——链（CoT）→ 树（ToT）→ 图（GoT）。
- 关联 [[2023-self-refine]]：GoT 的 refine/反馈环与 Self-Refine 的迭代自反馈思想相通，但被纳入图操作的统一框架。
- 局限：图的构造需按任务设计（非全自动）；评测任务偏结构化（排序/集合），在开放式推理上的优势待验证；调度复杂度更高。
