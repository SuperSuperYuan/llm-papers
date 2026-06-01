# 📚 LLM Papers

大语言模型（LLM）相关论文的阅读笔记与收藏，按研究主题分类整理。

## 🗂️ 主题分类

| 主题 | 说明 |
|------|------|
| [预训练与基础模型](pretraining/) | Scaling laws、预训练数据与方法、基座模型（GPT/LLaMA/Qwen 等） |
| [对齐与微调](alignment/) | SFT、RLHF、DPO、指令微调、偏好优化 |
| [推理与思维链](reasoning/) | Chain-of-Thought、自一致性、推理时计算、数学与代码推理 |
| [智能体与工具使用](agents/) | ReAct、工具调用、规划、多智能体、自主任务执行 |
| [高效化](efficiency/) | 量化、蒸馏、剪枝、推理加速、MoE、长上下文优化 |
| [多模态](multimodal/) | 视觉-语言模型、图文/音视频理解与生成 |
| [检索增强](retrieval/) | RAG、向量检索、知识注入、长文档问答 |
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
