# AI CLI 工具社区动态日报 2026-09-16

> 生成时间: 2026-09-16 03:55 UTC | 覆盖工具: 11 个

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
**数据窗口：2026-09-16**

---

## 1. 生态全景

AI CLI 工具已从“终端聊天助手”全面演进为**多形态 Agent 工作台**：CLI、TUI、VS Code 扩展、桌面端、Web 端并行发展，各头部工具均在构建自己的 runtime/daemon 架构（Codex 托管 daemon、DeepSeek Harness runtime API、Qwen serve/ACP、OpenCode app-server）。生态竞争焦点正从功能堆叠转向**可靠性、安全边界与成本透明度**——数据丢失事故、静默失败、配额计费问题成为各社区最高热度的痛点。同时 MCP、沙箱、headless/CI 集成已成为事实上的基础设施标配。

---

## 2. 各工具活跃度对比

| 工具 | 24h Issue 更新 | 24h PR 更新 | Release 情况 |
|---|---|---|---|
| Claude Code | 10+ 热点活跃 | 2 | v2.1.273 |
| OpenAI Codex | 10+ 热点活跃 | 10+（密集合入） | 3 个 alpha（0.155.0-a7/8/9） |
| Gemini CLI | 10+ 热点活跃 | 10+ | 3 个（nightly + preview + v0.60.0 稳定） |
| Copilot CLI | 10+ 热点活跃 | 0 | v1.0.85 + v1.0.84-9 |
| Kimi Code CLI | 2 | 0 | 无 |
| OpenCode | 50 | 50 | 无 |
| Qwen Code | 10+ 热点活跃 | 10+ | cua-driver-rs v0.20.9 |
| DeepSeek TUI | 50 | 21 | 无 |
| Pi | 158 | 15 | 无 |
| oh-my-pi | 183 | 397 | v18.2.1 / v18.2.0 |

**解读**：oh-my-pi、Pi 等社区驱动项目 Issue/PR 量级最高（数百条/日），Claude Code、Codex、Gemini CLI 热度稳定但官方主导；Kimi CLI 与 DeepSeek Harness 今日近乎静默。发布节奏上 Codex（连发 3 alpha）与 Gemini（多通道并行）最快。

---

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **破坏性操作防护 / 数据安全** | Claude Code（#92737 rm -rf 误删照片、#93408 清空主目录）、Codex（#43998 删源码、#42480 删生产库）、Gemini CLI（#22672 git force 防护）、OpenCode（#48468 误删 git 仓库）、DeepSeek TUI（#6251 会话级授权收窄） | Agent 执行 rm/git reset 前缺少验证；ask 规则不可靠拦截；审批 UI 甚至无法核对内容（Qwen #11966 工具块渲染为空） |
| **静默失败 / fail loudly** | Gemini CLI（#22323 subagent 误报 success）、DeepSeek TUI（#6184 引擎冻结无日志）、oh-my-pi（多处错误被吞）、Pi（#9577 信号杀死仍报成功）、OpenCode（#48447 消息重复投递） | “报错比假装成功好”是各社区一致共识 |
| **会话恢复与长任务连续性** | Codex（daemon 重启恢复 #45820、follow-up 丢失 #45019）、DeepSeek TUI（#6207/#6225 resume 失败）、Copilot CLI（OOM 无法恢复，7+ 条 Issue）、DeepSeek Harness（归档会话恢复）、oh-my-pi（`promote_queued_message`） | resume 可靠性、消息排队不打断、断点恢复是刚需 |
| **上下文/Compaction 管理** | Claude Code（v2.1.273 压缩监控头）、Pi（#8061 预算溢出、#9652 压缩被拒）、oh-my-pi（#11961 缓存前缀重写 580K token）、Qwen（#11969 压缩空摘要） | 压缩链路可靠性 + 缓存成本优化 |
| **计费/配额透明度** | Codex（#41220 元 Issue、容量错误集群）、Kimi CLI（#2626 cache 计费疑似放大 10 倍）、oh-my-pi（#11938 缓存抖动诊断、#12171 额度显示）、Pi（#6881 实际计费） | 付费用户要求可预测、可审计的消耗模型 |
| **Windows / WSL 支持** | Claude Code（AppX 容器锁，190 评论老问题）、Codex（#41290 WSL、沙箱策略重构）、Pi（#9361 shell 解析）、Qwen（#11952 签名）、Copilot CLI（#1148 CRLF） | Windows 均为二等公民，各项目集中投入 |
| **多 provider / 网关兼容** | Qwen（#11956 序列化 null、#11538 wire API 选择）、Pi（#9444 thoughtSignature 丢失）、OpenCode（多 provider 流式问题）、oh-my-pi（upstreamModel 透传） | OpenAI 兼容网关互操作是扩展生态关键 |

---

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线特点 |
|---|---|---|---|
| **Claude Code** | 全表面覆盖（TUI/VS Code/Desktop/Mobile），企业网关可观测 | 企业 + 专业开发者 | 闭源单模型（Anthropic），新版本发力网关头、沙箱、Cowork |
| **OpenAI Codex** | TUI 打磨 + Windows 一等公民 + 可视化（Mermaid 渲染） | 订阅制付费用户 | Rust 重写，托管 daemon 架构，alpha 快速迭代 |
| **Gemini CLI** | 安全加固 + AST 感知工具链 + Skills/Memory 体系 | 开发者 + 企业 | 开源（Apache），依托 Gemini 3 原生 bash 能力做零依赖沙箱 |
| **Copilot CLI** | VS Code 生态一体化、模态编辑（Vim 全量开放） | GitHub 生态开发者 | Node/V8，深度绑定 VS Code 配置体系 |
| **Kimi CLI** | 轻量，社区静默 | 国内用户 | 反馈渠道缺失，产品线 tracker 未整合 |
| **OpenCode** | 插件/扩展 API + 多 provider 中立 | provider 无关的高级用户 | 开源中立聚合器，插件生态是核心主线 |
| **Qwen Code** | Web Shell / 嵌入式宿主 / CUA 驱动 | 多形态宿主集成方 | serve/ACP 双平面架构，OpenAI 兼容生态互操作 |
| **DeepSeek TUI** | 编辑安全门禁（ast-grep/syn parse-gate）+ GPUI 桌面 | 追求写安全的重度用户 | Rust，写入前语法校验是独特防御纵深 |
| **Pi / oh-my-pi** | 架构级上下文管理（mid-conversation system messages）、多模型编排 | Hacker / 重度自定义用户 | 开源、社区驱动，Mitsuhiko 等核心开发者主导架构演进 |

---

## 5. 社区热度与成熟度

- **成熟稳定型**：Claude Code、Copilot CLI、Gemini CLI —— 问题多为基础体验顽疾（更新机制、OOM、复制粘贴），功能面完整，进入打磨期。
- **快速迭代型**：Codex（1 天 3 alpha + 10 个 PR 合入）、DeepSeek TUI（50 Issue/21 PR，v0.9.14 里程碑密集推进）、oh-my-pi（397 条 PR 更新，社区贡献极活跃）。
- **高活跃开源社区**：Pi（158 Issue 更新）报告质量高（含确定性复现与计时数据），社区工程素养突出。
- **早期/低活跃**：DeepSeek Harness（alpha 阶段，靠版本功能而非社区讨论驱动）、Kimi CLI（近乎停滞，官方响应待提升）。

**值得肯定**：OpenCode、oh-my-pi、DeepSeek TUI 的维护者响应速度极快，多数回归当日修复关闭。

---

## 6. 值得关注的趋势信号

1. **“Agent 安全”从口号进入工程化**：DeepSeek TUI 的写入前语法门禁、oh-my-pi 的 artifact 生产者隔离 + fail-closed、Codex 的插件安装权限收紧（#45806）表明行业正从“提示词劝阻”转向**结构性防御**（parse-gate、授权作用域、操作粒度审批）。选型时应将破坏性操作防护机制作为硬指标。

2. **静默失败是全行业信任杀手**：至少 5 个工具社区独立提出同一诉求。对开发者的启示：任何 Agent 编排层都应实现状态真实上报与错误显式传播，这是比功能更优先的工程项。

3. **成本可观测性成为付费决策因素**：Kimi（计费疑似放大 10 倍）、Codex（配额异常元 Issue）、oh-my-pi（缓存抖动诊断）显示 token 消耗审计正成为产品能力。企业选型建议优先支持 gateway 侧监控的方案（如 Claude Code v2.1.273 的网关提示头）。

4. **架构收敛于“本地 daemon + 多表面客户端”**：Codex、Qwen、OpenCode、DeepSeek 均在建设 app-server/runtime API，预示 CLI 工具正演变为**本地 Agent 平台**，CLI 只是宿主之一。插件/扩展 API 的成熟度将是下一轮竞争分水岭。

5. **对开发者的即时建议**：所有工具的破坏性命令防护均不可完全信赖——在高风险目录禁用 auto/yolo 模式、配置 deny 规则、维护快照/备份，仍是从业者的必要自救措施。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告
（数据截止 2026-09-16，来源：github.com/anthropics/skills）

> 说明：本期 PR 评论数据缺失，以下排名综合 PR 活跃度、关联 Issue 讨论热度和更新时间推断。

---

## 一、热门 Skills 排行（PR）

