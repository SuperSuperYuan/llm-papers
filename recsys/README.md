# 推荐系统

> 生成式推荐、序列推荐、召回/排序、用户行为建模，以及推理在推荐中的应用

## 快手 OneRec 谱系

> 端到端生成式推荐的演进主线：**奠基 → 引入推理 → 开源基座 → 系统激活推理**
> [OneRec](2025-onerec.md) → [OneRec-Think](2025-onerec-think.md) → [OpenOneRec](2025-openonerec.md) → [OneReason](2026-onereason.md)

## 论文清单

| 论文 | 年份 | 笔记 | 一句话总结 |
|------|------|------|-----------|
| [OneRec Technical Report](https://arxiv.org/abs/2506.13695) | 2025 | [笔记](2025-onerec.md) | 用单一端到端生成式模型取代多级级联推荐管线，encoder-decoder + 语义 ID + RL 对齐，快手线上承接 25% 流量、成本降至 ~10.6% |
| [OneRec-Think](https://arxiv.org/abs/2510.11639) | 2025 | [笔记](2025-onerec-think.md) | 在生成式推荐中引入显式文本推理（in-text reasoning），物品-文本对齐 + 推理激活 + 多有效性奖励，带来可解释/可控的推荐 |
| [OpenOneRec Technical Report](https://arxiv.org/abs/2512.24762) | 2025 | [笔记](2025-openonerec.md) | 生成式推荐的开源基座（1.7B/8B）+ RecIF-Bench 评测 + 9600 万交互数据，推荐能力可预测扩展且缓解通用知识遗忘 |
| [OneReason Technical Report](https://arxiv.org/abs/2606.06260) | 2026 | [笔记](2026-onereason.md) | 把「思考再回答」的推理范式引入生成式推荐：以感知（perception）+ 认知（cognition）为支点，经预训练/SFT/RL 三阶段激活推荐模型的推理能力 |

---

返回 [仓库首页](../README.md)
