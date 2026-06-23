# 📚 LLM Papers

大语言模型（LLM）相关论文的阅读笔记与收藏，按研究主题分类整理。

## ⭐ 专题：快手 OneRec 生成式推荐谱系

一条完整的演进主线——**从端到端生成取代级联，到把推理变成推荐的核心能力**：

```
OneRec ──▶ OneRec-Think ──▶ OpenOneRec ──▶ OneReason
奠基/端到端    引入显式推理     开源基座+评测    系统激活推理
```

| 论文 | 年份 | 定位 |
|------|------|------|
| [OneRec](recsys/2025-onerec.md) | 2025.06 | 端到端生成式取代多级级联管线，线上承接 25% 流量、成本降至 ~10.6% |
| [OneRec-Think](recsys/2025-onerec-think.md) | 2025.10 | 引入显式文本推理（in-text reasoning），可解释/可控 |
| [OpenOneRec](recsys/2025-openonerec.md) | 2025.12 | 开源基座（1.7B/8B）+ RecIF-Bench + 9600 万交互数据 |
| [OneReason](recsys/2026-onereason.md) | 2026.06 | 诊断「加思考为何无效」，以感知/认知为支点、三阶段激活推理 |

> 完整笔记与互链见 [推荐系统](recsys/) 主题。

## ⭐ 专题：Agent 学习路径

从建立全局观到工程落地的推荐阅读顺序——先读综述铺地图，再沿「范式 → 工具 / 搜索 / 记忆 三分支 → 工程实践」深入：

```
① 综述建全局
        │
        ▼
② 范式底座   CoT ──▶ ReAct ──▶ Plan-and-Solve
        │
        ├──▶ 🔧 工具/编排   Toolformer ──▶ LLMCompiler
        │
        ├──▶ 🌳 推理/搜索   ToT ──▶ GoT ──▶ LATS(MCTS)   ·  Self-Refine / Reflexion(反思)
        │
        └──▶ 🧠 记忆/长期   Generative Agents ──▶ MemGPT
        │
        ▼
③ 工程实践   Building Effective Agents ──▶ Multi-Agent Research System
```

| 阶段 | 论文 | 读它的理由 |
|------|------|-----------|
| ① 综述 | [Rise of LLM Agents](agents/2023-survey-rise-of-agents.md) · [Survey on Autonomous Agents](agents/2023-survey-autonomous-agents.md) | 先建全局：brain-perception-action 与 Profile/Memory/Planning/Action 两套框架 |
| ② 范式 | [CoT](reasoning/2022-chain-of-thought.md) · [ReAct](agents/2022-react.md) · [Plan-and-Solve](reasoning/2023-plan-and-solve.md) | 推理 + 行动交替，几乎所有 agent 的底层范式 |
| 🔧 工具 | [Toolformer](agents/2023-toolformer.md) · [LLMCompiler](agents/2023-llm-compiler.md) | 从「自学调用工具」到「并行编排工具」 |
| 🌳 搜索 | [ToT](reasoning/2023-tree-of-thoughts.md) · [GoT](reasoning/2023-graph-of-thoughts.md) · [LATS](agents/2023-lats.md) · [Self-Refine](reasoning/2023-self-refine.md) · [Reflexion](agents/2023-reflexion.md) | 推理拓扑（链→树→图）+ MCTS 搜索 + 自我反思 |
| 🧠 记忆 | [Generative Agents](agents/2023-generative-agents.md) · [MemGPT](agents/2023-memgpt.md) | 记忆流/反思（认知层）+ OS 式上下文调度（系统层） |
| ③ 工程 | [Building Effective Agents](agents/2024-building-effective-agents.md) · [Multi-Agent Research System](agents/2025-anthropic-multi-agent-research.md) | Anthropic 实战：何时别上多 agent，何时该上、怎么落地 |

> 完整笔记与互链见 [智能体与工具使用](agents/) 与 [推理与思维链](reasoning/) 主题。

## 🗂️ 主题分类

| 主题 | 说明 |
|------|------|
| [里程碑](milestone/) | 奠定方向的经典与里程碑式工作：思想源头、范式转折点、开创性论文 |
| [预训练与基础模型](pretraining/) | Scaling laws、预训练数据与方法、基座模型（GPT/LLaMA/Qwen 等） |
| [对齐与微调](alignment/) | SFT、RLHF、DPO、指令微调、偏好优化 |
| [推理与思维链](reasoning/) | Chain-of-Thought、自一致性、推理时计算、数学与代码推理 |
| [智能体与工具使用](agents/) | ReAct、工具调用、规划、多智能体、自主任务执行 |
| [高效化](efficiency/) | 量化、蒸馏、剪枝、推理加速、MoE、长上下文优化 |
| [多模态](multimodal/) | 视觉-语言模型、图文/音视频理解与生成 |
| [检索增强](retrieval/) | RAG、向量检索、知识注入、长文档问答 |
| [推荐系统](recsys/) | 生成式推荐、序列推荐、召回/排序、用户行为建模、推荐中的推理 |
| [模型架构](architecture/) | Transformer 变体、注意力机制、状态空间模型、新型架构 |
| [评测与基准](evaluation/) | Benchmark、评测方法、LLM-as-judge、能力测量 |
| [安全与可解释性](safety/) | 对抗攻击、越狱、幻觉、可解释性、red-teaming |

## ✍️ 如何添加一篇论文

1. 确定论文属于哪个主题，进入对应目录。
2. 复制笔记模板 [`templates/paper-note.md`](templates/paper-note.md)，重命名为有意义的文件名，例如：
   ```
   pretraining/2020-scaling-laws.md
   alignment/2022-instructgpt.md
   ```
   建议命名格式：`<年份>-<简短标识>.md`
3. 填写笔记内容。
4. 在该主题目录的 `README.md` 论文清单表格里加一行，链接到你的笔记。

## 📌 约定

- **文件命名**：`年份-关键词.md`，全小写、用连字符分隔。
- **跨主题论文**：放在最主要的主题下，用标签或在笔记里互相链接（`[[相关论文]]`）。
- **标签**：在笔记顶部用 `#tag` 标注细分方向，方便后续检索。

---

🤖 项目结构由 [Claude Code](https://claude.com/claude-code) 协助搭建。
