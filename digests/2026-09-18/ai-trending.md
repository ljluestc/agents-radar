# AI 开源趋势日报 2026-09-18

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-09-18 03:47 UTC

---

# AI 开源趋势日报 · 2026-09-18

---

## 一、今日速览

今日 GitHub Trending 被 **“Agent Skills / 编码智能体能力扩展”** 强势占领：alibaba/open-code-review（+3286）、cloudflare/security-audit-skill（+3607）领衔，Skill 化、插件化的编码 Agent 生态正在成为新的增长爆发点。大厂密集入场——阿里巴巴、腾讯（BrowserSkill、WeKnora、Octop）、Cloudflare、Anthropic 同日多项目登榜，Agent 基础设施成为兵家必争之地。本地推理方向出现亮点：纯 C 实现、零依赖流式加载 MoE 专家的 colibri 引起关注。RAG/记忆层（mem0、claude-mem、graphify）在主题搜索中持续走热，“Agent 上下文工程”正演化为独立赛道。

---

## 二、各维度热门项目

### 🔧 AI 基础工具（框架 / SDK / 推理引擎 / CLI）

| 项目 | Stars | 说明 |
|---|---|---|
| [JustVugg/colibri](https://github.com/JustVugg/colibri) | +873 today | 纯 C、零依赖的 MoE 推理引擎，专家权重从磁盘流式加载，让消费级硬件跑前沿 MoE 模型，今日本地推理赛道最亮眼新星 |
| [ollama/ollama](https://github.com/ollama/ollama) | 181k | 本地大模型运行事实标准，支持 Kimi/GLM/DeepSeek/gpt-oss/Qwen 等主流开源模型 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | 8.7k | Rust 生态的模块化 LLM 应用开发框架，Rust + AI 组合持续升温 |
| [Mirrowel/LLM-API-Key-Proxy](https://github.com/Mirrowel/LLM-API-Key-Proxy) | 553 | 统一 LLM 网关：单一 API 代理多厂商，OpenAI/Anthropic 兼容 + 智能负载均衡 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 152k | 本地优先的通用 AI 前端界面，支持 Ollama/OpenAI 等，仍是自托管首选 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 166k | 模型定义框架基石，文本/视觉/多模态训练与推理一体 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 说明 |
|---|---|---|
| [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) | +3607 today | 今日榜第一。多阶段安全审计的编码 Agent Skill，产出可机读、可独立验证的发现——“Skill 即产品”范式代表 |
| [alibaba/open-code-review](https://github.com/alibaba/open-code-review) | +3286 today | 阿里大规模实战检验的混合架构代码审查：确定性流水线 + LLM Agent，行级精准评论，兼容 OpenAI/Anthropic |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | +680 today | Google Chrome 团队 Addy Osmani 出品的生产级工程 Skills 合集 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 261k（+1171 today） | Agent Harness 性能优化系统：Skills、本能、记忆、安全一体化，横跨 Claude Code/Codex/Cursor |
| [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | +1302 today | 让 Agent 使用真实已登录浏览器且不打断用户工作，CLI + 扩展形态 |
| [alphaXiv/OpenResearch](https://github.com/alphaXiv/OpenResearch) | +939 today | 把编码 Agent 变成科研 Agent，Rust 实现 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 115k | 浏览器操作 Agent 的事实标准库 |
| [n8n-io/n8n](https://github.com/n8n-io/n8n) | +281 today | 400+ 集成的可视化工作流平台，原生 AI 能力持续增强 |

### 📦 AI 应用（垂直场景产品）

| 项目 | Stars | 说明 |
|---|---|---|
| [Tencent/WeKnora](https://github.com/Tencent/WeKnora) | +1125 today | 腾讯开源 LLM 知识平台：文档 → RAG → 自主推理 Agent → 自维护 Wiki 一条链 |
| [jamiepine/voicebox](https://github.com/jamiepine/voicebox) | +667 today | 开源 AI 语音工作室：克隆、听写、创作一体 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 65k | LLM 驱动的多市场股票分析系统，零成本定时运行，中文社区爆款 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 55k | 文档/主题 → 原生 PowerPoint（含动画、图表、旁白），办公场景 Agent 化代表 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | 124k | 关键词一键生成高清短视频的 AI 工作流 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 52k | 统一接入前沿 LLM 的生产力工作室，300+ 助手 |

### 🧠 大模型 / 训练（训练、微调、教育）

| 项目 | Stars | 说明 |
|---|---|---|
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 61.5k | 2 小时从零训练 64M 参数 LLM，中文社区最佳教学项目 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 105k | PyTorch 逐步实现 ChatGPT 级 LLM 的经典教程 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4.6k | 面向系统工程师：Apple Silicon 上手写迷你 vLLM + Qwen，推理系统入门佳作 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7.5k | 评测 100+ 数据集的 LLM 评测平台 |
| [thinkwee/AgentsMeetRL](https://github.com/thinkwee/AgentsMeetRL) | 1.8k | Agentic RL 论文精选列表，与 On-Policy Distillation（AwesomeOPD）同源，反映训练范式前沿 |

### 🔍 RAG / 知识库（向量库、检索、记忆）

| 项目 | Stars | 说明 |
|---|---|---|
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 119k | 把代码库/文档/SQL/PDF 变成可查询知识图谱的 Agent Skill，本地 AST 解析、无需向量库 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 94k | 跨会话持久化 Agent 上下文，兼容 Claude Code/Codex/Gemini 等全系编码 Agent |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 65.5k | Agent 记忆层基础设施，生产级 drop-in 方案 |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | 72.8k | LLM 输入压缩：JSON 省 60–95% token、编码 Agent 省 20%，代理/MCP 多形态 |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | 35.7k | 无向量、推理式 RAG 的文档索引，“vectorless RAG”新路线 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 90.9k | RAG + Agent 融合引擎，深度文档理解 |
| [alibaba/zvec](https://github.com/alibaba/zvec) | 16k | 阿里开源轻量级进程内向量库，嵌入式检索新选项 |

> **过滤说明**：Trending 榜中 ghidra（逆向工程）、cilium（eBPF 网络）、tinycast（macOS 启动器）、ever-gauzy（ERP）、coder（开发环境）、julia 语言、cs-video-courses、Developer-Y 等非 AI 核心项目已剔除。supervision、TensorFlow/PyTorch/scikit-learn 等归入广义 ML 基础设施，因篇幅聚焦本日热点仅部分列出。

---

## 三、趋势信号分析

**1）Agent Skills 成为爆发性品类。** 今日榜前两名（security-audit-skill +3607、open-code-review +3286）均属"Skill/插件"形态——轻量、可组合、依附于 Claude Code 等宿主 Agent 的能力包。这意味着编码 Agent 的竞争已从“谁做得好”转向“生态谁繁荣”，Skill 正在成为 Agent 界的 npm 包。

**2）大厂全面押注 Agent 基础设施。** 阿里（代码审查）、腾讯（浏览器 Skill、知识平台、多 Agent 助手三连发）、Cloudflare（安全审计）、Anthropic（官方插件库）同日登榜，企业级 Agent 工具链是明确的主战场。

**3）两条新兴技术栈首次显性化：** 一是**本地 MoE 推理**（colibri 纯 C + 磁盘流式专家），呼应开源前沿模型 MoE 化趋势，消费级硬件运行大模型需求旺盛；二是 **vectorless / 知识图谱 RAG**（graphify、PageIndex），对传统向量检索路线发起挑战。

**4）上下文工程（Context Engineering）成型。** claude-mem（记忆持久化）、headroom（输入压缩）、caveman（token 缩减）同场竞争，Agent 的上下文预算管理已独立成赛道，与 token 成本压力和长上下文模型竞争直接相关。

---

## 四、社区关注热点

- **[cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill)** — 今日 stars 第一，“可验证、机读的安全审计 Skill”定义了企业级 Skill 的质量标准，值得研究其多阶段验证设计
- **[alibaba/open-code-review](https://github.com/alibaba/open-code-review)](https://github.com/alibaba/open-code-review)** — 确定性规则 + LLM 混合架构是规避纯 LLM 幻觉的工程范本，可直接接入现有 CI
- **[JustVugg/colibri](https://github.com/JustVugg/colibri)** — 零依赖纯 C 跑 MoE，本地推理极简主义的代表，关注其磁盘流式专家加载思路
- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) + [PageIndex](https://github.com/VectifyAI/PageIndex)** — vectorless RAG 阵营双子星，若你正在做知识库，值得评估是否跳过向量库
- **[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** — 号称 JSON 场景省 60–95% token 且答案不变，是 Agent 成本优化的立竿见影方案

---
*数据来源：GitHub Trending（2026-09-18）+ GitHub Search API 主题检索；Trending 榜单 stars 总量字段缺失，以今日新增为准。*

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*