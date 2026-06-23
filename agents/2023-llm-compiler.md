# An LLM Compiler for Parallel Function Calling（LLMCompiler）

- **作者**：Sehoon Kim, Suhong Moon, Ryan Tabrizi, Nicholas Lee, Michael W. Mahoney, Kurt Keutzer, Amir Gholami
- **机构**：UC Berkeley（SqueezeAI Lab）/ ICSI / LBNL
- **发表**：ICML 2024 · arXiv:2312.04511（2023-12）
- **链接**：[arXiv](https://arxiv.org/abs/2312.04511) · [GitHub](https://github.com/SqueezeAILab/LLMCompiler)
- **主题标签**：`#agent` `#tool-use` `#function-calling` `#planning` `#parallel` `#dag` `#latency`

## 一句话总结

> 借鉴**编译器**思想给工具调用做编排：用 Planner 把任务编译成可并行的**有向无环图（DAG）**，Task Fetching Unit 解析依赖、Executor **并发执行**多个函数调用——相比 ReAct 的顺序「思考-行动」循环，最高 3.7× 加速、6.7× 降本，准确率还提升近 9%。

## 背景与动机

- ReAct 式 agent 是**顺序**的：思考一步→调一次工具→看观察→再思考，多个本可并行的工具调用被串行化。
- 后果：**高延迟、高 token 成本**；且顺序推理中易累积错误、被中间观察干扰。
- 目标：在多函数调用场景下，自动发现可并行性并高效执行。

## 核心方法

三大组件（类比编译器/运行时）：

1. **Function Calling Planner**：根据用户问题生成**任务编排计划**——一组带依赖关系的子任务，构成 DAG。
2. **Task Fetching Unit**：按 DAG 依赖解析任务，把就绪任务（及其参数，含对前序任务输出的引用替换）分发出去。
3. **Executor**：对相互独立的任务**并发执行**对应的工具/函数调用。

- 关键区别 vs ReAct：把「边想边逐个调用」变成「先一次性规划出依赖图，再并行调度执行」，最大化并行、减少 LLM 往返次数。

## 实验与结论

- 相比 ReAct 基线：**延迟最高降至 1/3.7（~3.7× 加速）**，**成本最高降至 1/6.7（~6.7×）**，**准确率提升最高约 9%**。
- 在多种函数调用模式上一致改善；适用于开源与闭源模型，代码开源。

## 个人评注

- 启发：把系统/编译器的「依赖分析 + 并行调度」引入 agent 工具编排，是对 ReAct 顺序范式的工程化突破——agent 效率问题的代表性解法。
- 关联 [[2022-react]]：直接针对 ReAct 顺序执行的延迟/成本痛点；二者是「顺序 vs 并行 DAG」的对照。
- 关联 [[2023-plan-and-solve]]：同属「先规划再执行」，但 LLMCompiler 的计划是**可并行的工具调用图**，Plan-and-Solve 的计划是纯文本推理步骤。
- 关联 [[2023-toolformer]]：Toolformer 解决「会不会调用」，LLMCompiler 解决「多调用如何高效编排」。
- 局限：依赖 Planner 正确识别依赖关系；动态/数据依赖强的任务并行度受限；DAG 规划本身也有开销。
