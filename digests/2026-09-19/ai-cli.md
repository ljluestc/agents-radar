# AI CLI 工具社区动态日报 2026-09-19

> 生成时间: 2026-09-19 03:44 UTC | 覆盖工具: 11 个

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
**日期：2026-09-19**

---

## 一、生态全景

AI CLI 工具已从“终端补全助手”全面演进为**多形态（CLI/TUI/桌面/Web）、多代理（subagent/fleet）、可扩展（Mods/hooks/MCP/skills）的编码代理操作系统**。行业标准化进程加速——AGENTS.md 落地 Claude Code、MCP 生态深度渗透所有工具、沙箱与权限治理成为安全竞争焦点。与此同时，各工具普遍进入“能力扩张后的偿债期”：数据安全事故（越权删除、压缩丢历史）、静默失败、Windows 平台劣化是全行业的共性痛点。头部工具迭代极快（Codex 单日 5 个 alpha），社区反馈直接驱动路线图，issue 区已成为事实上的产品共创空间。

---

## 二、各工具活跃度对比

| 工具 | 今日热点 Issues | PR 动态 | Release | 阶段特征 |
|---|---|---|---|---|
| **Claude Code** | 10+ 热点（含 5169👍 已落地需求） | 8 个 Mods/diff 相关 PR | v2.1.277 + v2.1.278 双发 | Mods 扩展系统冲刺发布 |
| **OpenAI Codex** | 10 热点 + 沙箱失败集群 | 10 个 PR（安全为主） | 稳定版 0.155.1 + 5 个 alpha | 高频迭代 + 安全舆情响应 |
| **Gemini CLI** | 10+ 热点（4 个 P1） | 10 个 PR（2 个 XL 级） | v0.62.0-nightly | AST 工具链架构升级 |
| **GitHub Copilot CLI** | 10 条（MCP 问题集中） | 0 条 | v1.0.87-0 | 企业策略层完善期 |
| **OpenCode** | 10 条（v2 迁移问题爆发） | 10 个 PR | 无（v2 成默认信号） | v2 迁移期阵痛 |
| **Qwen Code** | 10 条（3 个 P1 回归） | 10 个 PR | v0.24.1-preview.0 | 0.24.0 回归修复 + 桌面端冲刺 |
| **Pi** | 72 条有更新 | 20 个有进展（多项合并） | 无 | 高活性、快响应 |
| **oh-my-pi** | 70 条 | 112 条（含 7-PR stack） | v18.2.6 | RFC 密集期 + 缓存优化 |
| **DeepSeek TUI (Codewhale)** | 10 条 | 10 条（单日多重量级） | 无 | 0.9.14 重构清债版 |
| **Kimi Code CLI** | 批量关闭积压 + 2 新回归 | 1 条 | 无 | 2.0. Rust 迁移打磨期 |
| **DeepSeek Harness** | 无活动 | 无 | 无 | 静默 |

**观察**：Pi/oh-my-pi 这类中小社区的活动效率（当日报告当日修复、RFC 快速讨论）显著高于大厂仓库的治理节奏；Claude Code 的 #87647（6k+ 可复现 issue 被自动关闭）暴露了大体量仓库的治理瓶颈。

---

## 三、共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **上下文压缩与 token 成本** | oh-my-pi（RLM RFC v1–v7、prompt cache 修复）、Gemini CLI（文件级任务跟踪替代 WriteToDo、AST 搜索省 token）、Pi（thinking 块治理、compaction 问题簇）、OpenCode（compact 空摘要销毁历史）、Qwen Code（#12028 非对话 token 治理）、Claude Code | **所有工具的头号焦虑**：压缩可靠性、缓存命中、非对话开销可见性 |
| **破坏性操作安全防护** | Codex（#33624/#46022 越权删除事故 + 沙箱加固 PR）、Qwen Code（bwrap 沙箱基建）、Gemini CLI（MCP fail-closed）、oh-my-pi（补丁路径逃逸修复）、OpenCode（取消后仍执行子进程） | “即使 Full Access 也要有硬确认/恢复门控”成为共识 |
| **MCP 生态兼容性** | Copilot CLI（Figma/OAuth DCR 集中爆发）、oh-my-pi（Figma DCR 兼容 PR）、Codex（nextCursor 分页缺失）、Gemini CLI（工具数 128/400 上限）、Qwen Code（registrationUrl 丢失）、DeepSeek TUI（双 MCP 栈合并） | MCP 已是标配但兼容质量参差，OAuth DCR 与分页是高频坑 |
| **静默失败治理** | Claude Code（文本不落盘、MCP 工具静默丢弃）、Qwen Code（LSP 中文响应静默丢弃）、Pi（压缩静默 no-op、`--print` 零输出）、DeepSeek TUI（引擎无日志冻结）、OpenCode（GBK 文件静默损坏） | 跨工具的共识：“静默失败比崩溃更难排查”，要求显式诊断信息 |
| **Windows 平台一等公民化** | Claude Code（今日热点近半 Windows）、Codex（沙箱失败为最大痛点集群）、Pi（64 评论调研帖）、DeepSeek TUI（CI/路径修复） | Windows 体验普遍落后 macOS，是最大的平台性债务 |
| **长会话稳定性** | Claude Code、Codex（Thinking 卡死）、Pi（CPU 飙升）、oh-my-pi（写入变慢） | 长上下文场景的渲染、内存、流式性能全面承压 |
| **v2/重写迁移兼容性** | OpenCode（V1→V2 会话丢失）、Kimi CLI（Rust 重写回归）、Qwen Code（0.24.0 回归） | 架构重写期的功能回退与数据迁移是普遍风险 |

---

## 四、差异化定位分析

| 工具 | 定位与侧重 | 技术路线特点 |
|---|---|---|
| **Claude Code** | 企业级全形态代理平台 | Mods 扩展系统 + AGENTS.md 标准对接；企业网关/Bedrock/Vertex 配置粒度最细；桌面端多账户是短板 |
| **OpenAI Codex** | 全平台代理 + Computer Use 探索 | Rust 核心、沙箱安全投入最重（Seatbelt/Windows 身份/独立网络代理）；安全问题响应最快但事故也最多 |
| **Gemini CLI** | 上下文工程架构创新者 | 唯一系统性推进 AST 感知工具链与文件级任务跟踪；Auto Memory 是差异化能力但安全问题待解 |
| **Copilot CLI** | GitHub 企业生态入口 | 组织级策略/routing 托管配置是企业差异化；MCP 稳定性和 PR 活跃度偏弱 |
| **OpenCode** | 开源桌面优先的通用代理 | v2 schema 重构 + Zen API 托管服务；多提供商中立立场，对 CJK 编码支持最积极 |
| **Qwen Code** | 国内生态 + 多形态分发 | 唯一同时推进 Batch API（半价）、后台 agent、Web Terminal、browser-use 多会话；权限作用域模型最精细 |
| **Pi / oh-my-pi** | 极客/本地 LLM 社区驱动 | 本地模型友好（/retry、流截断重试）、提示缓存优化、RLM 上下文操作系统 RFC——前沿实验场 |
| **DeepSeek TUI** | Provider 中立化转型中 | 从 DeepSeek 单绑定转向多 Provider（CSDN 星图接入）、Fleet 多代理管理、运行时 API |

**目标用户分层**：Claude Code/Codex/Copilot 面向企业与主流开发者；Qwen/Kimi/DeepSeek 系深耕国内与性价比场景；Pi/oh-my-pi 服务本地 LLM 与深度定制用户；OpenCode/Gemini CLI 兼顾开源与企业集成。

---

## 五、社区热度与成熟度

- **最活跃第一梯队**：Claude Code（单 issue 5169👍）、Codex（数据安全事故引发 39 评论级讨论）——社区规模最大，但也伴随治理信任危机（issue 自动关闭争议）。
- **高效率快速迭代梯队**：Gemini CLI（XL 级 PR 连发）、Pi/oh-my-pi（当日报告当日修复、RFC 高密度讨论）、DeepSeek TUI（单人连发重量级 PR）——响应速度优于大厂。
- **成熟稳定期**：Copilot CLI（PR 近乎停滞，issue 以边缘兼容为主）、Kimi CLI（批量清债 + 新版回归修复）。
- **动荡期**：OpenCode（v2 迁移问题集中暴露，但桌面端质量投入明显）、Qwen Code（0.24.0 回归待 0.24.1 兜底）。
- **静默**：DeepSeek Harness 需警惕项目活跃度风险。

---

## 六、值得关注的趋势信号

1. **AGENTS.md 成为事实标准**：Claude Code 落地 5169👍 需求后，跨工具指令文件统一已不可逆，多工具协作开发者应尽快将项目指令迁移至 AGENTS.md。

2. **“破坏性操作防护”从可选变必选**：Codex 的越权删除事故与全行业的沙箱/门控投入表明，**即使 Full Access 模式也应假设代理会犯错**——生产环境务必启用 checkpoint/快照，勿在无版本控制的目录跑 agent。

3. **上下文压缩是下一个竞争高地**：从 Gemini 的文件级任务跟踪、AST 精确读取，到 oh-my-pi 的 RLM RFC、专用 compaction 模型，**“精细化读取 + 可靠压缩 + 缓存保温”将直接决定长任务成本**。当前压缩机制均有丢数据风险（OpenCode 空摘要销毁历史），重要会话建议先导出。

4. **静默失败治理是可靠性分水岭**：几乎所有工具都在补“错误可观测性”课。选型时应将“失败是否有显式诊断”作为评估维度。

5. **Windows 是当前全行业短板**：Windows 用户建议暂缓依赖沙箱的关键工作流（尤其 Codex），并关注 Claude Code 的内核内存泄漏新报告（#95489）。

6. **升级回归常态化，灰度验证是纪律**：Claude Code #95455、Qwen #12224、Copilot #4902 均为新版回归。**生产环境升级前小规模验证、锁定版本、关注回归追踪 issue** 应成为团队标准流程。

7. **国内 Provider 生态崛起**：Pi/Qwen/Kimi/DeepSeek TUI 社区中 GLM、DeepSeek、Qwen Token Plan 相关 PR/Issue 活跃度高，性价比 Coding Plan 正在重塑 CLI 工具的接入格局，值得关注多 Provider 中立架构的工具。

---

*报告基于 2026-09-19 各仓库公开社区动态汇总，反映单日快照，趋势判断需结合更长窗口验证。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告
（数据截止 2026-09-19，来源：anthropics/skills）

> ⚠️ **数据说明**：本次抓取的 PR 评论数均为空（undefined），故“热门”排序依据为 **Issue 讨论热度 + PR 更新活跃度 + 主题相关性** 综合判断，非严格评论数排名。所有列出 PR 状态均为 OPEN。

---

## 一、热门 Skills 排行（活跃 PR）

