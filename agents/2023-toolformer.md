# Toolformer: Language Models Can Teach Themselves to Use Tools

- **作者**：Timo Schick, Jane Dwivedi-Yu, Roberto Dessì, Roberta Raileanu, Maria Lomeli, Luke Zettlemoyer, Nicola Cancedda, Thomas Scialom
- **机构**：Meta AI Research (FAIR) / Universitat Pompeu Fabra
- **发表**：NeurIPS 2023 · arXiv:2302.04761（2023-02）
- **链接**：[arXiv](https://arxiv.org/abs/2302.04761)
- **主题标签**：`#agent` `#tool-use` `#self-supervised` `#api` `#toolformer`

## 一句话总结

> 让模型**自学**调用工具：以自监督方式，自动在文本中采样「在哪插入 API 调用、调什么」，只保留那些**能降低后续预测损失**的调用作为训练数据，微调后模型便能自己决定何时/如何调用计算器、问答、搜索、翻译、日历等工具——无需人工标注。

## 背景与动机

- LLM 擅长少样本学习，却在**算术、事实查询、时效信息**等离散任务上不可靠且易幻觉。
- 已有工具使用方案要么依赖大量人工标注，要么局限于特定任务。Toolformer 想要：**用极少示例、以自监督方式**让模型通用地学会用工具，同时不损害原有语言建模能力。

## 核心方法

三步自监督数据构造（self-supervised）：

1. **采样 API 调用**：用少量人工示例（每个工具一手示例）提示模型，在语料文本的候选位置生成可能的 API 调用。
2. **执行调用**：实际调用工具，得到返回结果。
3. **基于损失过滤**：只保留那些「插入调用结果后能**显著降低**对后续 token 的预测损失」的调用——即真正有用的调用。
- 用过滤后的、内嵌 API 调用的数据**微调模型本身**；推理时模型自主在生成中发起调用、读回结果继续生成。

**集成的工具**：计算器、问答系统、两个搜索引擎、翻译系统、日历。

## 实验与结论

- 在多种下游任务上**零样本性能大幅提升**，常能与**大得多的模型**竞争。
- 关键：在获得工具能力的同时**保持了核心语言建模能力**不退化。

## 个人评注

- 启发：与 ReAct 形成互补的另一条工具使用路线——ReAct 在**推理时用提示**决定调用，Toolformer 把工具使用**烤进权重**。「用损失下降作为自监督信号筛选有用调用」是非常优雅的 self-supervised 设计。
- 关联 [[2022-react]]：改流程 vs 改权重的两种工具使用范式；现代 agent / function-calling 模型常二者兼取。
- 关联 [[2022-chain-of-thought]]：都是为补足 LLM 的离散/精确计算短板，一个靠推理步、一个靠外部工具。
- 局限：API 调用相互独立、不支持链式/嵌套调用；每个工具需手工示例与接口；交互式多轮工具使用未覆盖。
