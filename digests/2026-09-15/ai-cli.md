# AI CLI 工具社区动态日报 2026-09-15

> 生成时间: 2026-09-15 03:57 UTC | 覆盖工具: 11 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Pi](https://github.com/earendil-works/pi)
- [oh-my-pi](https://github.com/can1357/oh-my-pi)
- [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具生态横向对比分析报告

**数据日期：2026-09-15 | 覆盖 11 个主流工具**

---

## 1. 生态全景

AI CLI 工具已进入“多智能体 + 扩展生态 + 桌面化”的深水区竞争阶段。头部工具（Claude Code、Codex、OpenCode）同时押注扩展机制/插件生态与 Windows 支持，表明生态锁定正在成为核心竞争维度。多智能体（subagent/Fleet/Agent Factory）在所有工具中都已落地，但**可靠性问题（挂起、误报成功、静默失败）同步成为最高频的社区投诉**。成本可观测性（token 计费、缓存费率、配额归因）从边缘需求上升为跨工具的共性痛点。Windows 平台在多个工具中同时暴露高密度缺陷，是当前生态公认的质量洼地。

---

## 2. 各工具活跃度对比

| 工具 | 热点 Issues（今日活跃） | PR 更新 | Release | 今日焦点 |
|---|---|---|---|---|
| **Claude Code** | 10 条重点（最高 426👍） | 3 条 | **2 个**（v2.1.271/272） | Mods/function hooks 生态确认“数周内”交付 |
| **OpenAI Codex** | 10 条重点 | 10+ 条 | **4 个 alpha**（0.155.0 系列） | daemon 独立化、Windows 沙箱密集 PR |
| **Gemini CLI** | 10 条重点 | 10+ 条 | 1 个 nightly | 企业安全加固 P1/P2 修复密集 |
| **Copilot CLI** | 10 条（24 条更新） | 0（内部流水线） | **3 个**（1.0.84-6→8） | Agent Factory 控制、MCP 兼容修复 |
| **OpenCode** | 10 条重点 | 10+ 条 | 1 个（v1.18.31） | 旧布局强制移除引发争议（63👍） |
| **Qwen Code** | 10 条重点 | 10 条 | 1 稳定版 + nightly + 2 驱动版 | 扩展系统稳定性、hooks 重构 |
| **DeepSeek TUI** | 10 条重点 | 5 条 | 0（0.9.13 验证中） | GPUI 桌面端路由密集落地 |
| **Pi** | 10 条重点 | 10+ 条 | 0 | 缓存计费准确性、上下文完整性 |
| **oh-my-pi** | 10 条重点（61 Issue 更新） | 26+ 条（151 更新） | **2 个**（v18.1.21/22） | Antigravity 虚假 429（102 评论）、密钥泄露修复 |
| **Kimi Code CLI** | 4 条 | 0 | 0 | CJK/IME 输入体验、审阅工作流需求 |
| **DeepSeek Harness** | 0 | 0 | 0 | 无活动 |

**观察**：oh-my-pi 与 Pi 的原始更新量（61/151 条）显示小体量社区的单用户贡献密度反而最高；Copilot CLI 以 Release 交付替代公开 PR，透明度最低；Kimi 与 DeepSeek Harness 处于低活跃区间。

---

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **成本/计费可观测性** | Claude Code、Codex、Pi、oh-my-pi、Gemini CLI | token 熔断器（CC #85422）、消耗异常飙升（CC #93596）、幽灵扣额（Codex #42765）、缓存 1h/5m 费率错算（Pi #9457）、闲置扣减（Codex #43566） |
| **多智能体可靠性** | Gemini CLI、Copilot CLI、Qwen Code、DeepSeek TUI、Claude Code | MAX_TURNS 误报成功（Gemini #22323）、子代理分钟级延迟/无限"running"（Copilot #4849/4850）、子代理无法可靠执行（DS TUI #5529）、后台任务误杀（CC #78674） |
| **扩展/插件/hook 生态** | Claude Code（Mods）、Qwen Code（hooks 事件化）、oh-my-pi（Marketplace）、OpenCode（插件 SDK）、Pi（扩展 API） | 各工具均在构建第三方扩展机制，且均暴露“插件能力声明与实际行为不一致”问题 |
| **Windows 平台支持** | Claude Code、Codex、Qwen Code、Pi、Copilot CLI | Plan9 挂载失效（CC #92984）、rename_staging EPERM 59GB（Codex #42484）、扩展卸载 EPERM（Qwen #11883）、进程树孤儿（Pi #9129）、PowerShell 窗口闪烁（Copilot #4549） |
| **会话持久化与恢复** | Codex、OpenCode、Pi、Gemini CLI、DeepSeek TUI | 中断后 transcript 保留（Codex PR #45549）、压缩不持久化（Gemini #21335）、孤儿 toolCall/残留 thinking 块（Pi #9306/#9391）、会话恢复状态丢失（OpenCode v1.18.31） |
| **第三方 Provider 兼容** | Codex、Qwen Code、Pi、oh-my-pi、Copilot CLI | DeepSeek/Gemini/Grok 经 OpenAI 兼容层的 schema、签名、reasoning 字段处理是系统性短板 |
| **沙箱与企业策略** | Gemini CLI、Copilot CLI、Qwen Code、Codex | 策略目录权限校验、沙箱绕过（Copilot #4846）、ACP 模式零确认执行（Qwen #11887）、Linux bwrap 后端（Qwen PR #11614） |

---

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线 |
|---|---|---|---|
| **Claude Code** | Mods 扩展生态、Cowork、云端 Remote 会话 | 重度专业开发者、企业 | TypeScript、封闭开源仓库、生态平台化 |
| **OpenAI Codex** | daemon 架构、沙箱、CUA 浏览器控制、Automations | ChatGPT 订阅用户 | Rust、alpha 高速迭代、订阅捆绑 |
| **Gemini CLI** | 企业安全、Auto Memory、A2A、AST 代码理解 | 企业/合规敏感用户 | TypeScript、nightly 节奏、安全优先 |
| **Copilot CLI** | Agent Factory、企业策略、BYOK 多模型 | GitHub 生态企业用户 | 封闭开发、Release 交付 |
| **OpenCode** | 桌面/TUI/Web 多端、Code Mode 解释器、worktree | 独立开发者、本地模型用户 | TypeScript/Bun、开源社区驱动 |
| **Qwen Code** | channels 多会话协作、DingTalk 集成、Web Terminal | 中文生态、团队协作场景 | 分叉系、快速功能扩张 |
| **DeepSeek TUI / Pi / oh-my-pi** | Fleet/多 provider、多账号轮换、轻量 | 高级用户、自托管/多模型玩家 | Rust（TUI）、TS（Pi 系）、极限可配置 |

**关键分野**：Claude Code/Codex 走“平台+订阅”路线；Gemini CLI 押注企业合规；Pi 系工具代表“多 provider 中立层”路线，直接受益于头部工具的配额经济痛点。

---

## 5. 社区热度与成熟度

- **第一梯队（生态平台期）**：Claude Code（单 issue 426👍，社区反馈实质影响官方设计）、Codex（付费用户投诉集中但 PR 吞吐量大）
- **快速迭代期**：Codex（日发 4 alpha）、Qwen Code（P1 密集但功能激进）、oh-my-pi（151 条 PR 更新，单人维护高产出）
- **争议调整期**：OpenCode（旧布局强制移除 + macOS 全量报错，信任消耗中）
- **稳步工程化**：Gemini CLI、DeepSeek TUI（里程碑式 stacked PR、crate 拆解，工程纪律最佳）
- **低活跃**：Kimi Code CLI、DeepSeek Harness

**成熟度信号**：Bug 类型可作代理指标——头部工具的 issue 已从“基础可用性”转向“计费精度、并发架构、策略作用域”等深层问题；Qwen Code/OpenCode 仍处于 P1 级基础缺陷高发期。

---

## 6. 值得关注的趋势信号

1. **配额经济驱动用户行为**：多账号轮换、欧洲合规网关、模型 role 路由（oh-my-pi PR #12103）成为高频需求——**AI CLI 选型时 provider 中立性正在变成采购考量**。
2. **“静默失败”是自动化信任的杀手**：误报成功、幽灵扣额、无提示崩溃在 6+ 工具中出现。构建 agent 工作流时应假设失败不可见，**checkpoint 和独立验证层必不可少**。
3. **扩展生态军备竞赛开启**：Claude Mods、Qwen hooks、Marketplace 插件同期推进，但均暴露权限/隔离缺口（CC #92533、Qwen #11887、Copilot #4846）。**hook 类机制在安全关键场景应先做隔离审计**。
4. **Windows 是系统性短板**：跨所有工具的高缺陷密度与各官方“重点投入 Windows”的 PR 流向吻合，Windows 生产部署仍需谨慎评估。
5. **对开发者的实操建议**：生产环境锁定稳定版（Codex 0.154.0 的 MCP 回归、Claude Code 2.1.269 的 WSL2 回归均为警示）；订阅制用户关注计量异常类 issue；自托管/多模型用户可关注 Pi 系与 OpenCode 作为配额规避路径。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至 2026-09-15）

## 一、热门 Skills 排行

基于 PR 活跃度与关联 Issue 讨论，社区关注度最高的 Skills 动态如下：

| # | Skill / PR | 功能与讨论热点 | 状态 |
|---|---|---|---|
| 1 | **skill-creator 可靠性修复**（[PR #1298](https://github.com/anthropics/skills/pull/1298)） | 修复触发评估误报、Windows `select()` 失败、运行时错误被误判为非触发等问题。关联 [Issue #556](https://github.com/anthropics/skills/issues/556)（`claude -p` 触发率 0%，12 条评论），触发评估可靠性是 skill-creator 最核心的痛点 | OPEN |
| 2 | **mcp-builder 系列修复**（[PR #1742](https://github.com/anthropics/skills/pull/1742)、[PR #1724](https://github.com/anthropics/skills/pull/1724)） | 适配 `mcp>=2.0` API 重命名（`streamable_http_client`）与自定义 header；评估默认模型升级至 claude-sonnet-5。关联 [Issue #1390](https://github.com/anthropics/skills/issues/1390)：评估器对真实 MCP 服务器始终得 0 分（TextContent 序列化 bug），是近期最热的 bug | OPEN |
| 3 | **document-typography**（[PR #514](https://github.com/anthropics/skills/pull/514)） | 修版质量控制：孤行、寡段、编号错位等 AI 生成文档的通病。“用户从不主动要求排版，但都受影响”——长期挂起但观点独特 | OPEN |
| 4 | **frontend-design 改进**（[PR #210](https://github.com/anthropics/skills/pull/210)） | 提升官方前端设计 skill 的清晰度与可执行性，确保每条指令 Claude 能在单次会话内落实 | OPEN |
| 5 | **odt skill**（[PR #486](https://github.com/anthropics/skills/pull/486)） | OpenDocument 创建、模板填充与 HTML 转换，补齐开源格式文档能力缺口 | OPEN |
| 6 | **meta skills：skill-quality-analyzer / skill-security-analyzer**（[PR #83](https://github.com/anthropics/skills/pull/83)） | 用 skill 审查 skill 的元能力工具，呼应社区对 skill 质量与安全的持续关注 | OPEN |
| 7 | **Hivemind 多智能体编排**（[PR #1628](https://github.com/anthropics/skills/pull/1628)） | 零成本方案：Claude Code 做规划者，将机械性工作下放给免费模型的 headless opencode worker，代表“省上下文/省成本”路线 | OPEN |
| 8 | **pyxel 复古游戏开发**（[PR #525](https://github.com/anthropics/skills/pull/525)） | 对接 pyxel-mcp，覆盖“编写→运行截图→检查→迭代”的复古游戏工作流，活跃维护至 9 月 | OPEN |

## 二、社区需求趋势

从高评论 Issues 提炼出的期待方向：

1. **安全与信任边界**（[Issue #492](https://github.com/anthropics/skills/issues/492)，43 条评论，最热）：社区 skill 冒用 `anthropic/` 命名空间分发，用户可能在误信下授予高权限——签名/命名空间隔离是头号诉求。
2. **组织级 skill 分发**（[Issue #228](https://github.com/anthropics/skills/issues/228)，16 条评论）：组织内共享 skill 库，取代 Slack 手传 `.skill` 文件。
3. **上下文效率**（[Issue #1487](https://github.com/anthropics/skills/issues/1487)）：claude-api skill 单次注入约 156k token 耗尽上下文，暴露了 skill 的渐进式加载（progressive disclosure）设计缺陷；[Issue #1329](https://github.com/anthropics/skills/issues/1329) 提议 compact-memory 符号化压缩 agent 状态，同属此方向。
4. **Skill/MCP 融合**（[Issue #16](https://github.com/anthropics/skills/issues/16)）：将 skill 能力暴露为 MCP 工具 API 的架构讨论。
5. **平台兼容性**（[Issue #29](https://github.com/anthropics/skills/issues/29)）：AWS Bedrock 等非一方平台的支持。
6. **质量门禁与治理**（[Issue #1385](https://github.com/anthropics/skills/issues/1385)、[Issue #412](https://github.com/anthropics/skills/issues/412)）：校准→对抗审查→交付验证的推理质量管线、agent 治理模式。
7. **包管理去重**（[Issue #189](https://github.com/anthropics/skills/issues/189)）：document-skills 与 example-skills 内容重复，浪费上下文窗口。

## 三、高潜力待合并 Skills

近期更新活跃、可能落地的 OPEN PR：

- **[PR #1742](https://github.com/anthropics/skills/pull/1742)** mcp-builder 适配 mcp≥2 —— 修复高优 Issue #1668，9 月仍活跃，合并概率高
- **[PR #541](https://github.com/anthropics/skills/pull/541)** docx 修订 ID 冲突修复 —— 根因明确（OOXML 共享 `w:id` 空间），修复文档损坏类硬 bug
- **[PR #1607](https://github.com/anthropics/skills/pull/1607)** claude-api skill 更新已退役模型 ID —— 对应 Issue #1603，典型文档时效性修复
- **[PR #1765](https://github.com/anthropics/skills/pull/1765)** office redlining UTF-8 解码修复 —— 对应 Issue #1707，覆盖非 ASCII 文档与 Windows 场景
- **[PR #1602](https://github.com/anthropics/skills/pull/1602)** 评估序列化与编码综合修复 —— 直接回应 Issue #1390 的 0/N 评分 bug
- **[PR #525](https://github.com/anthropics/skills/pull/525)** pyxel skill —— 2026-03 提交、09-13 仍更新，维护意愿强

## 四、Skills 生态洞察

**当前社区最集中的诉求是：把 Skills 从“能用的 prompt 片段”升级为“可信的工程化资产”——即安全可信的分发机制（命名空间/签名）、可靠的触发与评估工具链，以及对上下文窗口的精细化控制。**

---

# Claude Code 社区动态日报 · 2026-09-15

---

## 1. 今日速览

Claude Code 连发两个版本：v2.1.271 为 Remote 会话带来 fast mode、v2.1.272 跟进稳定性修复。备受期待的 **Mods 扩展机制（#91870，175 评论）** 官方确认将在数周内交付 function hooks，相关生态 PR 已开始落地。此外，Windows KB5124008 更新导致 Cowork Plan9 挂载全面失效（113 评论）成为今日最严重的外部兼容性事故。

---

## 2. 版本发布

- **[v2.1.271](https://github.com/anthropics/claude-code/releases/tag/v2.1.271)**
  - Remote 会话（云端及自托管 runner）新增 **fast mode**：可在会话中输入 `/fast` 或继承宿主机 fast-mode 设置（受组织策略限制）
  - 全屏模式下 `/config` 面板支持鼠标操作：滚轮可滚动设置项
- **[v2.1.272](https://github.com/anthropics/claude-code/releases/tag/v2.1.272)**
  - Bug 修复与可靠性改进

---

## 3. 社区热点 Issues

| # | Issue | 关注理由 |
|---|-------|---------|
| 1 | [#91870 Mods — 让 Claude 扩展性提升 10 倍](https://github.com/anthropics/claude-code/issues/91870) | **今日最重要动态**。官方 9/9 更新确认 function hooks 将在“数周内”（而非数天）发布。175 评论 / 105 👍，社区反馈已实质影响设计方向 |
| 2 | [#77136 Claude 4.7/4.8/5.0/Fable 文风退化](https://github.com/anthropics/claude-code/issues/77136) | 426 👍 为今日最高。多代模型出现重复修辞癖好、散文连贯性差的问题，即使有明确风格指令也难以纠正，属模型层而非客户端层缺陷 |
| 3 | [#92984 Windows KB5124008 导致 Plan9 挂载全灭](https://github.com/anthropics/claude-code/issues/92984) | 113 评论。Windows 更新后 Cowork 所有 Plan9 共享失败，卸载 KB 可恢复。有稳定复现，影响面大 |
| 4 | [#93596 Opus 5 @xhigh 自 9/11 起消耗异常飙升](https://github.com/anthropics/claude-code/issues/93596) | 无任何客户端改动的情况下，thinking 块出现在 ~100% 请求且输出 token 增加 2-7 倍，疑似服务端配置变更 |
| 5 | [#85422 Token 消耗熔断器需求](https://github.com/anthropics/claude-code/issues/85422) | 请求运行时强制消费上限（含 hooks/plugins/subagents 归因），而非仅警告。与 #93596 呼应，成本控制呼声强烈 |
| 6 | [#86928 沙箱 Bash 间歇性失败](https://github.com/anthropics/claude-code/issues/86928) | 约 1/10 的沙箱调用报 `unshare(CLONE_NEWUSER): Invalid argument`，已复现，影响沙箱功能可信度 |
| 7 | [#88405 `.claude/rules/` 符号链接未自动加载](https://github.com/anthropics/claude-code/issues/88405) | 实现与官方文档直接矛盾，破坏多项目共享 rules 的标准工作流 |
| 8 | [#93782 2.1.269 回归：WSL2 下 VS Code 终端无法粘贴](https://github.com/anthropics/claude-code/issues/93782) | 语音听写工具（Wispr Flow 等）粘贴失效，2.1.268 正常，明确的版本回归 |
| 9 | [#92533 function hooks 破坏 worktree 隔离](https://github.com/anthropics/claude-code/issues/92533) | 任何 `tool.call` hook 挂到 Bash 后，子代理的 worktree 隔离全面失效——对即将发布的 function hooks 是重要前置警告 |
| 10 | [#78674 Linux 内存压力收割器误杀后台任务](https://github.com/anthropics/claude-code/issues/78674) | MemAvailable 充足、PSI≈0 时仍批量杀死所有 `run_in_background` 任务，判断逻辑疑似只看 MemFree |

---

## 4. 重要 PR 进展

> 本周期仅 3 条 PR 更新，重点在 Mods 生态：

1. **[#94184 mods/diff: 固定头部 + 滚轮路由优化](https://github.com/anthropics/claude-code/pull/94184)**（已关闭）
   来自 Mods 主设计者 @poteat。停靠面板与内置 `/diff` 面板逐帧对齐：头部、base 行和 8 行文件列表固定，滚轮按 3 行/格滚动 hunks，支持 ctrl/opt+↑↓ 快捷键。**Mods 生态正在快速逼近内置功能的水准**。
2. **[#71627 docs(sandbox): 说明 prompt 批准的主机为会话级作用域](https://github.com/anthropics/claude-code/pull/71627)**（开放中）
   文档澄清：沙箱网络 prompt 批准的主机仅在当前会话有效，重启/恢复会丢失——补齐 settings README 的关键缺口。
3. **[#83890 Create pylint.yml](https://github.com/anthropics/claude-code/pull/83890)**（已关闭）
   社区提交的 CI 配置，已被关闭，无实质影响。

---

## 5. 功能需求趋势

- **Mods / 扩展生态（最热）**：function hooks 是绝对焦点，社区已在构建用量监控、成本台账、diff 面板等 mods（#91870、#94184、#94424），并要求增加 usage/rate-limit 变更事件（#94424）
- **成本可观测与控制**：消费熔断器（#85422）、token 异常消耗（#93596）、每轮成本追踪
- **Windows 平台质量**：今日多个高热度 issue 均为 Windows（Plan9/KB 兼容 #92984、Bash 反斜杠 #89392、MSIX 闪烁 #79220、MCP 就绪 #92758）
- **会话与工作流管理**：Routines 列表为空/无法自归档（#92773、#94418）、会话无法删除（#93835）、Cowork 默认项目目录（#44933）
- **IDE 集成打磨**：VS Code 权限模式丢失（#85077）、diff 重复弹出（#84542）、网络驱动器会话列表（#78461）

---

## 6. 开发者关注点

1. **Windows 是当前质量洼地**：过去 24 小时高热度 issue 中 Windows 相关占比过半，尤其 Cowork + Plan9 挂载被系统更新直接打断，建议 Windows 用户暂缓安装 KB5124008
2. **成本失控焦虑升温**：服务端疑似变更导致消耗倍增（#93596）叠加缺乏硬性熔断机制（#85422），重度用户对 token 可观测性和上限控制需求迫切
3. **Function hooks 落地前的隐患**：已知 hooks 会破坏 worktree 隔离（#92533）、条件 skills 在 auto 模式下永不触发（#90004），官方“数周内”交付前需关注这些结构性修复
4. **文档与实现的漂移**：rules 符号链接（#88405）、沙箱会话级批准（#71627）等案例表明，依赖文档的工作流需自行验证
5. **升级节奏建议**：2.1.269 存在 WSL2 粘贴回归（#93782），受影响用户可参考 2.1.268 等待修复确认

---

*数据来源：anthropics/claude-code GitHub（过去 24 小时）*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报
**日期：2026-09-15 | 数据来源：github.com/openai/codex**

---

## 1. 今日速览

今日 Codex 发布了 4 个 Rust v0.155.0 alpha 预发布版本，迭代节奏密集。社区焦点仍集中在 **容量限制/"Selected model is at capacity"** 相关问题上，多个高热度 Issue 持续发酵。Windows 平台的浏览器控制、沙箱安装（EPERM/rename_staging）以及 DeepSeek 等第三方 Responses 兼容供应商的兼容性问题构成今日三大痛点主线。

---

## 2. 版本发布

过去 24 小时连发 4 个 alpha 预发布：

| 版本 | 说明 |
|---|---|
| `rust-v0.155.0-alpha.6` | 最新预发布 |
| `rust-v0.155.0-alpha.5` | 日常迭代 |
| `rust-v0.155.0-alpha.4` | 日常迭代 |
| `rust-v0.155.0-alpha.2.4` | 分支补丁 |

均为 alpha 阶段，无正式 changelog，主要供内部验证与新功能灰度（结合今日 PR 看，涉及 daemon 独立打包、Windows 沙箱注册、附件 API 等）。正式用户仍以 0.154.0 稳定版为主。

---

## 3. 社区热点 Issues

1. **[#28507](https://github.com/openai/codex/issues/28507) — "Selected model is at capacity"（53 评论 / 50 👍）**
   最受关注的老问题，Pro 5x 用户长期受模型容量限制困扰，今天仍在活跃更新，说明问题持续未解。

2. **[#43410](https://github.com/openai/codex/issues/43410) — Windows 浏览器控制在 API-key 认证下失败（30 评论 / 17 👍）**
   Edge 插件可连接，但首个操作即报 `unsupported Codex auth method: apikey`，是 Windows + 浏览器控制用户的核心阻断问题。

3. **[#43237](https://github.com/openai/codex/issues/43237) — GPT-6 Astra 拒绝 `hi` 输入，invalid_prompt（15 评论）**
   跨 Linux/macOS 的最小复现，指向模型侧或 API 兼容性问题，诊断质量高。

4. **[#42765](https://github.com/openai/codex/issues/42765) — Pro 用户周额度从 ~45% 神秘降至 0%（13 评论）**
   无任何会话运行的情况下额度被消耗，与 [#43566](https://github.com/openai/codex/issues/43566)（闲置时额度递减）共同指向配额计量/后台任务问题。

5. **[#44458](https://github.com/openai/codex/issues/44458) — CLI 0.154.0 实验特性破坏捆绑 MCP 启动（12 评论）**
   macOS 上 Messages 与 Computer History 两个内置 MCP server 在新 CLI 下启动失败，影响 gpt-6-astra 用户。

6. **[#44723](https://github.com/openai/codex/issues/44723) — Automations 注入缺少 call_id 的 function_call_output（8 评论）**
   heartbeat/cron 触发后目标会话永久性 400 报错，属于会话损坏级别的严重缺陷。

7. **[#45019](https://github.com/openai/codex/issues/45019) — "Queued follow-up no longer exists"（6 评论 / 26 👍）**
   👍 数今日最高，排队跟进消息提交失败影响 Pro 20x 用户工作流。今日新开的 [#45592](https://github.com/openai/codex/issues/45592) 为同问题复现（已关闭，或已修复/合并处理）。

8. **[#29915](https://github.com/openai/codex/issues/29915) — 权限/审批模式选择不持久化（6 评论）**
   长期存在的沙箱权限设置体验问题，新老会话均受影响。

9. **[#42484](https://github.com/openai/codex/issues/42484) — Windows `cua_node rename_staging` EPERM 死循环，占用 ~59GB（5 评论）**
   桌面 UI 冻结 + 磁盘爆炸，今日新复现 [#45593](https://github.com/openai/codex/issues/45593) 表明启动路径仍存在 EPERM 时序问题。

10. **[#45585](https://github.com/openai/codex/issues/45585) — tool_search 空 schema 永久破坏 DeepSeek 线程（新）**
    与 [#37786](https://github.com/openai/codex/issues/37786) 同属“严格 Responses 供应商兼容性”系列，自定义 provider 生态的系统性问题。

---

## 4. 重要 PR 进展

> 今日合入 PR 以 bot（copyberry）批量合并为主，聚焦三大方向：**daemon 独立化、Windows 沙箱、附件/线程可靠性**。

1. **[#45546](https://github.com/openai/codex/pull/45546) — daemon 包从 CLI 独立安装中拆出**
   daemon 更新不再捆绑 CLI 版本选择，配套 [#45558](https://github.com/openai/codex/pull/45558)（从本地 CLI 包播种 daemon）、[#45580](https://github.com/openai/codex/pull/45580)（`daemon update --from-cli` 显式替换）。

2. **[#45542](https://github.com/openai/codex/pull/45542) — Windows 沙箱账户的服务级包注册**
   新增 `registered_core` 供应模式，为托管沙箱账户注册应用包并记录 runner 别名。

3. **[#45550](https://github.com/openai/codex/pull/45550) — Windows 沙箱 opt-in 注册包执行**
   通过服务记录的执行别名启动注册 runner，含所有权与包 ID 校验。

4. **[#45559](https://github.com/openai/codex/pull/45559) — 服务重启后恢复 Windows 沙箱注册刷新**
   修复供应服务重启导致注册流程中断的问题。

5. **[#45556](https://github.com/openai/codex/pull/45556) — 附件上传与解析 API**
   `AttachmentStore` 改为 `upload`/`resolve` 模型，支持文件 ID 与下载 URL 生命周期管理。

6. **[#45579](https://github.com/openai/codex/pull/45579) — 线程 fork 时复制附件**
   非临时 fork（含早前轮次的 fork）现在保留源线程附件。

7. **[#45549](https://github.com/openai/codex/pull/45549) — 中断/失败的 turn 保留已流式输出的答案与 plan**
   避免中断导致 transcript 内容缺失。

8. **[#45548](https://github.com/openai/codex/pull/45548) / [#45534](https://github.com/openai/codex/pull/45534) — Seatbelt 与 Linux 沙箱正确处理 Unix socket 权限**
   修复显式授权的 Unix socket 在 macOS/Linux 沙箱中被拒绝的问题。

9. **[#45537](https://github.com/openai/codex/pull/45537) — Guardian reviewer 生命周期移入扩展**
   确保父进程关闭或历史重置时停止 review，含限流重试场景下的清理。

10. **[#45529](https://github.com/openai/codex/pull/45529) — app-server 暴露 workspace 路由信息**
    新增实验性 `workspaceRouting` 元数据，暴露 ChatGPT workspace ID 与后端路由（`us`/`us_cr`）。

其他值得注意：[#45543](https://github.com/openai/codex/pull/45543)（统一 `ImageReference` 类型）、[#45544](https://github.com/openai/codex/pull/45544)（禁止日志输出完整图片生成结果）、[#45535](https://github.com/openai/codex/pull/45535)（工具分析事件按调用来源分类）。

---

## 5. 功能需求趋势

- **配额透明度与计费可靠性**：容量错误、闲置时额度异常扣减是最高频主题（#28507、#42765、#43566、#45192），社区强烈要求明确的用量归因与后台任务计量。
- **浏览器/电脑操控（CUA）**：Chrome/Edge 插件的安装、发现、认证兼容性问题集中（#43410、#40357、#45249、#45589、#45584），Windows 侧尤为突出。
- **第三方/自定义模型供应商支持**：DeepSeek 等严格 Responses 供应商的 schema 兼容（#44723、#37786、#45585）正成为系统性短板。
- **Windows 平台体验**：沙箱、启动 EPERM、性能占用问题占比极高，与官方近期密集合入 Windows 沙箱 PR 形成呼应。
- **自动化与可观测性**：Automations 稳定性（#44723）及本地日志中的 Skill 调用归因（#41760）需求上升。
- **多智能体（subagent）**：多智能体提示词中的委派指令冲突（#36973）显示该功能仍需打磨。

---

## 6. 开发者关注点

1. **额度/容量不可预测是最大痛点**：付费 Pro/20x 用户频繁遭遇 capacity 错误和“幽灵扣额”，且长任务中断后无法恢复，直接损害付费信任。
2. **会话永久性损坏类 Bug 需优先修复**：Automations 缺 call_id、tool_search 空 schema 等问题一旦触发即不可恢复，比瞬时错误更严重。
3. **Windows 仍是一等公民中的薄弱环节**：从启动 EPERM、rename_staging 死循环到浏览器插件安装失败，Windows 用户的问题密度显著高于 macOS/Linux；官方 PR 流向显示正在重点投入。
4. **自定义 provider 用户被边缘化**：多项兼容性问题长期 OPEN，建议依赖官方 API 或关注 wire_api 兼容性修复进展。
5. **CLI alpha 迭代过快带来的回归风险**：0.155.0 一天 4 个 alpha，同时 0.154.0 已暴露 MCP 启动回归（#44458），建议生产环境锁定稳定版。

---
*本报告基于 GitHub 公开数据自动整理，观点仅供技术参考。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 · 2026-09-15

## 1. 今日速览

今日发布 v0.61.0-nightly.20260915 夜间版本（迭代构建，无独立 changelog）。社区讨论焦点集中在 **Agent/子代理稳定性**（挂起、误报成功、内存系统问题）和 **企业级安全加固**（策略目录权限校验、日志脱敏、沙箱递归限制），多个 P1 级修复 PR 密集提交。

## 2. 版本发布

- **v0.61.0-nightly.20260915.g9c1b0a610**（2026-09-15）
  [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260914.g9c1b0a610...v0.61.0-nightly.20260915.g9c1b0a610)
  常规 nightly 自动构建，对应自动版本提升 PR [#29337](https://github.com/google-gemini/gemini-cli/pull/29337)。

## 3. 社区热点 Issues

1. **#22323** 子代理达到 MAX_TURNS 后仍上报 GOAL 成功，掩盖中断事实（P1，13 条评论）— 影响任务可靠性判定，是 Agent 可观测性核心问题。[链接](https://github.com/google-gemini/gemini-cli/issues/22323)
2. **#19873** 利用模型原生 bash 能力 + 零依赖 OS 沙箱与执行后意图路由（9 条评论）— 方向性增强提案，探讨安全与能力的平衡。[链接](https://github.com/google-gemini/gemini-cli/issues/19873)
3. **#21409** Generalist agent 无限挂起，简单操作也卡死（P1，👍 8）— 高影响稳定性 bug，用户只能手动禁止子代理规避。[链接](https://github.com/google-gemini/gemini-cli/issues/21409)
4. **#22745** EPIC：评估 AST 感知的文件读取/搜索/代码库映射（7 条评论）— 通过精确读取方法边界降低 token 消耗与轮次浪费。[链接](https://github.com/google-gemini/gemini-cli/issues/22745)
5. **#29141** DevTools HTTP 流在 chunk 边界切分多字节 UTF-8 字符导致乱码（6 条评论）— 小而典型的流式解码 bug。[链接](https://github.com/google-gemini/gemini-cli/issues/29141)
6. **#21968** 模型几乎不主动使用自定义 skills 和子代理（6 条评论）— 反映自动编排/工具选择策略的普遍痛点。[链接](https://github.com/google-gemini/gemini-cli/issues/21968)
7. **#26525** Auto Memory 需确定性脱敏并减少日志量（P2，安全）— 秘密先进入模型上下文再脱敏，流程设计存在风险。[链接](https://github.com/google-gemini/gemini-cli/issues/26525)
8. **#25166** Shell 命令完成后仍卡在 "Waiting input"（P1，👍 3）— 高频执行流挂起问题。[链接](https://github.com/google-gemini/gemini-cli/issues/25166)
9. **#26522** Auto Memory 对低信号会话无限重试 — 会话索引状态管理缺陷，配合 #26516 形成内存系统问题群。[链接](https://github.com/google-gemini/gemini-cli/issues/26522)
10. **#21335** `/compress` 压缩结果不持久化到会话文件，resume 后失效 — 影响 token 节省的实际效果。[链接](https://github.com/google-gemini/gemini-cli/issues/21335)

其他值得一提：Browser Agent 相关问题密集（#21983 Wayland 失败、#22267 忽略 settings.json 覆盖、#22232 会话接管恢复），子代理生态仍是问题高发区。

## 4. 重要 PR 进展

1. **#29335**（P1）修复 `AgentLoopContext` 属性在对象展开后丢失 — Config 类此前用原型 getter 实现接口，spread 会静默丢属性。[链接](https://github.com/google-gemini/gemini-cli/pull/29335)
2. **#29328**（P1，security）A2A server 日志遵循 LOG_LEVEL 并防止凭据泄露。[链接](https://github.com/google-gemini/gemini-cli/pull/29328)
3. **#29332**（P2）限制单次调用可触发沙箱扩展的次数 — 修复无限递归导致的堆内存溢出崩溃。[链接](https://github.com/google-gemini/gemini-cli/pull/29332)
4. **#29336**（P2，enterprise）对所有层级策略目录强制安全权限校验（修复 #29311）。[链接](https://github.com/google-gemini/gemini-cli/pull/29336)
5. **#29333**（P2，enterprise）校验按约定发现的策略目录权限 — 与 #29336 互补的安全加固。[链接](https://github.com/google-gemini/gemini-cli/pull/29333)
6. **#29327**（P2）SDK `AgentShell.exec` 真正生效 `env` 与 `timeoutSeconds` — 此前超时形同虚设。[链接](https://github.com/google-gemini/gemini-cli/pull/29327)
7. **#29330**（P2）修复 React 状态更新中的副作用违规，保留 logger 响应前输入的内容。[链接](https://github.com/google-gemini/gemini-cli/pull/29330)
8. **#29242**（P2）`isAuthenticationError` 不再把 "401" 当子串匹配（如端口号 4012），避免误触发重新登录。[链接](https://github.com/google-gemini/gemini-cli/pull/29242)
9. **#29229**（P2）设置编辑器拒绝非有限数字，防止 `1e309` 被存成 null 损坏配置。[链接](https://github.com/google-gemini/gemini-cli/pull/29229)
10. **#29117**（已合并）MCP OAuth 流程实施 RFC 9207 issuer 校验，防止 token 错误路由。[链接](https://github.com/google-gemini/gemini-cli/pull/29117)

另有 #29326 修复 GitHub workflow 中缺失循环的小型修复，社区贡献活跃。

## 5. 功能需求趋势

- **Agent/子代理能力增强**：AST 感知代码探索（#22745/#22746）、token 节约的“外科手术式”读取（#19561）、本地子代理 Sprint（#20195）、bash 原生能力 + 沙箱化（#19873）。
- **记忆系统（Auto Memory）治理**：脱敏、低信号过滤、无效补丁隔离（#26516/#26522/#26523/#26525），一整套质量改进正在推进。
- **企业安全与策略**：策略目录权限校验、OAuth issuer 验证、日志凭据防护成为 PR 主线。
- **可观测性与可调试性**：子代理轨迹分享（#22598）、bug report 包含子代理上下文（#21763）。
- **浏览器自动化**：Wayland 支持、会话锁恢复、配置覆盖生效。

## 6. 开发者关注点

- **挂起/卡死问题最痛**：#21409（agent 挂起）、#25166（shell 卡在等待输入）、#22465（交互式提示卡死）等高优 bug 长期开放，多处于 need-retesting 状态。
- **子代理可靠性报告失真**：MAX_TURNS 被报为成功（#22323）使用户难以信任自动化结果。
- **工具使用不足**：模型不主动调用 skills/子代理（#21968），且工具数量超限时直接 400（#24246）。
- **Token 成本压力**：/compress 不持久化、大文件读取导致上下文膨胀（约 36.6k tokens/轮基线），社区对精简读取方案呼声强烈。
- **配置与边界行为**：symlink 代理不被识别（#20079）、settings.json 覆盖被忽略（#22267）等“小而烦”的问题影响日常体验。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-09-15** | 数据来源：[github/copilot-cli](https://github.com/github/copilot-cli)

---

## 一、今日速览

过去24小时内 Copilot CLI 连发三个补丁版本（1.0.84-6 → 1.0.84-8），重点改进 Agent Factory 运行控制和 MCP 兼容性修复。社区共更新 24 条 Issues，其中新 Issue 集中爆发于**沙箱/企业策略管理**（6条）和**子代理（subagent）稳定性**（2条）两大方向。MCP 协议升级（2026-07-28 版本）带来的兼容性问题成为跨版本反复出现的主题。

---

## 二、版本发布

### v1.0.84-8
- **新增**：transcriptView 设为 "concise"，将工具活动折叠为可展开的工作摘要
- **改进**：可在 `/factories` 对话框中暂停/恢复 Agent Factory 运行
- **修复**：登录、切换账户或登出后模型列表正确刷新

### v1.0.84-7
- **修复**：Claude adaptive-only 模型的 thinking 参数处理——关闭 thinking 时降低 reasoning effort 而非直接失败；thinking 禁用时 reasoning effort 上限为 high
- 修复 `/clear` 关闭会话时执行 sessionEnd hooks

### v1.0.84-6
- **新增**：`/config` 命令打开 CLI 侧边栏配置界面
- **新增**：`/sandbox` 支持 Network host 允许/拒绝规则，且不覆盖已配置的上游代理
- **改进**：托管 Edit/Write 规则现可应用于原生 shell 重定向和 sed 原地编辑操作

---

## 三、社区热点 Issues（Top 10）

1. **[#4849](https://github.com/github/copilot-cli/issues/4849) 子代理工作流延迟过高**（新）
   反映 Agent 启动、任务交接、review/fix 循环单轮耗时数分钟，直接影响核心使用体验，属高优先级性能问题。

2. **[#4850](https://github.com/github/copilot-cli/issues/4850) 后台子代理无限期“运行中”**（新）
   工具活动停止 15 分钟后状态仍为 running，父会话无法回收结果，与 #4849 同日由同一作者提交，指向子代理生命周期管理缺陷。

3. **[#4725](https://github.com/github/copilot-cli/issues/4725) Linux 下频繁 JS 堆内存溢出**（持续发酵）
   CLI 每隔几分钟因 Mark-Compact 分配失败崩溃，是影响可用性的关键稳定性 Bug。

4. **[#4525](https://github.com/github/copilot-cli/issues/4525) MCP 初始化协议冲突（已关闭）**
   1.0.81-1 在成功 `server/discover` 后仍发送 legacy `initialize` 导致 -32022 错误，已修复关闭，验证了 MCP 兼容性修复正在落地。

5. **[#4846](https://github.com/github/copilot-cli/issues/4846) 沙箱策略被 "allow dev tool access" 绕过**（新）
   启用开发工具访问后，`python` 等命令可绕过文件系统沙箱策略——属安全敏感问题，值得尽快关注。

6. **[#4844](https://github.com/github/copilot-cli/issues/4844) `--yolo` 启动参数被 fail-closed 窗口吞掉**（新）
   预认证窗口内应用的 bypass 权限模式在策略解析后未重新应用，影响权限模式的一致性。

7. **[#4847](https://github.com/github/copilot-cli/issues/4847) 托管设置自动刷新破坏 IDE MCP 重载**（新）
   长会话连接 VS Code 时，managed-settings 刷新失败并禁用 `/allow-all`，跨产品集成链路问题。

8. **[#4836](https://github.com/github/copilot-cli/issues/4836) Grok 4.5 超过 350 工具数限制时返回裸 400**（新）
   CLI 未在客户端侧预检工具数量，错误信息不透明；BYOK 第三方模型适配仍是薄弱环节（另见 [#4840](https://github.com/github/copilot-cli/issues/4840) Deepseek 失效、[#4835](https://github.com/github/copilot-cli/issues/4835) Gemini Flash enum 兼容问题）。

9. **[#4505](https://github.com/github/copilot-cli/issues/4505) 恢复会话后连接 item ID 过期致 400 错误**（持续）
   中断响应后 resume/fork 均无法恢复会话，影响会话持久化可靠性，3 👍。

10. **[#4549](https://github.com/github/copilot-cli/issues/4549) Windows 下每条 shell 命令弹出 PowerShell 窗口**（持续）
    控制台窗口闪烁并抢焦点，严重影响 Windows 用户体验。

---

## 四、重要 PR 进展

过去 24 小时内无公开 PR 更新（本仓库开发以内部流水线为主，变更通过 Release 交付）。

---

## 五、功能需求趋势

| 方向 | 相关 Issues | 趋势解读 |
|---|---|---|
| **企业策略与沙箱治理** | #4783, #4837, #4844, #4846, #4847 | 企业落地诉求强烈：希望 yolo 模式、插件启用、沙箱规则有独立、可预测的策略作用域 |
| **子代理性能与生命周期** | #4849, #4850 | Subagent 工作流成为重度用户核心场景，延迟和状态管理是当前最大痛点 |
| **MCP 2026-07-28 协议支持** | #4525, #4834, #4842 | 社区要求完整支持 MRTR（input_required）与新版协议握手 |
| **BYOK 与多模型适配** | #4835, #4836, #4840 | Grok、Gemini、Deepseek 等第三方模型暴露工具 schema 兼容和限额预检短板 |
| **会话可靠性** | #4505, #4845 | 会话恢复、"In use" 状态残留等持久化问题反复出现 |

---

## 六、开发者关注点

- **性能瓶颈**：子代理启动与 review 循环延迟（分钟级）、内存溢出崩溃，是技术团队反馈最集中的稳定性问题。
- **企业可管理性**：托管策略与本地行为之间的竞态（fail-closed 窗口、策略刷新副作用）导致部署行为不可预测。
- **安全边界模糊**：沙箱策略在 dev tool access 场景下被绕过，权限模型需要更清晰的分层。
- **错误可观测性差**：多个 Issue 指向裸 HTTP 400 / 无提示静默失败，社区呼吁更透明的预检与错误上报。
- **跨平台体验**：Windows 控制台闪烁、Warp 主题不适配（[#4843](https://github.com/github/copilot-cli/issues/4843)）等细节问题影响日常使用。

---

*本报告基于过去 24 小时 GitHub 公开数据自动汇总，如有遗漏请以官方仓库为准。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-09-15 | 数据来源：MoonshotAI/kimi-cli**

---

## 一、今日速览

今日无新版本发布，也无活跃 PR 更新。社区动态集中在 Issues 层面：两条历史 Issue（#1433、#1435）于今日关闭，反映剪贴板 Cmd+V 兼容性问题已有处理进展；同时新增两条 CJK 用户相关的反馈（#2643 IME 输入冲突 bug、#2642 可视化批注需求），显示中文用户群体的产品诉求日益凸显。

---

## 二、版本发布

过去 24 小时无新 Release。

---

## 三、社区热点 Issues

今日活跃 Issue 共 4 条，均值得关注：

**1. [#1433] [bug] 剪贴板图片粘贴仅支持 Ctrl+V，忽略 Cmd+V（已关闭）**
- 作者：@ringotypowriter | 👍 1 | 评论 2
- macOS（Darwin arm64）用户在 CLI 内粘贴图片时，快捷键判断仅覆盖 Ctrl+V，未适配 Mac 的 Cmd+V，影响 v1.22.0 上的图片输入体验。
- 该 Issue 于今日关闭，或已修复/纳入处理，Mac 用户可关注后续 Release。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1433

**2. [#1435] [enhancement] 为 Kimi For Coding API 增加 PicoClaw 支持（已关闭）**
- 作者：@clawaizhang
- 用户希望将 Kimi For Coding 订阅用于开源 AI Agent 项目 PicoClaw，但 API 存在访问限制。该请求今日被关闭，官方态度（是否开放第三方 Agent 接入）值得持续关注。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1435

**3. [#2643] [kimi web] IME 组词状态下按 Enter 被误判为发送消息（OPEN）**
- 作者：@wangjin1982
- 中/日/韩输入法用户在 `kimi web` 输入框组词确认时，回车被误认为「发送」，导致未完成内容被发出。这是典型的 IME composition 事件处理遗漏，对 CJK 用户属于高频体验硬伤，建议优先修复。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2643

**4. [#2642] [功能需求] Kimi Work 支持对 Agent 回复的可视化批注与审阅反馈（OPEN）**
- 作者：@Zhywleo
- 希望对 Agent 的长回复（计划、报告、方案）支持逐段可视化批注，并以结构化形式回传给 Agent 用于修订，替代纯文字描述修改意见。这是一个质量较高的产品级需求，指向「人机协作审阅」工作流方向。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2642

---

## 四、重要 PR 进展

过去 24 小时无活跃 PR 更新。

---

## 五、功能需求趋势

从近期 Issues 可提炼出以下方向：

1. **CJK/国际化体验**：#2643 的 IME 组词冲突表明东亚用户输入体验仍需系统性排查（快捷键、输入框事件处理）。
2. **跨平台一致性**：#1433 暴露 macOS 适配盲区（Cmd 键位），建议团队建立平台差异化快捷键测试清单。
3. **API 开放性与生态接入**：#1435 反映社区希望 Kimi For Coding 订阅可用于更多第三方 Agent 项目，订阅授权边界的透明化是潜在诉求。
4. **协作与审阅工作流**：#2642 代表了对 Agent 输出进行可视化批注、结构化反馈的高级协作需求，是产品从「对话」走向「协作工具」的信号。

---

## 六、开发者关注点

- **Mac 用户痛点**：图片粘贴等快捷键操作在 Darwin 平台的兼容性需重点回归测试。
- **输入法兼容**：`kimi web` 前端需正确处理 `compositionstart/compositionend` 事件，避免 CJK 用户内容误发送。
- **API 使用范围限制**：订阅制（Kimi Coding Plan）与第三方工具集成的边界问题引发用户关注，官方政策沟通有待加强。
- **审阅流程效率**：重度用户已不满足于纯文本反馈循环，对结构化、可视化的人机迭代工作流有明确期待。

---
*本日报基于 GitHub 公开数据自动整理，链接均指向 MoonshotAI/kimi-cli 仓库。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-15

## 1. 今日速览

OpenCode 发布 v1.18.31，修复了 ACP 会话恢复/Fork 时模型、effort、mode 等状态丢失的核心 Bug。社区最大争议聚焦于**旧布局被强制移除且新布局不支持多工作树**（#48835），叠加 macOS 上所有 Prompt 均报错的严重回归（#48811），引发大量用户不满。PR 方面，Code Mode 解释器引入首个二进制类型支持（Uint8Array/TextEncoder），多工作树 API 项目化改造完成首个迭代。

---

## 2. 版本发布

### v1.18.31

**Core Bugfixes**
- 修复加载、恢复或 Fork 会话时，ACP 会话的 model、effort、mode 及 reasoning chunk 边界丢失的问题（@JacobNWolf）

**TUI Bugfixes**
- 启动时显示远程配置认证错误，并以失败状态退出（而非静默失败）

🔗 [Releases](https://github.com/anomalyco/opencode/releases)

---

## 3. 社区热点 Issues

### 🔥 争议与严重回归

**1. #48835 — 旧布局被强制移除，新布局不支持多工作树**（👍 9 | 💬 7）
9 月 14 日午夜 Desktop 强制切换到新布局，设置中显示“旧布局不再可用”，但新布局完全不支持多 worktree。与 #37012 的诉求叠加，是当前最激烈的社区矛盾。
🔗 [Issue #48835](https://github.com/anomalyco/opencode/issues/48835)

**2. #37012 — [FEATURE] 保留旧布局选项**（👍 63 | 💬 45）
两个多月长盛不衰的热帖。用户认为旧布局从主窗口即可触达所有功能、支持 workspace，新布局需要层层导航。63 个 👍 说明这是社区最强烈的声音。
🔗 [Issue #37012](https://github.com/anomalyco/opencode/issues/37012)

**3. #48811 — macOS 每次输入均报 `undefined is not an object`**（👍 29 | 💬 7）
启动和会话创建正常，但所有 Prompt/工具调用在 `SystemPrompt.environment` 处崩溃。影响面广、复现一致的严重回归。
🔗 [Issue #48811](https://github.com/anomalyco/opencode/issues/48811)

### 🐛 高影响 Bug

**4. #26602 — Desktop 对慢速本地模型 5 分钟 Headers Timeout**（💬 14）
本地 OpenAI 兼容 provider 请求在恰好 5 分钟后被中止，`"timeout": false` 配置不生效。本地模型用户的核心痛点。
🔗 [Issue #26602](https://github.com/anomalyco/opencode/issues/26602)

**5. #30611 — 瞬时网络错误导致会话直接失败而非重试**（💬 9）
重试逻辑只认 `ECONNRESET`，其他瞬时传输错误都被判定为硬错误，一轮短暂断网即杀死整个 assistant turn。
🔗 [Issue #30611](https://github.com/anomalyco/opencode/issues/30611)

**6. #36893 — [V2] `session.time_updated` 在活跃 turn 期间不更新**（💬 7）
时间戳只在少数投影事件时更新，导致正在流式输出的会话在列表中显示为“旧会话”，排序错乱。已有对应修复 PR（#49105）。
🔗 [Issue #36893](https://github.com/anomalyco/opencode/issues/36893)

**7. #48224 — [2.0] Code Mode 在 Web 会话中暴露 Desktop 专属浏览器工具**（💬 3）
`tools.browser.*` 在 Web 会话中被广播，调用后给出 Web 端无法完成的配置指引，属于能力发现与实际权限不一致的问题。
🔗 [Issue #48224](https://github.com/anomalyco/opencode/issues/48224)

**8. #49095 — CLI 多会话负载下单进程瓶颈**（💬 2，今日新增）
5+ 并发会话时 Node.js 单核饱和，新建/切换会话严重卡顿。直指架构层面的并发瓶颈，值得持续跟踪。
🔗 [Issue #49095](https://github.com/anomalyco/opencode/issues/49095)

**9. #23114 — 会话标题从注入的 memory/system 上下文生成**（💬 6）
Memory MCP 注入的历史摘要污染标题生成输入，标题与实际用户消息脱节。
🔗 [Issue #23114](https://github.com/anomalyco/opencode/issues/23114)

**10. #38450 — Edit 工具未读取文件最新内容**（💬 2）
用户与 Agent 并发编辑时，Edit 基于过期的文件快照执行，可能覆盖用户改动——涉及编辑安全性的经典问题。
🔗 [Issue #38450](https://github.com/anomalyco/opencode/issues/38450)

---

## 4. 重要 PR 进展

**1. #49105 — fix(core): 在 step 生命周期事件时更新 `time_updated`**
直接修复 #36893，会话排序失真问题的解决方案已就位。
🔗 [PR #49105](https://github.com/anomalyco/opencode/pull/49105)

**2. #49076 — feat(codemode): 引入 Uint8Array、TextEncoder、TextDecoder**
Code Mode 解释器的**首个二进制类型**。字节驻留程序内、以拷贝方式跨入扩展，工具边界拒绝裸二进制并提示先编码为文本。
🔗 [PR #49076](https://github.com/anomalyco/opencode/pull/49076)

**3. #49104 / #49100 — refactor(codemode): 解释器上下文统一与命名清理**
内置函数从三个重叠视图收敛为单一 `ctx` 对象；移除 `Program` 前缀的机械重命名。纯重构，无行为变化，为后续迭代铺路。
🔗 [PR #49104](https://github.com/anomalyco/opencode/pull/49104) | [PR #49100](https://github.com/anomalyco/opencode/pull/49100)

**4. #48867 — feat(core): worktree API 项目化改造（已合并）**
四项 worktree 操作全部要求 `projectID`，List 操作不再加载配置/激活插件。这是对 #48835 多工作树诉求的基础设施准备。
🔗 [PR #48867](https://github.com/anomalyco/opencode/pull/48867)

**5. #49106 — fix(client): 快照读取期间保留 inbox 事件**
修复远程客户端重连后，延迟的 inbox HTTP 响应覆盖新事件、导致已回答消息跳回底部且标记为 pending 的问题。
🔗 [PR #49106](https://github.com/anomalyco/opencode/pull/49106)

**6. #49097 — fix(plugin): 向松散插件文件提供打包的 SDK**
修复 `.opencode/plugins/foo.ts` 中的 `@opencode/plugin` 导入在 Bun 可执行文件中解析失败的问题。插件生态的可用性修复。
🔗 [PR #49097](https://github.com/anomalyco/opencode/pull/49097)

**7. #49099 — fix(ai): 按结构化错误码分类内容策略错误**
识别 Azure（`content_filter`/`ResponsibleAIPolicyViolation`）和 OpenRouter（`content_policy_violation`/`refusal`）的内容策略错误，改善错误处理语义。
🔗 [PR #49099](https://github.com/anomalyco/opencode/pull/49099)

**8. #48978 — fix(tui): 加固模型解析与变体选择**
`util/model.ts` 的 `parse` 对非字符串/undefined/空输入加防护，防止启动时 `U.split is not a function` 崩溃。
🔗 [PR #48978](https://github.com/anomalyco/opencode/pull/48978)

**9. #49089 — fix(tui): 退出时干净地重置终端模式**
修复 TUI 退出后终端状态损坏、epilogue 覆盖已恢复 shell 内容的问题。
🔗 [PR #49089](https://github.com/anomalyco/opencode/pull/49089)

**10. #49087 — feat(app): 清理 URL 凭据并加固浏览器附件上下文**
通过 `history.replaceState()` 清洗文档 URL，防止凭据泄漏；安全相关修复。
🔗 [PR #49087](https://github.com/anomalyco/opencode/pull/49087)

**其他值得关注**：#49103 为 Mac 桌面端补上标准 ⌘⇧[/] 标签切换快捷键；#43460 修复插件捆绑不同 effect 版本导致工具输入解码全数失败的问题；#48423 将双 WebSocket 开关合并为单一 transport 偏好。

---

## 5. 功能需求趋势

| 方向 | 代表 Issue | 趋势解读 |
|---|---|---|
| **布局/UX 回退诉求** | #37012、#48835 | 最强音。社区要求保留旧布局或至少补齐新布局的 worktree/workspace 能力 |
| **本地/慢速模型兼容** | #22132、#26602、#37412 | Ollama 挂起、5 分钟硬超时、指数退避重试——本地推理用户的超时与重试体系亟待完善 |
| **会话可靠性** | #30611、#36893、#49092 | 网络容错、时间戳准确性、输出中断，均指向会话生命周期健壮性 |
| **多会话监控** | #28175、#49095 | 侧边栏实时会话状态面板 + 后台完成通知；以及多会话并发下的架构性能 |
| **企业/合规错误语义** | #49099（PR）、多条 `needs:compliance` | 内容策略错误的结构化分类，服务企业场景 |
| **Provider 生态** | #36318（GPT-5.6 缓存默认值）、#32423（按 provider 限流）、#28731（xAI） | 对新模型特性和精细化 provider 管理的持续需求 |

---

## 6. 开发者关注点

1. **强制迁移引发的信任危机**：旧布局移除 + 新布局功能缺失 + macOS 全量报错（#48811）三重叠加，“强制升级不可回退”正在消耗社区信任，建议密切关注官方对 #37012 的最终表态。
2. **本地模型用户体验断层**：超时硬编码、重试策略单薄（只认 `ECONNRESET`）、headers timeout 不可配置，本地/自托管用户是当前抱怨密度最高的群体。
3. **并发与性能瓶颈浮现**：CLI 单进程单核饱和（#49095）、`.opencode/node_modules` 扫描挂起（#30337）表明性能问题开始从边缘场景走向主路径。
4. **编辑安全**：Edit 工具基于过期快照操作（#38450），并发编辑下的数据丢失风险是开发者信任 Agent 的底线问题。
5. **插件生态健壮性**：松散插件 SDK 解析失败（#49097）、effect 版本冲突（#43460）说明插件加载机制仍在补课，对生态扩展者是实际障碍。

---
*数据来源：github.com/anomalyco/opencode | 统计窗口：过去 24 小时*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-09-15

## 📌 今日速览

Qwen Code 发布 **v0.23.4** 稳定版及对应 nightly 版本，同时推进 cua-driver-rs 至 v0.20.8。社区反馈集中在 **扩展系统稳定性**（Windows EPERM、卸载失败）、**ACP/daemon 会话管理缺陷**以及 **hooks 体系重构**（相关 PR 密集合入/关闭）。P1 级 Bug 数量偏高，是本周期值得关注的信号。

---

## 🚀 版本发布

- **v0.23.4**（[Release](https://github.com/QwenLM/qwen-code/releases)）
  - ⚠️ **Breaking Change**：移除 channels 中可配置的 message-prefix 过滤，符合条件的消息不再需要前缀，直接走 sender/group/mention/pairing 策略（[#11571](https://github.com/QwenLM/qwen-code/issues/11571)）
  - 测试：记录 Windows inode gates 遮蔽的内容，并解除一处 skip（#11853）；CUA 相关修复
- **v0.23.4-nightly.20260914.f024b37689**：随主版本同步发布
- **cua-driver-rs v0.20.8 / v0.20.7**：预编译二进制，macOS 通用二进制已签名+公证，Linux 支持 x86_64/arm64（glibc 2.31+），Windows 提供 UIAccess worker + 原生 SDK payload

---

## 🔥 社区热点 Issues

1. **[#11834](https://github.com/QwenLM/qwen-code/issues/11834)** — P1：简单输入“你好”即触发 `API Error: 400 function parameters is empty (2013)`，影响基础可用性，6 条评论为今日最热
2. **[#11905](https://github.com/QwenLM/qwen-code/issues/11905)** — 同为 2013 错误：MiniMax 拒绝无参数内置工具，与 #11834 可能同源，值得合并排查
3. **[#11795](https://github.com/QwenLM/qwen-code/issues/11795)** — P1 架构级问题：权限队列按 ACP 连接为 key，一个空闲会话的未答 prompt 会**静默阻塞同 daemon 上所有其他会话**，修复 PR #11802 已开
4. **[#11908](https://github.com/QwenLM/qwen-code/issues/11908)** — P1：超大的 `available_commands_update` 通知触发 MAX_JSON_NODES，通道被拆除且后续请求全部 404，属 fail-closed 过激行为
5. **[#11849](https://github.com/QwenLM/qwen-code/issues/11849)** — P1：0.23.3 上间歇性静默崩溃，疑似与后台 shell/subagent 完成相关，与 #11500 关联
6. **[#11887](https://github.com/QwenLM/qwen-code/issues/11887)** — P2：`--acp` 模式忽略审批模式，限制性模式下工具**零权限确认直接执行**，安全影响显著
7. **[#11872](https://github.com/QwenLM/qwen-code/issues/11872)** — P1：Web Terminal 报 "PTY not available"——`@lydell/node-pty` 声明未打包，且 macOS 签名阻断本地 prebuilds
8. **[#11895](https://github.com/QwenLM/qwen-code/issues/11895)** — P1（wenshao 报告）：`/review` 的 dimension agents 读取主 checkout 而非 PR worktree，存在审错代码的风险
9. **[#11883](https://github.com/QwenLM/qwen-code/issues/11883)** — P1：Windows 上扩展更新/卸载报裸 `EPERM`，同批还有 #11884（无进度反馈）、#11885（目录删除后无法卸载重装），扩展生命周期管理问题集中爆发
10. **[#11894](https://github.com/QwenLM/qwen-code/issues/11894)** — P2：DeepSeek `deepseek-flash` 名字匹配失败导致 token 限额解析为 128k/32k（实际 V4 为 1M/384k），长会话压缩失败

---

## 🔧 重要 PR 进展

1. **[#11805](https://github.com/QwenLM/qwen-code/pull/11805)** — 扩展可发布动态 workflow 脚本，形成第三层 saved-workflow 体系
2. **[#11840](https://github.com/QwenLM/qwen-code/pull/11840)** — **跨会话消息默认开启**，同用户会话间可互相发现和通信（含评审规则）
3. **[#11906](https://github.com/QwenLM/qwen-code/pull/11906)**（已关闭）— hooks 通过 MessageBus 上报进度事件，配合 #11904（`/hooks` 打开时重载注册表）和 #11903（OpenTUI 完整 hooks 浏览器）形成本周 hooks 改造主线
4. **[#11900](https://github.com/QwenLM/qwen-code/pull/11900)** — 删除第一代 Stop-hook Goal 实现，净删 1,139 行产码 + 2,260 行测试，为二代方案让路
5. **[#11614](https://github.com/QwenLM/qwen-code/pull/11614)** — Linux bwrap 内核级沙箱后端：无需容器运行时/root/镜像，opt-in 启用
6. **[#11821](https://github.com/QwenLM/qwen-code/pull/11821)** — shell 拆分器支持 `#` 注释语义，配套 issue #11882 提出两个 splitter 需收敛
7. **[#11889](https://github.com/QwenLM/qwen-code/pull/11889)** — Windows 目录被锁时扩展产物改为 copy-aside 事务，直接对应 #11883
8. **[#11684](https://github.com/QwenLM/qwen-code/pull/11684)** — Responses 清理时保持 reasoning 与 function_call 组相邻，防止孤儿调用被误删
9. **[#11822](https://github.com/QwenLM/qwen-code/pull/11822)** — channels 共享输出模式（per_turn/per_response/per_task），DingTalk 首个集成
10. **[#11855](https://github.com/QwenLM/qwen-code/pull/11855)** — 基础设施：hk1/hk2 runner 每日两次在 review 与 CI 间切换，应对 ECS 舰队更新失败（#11633）

---

## 📈 功能需求趋势

- **扩展系统**：最活跃方向。工作流发布、文件重载、symlink 安全策略（#11896）、生命周期管理，一组连贯的体系化建设
- **Hooks/Goal 事件化**：`roadmap/hooks-events` 标签下已聚集 4+ issue，registry 重载、matcher 修复、进度事件均在推进
- **多模型支持**：MiniMax 2013 错误、DeepSeek token 限额，第三方模型接入的边缘 case 持续暴露
- **Channels/多会话协作**：跨会话消息默认开启 + DingTalk 输出模式，多 agent 协作通信是明确的产品方向
- **Web Shell / Desktop**：PTY 打包、会话总览、脚注预览、阅读位置跟踪，Web 端体验投入加大

## ⚠️ 开发者关注点

1. **扩展生命周期是最大痛点**：Windows EPERM、目录锁、卸载死锁、更新无反馈（#11883/84/85/89），建议 Windows 用户暂缓依赖扩展更新流程
2. **API 2013 错误波及多端点**（MiniMax、通用场景），升级 0.23.4 前建议确认所用端点
3. **daemon/ACP 会话隔离薄弱**：权限队列串扰、JSON 上限炸通道，重度多会话用户需关注 #11795/#11908 修复进展
4. **Linux 稳定性**：静默崩溃（#11849）与 Ink React #185 崩溃（#11873）尚在 need-retesting，长任务场景建议做好 checkpoint

---

*数据来源：QwenLM/qwen-code GitHub · 统计窗口：2026-09-14 至 2026-09-15*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (CodeWhale) 社区动态日报 — 2026-09-15

## 📌 今日速览

今日社区焦点集中在 **v0.9.14 里程碑的持续推进**：#6161（console-freeze / approval-death / 压缩与 session 保留修复）已合并，紧接着 #6175 作为第二个 stacked slice 已开（lazy MCP、session recovery 等 9 个 issue 切片）。同时，**GPUI 桌面端（app-server）迎来一波集中交付**，APPS-28/30/47/48 四条路由 Issue 当天创建当天关闭，显示桌面集成进入快车道。无新版本发布，`main` 为活跃线，0.9.13 仍在最终验证中。

---

## 🚀 版本发布

过去 24 小时无新 Release。据 [#6094](https://github.com/Hmbown/CodeWhale/issues/6094)：`0.9.13` 处于最终验证阶段，**未打 tag 前 CI 必须在确切 head 上全绿**；v0.9.14 里程碑已排队，重点是 catalog-owned 模型能力等。

---

## 🔥 社区热点 Issues

1. **[#5316](https://github.com/Hmbown/CodeWhale/issues/5316) — EPIC-005: CodeWhale TUI Crate 拆解（伞形）**（27 评论）
  最活跃的架构级 Issue，执行权已移交 Linear 的 Core execution plan（C03–C10），拆 crate 工作是 0.9.x 重构主线。

2. **[#5587](https://github.com/Hmbown/CodeWhale/issues/5587) — Dead-code 清扫 Phase 2-4**（7 评论）
  Phase 1 已落地（e5ca0aa86 移除 8 个确认死代码项）。全量审计 379 处 `allow(dead_code)`：18 处确认死代码待删、约 242 处过期 allow。代码卫生工作的基准文档。

3. **[#6011](https://github.com/Hmbown/CodeWhale/issues/6011) — Token 用量与工具调用诊断**（7 评论）
  按组件/模型的 token 计账、缓存命中率、工具错误模式统计，归属 Core C11。可观测性方向的重点需求。

4. **[#6018](https://github.com/Hmbown/CodeWhale/issues/6018) — [已关闭] Gemini 全新安装故障**
  影响新用户上手的关键 bug，已随 C22 修复关闭。

5. **[#6094](https://github.com/Hmbown/CodeWhale/issues/6094) — v0.9.14 起点指南**（5 评论）
  官方“从哪里看起”入口，明确版本状态、贡献方式与报告规范，新贡献者必读。

6. **[#6015](https://github.com/Hmbown/CodeWhale/issues/6015) — 自适应 anti-stall + 更宽的只读 shell 语法**（5 评论）
  Fleet 稳定性核心：此前“仅 postrelease 限制”已被推翻，纳入 C05/C06，且作为默认行为而非用户配置。

7. **[#6009](https://github.com/Hmbown/CodeWhale/issues/6009) — [已关闭] `/models` 不支持分页**
  未处理 `has_more`/`after` 游标导致大提供商模型列表被截断，已修复。

8. **[#6150](https://github.com/Hmbown/CodeWhale/issues/6150) — `Op::SendMessage` 上帝载荷 → `TurnSpec` 重构**
  ~20 个字段的枚举 arm 提取为 struct，并证明 UI 输入路径从不 await `send()`。0.9.14 重构积压中的代表性项。

9. **[#6035](https://github.com/Hmbown/CodeWhale/issues/6035) — 模型 pin 不传播**
  模型 id 在至少 6 处独立 pin，厂商下架旧 id（如 DeepSeek V4.1 Flash 更名）后 fleet/agent profile 残留死 id，缺乏统一 owner 与迁移机制。真实用户已踩坑。

10. **[#5529](https://github.com/Hmbown/CodeWhale/issues/5529) — 子代理无法可靠执行**
  wall-time 预算中途死亡丢失未提交工作、provider 路由失败阻塞 dispatch、shell 工具需 workaround——直击 Fleet 核心价值主张的可用性问题。

---

## 🔀 重要 PR 进展

1. **[#6161](https://github.com/Hmbown/CodeWhale/pull/6161) [已合并]** — v0.9.14：修复两个 console-freeze/silent-death 缺陷（turn 进行中执行 `/mcp`、无人值守审批因 idle-timeout 被取消）、压缩保留中的孤儿 `tool_result` 洞、销毁 session 保留。
2. **[#6175](https://github.com/Hmbown/CodeWhale/pull/6175) [开放]** — v0.9.14 slice run 2：lazy MCP、session recovery + picker UX、launch remedy 行等 9 个 issue 切片，一 issue 一 commit，逐项验证。
3. **[#5867](https://github.com/Hmbown/CodeWhale/pull/5867) [已关闭]** — 新增 `[reasoning_only]` 配置节，将硬编码的推理模型空响应重试次数（原固定 2 次）改为用户可配置。
4. **[#6171](https://github.com/Hmbown/CodeWhale/pull/6171) [开放]** — 新增 AICraft OpenAI 兼容提供商模板，社区贡献，沿用 SenseNova/Groq 等 descriptor 模式。
5. **[#6170](https://github.com/Hmbown/CodeWhale/pull/6170) [开放]** — 修复 Weixin bridge：文档指向不存在的路径、缺启动命令，且首条微信消息即触发故障。

**配套 Issue（GPUI/app-server 路由，今日当天关闭）：**
- [#6183](https://github.com/Hmbown/CodeWhale/issues/6183) — 类型化命令目录路由（APPS-28），GPUI 命令面板无需复制命令表。
- [#6182](https://github.com/Hmbown/CodeWhale/issues/6182) — 凭据管理路由（APPS-48），Engine-owned inspect/set/clear。
- [#6181](https://github.com/Hmbown/CodeWhale/issues/6181) — 后台/挂起调度与 3 类 engine notice 进入快照（APPS-47 收尾）。
- [#6177](https://github.com/Hmbown/CodeWhale/issues/6177) — 队列语义路由（APPS-30）：pending 输入 / 排队 follow-up / parked work 的 list/pause/resume/cancel。

（注：过去 24 小时实际更新的 PR 共 5 条，已全部覆盖。）

---

## 📈 功能需求趋势

- **GPUI/桌面集成（最热）**：APPS 系列路由密集落地，runtime API 正成为 TUI 与桌面端共享的单一运行时契约（#6152 的 broadcast/watch 事件投影也是为此铺路）。
- **Fleet / 多代理可靠性**：子代理执行、anti-stall、fleet 模型 shortlist 与角色分配（#5915、#6015、#5529、#5479）。
- **可观测性与诊断**：token 计账、工具调用错误模式、goal gates 独立验证（#6011、#6013）。
- **架构重构与代码卫生**：crate 拆解（#5316）、TurnSpec 提取（#6150）、依赖去重（#6151）、dead-code 清扫（#5587）。
- **插件化与生态扩展**：可插拔 agent memory backend（#6050，参考 mem0/causal-memory）、新 provider 模板（#6171）、computer-use 插件（#5856）。
- **模型目录管理**：分页、模型 pin 传播与厂商 id 退役迁移（#6009、#6035）。

---

## ⚠️ 开发者关注点

1. **静默失败是最大痛点**：workflow 失败无任何 TUI 提示（#5528）、取消的 automation run 无 transcript 回执（#6162）、无人值守审批静默死亡（#6161 已修）——“看起来在跑其实没跑”类问题反复出现。
2. **配置漂移与状态残留**：模型 id 六处独立 pin、MCP OAuth 登出后仍复用旧 workspace 授权（#6040）。
3. **资源边界**：engine 内两条 unbounded channel 可被病态工具无限撑爆内存（#6147 已修，另约 33 处待排查）；工具审批提示无超时（#6101 已修）。
4. **CI/构建确定性**：`CARGO_BUILD_WARNINGS=deny` 在 JSON 输出格式下退出码不一致（#6132）；nightly security sweep 因 PAT 未配置无法列出 CodeQL 告警（#6058）。
5. **新用户安装体验**：Gemini from-scratch 安装故障（#6018）、Weixin bridge 文档失修（#6170）——第三方集成/文档质量需关注。

---
*数据来源：github.com/Hmbown/DeepSeek-TUI（Issues/PR 过去 24 小时更新）*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 社区动态日报 — 2026-09-15

## 一、今日速览

今日无新版本发布，但社区活跃度极高（过去 24 小时 61 条 Issue 更新、26 条 PR 更新）。焦点集中在**缓存计费准确性**（Bedrock/Vercel Gateway 1h 缓存写入按 5m 费率错误计费）、**会话/上下文完整性**（压缩后残留 thinking 块、未匹配的 toolCall）以及 **Windows 平台体验**（shell 解析、进程树清理）。维护者 @mitsuhiko 的“会话中途系统消息”PR（#9548）持续引发关注。

---

## 二、版本发布

无。

---

## 三、社区热点 Issues

1. **#8752 — bedrock-converse 各模型族 `usage.input` 语义不一致，导致假缓存未命中告警与输入成本翻倍**（👍5）
   高价值计费 bug：Anthropic 系报净值、OpenAI 系报含缓存的毛值，pi 未归一化直接透传，用户实际多付钱。开放中，社区讨论活跃。
   [链接](https://github.com/earendil-works/pi/issues/8752)

2. **#9457 — bedrock-converse 1h 缓存写入按 5m 费率计费**（👍4）
   `cacheWrite1h` 从未依据 `cacheDetails` 设置，长缓存用户成本被低估。与 #9210（Vercel Gateway 同类问题）构成一组系统性计费缺陷。
   [链接](https://github.com/earendil-works/pi/issues/9457)

3. **#9391 — 压缩后过期签名 thinking 块每轮重放，Anthropic 全部丢弃（prefix_binding_mismatch）**
   长会话手动压缩后每次请求都刷屏报错，影响所有 Anthropic 长会话用户，属上下文管理核心缺陷。
   [链接](https://github.com/earendil-works/pi/issues/9391)

4. **#9306 — 中止/出错的 turn 残留未匹配 toolCall，后续续跑被 provider 拒绝**
   影响 agent 循环鲁棒性：错误中断后无法从同一上下文继续，是可靠性关键问题。
   [链接](https://github.com/earendil-works/pi/issues/9306)

5. **#9440 — `--session-id` 携带新 ID 时仍全量扫描 transcripts，4K+ 会话下启动耗时 ~16s**
   性能痛点明确，已有对应修复 PR #9601 今日更新。
   [链接](https://github.com/earendil-works/pi/issues/9440)

6. **#9444 — openai-completions 丢弃 Gemini 流式 tool_calls 的 thoughtSignature，多轮工具调用第二轮即 400**
   Gemini 经 OpenAI 兼容网关接入时的硬性故障，影响面大。
   [链接](https://github.com/earendil-works/pi/issues/9444)

7. **#9129 — Windows 上 bash 超时 kill 后管道子进程成孤儿**
   `taskkill /T` 对 MSYS2 bash 管道中间进程处理不当，Windows 可靠性高频痛点（与 #9501/#9504 同主题）。
   [链接](https://github.com/earendil-works/pi/issues/9129)

8. **#9298 — Grok 403 被误标为 "OpenAI API error"**（已关闭）
   openai-responses formatter 的错误归属问题，7 条评论，已解决——反映社区对多 provider 错误信息准确性的关注。
   [链接](https://github.com/earendil-works/pi/issues/9298)

9. **#9596 — 同目录两个 `pi -c` 并发运行无锁写入同一会话文件**
   新鲜出炉：会话文件无锁保护，两路对话交叉写入并产生意外分支，静默数据污染。
   [链接](https://github.com/earendil-works/pi/issues/9596)

10. **#9590 — 恢复含多个多 MB 图片的会话后 base64 损坏，后续所有请求 400**
    上下文中的损坏图片无法自愈，导致会话彻底不可用。
    [链接](https://github.com/earendil-works/pi/issues/9590)

其他值得留意：#9210/#9211（Vercel Gateway 1h 缓存与路由配置失效）、#9577（SIGKILL 的 bash 工具仍返回“成功”）、#9381（第三方包 pi-safe-compact 安全举报，已关闭无需行动）。

---

## 四、重要 PR 进展

1. **#9548 — 会话中途系统消息（Mid conversation system messages）** [@mitsuhiko] ⭐
   将系统提示与工具变更纳入 transcript 而非静默重写起点，支持恢复/分支导航时还原状态并保留缓存前缀。架构级改动。
   [链接](https://github.com/earendil-works/pi/pull/9548)

2. **#9601 — 精确 session ID 查找避免全量 transcript 扫描** [@metaist]
   直接修复 #9440 的启动性能问题，附微基准数据。
   [链接](https://github.com/earendil-works/pi/pull/9601)

3. **#8474 — 打包 Node 运行时** [@mitsuhiko]
   大幅减少文件加载数量，解决慢 IO 机器（尤其 Windows Defender 拖累）的启动问题。
   [链接](https://github.com/earendil-works/pi/pull/8474)

4. **#9607 — summarization 流也应用 provider hooks** [@lksgs0]
   修复压缩/分支摘要调用绕过 `before_provider_request` 扩展钩子的问题。
   [链接](https://github.com/earendil-works/pi/pull/9607)

5. **#8732 — 跨模型重放时保留 reasoning_content（DeepSeek 系）**
   修复 DeepSeek 思维模式端点拒绝重放请求的问题，覆盖多家兼容网关。
   [链接](https://github.com/earendil-works/pi/pull/8732)

6. **#9589 — 修复 Responses API 输入项缺少 `type` 字段**
   解决严格端点 400 拒绝的两个相关 bug。
   [链接](https://github.com/earendil-works/pi/pull/9589)

7. **#9501 / #9504 — Windows shell 解析统一化与 Store 别名支持** [@petrroll]
   统一散乱的二进制查找逻辑，修复 Windows Store shell 别名被 `existsSync` 误拒的问题。
   [链接](https://github.com/earendil-works/pi/pull/9501) | [链接](https://github.com/earendil-works/pi/pull/9504)

8. **#9434 — 允许扩展追加会话系统提示** [@wutongyuonce]
   `session_start` 处理器可返回 append-only 系统提示贡献，扩展能力重要补强。
   [链接](https://github.com/earendil-works/pi/pull/9434)

9. **#9594 — 新增 Gemini-only Antigravity provider**（已关闭）
   恢复订阅制 Gemini 接入的第一方 OAuth provider。
   [链接](https://github.com/earendil-works/pi/pull/9594)

10. **#9605 — 新增 GMI Cloud provider**（已关闭）
    OpenAI 兼容聚合端点，复用现有 openai-completions 实现。
    [链接](https://github.com/earendil-works/pi/pull/9605)

其他：#9274（diff 渲染缩进丢失修复）、#9351（远程编辑预览闪烁）、#6534（developer 消息角色，实验性）、#9329（Orca 终端 Kitty 图片支持）。

---

## 五、功能需求趋势

- **计费与用量准确性**：缓存计费（#8752、#9457、#9210）是本期最集中的主题，用户对成本可观测性要求显著提高。
- **上下文/会话完整性**：压缩残留、toolCall 匹配、thinking 块处理、会话文件并发安全（#9391、#9306、#9602、#9596）——长会话可靠性是核心诉求。
- **扩展与 API 能力**：扩展终止 turn、原子中断、系统提示追加、RpcClient 超时控制（#7824、#9578、#9434），headless/宿主集成场景增多。
- **Provider 生态扩展**：GMI Cloud、Antigravity、opencode-go 会话亲和头等，社区持续贡献新后端接入。
- **Windows 与终端体验**：shell 解析、进程清理、滚轮速度、图片渲染兼容性（Orca/kitty）。

---

## 六、开发者关注点

1. **启动性能**：transcript 全量扫描（#9440）与文件 IO 过多（#8474）是两大痛点，前者已有修复在途。
2. **多模型网关兼容性**：OpenAI 兼容层在各上游（Grok/Gemini/DeepSeek）的错误归属、签名保留、reasoning 字段处理上仍有一批边角 bug。
3. **错误与中断语义不清晰**：被信号杀死的命令仍报成功（#9577）、"fail to touch upstream" 不触发重试（#9585）——错误分类体系需要系统性梳理。
4. **扩展开发者体验**：多人通过运行时 patch 绕过限制（#7824），官方扩展点缺口明显；同时贡献流程（先开 Issue 等维护者确认）被频繁提及。
5. **macOS 隐私限制**：Local Network Privacy 阻断 pi 进程访问 LAN（#9453），需要公证或文档说明。

</details>

<details>
<summary><strong>oh-my-pi</strong> — <a href="https://github.com/can1357/oh-my-pi">can1357/oh-my-pi</a></summary>

# 📰 oh-my-pi 社区动态日报 · 2026-09-15

## 一、今日速览

今天社区焦点集中在 **Google Antigravity 虚假 429 配额耗尽问题**（#11689 已关闭，102 条评论），以及 **v18.1.22 发布修复了调试转储泄露 API Key 的安全隐患**。此外，多个涉及浏览器 relay、TUI 稳定性和 MCP 连接管理的 PR 持续推进，社区对多账号凭证管理和欧洲推理网关的需求仍然活跃。

---

## 二、版本发布

### v18.1.22（@oh-my-pi/pi-ai）
- 🔐 **安全修复**：400 请求调试转储现会对 provider 专属认证头（`x-goog-api-key`、`x-amz-security-token` 及任何名称含 key/token/secret 的 header）进行脱敏，不再使用固定白名单，共享转储文件不会再泄露有效 API Key（对应 [#12007](https://github.com/can1357/oh-my-pi/issues/12007)，已关闭）

### v18.1.21（@oh-my-pi/pi-coding-agent）
- 修复 Flatpak Chromium 启动器（含 `com.google.Chrome`、`org.chromium.Chromium`、ungoogled_chromium），`app.path` 现会被识别为浏览器并获得托管 Chromium profile 处理

---

## 三、社区热点 Issues

| # | Issue | 亮点 |
|---|-------|------|
| 1 | [#11689](https://github.com/can1357/oh-my-pi/issues/11689) 🟢CLOSED | **Antigravity 虚假 429 配额耗尽**（102 评论/18 👍）。使用 Google AI Pro 订阅时误报 `RESOURCE_EXACTED`。今日已关闭，是本周社区最大痛点 |
| 2 | [#11699](https://github.com/can1357/oh-my-pi/issues/11699) 🔴OPEN | 定位到 429 根因：system prompt 中的 `<system-conventions>` 标签触发 Antigravity 拒绝，首轮即失败，是 #11689 的关键补充分析 |
| 3 | [#11719](https://github.com/can1357/oh-my-pi/issues/11719) 🔴OPEN | 使用 Gemini 模型时抛出 **Claude 的 429 错误**，错误路由明显异常，请求被错误代理 |
| 4 | [#5289](https://github.com/can1357/oh-my-pi/issues/5289) 🔴OPEN | **撤销命令**需求（15 评论）：希望像 VSCode 一样 undo agent 上一次/整个会话的操作，长期热门需求 |
| 5 | [#11602](https://github.com/can1357/oh-my-pi/issues/11602) 🟢CLOSED | DeepSeek v4.1 flash 官方支持原生视觉输入，但 OMP 未能启用，模型被迫调用外部视觉模型，已修复 |
| 6 | [#3319](https://github.com/can1357/oh-my-pi/issues/3319) 🔴OPEN | **欧洲推理网关**一等公民支持（Melious 等），合规敏感用户的持续诉求 |
| 7 | [#8829](https://github.com/can1357/oh-my-pi/issues/8829) 🔴OPEN | 长会话卡死在 bash 工具：静默 toolResult 停滞、嵌套 hang、僵尸进程、429 retry-after 未被遵守——多 bug 复合的稳定性问题 |
| 8 | [#11014](https://github.com/can1357/oh-my-pi/issues/11014) 🔴OPEN | 智谱 429 重置时间解析 bug：中文"将在…重置"时间戳为北京时间却被当作 UTC，导致会话**晚醒 8 小时** |
| 9 | [#12007](https://github.com/can1357/oh-my-pi/issues/12007) 🟢CLOSED | Windows 主机 1448+ 调试转储全量普查：6 类 53 个可修复 400 错误 + API Key 泄露风险，已在 v18.1.22 修复 |
| 10 | [#12028](https://github.com/can1357/oh-my-pi/issues/12028) 🔴OPEN | Marketplace 插件的 agent `model:` frontmatter 被忽略，子代理始终回退到 `@default`，影响插件生态可用性 |

---

## 四、重要 PR 进展

| # | PR | 内容 |
|---|-----|------|
| 1 | [#12101](https://github.com/can1357/oh-my-pi/pull/12101) | **browser relay 始终驱动全新 omp 专属标签页**，修复 relay 自动接管用户当前可见标签页的危险行为 |
| 2 | [#11654](https://github.com/can1357/oh-my-pi/pull/11654) P0 | 修复 `--mode rpc` 模式下扩展 send 未启动 turn 时的**进程级 fatal unhandled rejection** 竞态 |
| 3 | [#9377](https://github.com/can1357/oh-my-pi/pull/9377) P0 | TUI 修复：已销毁的 live tool block 从共享 spinner ticker 注销，避免会话切换后 80ms ticker 泄漏 |
| 4 | [#12035](https://github.com/can1357/oh-my-pi/pull/12035) | `omp --resume` 会话重定位到已占用 bucket 时崩溃（ENOTEMPTY），现改为合并 artifacts |
| 5 | [#11803](https://github.com/can1357/oh-my-pi/pull/11803) P2 | MCP http/sse 服务器断线后自动指数退避重连（15s 起步、5 分钟上限），不再需要重启会话 |
| 6 | [#9793](https://github.com/can1357/oh-my-pi/pull/9793) P3 | **MCP 懒加载**：`lazy: true` 的服务器在首次调用工具时才启动，显著加快会话启动速度 |
| 7 | [#12085](https://github.com/can1357/oh-my-pi/pull/12085) | edit 工具首次失败即给出 Hashline 语法教学，检测 apply_patch/unified-diff 等错误格式，减少模型重试 |
| 8 | [#12103](https://github.com/can1357/oh-my-pi/pull/12103) | **模型特定 role 路由与预设**：切换默认 provider 时自动将各 role 映射到合适的小模型，解决限额驱动的频繁切换痛点 |
| 9 | [#11863](https://github.com/can1357/oh-my-pi/pull/11863) P1 | OpenAI Responses：处理不完整 payload，兼容 CR/LF/CRLF 混合 SSE 分帧，跨网络分块可靠解析 |
| 10 | [#12104](https://github.com/can1357/oh-my-pi/pull/12104) | 修复扩展（HCOM/collab/ACP/RPC）注入用户消息时**误清空 composer 草稿和待发图片**的问题 |

---

## 五、功能需求趋势

1. **多凭证/账号管理**（#4829、#4614、#11142）：多账号轮换策略、会话级手动切换 ChatGPT/OAuth 账号是最高频需求，反映限额经济下的用户行为。
2. **Provider 生态扩张**：欧洲合规网关（#3319）、Minimax 图像生成（#11808）、Nous Portal（#10444）、Ollama 网页搜索（#3791）、AnySearch（PR #9726）——社区对 provider 长尾覆盖热情高。
3. **模型能力适配**：DeepSeek v4.1 视觉（#11602）、Ollama thinking ladder（#11972）、模型特定 role 路由（PR #12103）。
4. **可观测与导出**：导出中 HTML 标签未渲染（#11690）、subagent 模型显示（#6546）、status line profile 指标（PR #9314）。
5. **会话回溯与安全网**：undo 命令（#5289）、prewalk 规划模型持久化设置（#7809）。

---

## 六、开发者关注点

- **429/配额处理是最大痛点**：Antigravity 虚假 429（3 个相关 issue 合计 140+ 评论）、智谱时区解析导致晚醒 8 小时、retry-after 不被遵守（#8829）——配额感知与重试逻辑需要系统性加固。
- **长会话稳定性**：bash 工具静默卡死、僵尸进程、RPC 竞态崩溃（PR #11654）等夜间挂机场景问题集中出现。
- **插件/扩展生态成熟度**：marketplace 插件 agent model 失效（#12028）、ACP 无结构化失败标记（#11644）、扩展 API 能力缺口（PR #9543、#11895）。
- **安全与隐私**：调试转储泄露密钥已在 v18.1.22 修复，但多账号用户对凭证隔离与脱敏仍高度敏感。

---
*数据来源：github.com/can1357/oh-my-pi · 统计窗口：过去 24 小时（61 条 Issue 更新 / 151 条 PR 更新）*

</details>

<details>
<summary><strong>DeepSeek Harness</strong> — <a href="https://github.com/deepseek-ai/deepseek-harness">deepseek-ai/deepseek-harness</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*