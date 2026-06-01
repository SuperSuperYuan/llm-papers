# A Survey of Monte Carlo Tree Search Methods（蒙特卡洛树搜索方法综述）

- **作者**：Cameron Browne, Edward Powley, Daniel Whitehouse, Simon Lucas, Peter Cowling, Philipp Rohlfshagen, Stephen Tavener, Diego Perez, Spyridon Samothrakis, Simon Colton
- **机构**：Imperial College London / University of Essex / University of Bradford
- **发表**：IEEE Transactions on Computational Intelligence and AI in Games, Vol. 4, No. 1 · 2012
- **链接**：[DOI 10.1109/TCIAIG.2012.2186810](https://doi.org/10.1109/TCIAIG.2012.2186810) · [本地存档](2012-mcts-survey.pdf)
- **主题标签**：`#mcts` `#uct` `#search` `#bandit` `#planning` `#test-time-compute`

## 一句话总结

> MCTS 把「树搜索的精确性」与「随机采样的通用性」结合起来：通过反复随机模拟、增量地非对称构建搜索树，用 UCB1（→ UCT）平衡探索与利用，无需中间状态的评估函数，几乎不依赖领域知识即可在围棋等高复杂度问题上取得突破。本文是 MCTS 头五年研究的系统性综述。

## 背景与动机

- 传统的深度受限 minimax 搜索需要对**中间状态**做评估，强依赖领域知识、且对评估噪声脆弱（尤其在延迟奖励的博弈中）。
- MCTS 只需终止状态的回报值，是一种**随算力增长而变强的 anytime 统计算法**，几乎无需领域知识。本文目标是把 2006 年以来散落在各领域（不止围棋）的大量变体与增强方法做统一梳理。

## 核心方法

**四步迭代循环**（每轮一次）：

1. **Selection 选择**：从根节点按 *tree policy* 递归下选，直到到达可扩展节点。
2. **Expansion 扩展**：加入一个新的子节点。
3. **Simulation 模拟 / Playout**：用 *default policy*（最简单为均匀随机走子）从该节点模拟到终局，得到回报 Δ。
4. **Backpropagation 回传**：把 Δ 沿选择路径回传，更新各节点的访问次数与平均回报 Q。

两类策略：**Tree Policy**（选择+扩展，树内）与 **Default Policy**（模拟，树外）。

**UCT = UCB1 应用于树**（Kocsis & Szepesvári, 2006），把每次选子节点建模为多臂老虎机问题，选择使下式最大的子节点 j：

$$ UCT = \overline{X_j} + 2C_p \sqrt{\frac{2\ln n}{n_j}} $$

- $\overline{X_j}$：利用项（子节点平均回报）；后一项：探索项（n 为父节点访问数，$n_j$ 为子节点访问数）。
- 未访问节点 UCT 视为 ∞，保证每个子节点至少被探索一次；UCB1 保证 regret 增长在最优界的常数倍内。
- 搜索预算耗尽后，按 max child / **robust child（最多访问）** / max-robust / secure child 等准则返回根节点的最佳动作。

**关键里程碑**（论文 Table 1）：1990 Abramson → 2002 Auer 等提出 UCB1 → 2006 Coulom 提出并命名 MCTS、Kocsis & Szepesvári 给出 UCT、Gelly 等的 MoGo 在围棋上大获成功。

**变体与增强（论文主体）**：

- *Tree Policy 增强*：First Play Urgency、Progressive Bias/Widening、Opening Books、UCB 变体（EXP3、HOO）等。
- *AMAF / RAVE 系列*：All-Moves-As-First、α-AMAF、RAVE-max、PoolRAVE —— 跨节点共享走子统计，加速收敛（围棋中尤为有效）。
- *MCTS-Solver / Score-Bounded MCTS*：引入证明数搜索思想处理必胜/必败。
- *并行化*：Leaf / Root / Tree（含 UCT-Treesplit）并行。
- *其它*：SP-MCTS（单人）、多玩家/多智能体、面向不完美信息的 Determinization、HOP、Sparse UCT、MCCFR 等；以及与 TDL 等学习方法结合。

## 实验与结论

- **应用领域综述**：围棋（核心驱动力，MoGo/Fuego 等达到 dan 级、击败职业棋手）、连接类游戏（Hex 的 MoHex 夺冠）、其它组合博弈、单人游戏、通用博弈（GGP，CadiaPlayer 世界冠军）、实时游戏、非确定/隐藏信息游戏，以及非博弈领域（约束满足、调度、采样式规划、程序化内容生成等）。UCT 是被采用最广的算法。
- **优势**：仅凭规则即可博弈、对启发式噪声鲁棒（与脆弱的 minimax 对比）、anytime、走子方式「类人」便于解释、树非对称增长聚焦于有希望的分支。
- **弱点**：基础算法常需领域增强才能达到强水平、且增强多靠手工经验调优；搜索动力学与参数/增强的影响尚缺理论理解。
- **展望**：通用增强、特定领域增强、对 MCTS 行为的理论理解、处理不确定性与隐藏信息。

## 个人评注

- 启发：这是「test-time search / 推理时计算」的方法论源头之一。从 AlphaGo/AlphaZero 把 MCTS 与神经网络价值/策略网结合，到近年 LLM 推理中用 MCTS 做搜索式推理（如 tree-of-thought、过程奖励引导搜索），其「探索-利用平衡 + 模拟回传」框架一脉相承。
- 与 [[2019-the-bitter-lesson]] 呼应：MCTS 正是 Sutton 所说能「随算力任意扩展」的**搜索**类通用方法的典范。
- 局限与疑问：本综述聚焦 2012 年前的博弈领域，未涵盖深度学习时代的 MCTS+NN 融合；现代 LLM 场景下「模拟」如何低成本进行、奖励如何定义，仍是开放问题。
