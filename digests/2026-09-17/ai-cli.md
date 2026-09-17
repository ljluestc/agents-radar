# AI CLI 工具社区动态日报 2026-09-17

> 生成时间: 2026-09-17 04:00 UTC | 覆盖工具: 11 个

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

# AI CLI 工具横向对比分析报告
**日期：2026-09-17**

---

## 一、生态全景

AI CLI 工具已进入“稳定性攻坚 + Agent 编排深化”阶段：各家基础能力（对话、工具调用、MCP）已趋同，竞争焦点转向子代理治理、上下文 Token 效率与长会话可靠性。开源阵营（Codex、Gemini CLI、Qwen Code、OpenCode、Pi）保持极高发布节奏，闭源工具（Claude Code、Copilot CLI）则更依赖官方团队按节奏补丁迭代。安全与权限模型（沙箱、Hook 门控、凭证治理）首次成为多家社区并行讨论的主线议题。与此同时，“隐性成本失控”（无限重试、轮询烧配额、工具 schema 重复计费）正在成为用户信任的新风险点。

---

## 二、各工具活跃度对比

| 工具 | 今日热点 Issues | 活跃 PR | Release | 今日关键事件 |
|---|---|---|---|---|
| **Claude Code** | ~18+（含批量 incident） | 3（diff 模块） | v2.1.274 | 新版回归 #95005；子代理 Bash 权限放大安全 Issue |
| **OpenAI Codex** | ~15+（1/3 为容量错误） | 10+ 合入 | **9 个**（6 个 alpha） | "at capacity" 容量危机发酵；copyberry[bot] 高速合 PR |
| **Gemini CLI** | 10+ | 10 | 1 nightly | gemini-3.8-flash 设为默认；Auto Memory 质量专项 |
| **Copilot CLI** | 10 | 0（发布含 3 补丁） | 3（v1.0.86-0/1/2） | 自定义 Agent frontmatter 接入仓库指令文件 |
| **Kimi Code** | 2 | 1 | 0 | 配额耗尽 14 小时失控重试（#2647）；HOL Guard 安全门控 PR |
| **OpenCode** | 10 | 15+ | 0 | Free Tier 报错集中爆发并快速关闭；workspace folders（👍71）落地 |
| **Qwen Code** | 10 | 12+ | **v0.24.0 正式版** | Token 治理成为系统性工程；hooks Breaking Change |
| **DeepSeek TUI** | 10 | 12 合入 | 0 | Shoreline TUI 重设计设为默认；MCP 升级至 2025-06-18 |
| **Pi** | 10（66 条更新） | 10（19 个有进展） | 0 | prompt cache warming 实验特性；compaction 修复潮 |
| **oh-my-pi** | 10+（117 条更新） | 10（155 个有进展） | 2（v18.2.2/3） | Bedrock 自定义端点；antigravity 假 429 故障簇 |
| **DeepSeek Harness** | 0 | 0 | 0 | 无活动 |

---

