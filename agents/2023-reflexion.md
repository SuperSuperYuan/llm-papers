# Reflexion: Language Agents with Verbal Reinforcement Learning

- **作者**：Noah Shinn, Federico Cassano, Edward Berman, Ashwin Gopinath, Karthik Narasimhan, Shunyu Yao
- **机构**：Northeastern University / MIT / Princeton University
- **发表**：NeurIPS 2023 · arXiv:2303.11366（2023-03）
- **链接**：[arXiv](https://arxiv.org/abs/2303.11366)
- **主题标签**：`#agent` `#reflexion` `#self-reflection` `#memory` `#verbal-rl` `#tool-use`

## 一句话总结

> 用**语言化的强化学习**替代权重更新：agent 把任务的反馈信号「用语言反思成经验文本」存入**情景记忆（episodic memory）**，下一次尝试时读回这些反思来改进决策——无需任何梯度训练，就能让模型在试错中越做越好。

## 背景与动机

- 让 LLM agent 通过试错学习很难：传统 RL 需大量样本与昂贵微调，对动辄百亿参数的 LLM 不现实。
- 思路：既然 LLM 本身擅长语言，就让它**用自然语言总结失败教训**作为「奖励信号」，存进记忆指导后续 trial——把强化信号从「数值梯度」换成「语言反思」。

## 核心方法

三个模块 + 记忆：

1. **Actor**：基于当前状态与记忆产生行动（可基于 ReAct / CoT）。
2. **Evaluator**：对一次完整 trajectory 打分/给反馈（可来自环境、启发式或自评）。
3. **Self-Reflection 模型**：把「这次为什么失败、下次怎么改」凝练成**反思文本**。
4. **Episodic Memory（记忆缓冲）**：存储反思文本，下一轮作为上下文喂给 Actor。
- 形成「尝试 → 评估 → 反思 → 记忆 → 再尝试」的闭环，跨 episode 积累经验。

## 实验与结论

- **HumanEval（代码）**：pass@1 达 **91%**，超过当时 GPT-4 的 80%。
- **HotpotQA（多跳 QA）**、**ALFWorld（序列决策）**：相比 ReAct 等基线显著提升。
- 消融研究分析了不同反馈类型/来源的作用。

## 个人评注

- 启发：开创「verbal RL / 语言化反思 + 外部记忆」这一无需训练的 agent 自我改进范式，是 self-improving agent 与 memory 研究的关键奠基。
- 关联 [[2022-react]]：Reflexion 的 Actor 常用 ReAct，加上跨 trial 的反思记忆层——给 ReAct 装上「长期记忆与复盘」。
- 关联 [[2023-self-refine]]：都是「自我反馈迭代」，但 Self-Refine 在**单次输出内**精修，Reflexion 跨**多次 episode**用记忆积累经验、且依赖环境反馈。
- 局限：依赖反馈信号质量；记忆增长与遗忘管理；反思可能自我强化错误判断。
