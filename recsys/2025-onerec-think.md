# OneRec-Think: In-Text Reasoning for Generative Recommendation

- **作者**：Zhanyu Liu, Shiyao Wang, Xingmei Wang, Jiaxin Deng, Jinghao Zhang, …, Ruiming Tang, Kun Gai, Guorui Zhou 等
- **机构**：快手（Kuaishou）
- **发表**：arXiv:2510.11639（cs.IR）· 2025-10（2025-11 修订）
- **链接**：[arXiv](https://arxiv.org/abs/2510.11639)
- **主题标签**：`#generative-recommendation` `#recsys` `#reasoning` `#cot` `#in-text-reasoning` `#interpretability`

## 一句话总结

> 在 OneRec 的端到端生成式推荐之上引入**显式文本推理（in-text reasoning）**：让模型像 CoT 一样在输出中先「想」再推荐，从而把 LLM 的可解释性/可控性引入推荐；通过物品-文本对齐、推理激活、推理增强三步实现，并在快手线上验证。

## 背景与动机

- OneRec 等生成式推荐模型本质是**隐式预测器**，缺乏显式推理能力，无法发挥 LLM 在可解释性、可控性上的优势——推荐"为什么这么推"不透明。
- 目标：把对话、推理、个性化推荐三者统一，让模型生成可读的推理过程。

## 核心方法

三大组件：

1. **Itemic Alignment（物品-文本对齐）**：跨模态把物品信息与语言表示对齐，为物品 token 提供语义接地。
2. **Reasoning Activation（推理激活）**：用 scaffolding 技术在推荐情境中激活 LLM 已有的推理能力。
3. **Reasoning Enhancement（推理增强）**：设计推荐专用奖励函数，处理用户偏好的**多有效性（multi-validity）**——即用户存在多个同样合理的偏好，不应被单一标签惩罚。
- **Think-Ahead 架构**：使「显式推理」能在工业延迟约束下实际部署。

## 实验与结论

- 公开 benchmark 上达到 SOTA。
- 快手线上部署，APP 使用时长 **+0.159%**。
- 在保持效果的同时提供透明、可控的推理输出。

## 个人评注

- 启发：首次把"显式 CoT"接到生成式推荐上，并直面推荐与 NLP 的关键差异——物品 token 需要先对齐到语言语义（itemic alignment）才能推理；"多有效性奖励"也很有洞见，因为推荐没有唯一正确答案。
- 谱系：[[2025-onerec]]（隐式预测）→ 本文（引入显式推理）→ [[2026-onereason]]（系统化诊断"加思考为何无效"并给出三阶段配方）。
- 关联 [[2026-onereason]]：OneReason 后续指出"直接加思考不一定有优势"，本文是该结论的重要前驱与对照。
- 局限与疑问：+0.159% 线上收益相对温和，显式推理的算力/延迟代价与收益的权衡仍是核心问题。
