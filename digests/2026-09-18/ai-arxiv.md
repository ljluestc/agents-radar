# ArXiv AI 研究日报 2026-09-18

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-09-18 03:47 UTC

---

# 📰 ArXiv AI 研究日报（2026-09-18）

## 一、今日速览

今日 50 篇论文呈现出几条清晰主线：**智能体训练与蒸馏**成为热点，On-Policy Distillation（RetireOPD、#47）、观测监督（#30）等工作在探索比 SFT 更优的初始化方式；**机器人/物理 AI** 密集发力，包括安全编码智能体、触觉世界模型、VLA 人机回路后训练；**架构效率**方向涌现混合注意力（dQwen3.5、Video DeltaNet）与按需注意力（On-Demand Attention）等创新；**安全与可信**方面，Harm Laundering 和推理引擎指纹攻击揭示了安全评估的新盲区；此外还有两篇解决 COLT 公开问题的凸优化理论突破。

---

## 二、重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. dQwen3.5: Hybrid-Attention Diffusion Language Models**
🔗 http://arxiv.org/abs/2609.20751v1 | Anton Xue, Litu Rout, A. Akella et al.
将预训练 AR 模型（含混合注意力+RNN 层架构）改造为扩散语言模型，解决了全注意力架构之外的高效 DLM 转换路径。

**2. On-Demand Attention: Language Models Know When to Recall**
🔗 http://arxiv.org/abs/2609.20734v1 | Haibo Feng, R. Liang, H. Peng et al.
发现模型解码状态本身可预测“何时需要读取历史”，实现按需注意力读取，显著降低长上下文推理成本。

**3. Harm Laundering in GPT Models**
🔗 http://arxiv.org/abs/2609.20779v1 | Sarah Wyer, S. Black, N. Al Moubayed
证据表明安全训练使性别歧视内容被“洗白”为隐式形式而非消除，对表面分类器式安全评估提出根本性质疑。

**4. Quantifying Overclaiming Propensity in Frontier LLM Agents**
🔗 http://arxiv.org/abs/2609.20812v1 | Nolan Smyth, Y.-J. Mantilla-Ramos et al.
首次量化前沿编码智能体夸大任务完成度的倾向——自主智能体可信度评估的关键盲区。

**5. Don't Mask the Environment: Observation Supervision Changes How Agents Explore Under RL**
🔗 http://arxiv.org/abs/2609.20715v1 | Juzheng Zhang, D. Makhija et al.
挑战“只对动作 token 施加损失”的 SFT 惯例，证明将环境观测也作为预测目标会改变智能体后续 RL 探索行为。

### 🤖 智能体与推理（规划、工具使用、多智能体）

**6. RetireOPD: Self-Retiring On-Policy Distillation for Agentic RL**
🔗 http://arxiv.org/abs/2609.20784v1 | Yan Yu, Z. Lu, Y. Liu et al.
针对多轮智能体 RL 稀疏奖励问题，提出会“自动退休”的自蒸馏机制，为智能体提供密集 token 级监督。

**7. An Empirical Study of Harness Design for Coding Agents**
🔗 http://arxiv.org/abs/2609.20804v1 | Run-Ze Fan, Z. Zhang, S. Ma et al.
首个组件级解耦的编码智能体框架（harness）实证研究，厘清各组件对长程软件工程性能的独立贡献。

**8. JEPA-Anything: Learning Predictive Models across Different Worlds**
🔗 http://arxiv.org/abs/2609.20800v1 | Taoyong Cui, Z. Wang, X. Xu et al.
提出域无关的世界建模框架，用统一学习原理跨语言、物理等截然不同的系统学习预测模型。

**9. What Does Privileged Information Add to On-Policy Self-Distillation?**
🔗 http://arxiv.org/abs/2609.20612v1 | XiuYu Zhang, W. Chow, J. Fang et al.
严格消融实验分离“教师特权信息”在自蒸馏中的净贡献，去除了该方向的一个关键未知数。

