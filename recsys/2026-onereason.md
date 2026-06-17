# OneReason Technical Report

- **作者**：OneRec 团队（83+ 贡献者），通讯/主要负责人 Jiangxia Cao 等
- **机构**：快手（Kuaishou）OneRec
- **发表**：arXiv:2606.06260（cs.IR）· 2026（Work in progress）
- **链接**：[arXiv](https://arxiv.org/abs/2606.06260) · [alphaXiv 解读](https://www.alphaxiv.org/audio/2606.06260)
- **主题标签**：`#generative-recommendation` `#recsys` `#reasoning` `#cot` `#rl` `#itemic-token`

## 一句话总结

> 把 LLM「think before answer」的推理范式引入**生成式推荐**：作者发现直接给推荐模型加思考过程并不能带来收益（仅 itemic token 构不成有意义的 CoT），于是提出推荐推理的两大支点——**感知（perception）**与**认知（cognition）**，并用「预训练强化 item token 感知 → SFT 三级认知增强 CoT → RL 先专精后统一」的三阶段配方真正激活推理能力。

## 背景与动机

- 受 LLM 推理范式（o1/R1 式「先思考后作答」）启发，团队尝试在生成式推荐（OneRec 系列）中引入推理能力。
- **意外现象**：在前期工作（OneRec-Think、OpenOneRec）中，**思考模式（thinking）相比非思考模式并没有优势**——生成式推荐模型只能吃到 scaling 的红利，推理能力难以被激活。
- **根因**：推荐序列只由 **itemic token（物品 token）** 组成，模型无法在「只有物品 token」的空间里构造出有意义的思维链（CoT）。物品 token 缺乏可供推理展开的语义与逻辑结构。

## 核心方法

作者主张：推荐中有效的推理建立在两种能力之上——

- **感知 Perception**：把 itemic token **接地（ground）到其底层语言语义**的能力（让模型"看懂"物品 token 到底代表什么）。
- **认知 Cognition**：把用户行为序列**重组为连贯的潜在兴趣点（latent interest points）**的能力（把零散行为抽象成可推理的兴趣结构）。

围绕这两点，OneReason 给出**三阶段训练配方**：

1. **Pre-training（预训练）**：强化 **itemic token 的感知能力**，把物品 token 与其语言语义对齐，为后续推理打基础。
2. **SFT（监督微调）**：为推荐任务设计**三级认知增强的 CoT 格式（three-level cognition-enhanced CoT）**，显式教模型如何把行为序列组织成兴趣→推理→推荐的思维链。
3. **RL（强化学习）**：采用 **specialize-then-unify（先专精、后统一）** 的训练配方，进一步增强思考能力。

**与已有工作的关键区别**：前作 OneRec-Think / OpenOneRec 验证了"直接加思考无效"这一负结果；OneReason 把推理从「附加功能」重新定位为推荐系统的**核心能力**，并从感知/认知两个层面对症下药，而非简单照搬 LLM 的 CoT。

## 实验与结论

- 关键负结果（动机来源）：thinking mode 不优于 non-thinking mode，推荐推理能力难以凭空激活。
- OneReason 通过三阶段配方使推理成为可被激活、可带来收益的能力（技术报告处于 work in progress 状态，完整指标以正式版本为准）。
- 谱系：OneRec → OneRec-Think → OpenOneRec（开源基座 + benchmark） → OneReason。

## 个人评注

- 启发：揭示了一个重要的领域差异——LLM 的 CoT 之所以有效，是因为语言 token 本身携带可推理的语义；而推荐的 itemic token 是"语义贫瘠"的 ID 化符号，必须先解决**感知接地**才能谈推理。这对任何"把 LLM 范式迁移到非语言模态"的工作都是警示。
- 与 [[2012-mcts-survey]]、[[2019-the-bitter-lesson]] 的关联：同属"推理时计算 / test-time reasoning"思潮在具体业务（推荐）中的落地与边界探索。
- 局限与疑问：报告为 work in progress，缺乏完整公开指标；"三级认知 CoT"与"specialize-then-unify"的具体设计细节、线上 A/B 收益仍待正式论文披露。