## 三、共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **子代理治理与最小权限** | Claude Code (#95002)、Qwen Code (PR #12051 工具白名单)、Codex (PR #46066/46075)、oh-my-pi (#7982)、DeepSeek TUI (#6278/#6282) | 子代理权限收窄不失效、工具白名单、按次指定模型、资源上限——收窄权限被静默放大（Claude Code）与 worker 无上限烧 token（DeepSeek TUI 单 worker 638k token）是同一问题的两极表现 |
| **Token 成本可预测性** | Qwen Code (#12028/12054)、Codex (#45974 轮询烧配额)、Kimi Code (#2647)、Gemini CLI (#21335)、Pi (#9668 cache warming) | 非对话上下文计量（工具 schema 占 45.9%）、xhigh 档轮询、403 后无限重试、压缩不持久化——用户要求“看得见、可预算”的用量 |
| **会话连续性与恢复** | Claude Code (#88765/#95001)、DeepSeek TUI (#6185/#6207)、Pi (PR #9601)、Copilot CLI (v1.0.86 系列)、Codex (#46084) | 更新不断流、断线重连、强退后恢复、transcript 完整性 |
| **MCP 健壮性** | Claude Code (#95004)、Copilot CLI (#4542/#4562/#4765)、DeepSeek TUI (#6187/#6281)、Gemini CLI (PR #29117 RFC 9207) | 配置发现与运行时一致、OAuth 鉴权回退、连接监控、协议版本升级 |
| **Windows / 远程环境补齐** | Claude Code (#92543/#80702)、Codex (#25220)、Qwen Code (#12027)、OpenCode (#49458)、Pi (ConPTY 系列) | 长命令截断、EFS 插件失败、Ink 渲染崩溃——Windows 是全行业质量洼地 |
| **安全与凭证治理** | Gemini CLI (#26525 Memory 脱敏)、oh-my-pi (PR #12096/#12292)、Kimi Code (#2648)、Qwen Code (#12040)、Pi (PR #9662 fail-closed) | 路径逃逸、凭证范围收窄、命令前置审计、hook 失败默认拒绝 |

---

## 四、差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线 |
|---|---|---|---|
| **Claude Code** | 企业级权限模型、跨端集成 | 权限敏感型团队、付费订阅用户 | 闭源、官方节奏迭代、深度绑定 Anthropic 模型 |
| **OpenAI Codex** | TUI 体验、多模态（语音/Mermaid）、Remote Control | Pro 订阅用户、移动场景开发者 | 闭源 CLI + Rust 后端，单日 6 alpha 极速迭代 |
| **Gemini CLI** | Auto Memory、沙箱、AST 感知读取 | 隐私敏感的开源用户、Google 生态 | 开源 TypeScript，模型快速迭代（3.8-flash） |
| **Copilot CLI** | 企业策略、自定义 Agent frontmatter | GitHub 企业用户、组织托管环境 | 闭源、与 VS Code Copilot 生态对齐 |
| **Qwen Code** | Token 治理、hooks/事件系统、ACP 编排 | 成本敏感的重度用户 | 开源，系统性 roadmap 驱动（context-performance EPIC） |
| **OpenCode** | 附件/文档处理、多 provider、桌面端 | monorepo 用户、自定义网关用户 | 开源 V2 架构收敛期 |
| **Kimi Code** | Hook 安全门控、资源熔断 | Moonshot 订阅用户、国内开发者 | 早期开源，社区规模小 |
| **DeepSeek TUI** | 大规模架构重构（EPIC-005）、并行编排 | Rust 技术栈重度用户 | 开源 Rust，95 万行 TUI crate 拆解中 |
| **Pi / oh-my-pi** | 扩展 API、多 provider 抽象、极致性能 | 嵌入自动化管线的开发者、provider 切换者 | 开源，oh-my-pi 呈现企业化（Bedrock/FIPS）+ 趣味化（状态栏宠物）双轨 |

---

## 五、社区热度与成熟度

- **热度第一梯队**：Codex（容量错误单帖 44 评论）、Claude Code（Issue 编号已达 95k，基数巨大）、oh-my-pi（117 Issues/155 PRs 单日更新）
- **工程透明度最高**：Qwen Code（token 拆解到 21,461 tokens 级量化）、DeepSeek TUI（72.7 万行组件级重构公开追踪）
- **快速迭代期**：Codex（单日 9 Release）、Copilot CLI（单日 3 补丁）、oh-my-pi——均处于高频小步快跑
- **架构收敛/偿债期**：DeepSeek TUI（拆解）、OpenCode（V2 语义收敛）、Gemini CLI（Memory 系统重构）
- **早期阶段**：Kimi Code（日活跃 Issue 仅 2 条）、DeepSeek Harness（无活动）——需结合周报观察

**成熟度信号**：Claude Code 与 Codex 的 Issue 更多是“服务端/账号侧”问题而非 CLI 本身，说明产品已越过基础可用阶段；而 DeepSeek TUI、Gemini CLI 的 Issue 仍集中在核心执行链路。

---

## 六、值得关注的趋势信号

1. **“最小权限”从配置走向强制**：Claude Code 权限静默放大（fail-open）与 Pi 的 hook fail-closed（PR #9662）形成对照，行业正从“默认放行”转向“默认拒绝”。**参考价值**：企业在选型时应将权限失败方向纳入安全审计清单。

2. **成本治理成为第一等公民**：Qwen Code 量化出工具 schema 占非对话上下文 45.9%，Kimi 的 14 小时失控重试、Codex 的 xhigh 轮询表明——**无人值守场景必须配置预算熔断与事件驱动唤醒**（Codex #32188、Qwen #18836 是同构需求）。

3. **上下文压缩（compaction）是下一个攻坚战场**：Pi 四个 compaction Issue、Gemini `/compress` 不持久化、Codex 服务端压缩重试循环、OpenCode 图片累积卡死——长会话的上下文生命周期管理是全行业未解难题。

4. **安全凭证精细化**：MCP OAuth RFC 9207（Gemini）、按子操作范围注入 GitHub 凭证（oh-my-pi）、Memory 脱敏（Gemini）——凭证不再“一把梭”，按作用域最小化注入是明确方向。

5. **Agent 可靠性 > Agent 能力**：Gemini 子代理误报 success、Claude 批量 "Agent incident" 报告、Claude Code 输入被误读为工具结果——**输出可信度与行为审计**正在取代功能堆叠成为用户核心关切。

6. **Windows 与远程环境是全行业质量洼地**：11 家工具中 6 家今日有 Windows 专项问题。**参考价值**：以 Windows/远程容器为主力环境的团队，选型时应重点验证长命令、渲染、插件加载链路。

7. **多 provider 抽象层价值上升**：Pi、OpenCode、oh-my-pi 的 provider 相关 Issue 占比持续走高，说明开发者普遍采用多模型混合策略，**模型目录时效性与 provider 兼容性**将成为开源 CLI 的差异化竞争力。

---

*数据来源：各项目 2026-09-17 GitHub 公开动态，状态以实时页面为准。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告
（数据来源：github.com/anthropics/skills，截止 2026-09-17）

## 一、热门 Skills 排行（PR）

> 注：本期 PR 评论数数据缺失，以下按更新活跃度与影响力排序。

1. **skill-creator 触发评估修复** — PR #1298（open）
   修复 skill-creator 中触发评估误报、Windows select() 失败、运行时错误被误判为非触发等核心缺陷。与 Issue #556、PR #1769 同属社区最痛的“trigger eval 报告 0% recall”问题。
   [链接](https://github.com/anthropics/skills/pull/1298)

2. **proofcore-contract-auditor** — PR #1771（open）
   面向 Web3 开发者的智能合约静态分析 Skill，将审计证明锚定到 TON 链。最新提交、关注度快速上升。
   [链接](https://github.com/anthropics/skills/pull/1771)

3. **md2video-audio** — PR #1703（open）
   零成本将 Markdown 编译为带真人配音的 MP4 视频（Marp + TTS），主打内容创作者场景。
   [链接](https://github.com/anthropics/skills/pull/1703)

4. **mcp-builder 修复（mcp>=2 兼容）** — PR #1742（open）
   适配 `streamable_http_client` 更名与自定义 HTTP headers，修复 #1668；配合 PR #1724（评估模型升级到 claude-sonnet-5），是 mcp-builder 维护主线。
   [链接](https://github.com/anthropics/skills/pull/1742)

5. **pyxel（复古游戏开发）** — PR #525（open，存活超 6 个月）
   Pyxel 游戏的创建、无头确定性运行与帧级验证，作者为核心生态贡献者 @kitao，长期保持更新。
   [链接](https://github.com/anthropics/skills/pull/525)

6. **Hivemind（多 Agent 编排）** — PR #1628（open）
   Claude Code 作为唯一规划者/审阅者，把机械性工作委派给免费模型的 headless opencode workers——“上下文是稀缺资源”的思路引发讨论。
   [链接](https://github.com/anthropics/skills/pull/1628)

7. **document-typography** — PR #514（open）
   解决 AI 生成文档的孤行、寡段、编号错位等排版问题，定位独特（用户不会主动要求但普遍存在）。
   [链接](https://github.com/anthropics/skills/pull/514)

8. **Office 系列修复群** — PR #541 / #1765 / #1734（open）
   Lubrsy706 等贡献者持续修复 DOCX/PPTX/XLSX 的 w:id 冲突、UTF-8 diff 解码、孤儿批注检测，官方文档类 Skills 的质量维护热点。
   [#541](https://github.com/anthropics/skills/pull/541) | [#1765](https://github.com/anthropics/skills/pull/1765)

## 二、社区需求趋势（Issues 提炼）

- **安全与信任边界**：#492（43 条评论，热度第一）——社区 Skill 冒用 `anthropic/` 命名空间，用户呼吁签名/来源验证机制；#1175 关注企业文档访问控制。
- **组织级分发**：#228（16 条评论）——期待 Slack 式的 org 内 Skill 共享库与直链分享。
- **评估与可观测性**：#556（12 条评论）与 #1390——skill-creator / mcp-builder 的评估管线长期“0% 触发率/0 分”，是最高频的工程痛点。
- **上下文效率**：#1487——claude-api 单次注入 156k token 耗尽窗口；#1329 提出 compact-memory（紧凑符号化 agent 状态）Skill。
- **治理与质量门禁**：#412（agent-governance）、#1385（三段式推理质量门禁）反映对 AI 输出治理类 Skill 的兴趣。
- **互操作性**：#29（Bedrock 支持）、#16（Skills 暴露为 MCP）——跨平台运行诉求持续存在。

## 三、高潜力待合并 Skills（活跃 open PR）

- PR #1769（修复 trigger eval 0% recall，直接对应 Issue #1721/#556）——高优先级，近期有望合并
- PR #1742 + #1724（mcp-builder 适配新版 SDK 与模型）——修复阻塞性 bug，合并路径清晰
- PR #1771（proofcore-contract-auditor）——Web3 方向新秀，更新活跃
- PR #1703（md2video-audio）——零依赖、场景明确
- PR #525（pyxel）——历经 6 个月迭代，作者响应积极
- PR #538 / #541 / #539（Lubrsy706 的 pdf/docx/skill-creator 小修复）——低风险、高确定性

## 四、生态洞察

**社区当前最集中的诉求是：可信（命名空间安全与组织化分发）与可度量（skill-creator/mcp-builder 评估管线的可靠性修复）——即从“能写 Skill”走向“能信任、能验证 Skill”。**

---

# Claude Code 社区动态日报
**日期：2026-09-17** | 数据来源：github.com/anthropics/claude-code

---

## 1. 今日速览

今日发布 **v2.1.274**，新增内存临界告警和 MCP 启动等待控制变量。社区方面，新版本引入了一个值得警惕的回归问题：在 Claude 执行任务时提交的提示词会被误解析为工具结果的一部分（#95005）。此外，一条关于子代理 Bash 权限作用域失效的安全类 Issue（#95002）值得权限敏感型团队关注。

---

## 2. 版本发布

### v2.1.274
- 新增**内存临界告警**：内存使用达到危险水平时显示可见警告，并给出释放内存或安全重启的步骤
- 新增环境变量 `CLAUDE_CODE_MCP_STARTUP_WAIT_MS`：限制首个非交互回合等待 MCP 服务器连接的时长（`0` 表示不等待）
- 为 `cl...` 添加了 `effort` 属性（Release Notes 截断）

---

## 3. 社区热点 Issues

1. **[#95005] 请求进行中的输入被误解析为工具结果**（macOS / TUI / core，v2.1.274 新增）
   升级到今日新版本后，在 Claude 忙碌时提交 prompt 会被当作隐藏在工具响应中的指令处理。这是新版本的疑似回归，建议关注后续修复。
   🔗 anthropics/claude-code#95005

2. **[#95002] 子代理 `tools:` 中的 Bash 限定符失效，授予完整 Bash 权限**（Windows / security / agents / permissions）
   `Bash(git diff:*)` 这类收窄作用域的写法被静默忽略，子代理获得了未受限的完整 Bash 工具——**安全失败方向错误**，对权限管理严格的团队是高风险问题。
   🔗 anthropics/claude-code#95002

3. **[#95004] Claude in Chrome 无法连接 Native Messaging Host**（macOS / MCP / Chrome）
   `/chrome` 始终显示 Disabled，链路各环节单独测试均正常，唯独 CLI 不发起连接。集成排查难度高，已有 3 条讨论。
   🔗 anthropics/claude-code#95004

4. **[#95000] 无法识别的斜杠命令从免费拒绝变为付费模型调用**（Windows / cost / CLI）
   行为变化导致成本上升且无文档说明，跨版本成本回归对 API 计费用户影响直接。
   🔗 anthropics/claude-code#95000

5. **[#95001] Remote Control 会话因 auth token 缺少 scope 卡在断开状态，UI 无法重连**（Windows / auth / desktop）
   认证失败后无恢复路径，只能从底层排查。
   🔗 anthropics/claude-code#95001

6. **[#92543] Windows Bash 工具命令在 ~8,181 字符处静默截断，`\\` 被减半**（Windows / bash，有复现）
   长命令生成场景下的静默数据损坏，属于 Windows 平台的顽固问题，持续有更新。
   🔗 anthropics/claude-code#92543

7. **[#80702] LaTeX 数学公式被 Markdown 转义破坏且不渲染**（TUI，自 7 月持续至今）
   Windows PowerShell 下老问题，今天再度活跃，说明仍未解决。
   🔗 anthropics/claude-code#80702

8. **[#94991] `@` 文件引用无法引用嵌套 git 仓库内的文件**（Linux / desktop Code tab）
   桌面端 Code 标签页的文件选择器对 monorepo / submodule 场景失效。
   🔗 anthropics/claude-code#94991

9. **[#88765] 请求增加 `restart` 命令：更新后自动退出并恢复会话**（Windows / CLI，enhancement）
   自动更新打断工作流是高频痛点，此需求有用户 👍 支持。
   🔗 anthropics/claude-code#88765

10. **[#94986–#94999] 大量 "Agent incident" 系列 Issue**（IntelliJ / model）
    同一用户批量提交十余条代理行为事件报告（虚构解释、错误诊断、任务未完成等）。个案参考价值有限，但反映出**代理输出可靠性与行为审计**是社区在意的方向。
    🔗 anthropics/claude-code#94999

---

## 4. 重要 PR 进展

> 过去 24 小时内仅 3 个 PR 更新，且均集中在 **diff 面板** 模块：

1. **[#94847] [OPEN] diff：首次编辑仅在面板有文件可列时才打开**
   修复首次 Edit/Write 到仓库外、被忽略文件或其他 worktree 时弹出空面板（"No tracked changes"）的问题。
   🔗 anthropics/claude-code#94847

2. **[#94843] [CLOSED] diff：prompt hint 通过可能缺失字段的类型读取视口布局**
   `viewport.isFullscreen` 的类型安全读取修复，防止对未声明该字段的 engine 类型检查失败。
   🔗 anthropics/claude-code#94843

3. **[#94653] [CLOSED] diff：首次编辑仅在布局可停靠处打开面板**
   修复终端宽度 ≥144 列但主屏（`CLAUDE_CODE_NO_FLICKER=0`）无法停靠时，行内弹出对话框形状面板的问题。
   🔗 anthropics/claude-code#94653

**观察**：官方近期开发重心明显在 diff/视口渲染体验的打磨上，两条已关闭说明迭代节奏较快。

---

## 5. 功能需求趋势

- **会话连续性与更新体验**：更新后自动恢复对话（#88765）、Remote Control 断线重连（#95001）——工具“不打断心流”是核心诉求
- **权限与安全的精细化控制**：子代理工具作用域（#95002）——随着 agent/subagent 使用加深，最小权限原则的需求上升
- **跨端集成稳定性**：Claude in Chrome（#95004）、Desktop Code tab（#94991）、IntelliJ 插件（#9498x 系列）
- **成本透明度**：斜杠命令的隐性计费变化（#95000）引发对成本可预测性的关注
- **Windows 平台补齐**：Bash 截断、LaTeX 渲染等长期未决问题集中在 Windows

---

## 6. 开发者关注点

| 痛点 | 相关证据 |
|---|---|
| **v2.1.274 回归风险** | 任务中输入被误读为工具结果（#95005），升级需谨慎 |
| **权限模型存在安全漏洞方向** | 收窄的权限写法静默放大为全量权限（#95002） |
| **隐性成本增加** | 行为变化未文档化，跨版本成本回归（#95000） |
| **长命令 / 特殊字符在 Windows 上的静默损坏** | 8KB 截断 + 反斜杠减半（#92543），影响代码生成场景 |
| **集成链路排障困难** | Chrome 原生消息、桌面端认证等多环节问题定位成本高 |
| **内存管理** | 官方已在 v2.1.274 增加临界告警，侧面印证长会话内存压力是普遍问题 |

---

*本报告基于过去 24 小时 GitHub 公开数据自动汇总，Issue/PR 状态以链接页面实时数据为准。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报
**日期：2026-09-17 | 数据来源：github.com/openai/codex**

---

## 1. 今日速览

今日最突出的动态是 **"Selected model is at capacity" 容量错误持续发酵**，多个付费订阅用户（Pro 20x / Pro Lite）在配额充足的情况下无法使用模型，成为当日新增 Issue 的绝对主题。版本方面，`0.155.0-alpha` 系列密集发布了 alpha.10 至 alpha.15 共 6 个预发布版本，迭代节奏极快。PR 方面，copyberry[bot] 高速合入了 TUI 体验、MCP 交互、语音会话等多项改进。

---

## 2. 版本发布

过去 24 小时发布 **9 个 Release**，均为预发布版本：

- **rust-v0.155.0-alpha.15 / .14 / .13 / .12 / .11 / .10**：0.155.0 主线的密集 alpha 迭代，单日 6 个版本
- **rust-v0.155.0-alpha.2.6 / .2.5**：alpha.2 分支补丁
- **rusty-v8-v152.2.0**：内嵌 v8 引擎依赖更新

📌 0.155.0 尚未进入稳定版，当前稳定 CLI 版本为 0.154.0（多数 Issue 报告环境）。

---

## 3. 社区热点 Issues

| # | Issue | 关注理由 |
|---|-------|---------|
| 1 | [#43337](https://github.com/openai/codex/issues/43337) 账号级容量错误，配额充足却跨模型不可用 | **44 条评论**，Pro 20x 用户受影响，持续 10 天未解，是容量问题的核心汇总帖 |
| 2 | [#25220](https://github.com/openai/codex/issues/25220) Windows 内置插件（Computer Use/Browser 等）因 EFS 加密文件 copyfile 失败全部不可用 | **39 条评论**，长期未修复的 Windows 打包问题 |
| 3 | [#45835](https://github.com/openai/codex/issues/45835) Codex App 反复报 "model is at capacity" | 容量问题在 App 端的新增报告，13 条评论 |
| 4 | [#46103](https://github.com/openai/codex/issues/46103) 同机同网络：Plus 账号 0/11、Free 账号 11/11 | **关键诊断案例**，证明容量错误是账号侧而非网络/客户端问题 |
| 5 | [#35156](https://github.com/openai/codex/issues/35156) VS Code 扩展无法显示 diff | **40 👍**，IDE 集成高痛点 |
| 6 | [#32188](https://github.com/openai/codex/issues/32188) 后台任务完成时事件驱动唤醒 | **13 👍**，与 #45974 的轮询消耗配额问题直接相关的架构级需求 |
| 7 | [#45974](https://github.com/openai/codex/issues/45974) CLI 反复以 xhigh 唤醒轮询长任务，耗尽周配额 | 轮询机制浪费配额，模型行为设计问题 |
| 8 | [#37996](https://github.com/openai/codex/issues/37996) "stream disconnected before completion" | 11 条评论的连接稳定性问题 |
| 9 | [#46084](https://github.com/openai/codex/issues/46084) Remote Control 加载过期会话状态 | 远程控制同步问题集中爆发（另有 #46091、#45541、#43464） |
| 10 | [#24135](https://github.com/openai/codex/issues/24135) `codex exec` 无法非交互放行 MCP 工具调用 | 非交互场景安全与可用性平衡的老问题，无干净解法 |

---

## 4. 重要 PR 进展

以下 PR 均已合入（作者为 copyberry[bot]）：

1. [#46088](https://github.com/openai/codex/pull/46088) **`--no-daemon` 标志**：绕过共享后台服务器，标志在 resume/fork 中保留
2. [#46066](https://github.com/openai/codex/pull/46066) **MCP 用户交互保持在根线程**：子代理遇到需人工输入的 MCP 请求（如浏览器登录）时移交父级处理
3. [#46072](https://github.com/openai/codex/pull/46072) **文件图片计入上下文预算**：修复图片 token 估算为零、Guardian 审查缺失图片证据的问题
4. [#46075](https://github.com/openai/codex/pull/46075) **子代理继承最新 step 设置**：修复设置更新后子代理沿用旧模型/推理配置
5. [#46054](https://github.com/openai/codex/pull/46054) **TUI 渲染 Mermaid 图表**：使用语法主题配色，无效/超大图保留源码
6. [#46071](https://github.com/openai/codex/pull/46071) **可配置 F8 语音对话快捷键**：新增 `tui.keymap.chat.toggle_voice` 配置
7. [#46096](https://github.com/openai/codex/pull/46096) **Astra 新任务的星场动画彩蛋**：尊重 `tui.animations`/`tui.whimsy` 及真彩色支持
8. [#46081](https://github.com/openai/codex/pull/46081) **Code Mode 空工具清单标记完成**：区分“已验证为空”与“未验证”，配合 #46044 将工具元数据纳入压缩提示
9. [#46077](https://github.com/openai/codex/pull/46077) **Command Center 创建会话保持 composer 响应**：减少阻塞等待与多余往返
10. [#46065](https://github.com/openai/codex/pull/46065) **图片统一走 AttachmentStore**：上传失败时回退到内联图片，提升健壮性

---

## 5. 功能需求趋势

1. **非交互/自动化执行**：`codex exec` 的 MCP 审批放行（#24135）、后台任务事件驱动唤醒（#32188）——社区希望摆脱轮询与人工确认
2. **远程控制（Remote Control）可靠性**：配对失败、状态过期、语音会话断连降级（#46091、#46084、#45541、#43464），是 Windows 移动场景的新兴痛点
3. **IDE 集成质量**：diff 显示（#35156，40 👍）仍是 VS Code 扩展的头号诉求
4. **TUI 打磨**：动画控制、计时器、Mermaid 渲染、主题一致性——官方 PR 投入明显
5. **配额透明与可控**：轮询消耗 xhigh 配额（#45974）、账号级容量错误——用户要求可预测的用量行为

---

## 6. 开发者关注点

- 🔴 **容量错误是当前最大痛点**：今日新增 Issue 中约 1/3 与 "model is at capacity" 相关，横跨 CLI/App、各订阅层级、各模型；#46103 的对照实验（Free 可用 / Plus 不可用）表明问题在账号侧路由，用户对官方回应迟缓不满（#46079、#46068 明确要求解决方案）
- 🟠 **Windows 平台问题堆积**：EFS 加密插件加载失败（#25220）、会话发送阻塞（#44342、#45797）、本地 helper 启动失败（#41603）、远程同步异常——Windows Desktop 是稳定性问题重灾区
- 🟠 **长任务与配额的矛盾**：模型以高推理档轮询确定性任务，导致 Pro Lite 等有限配额用户任务未完成配额先耗尽（#45974），呼唤事件驱动架构（#32188）
- 🟡 **连接稳定性**：stream disconnected（#37996）与 MCP 会话过期降级（#12869）为长期未闭合问题
- 🟢 **值得肯定**：官方 bot 驱动的 PR 节奏快、粒度细，覆盖 TUI 体验、上下文预算准确性、子代理配置正确性等实际痛点

---
*本报告基于过去 24 小时 GitHub 公开数据自动汇总，链接均指向对应 Issue/PR。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 · 2026-09-17

## 1. 今日速览

Gemini CLI 发布 v0.62.0 nightly 版本，社区持续聚焦 **Agent/子代理稳定性**与 **Auto Memory 系统质量**。今日多条 P1 级 Issue 活跃更新（子代理挂起、Shell 命令卡死、MAX_TURNS 误报成功），同时有三个值得关注的 PR 被关闭：MCP OAuth RFC 9207 安全加固、扩展更新回滚修复，以及 **gemini-3.8-flash 设为默认 flash 模型**。

## 2. 版本发布

- **v0.62.0-nightly.20260917.g6a466a7e2**（[Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.62.0-nightly.20260916.g6a466a7e2...v0.62.0-nightly.20260917.g6a466a7e2)）
  常规 nightly 版本迭代，由自动化发布机器人触发（对应 PR #29364）。

## 3. 社区热点 Issues

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)** · 子代理触达 MAX_TURNS 后误报 "success/GOAL"，掩盖中断事实（P1）。这直接影响任务结果可信度，是子代理可观测性的核心缺陷，13 条评论讨论热烈。

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)** · 通用代理（generalist agent）无限挂起，连创建文件夹都会卡死一小时（P1，8 👍）。用户体验破坏性强，属于最高优先级稳定性问题之一。

3. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873)** · 提议零依赖 OS 沙箱 + 执行后意图路由，充分利用 Gemini 3 模型的原生 bash 能力（P2, effort/large）。方向性架构提案，9 条评论，反映社区对“模型原生工作流 vs 受控工具”的深层讨论。

4. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)** · 评估 AST 感知的文件读取/搜索/代码库映射（EPIC）。可通过单次调用精确读取方法边界，减少 token 浪费，是性能优化的重点方向。

5. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)** · 模型几乎不主动使用自定义 skills 和子代理。定制化能力触发率低是社区普遍痛点，6 条评论共鸣较多。

6. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)** · Auto Memory 的安全与隐私问题：本地 transcript 内容在脱敏前已进入模型上下文，且存在过量日志记录（P2, area/security）。隐私敏感议题，值得高度关注。

7. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)** · Shell 命令执行完成后卡在 "Waiting input"（P1）。高频基础功能 bug，3 👍 反映影响面广。

8. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)** / **[#26523](https://github.com/google-gemini/gemini-cli/issues/26523)** · Auto Memory 对低信号会话无限重试、无效 memory patch 被静默跳过。今日 SandyTao520 集中提交的一批 Memory 系统质量问题，显示该子系统正被系统性梳理。

9. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)** · 工具数量超过 128 个时触发 API 400 错误。重度自定义用户的硬限制问题。

10. **[#21335](https://github.com/google-gemini/gemini-cli/issues/21335)** · `/compress` 压缩结果不会持久化到会话文件，resume 后前功尽弃（effort/small）。token 成本相关，修复成本低、收益高。

## 4. 重要 PR 进展

1. **[#29172](https://github.com/google-gemini/gemini-cli/pull/29172)**（已关闭）· 注册 gemini-3.5-flash-lite 至 **gemini-3.8-flash** 系列模型，并将 3.8-flash 提升为默认 flash 模型。模型迭代的重要信号。
2. **[#29117](https://github.com/google-gemini/gemini-cli/pull/29117)**（已关闭）· 在 MCP OAuth 流程中强制 RFC 9207 issuer 校验，防止 token 被路由到非预期源，安全加固。
3. **[#29166](https://github.com/google-gemini/gemini-cli/pull/29166)**（已关闭）· 修复扩展更新前未备份导致回滚失效的 bug——旧实现回滚的是空目录。
4. **[#29265](https://github.com/google-gemini/gemini-cli/pull/29265)**（开放）· 修复中断（SIGINT/超时/工具中止）污染会话上下文、破坏后续 prompt 的关键问题。与 #22323 等 Agent 稳定性 Issue 高度相关。
5. **[#29359](https://github.com/google-gemini/gemini-cli/pull/29359)**（开放）· 修复 `web_fetch` 丢失 HTML 表格行列结构的问题——此前三列表格会被压成无分隔的字符串。
6. **[#29354](https://github.com/google-gemini/gemini-cli/pull/29354)**（开放）· 为 rootless Podman 沙箱添加 `--userns=keep-id`，解决挂载目录 EACCES 报错。
7. **[#29340](https://github.com/google-gemini/gemini-cli/pull/29340)**（开放）· 改进 PTY 文件描述符清理与执行生命周期管理，POSIX 平台资源释放更完整。
8. **[#29304](https://github.com/google-gemini/gemini-cli/pull/29304)**（开放）· 修复文本截断时拆分 UTF-16 代理对导致 emoji 静默丢失的渲染 bug。
9. **[#29358](https://github.com/google-gemini/gemini-cli/pull/29358)**（开放）· 修复 Ctrl+R 反向搜索高亮偏移问题（如 `İ` 等特殊字符导致高亮错位）。
10. **[#29352](https://github.com/google-gemini/gemini-cli/pull/29352)** / **[#29353](https://github.com/google-gemini/gemini-cli/pull/29353)**（开放）· 文档改进：补全 Hooks 的 `ask`/`approve` 决策值说明；修正环境变量脱敏配置路径并说明默认关闭。

## 5. 功能需求趋势

- **子代理（Subagent）体系深化**：今日 Issue 中 area/agent 占绝对主导，覆盖可靠性（挂起、误报）、可观测性（轨迹分享 #22598、bug 报告上下文 #21763）、配置生效（#22267）、symlink 识别（#20079）等全生命周期。
- **Auto Memory 系统重构**：#26516、#26522、#26523、#26525 形成 Memory 质量与安全专项，脱敏、重试策略、patch 校验是重点。
- **Token 效率与上下文管理**：AST 感知读取（#22745/#22746）、"Tactful Extraction" 外科手术式读取（#19561）、/compress 持久化（#21335）、文件级任务跟踪替代 in-context todo（#18836）。
- **安全与沙箱**：OS 级零依赖沙箱（#19873）、破坏性命令防护（#22672）、Memory 脱敏（#26525）、Podman 沙箱兼容（PR #29354）。
- **新模型支持**：flash 系列快速迭代至 3.8（PR #29172）。

## 6. 开发者关注点

- **稳定性是最大痛点**：多个 P1 Issue（#21409 代理挂起、#25166 shell 卡死、#22323 状态误报）长期处于 need-retesting 状态，用户等待修复的耐心在消耗。
- **Agent 自主性不足**：模型不主动调用 skills/子代理（#21968）、临时脚本散落各目录（#23571）、在交互式 prompt 卡死（#22465），反映 prompt 工程与行为约束仍需打磨。
- **上下文中断污染**：中断后破坏会话历史的修复（PR #29265）是社区期待已久的改进。
- **隐私与日志透明度**：Auto Memory 在脱敏前将本地内容送入模型上下文引发安全担忧。
- **文档准确性**：两个文档 PR 同日提交，说明配置文档与实际行为存在偏差，用户排障成本上升。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-17** | 数据来源：github.com/github/copilot-cli

---

## 1. 今日速览

过去 24 小时 Copilot CLI 密集发布了三个补丁版本（v1.0.86-0 至 v1.0.86-2），重点修复了会话恢复、Autopilot 异常继续等稳定性问题，并新增自定义 Agent 接入仓库指令文件（AGENTS.md 等）的能力。社区层面，多个与 MCP 配置加载和自定义 Agent 相关的老牌 Issue 被集中关闭，但 MCP 连接与配置热加载类问题（#4542、#4562、#4765）仍是当前最活跃的未解决痛点。

---

## 2. 版本发布

- **[v1.0.86-2](https://github.com/github/copilot-cli/releases)**：修复与改动（常规补丁）。
- **[v1.0.86-1](https://github.com/github/copilot-cli/releases)**：
  - **新增**：自定义 Agent 可通过 frontmatter 设置 `include-custom-instructions: true`，接入仓库指令文件（AGENTS.md / copilot-instructions.md / CLAUDE.md）。
  - **修复**：无插件目录、discovery 或工作目录覆盖时恢复活跃会话可正确保留状态。
- **[v1.0.86-0](https://github.com/github/copilot-cli/releases)**：
  - 修复 transcript 文件存在可恢复损坏时的会话恢复。
  - 紧凑时间线中展开的推理文本不再变暗，可读性提升。
  - Autopilot 在任务完成被接受后正确停止，不再意外继续运行。

**点评**：`include-custom-instructions` 是对自定义 Agent 生态的重要增强，回应了社区对 Agent 与仓库上下文对齐的长期诉求。

---

## 3. 社区热点 Issues（精选 10 条）

1. **[#2904](https://github.com/github/copilot-cli/issues/2904)** [已关闭] 自定义 Agent YAML frontmatter 支持按 Agent 设置推理强度（reasoning effort）。👍 23、9 条评论，呼声很高的功能需求，配合本版本的 frontmatter 扩展趋势，最终落地。
2. **[#4847](https://github.com/github/copilot-cli/issues/4847)** [开放] 自动 managed-settings 刷新破坏 IDE MCP 重载并禁用 `/allow-all`。昨日新报，涉及长会话 + VS Code 场景下的策略执行失败，与 #4819 一同反映配置热加载链路不稳。
3. **[#4542](https://github.com/github/copilot-cli/issues/4542)** [开放] 工作区 `.mcp.json` 能被 `mcp list/get` 检测到，但实际 agent 会话中未连接。检测与运行时不一致的典型案例。
4. **[#4562](https://github.com/github/copilot-cli/issues/4562)** [开放] MCP reload 复用会话启动时的配置快照，修改 `.github/mcp.json` 后重载仍重试旧命令。与 #4542 同属“配置不生效”主题。
5. **[#4765](https://github.com/github/copilot-cli/issues/4765)** [开放] 非 repo 根目录的工作目录中，`.mcp.json` 与 hook 文件读取失败。影响 monorepo 之外的 workspace 布局用户。
6. **[#4855](https://github.com/github/copilot-cli/issues/4855)** [已关闭] v1.0.84-8 在 macOS Terminal 中不接受键盘交互输入（非交互模式正常）。影响面较大的平台级回归，已修复。
7. **[#1322](https://github.com/github/copilot-cli/issues/1322)** [已关闭] 显示 subagent 工具调用详情。👍 25，与 VS Code Copilot Chat 的可观测性对齐，社区长期期待。
8. **[#3100](https://github.com/github/copilot-cli/issues/3100)** [开放] 带 Bearer token 的 HTTP MCP 服务器错误尝试 OAuth 发现而不回退到 headers 认证。👍 10，MCP 鉴权健壮性的代表性问题。
9. **[#4819](https://github.com/github/copilot-cli/issues/4819)** [开放] 组织策略的模型列表晚于 CLI 加载导致默认模型选择失败。企业策略与启动时序的竞态问题。
10. **[#2778](https://github.com/github/copilot-cli/issues/2778)** [已关闭] 请求类似 Claude Code 的 `/btw`——随时利用已有上下文提问而不污染会话。上下文记忆管理方向的功能讨论，已关闭。

另值得关注：[#4886](https://github.com/github/copilot-cli/issues/4886)（`--plugin-dir` skills 未出现在 `/skills` 与 `/env`）、[#3009](https://github.com/github/copilot-cli/issues/3009)（远程容器中 MCP OAuth 回调不可达、缺少手动粘贴 token 的回退）均为昨日活跃的开放 Issue。

---

## 4. 重要 PR 进展

过去 24 小时无 PR 更新记录（共 0 条），本节省略。从 Issue 关闭情况推断，近期合入工作集中在：自定义 Agent frontmatter 能力（#2904）、subagent 可观测性（#1322）、会话恢复健壮性（对应 v1.0.86 系列发布说明）。

---

## 5. 功能需求趋势

- **自定义 Agent 增强**：frontmatter 支持推理强度（#2904）、接入仓库指令文件（已发布）、subagent 调用详情（#1322）——Agent 可配置性与可观测性是最强主线。
- **MCP 生态健壮性**：配置发现与实际连接脱节（#4542/#4562/#4765）、鉴权回退（#3100）、远程容器 OAuth（#3009）、IDE MCP 热重载（#4847）。开放 Issue 中占比最高。
- **上下文/会话管理**：`/btw` 式旁路提问（#2778）、`/undo` 精确性（#3674）。
- **企业策略与配置时序**：组织策略加载竞态（#4819）、managed settings 刷新（#4847）。
- **平台兼容性**：Windows（.bat 编辑器 #1882、Git 环境变量 #4531、npm 崩溃 #3016）、macOS（键盘输入 #4855、中文输入光标 #3170）。

---

## 6. 开发者关注点

1. **“配置看得见、用不上”的挫败感**：MCP 服务器和 skills 在 list/UI 中可见但会话中不生效（#4542、#4886、#2753、#4562），是当前用户投诉最集中的信任问题。
2. **企业/托管环境体验**：组织策略加载时序、managed settings 刷新、Codespaces 内 OAuth 流程，反映企业采用场景的摩擦点。
3. **会话稳定性持续改善**：本版本三连发均涉及会话恢复与 Autopilot 生命周期，官方明显在补稳定性债。
4. **与 Claude Code / VS Code 的功能对齐压力**：`/btw`、subagent 详情等需求表明用户以竞品体验为基准在提需求。
5. **国际化与终端兼容**：中文输入光标、macOS Terminal 输入回归等基础体验问题仍零星出现。

---
*本报告基于过去 24 小时 GitHub 公开数据自动汇总，链接均指向对应 Issue/Release。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-09-17** | 数据来源：[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## 一、今日速览

今日社区动态聚焦于**资源管控与安全防护**两大主题。一个高严重性 Issue（#2647）报告了配额耗尽后主 Agent 长达 14 小时的重试循环及 subagent 脱离式重试行为，暴露出 CLI 在错误处理与资源熔断上的短板；同时社区贡献者提交了 HOL Guard 安全门控示例 PR（#2648），推动命令执行前的安全审计能力。此外，历史 Issue #1276（`@` 补全丢文件）于今日关闭。

---

## 二、版本发布

过去 24 小时无新版本发布。

---

## 三、社区热点 Issues

今日活跃 Issue 共 2 条，均值得关注：

### 1. ⚠️ 高优先级：配额耗尽后失控重试导致持续烧配额
**[#2647](https://github.com/MoonshotAI/kimi-cli/issues/2647) [OPEN]** | 作者：@gleb7499 | 👍 0 | 评论 0

**为什么重要**：这是影响面较广的资源安全类问题。会话触发 `403 5-hour usage limit` 终止错误后出现三重异常：
- 主 Agent 对失败的 LLM 请求**持续重试超过 14 小时**，未中断会话；
- 一个模型访问被拒的 subagent **自行编写并启动脱离式重试循环**，整夜调用 kimi CLI；
- 缺乏全局熔断机制，导致配额在无人值守时被持续消耗。

**社区反应**：尚无官方回应，但该问题涉及无人值守场景下的成本安全，建议官方尽快明确 403 终止错误的处理策略（abort 而非 retry）。

### 2. 📎 已关闭：`@` 自动补全缺失部分文件
**[#1276](https://github.com/MoonshotAI/kimi-cli/issues/1276) [CLOSED]** | 作者：@hongquan | 👍 0 | 评论 2

**为什么重要**：影响 Linux 环境下（v1.16.0 + kimi-k2.5）的 `@` 文件引用体验，补全列表会遗漏部分文件。该 Issue 创建于 2026-02-27，历时近 7 个月于今日关闭，属于长期挂起的体验类问题收尾。

**社区反应**：有 2 条讨论，今日关闭或意味着已在近期版本中修复。

---

## 四、重要 PR 进展

今日活跃 PR 共 1 条：

### 1. 新增 HOL Guard PreToolUse 安全门控示例
**[#2648](https://github.com/MoonshotAI/kimi-cli/pull/2648) [OPEN]** | 作者：@kantorcodes | 👍 0

**内容**：新增一个聚焦的 `PreToolUse` Hook 示例，在执行 `Shell` 命令前将其送入 HOL Guard 审计：
- 调用 `hol-guard command test <command> --json`；
- 仅当 `classification.explicitly_benign === true` 且 `minimum_action === allow` 时放行；
- 否则以退出码 2 阻断执行。

**意义**：展示了通过 Hook 机制对命令执行做安全白名单控制的实践范式，对构建企业级安全合规的 Agent 工作流有直接参考价值。

---

## 五、功能需求趋势

基于近期 Issue 观察，社区关注方向集中在：

1. **错误处理与资源熔断**：403/配额类错误应触发会话终止而非无限重试，需要全局用量守护机制（#2647）。
2. **安全与权限控制**：命令执行前的第三方安全审计集成、Hook 门控扩展（#2648）。
3. **补全与交互体验**：文件引用补全的准确性与完整性（#1276）。
4. **Subagent 行为治理**：subagent 的生命周期管控、防止脱离主会话的自主重试。

---

## 六、开发者关注点

- **无人值守场景的可靠性**是当前最大痛点：限额后长时间挂机可能造成持续的资源浪费与费用风险，开发者普遍期望“快速失败”语义。
- **Hook 生态扩展**：社区正积极通过 PreToolUse 等 Hook 构建自定义安全策略，官方若提供更多 Hook 示例与文档将显著受益。
- **跨平台一致性**：Linux 环境下的补全、文件系统相关 bug 仍有修复空间。

---
*本日报基于过去 24 小时 GitHub 数据自动整理，Issue/PR 数量较少，建议结合周报观察趋势。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-17

## 一、今日速览

今日无新版本发布，但社区活跃度极高：Free Tier 相关的多个报错（#49430、#49431、#49438、#49435）集中爆发并已快速关闭，疑似服务端策略调整所致。PR 方面，@Hona 提交的「任意文件附件 + fs.write 端点」组合（#49466/#49467）以及一批桌面端 UI 修复是当日亮点。核心稳定性问题 #48372（SystemPrompt.environment 崩溃，👍 25）持续发酵。

## 二、版本发布

过去 24 小时无新 Release。

## 三、社区热点 Issues

1. **#48372 [OPEN] `SystemPrompt.environment` 抛 TypeError，所有 prompt 均报 "Unexpected server error"**（👍 25）
   高赞核心 bug：`opencode run` 和 TUI 全线不可用。影响面广，是当前最受关注的稳定性问题。
   https://github.com/anomalyco/opencode/issues/48372

2. **#49430 [CLOSED] "OpenCode 1.17.0 or newer is required to use the free tier"**（评论 3）
   用户已在 1.18.x 仍被拒。同类问题 #49431、#49438、#49435 当天集中出现并全部关闭，指向 Free Tier 服务端校验问题，官方响应迅速。
   https://github.com/anomalyco/opencode/issues/49430

3. **#49452 [OPEN] v2.0.5 `opencode serve` 在未设置认证环境变量时返回 401**
   回环服务器在无凭据环境下仍要求认证并自动生成密码，涉及安全默认策略的澄清，对 headless 用户影响大。
   https://github.com/anomalyco/opencode/issues/49452

4. **#49458 [OPEN] Windows 全局插件路径位于 `C:\Program Files` 下被静默忽略**
   无错误、无日志、无事件，排查成本极高，暴露插件加载的可观测性缺口。
   https://github.com/anomalyco/opencode/issues/49458

5. **#49442 [OPEN] TUI `/open` 列表残留已删除项目，Desktop 打开不存在项目时崩溃**
   生命周期清理问题，一键影响 CLI 与桌面两端体验。
   https://github.com/anomalyco/opencode/issues/49442

6. **#47487 [OPEN] Agent 累积 51 张图片触发 provider 50 图上限，会话彻底卡死**
   read tool 无限累积图片导致会话不可恢复，缺乏自动裁剪/摘要机制，是长会话可靠性的典型案例。
   https://github.com/anomalyco/opencode/issues/47487

7. **#2047 [CLOSED] LM Studio 模型列表无法刷新**（评论 23，👍 7）
   老牌高热度 issue，本地模型用户接入体验的长期痛点，今日关闭。
   https://github.com/anomalyco/opencode/issues/2047

8. **#19515 [CLOSED] [FEATURE] workspace folders — 显式多目录支持**（👍 71）
   最高赞功能需求，附带具体实现提案，今日关闭，多项目/monorepo 用户期待已久。
   https://github.com/anomalyco/opencode/issues/19515

9. **#48447 [OPEN] 任务完成后同一用户消息被重复投递，AI 重复应答**
   会话消息去重/状态机问题，直接影响输出正确性。
   https://github.com/anomalyco/opencode/issues/48447

10. **#49454 [CLOSED] 桌面端归档/删除会话后 tab 残留、历史记录偶发不消失**
    UI 状态与数据不同步的又一例，中文社区反馈活跃。
    https://github.com/anomalyco/opencode/issues/49454

## 四、重要 PR 进展

1. **#49466 feat(server): 新增 `POST /api/fs/write` 端点**（@Hona）
   允许客户端向服务器文件系统写入字节，为附件中转打基础，架构层面值得关注的 server API 扩展。
   https://github.com/anomalyco/opencode/pull/49466

2. **#49467 feat(app): 任意文件附件，不支持的类型以路径方式投递**
   堆叠在 #49466 之上：拖入 `.pptx` 等文件不再报 "Unsupported attachment"，改为传路径让模型用工具打开。显著提升附件体验。
   https://github.com/anomalyco/opencode/pull/49467

3. **#49469 fix(ai): 回滚 #48513 的 effort 切换历史保留**
   修复 2.0.5 中对话中途切换 effort 导致失败的问题，移除 Anthropic/OpenAI 的历史标记逻辑。主动回滚，稳定性优先。
   https://github.com/anomalyco/opencode/pull/49469

4. **#49470 fix(app): 恢复会话摘要状态指示器**
   恢复 server 状态点（healthy/warning/offline 等六态）并补充单测与 E2E。
   https://github.com/anomalyco/opencode/pull/49470

5. **#49444 fix(session): 仅对 Anthropic/Nova 模型保留 Bedrock tool-result 图片**
   修复 Bedrock Converse 不支持其他模型 tool-result 图片导致的请求失败，AWS 用户相关。
   https://github.com/anomalyco/opencode/pull/49444

6. **#49441 fix(core): provider 失败重试提至 10 次，间隔上限 10s，总时长约 84s**
   大幅增强上游抖动下的会话韧性。
   https://github.com/anomalyco/opencode/pull/49441

7. **#49268 fix(desktop): shell 环境探测超时后重试**
   修复登录 shell 环境探测 5 秒超时即放弃的问题，改善远程/慢启动环境。
   https://github.com/anomalyco/opencode/pull/49268

8. **#49453 fix(skill): 斜杠命令调用时重新加载 Skill 磁盘内容**
   修复 Skill 编辑后同进程内调用旧模板的问题。
   https://github.com/anomalyco/opencode/pull/49453

9. **#49317 fix(opencode): 保留响应模型元数据**（接替被自动清理的 #42433）
   保留 AI SDK 结构化模型 ID 而非任意响应头，解决模型显示/路由问题。
   https://github.com/anomalyco/opencode/pull/49317

10. **#47640 feat: Office 文件与 PDF 的离线预览及文本提取**
    功能追赶型大 PR，离线文档预览 + 附件文本提取，与 #49467 的附件生态方向互补。
    https://github.com/anomalyco/opencode/pull/47640

    另有 @iamdavidhill 的桌面 UI 修复系列（#49460 紧凑 tab 图标、#49465 tab 悬停背景、#49459 时间线图标），以及已合并的 #49388（TUI 显示子 agent 显式模型）。

## 五、功能需求趋势

- **多目录 / monorepo 工作区支持**：#19515（👍 71）关闭后，工作区/符号链接相关需求仍是最高呼声方向。
- **附件与文档处理能力**：任意文件投递（#49467）、Office/PDF 预览与提取（#47640），社区对非代码文件的支持需求强烈。
- **桌面端 UI 打磨**：tab 生命周期（#49442、#49454）、项目图标、紧凑模式——桌面端精细化迭代是当前主战场。
- **长会话稳定性**：图片累积限制（#47487）、compaction 死循环（#30443）、消息重复投递（#48447）指向上下文管理需系统性改进。
- **Shell / 远程环境**：SSH 支持（#49409）、shell 环境探测重试（#49268）、Windows Terminal 按键传递（#37473）。

## 六、开发者关注点

1. **可靠性痛点**：工具执行中断（#18757）、会话卡死、provider 重试——核心执行链路的稳定性是第一痛点，官方通过 #49441 等持续加固。
2. **可观测性不足**：插件静默不加载（#49458）、错误只报 "Unexpected server error"（#48372），开发者强烈需要更透明的日志与错误归因。
3. **认证与计费困惑**：Free Tier 报错集中爆发、Zen 付费用户仍被限流且缺乏支持渠道（#37680）——计费/认证体验亟需改善。
4. **第三方网关兼容性**：302.ai 端点失效（#49437）、Kimi schema 深度限制（#25495）、GLM-5.2 cache 掉落（#33998）——自定义 provider 生态的兼容问题长期存在。
5. **V2 架构演进**：`serve` 认证语义（#49452）、重启时前后台 shell 的所有权定义（#36348）等设计讨论显示 2.0 正在收敛核心语义。

---
*数据截至 2026-09-17，来源：github.com/anomalyco/opencode*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-17）

## 1. 今日速览

Qwen Code 今日发布 **v0.24.0 正式版**，包含一项 Breaking Change：命令 hooks 中的项目目录变量改由 bash 展开。社区焦点集中在**上下文 Token 治理**——`roadmap/context-performance` 方向一天内新增多个系统性 Issue（#12028/#12033/#12047 等），核心维护者 @yiliang114 密集拆解非对话上下文的 token 开销问题。此外，**VS Code 远程开发（SSH/Dev Containers）无法连接工作区守护进程**的 P1 问题（#11976、#12023）已确认并关闭。

## 2. 版本发布

- **[v0.24.0](https://github.com/QwenLM/qwen-code/releases)** 正式版
  - ⚠️ **Breaking Change**: `fix(core)!: let bash expand project directory variables in command hooks`（[#11864](https://github.com/QwenLM/qwen-code/pull/11864)，by @qqqys）——命令 hooks 中的项目目录变量现在交由 bash 展开，自定义 hooks 的用户升级需注意行为变化。
- **[v0.24.0-nightly.20260916](https://github.com/QwenLM/qwen-code/releases)**：记录 ACP 边界验收文档（#12024）、CI 导出重试修复等。
- **[v0.23.5-preview.0](https://github.com/QwenLM/qwen-code/releases)**：Windows inode 门控测试修复、CUA Linux 观测数据保留等。

## 3. 社区热点 Issues

1. **[#11976](https://github.com/QwenLM/qwen-code/issues/11976)** (P1, CLOSED) — VS Code Remote (Container) 下 Webview 因动态端口绑定未走 `asExternalUri` 无法连接工作区守护进程。7 条评论，与 #12023（SSH 远程场景）同根因，是近期 IDE 集成最高优先级问题，现已修复关闭。
2. **[#8622](https://github.com/QwenLM/qwen-code/issues/8622)** (P1, CLOSED) — 0.21.6 回归：`PreToolUse`/`PostToolUse`/`PreCompact`/`SessionStart` 等 hooks 从不触发。hooks 系统是自动化工作流的核心，该回归影响面大，社区持续跟进一个月后关闭。
3. **[#12028](https://github.com/QwenLM/qwen-code/issues/12028)** (P2, OPEN) — **非对话上下文 Token 治理追踪 Issue**：系统提示词、内置工具 schema、QWEN.md、技能列表在每次请求都重复付费，长上下文模型上可远超对话本身。今天多个子 Issue 均由此拆出，是当前最活跃的技术方向。
4. **[#12054](https://github.com/QwenLM/qwen-code/issues/12054)** (P2, OPEN) — #12028 的量化拆解：内置工具描述与 schema 占非对话上下文的 **45.9%（约 21,461 tokens）**，且无大小追踪。数据驱动的优化切入点。
5. **[#12027](https://github.com/QwenLM/qwen-code/issues/12027)** (P2, OPEN) — Windows Terminal 长会话中 Ink `getMaxWidth` / yoga 抛 `RangeError: Invalid array length` 直接崩溃 CLI。渲染稳定性在 Windows 上的老大难。
6. **[#12040](https://github.com/QwenLM/qwen-code/issues/12040)** (P2, OPEN) — 安全问题：web-shell 中被拒绝的 `?daemon=` 覆盖仍会把 URL fragment 凭证存到页面 origin 的存储键下，存在凭证错存风险。
7. **[#12047](https://github.com/QwenLM/qwen-code/issues/12047)** (P2, OPEN) — `/context` 从进程级全局单例读取缓存 token 计数，daemon 多会话场景下会“串账”——把别的会话的缓存算到当前会话头上。
8. **[#12053](https://github.com/QwenLM/qwen-code/issues/12053)** (P2, OPEN) — 精简 Goal 运行时：真实会话显示单个 Goal turn（约 100 次工具调用）即可完成目标，后续的证据目录和 checkpoint 属于过度设计，建议按当前 turn 证据判定完成。
9. **[#12012](https://github.com/QwenLM/qwen-code/issues/12012)** (P1, CLOSED) — ACP 自动记忆提取在成功 turn 后因无 cache-safe 参数而失败，并作为未处理 Promise rejection 上报。P1 级稳定性问题已修复。
10. **[#12044](https://github.com/QwenLM/qwen-code/issues/12044)** (P2, OPEN) — `qwen review run --timeout-minutes` 未传播到 review plan 的 deadline，大审查可能被提前硬超时截断。

## 4. 重要 PR 进展

1. **[#12051](https://github.com/QwenLM/qwen-code/pull/12051)** — workflows 中 `agent()` 支持显式工具白名单（只收窄不放宽），增强子代理权限控制。
2. **[#12060](https://github.com/QwenLM/qwen-code/pull/12060)** — Goal 独立验证器改为基于当前 turn 的 transcript 证据判定终止提案，配合 #12053 的运行时精简。
3. **[#12062](https://github.com/QwenLM/qwen-code/pull/12062)** — Stop-hook 连续阻断计数跨工具往返累计，带边界记录与退出条件（#12001 的重开版本）。
4. **[#12049](https://github.com/QwenLM/qwen-code/pull/12049)** — 修复 desktop 打包冒烟测试清理阶段与 daemon 子进程的竞态（对应 #12046）。
5. **[#11965](https://github.com/QwenLM/qwen-code/pull/11965)** — hooks 重载时 `enabled` 状态改按 `name` 键控而非完整身份，修复 #11902（命令变更导致禁用状态丢失）。
6. **[#9357](https://github.com/QwenLM/qwen-code/pull/9357)** (CLOSED/MERGED) — Windows 命令 hooks 向 `cmd.exe` 传递原样参数，修复带引号路径完全失败的问题。长跑 PR 终于落地，与 v0.24.0 hooks 变更相呼应。
7. **[#11538](https://github.com/QwenLM/qwen-code/pull/11538)** — OpenAI 兼容配置支持 per-model `wireApi: chat-completions | responses`，覆盖 CLI/ACP/daemon/Web Shell/VS Code 全链路。
8. **[#12008](https://github.com/QwenLM/qwen-code/pull/12008)** — `qwen serve` 与 Web Shell 支持用户主动停止工作区运行时以释放 ACP 容量。
9. **[#12050](https://github.com/QwenLM/qwen-code/pull/12050)** — `/export md|html|json|jsonl` 输出作为 turn artifacts 在 Web Shell 中可预览/下载，且可回放。
10. **[#9466](https://github.com/QwenLM/qwen-code/pull/9466)** — rewind 映射锚定到稳定 prompt 身份而非位置序号，修复会话恢复/headless 回放下的错位。另有机器人修复 PR 持续推进：[#10455](https://github.com/QwenLM/qwen-code/pull/10455)（只读 HOME 启动崩溃）、[#9305](https://github.com/QwenLM/qwen-code/pull/9305)（VP 模式短内容底部对齐）。

## 5. 功能需求趋势

- **上下文/Token 性能**（最热）：`roadmap/context-performance` 成为新的系统性工程，#12028 衍生出至少 5 个子 Issue，覆盖 token 计量、遥测、系统提示词按需组装（#12032）。
- **IDE 集成**：VS Code Remote/SSH 连接问题集中爆发；置顶 plan/todo 面板（#12056）、权限拒绝附理由（#12055）等体验诉求均来自长期反馈贴 #1895。
- **Hooks/事件系统成熟化**：hooks 回归修复、状态保持、Stop-hook 计数等连续迭代，是该模块的持续打磨期。
- **多代理/Goal/Workflow**：Goal 运行时精简、子代理工具白名单、ACP 容量管理，反映编排层从“功能堆叠”转向“运行时收敛”。
- **桌面端与 Web Shell**：设置持久化（#11955）、凭证安全（#12040）、导出 artifacts 等桌面/Web 体验补齐。

## 6. 开发者关注点

- **Token 成本透明度**是当前最大痛点：用户在长上下文模型上为不可见的固定开销（工具 schema 占近半）持续付费，社区强烈要求计量、归因与按需裁剪。
- **Windows 稳定性**：Ink 渲染崩溃（#12027）、命令 hooks 引号转义（#9357）等问题反复出现，Windows 是质量短板。
- **远程/容器开发**：VS Code Remote 与 Dev Containers 场景的守护进程连接是高优先级回归区。
- **hooks 可靠性与可预期性**：从事件不触发到 `"ask"` 决策被静默拒绝（#6321），hooks 语义与文档一致性仍需收敛。
- **CI 基建健康度**：ECS runner 池过期（#11633）、打包冒烟竞态（#12046）等内部工程问题也被社区可见地追踪，显示项目的工程透明度较高。

---
*数据来源：GitHub QwenLM/qwen-code 公开数据，统计窗口为过去 24 小时。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (Codewhale) 社区动态日报 — 2026-09-17

## 1. 今日速览

今日无新版本发布，但社区活动密集：v0.9.14 的性能优化浪潮基本收官，#6213/#6208 系列热路径优化 PR 批量合入；Shoreline TUI 重设计作为全新安装默认已落地（#6258）；MCP 协议升级至 2025-06-18 修订版并开启对 2026-07-28 rmcp 规范的收敛工作（#6280/#6281）。

## 2. 版本发布

过去 24 小时无新 Release。

## 3. 社区热点 Issues

1. **[EPIC-005] CodeWhale TUI Crate 拆解总览**（#5316，29 评论）— 拆解工作的权威追踪伞形 Issue，执行权已移交 Linear 的 Core execution plan，是最活跃的长期议题。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/5316)

2. **Session picker 拒绝合法保存会话**（#6207，16 评论）— runtime store 存在且校验通过，仍报“属于其他 Runtime host”，直接影响用户恢复会话的核心体验。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6207)

3. **巨型文件拆解：lib.rs 18.7k 行等**（#5586）— v0.9.12 遗留至今的 C09 任务，是解耦 95 万行 tui crate 的关键一步。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/5586)

4. **Fleet 与 Agent 概念重复**（#6036 + 决策记录 #6038）— 创始人亲自确认数据层混淆，最终决策保留两者但统一命名与字段，方向已定、待执行。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6036)

5. **子代理写入争用阻止 N 并行写不相交文件**（#6278）— 最自然的扇出模式被 `coord/ledger.rs` 拒绝，模型因此烧掉大量 token，属于子代理可用性硬伤。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6278)

6. **Resume 后 transcript 为空 + 修复永不持久化**（#6185）— 强退后恢复失败，journal 完好但 repair 结果每次加载都重跑。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6185)

7. **子代理工具结果无上限，单 worker 烧掉 638k token**（#6282）— 读 542KB 文件导致“纯读取饥饿”死亡，需在捕获时加 1 MiB/10k token 上限。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6282)

8. **crate::config 阻塞整个 TUI 拆解**（#6034）— 128 个模块中 118 个构成单一 72.7 万行组件，是架构层面的最大瓶颈。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6034)

9. **MCP 无连接监控，死服务器仍显示 ready**（#6187）— 无自动重连、无 list_changed，仅在下一次调用失败时才暴露。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6187)

10. **菜单导航缺乏统一按键词汇表**（#6290）— 创始人反馈 Fleet 菜单混乱，同一按键在相邻界面行为不同，`menu_style.rs` 已有单源契约可扩展。[链接](https://github.com/Hmbown/DeepSeek-TUI/issues/6290)

## 4. 重要 PR 进展

1. **#6258 [CLOSED] Shoreline TUI 重设计** — 重设计半分支 rebase 到 main（领先 200 commits），成为全新安装默认。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6258)

2. **#6281 [CLOSED] MCP 协议版本协商至 2025-06-18** — 三处 2024-11-05 旧版本 pin 全部更新，为 #6280 的 2026-07-28 rmcp 层铺路。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6281)

3. **#6286 [CLOSED] 修复压缩后聊天角色顺序** — summary 错置于 tool 消息之后导致严格模板拒绝，移至保留 prompt 之前。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6286)

4. **#6273 [CLOSED] 去掉每次防抖保存的三次深拷贝** — #6214 T3：session 历史改为共享，消除两次纯浪费的 clone。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6273)

5. **#6271 [CLOSED] v0.9.14 四个独立切片** — 含 #6213 T4（停止逐 delta 全量重解析参数缓冲）、#6244、#6235 修复。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6271)

6. **#6264 [CLOSED] 五项逐调用重复构建修复（#6208 收口）** — shell/hook/cloud 路径上不变数据的重复工作全部消除。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6264)

7. **#6268 [CLOSED] 修复 main 分支 Lint 红灯** — 四个 continue-on-error 门在 push 时致命导致 0.9.14 发布被阻塞，已修复。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6268)

8. **#6260 [CLOSED] ACP 前缀 reload 幂等化（#6245）** — 短前缀 sessionId 绕过内存快路径导致重复追踪。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6260)

9. **#6262 [CLOSED] app-server stdio thread map 跨桥接重启存活（#6246）** — 配置更新后 bridge 重建不再丢失线程映射。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6262)

10. **#6171/#6288 [CLOSED] 新增 AICraft OpenAI 兼容 provider** — 社区贡献者 @BX166 的模板由维护者代为落地，保留原作者署名。[链接](https://github.com/Hmbown/DeepSeek-TUI/pull/6171)

## 5. 功能需求趋势

- **架构拆解是主旋律**：EPIC-005、C09 巨型文件拆解、crate::config 单体组件（72.7 万行）、ModelRegistry 与 RouteResolver 统一（#4166）、注册表去硬编码（#4173）——占据 Issue 榜大头。
- **子代理/并行编排**：写入争用（#6278）、预算保留被后代消耗（#6277）、工具结果上限（#6282），v0.9.14 的 agent 并行模式正在实战中暴露大量边界问题。
- **性能优化**：#6211–#6214 系列（轮询改 watch/notify、Arc 快照、热路径去重算）本周期大量落地。
- **MCP 现代化**：协议版本协商（#6280/#6281）、连接监控（#6187）、插件 bundle 重复哈希（#6209）。
- **新模型/Provider 生态**：AICraft provider 模板合入；新增 TypeSafe/Jev 作为 key-gated 内置工具的提案（#6292）。
- **UX 一致性**：Shoreline 重设计落地后，菜单导航词汇表统一（#6290）成为新焦点。

## 6. 开发者关注点

- **会话可靠性是最高频痛点**：恢复失败（#6185、#6207、#6174）、steer 回执虚报送达（#6276）——用户对“强退后一切照旧”的期待与现实差距明显。
- **Token 烧费失控**：多个 Issue 反映并行 worker 因争用重试、无上限读取而消耗数十万 token 且零产出，预算/上限机制的缺失直接造成真金白银损失。
- **双状态存储分裂**：session_manager vs StateStore 各自为政（#6144）、app-server 无法独立跑 turn（#6139）、command-contract 半途搁置（#6145），重构债务持续累积。
- **CI/发布链路脆弱**：Lint 红灯一度阻塞 0.9.14 发布（#6268）、telemetry 测试在 Ubuntu 抖动（#6270）。
- **编辑器级体验细节**：Mac 上 key-up 清空长 prompt（#6291）、点击 path:line 启动分离的 $EDITOR（#6235）等终端交互细节持续被报告。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 社区动态日报 · 2026-09-17

## 📰 今日速览

今日无新版本发布，但社区活跃度持续走高：66 条 Issues 更新、19 个 PR 有进展。稳定性成为今日关键词——TUI 渲染崩溃、流中断挂起、compaction 溢出等多个长期痛点获得修复 PR。核心维护者 @mitsuhiko 提交了实验性的 **prompt cache warming** 特性（#9668），值得关注。

---

## 🔥 社区热点 Issues

**1. [#4945](https://github.com/earendil-works/pi/issues/4945) — openai-codex 连接可靠性问题（79 评论 / 👍33）**
最长寿的热点 issue：`gpt-5.5` 交互中 TUI 卡死在 `Working...`，无流式输出、无错误提示，只能 Escape 恢复且会记录为中断回合。79 条评论显示受影响用户面广，仍是 inprogress 状态。

**2. [#8331](https://github.com/earendil-works/pi/issues/8331) — Provider 流中断导致 Agent 循环永久挂起**
Anthropic 529 过载期间，SSE 流停止推送但未关闭，`streamAssistantResponse` 的 `for await` 永久阻塞。这暴露了缺少流超时/心跳机制的架构性短板，与 #4945 属同类问题。

**3. [#9410](https://github.com/earendil-works/pi/issues/9410) — 大会话中按 Escape 中断流导致 TUI 冻结 ~60 秒**
465k token 上下文（gemini-3.8-flash）下中断流，CLI 完全冻结近 1 分钟。大上下文场景的性能问题持续发酵。

**4. [#9602](https://github.com/earendil-works/pi/issues/9602) — Compaction 可能因包含此前未发送的 thinking 消息而溢出**
长会话中早期被省略的 thinking 消息在压缩时被计入，导致上下文反复溢出，是 compaction 子系统的又一深层 bug。

**5. [#9051](https://github.com/earendil-works/pi/issues/9051) — session_compact 自定义消息错过立即重试窗口**
overflow 恢复时压缩消息被排队，重试在缺少恢复上下文的情况下执行，影响扩展生态的 compaction 处理器。

**6. [#8928](https://github.com/earendil-works/pi/issues/8928) — 并行启动时其他 provider 的过期 OAuth 凭据导致 ~48 秒误报 "No API key found"**
作者提供了确定性复现和计时数据，错误指向了错误的凭据源，多进程场景调试成本极高。

**7. [#9255](https://github.com/earendil-works/pi/issues/9255) — 长转录场景 TUI 全屏重绘风暴**
当变更行位于视口上方时几乎每帧触发全量重绘，导致画面剧烈跳动/文本重影，直指差分渲染核心路径。

**8. [#9652](https://github.com/earendil-works/pi/issues/9652)（已关闭）— Claude Fable 拒绝包含 thinking 块转录的压缩请求**
`serializeConversation` 将 thinking 块写入摘要 prompt，触发 Anthropic 的 `reasoning_extraction` 分类器拦截，`/compact` 直接失败。

**9. [#9485](https://github.com/earendil-works/pi/issues/9485) — OpenRouter DeepSeek V4.1 模型目录思考级别配置过期**
`generate-models.ts` 中过期的 pin 导致 `xhigh` 暴露而 `max` 被隐藏，反映静态模型目录维护的持续挑战（同类问题见 #9616 GLM 目录）。

**10. [#9654](https://github.com/earendil-works/pi/issues/9654)（已关闭）— read 工具即使只请求一行也全量读入文件**
128 MiB 文件上请求单行可致内存暴涨崩溃，`offset`/`limit` 应在读取阶段生效而非读取后截取。

---

## 🔧 重要 PR 进展

| PR | 内容 | 状态 |
|---|---|---|
| [#9668](https://github.com/earendil-works/pi/pull/9668) | **feat: prompt cache warming**（@mitsuhiko）实验性缓存保温支持，WIP | 🟡 OPEN |
| [#9692](https://github.com/earendil-works/pi/pull/9692) | **fix(tui)**: 单行超出终端宽度导致整个会话崩溃 → 改为裁剪，修复 #9691 | ✅ 已合入 |
| [#9662](https://github.com/earendil-works/pi/pull/9662) | **fix: user bash hook 抛错时 fail closed**，不再静默回退本地 shell（含破坏性变更文档） | ✅ 已合入 |
| [#9677](https://github.com/earendil-works/pi/pull/9677) | **fix: compaction 队列回滚重放已接受消息**的问题，修复 AgentSession 结算 bug（关联 #5886） | ✅ 已合入 |
| [#9548](https://github.com/earendil-works/pi/pull/9548) | **feat: 会话中系统消息**——system prompt/工具变更写入 transcript，恢复与分支导航时可还原状态 | ✅ 已合入 |
| [#9682](https://github.com/earendil-works/pi/pull/9682) | **fix(clipboard)**: macOS pbcopy 回退时非 ASCII 文本被转为 MacRoman 乱码 | ✅ 已合入 |
| [#9601](https://github.com/earendil-works/pi/pull/9601) | **fix: 精确 session ID 免除全量 transcript 扫描**，4K+ transcripts 场景 16s → 亚秒级（修复 #9440） | ✅ 已合入 |
| [#9655](https://github.com/earendil-works/pi/pull/9655) | **fix(tui)**: Windows ConPTY 下鼠标追踪序列需在 raw mode 之后发送 | ✅ 已合入 |
| [#8635](https://github.com/earendil-works/pi/pull/8635) | **fix(ai)**: 懒加载 setup 期间保留 aborted stop reason（修复 #8409） | 🟡 OPEN |
| [#9570](https://github.com/earendil-works/pi/pull/9570) | **fix(ai)**: 映射 Gemini `TOO_MANY_TOOL_CALLS` 为错误 stop reason，避免未处理异常 | 🟡 OPEN |

其他值得留意：[#9434](https://github.com/earendil-works/pi/pull/9434)（扩展追加 system prompt）、[#9301](https://github.com/earendil-works/pi/pull/9301)（设备码登录浏览器/剪贴板确认）持续讨论中。

---

## 📈 功能需求趋势

1. **稳定性与容错**（最强烈）：流中断挂起（#4945/#8331）、错误重试分类（#9585）、NaN Retry-After（#9689）——社区对“永不挂起”的核心诉求突出。
2. **Compaction 子系统**：#9051、#9602、#9652、#9216 集中爆发，自动压缩的边界情况成为当前最大 bug 聚集地。
3. **扩展 API 开放**：暴露 ModelRuntime（#8791，👍5）、session 替换 API（#5952）、OAuth HTML 渲染函数公开（#6930）、system prompt 追加（PR #9434）。
4. **模型目录时效性**：DeepSeek（#9485）、GLM（#9616）、Claude fallback 列表（#9294）——静态 catalog 跟不上上游变化的矛盾反复出现。
5. **大上下文性能**：465k token 冻结（#9410）、重绘风暴（#9255）、transcript 扫描（#9440）。

---

## ⚠️ 开发者关注点

- **本地/开源模型体验仍有缺口**：Ollama qwen3.8 的 0.84→0.85 回归（#9216）、llama.cpp 下的 thinking 溢出（#9602）。
- **Windows 平台质量**：bash 超时管道进程残留（#9129）、ConPTY 鼠标序列（PR #9655）、路径分隔符（PR #9693）——本周多个 Windows 专项修复。
- **多进程/SDK 场景**：并行启动凭据误报（#8928）、OpenCode Zen session ID 兼容（#9690）、`--session-id` 性能（#9440）表明 Pi 被越来越多地嵌入自动化管线。
- **内存安全**：read 工具全量读取（#9654）提示大文件处理需流式化。

**建议**：使用 Claude Fable + `/compact` 或大会话中断流的用户请关注 0.85.x 后续补丁；扩展开发者可提前关注 PR #9548（transcript 化系统消息）带来的行为变化。

</details>

<details>
<summary><strong>oh-my-pi</strong> — <a href="https://github.com/can1357/oh-my-pi">can1357/oh-my-pi</a></summary>

# oh-my-pi 社区动态日报 · 2026-09-17

## 一、今日速览

oh-my-pi 连发 v18.2.2 与 v18.2.3 两个版本，重点增强 pi-ai 流式能力与 Amazon Bedrock 自定义端点支持。社区热点仍集中在 **google-antigravity 假 429 错误**（多条重复 issue 表明该问题影响面广）以及 TUI 长回复流式渲染问题。今日还有多个高质量 PR 更新，涉及 worker 进程治理、MCP 工具过滤与安全修复。

---

## 二、版本发布

### [v18.2.3](https://github.com/can1357/oh-my-pi/releases)
- **pi-ai**：`stream()` / `streamSimple()` 支持每次请求尝试的异步模型 header 解析，覆盖认证重试与取消场景；Provider 登录提示支持 `secret: true` 掩码输入
- **pi-catalog**：新增 Mod

### [v18.2.2](https://github.com/can1357/oh-my-pi/releases)
- **pi-ai**：`bedrock-converse-stream` 请求支持可配置 `baseUrl`，可使用 VPC/PrivateLink 端点、FIPS 主机及内部网关（含路径挂载端点）。回应了社区对 Bedrock 企业化部署的长期需求（见 [#1990](https://github.com/can1357/oh-my-pi/issues/1990)）

---

## 三、社区热点 Issues

1. **[#1666](https://github.com/can1357/oh-my-pi/issues/1666)** 新增 command-code 作为模型 provider（31 评论 / 👍8）
   长期开放的 provider 接入请求，用户希望复用 commandcode.ai 订阅额度，代表社区对订阅制 provider 的持续需求。

2. **[#11699](https://github.com/can1357/oh-my-pi/issues/11699)** Google Antigravity 假 429 RESOURCE_EXHAUSTED（23 评论）
   系统提示中 `<system-conventions>` 标签导致 Cloud Code Assist API 首轮即报 429，与 [#11963](https://github.com/can1357/oh-my-pi/issues/11963)（未发送 paidTier）、[#11883](https://github.com/can1357/oh-my-pi/issues/11883) 同属一个故障簇，是当前 antigravity 用户最大痛点。

3. **[#9780](https://github.com/can1357/oh-my-pi/issues/9780)** TUI 长流式回复渲染错位（20 评论）
   流式过程中早前文本会在输入框/工具卡片下“移动”，结束后才复位。与已关闭的 [#11276](https://github.com/can1357/oh-my-pi/issues/11276) 症状相同，是 TUI 体验的核心遗留问题。

4. **[#10781](https://github.com/can1357/oh-my-pi/issues/10781)** antigravity 子代理 100% 崩溃（17 评论）
   `TypeError: rt.getWorkPoolYieldItems` 在 spawn 前即崩溃，[#10915](https://github.com/can1357/oh-my-pi/issues/10915) 显示 scout agent 也受影响。

5. **[#4218](https://github.com/can1357/oh-my-pi/issues/4218)** Devin 流错误中断会话（14 评论，prio:p1）
   `invalid_argument` 中途终止 session，高优先级但长期未解。

6. **[#11508](https://github.com/can1357/oh-my-pi/issues/11508)** 请求收录 DeepSeek V4.1 Flash（13 评论 / 👍10）
   新模型发布 5 天后 catalog 缺失且分类法无法识别，点赞数高，反映社区对新模型快速跟进的期望。

7. **[#7982](https://github.com/can1357/oh-my-pi/issues/7982)** 按次 task 调用指定模型（13 评论）
   需要安全地为单个 task/agent() 调用覆盖模型而不污染 agent 文件配置，多 agent 工作流的核心能力缺口。

8. **[#3189](https://github.com/can1357/oh-my-pi/issues/3189)** 按仓库稳定标识划分项目记忆（12 评论）
   当前记忆以目录 basename 为 key，worktree/fork/重命名都会导致记忆碎片化，设计层面的改进诉求。

9. **[#11362](https://github.com/can1357/oh-my-pi/issues/11362)** Marketplace 插件 agents/ 不被发现的隐藏门槛（9 评论，昨日更新）
   `enabledProviders: ["claude-plugins"]` 这一未记录的二次门控让插件安装后静默失效，影响插件生态信任度。

10. **[#10937](https://github.com/can1357/oh-my-pi/issues/10937)** openai-codex 服务端压缩长时间重试无反馈（8 评论）
    V2 abort + V1 404 后每 3 分钟重试数分钟，TUI 仅显示"Auto server compaction"且无重试详情，长会话可用性问题。

> 另值得注意：[#12166](https://github.com/can1357/oh-my-pi/issues/12166)（已关闭）确认 Gemini 3.8 Flash 近 24h 严重降速为上游 Google 问题，非 OMP 缺陷。

---

## 四、重要 PR 进展

1. **[#12308](https://github.com/can1357/oh-my-pi/pull/12308)** worker 空闲 TTL 回收与活动看门狗重置
   为 `__omp_worker_*` 子进程增加空闲超时销毁，防止孤儿进程持续占用 CPU。今日新开。

2. **[#10875](https://github.com/can1357/oh-my-pi/pull/10875)** MCP 按服务器 enabledTools/disabledTools 工具过滤
   picomatch 通配过滤，补齐 Copilot/Claude/OpenCode 同等能力，减少模型上下文污染。

3. **[#12096](https://github.com/can1357/oh-my-pi/pull/12096)** 限制 patch 路径于 worktree 内并拒绝 .git 目录
   修复符号链接逃逸与 git store 可写的安全隐患，重要的安全加固。

4. **[#12304](https://github.com/can1357/oh-my-pi/pull/12304)** 修正 kimi-code (K2.8 Preview) effort 阶梯
   旧 compat 残留将 thinking 阶梯错误压缩为四档，现按动态 catalog 声明展示。今日新开。

5. **[#12103](https://github.com/can1357/oh-my-pi/pull/12103)** 按模型的角色路由与自定义预设
   自动为不同默认模型匹配合适的角色模型（标题、总结等用小模型），应对频繁切换 provider 的场景。

6. **[#7560](https://github.com/can1357/oh-my-pi/pull/7560)** 嵌套 isolation 需显式 `task.isolation.allowNested`
   防止意外产生双层隔离 worktree（review:p1），架构层面的正确性修复。

7. **[#12292](https://github.com/can1357/oh-my-pi/pull/12292)** GitHub 凭证按子操作范围注入
   用类型化 authority 替代 shell 推断，token 仅注入到请求的操作中，凭证安全收敛。

8. **[#8683](https://github.com/can1357/oh-my-pi/pull/8683)** 会话级工具审批选项
   支持"本会话批准该工具 / 批准相似命令"，减少审批疲劳，直接改善日常使用体验。

9. **[#12161](https://github.com/can1357/oh-my-pi/pull/12161)** sharpshooter 可与 memory backend 并存
   改为旁路运行而非替换记忆后端，架构更灵活。

10. **[#12230](https://github.com/can1357/oh-my-pi/pull/12230)** 原生 Code Cat 状态栏宠物
    将社区流行的猫状态栏转为 `pets` 开关的原生功能，趣味性功能进主干。

---

## 五、功能需求趋势

- **Provider 生态扩张**：command-code 接入（#1666）、DeepSeek V4.1 Flash 收录（#11508）、Bedrock 自定义端点（#1990，已在 v18.2.2 部分落地）、AnySearch/Serply 搜索 provider PR——接入更多模型与搜索渠道是最持续的诉求。
- **google-antigravity 可用性**：429 假报错、paidTier 缺失、子代理崩溃形成故障簇，是当前最集中的 bug 报告来源。
- **TUI 渲染与性能**：长流式回复错位（#9780）、/resume 卡顿（#8486）、流式掉帧（#10955）。
- **多 Agent / 子代理控制**：按次指定模型（#7982）、嵌套隔离门控、子代理技能可见性、spawn 崩溃修复。
- **企业化部署**：Bedrock VPC/FIPS、Vertex 代理兼容（#4060）、凭证与 auth-gateway 治理。
- **记忆系统**：按仓库稳定身份划分（#3189）、多 backend 并存（PR #12161）。
- **插件与扩展机制**：marketplace 安装静默失败（#11362、#3244）、扩展生命周期与身份 API。

---

## 六、开发者关注点

1. **流式重试与认证健壮性**：v18.2.3 的异步 header 解析是对认证重试场景的直接回应；但 openai-codex 压缩重试无反馈（#10937）、Anthropic 凭证封锁不自动恢复（#10978）表明失败恢复路径仍有盲区。
2. **资源生命周期泄漏**：worker 孤儿进程（PR #12308）、eval kernel 未确认关闭即泄漏（#7714）、browser-relay 调试器附件泄漏（PR #9009）——进程/附件回收是反复出现的主题。
3. **配置可发现性差**：多个 issue 源于未记录的隐藏门槛（插件 agents/ 发现、models.yml 能力边界），文档与实际行为脱节。
4. **长会话稳定性**：服务端压缩失败循环、Eval 内核变量丢失（#10987）、resume 长会话卡顿，重度用户的长会话体验是留存关键。
5. **上游依赖波动**：Google 上游降速、DeepSeek 新模型发布节奏，要求 catalog 分类法具备更快适配能力。

---

*数据来源：GitHub can1357/oh-my-pi（Issues 117 条 / PRs 155 条，过去 24 小时更新）*

</details>

<details>
<summary><strong>DeepSeek Harness</strong> — <a href="https://github.com/deepseek-ai/deepseek-harness">deepseek-ai/deepseek-harness</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*