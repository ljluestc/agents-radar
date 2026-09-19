# AI 开源趋势日报 2026-09-19

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-09-19 03:44 UTC

---

# 📰 AI 开源趋势日报 · 2026-09-19

---

## 一、今日速览

今日 GitHub Trending 几乎被 **AI Coding Agent 生态**“包场”：Cloudflare 的安全审计 Skill、阿里的 LLM 代码评审工具、腾讯的浏览器操控 Skill 集中登榜，标志着 **Agent Skills（技能插件）** 已成为 2026 年下半年最热门的开源叙事。同时，**Agent Harness 优化**（ECC、agent-skills、claude-mem）和 **Spec 驱动开发**（OpenSpec）走向成熟，社区关注点从“Agent 能不能干活”转向“如何让 Agent 干得更快、更省、更可控”。企业级玩家（阿里、腾讯、Cloudflare、Anthropic）密集入场，是这个赛道商业化的强烈信号。

---

## 二、各维度热门项目

### 🔧 AI 基础工具（框架、SDK、CLI、开发工具）

| 项目 | Stars | 说明 |
|---|---|---|
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | +444 today | 终端原生 agentic 编程工具，整个 Skill 生态的“母平台” |
| [alibaba/open-code-review](https://github.com/alibaba/open-code-review) | +2704 today | 混合架构代码评审：确定性流水线 + LLM Agent，阿里规模验证，内置 NPE/线程安全/SQL 注入等规则 |
| [Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec) | +296 today | Spec 驱动开发（SDD）工具，用规范文档约束 AI 编码助手，SDD 方法论的代表作 |
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐181,241 | 本地大模型推理入口，支持 Kimi、GLM、DeepSeek、gpt-oss、Qwen 等 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐166,309 | 模型定义与训练推理的事实标准框架 |
| [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | ⭐106,621 | 病毒式传播的省 token 方案：让 Agent “说原始人语”，编码 Agent 削减 65% token |
| [Mirrowel/LLM-API-Key-Proxy](https://github.com/Mirrowel/LLM-API-Key-Proxy) | ⭐554 | 统一 LLM 网关：一个 API 对接全部厂商，OpenAI/Anthropic 兼容 + 智能负载均衡 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐8,669 | Rust 生态模块化 LLM 应用框架 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 说明 |
|---|---|---|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | ⭐262,152 / +958 today | Agent Harness 性能优化系统：技能、本能、记忆、安全一体化，今日最热新兴项目之一 |
| [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) | +3006 today（今日榜首） | 多阶段安全审计 Coding-Agent Skill，机器可读、独立验证的审计结论 |
| [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | +1306 today | 让 Agent 使用你真实登录态的浏览器，CLI + 扩展，适配任意 Agent Shell |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | +675 today | Google Chrome 团队 Addy Osmani 出品的生产级工程技能包 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐246,948 | “与你共同成长的 Agent”，开源社区头部 Agent 项目 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐107,496 | 多智能体 LLM 金融交易框架，学术与实战结合的标杆 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐115,187 | 浏览器 Agent 基础设施，与 BrowserSkill 同赛道的前辈 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐187,442 | 自主 Agent 先驱，仍在持续迭代 |

### 📦 AI 应用（垂直场景解决方案）

| 项目 | Stars | 说明 |
|---|---|---|
| [TencentCloud/Octop](https://github.com/TencentCloud/Octop) | +569 today | 自托管多用户多 Agent AI 助手，企业私有化部署场景 |
| [tradesdontlie/tradingview-mcp](https://github.com/tradesdontlie/tradingview-mcp) | +79 today | MCP 连接 Claude Code 与 TradingView 桌面端，个人交易工作流自动化 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐55,210 | 文档/主题 → 原生 PowerPoint（形状、动画、图表、语音旁白），办公生产力爆款 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | ⭐124,610 | 一键生成高清短视频的自动化 AI 工作流 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐51,978 | 300+ 助手的 AI 生产力工作站，统一接入主流大模型 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | ⭐65,264 | LLM 驱动多市场股票分析：行情 + 新闻 + 决策看板 + 零成本定时推送 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐152,508 | 最流行的本地 LLM 交互界面，支持 Ollama/OpenAI API |
| [coder/coder](https://github.com/coder/coder) | +478 today | “为开发者及其 Agent 提供安全环境”——开发环境平台正式 Agent 化 |

### 🧠 大模型/训练（模型、训练与教学）

| 项目 | Stars | 说明 |
|---|---|---|
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | ⭐200,176 | 深度学习基础框架常青树 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | ⭐105,210 | PyTorch 从零实现 ChatGPT 级 LLM，最佳学习路径 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | ⭐61,615 | 2 小时从零训练 64M 参数 LLM，中文社区教学标杆 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,579 | Apple Silicon 上的迷你 vLLM 推理系统教学项目 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,456 | 覆盖 100+ 数据集的 LLM 评测平台 |
| [bojieli/ai-agent-book](https://github.com/bojieli/ai-agent-book) | ⭐48,556 | 《深入理解 AI Agent》开源书 + 配套代码，Agent 工程知识体系化 |

### 🔍 RAG/知识库（向量库、检索增强、记忆）

| 项目 | Stars | 说明 |
|---|---|---|
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | ⭐119,407 | 把代码库变成可查询知识图谱的 Skill，本地 AST 解析、无需向量库——RAG 新范式 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐94,216 | 跨会话持久上下文：AI 压缩会话历史并注入后续会话，兼容所有主流 Agent |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐90,967 | RAG + Agent 融合引擎，企业级 RAG 首选 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐65,614 | Agent 记忆层基础设施，生产级持久上下文方案 |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | ⭐72,974 | LLM 输入压缩：编码 Agent 省 20%、JSON 省 60-95% token，答案不变 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐46,157 | 云原生向量数据库头部项目 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | ⭐12,946 | MLSys 2026 最佳论文：省 97% 存储的个人设备 RAG |
| [supermemoryai/supermemory](https://github.com/supermemoryai/supermemory) | +140 today | 可完全本地运行的记忆与上下文引擎，“AI 时代的 Memory API” |

> **已过滤**：anki（间隔重复记忆卡）、rustfs（对象存储）、supabase（通用数据库平台）、hister（自建搜索引擎，无 AI 特性）、gitdiagram（通用图表工具）、Julia/cs-video-courses 等泛 ML 关联但非 AI 直接相关的项目。

---

## 三、趋势信号分析

**1）Agent Skills 生态全面爆发。** 今日热榜 Top 5 中有三个是 Skill 类项目（security-audit-skill +3006、open-code-review +2704、BrowserSkill +1306），加上 agent-skills、graphify、claude-mem 等，"Skill" 已成为独立品类——围绕 Claude Code / Codex / Cursor 等宿主构建可复用能力包，正复制当年 VS Code 插件生态的路径。

**2）Harness 工程化与 token 经济成为新焦点。** ECC（26 万 stars）、caveman、headroom、ponytail 等项目共同指向一个命题：Agent 的竞争力正从模型能力转向**上下文工程与成本工程**——压缩输入、持久记忆、精简输出。

**3）大厂与学术界双线入场。** Cloudflare（安全审计）、阿里（代码评审）、腾讯（浏览器操控、私有助手）将 Skill 从个人玩具推向企业级；LEANN 拿下 MLSys 2026 最佳论文说明学界也在响应“个人设备 RAG / 去 RAG”方向。垂直方向上，金融 Agent（TradingAgents、Vibe-Trading、daily_stock_analysis）持续走热，与近月 agentic RL、Process Reward Model 的研究热度形成呼应。

---

## 四、社区关注热点

- **[cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill)** — 今日 +3006 stars 居首，“机器可读 + 独立验证”的审计范式可能成为 Agent 安全类 Skill 的模板。
- **[alibaba/open-code-review](https://github.com/alibaba/open-code-review)** — 确定性规则 + LLM 混合架构是规避 LLM 幻觉的工程范本，阿里规模验证，适合直接落地。
- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** — 26 万 stars 的 Harness 优化系统，代表“Agent 操作系统层”的新叙事，值得跟踪其 Skills/Instincts 设计。
- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** — 知识图谱 + AST 的“无向量库 RAG”路线，对传统向量检索构成挑战。
- **[Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill)** — 复用真实登录态浏览器是浏览器自动化的务实解法，与 browser-use 的对比值得关注。

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*