# ArXiv AI 研究日报 2026-09-17

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-09-17 04:00 UTC

---

# ArXiv AI 研究日报（2026-09-17）

## 一、今日速览

今日 50 篇 AI 相关论文中，**LLM 智能体（Agent）研究持续高热**，覆盖基准构建、工具调用调度、多智能体治理与安全等全链条议题。对齐与安全方向出现两项有趣工作：基于内部表征监测 reward hacking、以及零阶优化偏好对齐新范式。架构层面，"Infinite-Parameter LLMs" 提出从实时数据动态生成权重的思路，挑战了传统 MoE 的静态参数库假设，值得关注。

## 二、重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **Infinite-Parameter LLMs: Generating and Adapting Weights from Live Data** — [arxiv.org/abs/2609.18842](http://arxiv.org/abs/2609.18842v1) | Jinli Hu et al.
   突破 MoE 静态参数库范式，让模型从实时数据生成并适配权重，是架构层面的大胆探索。

2. **A Zeroth-Order Paradigm for LLM Preference Alignment** — [arxiv.org/abs/2609.19144](http://arxiv.org/abs/2609.19144v1) | Peter Chen et al.
   针对直接偏好对齐中的 likelihood displacement 问题，提出零阶优化替代方案。

3. **How Model Growth, Recursion, and Boundary Operators Influence Scaling Exponents** — [arxiv.org/abs/2609.19107](http://arxiv.org/abs/2609.19107v1) | Zixi Chen et al.
   证明架构干预可修改 scaling 指数，实现随算力指数级提升，挑战“架构不改 scaling law”的共识。

4. **Monitoring and Discovering Reward Hacking with Internal Representations during LLM Evaluations** — [arxiv.org/abs/2609.19101](http://arxiv.org/abs/2609.19101v1) | Leon Bergen et al.
   发现 reward hacking 在模型内部表征中留下可检测的“签名”，可用于监测与发现。

5. **Higher-order pruning of experts in mixture-of-experts language models** — [arxiv.org/abs/2609.18916](http://arxiv.org/abs/2609.18916v1) | Alex M. Tseng et al.
   考虑专家间依赖关系的高阶 MoE 剪枝，直击 MoE 内存瓶颈。

6. **Double descent is the principle of least action** — [arxiv.org/abs/2609.19076](http://arxiv.org/abs/2609.19076v1) | Congzhou M Sha
   用统计力学中的最小作用量原理统一解释 double descent 现象，理论视角新颖。

7. **Preventing Model Collapse: A Fisher-Rao Perspective** — [arxiv.org/abs/2609.18878](http://arxiv.org/abs/2609.18878v1) | Matteo Marchi et al.
   从 Fisher-Rao 几何刻画合成数据递归训练导致模型坍缩的动力学。

### 🤖 智能体与推理

8. **Compositional Policy Violations: When Step-Level Compliance Fails In Agentic AI Workflows** — [arxiv.org/abs/2609.18820](http://arxiv.org/abs/2609.18820v1) | Ashwini Kurady et al.
   指出逐步合规的治理框架会漏掉工作流级复合违规，对受监管场景的 Agent 部署意义重大。

9. **Taming the Agentic RAN: Stability-Guaranteed Arbitration of Autonomous AI Agents in O-RAN** — [arxiv.org/abs/2609.18857](http://arxiv.org/abs/2609.18857v1) | S. B. H. Natanzi & Bo Tang
   在真实 O-RAN 系统上演示多个独立闭环 Agent 的不安全性，并提出稳定性保证的仲裁机制。

10. **Flag Game: A Toy Model for Mechanistic Swarm Interpretability** — [arxiv.org/abs/2609.19124](http://arxiv.org/abs/2609.19124v1) | Elizabeth Pavlova & Hidenori Tanaka
    为多 Agent 涌现协同行为与“信念传播”提供可解释性玩具模型，连接群体对齐与安全。

11. **Ask the Tool, Don't Guess** — [arxiv.org/abs/2609.18849](http://arxiv.org/abs/2609.18849v1) | Yipeng Liu et al.
    让 serving 系统直接读取工具调用的进度信息而非猜测，优化 Agent 推理时的 KV cache 管理。

12. **CERA-MoA: Co-Evolving Routing Mechanisms with Continually Learning LLM Agents** — [arxiv.org/abs/2609.18779](http://arxiv.org/abs/2609.18779v1) | Jiaxuan Jiang et al.
    路由与 Agent 微调共进化，解决 MoA 路由策略跟不上 Agent 能力演化的问题。

13. **Cognitive Extensions for Dual-Process Language Agents** — [arxiv.org/abs/2609.19128](http://arxiv.org/abs/2609.19128v1) | J. M. dos Santos & A. L. Oliveira
    为 SwiftSage 双过程 Agent 增加记忆与自反思模块，提升交互环境中的长程鲁棒性。

### 🔧 方法与框架（基准、效率、可解释性）

14. **Beyond Outcomes: Dual-View Relational Learning for Efficient Agent Benchmarking** — [arxiv.org/abs/2609.18909](http://arxiv.org/abs/2609.18909v1) | Xinshuai Guo et al.
    建模任务-模型关系而非仅最终分数，大幅压缩 Agent 基准的评估成本。

15. **Decodable but Misrouted: Sparse Features Uncover a Readout Gap in VLMs** — [arxiv.org/abs/2609.18860](http://arxiv.org/abs/2609.18860v1) | Girish A. Koushik et al.
    用 SAE + 因果干预区分“证据缺失”与“证据未路由到输出”两类 VLM 失败。

16. **Using OCR Heads to Verbalize Image Semantics** — [arxiv.org/abs/2609.18823](http://arxiv.org/abs/2609.18823v1) | Sheridan Feucht et al.
    发现 OCR 必要的注意力头实为通用像素-语义映射头，VLM 机理研究佳作。

### 📊 应用（垂直领域、多模态、科学）

17. **ScienceIDE: Turning World's Scientific Codebase into Agent Learnable Environments** — [arxiv.org/abs/2609.19134](http://arxiv.org/abs/2609.19134v1) | Hejia Geng et al.
    将科学代码库转化为可执行、可验证的 Agent 学习环境。

18. **Evidence-Grounded Agentic Formulation Development in an Autonomous Laboratory** — [arxiv.org/abs/2609.19099](http://arxiv.org/abs/2609.19099v1) | Michael M. Craig et al.
    Andromeda 2 系统在自主实验室中完成药物制剂开发，科学 Agent 落地标杆。

19. **EviGen: Predictive Evidence Scaffolding for Verifiable Clinical Rationale Generation** — [arxiv.org/abs/2609.18852](http://arxiv.org/abs/2609.18852v1) | Fengnan Li et al.
    从纵向 EHR 中抽取预测性证据脚手架，生成可验证的临床推理。

20. **Interpretable MIL for Early Prediction of Key Molecular Alterations in AML** — [arxiv.org/abs/2609.18825](http://arxiv.org/abs/2609.18825v1) | Jonathan Legrand et al.
    用可解释多实例学习从常规流式细胞术数小时内预测 NPM1/FLT3 突变，临床价值极高。

21. **rMuscle: Robotic Muscle Memory for Efficient VLA Model Inference** — [arxiv.org/abs/2609.19104](http://arxiv.org/abs/2609.19104v1) | Kaijun Zhou et al.
    针对工厂重复作业的 VLA “肌肉记忆”缓存机制，显著降低推理成本。

## 三、研究趋势信号

今日论文呈现三条清晰趋势：**（1）Agent 安全与治理成为独立研究方向**——复合策略违规、O-RAN 多 Agent 稳定性、群智能可解释性、Agent 会话隐私暴露等工作，标志着社区从“让 Agent 能干”转向“让 Agent 可控”，且关注点正从单步检查升级到工作流/系统级审计。**（2）Agent 评估与基础设施精细化**：基准压缩、serving 系统与工具调用的协同设计、路由与微调共进化，反映 Agent 已进入工程化落地阶段。**（3）LLM 理论与内部机理深化**：scaling 指数可被架构改变、double descent 的最小作用量解释、reward hacking 的表征签名，暗示“干预内部表征”正成为对齐与可解释性的共同语言。

## 四、值得精读

1. **Infinite-Parameter LLMs**（[2609.18842](http://arxiv.org/abs/2609.18842v1)）：对 scaling law 与 MoE 静态参数假设的根本性挑战，若可行可能开启“动态权重生成”新范式。
2. **Monitoring and Discovering Reward Hacking with Internal Representations**（[2609.19101](http://arxiv.org/abs/2609.19101v1)）：reward hacking 是前沿模型的核心风险，基于内部表征的检测方法兼具理论与实践价值。
3. **Compositional Policy Violations**（[2609.18820](http://arxiv.org/abs/2609.18820v1)）：首次系统指出逐步合规治理的盲区，对 Agent 在金融、医疗等受监管领域部署有直接指导意义。

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*