| # | Skill / PR | 功能 | 讨论热点 | 状态 |
|---|---|---|---|---|
| 1 | **skill-creator 触发评估修复** — [PR #1298](https://github.com/anthropics/skills/pull/1298) | 修复触发评估的假阴性、Windows select() 失败等问题 | 与 [Issue #556](https://github.com/anthropics/skills/issues/556)（0% 触发率，12 条评论）、[Issue #202](https://github.com/anthropics/skills/issues/202)（skill-creator 最佳实践，8 条评论）及 [PR #1769](https://github.com/anthropics/skills/pull/1769) 形成热点集群，是社区最集中的痛点 | OPEN（长期活跃，6 月起持续更新） |
| 2 | **AWT — AI E2E 测试** — [PR #822](https://github.com/anthropics/skills/pull/822) | 赋予 Claude 视觉与浏览器控制能力，零代码生成 E2E 测试 | 测试自动化是社区高需求方向；持续更新至 9/19，仍在打磨 | OPEN |
| 3 | **Pyxel 复古游戏开发** — [PR #525](https://github.com/anthropics/skills/pull/525) | 指导 Agent 用 Python 创建/调试复古游戏，含确定性无头验证 | 创意 + 可验证执行的代表案例；3 月提交至今仍在跟进 | OPEN |
| 4 | **mcp-builder 修复** — [PR #1742](https://github.com/anthropics/skills/pull/1742) | 适配 mcp>=2 的 `streamable_http_client` 重命名与自定义 header | 对应 [Issue #1390](https://github.com/anthropics/skills/issues/1390)（评估脚本 0/N 得分，4 条评论）；配合 [PR #1724](https://github.com/anthropics/skills/pull/1724)（默认模型升级 claude-sonnet-5），mcp-builder 是最常被修的核心 Skill | OPEN（9/17 刚更新） |
| 5 | **blast-radius** — [PR #1776](https://github.com/anthropics/skills/pull/1776) | 批量/破坏性写操作前的检查清单 Skill | 安全治理方向，与 [Issue #412](https://github.com/anthropics/skills/issues/412)（agent-governance 提案）呼应 | OPEN（9 月新鲜提交） |
| 6 | **document-typography** — [PR #514](https://github.com/anthropics/skills/pull/514) | 排版质量控制：孤行、寡行、编号错位 | “AI 生成文档的通病”引发共鸣；同领域还有 [PR #486 ODT](https://github.com/anthropics/skills/pull/486)、[#538](https://github.com/anthropics/skills/pull/538)、[#541](https://github.com/anthropics/skills/pull/541)、[#1734](https://github.com/anthropics/skills/pull/1734) 一批 docx 修复 | OPEN |
| 7 | **Hivemind 多智能体编排** — [PR #1628](https://github.com/anthropics/skills/pull/1628) | Claude 做规划/审查，机械工作委托给免费 headless worker | “昂贵模型的上下文才是稀缺资源”理念受关注；但需注意其绑定竞品 opencode | OPEN |
| 8 | **frontend-design 改进** — [PR #210](https://github.com/anthropics/skills/pull/210) | 提升前端设计 Skill 的清晰度与可执行性 | 官方核心 Skill 的社区迭代，代表“改进型 PR”路线 | OPEN |

---

## 二、社区需求趋势（来自 Issues）

1. **组织级协作与分发**：[Issue #228](https://github.com/anthropics/skills/issues/228)（16 评论，8 👍）——组织内直接共享 Skill 库，取代 Slack 手传 `.skill` 文件；是呼声最高的功能需求。
2. **信任与安全边界**：[Issue #492](https://github.com/anthropics/skills/issues/492)（43 评论，全库最热）——社区 Skill 冒用 `anthropic/` 命名空间造成信任滥用；[Issue #1175](https://github.com/anthropics/skills/issues/1175) 关注 SPO 场景下权限写在 SKILL.md 的安全隐患。**安全是第一大讨论焦点**。
3. **上下文效率**：[Issue #1487](https://github.com/anthropics/skills/issues/1487)——claude-api Skill 一次注入 156k token 灌爆上下文；[Issue #1329](https://github.com/anthropics/skills/issues/1329) 提议 compact-memory 符号化压缩 agent 状态。
4. **评估/触发可靠性**：[#556](https://github.com/anthropics/skills/issues/556)、[#1390](https://github.com/anthropics/skills/issues/1390)——评估脚本在真实环境下全链路失效，社区要求可信的 Skill 质量评测。
5. **质量治理新 Skill 方向**：[#1385](https://github.com/anthropics/skills/issues/1385)（三段式推理质量门禁）、[#412](https://github.com/anthropics/skills/issues/412)（agent-governance）——“元 Skill / 自我治理”类提案密集。
6. **互操作与平台支持**：[#16](https://github.com/anthropics/skills/issues/16)（Skill 暴露为 MCP）、[#29](https://github.com/anthropics/skills/issues/29)（Bedrock 支持）、[#189](https://github.com/anthropics/skills/issues/189)（插件重复安装，9 👍）。

---

## 三、高潜力待合并 Skills（活跃且近期更新）

- [PR #1298](https://github.com/anthropics/skills/pull/1298) & [PR #1769](https://github.com/anthropics/skills/pull/1769) — skill-creator 触发评估双重修复，对应长期 Issue #556/#1721，**合并概率最高、影响面最大**
- [PR #1742](https://github.com/anthropics/skills/pull/1742) — mcp-builder 适配 mcp>=2，修复明确 Issue #1668，典型 bugfix 优先合入
- [PR #1765](https://github.com/anthropics/skills/pull/1765) — Office redlining UTF-8 解码修复（Issue #1707），含波兰语验证，小而确定
- [PR #1776](https://github.com/anthropics/skills/pull/1776) — blast-radius 安全清单，契合社区安全关注主线
- [PR #1703](https://github.com/anthropics/skills/pull/1703) — md2video-audio（Markdown → MP4 + 配音），9 月持续更新中
- [PR #822](https://github.com/anthropics/skills/pull/822) — AWT E2E 测试，活跃至数据截止当日
- ⚠️ 风险项：[PR #1771](https://github.com/anthropics/skills/pull/1771)（proofcore，TON 链上锚定）带有明显商业推广属性，正是 Issue #492 所警惕的信任边界问题，合并存疑

---

## 四、生态洞察（一句话）

> **社区最集中的诉求是“可信”二字——Skill 的安全命名空间治理、触发/评估的可测量性、以及对上下文窗口的克制使用，三者共同指向：Skills 生态正从“能不能用”迈向“能不能被放心地规模化使用”。**

---

# Claude Code 社区动态日报
**日期：2026-09-19 | 数据来源：github.com/anthropics/claude-code**

---

## 一、今日速览

今天最大的新闻是 **AGENTS.md 正式落地**：v2.1.277 发布了社区呼声最高的功能（Issue #6235，5169 👍），项目无 CLAUDE.md 时自动读取 AGENTS.md，与 Codex、Cursor 等工具的生态标准接轨。同日 v2.1.278 发布，auto 模式默认改用服务端分类器，不再收取分类器开销费用。Mods 扩展系统持续密集迭代，diff 面板和 agents-md 模块的多个 PR 合入。

---

## 二、版本发布

### v2.1.278
- auto 模式（Claude API、Enterprise、Bedrock/Vertex/Foundry 及网关用户）默认使用**服务端分类器**，不再收取分类器开销费用；企业部署可通过 `CLAUDE_CODE_AUTO_MODE_SERVER=0` 退回本地分类器。

### v2.1.277
- **新增 AGENTS.md 支持**：项目无 CLAUDE.md 时读取 AGENTS.md，可在 `/config` 的 "Project instructions" 中切换（Bedrock/Vertex/Foundry 暂不支持）。
- 新增 `CLAUDE_GATEWAY_PROXY_IS_EGRESS_BOUNDARY=1` 环境变量，用于出口边界型 Claude 网关。

---

## 三、社区热点 Issues

1. **[#6235] Support AGENTS.md（已关闭）** — 5169 👍 / 400 评论
   社区呼声第一的功能需求今日终于落地（v2.1.277）。AGENTS.md 已成为跨工具编码代理的事实标准，此次支持消除了多工具协作时的指令文件割裂问题。
   🔗 https://github.com/anthropics/claude-code/issues/6235

2. **[#91870] Mods 扩展系统（开放中）** — 121 👍 / 201 评论
   官方确认 Mods 将在数周内发布（含 function hooks）。社区高信号反馈持续塑造设计，这是当前最活跃的功能讨论线程。
   🔗 https://github.com/anthropics/claude-code/issues/91870

3. **[#18435] Claude Desktop 多账户切换（开放中）** — 815 👍 / 192 评论
   桌面端多 profile 管理需求持续高热度，个人/工作账户隔离是重度用户的核心痛点。
   🔗 https://github.com/anthropics/claude-code/issues/18435

4. **[#53247] Windows 桌面端崩溃后无法启动（开放中）** — 98 评论
   崩溃残留 Silo/Job Object 导致 HRESULT 0x80070020，仅注销/重启可恢复。影响 Windows 用户可用性的严重 bug。
   🔗 https://github.com/anthropics/claude-code/issues/53247

5. **[#95489] fswatch 探测重试致内核内存泄漏（新）** — 2 评论
   Windows MSIX 版引擎每秒重试失败探测 ~38,000 次，ntfs.sys 非分页池以 ~230 MB/分钟泄漏直至重启。有 `CLAUDE_CODE_TMPDIR` 临时解法，今日新报告，值得警惕。
   🔗 https://github.com/anthropics/claude-code/issues/95489

6. **[#87647] 6k+ "has repro" Issue 被自动关闭（开放中）** — 49 👍
   元问题：自 2026 年 3 月以来大量带复现步骤的 Issue 被批量自动关闭，反映社区对 issue 治理机制的不满。
   🔗 https://github.com/anthropics/claude-code/issues/87647

7. **[#81472] 复制/粘贴全平台损坏追踪 Issue（开放中）**
   汇总 42 个开放 issue，横跨 TUI、VS Code 扩展、桌面端，是长期未根治的顽疾。
   🔗 https://github.com/anthropics/claude-code/issues/81472

8. **[#77651] 工具调用间的助手文本静默丢失（开放中）** — 11 评论
   interleaved thinking 场景下中间文本不渲染、不持久化到 session jsonl，影响会话回放与审计。
   🔗 https://github.com/anthropics/claude-code/issues/77651

9. **[#77508] Windows 沙箱破坏 Gradle/JVM 回环 IPC（开放中）**
   沙箱内任何使用 NIO Selector 的 JVM 工具启动失败，前序 issue 被关闭未修复。JVM 开发者工作流受阻。
   🔗 https://github.com/anthropics/claude-code/issues/77508

10. **[#95455] v2.1.277 回归：excludedCommands 误拦截带前置 flag 的单命令（新）**
    新版 glob 修复引入回归，`git -C`、`--git-dir` 等形式被沙箱误拦截。升级需注意。
    🔗 https://github.com/anthropics/claude-code/issues/95455

---

## 四、重要 PR 进展

Mods 相关 PR 密集合入（多为 @poteat），显示扩展系统正在冲刺发布：

1. **PR #95409（已合）**：新增 `mods/agents-md` 模块，以与 CLAUDE.md 一致的方式读取 AGENTS.md，受 `instructionFiles` 选项控制。
   🔗 https://github.com/anthropics/claude-code/pull/95409

2. **PR #95417（已合）**：agents-md 模块在 `--bare` 或禁用附件模式下不再附带嵌套 AGENTS.md，行为对齐引擎。
   🔗 https://github.com/anthropics/claude-code/pull/95417

3. **PR #95488（已合）**：diff 停靠面板在打开前先读取仓库，消除 "Loading diff" 空白状态。
   🔗 https://github.com/anthropics/claude-code/pull/95488

4. **PR #95476（已合）**：首次编辑仅在主循环 + checkpointing 开启时自动打开 diff 面板，子代理编辑不再触发。
   🔗 https://github.com/anthropics/claude-code/pull/95476

5. **PR #95423（开放）**：diff 模块跳过只读 shell 命令（ls、git status、cat）后的 diff 重新拉取，降低开销。
   🔗 https://github.com/anthropics/claude-code/pull/95423

6. **PR #94847（开放，@bcherny）**：首次编辑仅在有待展示文件时才打开 diff 面板，避免对仓库外/ignored 文件弹出空面板。
   🔗 https://github.com/anthropics/claude-code/pull/94847

7. **PR #95198（已合）**：diff 模块 `openPane` 返回类型改为 `Promise<unknown>`，为 `$.ui.open` 返回更丰富结果铺路。
   🔗 https://github.com/anthropics/claude-code/pull/95198

8. **PR #51452（已关闭）**：社区贡献的 README 重写，去 AI 腔、修复 npm badge。
   🔗 https://github.com/anthropics/claude-code/pull/51452

---

## 五、功能需求趋势

| 方向 | 信号强度 | 说明 |
|---|---|---|
| **AGENTS.md / 指令文件标准化** | ★★★★★ | 已落地（#6235），mods/agents-md 仍在深化嵌套读取 |
| **Mods 可扩展性** | ★★★★★ | #91870 + 密集 PR，数周内发布 function hooks |
| **桌面端多账户/多 profile** | ★★★★ | #18435（815 👍）长期高热度 |
| **Remote Control / iOS 联动** | ★★★ | 多个新 issue：会话丢失、任务不同步、deep link 失效（#94735、#95407、#95491、#95478） |
| **企业网关/云部署可控性** | ★★★ | 新增 egress boundary、server classifier 退出开关，企业场景配置粒度持续细化 |
| **终端主题定制** | ★★ | #89606 请求透明背景支持 |

---

## 六、开发者关注点

1. **Windows 稳定性是重灾区**：桌面端无法启动（#53247）、内核内存泄漏（#95489、#94198）、沙箱破坏 JVM IPC（#77508）、窗口置顶卡死（#95264）——今日热点 issue 中近半与 Windows 相关。
2. **桌面端自动更新破坏会话**：静默自动更新导致 Remote Control 断连且不恢复（#95491、#95407），更新机制的侵入性引发不满。
3. **静默行为丢失数据**：工具调用间文本不落盘（#77651）、MCP 工具因 allOf/if/then schema 被静默丢弃（#95504）、磁盘 skills 不加载（#95367）——"静默失败"模式降低可调试性。
4. **Issue 治理信任危机**：6k+ 可复现 issue 被自动关闭（#87647）叠加 #47579（Co-Authored-By 无 opt-out），社区对透明度有持续诉求。
5. **升级回归需留意**：v2.1.277 的 excludedCommands 行为变化（#95455）可能影响带前置 flag 的 git 命令沙箱豁免配置。

---
*本日报由 GitHub 公开数据自动汇总生成，仅供参考。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-19

## 1. 今日速览

Codex 持续高频迭代，过去 24 小时内连发 **0.156.0-alpha.6** 等多个 alpha 版本，稳定版 **0.155.1** 修复了 TUI 本地会话因 reasoning summary 导致的请求被拒问题。安全方面，社区对 **越权批量删除导致数据丢失** 的两起事件（#46022、#33624）讨论持续升温，官方同步合并了一批 **沙箱加固 PR**（macOS Seatbelt、Windows 包身份保持）。Windows 平台的沙箱初始化失败（`setup refresh had errors`）仍是最大痛点集群。

---

## 2. 版本发布

### rust-v0.155.1（稳定版）
- **Bug 修复**：新建本地 TUI 会话默认**关闭 reasoning summaries**，解决不支持该能力的 provider 拒绝请求的问题；显式配置的 reasoning-summary 设置仍会被尊重（#46467）
- [Release 链接](https://github.com/openai/codex/releases/tag/rust-v0.155.1)

### Alpha 版本
- **0.156.0-alpha.2 ~ alpha.6** 连发 5 个预发布版本，节奏极快，显示主分支正密集合入功能（与下方大量 PR 对应）

---

## 3. 社区热点 Issues

| # | Issue | 重要性 |
|---|-------|--------|
| 1 | [#40968](https://github.com/openai/codex/issues/40968) Windows 桌面版发送按钮永久转圈，prompt 无法提交 | 评论 42 条，Pro x5 用户无法正常使用，Windows 桌面基础体验问题 |
| 2 | [#33624](https://github.com/openai/codex/issues/33624) 安全提案：Full Access 下批量/家目录删除需硬确认与恢复门控 | 评论 39 条，源于 GPT-5.6 Sol 误删用户家目录的公开事故，安全设计讨论核心帖 |
| 3 | [#24287](https://github.com/openai/codex/issues/24287) 桌面版 UI 卡在 Thinking、Stop 失效、重启后对话不可见 | 评论 32 条，长会话稳定性老问题，👍 14 |
| 4 | [#46022](https://github.com/openai/codex/issues/46022) **[严重数据丢失]** Windows 上 Codex 大规模删除项目范围外数百 GB 文件 | 评论 26 条，最新一起破坏性文件操作越界事件，安全性质严重 |
| 5 | [#43596](https://github.com/openai/codex/issues/43596) Windows Computer Use 无法访问原生应用（空应用清单 + sky RPC 不可用） | 评论 19 条，Computer Use 在 Windows 可用性问题的集中反馈帖 |
| 6 | [#40865](https://github.com/openai/codex/issues/40865) Remote SSH 任务间协调工具失效，0.148 缺少 codex_app MCP 替代 | 评论 18 条，👍 15，远程开发工作流回归 |
| 7 | [#42739](https://github.com/openai/codex/issues/42739) Windows 桌面更新后本地项目从侧边栏消失 | 评论 15 条，升级路径破坏用户数据展示 |
| 8 | [#41942](https://github.com/openai/codex/issues/41942) Windows 生命周期钩子使每次 exec_command 增加约 17-25 秒 | 评论 10 条，A/B 实测 10-16 倍性能退化，性能痛点代表 |
| 9 | [#32477](https://github.com/openai/codex/issues/32477) Windows 下 apply_patch 单行修改前卡顿 40-60 秒 | 评论 10 条，👍 6，跨版本复现，CLI 性能顽疾 |
| 10 | [#28858](https://github.com/openai/codex/issues/28858) Codex 不遵循 MCP `tools/list` 的 `nextCursor` 分页 | 评论 8 条，👍 6，MCP 生态兼容性标准问题，影响工具数多的服务器 |

> ⚠️ 另有 `setup refresh had errors` 沙箱失败集群（[#44696](https://github.com/openai/codex/issues/44696)、[#42513](https://github.com/openai/codex/issues/42513)、[#44425](https://github.com/openai/codex/issues/44425)、[#44309](https://github.com/openai/codex/issues/44309)），是 Windows 平台当前最高频的阻塞性问题。

---

## 4. 重要 PR 进展

| PR | 内容 | 意义 |
|----|------|------|
| [#46583](https://github.com/openai/codex/pull/46583) | macOS Seatbelt 配置中拒绝 XPC service 查询 | 沙箱逃逸面收窄，直接回应当前安全舆情 |
| [#46571](https://github.com/openai/codex/pull/46571) | 保留 macOS Seatbelt 在 scratch 目录中的排除规则 | 修复临时目录隐式授权绕过文件系统限制的漏洞 |
| [#46575](https://github.com/openai/codex/pull/46575) | 为沙箱子进程保留 Windows 包身份 | 修复 Windows 沙箱身份传播，关联 helper 失败集群 |
| [#46577](https://github.com/openai/codex/pull/46577) | 允许 thread 指令 provider 向子代理同步更新 | 解决 subagent 继承指令快照后无法接收更新的问题（呼应 #40865/#42973） |
| [#46573](https://github.com/openai/codex/pull/46573) | 新增独立网络代理二进制 + JSON 配置 | 网络策略代理可脱离完整 Codex 权限配置独立运行 |
| [#46562](https://github.com/openai/codex/pull/46562) | 登录与启动请求增加系统代理回退 | 修复企业代理环境下登录/配置引导失败 |
| [#46561](https://github.com/openai/codex/pull/46561) | 支持显式 provider 模型目录 URL | provider 可独立托管模型元数据，利好第三方接入 |
| [#46574](https://github.com/openai/codex/pull/46574) | TUI 中异步问题到达时通知用户 | 改善长任务下的 TUI 交互体验 |
| [#46580](https://github.com/openai/codex/pull/46580) | Guardian 审查固定在已应用的指令快照上 | 避免审查时读取变更后的指令导致判定偏差，安全相关 |
| [#46566](https://github.com/openai/codex/pull/46566) | 当前线程不可用时仍允许恢复命令 | 修复线程失联阻塞 slash 命令的可用性问题 |

---

## 5. 功能需求趋势

1. **安全与数据保护**（最热）：删除操作的硬确认门控、恢复机制、沙箱逃逸防护（#33624、#46022），官方 PR 已密集响应
2. **Windows 平台可用性**：沙箱 helper、Computer Use、桌面应用稳定性是 Issue 量最大的方向
3. **Computer Use / Browser Use**：Windows 原生应用访问（#43596）、Intel Mac 支持（#42514）、文件上传能力（#20785）
4. **远程 / SSH 开发**：任务间协调与消息委托回归（#40865、#42973）
5. **MCP 生态兼容**：分页支持（#28858）、cua_repl 配置覆盖（#42454）
6. **CLI / TUI 性能**：apply_patch 卡顿、生命周期钩子开销（#32477、#41942）

---

## 6. 开发者关注点

- **数据安全信任危机**：多起越权删除事故后，开发者强烈要求“即使 Full Access 也有破坏性操作防护”，这是当前社区情绪核心
- **Windows 体验明显落后于 macOS**：沙箱初始化失败、性能退化、桌面 Bug 集中爆发，建议 Windows 用户暂缓依赖沙箱的关键工作流
- **性能回归需警惕**：exec_command 与 apply_patch 的秒级到分钟级卡顿在多个 CLI 版本复现，升级前建议小规模验证
- **企业/代理环境**：系统代理回退 PR（#46562）合入后将改善受限网络下的登录与启动
- **版本升级风险**：桌面端多次出现升级破坏现有功能（#42739、#40865），自动更新策略需谨慎

---
*数据来源：github.com/openai/codex · 统计窗口：过去 24 小时*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 · 2026-09-19

## 1. 今日速览

今日发布 v0.62.0-nightly 版本，核心修复了 ConPTY 进程退出生命周期同步问题。社区 PR 方面迎来两项重量级功能落地：**基于文件的持久化任务跟踪系统（替代 WriteToDo）** 和 **AST 感知结构化搜索工具 `ast_search`**，标志着 Agent 能力向“精确导航 + 上下文节约”方向演进。Issue 区焦点仍集中在 Subagent 可靠性与 Auto Memory 安全/质量问题。

---

## 2. 版本发布

**[v0.62.0-nightly.20260919.gcfbcaa8df](https://github.com/google-gemini/gemini-cli/releases)**
- 版本号升级（[#29383](https://github.com/google-gemini/gemini-cli/pull/29383)）
- **fix(core)**: 同步 ConPTY 进程退出生命周期，加固 PTY 输出终结逻辑（Windows 终端下子进程退出相关稳定性修复）

---

## 3. 社区热点 Issues

| # | Issue | 关注理由 |
|---|-------|---------|
| 1 | [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) 🔴P1 | Subagent 达到 `MAX_TURNS` 中断后仍上报 `GOAL success`，掩盖了真实失败——影响任务可靠性的核心问题，13 条评论持续讨论 |
| 2 | [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) 🔴P1 👍8 | Generalist agent 无限挂起，简单操作如建目录也会卡死 1 小时以上，8 个 👍 反映影响面广 |
| 3 | [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) 🔴P1 | Browser subagent 在 Wayland 下完全失败，Linux 桌面用户被阻断 |
| 4 | [#22186](https://github.com/google-gemini/gemini-cli/issues/22186) 🔴P1 | `get-shit-done` output hook 导致 CLI 崩溃 |
| 5 | [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) 🟠P2 | 利用 Gemini 3 原生 bash 能力 + 零依赖 OS 沙箱 + 执行后意图路由，是 agent 执行架构的重要方向讨论 |
| 6 | [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) 🟠P2 | AST 感知文件读取/搜索/映射 EPIC——对应今日 PR #29396，方向已验证落地 |
| 7 | [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) 🟠P2 | 安全问题：Auto Memory 在脱敏前即将 transcript 内容送入模型上下文，要求确定性脱敏 |
| 8 | [#26522](https://github.com/google-gemini/gemini-cli/issues/26522) / [#26523](https://github.com/google-gemni/gemini-cli/issues/26523) 🟠P2 | Auto Memory 对低信号会话无限重试、无效 inbox patch 被静默跳过，记忆系统质量问题集中暴露 |
| 9 | [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) 🟠P2 | 模型几乎从不主动使用自定义 skills 和 subagents，需显式指令才触发——编排能力的实际瓶颈 |
| 10 | [#24246](https://github.com/google-gemini/gemini-cli/issues/24246) 🟠P2 | 工具数超过 128/400 触发 API 400 错误，MCP 重度用户高频踩坑 |

其他值得注意：[#21335](https://github.com/google-gemini/gemini-cli/issues/21335) `/compress` 结果不持久化到 session 文件；[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) agents 目录 symlink 不被识别。

---

## 4. 重要 PR 进展

| # | PR | 内容 |
|---|-----|------|
| 1 | [#29393](https://github.com/google-gemini/gemini-cli/pull/29393) 🏗️XL | **用持久化文件任务跟踪（CRUD + TrackerService）替换 WriteToDo**，解决 context rot 和 token 成本问题（关闭 #18836） |
| 2 | [#29396](https://github.com/google-gemini/gemini-cli/pull/29396) 🏗️XL | **新增 AST 感知 `ast_search` 工具**，支持符号级精确导航，替代整文件读取/猜行号（实现 #22745） |
| 3 | [#29404](https://github.com/google-gemini/gemini-cli/pull/29404) | 新增 `gemini models list` 子命令，支持 JSON 输出，供外部集成发现可用模型 |
| 4 | [#29402](https://github.com/google-gemini/gemini-cli/pull/29402) 🔴P1 | 持久化状态写入改为“临时文件 + fsync + 原子 rename"，防止中断导致 state.json 损坏 |
| 5 | [#29400](https://github.com/google-gemini/gemini-cli/pull/29400) 🔴P1 | 修复 `-r` 恢复会话时 `functionResponse` 重复回放问题 |
| 6 | [#29368](https://github.com/google-gemini/gemini-cli/pull/29368) 🔴P1 | ACP 会话按 ID 加载，即使无可恢复内容也能成功 |
| 7 | [#29201](https://github.com/google-gemini/gemini-cli/pull/29201)（已合） | 修复 TOML 命令多个 `!{...}` 注入时确认循环永不收敛的安全策略问题 |
| 8 | [#29200](https://github.com/google-gemini/gemini-cli/pull/29200)（已合） | MCP 运行时策略统一：空 `mcp.allowed` 改为 fail-closed，企业安全语义对齐 |
| 9 | [#29203](https://github.com/google-gemini/gemini-cli/pull/29203)（已合） | `stripShellWrapper` 支持带额外 flag 的 shell 包装，堵住命令检查绕过口子 |
| 10 | [#29217](https://github.com/google-gemini/gemini-cli/pull/29217)（已合） | 修复 `--model gemini-2.5-flash` 被 `endsWith('flash')` 误匹配后静默升级到 3.5 Flash |

---

## 5. 功能需求趋势

1. **Agent 编排可靠性**（最热）：subagent 挂起、误报成功、不主动调用 skills/子代理——多数字标签为 `area/agent` 的 issue 属于此类
2. **AST 感知工具链**：符号级精确读取/搜索/代码库映射，降低 token 消耗（#22745/#22746/#19561），已进入实现阶段
3. **持久化状态与任务管理**：文件级 CRUD 任务跟踪替代上下文内 todo，跨会话记忆
4. **Auto Memory 安全与质量**：确定性脱敏、低信号过滤、patch 校验（#26525/#26522/#26523 系列）
5. **沙箱化执行**：零依赖 OS 沙箱 + bash 原生能力利用 + 破坏性操作防护（#19873/#22672）
6. **非交互/企业集成**：`models list` JSON 输出、MCP 策略一致性、ACP 会话管理

## 6. 开发者关注点

- **Subagent 黑盒化**：`/bug` 报告不含子代理上下文（#21763），轨迹需经 `/chat share` 才可查看（#22598），调试体验是高频痛点
- **Agent 挂起类问题集中**：#21409、#22465（vite 交互式提示卡死）等，涉及交互式进程处理，与今日 ConPTY 修复方向吻合
- **上下文成本焦虑**：36.6k tokens/turn 基线 + 大文件读取 "firehose"，社区强烈要求精细化读取（Tactful Extraction）
- **配置一致性**：settings.json 覆盖被 Browser Agent 忽略（#22267）、`/compress` 不持久化（#21335），配置语义不一致引发信任问题
- **安全边界**：MCP fail-closed、shell wrapper 绕过、Auto Memory 数据外泄，安全类 PR 近期密集合入，值得企业用户关注

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-19 | 数据来源：github.com/github/copilot-cli**

---

## 1. 今日速览

今日发布 **v1.0.87-0**，引入 Auto routing 层的用户/托管启动默认值（含组织级严格策略），并改进了 steering prompts 的合并与回退编辑体验。社区方面，MCP 生态问题集中爆发——Figma 远程服务器连接失败、OAuth DCR 注册被拒、重连通知刷屏等多个新 Issue 指向 MCP 集成的稳定性短板。昨日一天内新增约 10 条 Issue，会话管理和配置可靠性成为反馈焦点。

---

## 2. 版本发布

### v1.0.87-0
**Added**
- 为 Auto routing 层新增用户级与托管级启动默认值，支持严格模式和用户可覆盖的组织策略
- 同一模式下连续的 steering prompts 会合并为一条待处理消息；在空输入框按 **Up** 可取回编辑（包括粘贴的文本）

---

## 3. 社区热点 Issues

1. **#1632 [CLOSED] Skills 支持子文件夹组织**（👍 24 | 💬 12）
   用户反馈 skills 目录只能扁平结构，10+ 个 skill 难以管理。高票需求已关闭，或已落地。[链接](https://github.com/github/copilot-cli/issues/1632)

2. **#1285 [OPEN] 组织级 Agent 不显示**（👍 13 | 💬 10）
   企业用户在 `.github-private` 仓库中配置的 Agent 无法在 CLI/VS Code 中出现，影响企业级推广，长期未解。[链接](https://github.com/github/copilot-cli/issues/1285)

3. **#4870 [OPEN] Figma MCP 远程服务器加载失败**（👍 11 | 💬 6）
   CLI 将 `server/discover` 返回的 `-32601` 视为致命错误导致工具注册失败，而 VS Code 可正常工作。暴露 CLI MCP 发现逻辑过于严格。[链接](https://github.com/github/copilot-cli/issues/4870)

4. **#1824 [CLOSED] 默认模型选择**（💬 6）
   用户希望自定义默认模型而非每次 Claude Sonnet，已关闭。[链接](https://github.com/github/copilot-cli/issues/1824)

5. **#4765 [OPEN] 非 repo 根目录的配置读取失败**（💬 4）
   工作目录不是 git repo 根时 `.mcp.json` 和 hooks 失效，影响多 repo workspace 用户。[链接](https://github.com/github/copilot-cli/issues/4765)

6. **#1086 [CLOSED] Windows 不应强制 PowerShell**（💬 4）
   cmd 环境下无法运行 `gradlew` 等批处理命令，Windows 兼容性老问题，已关闭。[链接](https://github.com/github/copilot-cli/issues/1086)

7. **#4905 [OPEN] 桌面版会话数分钟后死亡**（💬 3）
   "GitHub credential registration is no longer available" 导致 github-mcp-server 目录过期且致命，影响桌面 app 1.1.22 + CLI 1.0.84-5。[链接](https://github.com/github/copilot-cli/issues/4905)

8. **#4886 [OPEN] `--plugin-dir` skills 未出现在 `/skills` 与 `/env`**（💬 3）
   后端已发现插件 skills 但交互面板不显示，非交互 JSON 输出正常——前后端展示不一致。[链接](https://github.com/github/copilot-cli/issues/4886)

9. **#4900 [OPEN] 并发会话退出时互相覆盖 config.json**（💬 1）
   `trustedFolders` 等托管状态在多会话并发退出时丢失，属于典型的“读-改-写”竞态，可靠性隐患。[链接](https://github.com/github/copilot-cli/issues/4900)

10. **#4902 [OPEN] `-p` 值以 `-` 开头被误解析为 flag**（1.0.85 回归）
    以 `---` 开头的 prompt（如 YAML frontmatter）触发误导性引号报错。[链接](https://github.com/github/copilot-cli/issues/4902)

---

## 4. 重要 PR 进展

过去 24 小时内无 PR 更新，本节省略。

---

## 5. 功能需求趋势

- **MCP 集成稳定性**：今日最密集的主题（#4870、#4905、#4906、#4901、#4907），涵盖发现协议容错、OAuth DCR 注册（`client_name` 被 Figma allowlist 拒绝）、重连通知治理。
- **Skills/插件组织能力**：子文件夹支持（#1632）、工具可调用的 `cwd`（#3035）、插件 skills 展示一致性（#4886）。
- **模型与模式可控性**：默认模型选择（#1824）、Rubber Duck 模式指定模型（#3480）、autopilot 澄清延迟可配置（#4899）。
- **会话管理**：分支型会话 `updated_at` 刷屏侧栏（#4903）、会话元数据不新鲜（#4904）、多会话配置并发写入（#4900）。
- **平台细节体验**：Windows 的 Ctrl+Backspace（#3858）、Linux PRIMARY selection（#4236）、任务栏图标可关闭（#4839）。

---

## 6. 开发者关注点

1. **MCP 是当前最大痛点**：从协议容错（`-32601` 致命化）到 OAuth 兼容性（Figma/Atlassian 均受影响）再到通知噪音，社区呼吁 CLI 对第三方 MCP 服务器更宽容、更透明。
2. **配置与状态可靠性**：非 repo 根目录配置不加载（#4765）、并发覆盖 config.json（#4900）、AGENTS.md 沿符号链接越界加载无关仓库指令（#4822）——多场景下的配置发现与写入逻辑需要系统性加固。
3. **会话规模化体验**：重度用户（60-70 个会话）遭遇侧栏刷屏、元数据失真、压缩失败（#4698）等问题，长会话/多会话是核心使用模式但支持不足。
4. **企业级能力待成熟**：组织级 Agent 分发（#1285）和托管策略（新版的组织级 routing 策略）是企业用户持续关注的两个方向。
5. **平台差异化细节**：Windows（PowerShell 强制、快捷键）和 Linux（剪贴板、bash 5.3 兼容）的“小问题”反复出现，跨平台一致性仍需打磨。

---
*数据截至 2026-09-19，Issues 共 32 条（展示 30 条），PR 0 条。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-09-19 | 数据来源：[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)**

---

## 一、今日速览

今日无新版本发布。社区活动以历史 Issue 的批量关闭为主，官方对积压问题进行了一轮集中清理，涵盖网络代理、HTTP 头校验、安装脚本等多个方向。同时新增 2 条来自 2.0.0 版本的新 Bug 报告（OpenCode Go 400 错误、macOS 粘贴图片回归），显示新版本仍有打磨空间。

---

## 二、版本发布

过去 24 小时无新 Release。

---

## 三、社区热点 Issues

1. **#2653 [OPEN] OpenCode Go 返回 400：缺少 x-opencode-session 头**（新增）
   今日新报，使用 OpenCode Go 提供商时请求全部失败，提示缺少 `x-opencode-session` 头，疑为兼容层适配问题，值得关注后续修复进展。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/2653

2. **#2652 [OPEN] macOS 2.0.0 粘贴图片偶发静默失败（0.43.x 回归）**（新增）
   2.0.0 单文件版（Rust 重写）相对 Python 版 0.43.x 出现回归：剪贴板含图片时 Ctrl+V 偶发无任何反应、无报错。涉及新版核心交互链路，优先级较高。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/2652

3. **#1234 [CLOSED] 环境变量代理在 `kimi login` 时失效**
   aiohttp 默认设置导致基于环境变量的代理不生效，14 条评论、2 👍，是本期讨论热度最高的问题，影响企业网络环境用户，今日关闭。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/1234

4. **#1266 [CLOSED] `platform.version()` 尾部空白导致 HTTP 头校验失败**
   Ubuntu 上的 Connection error 根因之一，与 #1364、#1368 同属“非法 HTTP 头值”问题簇，今日一并关闭，说明该系列修复已落地。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/1266

5. **#1364 / #1368 [CLOSED] Ubuntu 下非法 HTTP 头引发 Connection error**
   内核版本字符串含 `#` 等字符破坏 HTTP 头，多用户复现，是 1.17.0 时代的高频报错，今日关闭。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/1364 ｜ https://github.com/MoonshotAI/kimi-cli/issues/1368

6. **#1680 [OPEN] VSCode 插件独立调节 Kimi 窗口字体大小**
   长期开放的功能请求，用户希望仿照 CodeGeeX 支持面板字体独立缩放，2 👍，反映 IDE 集成体验的细节诉求。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/1680

7. **#1342 [CLOSED] 增加 OSC 9/777 终端任务完成通知**
   请求在任务完成时发出 OSC 转义序列，使 iTerm2、kitty、WezTerm 等终端可弹出桌面通知，对长时间后台任务用户价值大。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/1342

8. **#734 [CLOSED] Google GenAI 提供商对含 $schema 的工具参数报 extra_forbidden**
   使用 Exa MCP + gemini-3-pro 时工具参数校验失败，涉及第三方 provider 兼容性，今日关闭。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/734

9. **#1107 [CLOSED] 安装 sh 脚本在无 uv 环境下有 bug**
   `curl -LsSf https://code.kimi.com/install...` 安装路径的脚本缺陷，影响新用户首次安装体验。
   🔗 https://github.com/MoonshotAI/kimi-cli/issues/1107

10. **#1495 [CLOSED] 支持配置 Plan Mode 生成计划的保存路径**
    请求在 `~/.kimi/config.toml` 增加 `plans_dir` 配置项，属于工作流可定制化需求，已关闭。
    🔗 https://github.com/MoonshotAI/kimi-cli/issues/1495

---

## 四、重要 PR 进展

过去 24 小时仅 1 条 PR 更新：

- **#2176 [OPEN] fix(hooks): UserPromptSubmit hook 从 ContentPart 中提取文本**
  修复 `user_input` 为 `list[ContentPart]`（当前消息的默认格式）时，`UserPromptSubmit` hook 收到空 `prompt` 和 `matcher_value` 的问题——原代码只处理了 `str` 分支，导致正则匹配完全失效。该修复对 hook 生态可用性至关重要，关联 Issue #2148，自 5 月提交至今仍待合入。
  🔗 https://github.com/MoonshotAI/kimi-cli/pull/2176

---

## 五、功能需求趋势

从本期 Issue 可提炼出以下方向：

- **IDE 集成体验深化**：VSCode 插件字体独立调节（#1680）、Plan 保存路径可配置（#1495）、Web UI 布局修复（#1302）——用户对插件端的精细化定制需求持续增长。
- **第三方 Provider / 协议兼容**：OpenCode Go 会话头（#2653）、Google GenAI 参数校验（#734）、MCP 断连容错（#1296），多提供商接入的健壮性是高频议题。
- **终端原生体验**：OSC 桌面通知（#1342）、ghostty 浅色主题可辨识性（#1301），体现 CLI 深度用户对终端集成细节的追求。
- **网络环境适配**：代理支持（#1234）、IPv6 环境（#1371）、HTTP 头清洗（#1266/#1364/#1368），企业及特殊网络环境稳定性需求集中。

---

## 六、开发者关注点

1. **2.0.0 版本回归风险**：Rust 单文件版相较 Python 版出现粘贴图片回归（#2652），迁移期质量保障是当前焦点。
2. **Hook 系统可用性**：PR #2176 暴露 hook 对结构化输入（ContentPart）支持不足，且修复等待周期较长（4 个月+）。
3. **企业网络环境兼容**：代理、IPv6、防火墙场景下连接失败类 Issue 占比显著，虽有批量关闭，但反映出网络层默认配置需更鲁棒。
4. **安装与上手体验**：安装脚本 bug（#1107）影响零基础用户首触，低门槛安装仍是获取用户的关键环节。

---
*本日报由 GitHub 公开数据自动汇总生成，仅反映过去 24 小时动态。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-19

## 一、今日速览

今日无新版本发布，但社区活动极为活跃：桌面端迎来一波密集的质量优化（启动性能、内存泄漏修复、文件制品展示），同时 **v2 迁移期的数据兼容性问题**开始集中暴露（V1→V2 会话导入器跳过部分旧会话、CLI 时间戳开关缺失）。Zen API 的 `encrypted_content` 报错是当前最热的开放问题，影响 Muse Spark 1.3 用户。

---

## 二、版本发布

过去 24 小时无新 Release。（注：PR #49874 已将 Console 安装链接全面切换至 v2，暗示 v2 正在成为默认分发版本。）

---

## 三、社区热点 Issues

1. **Zen API CORS 预检 404，阻塞所有浏览器客户端** [#31041](https://github.com/anomalyco/opencode/issues/31041)（已关闭，12 评论 / 11 👍）
   Zen 全部端点在 OPTIONS 预检时返回 404 HTML，导致浏览器端无法调用 API。POST 本身正常，纯路由层问题。今日有关键进展并关闭，浏览器生态接入者需关注。

2. **Zen 调用报 `encrypted_content was not issued to this caller`** [#48973](https://github.com/anomalyco/opencode/issues/48973)（开放中，8 评论）
   Muse Spark 1.3 + OpenCode Zen 组合下高频触发，是当前最活跃的开放问题，疑似与推理内容的加密绑定/会话路由有关。

3. **/compact 落地“纯推理空摘要”，导致不可逆的上下文丢失** [#44080](https://github.com/anomalyco/opencode/issues/44080)（开放中）
   compact 模型只返回 reasoning 无正文时，系统仍标记压缩成功并销毁原始历史。数据安全问题，风险高。

4. **V1→V2 会话导入器为一次性任务，遗漏后续创建的旧版会话** [#49641](https://github.com/anomalyco/opencode/issues/49641)（开放中）
   v2.0.7 迁移后，首次 V2 启动之后由 1.x 创建的会话永远丢失。v2 升级用户的核心痛点。

5. **CLI v2.0.8 缺失消息时间戳开关** [#49742](https://github.com/anomalyco/opencode/issues/49742)（开放中）
   v1.18.31 的 Ctrl+P 时间戳切换在 v2 中消失，属于迁移期功能回退的典型反馈。

6. **多实例间会话消息串扰** [#38008](https://github.com/anomalyco/opencode/issues/38008)（已关闭）
   多个 OpenCode 实例并行时消息互相泄漏，与 provider 无关。今日关闭，多开工作流的用户建议验证修复。

7. **并行子代理“一损俱损”** [#37315](https://github.com/anomalyco/opencode/issues/37315)（已关闭）
   一个子代理卡死会中止全部并行任务，成功完成的也被丢弃。与 #37959 同源，均于今日关闭，并行编排稳定性显著改善的信号。

8. **取消后仍执行子进程工具调用** [#33364](https://github.com/anomalyco/opencode/issues/33364)（已关闭）
   SIGINT 中断后 OpenCode 仍继续派生子进程工具，涉及安全与控制权边界，今日关闭。

9. **TUI 黑屏：渲染循环静默卡死** [#37803](https://github.com/anomalyco/opencode/issues/37803)（已关闭）
   发送 prompt 后 TUI 全黑但进程存活，切终端 tab 可恢复。TUI 渲染稳定性的长期问题今日了结。

10. **网络受限环境下的内置代理支持（Feature）** [#37993](https://github.com/anomalyco/opencode/issues/37993)（已关闭）
    面向受限网络用户的代理自动启停方案，对国内开发者群体尤其重要，今日关闭值得关注后续落地形式。

---

## 四、重要 PR 进展

1. **feat(app): agent 引用的文件以富媒体标签页打开** [#49882](https://github.com/anomalyco/opencode/pull/49882)
   解决截图/报告/CSV 等制品链接被 DOMPurify 剥离或被当文本渲染的问题，大幅改善桌面端产物浏览体验。

2. **feat(tool): 支持 non-UTF8 文件编码** [#49881](https://github.com/anomalyco/opencode/pull/49881)
   `edit`/`write`/`apply_patch` 此前强制按 UTF-8 解码，GBK/Shift-JIS/Big5 文件会被静默损坏——对中日韩用户是重量级修复。

3. **fix(core): glob 结果排除隐藏文件** [#48894](https://github.com/anomalyco/opencode/pull/48894)
   `**/*.ts` 会匹配到 `.hidden.ts`，修复工具语义与常规 glob 预期不一致的问题。

4. **fix(cli): 启动连接失败时报告版本不匹配** [#49886](https://github.com/anomalyco/opencode/pull/49886)
   将晦涩的 `UnknownError: Effect.tryPromise` 替换为真实原因（连接失败 / 服务器版本不匹配），改善诊断体验。

5. **perf(desktop): 渲染器启动期间显示上一个 shell** [#49890](https://github.com/anomalyco/opencode/pull/49890)
   消除首窗口白屏，桌面启动性能专项（配合 #49872 的启动阶段打点）持续推进中。

6. **fix(app): 修复失败发送被历史记录 retained 导致的内存泄漏** [#49717](https://github.com/anomalyco/opencode/pull/49717)（已合并）
   来自生产环境堆快照：3×51MB toast 字符串 + 38MB 附件泄漏，实测驱动的优化典范。

7. **perf(app): 移除 luxon 依赖** [#49876](https://github.com/anomalyco/opencode/pull/49876)（已合并）
   仅三处日期操作就背上 68KB 依赖，替换后主包显著瘦身。

8. **refactor(schema): provider 与 model 设置拆分为独立契约** [#49850](https://github.com/anomalyco/opencode/pull/49850)（已合并）
   v2 公共 schema 持续重构的一部分；配套的 [#49883](https://github.com/anomalyco/opencode/pull/49883) 将 `providerState` 重命名为 `state`（保留旧字段兼容解码）。

9. **fix(app): `opencode://new-session` 路由至新布局下的草稿** [#49875](https://github.com/anomalyco/opencode/pull/49875)
   一并修复 #44160 / #35225，取代了机制本身失效的旧 PR #49657。

10. **feat(console): 安装链接全面切换至 v2** [#49874](https://github.com/anomalyco/opencode/pull/49874)（已合并）
    文档导航指向 `/v2/docs`、GitHub 指向 `v2` 分支——v2 正式成为默认版本的明确信号。

---

## 五、功能需求趋势

- **v2 迁移兼容性**：会话导入遗漏（#49641）、功能回退（#49742）、schema 重构（#49850/#49883），迁移期问题是当前最大主题。
- **桌面端体验与性能**：启动白屏、内存泄漏、文件制品展示、通知恢复窗口状态（#35444）——桌面端进入精细化打磨阶段。
- **受限网络/本地化支持**：内置代理（#37993）、桌面菜单 i18n（#35601）、非 UTF-8 编码（#49881），非英语/受限环境用户声量上升。
- **上下文与压缩可控性**：compact 空摘要数据丢失（#44080）、默认关闭自动压缩（#38018），用户要求对上下文销毁有更多控制权。
- **多代理编排稳定性**：并行子代理失败传播（#37315/#37959）今日双双关闭，说明社区在该方向的反馈已被消化。

---

## 六、开发者关注点

1. **Zen 服务可靠性**：CORS 404（已修）与 `encrypted_content` 报错（未修）叠加，Zen 付费用户对服务端稳定性信心承压。
2. **数据安全边界**：compact 不可逆销毁历史（#44080）与取消后仍执行工具（#33364）表明“破坏性操作的防护”仍是薄弱点。
3. **错误信息可诊断性**：从静默错误（#37939）到 Effect 包装异常（#49886），社区持续抱怨排障困难，相关修复正在落地。
4. **订阅/计费稳定性**：Go 订阅异常停用（#38025）偶发但影响付费信任。
5. **多实例与状态隔离**：会话消息串扰（#38008）已修，但提示本地状态管理仍是复杂度热点。

---
*数据来源：github.com/anomalyco/opencode · 统计窗口：过去 24 小时*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-19

## 一、今日速览

Qwen Code 发布 **v0.24.1-preview.0** 预览版，主要修复 CI 打包问题并记录 ACP 边界验收文档。社区热度集中在 v0.24.0 的回归 Bug 上：`/cd` 命令失效（P1）、LSP 非 ASCII 响应静默丢弃（P1）和 Web Terminal PTY 不可用（P1）成为最受关注的三大问题。同时，桌面端 node-pty 打包修复 PR（#12225）和 Chrome 多会话共享（#12229）等新功能持续推进。

---

## 二、版本发布

### v0.24.1-preview.0
- **docs(serve)**: 记录已合并的 ACP 边界验收（PR #12024，@wenshao）
- **fix(ci)**: 打包前等待导出的 renderer 发布完成
- 同日发布 nightly: `v0.24.0-nightly.20260918.537311b8a5`，内容一致

🔗 https://github.com/QwenLM/qwen-code/releases/tag/v0.24.1-preview.0

---

## 三、社区热点 Issues

1. **[#11872] Web Terminal 报 "PTY not available"（P1，10 条评论）**
   `@lydell/node-pty` 已声明但未打包进 Desktop 运行时，macOS 代码签名又阻止本地 prebuild 加载，导致 Web 终端完全不可用。今天对应的修复 PR #12225 已提交，形成 Issue-PR 闭环。
   🔗 https://github.com/QwenLM/qwen-code/issues/11872

2. **[#12224] v0.24.0 后 `/cd` 命令失效（P1，5 条评论）**
   升级到 0.24.0 后，即使无活跃会话，`/cd` 也报 "response or tool call is in progress"。新版本回归 Bug，影响面广，社区反馈积极。
   🔗 https://github.com/QwenLM/qwen-code/issues/12224

3. **[#12206] LSP 非 ASCII 响应被静默丢弃（P1）**
   Content-Length 字节数与 UTF-16 字符串长度比较错误，导致含中文的 LSP 响应返回空结果（如 Markdown 中文标题的 documentSymbol）。对中文用户影响尤甚。
   🔗 https://github.com/QwenLM/qwen-code/issues/12206

4. **[#12053] Goal 运行时瘦身提案（P2，8 条评论）**
   基于真实 `/goal-draft` 会话证据，提出仅凭当前回合证据判断完成、移除证据目录与 checkpoints，是 Goal 子系统演进的方向性讨论。
   🔗 https://github.com/QwenLM/qwen-code/issues/12053

5. **[#11783] TUI 因 React error #185 崩溃（P1）**
   注册后台 shell 任务数秒后触发 "Maximum update depth exceeded"，TUI 进程直接死亡，稳定性问题严重。
   🔗 https://github.com/QwenLM/qwen-code/issues/11783

6. **[#12028] 非对话上下文 Token 治理（P2）**
   系统提示、内置工具 schema、QWEN.md、skills 列表每次请求都要付费，在长上下文模型上可能远超对话本身，是 context 性能 roadmap 的跟踪 Issue。
   🔗 https://github.com/QwenLM/qwen-code/issues/12028

7. **[#12165] MCP OAuth 丢失 registrationUrl（P2）**
   WWW-Authenticate 发现过程丢弃 registrationUrl，导致 Atlassian 远程 MCP 无法完成 OAuth 认证，集成类问题代表。
   🔗 https://github.com/QwenLM/qwen-code/issues/12165

8. **[#12212] Session writer 残留 claim 导致永久 503（P2）**
   daemon 非优雅退出后，多种不同故障共享同一个 errorKind，残留 `.claim` 使会话永久不可服务。配套的还有启动时锁目录清单提案 #12213 和文档补充 #12214。
   🔗 https://github.com/QwenLM/qwen-code/issues/12212

9. **[#12216] MCP workspace 发现导致 ACP 进程双份 LSP 服务器（P2）**
   `qwen serve` 给每个 ACP 子进程传 `--experimental-lsp`，叠加 MCP workspace 发现逻辑后启动两套完整 LSP 服务器，资源浪费。
   🔗 https://github.com/QwenLM/qwen-code/issues/12216

10. **[#12223] 项目级权限规则应覆盖用户级规则（已关闭，4 条评论）**
    提出按配置作用域和目标特异性解决权限冲突，而非全局 `deny > ask > allow`。与 #12226（文件系统作用域权限权威）共同反映企业级权限管理的诉求。
    🔗 https://github.com/QwenLM/qwen-code/issues/12223

---

## 四、重要 PR 进展

1. **[#12225] Desktop 运行时打包 node-pty prebuild**（@yiliang114）
   将 `@lydell/node-pty` 及 prebuild 打入 Desktop 的 `lib/node_modules`，附带真实 PTY spawn 冒烟测试——直接修复今日最热的 #11872。
   🔗 https://github.com/QwenLM/qwen-code/pull/12225

2. **[#12229] browser-use 支持多会话共享 Chrome profile**（@tanzhenxin）
   多个 Qwen 会话可同时驱动同一 Chrome profile，tab 归属隔离并引入 `TAB_OWNERSHIP_CONFLICT` 冲突检测。
   🔗 https://github.com/QwenLM/qwen-code/pull/12229

3. **[#11874] `qwen batch` 命令 + headless `--batch` 模式**（@yiliang114）
   对接 DashScope Batch API（半价、独立配额），支持 submit/status/fetch/cancel，适合大批量单轮任务。
   🔗 https://github.com/QwenLM/qwen-code/pull/11874

4. **[#12198] 未决信任的工作区默认不信任**（@yiliang114）
   启用 folder trust 时，无信任决策的工作区以不信任状态启动，禁用项目设置/环境文件/hooks——安全加固的重要一步。
   🔗 https://github.com/QwenLM/qwen-code/pull/12198

5. **[#12067] bwrap 执行基础设施**（@doudouOUC）
   为规划中的工具级 Linux 沙箱打地基：结构化启动、bwrap 适配器、进程监督与受限二进制 worker。
   🔗 https://github.com/QwenLM/qwen-code/pull/12067

6. **[#12119] `/context` 分类总和等于 provider 总量**（@yiliang114）
   重做 `/context` 分解，按内容划分请求并精确对齐 provider 上报总量，skills 行纳入实际发送的 listing——配合 #12028 的 token 治理。
   🔗 https://github.com/QwenLM/qwen-code/pull/12119

7. **[#11859] 全面切换 pnpm，退役 package-lock.json**（@yiliang114）
   CI 与发布统一使用固定版本 pnpm，确保测试与发布的依赖图一致。
   🔗 https://github.com/QwenLM/qwen-code/pull/11859

8. **[#10943] `qwen --bg` 启动后台 Agent View 会话**（@yiliang114）
   后台会话独立于启动 shell 存活，为后台 agent 生态铺路（配套 #10954 的 `GET /background-agents` API）。
   🔗 https://github.com/QwenLM/qwen-code/pull/10943

9. **[#12115] Linux 独立安装包预检 glibc**（@dijedontahiri）
   CentOS 7 等旧发行版上，安装器现在能在安装前检测 glibc 兼容性，避免装完才报 GLIBC 符号缺失。
   🔗 https://github.com/QwenLM/qwen-code/pull/12115

10. **[#12228] Vim 模式支持 operator-pending 查找/行内 motion**（@josephgimenez）
    `d/c/y` 现可与 `t/f/T/F`、`$`/`0`/`^` 组合，编辑可用 `.` 重复——TUI 编辑体验的持续打磨。
    🔗 https://github.com/QwenLM/qwen-code/pull/12228

---

## 五、功能需求趋势

- **会话/daemon 稳定性**：非优雅退出恢复、session writer 锁治理（#12212/#12213/#12214）、会话恢复误报（#11995）——daemon 架构成熟期的集中诉求。
- **Token 与上下文效率**：非对话上下文开销治理（#12028）、`/context` 精确分解（#12119），长上下文模型成本可见性成为焦点。
- **企业级权限与安全**：作用域化权限规则（#12223/#12226）、工作区信任默认收紧（#12198）、部署托管扩展目录（#12147）。
- **IDE/ACP 集成**：Zed 中 AskUserQuestion 显示原始输入（#11361）、ACP 与 LSP 双启动问题（#12216）、MCP OAuth 兼容性（#12165）。
- **Goal 子系统瘦身**：#12053 及 ladder 系列（#12179）推动运行时简化。
- **批量与后台执行**：Batch API 集成（#11874）、后台 agent 可观测（#10943/#10954）。

---

## 六、开发者关注点

1. **v0.24.0 回归风险**：`/cd` 失效（#12224）、PTY 缺失（#11872）等升级即触发的 Bug 是当前最直接的痛点，建议关注 v0.24.1 正式版再升级 Desktop/Web 场景。
2. **中文/CJK 场景缺陷**：LSP 非 ASCII 响应丢弃（#12206）对中文用户是静默失败，排查成本高，需优先修复。
3. **错误可观测性不足**：LSP 失败被吞为空数组（#12220）、session writer 多种故障共享同一错误码（#12212）、node-repl 缺分号报内部标识符错误（#12167）——用户普遍反映“静默失败比崩溃更难排查”。
4. **TUI 稳定性**：React #185 崩溃（#11783）、工具取消路径的清理遗漏（#11162/#11148）表明交互式渲染和调度层仍需加固。
5. **国际化细节**：session recap 强制英文（#11847），与多语言用户体感相关。

---
*数据截至 2026-09-19，来源：github.com/QwenLM/qwen-code*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (Codewhale) 社区动态日报 — 2026-09-19

## 1. 今日速览

今日社区活跃度集中在 **Runtime API、Provider 扩展与 CI 修复**三大方向。 [@Hmbown](https://github.com/Hmbown) 一天内连发多个重量级 PR：Runtime API 终端字节流与断线恢复（#6361）、CSDN 星图 Provider 接入（#6353）、修复 main 分支 CI 红灯（#6354）。Issues 侧，引擎运行中静默冻结（#6184）和 ACP 模式忽略 sandbox 配置（#6310）是当前最受关注的用户痛点。

## 2. 版本发布

过去 24 小时无新 Release。

## 3. 社区热点 Issues

1. **[Issue #6184](https://github.com/Hmbown/Codewhale/issues/6184) — 引擎运行中静默冻结（6 评论）**
   长、重工具调用的运行中引擎突然停止产出，用户消息被持久化但无任何回应，无错误、无日志、无崩溃记录。这是影响生产使用的严重 bug，属当前最高优先级的用户痛点。

2. **[Issue #6310](https://github.com/Hmbown/Codewhale/issues/6310) — `serve --acp` 忽略 config.toml 的 sandbox_mode/ask（4 评论）**
   ACP 会话被卡在 Work posture，配置不生效。随着 IDE 集成（Zed、JetBrains 等 ACP 宿主）推进，ACP 路径的配置一致性愈发关键。

3. **[Issue #6011](https://github.com/Hmbown/Codewhale/issues/6011) — Token 计量与工具调用诊断（9 评论）**
   按组件/模型统计 token、缓存命中率、压缩成本及工具调用错误模式。属于 Core 计划 C11，是可观测性方向的核心需求。

4. **[Issue #6015](https://github.com/Hmbown/Codewhale/issues/6015) — 自适应 anti-stall + 只读 shell 语法扩展（9 评论）**
   自适应反卡死与更宽的安全只读 shell 命令白名单（默认行为，非按用户配置），已纳入 Core 计划 C05/C06。

5. **[Issue #5587](https://github.com/Hmbown/Codewhale/issues/5587) — 死代码清扫 Phase 2-4（9 评论）**
   对 crates/tui 中全部 379 处 `allow(dead_code)` 做全量审计分类，Phase 1 已落地。反映项目正在系统性偿还技术债。

6. **[Issue #6142](https://github.com/Hmbown/Codewhale/issues/6142) — 合并两套 MCP 客户端栈（5 评论）**
   `tui/src/mcp`（13.2k 行）与 `crates/mcp`（4.5k 行）功能重复，app-server 与 engine 各用一套，是 0.9.14 重构重点。

7. **[Issue #6187](https://github.com/Hmbown/Codewhale/issues/6187)（已关闭）— MCP 无连接监管**
   MCP server 中途死亡仍显示 "connected"，直到下次调用失败才暴露，无自动重连。已修复关闭，是 MCP 可靠性提升的标志。

8. **[Issue #6309](https://github.com/Hmbown/Codewhale/issues/6309)（已关闭）— “我想找回 YOLO 模式”**
   用户因 DeepSeek V4 Flash 在 terminalbench 高分而重度使用，但苦于每次审批点击。引发关于审批粒度/自动批准的热议，已关闭（应有解决方案落地）。

9. **[Issue #6050](https://github.com/Hmbown/Codewhale/issues/6050) — 可插拔 Agent 记忆后端（4 评论）**
   社区请求 `MemoryBackend` 支持第三方实现（causal-memory / mem0），目前仅有 Native/Off 两种硬编码变体。

10. **[Issue #6035](https://github.com/Hmbown/Codewhale/issues/6035) — Model pin 不随 Provider 迁移传播**
    模型 id 在至少 6 处独立固定，厂商下线旧 id（如 DeepSeek 弃用 `deepseek-v4-flash`）后 fleet 成员和 agent profile 仍持有失效 id，无迁移机制。

## 4. 重要 PR 进展

1. **[PR #6361](https://github.com/Hmbown/Codewhale/pull/6361)（Open）— Runtime API：终端字节流 + 流恢复 + 幂等提交**
   一次性解决 App 侧追踪的三个 Core unblock：认证字节输入/输出、resize、有界回放，以及断线后的流恢复与幂等提交。

2. **[PR #6353](https://github.com/Hmbown/Codewhale/pull/6353)（Closed，已合入）— 新增 CSDN 星图 Provider**
   接入 CSDN OpenAI 兼容端点，默认绑定 Coding Plan 专属模型 `glm_for_coding`，支持其市场透传模型 id。Provider 生态持续扩张。

3. **[PR #6354](https://github.com/Hmbown/Codewhale/pull/6354)（Closed）— 修复 main 分支 CI 红灯**
   两个独立缺陷：`check-blocking-calls-budget` 在 push 时才致命、mcp stdio 测试在负载 runner 上才触发竞态。PR rollup 中不可见的典型 CI 问题。

4. **[PR #6350](https://github.com/Hmbown/Codewhale/pull/6350)（Closed）— 清除 Provider 中立机制中的 DeepSeek 化石命名**
   `DeepSeekClient` → `CodewhaleClient`，`deepseek_base_url` → `active_route_base_url`。代码去单供应商化的里程碑。

5. **[PR #6347](https://github.com/Hmbown/Codewhale/pull/6347)（Closed）— codewhale-main 栈扩至 32 MiB**
   修复自 9 月 16 以来每个 PR ubuntu 测试腿必挂的问题：debug 模式下 poll 链过深导致栈溢出，TUI 进程在插件信任确认后死亡。

6. **[PR #6352](https://github.com/Hmbown/Codewhale/pull/6352) / [#6351](https://github.com/Hmbown/Codewhale/pull/6351)（Closed）— Shoreline 主题令牌导出到 Web**
   之前 web 端手维护 `--gpui-*` 镜像已漂移；现在从生成的 Shoreline 令牌统一导出，TUI/GPUI/Web 三端主题单一来源。

7. **[PR #6349](https://github.com/Hmbown/Codewhale/pull/6349)（Closed）— Windows crate 分组升级**
   `windows` 与 `windows-core` 必须同步升级，否则 BOOL/HRESULT 成为两种类型导致编译失败——对 dependabot 分组策略的重要修正。

8. **[PR #6348](https://github.com/Hmbown/Codewhale/pull/6348)（Closed）— Windows 路径规范化测试修复**
   修复 `\\?\` verbatim 前缀导致的断言路径不一致，Windows CI 腿恢复绿色。

9. **[PR #5752](https://github.com/Hmbown/Codewhale/pull/5752)（Closed）— Cloud facts 通道 Slice 1**
   Supabase 支撑的签名+版本化+缓存的 facts 通道（模型目录增量、Provider 默认值、发布公告），默认关闭，是云端联动基础设施。

10. **[PR #6359](https://github.com/Hmbown/Codewhale/pull/6359)（Open）— windows-core 0.62 → 0.100 分组升级**
    大版本跨越，配合 #6349 的分组策略推进。另有 #6355–#6360 等一批 dependabot 例行升级（wrangler、autoprefixer、nixpkgs 等）。

## 5. 功能需求趋势

- **Fleet / 多 Agent 管理**：#5479、#5915、#6035 持续演进——子 agent 实时状态面板、provider→model→shortlist→role 的角色分配流程、model pin 迁移。
- **可观测性与计量**：#6011（token 计量/缓存命中率）、#6315（子 agent 用量持久化）、#6193（运行时性能门禁）——社区要求“看得见、可防御”的性能与成本。
- **IDE / ACP 集成**：#5835（ACP 跑在完整 thread/turn 运行时）、#6088（消除 acp_server.rs 第二轮询循环）、#6310（ACP 配置一致性）。
- **Provider 生态扩张**：#6029（Provider 中立的厂商选择）、#6035（模型 id 迁移）、今日合入的 CSDN 星图——从 DeepSeek 单一走向多 Provider 中立。
- **Agent 记忆体系**：#6050（可插拔记忆后端）、#6086（scratchpad + 三存储统一寻址）。
- **代码工程质量**：#6142（MCP 栈合并）、#6143（Config 单一权威）、#6151（依赖去重）、#5587（死代码清扫）——0.9.14 是明确的“重构清债版”。

## 6. 开发者关注点

- **稳定性静默失败最伤信任**：#6184 引擎无日志冻结、#6187 MCP 假连接——开发者反复强调“没有错误信息的失败最难排查”。
- **审批流程繁琐**：#6309 的 YOLO 模式诉求代表重度终端用户希望有更粗粒度/可配置的自动批准选项。
- **配置碎片化**：模型 id 六处固定（#6035）、双 Config 实现（#6143）、双 MCP 栈（#6142）——配置权威不统一导致的漂移是高频问题根源。
- **编辑工具锚定失败**：#6203 指出 `edit_file` 的主要失败模式是文本匹配锚定而非语法，社区期待 AST 级 `edit_symbol`。
- **远程开发场景**：#6158 SSH 远程工作空间，创始人定调“SSH 应是基本能力而非 workaround”。
- **CI 可靠性**：main 红灯（#6354）、栈溢出挂测试（#6347）说明 CI 环境特异性问题正在消耗维护精力，本周多个 PR 致力于恢复绿灯。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 社区动态日报 · 2026-09-19

## 📰 今日速览

今日无新版本发布，但社区活跃度很高：过去 24 小时内 72 条 Issues 有更新、20 个 PR 有进展。Windows 生态问题仍是讨论焦点（#7547 单帖 64 条评论），当天涌现多个高质量修复 PR，包括 `/retry` 命令、歧义 session 前缀拒绝、TUI 崩溃防护等，多项已快速合并。

---

## 🔥 社区热点 Issues

**1. [#7547](https://github.com/earendil-works/pi/issues/7547) — Windows 使用方式调研（64 评论）**
官方发起的调研帖，旨在厘清 Windows 上运行 Pi 的多种方式，决定核心支持与外部托管的边界。持续一个月仍是讨论中心，Windows 体验显然是当前战略重点。

**2. [#6278](https://github.com/earendil-works/pi/issues/6278) — 新 Claude 模型与 edit 工具兼容性差（25 评论，👍10，已关闭）**
LLM 自造额外字段导致约 20% 编辑失败。已随修复关闭，但揭示了新版模型下工具 schema 校验宽容度的普遍课题。

**3. [#7730](https://github.com/earendil-works/pi/issues/7730) — macOS 长会话 CPU 飙升（16 评论，👍10）**
长会话下 CPU 在 50–110% 波动、内存 600–800MB，疑似与上下文规模相关，性能问题中受关注最高。

**4. [#8928](https://github.com/earendil-works/pi/issues/8928) — 并行启动时 48 秒误报 "No API key found"（11 评论）**
作者提供了确定性复现：过期 OAuth 凭据在多进程场景下锁住了鉴权。对 CI/自动化用户影响显著。

**5. [#8684](https://github.com/earendil-works/pi/issues/8684) — `PI_OFFLINE` 实际禁用全部模型发现（11 评论）**
文档说只关 housekeeping，实际连整个会话的 provider 模型目录网络发现都关了——文档与行为不一致的典型案例。

**6. [#9549](https://github.com/earendil-works/pi/issues/9549) — 全屏模式大转录每帧重渲染（5 评论）**
Windows 2 核机器上每次 resize 重发整个 transcript、打满单核。报告由用户本地 Pi 代理起草并披露，社区协作模式值得注意。

**7. [#9652](https://github.com/earendil-works/pi/issues/9652) — Claude Fable 拒绝压缩，因 thinking 块被转写进摘要（6 评论）**
`serializeConversation` 把 thinking 块转写进 prompt 触发 Anthropic 分类器拒绝。与 #9391、#9602 同属“thinking 块生命周期管理”这一系统性问题簇。

**8. [#9361](https://github.com/earendil-works/pi/issues/9361) — Windows shellPath 非确定性失效，回退到 WSL bash.exe（8 评论）**
加载扩展后 `shellPath` 被忽略，最终可能执行 WSL System32 的 bash——隐蔽且危险的路径解析问题。

**9. [#9740](https://github.com/earendil-works/pi/issues/9740) — 阈值压缩静默失效（已关闭）**
最新一轮工具结果超过 `keepRecentTokens` 时压缩静默 no-op，运行中不可见，结束后才补做。当天报告当天关闭，响应很快。

**10. [#9718](https://github.com/earendil-works/pi/issues/9718) — `--print` 输出预算耗尽时 exit 0 且零输出**
脚本调用方无法区分“模型没产出”和“预算用尽”——对自动化管道是实际的可用性陷阱。

---

## 🔀 重要 PR 进展

**1. [#9744](https://github.com/earendil-works/pi/pull/9744) — 新增 `/retry` 命令（已合并）**
重连重试耗尽后可恢复被放弃的 turn，本地 LLM 用户（llama-server 重启等场景）的刚需。

**2. [#9734](https://github.com/earendil-works/pi/pull/9734) — 拒绝歧义 `--session` 前缀（已合并）**
此前匹配多个会话时静默打开最近的，可能污染错误的 session 文件；现改为列出候选并退出。

**3. [#9762](https://github.com/earendil-works/pi/pull/9762) — TUI 防护无 content 数组的工具结果（已合并）**
扩展返回不规范结果对象会导致整个 TUI 进程崩溃，现已加防护。扩展生态健壮性的重要补丁。

**4. [#9738](https://github.com/earendil-works/pi/pull/9738) — 溢出重试前 flush 延迟自定义消息（已合并）**
修复 `session_compact` 处理器在自动压缩重试路径上的挂起消息丢失。

**5. [#9736](https://github.com/earendil-works/pi/pull/9736) — 无差别重试未到终止事件的流截断（已合并）**
统一按事件类型而非错误措辞判断重试，代理/中转场景更稳。

**6. [#9668](https://github.com/earendil-works/pi/pull/9668) — 提示缓存保温（实验性，进行中）**
@mitsuhiko 出品，目前仅限 Anthropic 显式缓存。长会话成本优化方向值得关注。

**7. [#9096](https://github.com/earendil-works/pi/pull/9096) — Meta Muse 订阅 provider（进行中）**
OAuth + 每日重铸 token 的特殊机制，“伪流式”突发输出，是新 provider 接入的代表。

**8. [#9434](https://github.com/earendil-works/pi/pull/9434) — 允许扩展追加 session 系统提示词（进行中）**
append-only 的 `systemPromptAppend` 机制，扩展能力的又一扩展点。

**9. [#9746](https://github.com/earendil-works/pi/pull/9746) — 文件补全识别 CJK 标点边界（开放中）**
修复中文标点后无法触发 tab 补全，对中文用户是实际体验改善。

**10. [#9763](https://github.com/earendil-works/pi/pull/9763) — pi.dev 兼容性检查工作流（开放中）**
为 PR 提供模型目录兼容性 commit status，CI 基建完善。

其他值得一提：#9720（Mistral reasoning 派发改由 thinkingLevelMap 驱动 + 新增 zai-glm-5-3）、#9754（同仓库 worktree 视为同一项目）、#9749（SDK 自定义 resume 命令）、#9488（Codex turn 归因元数据）。

---

## 📈 功能需求趋势

1. **Windows 一等公民化**：#7547 调研、#9361 shell 解析、#9129 进程树清理、#9549 渲染性能——Windows 相关 Issue 密度显著偏高。
2. **Compaction / thinking 块治理**：#9652、#9391、#9602、#9740，长会话下的上下文生命周期管理是当前最大问题簇。
3. **性能与内存**：CPU 飙升（#7730）、每帧重渲染（#9549）、SSE 缓冲 OOM（#9036）、流式解析 O(N²)（#9062）、fuzzy 搜索优化（#9267）。
4. **新模型 / Provider 目录维护**：DeepSeek V4.1 系列（#9485、#9737）、GLM-5.3（#9616）、Azure Foundry（#9645）、Qwen Token Plan CN（#7989）——上游模型迭代快，目录陈旧成常态痛点。
5. **可靠性与静默失败治理**：`--print` 零输出（#9718）、`--mode` 静默忽略（#9045）、模板静默丢弃（#9354）、`/export` 丢内容（#8896）——社区对“静默 no-op”类问题容忍度很低。

---

## ⚠️ 开发者关注点

- **错误可观测性不足**：多个高热 Issue 本质是“静默失败”（压缩 no-op、配置被忽略、输出为空），社区强烈期望显式诊断信息。
- **多进程/CI 场景的鉴权与生命周期**：#8928 的 48 秒误报在生产环境调试成本高，自动化用户是重要群体。
- **扩展生态的质量护栏**：不规范扩展返回值可击穿 TUI（#9762 已修）、shellPath 非确定性失效（#9361）——扩展加载路径的隔离与可预测性待加强。
- **国内模型接入需求旺盛**：GLM Coding Plan、Qwen Token Plan CN、DeepSeek 等相关 Issue/PR 活跃，中国区 provider 维护是持续投入方向。
- **本地 LLM 用户体验**：`/retry`、流截断重试、输出预算耗尽处理等改进均源于本地模型用户的真实痛点。

---

*数据来源：github.com/earendil-works/pi · 统计窗口：2026-09-18 至 2026-09-19*

</details>

<details>
<summary><strong>oh-my-pi</strong> — <a href="https://github.com/can1357/oh-my-pi">can1357/oh-my-pi</a></summary>

# oh-my-pi 社区动态日报 · 2026-09-19

## 一、今日速览

今日发布 **v18.2.6**，修复了 Anthropic prompt cache 在 memory recall 刷新时反复重新计费的关键问题（呼应 #12392）。社区方面，@kvnloo 一口气抛出 **RLM 上下文引擎 RFC 系列（v1–v7 路线图）**，成为当日最热讨论；同时 OpenCode Free Tier 403 问题持续发酵，多项 issue 汇聚。PR 侧异步进度交付系列（#9368–#9374）持续推进。

## 二、版本发布

- **v18.2.6**（[Release](https://github.com/can1357/oh-my-pi/releases)）
  - `@oh-my-pi/pi-ai`：修复 Anthropic prompt cache 断点每次 memory recall 刷新都重新基线化的问题——系统断点现锚定在最后一个稳定段而非易变的 recall 后缀，稳定系统指纹忽略 recall 块，避免 recall 刷新导致整段缓存重新计费。直接回应 #12392 反馈。

## 三、社区热点 Issues

1. **[RFC v3：RLM Runtime Membrane](https://github.com/can1357/oh-my-pi/issues/12410)**（@kvnloo）
   v3 将 v1/v2 的上下文边界从“提示词约束”升级为真正的运行时不变量：隔离上下文、会话所有权、租约式执行。是 RLM 系列当日三连发之一。

2. **[RLM RFC 系列总路线图（v1–v7 上下文操作系统）](https://github.com/can1357/oh-my-pi/issues/12413)**（@kvnloo）
   被标注为该系列的 "source of truth"，目标直指 OMP 的上下文操作系统化。同日发布的还有 [RFC v2（depth-1 子调用 + kernel bind）#12407](https://github.com/can1357/oh-my-pi/issues/12407) 和 [RFC v1（prompt-as-variable）#12400](https://github.com/can1357/oh-my-pi/issues/12400)。三条 RFC 均获 9 条左右评论，讨论热度最高。

3. **[图形界面请求（桌面 + Web）](https://github.com/can1357/oh-my-pi/issues/5742)**（@HarshalRathore，👍26，评论13）
   长期高热度需求：对标 OpenCode/Codex CLI/Cursor，请求在 TUI 之上提供 GUI 层。与 [#2149 桌面版诉求](https://github.com/can1357/oh-my-pi/issues/2149) 形成呼应。

4. **[Anthropic prompt cache 仍为 head-only（v18.2.5）](https://github.com/can1357/oh-my-pi/issues/12392)**（@renanlido）
   #12318 的后续反馈：尽管 `ab88e931` 修复已进入 v18.2.5，冻结的 head-only 缓存签名仍在复现。今日 v18.2.6 应是针对此的进一步修复，值得验证。

5. **[OpenCode Free Tier 403 FreeTierError](https://github.com/can1357/oh-my-pi/issues/12306)**（@krishan-19-dev，👍8）
   `muse-spark-1.3-contributor-free` 在 OpenCode 可用、经 OMP 返回 403。[#12418](https://github.com/can1357/oh-my-pi/issues/12418) 为同日新报的相同问题，可能是 provider 端检测客户端来源所致。

6. **[长会话中 write 流式/编辑性能问题](https://github.com/can1357/oh-my-pi/issues/12261)**（@vzarytovskii）
   1.1M 上下文会话约 40% 处写入速度骤降至 5 秒 1-2 token。#10955 修复后从“挂死”变“极慢”，与 #2089 同属长会话性能主题。

7. **[专用 compaction 模型](https://github.com/can1357/oh-my-pi/issues/4139)**（@MRGRD56，👍4）
   请求为 `context-full` 压缩策略指定独立模型（新模型角色或独立配置），与 RLM 系列的 token 成本议题一脉相承。

8. **[凭证明文存储问题](https://github.com/can1357/oh-my-pi/issues/11399)**（@kvnloo）
   `agent.db` 中 API key/OAuth token 为明文 JSON，请求可选的静态加密、OS keyring 或 Bitwarden 集成。安全敏感度高的正确诉求。

9. **[ advisor 关注点延迟到达导致趋向 blocker](https://github.com/can1357/oh-my-pi/issues/10600)**（@skeet70）
   自主会话中 advisor 的 concern/nit 要等主 agent 整轮结束才送达，信息过期使 advisor 倾向于升级为 blocker。配合 [#9074 可配置 steering 严重度阈值](https://github.com/can1357/oh-my-pi/issues/9074)，advisor 机制是近期持续打磨点。

10. **[macOS 多会话无崩溃报告中途退出](https://github.com/can1357/oh-my-pi/issues/9956)**（@luw2007）
    多个独立会话在 turn/tool 活跃期间数秒内退出，无 crash report，标记 wontfix/needs-info，但仍是 macOS 用户痛点。

## 四、重要 PR 进展

1. **[fix(tui-debug)：PTY 屏幕销毁后丢弃数据 #12486](https://github.com/can1357/oh-my-pi/pull/12486)**
   修复会话拆除时 PTY 回调触发 `KittyTerminal used after dispose()` 导致整个 agent 会话崩溃的问题。

2. **[异步进度交付系列（#9368–#9374，7 个 PR）](https://github.com/can1357/oh-my-pi/pull/9374)**
   @pedropaulovc 的大型 stack：有限时 Bash 命令自动转后台（#9372）、有界限流进度流（#9369）、v4 输出监控协议（#9370）、Hub monitor 进度模式（#9371）、统一异步进度提示策略（#9373）、TUI 折叠渲染（#9374），以及 p1 修复 broker 不再过早关闭认证中的 socket（#9368）。

3. **[prompt cache 抖动诊断 #11938](https://github.com/can1357/oh-my-pi/pull/11938)**
   可选、有界的 prompt-cache 日志（基于 HMAC 指纹而非明文内容），Anthropic 适配器关联物理请求与缓存命中。与今日 v18.2.6 修复相辅相成，是排查 #12392 类问题的工具。

4. **[gpt-reserve 层级回退 #12480](https://github.com/can1357/oh-my-pi/pull/12480)**
   GPT 标准额度耗尽时自动回退到 OpenAI 新增的 "gpt-reserve" 计费层，避免直接报错。

5. **[fix(edit)：首次失败即教学 hashline 语法 #12085](https://github.com/can1357/oh-my-pi/pull/12085)**
   改进 #11771 的恢复流程：首次错误消息即提供正确格式信息，避免模型多次试错。

6. **[plugin upgrade --dry-run 真正生效 #12383](https://github.com/can1357/oh-my-pi/pull/12383)**
   此前 `--dry-run` 标志被接受但无效，实际会安装插件。现改为真正的预览模式。

7. **[fix(vcs)：补丁路径限制在 worktree 内 #12096](https://github.com/can1357/oh-my-pi/pull/12096)**
   堵住 `validate_repo_path` 未检查符号链接逃逸和 `.git/` 目录的安全缺口。

8. **[autoResume 不进入非交互运行 #12313](https://github.com/can1357/oh-my-pi/pull/12313)**
   修复 `omp -p` 被脚本/自身调用时递归 resume 多个会话的问题。

9. **[Figma 远程 MCP OAuth DCR 兼容 #12470](https://github.com/can1357/oh-my-pi/pull/12470)**
   针对 Figma 服务端的 DCR 特殊要求（client_name、固定回调端口）做兼容，改善 MCP 接入体验。

10. **[openzoo provider（x402 按次付费本地代理）#10535](https://github.com/can1357/oh-my-pi/pull/10535)**
    接入本地 x402 链上微支付代理，无需账号和 API key，是 provider 生态的有趣扩展。

## 五、功能需求趋势

- **上下文管理与 token 成本（最热）**：RLM RFC 系列（v1–v7）、专用 compaction 模型（#4139）、内置工具延迟加载以省 token（#12393）、prompt cache 诊断与修复——长会话成本是核心焦虑。
- **图形化/桌面端**：#5742（👍26）与 #2149 持续升温，社区希望突破纯 TUI 形态。
- **多账号与认证体验**：手动切换 OAuth 账号（#4829、#4614）、凭证静态加密（#11399）、gpt-reserve 回退。
- **MCP 生态增强**：per-server 工具级 allow/deny（#6299）、Figma OAuth 兼容、stdio 错误信息改进（#12476）、让 agent 自助管理 MCP 配置（#11265）。
- **Agent 可观测性**：advisor steering 阈值与时机（#9074、#10600）、任务结果记录模型决策链（#9647）、roster 成本统计准确性（#12344）。

## 六、开发者关注点

1. **长会话性能仍是头号痛点**：写入流式变慢（#12261）、整体资源攀升（#2089）、macOS 会话无声退出（#9956）——高上下文场景下的稳定性与性能持续被诟病。
2. **缓存失效即成本失控**：prompt cache head-only 问题（#12392）已连续两个版本迭代修复，v18.2.6 能否彻底解决需要社区验证；建议配合 #11938 的诊断工具上报数据。
3. **Provider 兼容性摩擦**：OpenCode Free Tier 403（#12306、#12418）反映 provider 端客户端检测带来的兼容风险，多 issue 汇聚，优先级或应上调。
4. **安全面正在补齐**：明文凭证（#11399）与补丁路径逃逸（#12096）先后被提出/修复，本地 agent 的安全边界值得持续关注。

---
*数据截至 2026-09-19，来源：github.com/can1357/oh-my-pi（Issues 70 条 / PRs 112 条，本文展示讨论度最高的子集）*

</details>

<details>
<summary><strong>DeepSeek Harness</strong> — <a href="https://github.com/deepseek-ai/deepseek-harness">deepseek-ai/deepseek-harness</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*