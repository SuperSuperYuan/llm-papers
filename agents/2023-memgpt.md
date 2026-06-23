# MemGPT: Towards LLMs as Operating Systems

- **作者**：Charles Packer, Sarah Wooders, Kevin Lin, Vivian Fang, Shishir G. Patil, Ion Stoica, Joseph E. Gonzalez
- **机构**：UC Berkeley
- **发表**：arXiv:2310.08560（2023-10，2024-02 修订）
- **链接**：[arXiv](https://arxiv.org/abs/2310.08560)
- **主题标签**：`#agent` `#memory` `#memgpt` `#context-management` `#virtual-memory` `#long-context` `#os`

## 一句话总结

> 把**操作系统的分层内存/虚拟内存**思想搬到 LLM：用「虚拟上下文管理」在有限上下文窗口（主上下文）与外部存储（外部上下文）之间，通过**函数调用做「换页（paging）」、用中断管理控制流**，让模型处理远超原生窗口的长文档与跨多轮会话的长期记忆。

## 背景与动机

- LLM 的**上下文窗口有限**，长文档分析、跨会话的长期对话都会超出窗口、丢失早期信息。
- 直接扩窗成本高且有上限。能否像 OS 用虚拟内存「以有限物理内存营造无限地址空间」那样，给 LLM 营造「无限上下文」的错觉？

## 核心方法

- **分层内存（memory hierarchy）**：
  - **Main context（主上下文）**：当前在窗口内的内容，类比 RAM；
  - **External context（外部上下文）**：窗口之外的持久存储，类比磁盘。
- **Paging via function calls**：LLM 通过**自己调用函数**把数据在主/外部上下文间换入换出（检索、写入、分页），即模型自主管理自己的记忆。
- **Interrupts（中断）**：用中断机制处理系统与用户之间的控制流（如何时让出/收回控制）。
- 整体把 LLM 当作「OS 内核」来调度有限的上下文资源。

## 实验与结论

- **长文档分析**：能在超出底层模型上下文窗口的文本上完成问答/分析。
- **多会话对话 agent**：跨会话保持连续性，能回顾过去交互、随长期互动「成长」。
- **结论**：把上下文限制从「硬约束」转化为「可管理的资源」，为更长时程的 LLM 应用铺路。

## 个人评注

- 启发：用 OS 抽象（虚拟内存/分页/中断）重新框定 LLM 记忆问题，非常优雅；「让模型用 function call 自管记忆」直接影响了后续 long-term memory agent 与 memory 框架（如 Letta）。
- 关联 [[2023-generative-agents]]：互补的两条记忆路线——Generative Agents 解决「记忆如何组织、提炼成洞见」（认知层），MemGPT 解决「上下文如何分层调度、突破窗口」（系统层）。
- 关联 [[2022-react]]：MemGPT 的记忆操作正是通过工具/函数调用实现，是 ReAct 式工具使用在「自我记忆管理」上的应用。
- 局限：换页/检索质量依赖模型的函数调用可靠性；多次往返带来延迟与成本；外部存储的组织与检索策略仍需精心设计。