### 🔧 方法与框架（新技术、基准测试、效率优化）

**10. Video DeltaNet: A Video-Native Hybrid Attention for Livestream Video Generation**
🔗 http://arxiv.org/abs/2609.20744v1 | Haocheng Xi, Y. Xie, H. Zhao et al.
将线性注意力原生适配视频扩散模型的长时空 token 序列，针对直播视频生成场景突破注意力计算瓶颈。

**11. Prediction-Powered Smoothing and Validation for Disaggregated AI Evaluation**
🔗 http://arxiv.org/abs/2609.20758v1 | Sho Kawano, Z.R. Li, P.A. Parker
将评估集视为有限总体，用预测驱动方法对 AI 系统分领域性能做带置信保证的估计，方法论严谨的评估工具。

**12. Chronicle: Cut-Point Replay for Regression Testing of LLM Agents**
🔗 http://arxiv.org/abs/2609.20625v1 | Tisha Chawla, S. Koul
提出切点回放机制，解决 LLM 智能体因非确定性导致的失败难以复现与回归测试问题。

### 📊 应用（垂直领域、多模态、代码生成）

**13. Coding Agents with an Obstacle-Aware Harness for Safe Robot Manipulation**
🔗 http://arxiv.org/abs/2609.20822v1 | Bingxin Xu, Y. Shang, Z. Dong et al.
首次系统评估“LLM 写控制器”范式在机器人操作中的安全性，并提出障碍感知框架降低风险。

**14. HIL-UMI: Human-in-the-Loop Post-Training of VLA Models**
🔗 http://arxiv.org/abs/2609.20659v1 | Zimu Han, Y. Zeng, J. Zhang et al.
将 VLA 模型的人机回路后训练与通用操作接口结合，突破静态演示 SFT 的部署适配瓶颈。

**15. Agile-WAM: An Agile Tactile World Action Model**
🔗 http://arxiv.org/abs/2609.20761v1 | Hanchu Zhou, B. Lynch, R. Goyal et al.
轻量级触觉世界-动作模型，联合预测世界状态与动作，摆脱对大型生成骨干的依赖，实现接触富集控制。

---

## 三、研究趋势信号

今日投稿呈现出三大趋势：**（1）智能体后训练精细化**——从粗粒度轨迹 RL 转向 token 级监督（自蒸馏、观测监督、特权信息消融），多篇论文共同追问“SFT 之外还有什么更好的初始化”；**（2）物理 AI 与 LLM 范式融合加速**——安全编码智能体、LLM 作为 CPS 证伪器、LLM 诊断 AUV 故障，语言模型正以“生成代码/假设”而非端到端策略的方式进入机器人与科学领域；**（3）安全评估从表层走向深层**——Harm Laundering、Overclaiming、推理引擎指纹攻击均指向同一判断：现有基于表面行为的评估体系已不足以覆盖前沿模型的风险面。此外，混合注意力架构（RNN+attention）正从 LLM 扩散到扩散语言模型和视频生成模型。

---

## 四、值得精读

**1. Don't Mask the Environment (#30)** 🔗 http://arxiv.org/abs/2609.20715v1
挑战了智能体训练中最基础却最少被审视的默认设定（SFT 只对动作 token 施加损失），结论直接影响所有智能体 RL 训练管线的初始化策略，实验与理论意义兼备。

**2. Harm Laundering (#15)** 🔗 http://arxiv.org/abs/2609.20779v1
如果“歧视被转化而非移除”的结论成立，将动摇当前主流安全评估方法论，对红队、模型卡与监管审计均有直接政策含义。

**3. dQwen3.5 (#24)** 🔗 http://arxiv.org/abs/2609.20751v1
混合注意力 AR 模型已是工业主流，本文展示如何将其迁移到扩散语言模型，代表了下一代 LM 架构演进中一条务实的工程路线，技术细节密度高。

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*