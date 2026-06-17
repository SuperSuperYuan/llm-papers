# OpenOneRec Technical Report

- **作者**：Guorui Zhou, Honghui Bao, Jiaxin Deng, Jinghao Zhang, …, Defu Lian, Ruiming Tang, Kun Gai 等（共 47 位）
- **机构**：快手（Kuaishou）
- **发表**：arXiv:2512.24762（cs.IR）· 2025-12（2026-02 修订）
- **链接**：[arXiv](https://arxiv.org/abs/2512.24762) · [GitHub](https://github.com/Kuaishou-OneRec/OpenOneRec)
- **主题标签**：`#generative-recommendation` `#recsys` `#foundation-model` `#open-source` `#benchmark` `#recif-bench`

## 一句话总结

> 面向生成式推荐的**开源基座模型 + benchmark**：发布 1.7B / 8B 的 OneRec Foundation 模型、RecIF-Bench 评测套件与 9600 万条交互的开放训练数据，证明推荐能力可随规模可预测地扩展，同时缓解对通用知识的灾难性遗忘——弥合"专用推荐引擎"与"通用智能"之间的鸿沟。

## 背景与动机

- 生成式推荐研究缺乏**开放基座、统一评测和可复现训练数据**，难以横向比较、难以推进。
- 关键张力：让模型学会推荐时，往往会**灾难性遗忘**通用语言知识；如何兼得推荐专精与通用能力是核心挑战。

## 核心方法

- **模型**：OneRec Foundation，提供 **1.7B 与 8B** 两档；在 RecIF-Bench 全任务取得 SOTA，迁移到 Amazon 系列 benchmark 时 **Recall@10 平均提升 26.8%**（10 个数据集）。
- **Benchmark / 数据**：**RecIF-Bench** 覆盖 8 类评测任务（从基础预测到复杂推理）；开放训练集含 **16 万用户、9600 万条交互**，支持可复现研究。
- **训练框架**：数据处理 → 协同预训练（co-pretraining）→ 后训练（post-training）三阶段，使推荐能力**可预测扩展**且**缓解灾难性遗忘**。

## 实验与结论

- RecIF-Bench 全任务 SOTA；跨域迁移（Amazon）Recall@10 平均 +26.8%。
- 验证：生成式推荐模型可在发展领域专精的同时保持广泛的通用知识。

## 个人评注

- 启发：把生成式推荐推向"开源基座 + 标准 benchmark"的范式，类似 NLP 领域 LLaMA/开放评测对社区的推动作用；"推荐专精 vs 通用知识遗忘"的权衡是把 LLM 思路迁入推荐时绕不开的问题。
- 谱系：[[2025-onerec]] → [[2025-onerec-think]] → 本文（开源基座 + benchmark）→ [[2026-onereason]]（在此基础上系统激活推理）。OneReason 报告中提到的"前期工作 OpenOneRec 发现思考模式无优势"即指本谱系的实验观察。
- 局限与疑问：RecIF-Bench 的任务设计是否充分代表真实推荐场景、co-pretraining 中推荐与语言数据的配比策略仍值得深挖。