| # | Skill / PR | 功能 | 讨论热点 | 状态 |
|---|---|---|---|---|
| 1 | **skill-creator 触发评估修复**（[PR #1298](https://github.com/anthropics/skills/pull/1298)） | 修复触发评估误报、Windows `select()` 失败、运行时错误被误判为非触发 | skill-creator 是官方最核心的元技能，其评估管线 bug 是社区长期痛点（关联 Issue #556、#1721） | OPEN |
| 2 | **触发检测 0% recall 修复**（[PR #1769](https://github.com/anthropics/skills/pull/1769)） | 修复所有 skill 一律报告 `precision=100% recall=0%` 的问题，阻止基于错误证据优化描述 | 修复 [#1721](https://github.com/anthropics/skills/issues/1721)，是 skill 质量评估可信度的关键修复 | OPEN（近期活跃） |
| 3 | **mcp-builder 系列修复**（[PR #1742](https://github.com/anthropics/skills/pull/1742)、[#1602](https://github.com/anthropics/skills/pull/1602)、[#1724](https://github.com/anthropics/skills/pull/1724)） | 支持 mcp>=2 API 重命名、修复评估序列化导致 0/N 评分、更新默认模型至 claude-sonnet-5 | 关联高热度 Issue [#1390](https://github.com/anthropics/skills/issues/1390)（评估对真实 MCP 服务器全失败），mcp-builder 是 MCP 集成事实标准 | OPEN |
| 4 | **md2video-audio**（[PR #1703](https://github.com/anthropics/skills/pull/1703)） | 零成本将 Markdown 编译为带真人配音的 MP4 视频（Marp 转幻灯片） | "零成本内容生产"方向的新晋热门贡献 | OPEN |
| 5 | **document-typography**（[PR #514](https://github.com/anthropics/skills/pull/514)） | AI 生成文档的排版质控（孤行、寡段、编号错位） | 定位独到："用户不会主动要求好排版，但每个文档都受影响" | OPEN（3月提交，挂起较久） |
| 6 | **Hivemind 多智能体编排**（[PR #1628](https://github.com/anthropics/skills/pull/1628)） | Claude Code 作为 planner/reviewer，将机械工作委派给运行免费模型的 headless opencode worker | 呼应社区对"节省昂贵模型上下文"的强烈诉求 | OPEN |
| 7 | **pyxel 复古游戏开发**（[PR #525](https://github.com/anthropics/skills/pull/1703)→[#525](https://github.com/anthropics/skills/pull/525)） | Python 复古游戏的创建、确定性无头运行与帧级验证 | 作者为 Pyxel 原作者 kitao，权威性强，9月仍活跃更新 | OPEN |
| 8 | **skill-quality / security-analyzer 元技能**（[PR #83](https://github.com/anthropics/skills/pull/83)） | 对 Skill 本身做五维质量评估与安全审计 | 与信任边界安全议题（Issue #492）高度相关 | OPEN |

---

## 二、社区需求趋势（Issues 提炼）

1. **安全与信任边界**：[Issue #492](https://github.com/anthropics/skills/issues/492)（43 评论，最热）——社区 skill 冒用 `anthropic/` 命名空间，用户可能在误信下授予高权限。结合 [#1175](https://github.com/anthropics/skills/issues/1175)（SharePoint 权限控制写入 SKILL.md 的安全顾虑），**Skill 分发安全是第一大诉求**。
2. **组织级分发与共享**：[Issue #228](https://github.com/anthropics/skills/issues/228)（16 评论）——组织内共享 skill 库、直接分享链接，替代 Slack 传文件的原始方式。
3. **上下文效率**：[#1487](https://github.com/anthropics/skills/issues/1487)（claude-api skill 单次注入 156k token）、[#1329](https://github.com/anthropics/skills/issues/1329)（compact-memory 符号化压缩 agent 状态）——skill 的"轻量按需加载"是普遍期待。
4. **Agent 治理与质量门禁**：[#412](https://github.com/anthropics/skills/issues/412)（agent-governance）、[#1385](https://github.com/anthropics/skills/issues/1385)（三段式推理质量门禁管线）。
5. **互操作与平台支持**：[#16](https://github.com/anthropics/skills/issues/16)（Skills 暴露为 MCP）、[#29](https://github.com/anthropics/skills/issues/29)（Bedrock 支持）。
6. **文档/办公技能稳定性**：docx/pdf 的 ID 冲突（[PR #541](https://github.com/anthropics/skills/pull/541)）、大小写引用（[PR #538](https://github.com/anthropics/skills/pull/538)）、UTF-8 编码（[PR #1765](https://github.com/anthropics/skills/pull/1765)）持续有修复需求。

---

## 三、高潜力待合并 Skills（活跃 OPEN PR）

- [PR #1769](https://github.com/anthropics/skills/pull/1769) — trigger detection recall 修复，9/14 创建次日即更新，修复高优先级 bug，**最可能近期合并**
- [PR #1742](https://github.com/anthropics/skills/pull/1742) — mcp-builder 兼容 mcp>=2，修复已确认的 Issue #1668
- [PR #1765](https://github.com/anthropics/skills/pull/1765) — office redlining UTF-8 修复，含波兰语验证，修复 Issue #1707
- [PR #1703](https://github.com/anthropics/skills/pull/1703) — md2video-audio，9 月活跃
- [PR #1602](https://github.com/anthropics/skills/pull/1602) — 跨平台评估/编码/指标综合修复（mcp-builder 相关）
- [PR #525](https://github.com/anthropics/skills/pull/525) — pyxel skill，9/15 仍有更新，维护意愿强

---

## 四、生态洞察（一句话）

**社区最集中的诉求是：让 Skills 的"触发—评估—分发"基础设施变得可信且安全——即 skill 能被正确触发、评估分数真实可信、命名空间与权限边界清晰，其次才是更多新技能本身。**

---

# Claude Code 社区动态日报 · 2026-09-16

## 1. 今日速览

Claude Code 发布 **v2.1.273**，主要为 LLM 网关新增多个请求提示头（opt-in），面向企业网关观测场景。社区方面，**Windows 桌面版自动更新机制**成为持续焦点：孤进程文件锁、强制重启、远程控制桥接丢失等多个高热度问题在今日继续活跃。此外出现多起**数据丢失级高危 Bug**（`rm -rf` 误删、macOS 主目录被清空），值得所有用户警惕。

---

## 2. 版本发布

### v2.1.273
- 新增面向 LLM 网关的请求头：`x-claude-code-request-class`、`x-claude-code-agent-type`、`x-claude-code-prev-tool-durations`、`x-claude-code-compaction`、`x-claude-code-context-compacted`
- 通过 `CLAUDE_CODE_GATEWAY_HINT_HEADERS=1` 显式开启，方便网关侧做请求分类、上下文压缩监控与降级路由

---

## 3. 社区热点 Issues（Top 10）

| # | Issue | 关注理由 |
|---|-------|---------|
| 1 | [#89680](https://github.com/anthropics/claude-code/issues/89680) Windows 静默更新残留旧 AppX 容器，新版本启动失败 (0x80070020) | 与 #73107 同根源，"stealth update" 无提示且需重启才能恢复，Windows 用户核心痛点 |
| 2 | [#73107](https://github.com/anthropics/claude-code/issues/73107) 升级后孤进程钉住旧版 AppX 容器导致无法启动 | 190 评论的 #42776 即此类问题，有完整复现，诊断深入到 job-object 层 |
| 3 | [#92737](https://github.com/anthropics/claude-code/issues/92737) **高危数据丢失**：`rm -rf` 删除用户不可替代的个人照片 | 标记 high-priority / data-loss，Agent 未验证移动成功即删除源文件 |
| 4 | [#93408](https://github.com/anthropics/claude-code/issues/93408) **高危**：桌面版清空 macOS 主目录（含钥匙串） | 同为 data-loss 标签，涉及沙箱权限边界，安全敏感 |
| 5 | [#93683](https://github.com/anthropics/claude-code/issues/93683) 每个工具结果注入隐藏指令且无法关闭 | 透明度问题：注入指令覆盖用户显式配置，社区对不可控 system-level 注入敏感 |
| 6 | [#81472](https://github.com/anthropics/claude-code/issues/81472) 复制/粘贴跨端损坏 Meta issue（聚合 42 个子问题） | 长期存在的全表面（TUI/VS Code/Desktop）体验顽疾，今日继续有讨论 |
| 7 | [#92246](https://github.com/anthropics/claude-code/issues/92246) Windows 桌面 9 天内 9 次强制自更新中断会话 | 无提示、无推迟选项，直接破坏长时间运行的任务，与 #94049（更新丢失 Remote Control 桥接）呼应 |
| 8 | [#24726](https://github.com/anthropics/claude-code/issues/24726) VS Code 扩展：请求关闭“自动附加打开文件/选区” | 242 👍，VS Code 上下文自动注入是长期高票需求 |
| 9 | [#36151](https://github.com/anthropics/claude-code/issues/36151) Claude Mobile 多账号切换（726 👍） | 社区呼声最高的功能需求之一，182 条评论持续发酵 |
| 10 | [#94640](https://github.com/anthropics/claude-code/issues/94640) Cowork 沙箱代理对默认白名单域名返回 403 | 沙箱网络出站规则回归性故障（9 月初起），影响 Playwright 等工具链 |

---

## 4. 重要 PR 进展

过去 24 小时仅 2 个 PR 更新（均为官方成员 @poteat 的 diff 模块）：

1. **[#94653](https://github.com/anthropics/claude-code/pull/94653)**（Open）：修复 `mods/diff` 在首次编辑时无条件打开面板的问题——此前只要终端宽于 144 列就触发，与布局是否能停靠无关；现仅在布局实际可停靠时打开。
2. **[#94594](https://github.com/anthropics/claude-code/pull/94594)**（Closed）：调整 `mods/diff` 的 git 调用时机，不再在 `session.start` 钩子中同步执行全仓库 `git status`，避免大仓库下阻塞首条提示；改为与内置面板相同的触发时机。

---

## 5. 功能需求趋势

- **桌面端更新控制权**：请求可配置/可推迟的更新策略（#92246、#94049、#89680），Windows 尤甚
- **会话管理**：跨平台列举运行中会话及其状态（#94620）、`claude://resume` 去重与聚焦已有标签页（#80773）、VS Code 会话删除能力（#91945）、消息排队而非打断任务（#30677）
- **IDE 上下文控制**：关闭 VS Code 自动附加文件/选区（#24726，242 👍）
- **多账号**：Mobile 端多账号切换（#36151，726 👍）
- **沙箱/网络可观测性**：本次 v2.1.273 的网关提示头与 #94640、#94639（校验和与 entitlements 披露）反映社区对安全可审计性的诉求
- **本地化**：中文语音听写支持（#78728）

---

## 6. 开发者关注点（痛点总结）

1. **数据安全是最大风险**：多起 data-loss 级报告（#92737、#93408、#80868 生产库被清空）表明 Agent 执行破坏性命令前的验证机制不足，auto 模式 + ask 规则未可靠拦截。建议在高风险目录禁用 auto 模式、配置 deny 规则并做快照。
2. **Windows 桌面更新链路脆弱**：孤进程 + AppX 容器锁定是长期未解的系统性问题（#42776 累计 190 评论），遇 0x80070020 目前只能重启。
3. **隐藏行为损害信任**：工具结果中注入不可关闭的指令（#93683）与未公开校验和的 `.app` bundle（#94639）引发透明度质疑。
4. **更新破坏本地状态**：桌面更新清空本地定时任务与会话列表（#94628）、丢失 Remote Control 桥接（#94049），建议关键任务前自行备份。
5. **基础体验仍待打磨**：复制/粘贴（42 个子 issue）、VS Code 会话重命名回归（#94349）等长期问题悬而未决。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-16

## 1. 今日速览

今日 Codex 发布了 **rust-v0.155.0-alpha.7/8/9** 三个 alpha 版本，迭代节奏密集。Issues 中 "Selected model is at capacity" 相关的容量/配额问题持续发酵，多个新报告（#45832、#45835、#45648）今日集中涌现。PR 方面，TUI 体验（会话级模型切换、就地编辑历史 prompt）、Windows 沙箱策略和托管 daemon 恢复机制成为开发重点。

## 2. 版本发布

- **rust-v0.155.0-alpha.9 / alpha.8 / alpha.7**（24小时内连续发布）：0.155.0 预发布版本快速迭代，尚未附详细 changelog，推测包含今日合入的 TUI 与 Windows 沙箱相关改动。
  - 链接：[rust-v0.155.0-alpha.9](https://github.com/openai/codex/releases/tag/rust-v0.155.0-alpha.9)

## 3. 社区热点 Issues

1. **#41290 [OPEN]** — Windows WSL 环境下项目创建/删除失败（70 评论 / 51 👍）。高订阅用户长期受困，是最受关注的 Windows 适配问题。今日相关修复 PR #45837、#45811 已合入，值得观察是否解决。
   https://github.com/openai/codex/issues/41290

2. **#28507 [OPEN]** — "Selected model is at capacity" 持续报错（54 评论 / 51 👍）。Pro 5x 用户报告模型容量问题，与今日多个新报错共同构成最大痛点集群。
   https://github.com/openai/codex/issues/28507

3. **#25178 [OPEN]** — Windows 10 22H2 上 Computer Use 截图失败（61 评论 / 26 👍）。`SetIsBorderRequired` 接口不受支持，阻塞桌面自动化工作流。
   https://github.com/openai/codex/issues/25178

4. **#31836 [OPEN]** — Projects "Last updated" 排序仅作用于组内而非项目间（50 评论 / 51 👍）。macOS 桌面端基础体验缺陷，影响日常项目管理。
   https://github.com/openai/codex/issues/31836

5. **#41220 [OPEN]** — 配额消耗异常与用量统计不一致的跨报告追踪元 Issue（44 评论 / 15 👍）。汇总多份配额异常加速消耗的报告，是计费透明度问题的集中讨论区。
   https://github.com/openai/codex/issues/41220

6. **#37458 [CLOSED]** — VSCode 扩展无法加载资源（55 评论）。已关闭，或与近期扩展修复相关，Windows 用户可关注修复版本。
   https://github.com/openai/codex/issues/37458

7. **#43375 [OPEN]** — 多个 GPT-5/GPT-6 模型同时返回容量错误（27 评论 / 14 👍）。说明问题非单模型路由故障，而是容量管理系统性问题。
   https://github.com/openai/codex/issues/43375

8. **#45019 [OPEN]** — app-server 队列中的 follow-up 消息丢失（10 评论 / 41 👍）。高 👍 表明影响面广，直接破坏多轮任务连续性。
   https://github.com/openai/codex/issues/45019

9. **#45444 [OPEN]** — 回归：长任务运行中触达限额时直接中断而非完成当前轮次。行为变更引发信任问题，与 #41220 配额议题相关联。
   https://github.com/openai/codex/issues/45444

10. **#43998 [OPEN]** — Agent 执行不安全递归删除导致源码永久丢失（Critical）。同类 #42480（删除生产数据库）也持续活跃，**安全沙箱与破坏性操作防护是社区最严重的安全关切**。
    https://github.com/openai/codex/issues/43998

## 4. 重要 PR 进展

1. **#45845** — TUI 编辑历史 prompt 时改用 `thread/revert` 回退当前线程，保留线程身份与设置。直接回应 #35005 的“就地编辑 vs fork”需求。
   https://github.com/openai/codex/pull/45845

2. **#45831** — TUI 支持会话级模型与推理力度选择（`s` 快捷键），不覆盖保存的默认配置。高频用户诉求落地。
   https://github.com/openai/codex/pull/45831

3. **#45837** — 在受限 Linux 沙箱中隐藏 WSLg 重复根目录，防止沙箱路径掩码外的文件系统内容泄露。安全加固 + WSL 修复。
   https://github.com/openai/codex/pull/45837

4. **#45820 / #45807** — 托管 daemon 重启后自动恢复中断的工作；恢复快照记录未完成的 turn 及其选项。显著提升长任务可靠性，或缓解 #45019。
   https://github.com/openai/codex/pull/45820

5. **#45813 / #45821 / #45830** — Windows 沙箱策略跟踪与 per-thread executor host 管理，TUI 沙箱状态改为以 app-server 配置为准。系统性重构 Windows 沙箱体验。
   https://github.com/openai/codex/pull/45813

6. **#45817** — 新增 `codex-mermaid` crate，在终端以 Unicode 文本渲染 Mermaid 图表（流程图、时序图、状态图等）。TUI 可视化能力增强。
   https://github.com/openai/codex/pull/45817

7. **#45812** — Responses 请求增加 workspace 路由支持，AuthManager 可按会话配置解析后端源与账户路由。
   https://github.com/openai/codex/pull/45812

8. **#45854** — 新增 `/daemon` 菜单，可在 TUI 内完成本地后台服务器更新，替代手工 shell 命令。
   https://github.com/openai/codex/pull/45854

9. **#45811** — WSL 终端检测增加超时上限并安全处理不确定结果，修复 TUI 启动卡死及 VS Code WSL 下 dead-key 输入问题。
   https://github.com/openai/codex/pull/45811

10. **#45806** — 限制插件安装请求仅允许根线程发起，非 root agent 的请求被拒绝。安全边界收紧。
    https://github.com/openai/codex/pull/45806

## 5. 功能需求趋势

- **Windows / WSL 一等公民支持**：Issues（#41290、#25178、#38310、#42964、#44342）与 PRs 均显示 Windows 生态（WSL、沙箱、MSIX、Computer Use）是当前投入最大且痛点最集中的方向。
- **会话管理精细化**：就地编辑历史 prompt（#35005）、防误触发送（#45588）、会话级模型切换、对话删除残留清理（#44343）。
- **可靠性 / 断点恢复**：daemon 重启恢复、中断 turn 记录、排队消息不丢失，长任务连续性是核心诉求。
- **配额与容量透明度**：容量错误、配额消耗异常、限额中断行为，用户要求更可预测的用量模型。
- **TUI 可视化与交互**：Mermaid 文本渲染、`/daemon` 菜单等，终端体验持续打磨。

## 6. 开发者关注点

- **模型可用性是头号痛点**："Selected model is at capacity" 今日新增至少 3 个报告（#45832、#45835、#45648），覆盖 Pro/X20/Pro Lite 多档订阅，且出现“新会话失败而旧会话可用”的异常路由行为，社区期待官方统一回应。
- **安全与数据保护**：两起 Critical 级数据丢失（#43998 递归删除源码、#42480 删除生产库）表明破坏性操作缺少有效防护，叠加 #30290（未经批准执行状态变更），Agent 安全边界亟需加强——今日 PR #45806、#45837 的安全收紧是积极信号。
- **桌面端稳定性**：扩展加载失败、更新后无法启动（#42964）、`/` 键崩溃（#38310）等发布质量问题影响 Windows 用户留存。
- **计费一致性**：#41220 追踪的用量统计与实际消耗不符问题，若持续无回应可能侵蚀付费用户信任。

---
*数据来源：github.com/openai/codex · 统计窗口：2026-09-15 ~ 2026-09-16*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-16

## 📰 今日速览

今日发布 **v0.62.0-nightly** 与 **v0.61.0-preview.0** 两个新版本，v0.60.0 稳定版也已上线，重点修复了 core 上下文保留、web fetch 安全校验及 MCP OAuth 合规问题。社区讨论持续聚焦 **Agent 可靠性**（挂起、误报成功）与 **Auto Memory 安全性**。PR 方面安全类修复活跃，包括路径遍历绕过、原子文件写入等关键修复。

---

## 🚀 版本发布

### [v0.62.0-nightly.20260916](https://github.com/google-gemini/gemini-cli/releases)
- **fix(core)**: 确保对象展开时 `AgentLoopContext` 属性不丢失（[PR #29335](https://github.com/google-gemini/gemini-cli/pull/29335)）
- **fix(a2a-server)**: tasks metadata 端点对不支持的 store 提前返回

### [v0.61.0-preview.0](https://github.com/google-gemini/gemini-cli/releases)
- 版本迭代与 changelog 整理（v0.59 / v0.60-preview）

### [v0.60.0 稳定版](https://github.com/google-gemini/gemini-cli/releases)
- **fix(core)**: 改进 web fetch 工具的目标校验与连接路由（[PR #29120](https://github.com/google-gemini/gemini-cli/pull/29120)）
- **fix(core)**: MCP OAuth 流程强制遵循 RFC 9207 issuer 标识

---

## 🔥 社区热点 Issues

### 可靠性 / Agent 执行

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 💬13) — Subagent 触达 `MAX_TURNS` 后仍报告 `success/GOAL`，掩盖了实际中断。状态上报失真会误导上层 Agent 决策，是最受关注的 bug 之一。

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 💬8, 👍8) — Generalist agent 无限挂起，连建目录这类简单操作都会卡死长达一小时。用户只能通过指令禁止 subagent 绕过，直接影响日常可用性。

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 💬4, 👍3) — Shell 命令已执行完成后仍卡在 "Waiting input"，简单命令即可复现，影响交互体验。

### 安全与隐私

4. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 💬5) — Auto Memory 将本地 transcript 发送给后台提取模型后才做脱敏，密钥已进入模型上下文。呼吁**确定性脱敏**（发前处理）并减少日志暴露。

5. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, 💬3) — Agent 在 git 操作中偶尔使用 `git reset` / `--force` 等破坏性命令，社区要求内置防护与危险操作劝阻机制。

### 能力增强方向

6. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, 💬9) — 利用 Gemini 3 的原生 bash 能力：零依赖 OS 沙箱 + 执行后意图路由，让模型用 `grep/sed/awk` 原生工作流提升效率，同时不牺牲安全。

7. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, 💬7) — EPIC：评估 AST 感知的文件读取/搜索/代码库映射，可精确读取方法边界、降低 token 噪音。配套调查 [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) 建议以 tilth 或 glyph 为起点。

8. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 💬6) — 模型几乎不主动使用自定义 skills 和 sub-agents，仅在显式要求时才调用，削弱了技能系统的实际价值。

### 其他值得关注

9. **[#22186](https://github.com/google-gemini/gemini-cli/issues/22186)** (P1, 💬3) — get-shit-done output hook 在输出用户摘要时导致崩溃。

10. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, 💬3) — 工具数量超限时直接 400 错误，期望 Agent 智能裁剪工具作用域。

---

## 🔧 重要 PR 进展

1. **[#29349](https://github.com/google-gemini/gemini-cli/pull/29349)** (P1, size/xl, 🆕今日) — VS Code 扩展：关闭 diff 标签页时保持终端焦点，修复多文件编辑时反复丢焦的体验问题。

2. **[#29347](https://github.com/google-gemini/gemini-cli/pull/29347)** (P1, maintainer) — UI 边框渲染防御负数尺寸，修复 `RangeError: Invalid count value: -1` 崩溃。

3. **[#29244](https://github.com/google-gemini/gemini-cli/pull/29244)** (P1, size/l) — **文件写入原子化**：并行工具写同一路径时当前会静默丢失编辑且双双报成功，此 PR 引入序列化写入，属关键数据完整性修复。

4. **[#29249](https://github.com/google-gemini/gemini-cli/pull/29249)** (P1) — 修复 `get_internal_docs` 路径守卫的**同级前缀绕过**漏洞（字符串前缀比较无路径边界），堵住目录遍历风险。

5. **[#29339](https://github.com/google-gemini/gemini-cli/pull/29339)** (P1) — OAuth refresh 时保留 `refresh_token` 并使凭据删除幂等，解决重新认证死循环（GH-21691）。

6. **[#29343](https://github.com/google-gemini/gemini-cli/pull/29343)** — 抑制 Node 23+ 下取消请求时同步抛出的 `AbortError` 导致的硬崩溃。

7. **[#29163](https://github.com/google-gemini/gemini-cli/pull/29163)** (P1, ✅已合并) — 修复 macOS Seatbelt 等受限环境下 git 仓库内启动崩溃（`useGitBranchName` hook 问题）。

8. **[#29156](https://github.com/google-gemini/gemini-cli/pull/29156)** (✅已合并) — 停止在 shell 执行中将 git 全局配置指向 `/dev/null`，恢复 `user.name` 等真实配置可见性。

9. **[#29333](https://github.com/google-gemini/gemini-cli/pull/29333)** (P2, enterprise) — 校验按约定发现的策略目录权限，加固企业策略加载安全。

10. **[#29352](https://github.com/google-gemini/gemini-cli/pull/29352)** (🆕今日) — 补全 Hooks 文档中 `ask` / `approve` 决策值的说明。

---

## 📈 功能需求趋势

| 方向 | 代表 Issue | 社区诉求 |
|---|---|---|
| **Agent 可靠性** | #22323, #21409, #25166 | 修复挂起、状态误报、shell 卡死——当前最高优先级 |
| **安全加固** | #26525, #22672 | 确定性脱敏、破坏性命令防护、沙箱执行（#19873） |
| **AST 感知工具链** | #22745, #22746, #19561 | 精确代码读取、token 节俭的“外科手术式”提取 |
| **Memory 系统改进** | #26516, #26522, #26523 | Auto Memory 的健壮性与可观测性批量修复 |
| **Skills/Subagent 触发** | #21968, #20079 | 提高模型自主调用技能与子代理的频率；支持 symlink |
| **任务追踪演进** | #18836, #21000 | 用持久化文件 CRUD 替代 in-context todo，对抗 context rot |

---

## ⚠️ 开发者关注点

1. **“静默失败”是最大痛点**：并行写文件丢数据（PR #29244）、subagent 误报成功（#22323）、memory patch 静默跳过（#26523）——开发者反复强调“报错比假装成功好”。
2. **Agent 挂起类问题影响信任**：generalist agent 挂起、shell 等待输入、交互式提示卡死等多条 P1 长期未解。
3. **配置不生效**：Browser Agent 忽略 `settings.json` 覆盖（#22267）、symlink agent 不识别（#20079），自定义能力打了折扣。
4. **安全边界收紧中**：路径遍历、OAuth 合规、git config 隔离等修复密集落地，建议及时升级到 v0.60.0+。
5. **上下文成本敏感**：社区对每 turn ~36.6k token 基线和文件读取"firehose"问题持续关注（#19561）。

---
*数据来源：github.com/google-gemini/gemini-cli · 统计窗口：过去 24 小时*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-16 | 数据来源：github.com/github/copilot-cli**

---

## 📌 今日速览

GitHub Copilot CLI 今日发布 **v1.0.85**，最受期待的功能——**Vim 模式正式面向所有用户开放**（`/vim` 或设置 `editorMode: vim`），呼声最高的 Issue #13 同日关闭。此外，社区反馈最为集中的**长会话内存溢出（OOM）问题**持续发酵，多个相关 Issue 保持活跃讨论。

---

## 🚀 版本发布

### v1.0.85（2026-09-16）
- **Vim 模式全量开放**：通过 `/vim` 命令或设置 `editorMode: vim` 启用，composer 中支持模态编辑，输入时显示当前模式
- 新增 `/settings` 选项，可为 agents 和 subagents 选择性启用上下文管理工具
- 调整 transcriptView 相关设置

### v1.0.84-9
- **新增**：`/settings` 中可启用 agents/subagents 的上下文管理工具
- **改进**：大幅缩短大型本地会话历史的元数据扫描时间（代价是线程和内存占用增加）
- **修复**：End 和 Ctrl+E 现在将光标移动到折行的真实行尾

---

## 🔥 社区热点 Issues（Top 10）

1. **#13 [已关闭] CLI 输入应支持 vi/vim 模式**（👍 76 | 💬 13）
   社区呼声最高的功能请求，运行近一年后随 v1.0.85 落地关闭。模态编辑爱好者的胜利。
   🔗 github.com/github/copilot-cli/issues/13

2. **#54 [已关闭] 与 VS Code Copilot Chat 设置深度集成**（👍 20 | 💬 13）
   要求 CLI 复用 VS Code 项目的 Copilot 配置，反映社区对统一体验的强烈诉求，已关闭。
   🔗 github.com/github/copilot-cli/issues/54

3. **#4664 恢复长期会话时 JavaScript 堆内存溢出崩溃**（💬 8）
   恢复大型旧会话即触发 V8 OOM，是当前最集中的痛点之一。
   🔗 github.com/github/copilot-cli/issues/4664

4. **#1148 Windows 下强制将 LF 行尾改为 CRLF**（👍 8 | 💬 7）
   CLI 编辑文件时破坏原有行尾格式，对 Windows 开发者影响广泛且长期未修。
   🔗 github.com/github/copilot-cli/issues/1148

5. **#4438 `disable-model-invocation: true` 导致 Skill 彻底不可用**（👍 7 | 💬 6）
   本应“仅手动调用”的 Skill 却在 CLI 中完全无法触达，语义与预期不符。
   🔗 github.com/github/copilot-cli/issues/4438

6. **#4725 Linux 上频繁 OOM 崩溃**（💬 6）
   每隔几分钟即崩溃，几乎不可用，属高严重性稳定性问题。
   🔗 github.com/github/copilot-cli/issues/4725

7. **#3954 `explore` 工具硬编码 `gpt-5.4-mini`，忽略自定义模型**（💬 4）
   自定义 API（如 DeepSeek）用户被硬编码模型卡住，涉及模型可配置性。
   🔗 github.com/github/copilot-cli/issues/3954

8. **#4251 1.0.74 恢复大会话回归：内存暴增 3-4 倍**（💬 4）
   严谨的 A/B 测试定位回归版本，与 #4664 同属会话恢复内存问题家族。
   🔗 github.com/github/copilot-cli/issues/4251

9. **#4699 长 `--resume` 会话 OOM，且崩溃转储写入用户工作目录**（👍 5 | 💬 4）
   14 小时内崩溃 3 次，同时污染 cwd，双重问题。
   🔗 github.com/github/copilot-cli/issues/4699

10. **#4854 沙箱 "Allow local network" 设置不生效**（💬 3）
    官方已在评论中确认为 `/sandbox policy` 显示层 bug，修复在途（见 #4867）。
    🔗 github.com/github/copilot-cli/issues/4854

**其他值得留意**：#4855（macOS Terminal 1.0.84-8 无法交互输入，已关闭）、#4807（空闲进程 FileWatch 风暴吃满双核、写 33GB 日志）、#4780（压缩 OOM 死循环导致会话永久无法恢复）。

---

## 🔀 重要 PR 进展

过去 24 小时内无 PR 更新，本节省略。

---

## 📈 功能需求趋势

1. **内存与长会话稳定性**（最强烈）：OOM 类 Issue 至少 7 条（#4664、#4725、#4251、#4699、#4639、#4780、#4506），是当前社区最大痛点
2. **模态编辑 / 键盘效率**：Vim 模式已落地（#13），Ctrl-D/End 等键位行为持续打磨（#4866）
3. **IDE / VS Code 一体化**：配置与 MCP 复用诉求明确（#54、#4847、#4552）
4. **沙箱与企业管控**：yolo 模式企业策略（#4783）、策略执行一致性（#4846、#4854）
5. **插件生态**：自动更新插件（#2734，👍 13）、marketplace 注册失效（#4556）
6. **模型可配置性**：自定义端点/模型未被尊重（#3954）
7. **可观测性 / OTel**：遥测数据缺失与误报（#4862、#4863）
8. **交互体验**：用聊天代替表单进行澄清提问（#4865）

---

## 🛠️ 开发者关注点

- **内存管理是头号敌人**：长会话/恢复会话场景的 V8 堆 OOM 几乎是所有高热度 Issue 的共同主题，涉及事件存储重试风暴、压缩死循环、看门狗误触发等多个根因。v1.0.84-9 的元数据扫描优化以更高内存占用换速度，可能加剧此问题
- **Windows 兼容性**：CRLF 行尾破坏（#1148）长期未修，影响文件完整性
- **崩溃副作用**：诊断报告写入 cwd（#4699）、33GB 日志（#4807）等“二次伤害”缺乏防护
- **认证与集成边缘情况**：CIMD OAuth 回调端口不匹配（#4800、#4793）阻断 MCP 服务器接入
- **会话生命周期健壮性**：过期锁文件使会话无法恢复（#4805）、后台 subagent 永久挂起（#4850）

---
*本报告基于过去 24 小时 GitHub 公开数据自动生成。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-09-16 | 数据来源：[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)**

---

## 📌 今日速览

今日仓库整体较为平静：过去 24 小时无新版本发布、无 PR 更新，社区活动集中在 2 条 Issue 上。其中最值得关注的仍是持续发酵的**配额异常扣费问题（#2626）**——cache_read 每轮计费但 cache_creation 恒为 0，疑似放大 10 倍以上消耗，付费用户投诉强烈。另有用户向仓库提交了针对 Kimi Work 桌面端的功能建议，侧面反映出官方缺乏专门的产品级 issue tracker。

---

## 🚀 版本发布

过去 24 小时无新 Release。

---

## 🔥 社区热点 Issues

> 今日仅 2 条活跃 Issue，全部列出：

### 1. 配额消耗异常：每轮计费 cache_read，cache_creation 恒为 0（消耗放大 >10 倍）
- **状态**：OPEN | 作者：@ahmxyaseen35-coder | 创建：2026-08-29，昨日（09-15）仍有更新
- **链接**：[Issue #2626](https://github.com/MoonshotAI/kimi-cli/issues/2626)
- **为什么重要**：直接关系到付费用户的真金白银。年费订阅用户报告在 5 小时配额窗口内，轻度使用几分钟即损失约 40% 配额。CLI 日志显示 cache_read 每轮都被计费，而 cache_creation 始终为 0，意味着缓存命中计费模式可能存在 bug，实际消耗放大超过 10 倍。
- **社区反应**：2 条评论，尚无官方修复确认。该问题自 8 月底提交至今近 3 周仍处 OPEN 状态，建议官方尽快回应计费透明度问题。

### 2. 功能建议：Kimi Work 会话标题自动带创建日期前缀（YYYYMMDD）
- **状态**：OPEN | 作者：@GH-Mason | 创建/更新：2026-09-15
- **链接**：[Issue #2646](https://github.com/MoonshotAI/kimi-cli/issues/2646)
- **为什么重要**：虽然针对的是 Kimi Work 桌面端，但作者明确指出**找不到 Kimi Work / Kimi Desktop 的公开 issue tracker**，只能参照 #2143 先例提交到 CLI 仓库。这暴露出 MoonshotAI 产品线反馈渠道缺失的问题——桌面端用户的反馈被迫“路由”到 CLI 仓库。
- **社区反应**：暂无评论，等待官方分流处理。

---

## 🔧 重要 PR 进展

过去 24 小时无 PR 更新。

---

## 📈 功能需求趋势

从近期 Issue 可提炼出以下方向：

1. **计费与配额透明度**（#2626）：用户对 cache 计费机制的可观测性有强烈诉求，期望 CLI 能提供更清晰的 token/配额消耗明细。
2. **会话管理体验**（#2646）：会话标题自动加日期前缀等小而实用的管理功能，反映重度用户对多会话整理效率的关注。
3. **产品线反馈渠道整合**：Kimi Work / Desktop 缺乏独立 tracker，社区呼吁官方建立统一或分产品的反馈入口。

---

## ⚠️ 开发者关注点

- **计费可靠性是当前最大痛点**：#2626 属于影响付费用户信任的 P0 级问题，涉及缓存计费逻辑（cache_creation 应在首轮产生却为 0，cache_read 却每轮计费），建议官方优先排查并对受影响用户给出补偿方案。
- **官方响应速度待提升**：#2626 已挂起近 3 周，仅 2 条评论；#2646 需要明确的分流责任人。
- **维护节奏偏静**：今日无 Release、无 PR 活动，社区处于等待官方动作的状态。

---

*本日报基于过去 24 小时 GitHub 数据自动汇总，数据截至 2026-09-16。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-09-16）

## 1. 今日速览

今日无新版本发布，但社区活跃度极高：50 条 Issues 与 50 条 PR 在过去 24 小时内更新。核心开发团队（@thdxr、@rekram1-node）集中合入了多个稳定性修复，包括 `/connect` 凭据切换性能优化、provider 超时机制重构等。同时两个高热度崩溃类 Bug（`SystemPrompt.environment` TypeError、消息重复投递）仍处于 OPEN 状态，值得用户关注。

## 2. 版本发布

过去 24 小时无新 Release。

## 3. 社区热点 Issues

1. **[#48372](https://github.com/anomalyco/opencode/issues/48372) [OPEN] `SystemPrompt.environment` 崩溃导致所有 prompt 失败** — 👍 23、7 条评论。TUI 和 `opencode run` 的每条消息都触发 "Unexpected server error"，属阻断性 Bug，热度最高但尚未修复。
2. **[#48447](https://github.com/anomalyco/opencode/issues/48447) [OPEN] 任务完成后 AI 重复应答同一消息** — 消息重复投递影响会话正确性，v1.16.0 起可复现，未关闭。
3. **[#48468](https://github.com/anomalyco/opencode/issues/48468) [OPEN] Windows 下“清理垃圾文件”误删 git 仓库** — 安全类严重事故：`Remove-Item -Force` 永久删除工作树和 `.git/objects`，凸显 shell 命令防护不足。
4. **[#49271](https://github.com/anomalyco/opencode/issues/49271) [OPEN] Skill 发现机制无限递归扫描** — `skills/**/SKILL.md` 无深度限制，工具内嵌 skill 副本会导致行为偏离，今日新报。
5. **[#49252](https://github.com/anomalyco/opencode/issues/49252) [CLOSED] Muse Spark 模型报错 `encrypted_content` 未授权** — provider 侧 reasoning 内容鉴权问题，今日报今日关，响应迅速。
6. **[#5305](https://github.com/anomalyco/opencode/issues/5305) [CLOSED] Plugin Hook：即时 TUI 命令** — 20 条评论、👍 14，长期热议的插件能力扩展，现已关闭。
7. **[#37070](https://github.com/anomalyco/opencode/issues/37070) [CLOSED] Plan/Build 模式切换从聊天 UI 消失** — 👍 22、17 条评论，v1.18.1 升级引发的 UI 回归，已修复。
8. **[#35772](https://github.com/anomalyco/opencode/issues/35772) [CLOSED] Desktop `Provider.list()` TypeError 启动崩溃** — Windows 用户每次启动均无模型/Provider 显示，已关闭。
9. **[#37258](https://github.com/anomalyco/opencode/issues/37258) [CLOSED] OpenAI Responses reasoning-only 流失败无限重试** — 子代理死循环阻塞父任务，影响多代理编排可靠性。
10. **[#44748](https://github.com/anomalyco/opencode/issues/44748) [OPEN] 子代理抢占原语需求** — 生产级批量流水线用户请求 max-turns、取消、流式工具调用等编排能力，反映企业级使用场景。

## 4. 重要 PR 进展

1. **[#49255](https://github.com/anomalyco/opencode/pull/49255) [CLOSED/合并] 凭据切换时复用模型目录** — 修复 `/connect` 3-5 秒卡顿（10+ Location 场景），由 @thdxr 快速取代并合入 #49109，性能优化代表。
2. **[#49229](https://github.com/anomalyco/opencode/pull/49229) [OPEN] Provider 请求默认 5 分钟 header/chunk 超时** — 重新实现 #46917，chunk 计时器按数据到达重置，解决流式请求挂死。
3. **[#49195](https://github.com/anomalyco/opencode/pull/49195) [OPEN] 网关账户限额归类为 Quota、4xx 不重试** — 402 及 Zen 限额错误码正确分类，避免无效重试。
4. **[#49259](https://github.com/anomalyco/opencode/pull/49259) [OPEN] TUI 中点击 execute 工具行打开详情弹窗** — 提升工具调用可观测性。
5. **[#49242](https://github.com/anomalyco/opencode/pull/49242) [OPEN] Codemode tool/extension 调用 before/after hooks** — 取代旧 `onToolCallStart/End`，支持 deny 能力，插件架构升级。
6. **[#49273](https://github.com/anomalyco/opencode/pull/49273) [OPEN] MCP OAuth 认证从 summary 触发** — agent bot 贡献的回归测试覆盖型修复。
7. **[#49272](https://github.com/anomalyco/opencode/pull/49272) [OPEN] 文件视图渲染 Markdown** — 桌面端体验改进。
8. **[#46690](https://github.com/anomalyco/opencode/pull/46690) [OPEN] 插件 API 暴露 session 表单、会话列表与全局事件流** — 为 telegram bot 等外部集成铺路，插件生态重要扩展。
9. **[#49263](https://github.com/anomalyco/opencode/pull/49263) [OPEN] `/update` 前刷新最新版本号** — 避免安装过期缓存版本。
10. **[#49185](https://github.com/anomalyco/opencode/pull/49185) [OPEN] 修复文件拖放 mention 二次失效** — v2 提示输入框 UX 修复（关闭 #39705）。

## 5. 功能需求趋势

- **插件与扩展性**：TUI 命令 hook（#5305）、session API 暴露（#46690）、palette 命令字段文档化（#37276）——插件生态是当前最强需求方向。
- **子代理编排**：后台子代理状态 UI（#37431）、抢占/取消原语（#44748），多代理生产化诉求明确。
- **Skill 机制完善**：元数据持久化、行为一致性（#31616）、递归扫描限制（#49271）。
- **模型与 Provider 兼容**：OpenAI Responses、Ollama、Muse Spark、Kilo 等多 provider 的流式/推理/附件兼容问题持续出现。
- **桌面端体验**：会话归档快捷操作、设置项目管理、键盘快捷键（ctrl+p 失效）。

## 6. 开发者关注点

- **稳定性**：启动崩溃（Provider.list、SystemPrompt.environment）和无限重试是最大痛点，其中 #48372 仍未修复，建议受影响用户关注进展。
- **安全性**：#48468 的误删仓库事故警示 shell 权限对话框描述缺失（#35415）与破坏性命令防护需加强，Windows 用户尤需谨慎。
- **网络与代理**：Bun 运行时对 LAN baseURL 的 ECONNREFUSED（#37432）表明自定义 provider 网络兼容仍是弱项。
- **升级回归频发**：1.18.x 系列出现多个 UI/功能回归（Plan/Build 切换、ctrl+p、Web UI 打开仓库），建议团队加强升级前回归测试；好消息是维护者响应速度快，多数回归已修复关闭。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-09-16

## 一、今日速览

VS Code 远程环境（Remote-SSH / Dev Containers / WSL）下 Webview 无法连接工作区守护进程成为今日最热议题，同日已出现针对性修复 PR #11983。桌面端问题集中爆发——主题/语言设置失效、工具调用块渲染为空。此外 `cua-driver-rs v0.20.9` 发布，提供三平台预编译二进制。

## 二、版本发布

**cua-driver-rs v0.20.9**（Qwen CUA Driver 预编译二进制）
- macOS：已签名 + 公证的 universal binary 及 `QwenCuaDriver.app`
- Linux：x86_64 / arm64（glibc ≥ 2.31），未签名
- Windows：未签名 UIAccess worker + 原生 SDK payload（x86_64 / arm64）

## 三、社区热点 Issues

1. **#11500** [P1] 多个后台 Agent 相继完成时 TUI 静默退出——Ink `useBoxMetrics` 布局监听器触发 React #185（Maximum update depth exceeded），进程直接掉回 shell 且无错误渲染。评论最多（15 条），与 #11858 形成修复跟进链。
2. **#11976** [P1] Dev Containers 下 Webview 无法访问工作区守护进程：动态端口绑定未使用 `asExternalUri`，报 "Failed to fetch"。今日新建即获 5 条评论，已 ready-for-human。
3. **#11956** [P2] 0.23.4 将无参数工具的 `parameters` 序列化为 `null`，导致严格的 OpenAI 兼容网关整体拒绝请求——互操作性问题，直接影响第三方网关用户。
4. **#11895** [P1, @wenshao] `/review` 维度 Agent 读取主 checkout 而非 PR worktree——简报只给了 diff 的绝对路径，代码审查正确性风险高。
5. **#11969** [P2] `stripAnalysisBlock()` 在 thinking 模型以 `</think>` 结尾时丢弃整个摘要，触发 `COMPRESSION_FAILED_EMPTY_SUMMARY`，本地 Ollama 部署用户受阻。
6. **#11955** [P2] 桌面端忽略 `ui.theme` 与 `general.language` 设置，配置面板显示正确但界面保持暗色/英文。
7. **#11966** [P2] 桌面端工具调用块渲染为空——`Edit`/`Shell` 块只显示 `{}`，用户无法在批准前核对内容，安全审批流程受影响。
8. **#11908** [P1] serve/acp 模式下超大 `available_commands_update` 通知越过 `MAX_JSON_NODES`，通道被拆毁后所有请求 404，会话丢失。
9. **#11887** [P2] ACP 模式忽略审批模式：限制模式下文件写入和 shell 命令零权限请求直接执行——安全隐患。
10. **#11878** [P2] Web Shell Session Overview 表格不显示无工作区（standalone）会话，且行点击路径会打开错误上下文。

其他值得注意：#11834（API 400 参数为空，已关闭）、#11936（`USE_OPENAI_RESPONSES` 泄漏 `${session_id}` 字面量，已关闭）、#11862（hooks matcher 尾部转义空格导致失效，已关闭）。

## 四、重要 PR 进展

1. **#11983** fix(vscode): 让远程窗口的 Webview 可达工作区守护进程——直接对应今日热点 #11976，覆盖 Remote-SSH / Dev Containers / WSL。
2. **#11979** feat(serve): workflow run 支持 `args`、`sourceRef` 与调用方脚本注入，扩展 headless 工作流能力。
3. **#11982** feat(web-shell): 展开的工具详情中新增 "View file / View image"，右侧面板预览文件且保留历史 diff。
4. **#11975** feat(web-shell): 宿主可排除指定设置项，服务嵌入式集成场景（对应 #11949 需求）。
5. **#11538** feat: 按模型选择 OpenAI wire API（`chat-completions` / `responses`），提升多模型网关兼容性。
6. **#11916** refactor(serve): 分离 ACP 控制平面与通道 harness，会话策略与物理通道监督解耦——架构级重构，或缓解 #11908 类问题。
7. **#9466** refactor: rewind 映射锚定到稳定 prompt 身份而非位置序号，使跨界面（resume、headless）回卷可靠。
8. **#10949** feat(cli): `qwen sessions peek/answer/stop` 三条子命令，可查看、应答和终止后台会话。
9. **#11950** docs: 修正与代码矛盾的 JSDoc/注释（配套 #11948），降低维护与 AI 辅助阅读成本。
10. **#11965** fix(hooks): `enabled` 状态按 hook `name` 而非完整身份索引，修复配置重载后开关状态丢失。

## 五、功能需求趋势

- **IDE / 远程集成**：Remote-SSH、Dev Containers、WSL 下扩展可用性是当前最高优先级方向（#11976、#11556、#11983），已列入 ide-integration 路线图。
- **Web Shell / Desktop 成熟度**：设置可配置化（#11975）、会话管理（#11878）、附件分块上传（#11958）、Markdown 预览（#11951）——嵌入式宿主集成需求明显上升。
- **OpenAI 兼容生态互操作**：wire API 按模型选择（#11538）、parameters 序列化（#11956）、customHeaders 占位符（#11936）。
- **本地/开源模型支持**：thinking 模型的压缩兼容（#11969）。
- **安全与权限**：Plan mode 只读命令白名单（#9694）、ACP 审批模式（#11887）、Windows 桌面签名（#11952）。
- **工程质量自动化**：autofix/review 流程自身的能力增强（#11964、#9071）。

## 六、开发者关注点

1. **稳定性痛点集中在 TUI 崩溃与会话丢失**：#11500（React #185 静默退出）、#11908（ACP 通道拆毁后 404）、#11914（重载后 Goal 状态误报中断）。
2. **远程/容器开发环境是最大摩擦点**：多个 P1 均与 VS Code Remote 场景相关，修复 PR 已在快速跟进。
3. **审批可验证性**：桌面端工具块渲染为空（#11966）使用户无法在批准前审查 Edit/Shell 内容，安全流程形同虚设。
4. **第三方网关兼容性回归**：0.23.x 版本引入的序列化行为变化（#11834、#11956）影响面广，建议升级前关注 changelog。
5. **文档与代码一致性**：JSDoc 与实现矛盾（#11948/#11950）被社区点名——对依赖 AI 辅助阅读代码的贡献者尤其耗时。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (Codewhale) 社区动态日报
**日期：2026-09-16 | 数据来源：github.com/Hmbown/DeepSeek-TUI**

---

## 1. 今日速览

今日无新版本发布，但社区活跃度极高：一天内有 50 条 Issue 更新、21 条 PR 更新。最突出的动态是 **TUI 重设计 "Shoreline" 以干净分支（#6258）重新提交并有望成为全新安装的默认界面**，以及围绕 **会话恢复失败（"belongs to another Runtime host"）** 的多个高热度 bug 报告持续发酵。同时维护者 @Hmbown 高速合入了编辑安全、性能门禁、runtime API 等多个 v0.9.14 里程碑切片。

---

## 2. 版本发布

过去 24 小时无新 Release。

---

## 3. 社区热点 Issues

1. **#6207 — Session picker 拒绝恢复已有 runtime store 的会话**（9 评论）
   最热 Issue。会话归属校验过严导致本地已存在的会话无法恢复，是近期用户反馈最集中的痛点。
   链接：[Hmbown/Codewhale Issue #6207](https://github.com/Hmbown/DeepSeek-TUI/issues/6207)

2. **#6225 — 全新进程内也无法 /resume**（6 评论）
   与 #6207 同源：干净安装下 quit 后重启、`/resume` 直接失败，是“最朴素路径”上的阻塞级 bug。#6233 已提交修复说明。
   链接：[Hmbown/Codewhale Issue #6225](https://github.com/Hmbown/DeepSeek-TUI/issues/6225)

3. **#6184 — 引擎运行中静默冻结**（5 评论，OPEN）
   长时间工具密集运行中引擎停止输出，用户消息被持久化但永不回复，无任何错误日志——可观测性空白导致排查极难。
   链接：[Hmbown/Codewhale Issue #6184](https://github.com/Hmbown/DeepSeek-TUI/issues/6184)

4. **#6190 — Steer 消息插入位置错乱**（5 评论，已关闭，PR #6239 修复）
   运行中插入的引导消息显示在已有工作之上，时间线与实际顺序不符，被用户报告为“令人困惑”。
   链接：[Hmbown/Codewhale Issue #6190](https://github.com/Hmbown/DeepSeek-TUI/issues/6190)

5. **#6165 — `/hooks edit` 未暂停 TUI 输入线程**（4 评论，已关闭）
   启动 $EDITOR 时按键被编辑器与 composer 双方瓜分，属于“用户丢东西”级别的终端控制权 bug，已随 #6239 修复。
   链接：[Hmbown/Codewhale Issue #6165](https://github.com/Hmbown/DeepSeek-TUI/issues/6165)

6. **#6169 — 无作业控制握手，SIGTTIN 后 TUI 状态损坏**（4 评论，OPEN）
   前台检查仅在启动时执行一次，进程被切到后台后鼠标/粘贴/raw 模式残留、进行中的 turn 只存在于 checkpoint。深层终端架构问题。
   链接：[Hmbown/Codewhale Issue #6169](https://github.com/Hmbown/DeepSeek-TUI/issues/6169)

7. **#6202 — 编辑路径嵌入 ast-grep-core 做语法门禁**（2 评论，OPEN）
   v0.9.14 核心增强：在文件写入前拒绝破坏语法的补丁，配套 #6204（syn 精确校验）、#6206（TOML/JSON 门禁）大部分已由 PR #6238 落地。
   链接：[Hmbown/Codewhale Issue #6202](https://github.com/Hmbown/DeepSeek-TUI/issues/6202)

8. **#6236 — headless 模式 `request_user_input` 永久挂起**（2 评论，OPEN）
   无头运行时工具仍被提供给模型，请求发出后无人应答且禁用开关又移除了绑定——静默死锁风险。
   链接：[Hmbown/Codewhale Issue #6236](https://github.com/Hmbown/DeepSeek-TUI/issues/6236)

9. **#6234 — 多主题黑底黑字**（1 评论，OPEN）
   gruvbox-dark、underwater 等主题部分界面黑字黑底不可读，macOS 0.9.13 可稳定复现。
   链接：[Hmbown/Codewhale Issue #6234](https://github.com/Hmbown/DeepSeek-TUI/issues/6234)

10. **#6237 — Ctrl+C 应先清空 composer 再触发退出**（1 评论，OPEN）
    对齐 Claude Code 等竞品的肌肉记忆交互（Esc/Ctrl+C 分工），反映社区对 TUI 交互一致性的高期待。
    链接：[Hmbown/Codewhale Issue #6237](https://github.com/Hmbown/DeepSeek-TUI/issues/6237)

---

## 4. 重要 PR 进展

1. **#6258 — Shoreline TUI 重设计，rebase 到 main（OPEN）**
   从 #6222 抢救出的重设计提交，将作为全新安装默认界面，剥离了搭车的无关提交。
   链接：[PR #6258](https://github.com/Hmbown/DeepSeek-TUI/pull/6258)

2. **#6251 — 会话级 patch 授权限定到用户实际批准的文件（CLOSED）**
   修复"approve for the session"授权范围过宽（甚至为空）的安全问题，关闭 #6247。
   链接：[PR #6251](https://github.com/Hmbown/DeepSeek-TUI/pull/6251)

3. **#6238 — 编辑安全：写入前 parse-gate（CLOSED）**
   一举关闭 #6204/#6205/#6206：Rust 用 `syn::parse_file` 精确校验、TOML/JSON 结构化门禁、编辑后格式归一保持锚点稳定。
   链接：[PR #6238](https://github.com/Hmbown/DeepSeek-TUI/pull/6238)

4. **#6239 — 编辑器交接、steer 顺序、/models 报错三合一修复（CLOSED）**
   关闭三个“用户丢工作”级 bug（#6165/#6190 等）。
   链接：[PR #6239](https://github.com/Hmbown/DeepSeek-TUI/pull/6239)

5. **#6259 — 流式渲染性能门禁（CLOSED）**
   #6193 的第一片：零依赖的确定性整数预算测量，针对 streaming reveal 路径，防止用户路径回归变慢。
   链接：[PR #6259](https://github.com/Hmbown/DeepSeek-TUI/pull/6259)

6. **#6229 — 原生客户端 runtime API 路由（CLOSED）**
   为 GPUI 桌面端提供 jobs/files/artifacts/git/LSP/secrets 等 HTTP 面，约 +5,900 行（含 1,758 行测试），是桌面集成的地基。
   链接：[PR #6229](https://github.com/Hmbown/DeepSeek-TUI/pull/6229)

7. **#6250 — MCP 死子进程探测与重连降级（CLOSED）**
   `is_ready()` 内同步探测死亡的 stdio 子进程，重连失败时保留 last-good catalog，关闭 #6187。
   链接：[PR #6250](https://github.com/Hmbown/DeepSeek-TUI/pull/6250)

8. **#6248 — 模型推理能力改由 Models.dev 目录驱动（CLOSED）**
   消除硬编码前缀判断（#6032），优先查询内置 catalog 快照。
   链接：[PR #6248](https://github.com/Hmbown/DeepSeek-TUI/pull/6248)

9. **#6262 — runtime bridge 重启时保留 stdio 线程映射（OPEN）**
   修复配置更新后 stdio 消息触发子进程重建导致 thread_map 丢失的问题。
   链接：[PR #6262](https://github.com/Hmbown/DeepSeek-TUI/pull/6262)

10. **#6257 — 持久化与 lifecycle-outbox 队列加上限 + latest-wins 合并（CLOSED）**
    关闭 #6213 的 R5/R6 两个发现，防止无界队列导致内存膨胀。
    链接：[PR #6257](https://github.com/Hmbown/DeepSeek-TUI/pull/6257)

---

## 5. 功能需求趋势

- **会话可靠性与恢复**：#6207/#6225/#6233/#6260 显示会话恢复是最强需求，涉及归属校验、幂等 reload。
- **桌面端（GPUI）集成**：#6163/#6164/#6166/#6176/#6179 及 PR #6229 表明 app-server 的 runtime API 面正在快速成形，是当前最大工程主线。
- **编辑/写入安全门禁**：#6202/#6204/#6205/#6206 系列构成“语法解析 + 格式归一”的防御纵深，防止模型坏补丁落地。
- **性能与可观测性**：#6193（运行时性能门禁）、#6184（静默冻结无日志）、PR #6249/#6259 反映对“用户路径速度 + 故障可见性”的双重关注。
- **架构清理（v0.9.14 重构 backlog）**：#6142（合并两套 MCP 栈）、#6139（app-server 接入 runtime API）、#6152（事件广播化）。
- **交互体验对标主流 Agent**：#6237（Ctrl+C 行为）、#6234（主题可读性）、Shoreline 重设计。

---

## 6. 开发者关注点

1. **静默失败是最大痛点**：引擎冻结（#6184）、headless 永久等待（#6236）、/models 报错（#6173）均无错误输出，社区强烈要求“失败要说话”。
2. **会话数据安全**：session 恢复失败的系列 bug 直接威胁用户工作成果，社区对此容忍度最低。
3. **终端控制权管理**：编辑器交接、后台挂起（#6169）、按键分流等问题表明 TUI 对真实终端环境的作业控制仍欠完善。
4. **多 provider/多模型支持**：Gemini、GLM-5.3-Flash 等第三方接入报错频出，模型能力判断去硬编码（#6032）是正确方向但仍需打磨。
5. **大规模/无头场景**：sub-agent 限流调度（PR #6055）、多仓库 workspace 并行写入（#6232）表明 fleet/headless 用例在增长，稳定性需求随之上升。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 社区动态日报 · 2026-09-16

## 一、今日速览

今日无新版本发布，但社区活跃度极高：过去 24 小时内共有 158 条 Issue 更新、15 个 PR 更新。围绕 **Compaction（上下文压缩）可靠性**、**扩展系统健壮性** 和 **Provider 适配细节** 出现多个高质量 bug 报告与修复 PR。Mitsuhiko 的“mid-conversation system messages" 架构性改进持续吸引关注。

## 二、版本发布

过去 24 小时无新 Release。

## 三、社区热点 Issues（Top 10）

1. **#2870 [CLOSED] 遵循 XDG Base Directory 规范**（22 评论 / 60 👍）
   Linux 下配置文件散落在 home 目录，应遵循 `$XDG_CONFIG_HOME` 标准。社区呼声最高的历史 issue，现已关闭，说明已得到解决。
   🔗 earendil-works/pi Issue #2870

2. **#8061 [inprogress] Context budget 忽略 maxTokens 输出预留导致溢出，恢复重试也失败**（9 评论）
   输入仅占上下文 78% 时请求仍被拒，且 compact-and-retry 恢复机制二次失败。核心上下文管理逻辑问题，标记为进行中。
   🔗 earendil-works/pi Issue #8061

3. **#8928 [inprogress] 并行启动时因其他 Provider 过期 OAuth 凭据误报 "No API key found"（约 48 秒）**
   报告者给出确定性复现与计时数据，解释了多进程场景下高发的原因。错误指向错误的 Provider 是排障痛点。
   🔗 earendil-works/pi Issue #8928

4. **#9571 [bug] Retry-After HTTP-date 格式非法时零延迟死循环重试**
   `Date.parse` 对非法日期返回 NaN，导致 429 紧密循环重试无退避。今日更新，经典边界条件 bug。
   🔗 earendil-works/pi Issue #9571

5. **#9652 [CLOSED] Claude Fable 因转写的 thinking 块拒绝压缩请求**
   `/compact` 失败：`serializeConversation` 将 thinking 块转写入摘要 prompt，触发 Anthropic `reasoning_extraction` 分类器拦截。Compaction 链路又一问题。
   🔗 earendil-works/pi Issue #9652

6. **#9306 [inprogress] 中止/错误的 turn 留下未匹配的 toolCall 块，后续续写被 Provider 拒绝**
   流式输出中途出错时上下文残留孤儿 toolCall，是影响多轮工具调用的上下文完整性问题。
   🔗 earendil-works/pi Issue #9306

7. **#9361 Windows：加载扩展时 shellPath 被非确定性忽略，PATH 回退到 WSL System32 bash.exe**
   Windows shell 解析链路在扩展加载后变得不可预测，影响所有 Windows 用户的基础工具执行。
   🔗 earendil-works/pi Issue #9361

8. **#9577 bash 工具被 SIGKILL/SIGTERM 杀死后仍成功 resolve**
   调用方无法区分部分输出与真正成功。与早前 #8992/#8882 修复相关但未覆盖信号杀死的场景。
   🔗 earendil-works/pi Issue #9577

9. **#9444 openai-completions 丢弃流式 tool_calls 上的 Gemini thoughtSignature**
   经 OpenAI 兼容网关调用 Gemini 时，第二轮工具调用即失败。混合网关场景的兼容性硬伤。
   🔗 earendil-works/pi Issue #9444

10. **#9549 [fullscreen] 大型 transcript 每帧全量重渲染，resize 重发整个 transcript（单核打满）**
    由报告者本地 pi agent 协助起草并验证的性能报告，规范值得称道。TUI 渲染性能是近期持续热点。
    🔗 earendil-works/pi Issue #9549

## 四、重要 PR 进展（Top 10）

1. **#9548 Mid-conversation system messages**（@mitsuhiko，OPEN）
   将 system prompt 与工具变更纳入 transcript，而非静默改写初始条件；支持 resume/分支导航后恢复状态、保留缓存前缀。架构级改进，关联 RFC 54。
   🔗 earendil-works/pi PR #9548

2. **#9630 feat: 事件处理器取消订阅**（OPEN）
   修复 #8967，为扩展事件订阅提供 unsubscribe 能力，测试待补。
   🔗 earendil-works/pi PR #9630

3. **#6881 feat: 使用 Provider 上报的实际计费成本**（OPEN，进行中）
   响应含 `usage.cost` 时替代目录费率计算，支持 BYOK 上游成本分摊。长期进行中的成本准确性改进。
   🔗 earendil-works/pi PR #6881

4. **#9619 fix: 保留 Anthropic 工具 schema 根级组合子**（CLOSED，已合并）
   修复 #9134：`anyOf/oneOf/allOf` 不再被静默丢弃，模型可见合法取值组合。
   🔗 earendil-works/pi PR #9619

5. **#9615 feat: 新增 /forget 命令实现上下文回滚**（CLOSED）
   支持软/硬两种模式移除最近 N 轮用户对话，可选择性作用于会话文件。
   🔗 earendil-works/pi PR #9615

6. **#9434 feat: 允许扩展追加 session system prompt**（OPEN）
   `session_start` 处理器可返回 append-only 的 `systemPromptAppend`，含来源元数据与错误隔离。
   🔗 earendil-works/pi PR #9434

7. **#8635 fix: 惰性 setup 期间保留 aborted 停止原因**（OPEN）
   修复 #8409：将 abort 信号穿透惰性流式 setup 包装层，避免误报为普通错误。
   🔗 earendil-works/pi PR #8635

8. **#9648 / #9646 Baseten session affinity 请求头修复**（CLOSED）
   两连发修复 Baseten Provider 的会话亲和性请求头，从 sessionId 派生。
   🔗 earendil-works/pi PR #9648

9. **#9642 fix: 导出扩展事件钩子类型**（CLOSED）
   将 `ExtensionAPI.on()` 相关事件/结果类型从包入口导出，改善扩展开发 TS 体验。
   🔗 earendil-works/pi PR #9642

10. **#9611 fix: 移除 prompt-url-widget 中过时的 session_switch 处理器**（CLOSED）
    清理已被 `session_start` + `event.reason` 取代的旧 API，反映扩展 API 的演进方向。
    🔗 earendil-works/pi PR #9611

## 五、功能需求趋势

- **上下文与 Compaction 管理**：最高频主题。#8061、#9602、#9512、#9652 均指向压缩/预算计算的边界缺陷；PR #9615（/forget）、#9548（transcript 化 system 消息）显示社区在推动更精细的上下文生命周期控制。
- **扩展系统健壮性**：#8791（暴露 ModelRuntime）、#9632（原子化 idle 提交）、#9650（加载状态可观测）、#9649（工具名冲突降级而非退出）——扩展作者正在系统性提出 API 补全需求。
- **Provider 兼容性与成本准确性**：#7010（schema 规范化）、#9444（thoughtSignature）、#9457（Bedrock 1h 缓存计费）、#9485（DeepSeek V4.1 reasoning 档位过时）、#6881（实际计费）。
- **TUI/渲染性能**：#9549、#7839 表明大 transcript 场景下的渲染性能已成为重点。
- **平台兼容性**：Windows 相关问题密集（#9361、#9490、#9577）。

## 六、开发者关注点

1. **错误恢复链路的可靠性**：重试分类器漏判（#9585）、NaN 退避（#9571）、压缩恢复二次失败（#8061）——开发者期望失败路径与成功路径同等健壮。
2. **可观测性不足**：多进程下错误指向错误的 Provider（#8928）、扩展加载结果不可读（#9650）等，排障成本高是高频抱怨。
3. **进程/信号语义**：bash 工具被信号杀死后仍报成功（#9577），以及 abort 信号在惰性路径上的丢失，影响上层自动化决策。
4. **多模态 Schema 保真度**：根级 `anyOf` 被丢弃、`required` 未规范化、thoughtSignature 丢失——跨 Provider 转发层的信息损耗正在集中暴露。
5. **扩展冲突处理偏激进**：工具名冲突直接 exit 1（#9649），而 command/shortcut 冲突仅警告，行为不一致令扩展生态维护者困扰。

</details>

<details>
<summary><strong>oh-my-pi</strong> — <a href="https://github.com/can1357/oh-my-pi">can1357/oh-my-pi</a></summary>

# 📰 oh-my-pi 社区动态日报 — 2026-09-16

## 1️⃣ 今日速览

oh-my-pi 今日发布 **v18.2.1 与 v18.2.0** 两个版本，重点修复长对话流式处理 CPU 飙升问题，并新增 Anthropic 兼容主机的 `upstreamModel` 透传以检测路由模型替换。Issue 端插件/agent 发现机制相关缺陷集中爆发（#11151、#11362），PR 端社区贡献活跃，涌现多个权限精细化、artifact 溯源等高质量功能提案。

---

## 2️⃣ 版本发布

### [v18.2.1](https://github.com/can1357/oh-my-pi/releases)
- **pi-agent-core 新增**：可选的排队消息预处理，支持取消安全投递与附加上下文（[#11835](https://github.com/can1357/oh-my-pi/pull/11835) by @andrebrait）
- **修复**：长对话回合中流式处理 CPU 飙升问题

### [v18.2.0](https://github.com/can1357/oh-my-pi/releases)
- **pi-ai 新增**：Anthropic 兼容主机（直连或经 OpenRouter `reasoning_details`）的助手回合携带 `upstreamModel`——从签名 thinking block 中恢复实际服务模型 ID，调用方可据此检测路由是否偷换了请求的模型

---

## 3️⃣ 社区热点 Issues

| # | Issue | 关注理由 |
|---|-------|---------|
| 1 | [#10124](https://github.com/can1357/oh-my-pi/issues/10124) ⛔ | **P1 安全缺陷**：eval 工具在非交互子代理会话中绕过审批墙（fail-open），与 bash/edit/write 的行为不一致，20 条讨论，已修复关闭 |
| 2 | [#10913](https://github.com/can1357/oh-my-pi/issues/10913) ⛔ | **P1 数据丢失**：isolated task 子代理 yield 时隔离 worktree 被直接删除，已提交的 6 个 commit 全部丢失，触目惊心，已关闭 |
| 3 | [#7982](https://github.com/can1357/oh-my-pi/issues/7982) 🔓 | **仍在开放的增强需求**：为单次 task 调用安全设置模型（task 工具与 eval 脚本均需支持），6 👍，多模型编排场景刚需 |
| 4 | [#11362](https://github.com/can1357/oh-my-pi/issues/11362) 🔓 | marketplace 安装的插件 `agents/` 默认不被发现，`discoverAgents` 存在未文档化的第二道门槛，与 #11151 同属插件发现体系问题 |
| 5 | [#11151](https://github.com/can1357/oh-my-pi/issues/11151) | `--plugin-dir` 不再发现插件中的 agents（仅 extension 可用），18.1.6 后行为回归 |
| 6 | [#11014](https://github.com/can1357/oh-my-pi/issues/11014) | 智谱 429 重置时间解析缺陷：中文“将在…重置”时间戳被当作 UTC，导致会话在 UTC+8 机器上**多等 8 小时**，典型时区陷阱 |
| 7 | [#11961](https://github.com/can1357/oh-my-pi/issues/11961) | Hindsight 心智模型 TTL 刷新反复重写 Anthropic 缓存前缀，单会话重写高达 580K token，缓存效率痛点 |
| 8 | [#11947](https://github.com/can1357/oh-my-pi/issues/11947) | Advisor 子系统遇首次 429 即永久瘫痪，而主 agent 同日遇百次仍能恢复——瞬态错误分类不当 |
| 9 | [#9783](https://github.com/can1357/oh-my-pi/issues/9783) | TUI 底部 agent 状态行重复插入导致无限滚动，仅影响 isolation worker 场景，13 条讨论 |
| 10 | [#7714](https://github.com/can1357/oh-my-pi/issues/7714) 🔓 | eval kernel 关闭未确认时泄漏 setsid 分离进程，无进程组 kill，长期驻留系统资源 |

> 📊 过去 24 小时 Issue 更新共 **183 条**，显示社区活跃度极高；多条 P1/P2 缺陷被快速 triage 并关闭，响应速度值得肯定。

---

## 4️⃣ 重要 PR 进展

| # | PR | 内容 |
|---|-----|------|
| 1 | [#12187](https://github.com/can1357/oh-my-pi/pull/12187) | 尊重硬性 session_stop 阻断并保留显式取消，修复 advisory 结果掩盖后续硬阻断的问题 |
| 2 | [#12082](https://github.com/can1357/oh-my-pi/pull/12082) | **artifact 生产者级作用域**：记录产出会话 ID，opt-in `producer` scope 仅解析本会话产物，无溯源信息时 fail closed——安全设计意识良好 |
| 3 | [#12081](https://github.com/can1357/oh-my-pi/pull/12081) | GitHub 工具支持**按操作粒度**的审批策略（`github.<operation>`），工具级策略作为回退 |
| 4 | [#10222](https://github.com/can1357/oh-my-pi/pull/10222) | 修复 MCP 网关冷启动期间“成功但为空”的 `tools/list` 被缓存为权威结果的问题，新增 `/mcp refresh` |
| 5 | [#11938](https://github.com/can1357/oh-my-pi/pull/11938) | **Prompt 缓存抖动诊断**：opt-in 缓存日志（HMAC 指纹，不留存明文），关联物理请求与响应缓存命中，直击 #11961 类成本痛点 |
| 6 | [#12171](https://github.com/can1357/oh-my-pi/pull/12171) | OpenAI Codex：信用额度账户在计划额度耗尽后仍可选，`/wham/usage` 仅报计划额度的问题修复 |
| 7 | [#11618](https://github.com/can1357/oh-my-pi/pull/11618) | RPC 新增 `promote_queued_message`，将排队的用户 follow-up 提升为 steering 消息，增强运行时干预能力 |
| 8 | [#9379](https://github.com/can1357/oh-my-pi/pull/9379) | Skills 体系大升级：嵌套命名空间发现、extension skillPaths、插件 manifest 目录 |
| 9 | [#9543](https://github.com/can1357/oh-my-pi/pull/9543) | Extensions API 可列出/检查/复活/驱动命名注册 agent，覆盖 print、交互、ACP、子代理全宿主 |
| 10 | [#11762](https://github.com/can1357/oh-my-pi/pull/11762) | 新增 `--new` 标志，autoResume 配置下单次启动全新会话 |

其他值得关注：[#12083](https://github.com/can1357/oh-my-pi/pull/12083)（系统提示中澄清 omp 身份，消除 Anthropic OAuth 指纹混淆）、[#12194](https://github.com/can1357/oh-my-pi/pull/12194)（Handlebars 系统提示模板覆盖）、[#10289](https://github.com/can1357/oh-my-pi/pull/10289)（会话内重启工具）。

> 📊 过去 24 小时 PR 更新共 **397 条**。

---

## 5️⃣ 功能需求趋势

1. **多模型编排精细化** — 按任务指定模型（#7982）、`upstreamModel` 模型替换检测（v18.2.0）、modelRole 引用解析（#10853）
2. **插件与 Agent 生态** — 插件 agents 发现链路问题频发（#11151、#11362、#10827），配套 PR 集中在 skills 命名空间与 registry agent API（#9379、#9543）
3. **审批与安全模型** — eval fail-open（#10124）、操作级审批策略（#12081）、artifact 生产者隔离（#12082）显示权限边界是当前核心关切
4. **成本与缓存优化** — 缓存前缀重写（#11961）、缓存抖动诊断（#11938）、额度耗尽策略（#12171）
5. **Provider 兼容性** — 智谱时区（#11014）、OpenAI 自定义端点（#11121）、Antigravity 图片模型 404（#11106）、Muse 上限（#12199）

---

## 6️⃣ 开发者关注点

- **静默失败最伤人**：多条高热度 Issue 的共同模式是“错误被吞掉”——Antigravity 图片 404 静默换 provider（#11106）、wake 回合失败对唤醒方零反馈（#11290）、ACP 权限应答被忽略后挂起（#10850）。开发者强烈呼吁 fail loudly。
- **插件系统可靠性**：lock.json 版本漂移且 doctor 检不出（#11090）、marketplace 大小写校验过严（#10827）、agents 发现回归——插件链路需要系统性加固而非零散修复。
- **子代理生命周期脆弱**：worktree 删除丢数据（#10913）、空回合 yield 崩溃（#11150）、continuation drain 期间被替换（#10378），隔离/复活机制的边界条件仍是重灾区。
- **长会话成本可控性**：Hindsight TTL 刷新破坏缓存、artifact 恢复撑爆上下文（#11365），重度用户对 token 浪费高度敏感。
- **状态一致性**：RULES.md 热更新失效（#10940）、planModePaused 残留（#11692）、RPC 控制误写全局配置（#11431）——配置作用域与状态同步需明确契约。

---

*数据来源：github.com/can1357/oh-my-pi | 生成时间：2026-09-16*

</details>

<details>
<summary><strong>DeepSeek Harness</strong> — <a href="https://github.com/deepseek-ai/deepseek-harness">deepseek-ai/deepseek-harness</a></summary>

# DeepSeek Harness 社区动态日报
**日期：2026-09-16** | 数据来源：[deepseek-ai/deepseek-harness](https://github.com/deepseek-ai/deepseek-harness)

---

## 1. 今日速览

今日 DeepSeek Harness 发布了 **v0.1.6-alpha.1** 预发布版本，重点增强了 Web 端交互体验（多标签终端、会话恢复）与 MCP 协议能力（资源发现、URI 模板），并扩展了 Headless 模式的脚本化能力。过去 24 小时内暂无新增 Issue 与 PR 更新，社区讨论热度平稳。

---

## 2. 版本发布

### dsh-v0.1.6-alpha.1
🔗 [Release 链接](https://github.com/deepseek-ai/deepseek-harness/releases)

**新增功能：**

- **Web 侧边栏新增终端**：支持多标签页、Shell 选择，刷新后可恢复会话状态（@LegGasai）——显著改善浏览器端开发工作流，无需切换本地终端。
- **已归档会话列表**：设置页中新增归档会话查看与恢复功能（@tianyicui）——解决长周期任务中断后找回上下文的痛点。
- **MCP 资源能力增强**：支持资源发现与读取、URI 模板；内置 Profile 配置 MCP 服务器后可直接使用共享资源工具（@tianyicui）——使 DeepSeek Harness 作为 MCP 客户端的能力更加完整。
- **Headless 标准输入支持**：可从 stdin 接收任务，配合 `--session-id` 继续已有会话——为 CI/CD 管道和自动化脚本集成铺平道路。

**简评**：本次 alpha 版本方向明确——强化 Web/Headless 双端的“会话连续性”和 MCP 生态整合，值得关注后续稳定版发布。

---

## 3. 社区热点 Issues

过去 24 小时内无 Issue 更新，本节暂缺。建议持续关注 [Issues 列表](https://github.com/deepseek-ai/deepseek-harness/issues) 的后续动态。

---

## 4. 重要 PR 进展

过去 24 小时内无 PR 更新，本节暂缺。建议关注 [Pull Requests 列表](https://github.com/deepseek-ai/deepseek-harness/pulls)。

---

## 5. 功能需求趋势

结合近期版本迭代方向，可观察到以下趋势：

- **MCP 生态集成**：资源发现、URI 模板等能力持续落地，MCP 兼容性是当前投入最集中的方向。
- **Web/远程开发体验**：多标签终端、会话恢复等表明 Web 端正在向“可替代本地 IDE”演进。
- **自动化与脚本化**：Headless 模式的 stdin 输入与 `--session-id` 会话续接，反映对 CI/CD 集成场景的重视。
- **会话管理**：归档、恢复、续接等能力贯穿多个端，长上下文任务的连续性是核心诉求。

---

## 6. 开发者关注点

- **浏览器端能力边界**：终端刷新恢复意味着 Web 端状态持久化正在成熟，开发者可更多在纯浏览器环境中完成工作。
- **自动化脚本作者**：`--session-id` + stdin 的组合使批量任务和管道式调用成为可能，建议提前验证 alpha 版稳定性。
- **MCP 服务器维护者**：新版本客户端已支持资源发现与 URI 模板，是时候评估服务器端是否暴露 resources 能力。

---

*本日报基于 GitHub 公开数据自动汇总，如需补充细节请查阅原文链接。*

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*