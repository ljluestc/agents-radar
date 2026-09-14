# OpenClaw 生态日报 2026-09-14

> Issues: 500 | PRs: 500 | 覆盖项目: 14 个 | 生成时间: 2026-09-14 03:57 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyclaw)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [EasyClaw](https://github.com/gaoyangz77/easyclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-14

---

## 1. 今日速览

OpenClaw 今日保持高活跃度：过去 24 小时共有 **500 条 Issue 更新**（新开/活跃 279，关闭 221）和 **500 条 PR 更新**（待合并 296，合并/关闭 204），无新版本发布。焦点仍集中在 **2026.9.3/9.4 升级可靠性**（维护者跟踪 Issue #145252 持续活跃）、**Windows 平台更新失败**（#146860、#145510 等多个 P0）以及 **Gateway 进程/资源管理类缺陷**（僵尸进程、事件循环阻塞、SQLite WAL 膨胀）。核心贡献者 @steipete 今日密集提交了十余个 PR，覆盖 Windows 数据库路径修复、云会话冷启动优化和 Control UI 体验打磨。

---

## 2. 版本发布

今日**无新版本发布**。当前主线版本仍为 2026.9.4（2026.9.3 → 9.4 管理式升级链问题较多，见第 5 节）。

---

## 3. 项目进展

今日有多条值得关注的 PR 推进（多数为 9/13–9/14 新开、待维护者复核）：

- **[#147762](https://github.com/openclaw/openclaw/pull/147762)** — 修复 Windows 下重复 agent 数据库路径注册（extended-length 文件名导致），并在 Doctor 中修复别名。直接关联两个 P0 更新失败 Issue（#147409、#145510），是 Windows 升级链的关键修复。标记 merge-risk: compatibility。
- **[#147785](https://github.com/openclaw/openclaw/pull/147785)** — Hot reload 时撤销已放行但未完成的 hook 准入（安全边界修复，needs proof）。
- **[#145117](https://github.com/openclaw/openclaw/pull/145117)** — 持久化 `agent.wait` 终态回执，消除 Gateway 重启导致的“已完成任务变未知超时”问题（XL，triage: dirty-candidate）。
- **[#147682](https://github.com/openclaw/openclaw/pull/147682)** — Artifacts 支持按 run 过滤 assistant 交付文件（`messageRole: "assistant"`）。
- **[#147787](https://github.com/openclaw/openclaw/pull/147787)** — 降低云会话冷启动时间，worker bundle 打包提前到远程节点安装阶段。
- **[#144600](https://github.com/openclaw/openclaw/pull/144600)** — 修复插件自动启用时静默丢弃 compaction/渠道等已计算默认值。
- **[#112375](https://github.com/openclaw/openclaw/pull/112375)** — cron 任务新增 shell precheck 门控，无事可做时跳过 LLM 调用（成本优化方向，仍 needs proof）。
- **[#147731](https://github.com/openclaw/openclaw/pull/147731)** — 修复 Control UI 助手回复中文本与图片顺序错乱。
- **[#147675](https://github.com/openclaw/openclaw/pull/147675)** — 修复 memory-core 搜索命中 agent 文件但读取到父级文件的问题。

整体看，今日推进以 **Windows 升级链修复 + 性能/冷启动优化 + Control UI 体验**三条线为主，204 个 PR 合并/关闭表明 review 吞吐量健康，但 296 个待合并 PR 中标记 needs proof 的比例不低，review 债务在累积。

---

## 4. 社区热点

| Issue | 评论 | 主题 | 状态 |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 40 | 工具调用间的中间文本泄漏到消息渠道（Slack/iMessage） | OPEN，自 2 月未解决 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 31 | hook/工具子进程未 reap，僵尸进程累积致运行时退化 | OPEN |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 28 | 子代理完成结果静默丢失（无重试/通知/超时重启） | OPEN，Telegram 场景 |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | 23 | Codex PreToolUse hook relay 满载 CPU、阻塞 Gateway RPC | OPEN，P0 |
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | 22 | #84076 回归：Codex turn 完成确认再次 stall | 已 CLOSED |
| [#119720](https://github.com/openclaw/openclaw/issues/119720) | 19 | 同步持久化/transcript 维护在规模化时阻塞 Gateway 事件循环 | OPEN，评论中追踪部分修复落地 |
| [#102175](https://github.com/openclaw/openclaw/issues/102175) | 19 | 嵌入式会话跨边界丢失 provider prompt cache | OPEN |

**诉求分析**：
- **内部输出泄漏类**（#25592、#137927 已关）是长期第一痛点——用户希望 agent 的内部处理文本/上下文脚手架绝不流入 IM 渠道，这直接关系到能否在真实工作群组中部署。
- **子代理编排可靠性**（#44925、#141474）反映多 agent 工作流用户对“静默失败零容忍”的诉求。
- **规模化性能**（#119720、#91009、#143524）显示重度自托管用户已把 OpenClaw 当作长驻生产服务，对进程/资源治理要求接近运维级。

---

## 5. Bug 与稳定性（按严重程度）

### P0（阻塞级）
- **[#146860](https://github.com/openclaw/openclaw/issues/146860)** — Windows Scheduled Task（InteractiveToken）下管理更新 handoff 永远拿不到进程启动身份，stall 后 abandoned。🔴 无 fix PR。
- **[#145510](https://github.com/openclaw/openclaw/issues/145510)** / **[#146394](https://github.com/openclaw/openclaw/issues/146394)** — 2026.9.3 → 9.4 更新在 runtime-verification / global-install 阶段失败。🟡 关联 PR #147762（Windows 数据库路径）可能覆盖部分场景。
- **[#145192](https://github.com/openclaw/openclaw/issues/145192)** — 9.2→9.4 管理更新在 candidate-Doctor 处确定性失败并回滚到已迁移状态（#144742 升级路径）。🔴 无 fix PR。
- **[#144911](https://github.com/openclaw/openclaw/issues/144911)** — stdio MCP server 初始化超时触发未处理 rejection，**整个 Gateway 崩溃**（9.9.4）。标记 queueable-fix 但尚无 fix PR。
- **[#143524](https://github.com/openclaw/openclaw/issues/143524)** — Windows 下 agent SQLite WAL 数日内膨胀至 1.4–2.8 GB，阻塞 Gateway 启动。🔴 无 fix PR。
- **[#145252](https://github.com/openclaw/openclaw/issues/145252)** — 维护者跟踪汇总 9.3/9.4 更新、升级与恢复可靠性（umbrella）。

### P1（重要）
- **[#97616](https://github.com/openclaw/openclaw/issues/97616)** — 僵尸子进程泄漏累积。
- **[#88312](https://github.com/openclaw/openclaw/issues/88312)** — Codex turn-completion stall 回归（已关闭，+#85107 修复谱系）。
- **[#141252](https://github.com/openclaw/openclaw/issues/141252)** — 9.2 回归：“Reply operation has no active tool authority snapshot”（已关闭）。
- **[#134993](https://github.com/openclaw/openclaw/issues/134993)** — 大规模 skill/agent 场景下文件系统发现 busy-loop 打满单核。
- **[#101929](https://github.com/openclaw/openclaw/issues/101929)** — midturn 上下文预检估算偏高 2.3–2.6 倍，误触发截断恢复。
- **[#113701](https://github.com/openclaw/openclaw/issues/113701)** — 大工具输出超上下文后 compaction 无法恢复，会话进入失败循环。
- **[#139710](https://github.com/openclaw/openclaw/issues/139710)** — 插件热重载 supersede 杀死系统 agent turn，报错误导性地指向 `openclaw onboard`。

**结论**：升级/更新链（尤其 Windows）是当前最大稳定性风险面；多数 P0 尚无对应 fix PR，建议优先。

---

## 6. 功能请求与路线图信号

- **[#27445](https://github.com/openclaw/openclaw/issues/27445)**（12 评论，linked-pr-open）— `announceTarget` 让子代理完成通知路由回父会话，支持主 agent 编排多步工作流。已有开放 PR，纳入概率高。
- **[#48788](https://github.com/openclaw/openclaw/issues/48788)** — 集中式文件名编码工具，统一处理 Feishu/Shift-JIS/GB18030 等多编码 Content-Disposition（P3 但架构信号明确）。
- **[#52640](https://github.com/openclaw/openclaw/issues/52640)** — 长任务的一等持久状态面板（Discord 优先），呼应今日 PR #144862（完成会话通知加显式标签），通知/状态呈现是明确方向。
- **PR [#112375](https://github.com/openclaw/openclaw/pull/112375)** — cron 免 LLM precheck 门控，反映“降低静默轮询成本”路线，若合入将是下一版本的成本类亮点。
- **PR [#147307](https://github.com/openclaw/openclaw/pull/147307)** — Android 端支持 Cloudflare Access 登录，移动端接入安全是投入方向。
- **[#74077](https://github.com/openclaw/openclaw/issues/74077)** — `/stream` 命令按会话切换预览流式模式（linked-pr-open，等待产品决策）。

---

## 7. 用户反馈摘要

**痛点**：
- **升级即故障**是最集中的负面情绪来源：多个用户报告 9.3/9.4 升级失败、回滚后状态不一致（#145192、#146394、#135776 插件版本偏斜），自托管用户对“升级要赌运气”感到疲惫。
- **Windows 体验明显落后**：WAL 膨胀（#143524）、Scheduled Task 更新失败（#146860）、restart 误杀启动中的 Gateway（#140162）。
- **静默失败不可接受**：子代理结果丢失（#44925，👍2）、消息丢失、内部上下文泄漏到 Telegram（#137927）均属“无法在生产环境信任”级别反馈。
- **中文渠道用户活跃**：WeChat 回复分发失败（#145563）、Feishu 搜索/文件名编码问题，说明中文生态是重要用户群但适配欠佳。

**满意点**：
- Issue 模板与诊断信息质量高，大量报告附带完整 trace/日志，社区工程素养好。
- @steipete 的修复节奏（单日 10+ PR）和 PR #145117、#144600 等对 durable state / 默认值保护的投入获得正向回应。
- 快速的回归修复文化（#88312、#141252 均已关闭）。

---

## 8. 待处理积压

- **[#25592](https://github.com/openclaw/openclaw/issues/25592)**（2/24 创建，40 评论，钻石级）— 渠道文本泄漏，needs-maintainer-review + needs-product-decision + needs-security-review 三重挂起，**积压近 7 个月**，应尽快给出产品决策。
- **[#44925](https://github.com/openclaw/openclaw/issues/44925)**（3/13 创建）— 子代理静默丢失，同样多标签挂起无 fix PR。
- **[#91009](https://github.com/openclaw/openclaw/issues/91009)**（P0，6/6 创建）— Codex hook relay CPU 风暴，影响 gateway 可用性，仍 OPEN。
- **[#69208](https://github.com/openclaw/openclaw/issues/69208)**（maintainer umbrella，4/20 创建）— 跨渠道重复 transcript/replay 统一修复，进展缓慢。
- **[#99586](https://github.com/openclaw/openclaw/issues/99586)**、**[#76038](https://github.com/openclaw/openclaw/issues/76038)** 等已标记 stale 的 P1 回归——stale 化高影响 issue 有“问题被埋没”的风险。
- **PR 侧**：#112375（7/21）、#124467（8/16，stack PR 等待依赖 #118008）、#145117（triage: dirty-candidate）等 XL 级 PR 长期未合，建议维护者安排专项 review。

---

**健康度小结**：社区参与度与修复吞吐均处于高位，但 9.3/9.4 升级链缺陷密集（多个 P0 无 fix PR），Windows 平台与升级可靠性是下一版本前必须收敛的两大风险面。

---

## 横向生态对比

# 个人 AI 助手/智能体开源生态横向对比分析报告

**数据日期：2026-09-14**

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态呈明显的“金字塔”结构：OpenClaw 以单日 1000 条 Issue/PR 更新占据绝对头部，是生态的复杂度和话题风向标；中部 Hermes Agent、CoPaw、Zeroclaw 构成“高活跃第二梯队”，分别背负架构级重构和版本质量收敛任务。长尾项目分化剧烈——TinyClaw、IronClaw 等处于低活跃维护期，而 LobsterAI 出现**安全修复无人合并的维护停滞信号**。跨项目共性痛点高度收敛：**Windows 平台体验、SQLite/持久化可靠性、长期记忆能力、升级链稳定性**是全生态的四条主线。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | 合并/关闭 | Release | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 500（新279/关221） | 500 | 204 | 无 | 🟢 活跃度高，但 9.3/9.4 升级链多个 P0 无 fix PR，Windows 与升级可靠性是风险面 |
| **Hermes Agent** | 50 | 50 | 16 | 无 | 🟢 响应链路健康（当日 bug 当日 fix），但存量 P1 滞后 |
| **CoPaw** | 17 | 25 | 3 | 无 | 🟢 版本后修复冲刺期，闭环快，2.2.x 质量待收敛 |
| **Zeroclaw** | 37 | 50 | **0** | 无 | 🟡 高输入零合并，治理/流程类议题热度超过技术议题，review 带宽是瓶颈 |
| **NanoClaw** | 5 | 16 | 2 | 无 | 🟢 中等活跃，安装链路与 Mattermost 加固，响应迅速 |
| **NanoBot** | 0 | 7 | 3 | 无 | 🟡 周末后安静状态，WebUI 打磨为主，1 条 PR 积压近 5 个月且有冲突 |
| **Moltis** | 3 | 5 | 4 | ✅ 20260913.02 | 🟢 单人主导但节奏稳定，积压净下降，今日唯一发布版本的项目 |
| **PicoClaw** | 5 | 4 | **0（全关）** | 无 | 🟠 清理性关闭有价值社区贡献（iMessage、i18n），数据丢失 Issue 被 stale 关闭 |
| **LobsterAI** | 4（全 stale） | 4（全 stale） | 0 | 无 | 🔴 维护停滞，**P0 安全修复 PR #1042 积压 5.5 个月未合并** |
| **TinyClaw / ZeptoClaw / IronClaw** | 1 / 1 / 0 | 0 / 0 / 5(依赖) | 0 | 无 | ⚪ 低活跃维护期（IronClaw 仅 dependabot 轮替） |
| **NullClaw / EasyClaw** | 0 | 0 | 0 | 无 | ⚪ 无活动 |

---

## 3. OpenClaw 在生态中的定位

**规模对比**：OpenClaw 单日 Issue/PR 更新量（各 500）约为第二名 Hermes Agent 的 10 倍、长尾项目的百倍以上；Issue 编号已进入 14 万级，是生态中唯一达到“大型基础设施级”复杂度的项目。

**优势**：
- **社区工程素养最高**——报告普遍附完整 trace/日志，Issue 模板与诊断信息质量被广泛认可；
- **维护者响应强度大**——@steipete 单日 10+ PR，修复节奏获正向回应；
- **功能纵深最全**——Gateway 编排、多渠道（Slack/iMessage/Telegram/WeChat/Feishu）、cron、Control UI、云会话、Android 端，覆盖面无同类可及。

**风险面**：正是规模带来了独有的问题类别——9.3/9.4 管理式升级链、Windows Scheduled Task/WAL 膨胀、Gateway 进程治理等“运维级”缺陷是其他项目尚未触及的复杂度层级。此外 #25592（渠道文本泄漏）积压近 7 个月且三重 review 挂起，属于头部项目不该有的决策债。

**技术路线差异**：OpenClaw 走“全功能自托管 Gateway”路线；Zeroclaw/ZeptoClaw 走 Rust 单二进制、本地优先路线；NanoBot/NanoClaw 轻量化快速迭代；Hermes Agent 则在押注 GUI 自主操作（Bot Screen）与统一网关架构。

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **持久化/长期记忆** | TinyClaw #296、ZeptoClaw #678、Moltis #1268、CoPaw #7733/#7719、LobsterAI #2660、OpenClaw #147675 | 最跨项目共振的主题。MemCode 创始人同一人在 4+ 个项目发起记忆集成提案（明显的生态扩张行动）；用户侧痛点是“反复强调的规则仍被遗忘”（CoPaw #7571）和跨运行上下文保留 |
| **SQLite WAL / 持久化可靠性** | OpenClaw #143524、Hermes #109966、PicoClaw #3351 | WAL 膨胀、sidecar inode 阻塞网关、压缩物理删除历史——三家均出现“持久层设计缺陷导致数据不可用/丢失” |
| **Windows 二等公民问题** | OpenClaw（多个 P0）、Hermes #63577/#110526、Zeroclaw #9381/#10793、NanoBot #5756 | 升级失败、skill 安装截断、symlink/CI 失败，几乎所有跨平台项目 Windows 体验落后 |
| **cron/定时任务可靠性** | NanoBot #3245/#5751、Zeroclaw #10324、OpenClaw PR #112375、CoPaw #7709、Hermes #97629 | 任务重复执行、编辑后丢失执行、输出丢失；成本侧诉求（免 LLM precheck）仅 OpenClaw 出现 |
| **内部输出泄漏到渠道** | OpenClaw #25592、Hermes #107899 | 内部处理文本/诊断信息流入 IM 渠道，直接阻塞生产部署，是 customer-facing 场景的共同红线 |
| **OpenCode session header** | Zeroclaw #10603、PicoClaw #3369 | prompt cache 保持与账号安全，provider 兼容层的共性需求 |
| **可观测性/成本可见性** | NanoClaw PR #3796、Zeroclaw #10635/#10645、Hermes #95267 | OTel tracing、预算边界可信度、大上下文缓存成本 |

---

## 5. 差异化定位分析

| 维度 | 分层 |
|---|---|
| **功能侧重** | OpenClaw（全功能生产级 Gateway）/ Zeroclaw·ZeptoClaw（Rust 本地优先、单二进制、安全基建 OIDC/RPC）/ Hermes（GUI 自主操作 Bot Screen + 统一会话架构）/ CoPaw（多渠道 + Creator 内容生产 + Hub）/ NanoBot·NanoClaw（轻量快速迭代，WebUI/安装体验）/ PicoClaw（嵌入式/低性能设备，RISC-V）/ Moltis（推理等级精细化 + 渠道安全策略）/ IronClaw（WASM 沙箱插件运行时） |
| **目标用户** | OpenClaw、Hermes：重度自托管/多网关 fleet 生产用户；Zeroclaw：多 ACP 会话×大上下文重度用户（200k token 级）；NanoClaw：本地模型 + 无特权环境用户；PicoClaw：边缘设备用户；CoPaw：中文多渠道（微信/钉钉）企业用户 |
| **技术架构** | TypeScript 系（OpenClaw、NanoBot）vs Rust 系（Zeroclaw、ZeptoClaw、IronClaw）是生态最大架构分野；Moltis 与 CoPaw（Qwen 生态）代表厂商背书路线 |

---

## 6. 社区热度与成熟度分层

- **快速迭代/扩张期**：OpenClaw（功能线最宽、贡献者最密，但正在为升级链质量买单）、Hermes Agent（架构级重构 + Bot Screen 大特性押注）
- **质量巩固期**：CoPaw（2.2.x 修复冲刺，闭环率约 5/11）、NanoClaw（安装链路 + Mattermost 加固）、NanoBot（WebUI 打磨）、Moltis（小而稳，唯一今日发版）
- **流程瓶颈期**：Zeroclaw——贡献量充足但 50 PR 零合并，社区最热议题是 RFC 投票流程本身（治理类议题 32 条评论超任何单个技术 bug），典型“成长阵痛”
- **衰退/停滞预警**：LobsterAI（安全修复 5.5 个月无响应，stale bot 驱动的虚假活跃）、PicoClaw（有价值贡献被清理性关闭，贡献者流失风险）

---

## 7. 值得关注的趋势信号

1. **记忆层成为下一个竞争焦点，且有商业力量主动渗透**——MemCode 创始人单日内在 ≥4 个项目发起同构提案（持久记忆 + 本地优先边界），是明确的生态卡位行动。维护者需尽快明确立场：内置记忆、插件接口、还是拒绝集成。OpenClaw 的 #27445（announceTarget）与 CoPaw 的 #7733（自主上下文管理）显示头部项目已开始自研。

2. **“静默失败零容忍”成为生产用户的准入门槛**——子代理结果丢失（OpenClaw #44925）、turn 误取消（Zeroclaw #10785）、会话/配置丢失（CoPaw #7724）、输出泄漏（OpenClaw #25592、Hermes #107899）反复出现。agent 编排框架若想进入生产，必须优先解决**终态回执、持久化确认、失败通知**这三件事。

3. **SQLite 是全生态的共性阿喀琉斯之踵**——WAL 膨胀、inode 阻塞、压缩覆盖、commit 时序，三家头部项目同时暴露。长驻 agent 框架的存储层设计（checkpointing、sidecar 生命周期、多进程并发访问）值得专项投入。

4. **Windows 是被系统性低估的市场**——所有跨平台项目的 Windows 用户都在抱怨升级、安装、CI。谁先做到 Windows 一等公民，谁就能吃下这部分明显存在且未被满足的用户群（OpenClaw 中文渠道用户活跃也印证了非英语市场潜力）。

5. **成本可观测性从锦上添花变为刚需**——OTel tracing（NanoClaw）、预算边界可信度（Zeroclaw #10645 预算可被绕过属安全问题级）、缓存击穿费用确认（Hermes #95267）、cron 免 LLM precheck（OpenClaw）。agent 框架的下一步差异化在“每一分钱的去向可解释”。

6. **治理流程本身成为瓶颈**——Zeroclaw 的“零合并日 + RFC 流程改革热度第一”、OpenClaw 296 待合并 PR 中 needs proof 比例上升、各项目 XL 级 PR 长期滞留。对开发者的启示：**review 带宽是开源 agent 项目最稀缺的资源**，CI 证据链、stack PR 管理、快速合并通道等工程实践的价值正在被社区重新定价。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 · 2026-09-14

## 1. 今日速览

今日 NanoBot 仓库呈现「代码活跃、议题安静」的典型周末后状态：Issues 更新为 0 条，PR 更新 7 条（4 条待合并、3 条已关闭），无新版本发布。WebUI 相关修复是本日主线，涵盖连接页面、会话历史搜索、移动端交互与品牌统一等多个方向。另有两条来自 9 月 13 日的重要修复（cron 待执行任务保留、SSRF 测试密封性）仍在待合并队列中。整体来看，贡献者以 bug 修复和体验打磨为主，处于稳定迭代期而非功能扩张期。

## 2. 版本发布

今日无新版本发布，省略。

## 3. 项目进展

今日关闭的 3 条 PR 均已快速合入或处理，主要推进：

- **[PR #5758](https://github.com/HKUDS/nanobot/pull/5758)**（已关闭，@chengyongru）：重构 WebUI 连接页面 —— 采用紧凑居中布局、内联连接箭头、语言切换器和可折叠密码设置帮助，验证错误不再导致布局抖动，密码字段内直接展示简短校验反馈。附测试。
- **[PR #5755](https://github.com/HKUDS/nanobot/pull/5755)**（已关闭，@Re-bin）：改进移动端 composer 与设置导航，控件根据可用宽度自适应、附件/模型控件分区布局，且不改动后端与已保存配置。
- **[PR #5754](https://github.com/HKUDS/nanobot/pull/5754)**（已关闭，@Re-bin）：统一应用目录中的 Logo 与品牌名展示（Linear、iTerm2、Draw.io、Google Drive 等），保持尺寸与垂直对齐一致性。

合并节奏健康，WebUI 的易用性与视觉一致性明显推进，属于渐进式改进。

## 4. 社区热点

今日无新增 Issues，PR 评论数据缺失（评论数均为 undefined），暂无明确的讨论热点。从 PR 活动看，**[PR #3245](https://github.com/HKUDS/nanobot/pull/3245)**（cron claim 持久化修复）在创建近 5 个月后（2026-04-17 创建）于今日再次更新，且带有 `conflict` 标签，是值得关注的长期讨论对象。

## 5. Bug 与稳定性

今日无新报告 Issue，但从待合并 PR 可见以下已识别缺陷（均已有 fix PR）：

| 严重程度 | 问题 | 修复 PR | 状态 |
|---|---|---|---|
| P2 | `CronService` 在 await 回调前未持久化 running claim，可能导致任务重复执行；新增回归测试验证 `jobs.json` 落盘时序 | [PR #3245](https://github.com/HKUDS/nanobot/pull/3245) | 待合并，**存在冲突** |
| P2 | 编辑自动化任务的名称/指令会错误地重算下次执行时间：interval 任务被推迟、到期 cron 被跳过、一次性任务 `next_run_at_ms=None` 永不执行 | [PR #5751](https://github.com/HKUDS/nanobot/pull/5751) | 待合并 |
| P2 | `search_sessions` 与过滤版 `read_session` 只读取最新一页 transcript，长会话中较旧消息被静默遗漏 | [PR #5757](https://github.com/HKUDS/nanobot/pull/5757) | 待合并 |
| P2 | SSRF/代理测试模块的 fixture 仅清除 `*_PROXY` 环境变量，在有系统级代理（Windows 注册表 / macOS SystemConfiguration）的主机上测试不密封、可能误报 | [PR #5756](https://github.com/HKUDS/nanobot/pull/5756) | 待合并 |

值得注意：两条 cron 相关修复（#3245、#5751）指向同一子系统的可靠性隐患，建议维护者优先审阅。

## 6. 功能请求与路线图信号

今日无新功能请求 Issue。从 PR 流向可推断的近期方向：

- **WebUI 移动端体验**：#5755 显示移动端是打磨重点，后续可能继续有响应式改进。
- **自动化（cron）可靠性**：#3245 + #5751 表明调度子系统的状态持久化与任务编辑语义正在被系统性加固，有望进入下一个版本。
- **安全测试基础设施**：#5756 体现对跨平台 CI 稳定性的投入。

## 7. 用户反馈摘要

今日无 Issue 评论数据，无法提炼用户反馈。间接信号：PR 中描述的 bug（长会话搜索遗漏旧消息、自动化编辑后任务丢失）反映了长期使用场景下的真实痛点，即**长时间运行的会话数据完整性与定时任务的持续性**是用户可能反复遭遇的问题域。

## 8. 待处理积压

- **[PR #3245](https://github.com/HKUDS/nanobot/pull/3245)**：开放近 5 个月（2026-04-17 创建），今日虽有更新但带 `conflict` 标签，涉及 cron 任务重复执行风险。**建议维护者优先处理冲突并推进合并。**
- **[PR #5751](https://github.com/HKUDS/nanobot/pull/5751)**、**[PR #5756](https://github.com/HKUDS/nanobot/pull/5756)**、**[PR #5757](https://github.com/HKUDS/nanobot/pull/5757)**：均为 9 月 12-14 日创建的待合并修复，尚处新鲜期，暂不算积压，但建议在一周内完成评审以避免形成类似 #3245 的长尾。

---
*数据来源：HKUDS/nanobot GitHub 仓库，统计窗口 2026-09-13 至 2026-09-14。*

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目日报 · 2026-09-14

---

## 1. 今日速览

- 过去 24 小时 Issue 活跃度显著偏高：**37 条更新（32 新开/活跃，5 关闭）**，PR 更新 50 条（全部待合并，**0 合并/关闭**），项目整体处于“高输入、零落地”的积压消化阶段。
- 今日新增 Issue 覆盖配置校验、ZeroCode/ACP 会话、provider 可靠性、可观测性等多个方向，其中 P0/P1 级 bug 密集，稳定性压力明显。
- 治理类讨论（RFC 决策队列、RFC 投票流程简化）持续占据评论区热度榜首，表明社区在流程层面存在摩擦。
- 无新版本发布，v0.8.5 周度稳定线（#9459）仍在推进中，周度切分机制尚未产出今日发布。

---

## 2. 版本发布

今日无新版本发布。最近的发布节奏参考 v0.8.5 稳定线 tracker（[#9459](https://github.com/zeroclaw-labs/zeroclaw/issues/9459)）。

---

## 3. 项目进展

**今日无任何 PR 合并或关闭（50 条 PR 全部 OPEN）**，短期进展主要体现在讨论推进与新 PR 提交：

- [#10845](https://github.com/zeroclaw-labs/zeroclaw/pull/10845) — MCP 延迟工具索引改为每个工具渲染一行摘要（截断 200 字符），改善工具列表可读性。
- [#10840](https://github.com/zeroclaw-labs/zeroclaw/pull/10840) — mdBook 构建新增 `llms.txt` / `llms-full.txt` 生成器，面向 LLM 消费文档的基建投入，值得关注。
- [#10843](https://github.com/zeroclaw-labs/zeroclaw/pull/10843) — Telegram 表情回应（add/remove_reaction）真实实现，修复此前“静默假成功”的 trait 默认行为。
- [#10839](https://github.com/zeroclaw-labs/zeroclaw/pull/10839) — 补齐 webhook-ingress channel 能力旗标文档，解除 mdBook 构建门禁阻塞。
- 大型长期 PR（#9134 插件字节准入、#9143 插件事件路由、#8965 skills 声明式激活、#10259 RPC 认证主体）均有更新但无合并迹象，其中 #9134/#9109 处于 `blocked/do-not-merge` 状态。

⚠️ 连续高活跃但零合并，提示 review 带宽或流程门禁（见 RFC 讨论）可能是瓶颈。

---

## 4. 社区热点

| Issue | 评论 | 主题 |
|---|---|---|
| [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) Tracker: 维护者决策队列 | 15 | RFC/设计 Issue 的决策积压本身成为最热议题，与"零合并日"互相印证 |
| [#10549](https://github.com/zeroclaw-labs/zeroclaw/issues/10549) RFC: 简化 RFC 投票流程 | 10 | 社区诉求：取消强制 48/72 小时讨论窗、REVISE 中止当前快照，反映流程摩擦真实存在 |
| [#10366](https://github.com/zeroclaw-labs/zeroclaw/issues/10366) RFC: PR review 证据与快速合并通道 | 7 | 提议"expedited merge lane"，直指 review 带宽不足 |
| [#10734](https://github.com/zeroclaw-labs/zeroclaw/issues/10734) RpcDispatcher 栈溢出风险 | 7 | Windows advisory CI 频繁暴露平台特异性问题 |
| [#9381](https://github.com/zeroclaw-labs/zeroclaw/issues/9381) crates.io 发布/打包跟进 | 5 | Windows 无开发者模式 checkout 因 symlink 失败，影响真实用户 |

**诉求解读**：治理/流程类议题（#8692、#10549、#10366）合计 32 条评论，热度超过单个技术 bug，说明社区当前最大痛点是**决策与合并吞吐**，而非代码本身。

---

## 5. Bug 与稳定性（按严重度）

**P0**
- [#10066](https://github.com/zeroclaw-labs/zeroclaw/issues/10066) SOP 引擎在记录 output-schema 拒绝**之前**就推进并执行后续步骤（S1 工作流阻塞）。已接受、无明确 fix PR，**最需关注**。

**P1**
- [#10603](https://github.com/zeroclaw-labs/zeroclaw/issues/10603) OpenCode provider 不发 `x-opencode-session` 头，破坏 Go 模型 prompt cache、有账号被标记风险（👍3）→ **已有 fix PR [#10604](https://github.com/zeroclaw-labs/zeroclaw/pull/10604)**（needs-author-action）。
- [#10785](https://github.com/zeroclaw-labs/zeroclaw/issues/10785) zerocode 通知延迟触发 `begin_notification_resync` 误取消所有运行中 turn（约 200k token 大上下文场景）。
- [#10635](https://github.com/zeroclaw-labs/zeroclaw/issues/10635) runtime profile 显示无上限成本额度，与全局每日 $10 预算不一致，误导用户。
- [#10645](https://github.com/zeroclaw-labs/zeroclaw/issues/10645) 委托子循环未挂接成本追踪上下文，预算可被绕过（security 风险，已接受）。
- [#10736](https://github.com/zeroclaw-labs/zeroclaw/issues/10736) / [#10787](https://github.com/zeroclaw-labs/zeroclaw/issues/10787) Reliable provider 流式失败后回退/重试逻辑缺陷（529 过载仅重试一次无退避）。
- [#10788](https://github.com/zeroclaw-labs/zeroclaw/issues/10788) Code/ACP turn 失败时丢弃已完成的 prompt 和 tool 交换的持久历史。
- [#10828](https://github.com/zeroclaw-labs/zeroclaw/issues/10828) `openai-codex --device-code` 使用过时设备授权端点直接 404。

**P2**
- [#10320](https://github.com/zeroclaw-labs/zeroclaw/issues/10320) `config set` / RPC `config/set` 绕过校验持久化越界值；相关 [#10837](https://github.com/zeroclaw-labs/zeroclaw/issues/10837) 今日开、今日关（快速修复，正面信号）。
- [#10793](https://github.com/zeroclaw-labs/zeroclaw/issues/10793) Windows advisory CI 三项测试无端失败（伴随 #10734，Windows CI 噪声偏高）。
- [#10821](https://github.com/zeroclaw-labs/zeroclaw/issues/10821) `zeroclaw service logs` 展示陈旧 stderr，误导排障。

**今日已关闭**：#10721（`~` 全局替换 bug）、#10324（cron TOCTOU 跨 agent 边界）、#10580（docs 链接门禁）、#10533（model_routing_config 拒绝 custom.*）、#10837 —— 5 条均为有效问题闭环。

---

## 6. 功能请求与路线图信号

- [#10822](https://github.com/zeroclaw-labs/zeroclaw/issues/10822) `config/set-many` 原子批量配置 RPC —— 已 in-progress，修复 #10320 系列的自然延伸，大概率近期落地。
- [#10826](https://github.com/zeroclaw-labs/zeroclaw/issues/10826) ZeroCode 会话根目录显式选择与恢复保留 —— 基于 #10565 的 follow-up，方向已接受。
- [#10360](https://github.com/zeroclaw-labs/zeroclaw/issues/10360) 家庭边缘 mesh（pull worker + 签名回执）—— 大方向 RFC，契合 local-first/多设备叙事，尚需作者行动。
- [#10812](https://github.com/zeroclaw-labs/zeroclaw/issues/10812) WhatsApp PDF 缩略图预览 —— 小改进，易纳入。
- 大型安全基建（OIDC #10255、RPC 认证 #10259）持续更新，是 #8289 多阶段路线的落地中段，构成下一版本的主干候选。

---

## 7. 用户反馈摘要

- **多设备/多会话重度用户**（#10785，~200k token × 3 ACP 会话）是核心使用画像，对 turn 被误取消极其敏感。
- **成本可见性焦虑**：#10635/#10645 显示用户关心预算边界可信度——既怕被误杀（$10 上限未告知），也怕被绕过（委托循环逃逸）。
- **Windows 用户摩擦持续**：symlink checkout（#9381）、advisory CI 失败（#10734/#10793）、栈溢出，Windows 属二等公民体感。
- **排障体验差**：#10821（stale logs）、#10779（429 配额耗尽仍亚秒重试不 fail fast）直接打击操作者信心。
- 正面信号：#10837 当日开当日关，社区对快速修复响应有感知；PR 描述质量与 maintainer note 透明度普遍较高。

---

## 8. 待处理积压（维护者关注）

| 项目 | 状态 | 风险 |
|---|---|---|
| [#10066](https://github.com/zeroclaw-labs/zeroclaw/issues/10066) SOP 步骤乱序执行 (P0) | 已接受 8/17 起，无 fix PR | 高 |
| [#10604](https://github.com/zeroclaw-labs/zeroclaw/pull/10604) OpenCode session 头修复 | needs-author-action | 高（S1 + 账号风险） |
| [#9134](https://github.com/zeroclaw-labs/zeroclaw/pull/9134) 插件字节准入 | blocked / do-not-merge，挂起近 2 月 | 高 |
| [#9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109) Hailo-Ollama 原生支持 | blocked / do-not-merge | 高 |
| [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) 决策队列 tracker | 持续积压，与"50 PR 零合并"互为因果 | 流程性 |
| #9819 / #8965 / #9535 / #10407 等多个 XL PR | 长期 needs-author/maintainer-action | 高 |

**健康度总评**：社区输入量充足、Issue 质量高、bug 修复闭环速度快（当日开闭），但**合并吞吐为零**且大量 XL PR 长期滞留，配合治理类 RFC 的讨论热度，下一步瓶颈在 review 带宽与决策流程，而非贡献量。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 · 2026-09-14

## 1. 今日速览

Hermes Agent 今日保持高活跃度：过去 24 小时共 100 条 Issue/PR 更新（Issues 40 新开活跃 + 10 关闭；PR 34 待合并 + 16 合并/关闭），无新版本发布。最突出的信号是 **state.db WAL 文件句柄问题在 fleet 重启场景下集中爆发**（#109966、#110497 为同一根因簇），多名用户报告网关被长时间阻塞。另一方面，维护者 @teknium1 持续批量合入修复与移植 PR，社区贡献者贡献了多个高质量新 PR（如 #110537、#110531），修 bug 响应速度整体健康。

## 2. 版本发布

今日无新版本发布。需注意 **0.21.0 的 schema v2→v3 迁移缺口**（#103363）仍在影响存量 Telegram 用户，下一次版本发布需关注是否补上迁移触发逻辑。

## 3. 项目进展

今日共 16 个 PR 合并/关闭，代表性进展：

- **#96068**（已关闭）：Telegram 大图 PNG 上传超时修复 — 超过 1MB 的图片预压缩为渐进 JPEG，消除 `media_write_timeout` 失败。([PR #96068](https://github.com/NousResearch/hermes-agent/pull/96068))
- **#98063**（已关闭）：`hermes doctor` 在所有 gh CLI 版本上正确检测认证，同时修复 #98051 与 #95162 的回归。([PR #98063](https://github.com/NousResearch/hermes-agent/pull/98063))
- **#96557**（已关闭）：`WHATSAPP_ENABLED=true` 不再覆盖显式的 `platforms.whatsapp.enabled: false`，env 强制启用问题全平台收口（对应 Issue #73289 同日关闭）。([PR #96557](https://github.com/NousResearch/hermes-agent/pull/96557))
- **#97280**（已关闭）：消除 banner update-check 守护线程污染 subprocess mock 的 CI flake 类。
- **#95257 / #95267**（已关闭）：`hermes worktree` 支持 `--json`/`--older-than`；大会话切换模型前确认以避免缓存击穿费用。([PR #95267](https://github.com/NousResearch/hermes-agent/pull/95267))
- **#97629**（已关闭）：cron 任务 prompt 中的重复性语言不再诱导 agent 自我再调度。

整体看，今日合并集中在**消息投递可靠性、CLI 兼容性、成本控制**三个方向，属于稳定性和运维体验的持续加固。

## 4. 社区热点

- **#109966 [P1]** — 8 条评论，今日最热。Fleet 重启后长生命周期进程持有已删除的 `-wal`/`-shm` inode，导致后续所有 opener 被拒数小时。与同日新开的 #110497（标记 duplicate）构成同一故障面，反映**多进程/多网关部署场景下 SQLite WAL 生命周期管理是当前最大痛点**。([Issue #109966](https://github.com/NousResearch/hermes-agent/issues/109966))
- **#59293 [security, P2]** — 7 条评论。`hermes config set` 可绕过系统配置写保护、无门禁关闭审批层，直击 agent 安全边界的核心诉求，仍处 `needs-decision` 状态。([Issue #59293](https://github.com/NousResearch/hermes-agent/issues/59293))
- **#60789 [P2]** — 7 条评论，7 月至今未修复。`session_search(profile=...)` 静默搜索当前 profile，属数据正确性问题。
- **#98382 [P1]** — 6 条评论。插件 observer-hook 并发调用被误判为超时丢弃，影响插件生态可靠性。

## 5. Bug 与稳定性（按严重度）

| 级别 | Issue | 问题 | Fix 状态 |
|---|---|---|---|
| P1 | [#109966](https://github.com/NousResearch/hermes-agent/issues/109966) / [#110497](https://github.com/NousResearch/hermes-agent/issues/110497) | state.db WAL sidecar 被短命进程 unlink，网关永久阻塞 | ⚠️ 暂无专门 fix PR，仅 [#109600](https://github.com/NousResearch/hermes-agent/pull/109600) 处理相关的 fleet 重启残留 marker |
| P1 | [#98382](https://github.com/NousResearch/hermes-agent/issues/98382) | 并发 observer-hook 被误丢 | 无 fix PR |
| P1 | [#103363](https://github.com/NousResearch/hermes-agent/issues/103363) | 0.21.0 schema v2→v3 迁移未触发，Telegram 改名静默失效 | 无 fix PR |
| P2 | [#110530](https://github.com/NousResearch/hermes-agent/issues/110530) | MCP 参数名含 `properties` 时 schema 修复逻辑误判 → 400 | ✅ 同日即有 [PR #110537](https://github.com/NousResearch/hermes-agent/pull/110537)（响应极快） |
| P2 | [#110526](https://github.com/NousResearch/hermes-agent/issues/110526) | Windows 上 skill 安装被截断（213 文件只装 52 个） | ✅ [PR #110529](https://github.com/NousResearch/hermes-agent/pull/110529) 同日提交 |
| P2 | [#63577](https://github.com/NousResearch/hermes-agent/issues/63577) | Windows `hermes update` 杀会话/毁本地提交 | ✅ [PR #110531](https://github.com/NousResearch/hermes-agent/pull/110531) 修复桌面端 30s 退出中止问题 |
| P2 | [#107899](https://github.com/NousResearch/hermes-agent/issues/107899) | WhatsApp 客户对话泄露 5 类内部诊断信息 | 无 fix PR，生产用户受影响 |
| P2 | [#55487](https://github.com/NousResearch/hermes-agent/issues/55487) | WeCom 断连 busy-loop 打满 CPU 冻结全平台 | 长期未修 |
| P2 | [#107905](https://github.com/NousResearch/hermes-agent/issues/107905) | resume 上限把 compaction 世代副本计入，4.7k 消息会话被拒 | 无 |

**观察**：新报 bug（今日提交的）当天就有 fix PR，响应链路健康；但**存量 P1/P2（WAL、hook 并发、WeCom）修复滞后**，且 Windows 平台仍是问题重灾区。

## 6. 功能请求与路线图信号

- **[#108914](https://github.com/NousResearch/hermes-agent/pull/108914)（Open，超大 PR）**：Bot Screen — 每个 bot 独享 Xfce 桌面并串流到 Hermes Desktop，支持人工接管完成 2FA 后交还。这是向“agent 自主操作 GUI + 人机协作”方向的重大能力扩展，结合 #92524 讨论热度，很可能成为下一版本主打特性。
- **[#106742](https://github.com/NousResearch/hermes-agent/pull/106742)（Open，P1）**："One gateway owns every local session" 统一架构 — CLI/TUI/Desktop/ACP/bot/cron 共享同一活会话。这是当前最大的架构级重构，直接关联今日多个 session-state 类 bug，值得维护者优先推进。
- **[#110527](https://github.com/NousResearch/hermes-agent/pull/110527)**：会话级临时工具集（session-owned toolsets），扩展插件生态能力。
- **[#110536](https://github.com/NousResearch/hermes-agent/issues/110536)**：要求 skill 选择“窄化、显式、模型中立”，呼应 GPT-6 时代上下文成本考量，方向合理。
- **[#110528](https://github.com/NousResearch/hermes-agent/issues/110528)**：Kanban 阻塞任务自动升级给创建者 agent，完善多自主工作流闭环。

## 7. 用户反馈摘要

- **多网关/fleet 用户**苦于 WAL 阻塞问题数小时不可用（#109966），属当前最尖锐的生产事故反馈。
- **客服场景用户**（#107899，印尼语报告）对内部诊断信息泄露到客户聊天强烈不满，说明 customer-facing 部署模式需要一等公民支持。
- **Windows 用户**持续抱怨更新流程（#63577、#110531）与 skill 安装（#110526）的脆弱体验。
- **插件/开发者生态**对 hook 并发丢弃（#98382）、MCP schema 兼容（#110530）反馈积极于快速修复，但对 `hermes config set` 语义问题（#59293、#76457）长期未决感到沮丧。
- **成本敏感用户**欢迎 #95267 的缓存确认机制 — 大会话切模型的隐性费用是真实付费痛点。

## 8. 待处理积压

| Issue | 年龄 | 状态信号 |
|---|---|---|
| [#55487](https://github.com/NousResearch/hermes-agent/issues/55487) WeCom busy-loop | ~2.5 个月 | 仅 2 评论，疑似缺乏维护者复现环境 |
| [#59293](https://github.com/NousResearch/hermes-agent/issues/59293) 安全绕过 | ~2 个月 | `needs-decision` 悬而未决，**安全问题应提级** |
| [#60789](https://github.com/NousResearch/hermes-agent/issues/60789) profile 搜索错误 | ~2 个月 | `awaiting-reporter`，数据正确性问题不应久拖 |
| [#63577](https://github.com/NousResearch/hermes-agent/issues/63577) Windows 更新 | ~2 个月 | 已有部分 fix PR（#110531），需合并收口 |
| [#98382](https://github.com/NousResearch/hermes-agent/issues/98382) hook 并发丢弃 | ~2 周 | P1 无认领 |
| [#108914](https://github.com/NousResearch/hermes-agent/pull/108914) / [#106742](https://github.com/NousResearch/hermes-agent/pull/106742) | — | 两个大型 Open PR 长期占用 review 带宽，建议尽快排期评审 |

**健康度小结**：响应速度良好（当日 bug 当日 fix），但 P1 级会话状态/稳定性积压与 Windows 体验是两大短板；安全类 issue #59293 建议维护者尽快给出决策。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 — 2026-09-14

## 1. 今日速览

PicoClaw 过去 24 小时共有 9 条 Issues/PR 动态（Issues 5 条、PR 4 条），但**无新代码合并、无新版本发布**。值得注意的是，今日动态以“关闭陈旧条目”为主：2 条 Issue 和 4 条 PR 均被标记 `[stale]` 或关闭，其中部分是长期积压的社区贡献（最早可追溯至 2026-02），显示维护者正在进行一轮 backlog 清理。活跃讨论集中在 Web UI 性能和长消息处理两条 Issue 上，社区对低性能设备体验的诉求持续升温。

## 2. 版本发布

今日无新版本发布。（最新已提及版本仍为 0.3.1）

## 3. 项目进展

今日无 PR 被合并，4 条 PR 全部被关闭，且多为积压已久的陈旧贡献：

- **PR #20**（[链接](https://github.com/sipeod/picoclaw/pull/20)，2026-02 创建）：修复 README 配置示例（OpenRouter `api_base`、snake_case 键名等）——被关闭，文档问题未落地。
- **PR #1545**（[链接](https://github.com/sipeed/picoclaw/pull/1545)，2026-03 创建）：尝试合并 5 个待合并修复 PR 的聚合 PR——被关闭。
- **PR #1268**（[链接](https://github.com/sipeed/picoclaw/pull/1268)）：iMessage 支持、stop 命令、隐私 sanitizer 等功能集——被关闭。
- **PR #3348**（[链接](https://github.com/sipeed/picoclaw/pull/3348)）：捷克语 i18n 补全——被关闭。

⚠️ **风险信号**：今日关闭均为“清理性关闭”而非合并，多个有价值的社区贡献（iMessage 支持、文档修复、i18n）未经合并即被关闭，可能造成贡献者流失。项目今日实质功能推进为零。

## 4. 社区热点

- **#3287 [Feature] IRC 长消息支持**（12 条评论，持续至 09-13）——[链接](https://github.com/sipeed/picoclaw/issues/3287)
  IRC 512 字节限制导致长消息被客户端切分，用户希望 PicoClaw 将切分消息识别为单一连贯消息。诉求本质：**多渠道接入场景下的消息完整性**。
- **#3281 [BUG] Web UI 输入卡顿**（11 条评论，2 👍）——[链接](https://github.com/sipeed/picoclaw/issues/3281)
  聊天历史变长后输入框明显卡顿，讨论热度高，且与 #3350（嵌入式设备同样问题）形成呼应，是当前最痛的体验问题。

## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 | Fix PR |
|---|---|---|---|
| 🔴 高 | [#3281](https://github.com/sipeed/picoclaw/issues/3281) Web UI 历史变长后输入严重卡顿（v0.3.1） | OPEN，活跃讨论 | 暂无 |
| 🔴 高 | [#3351](https://github.com/sipeed/picoclaw/issues/3351) session 自动压缩**物理删除**原始记录，历史不可恢复（`pkg/memory/jsonl.go` 的 `rewriteJSONL` 覆盖 jsonl 文件） | 已关闭（stale） | 暂无 |
| 🟠 中 | [#3350](https://github.com/sipeed/picoclaw/issues/3350) 嵌入式/低性能设备（RV1106、RISC-V）输入框打字卡顿、CPU 飙升 | 已关闭（stale） | 暂无 |

⚠️ **#3351 数据丢失类问题被以 stale 关闭且无修复**，属于较严重的稳定性/数据安全信号，建议维护者重新评估。

## 6. 功能请求与路线图信号

- **#3369 OpenCode Go session header 支持**（2 👍）——[链接](https://github.com/sipeed/picoclaw/issues/3369)：需要 OpenAI 兼容 provider 支持映射 `x-opencode-session` header。改动集中在 provider 层，实现成本低，是**最可能进入下一版本**的候选。
- **#3287 IRC 长消息合并处理**：讨论充分（12 评论），涉及 IRCv3 特性，适合作为 channel 层增强纳入规划。
- 被关闭的 PR #1268（iMessage 支持、stop 命令、隐私 sanitizer）反映社区对**渠道扩展和隐私功能**有真实需求，即便该 PR 未合并，方向值得吸收。

## 7. 用户反馈摘要

- **痛点 1：Web UI 性能随历史增长劣化**——桌面（#3281）与嵌入式（#3350）用户双重印证，输入每字符都有延迟，说明前端可能在每次输入时对全量历史做了不必要的处理。
- **痛点 2：数据不可逆丢失**（#3351）——用户检查 `.jsonl` 文件确认压缩后原始记录被物理删除，“不是显示问题”，对记忆压缩机制的持久化设计不满。
- **痛点 3：贡献被冷落**——多个 2026 年初的 PR（#20、#1268、#1545）长期无响应后被关闭，贡献者体验欠佳。
- **满意点**：用户深入到源码层面定位问题（如 jsonl.go 的 rewrite 逻辑），且积极提出修复方案，说明社区技术参与度较高、对项目本身有较强粘性。

## 8. 待处理积压

| 条目 | 创建时间 | 状态 | 建议 |
|---|---|---|---|
| [#3281](https://github.com/sipeed/picoclaw/issues/3281) 输入卡顿 | 07-21 | OPEN，11 评论 | 高优，影响核心体验，需维护者给出修复时间表 |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) IRC 长消息 | 07-22 | OPEN，12 评论 | 讨论成熟，等待方案拍板 |
| [#3369](https://github.com/sipeed/picoclaw/issues/3369) OpenCode header | 09-06 | OPEN | 低成本改进，建议尽快认领 |
| 已关闭的 #3351 / #3350 | 08-30 | stale 关闭 | 数据丢失与嵌入式性能问题不应仅以 stale 处理，建议重开或转化为 roadmap 项 |

---
**健康度小结**：今日项目呈“高讨论、零合并”状态。清理积压是好事，但连续关闭有价值的社区贡献而无替代方案，加上核心性能/数据安全 Issue 未解决即关闭，短期健康度偏弱，建议维护者尽快回应 #3281 与 #3351 两条高热 Issue。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报 — 2026-09-14

## 1. 今日速览

今日 NanoClaw 处于**中等偏高的活跃状态**：过去 24 小时内有 16 条 PR 更新（14 条待合并）、5 条 Issue 更新（4 新开/活跃、1 关闭），无新版本发布。活动焦点集中在两条主线上：**安装/Setup 链路的回归修复**（provider picker、Codex 认证、linger 校验）与 **Mattermost 通道的可靠性加固**（一组 5+ 个相关 PR）。社区贡献者 @glifocat 与 @foxsky 密集提交高质量 bug 报告，其中 #3790 已快速修复关闭，显示维护团队响应迅速。

## 2. 版本发布

本期无新版本发布，修复仍处于 `main` 分支滚动合入阶段。

## 3. 项目进展

### 已关闭的 PR

- **PR #3790** [fix(setup): restore the agent provider picker for fresh installs](https://github.com/nanocoai/nanoclaw/pull/3790) — 修复了社区门户 PR #3729 引入的回归：`askAgentProviderChoice` 在 `DEFAULT_AGENT_PROVIDER` 解析为 `claude` 时跳过运行时选择器，导致全新安装无法选择 Codex 等可安装 provider。当日报告（#3787）、当日修复，闭环速度值得肯定。
- **PR #3792** [fix(setup): bootstrap pinned Codex CLI for auth](https://github.com/nanocoai/nanoclaw/pull/3792) — 解决全新 Codex 设置要求全局安装 CLI 的问题，允许无特权用户在默认 `/usr` prefix 下完成认证。对应 Issue #3791。

两项修复共同恢复了“全新安装 → 选择任意 provider → 完成认证”这条关键路径，是今日最实质的进展。

## 4. 社区热点

- **Issue #3787**（[链接](https://github.com/nanocoai/nanoclaw/issues/3787)，2 条评论，已关闭）：fresh install 跳过 provider picker 静默选择 Claude——用户对首装体验回归最敏感，好在当天即被 #3790 修复。
- **Issue #3643**（[链接](https://github.com/nanocoai/nanoclaw/issues/3643)，priority/high）：硬编码 30 分钟 `ABSOLUTE_CEILING_MS` 冷杀本地模型长回合任务。这是今日**唯一带 priority/high 标签**的活跃 Issue，涉及本地模型用户的硬性可用性，**目前仍无对应 fix PR**，值得维护者优先关注。
- **PR #3796**（[链接](https://github.com/nanocoai/nanoclaw/pull/3796)，@jhisse）：新增 `/add-telemetry` 技能，为 agent 容器导出 OpenTelemetry traces（覆盖 turns、模型调用、工具、子代理、压缩、后台任务），span 携带成本与 token 缓存明细——反映了社区对**可观测性**的强烈诉求。

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 状态 |
|---|---|---|
| 高 | [#3643](https://github.com/nanocoai/nanoclaw/issues/3643) 30 分钟硬超时冷杀本地模型长回合，无配置接口 | ❌ 暂无 fix PR |
| 中 | [#3801](https://github.com/nanocoai/nanoclaw/issues/3801) `update-nanoclaw validate` 通道刷新会覆盖本地补丁修改过的文件 | ❌ 今日新开 |
| 中 | [#3800](https://github.com/nanocoai/nanoclaw/issues/3800) 文档化的 controller 提取遗漏 3 个脚本导致 controller 无法加载 | ❌ 今日新开 |
| 中 | [#3791](https://github.com/nanocoai/nanoclaw/issues/3791) Fresh Codex setup 需全局 CLI | ✅ 已由 PR #3792 处理 |
| 已修复 | [#3787](https://github.com/nanocoai/nanoclaw/issues/3787) 首装跳过 provider picker | ✅ PR #3790 已关闭 |

另有一批待合并的稳定性修复 PR：#3789（watch feed 订阅失败不得破坏 arming）、#3463（OpenCode provider 时序竞态 fallback）、#3779（重启后校验 host 身份与就绪）。

## 6. 功能请求与路线图信号

- **Tools-only 投递模式**：PR #3713（per-agent-group `delivery_mode` 配置）+ PR #3781（agent-runner 强制 tools-only 投递）构成一个完整功能对，针对无法稳定产出 final-text envelope 的 provider（如本地模型）。两 PR 均在活跃推进，很可能一并进入下一版本。
- **可观测性**：PR #3796 OpenTelemetry 技能若合入，将填补运维监控空白。
- **Codex 认证结构化**：PR #3489 提供结构化 setup-driver 认证（浏览器/设备码登录、类型化 driver 事件），是 provider 生态扩展的重要一步。
- **Mattermost 通道治理**：PR #3777/#3778/#3780/#3797 一组重构+加固，方向是“NanoClaw 只负责连接、不托管服务器”，架构边界更清晰。

## 7. 用户反馈摘要

- **本地模型用户**是当前最痛的群体：长任务被 30 分钟硬超时杀掉（#3643），且 OpenCode provider 存在最终文本丢失竞态（#3463）。
- **首次安装体验**脆弱：provider picker 回归（#3787）、Codex 需全局 CLI（#3791）、最小化主机上 polkit 交互问题（PR #3798）——集中在无特权/精简环境。
- **高级自托管用户**（@foxsky）报告 update 流程破坏本地定制（#3800、#3801），说明存在一批深度魔改部署的用户群体。
- 整体看，反馈质量高、复现信息完整，社区与维护者协作模式健康。

## 8. 待处理积压

- **#3643（priority/high，创建于 08-28，仅 1 条评论）**：高优先级 bug 挂钩近三周无修复动静，是当前最显眼的积压项，建议尽快给出配置 seam（如可配置 ceiling）或与 #3713 的 delivery_mode 工作统筹考虑。
- **PR #3489**（08-23 开启）与 **PR #3463**（08-23 开启）：两个重要的 provider 级 PR 已开启三周仍未合并，需确认评审阻塞点。
- **PR #3463 所修复的 Issue #2985** 存在约 78ms 的时序竞态窗口，属难以稳定复现的问题，建议尽快落地。

---
*数据来源：NanoClaw GitHub 仓库过去 24 小时活动快照。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-09-14

## 1. 今日速览

IronClaw 今日整体活跃度**偏低**，属于典型的维护型日常节奏。过去 24 小时内无新 Issue、无新版本发布，PR 动态全部来自 dependabot 自动化依赖更新（5 条，其中 1 条已关闭）。项目处于「依赖维护期」，核心功能开发暂无新的公开进展，无用户反馈或社区讨论产生。项目健康度方面：依赖更新及时、自动化维护机制运转正常，但需注意积压的待合并依赖 PR 数量在增长。

## 2. 版本发布

今日无新版本发布，最近亦无 Release 记录。省略。

## 3. 项目进展

- **[#8097](https://github.com/nearai/ironclaw/pull/8097) [已关闭]** — dependabot 的 Rust 依赖批量更新（24 项，含 uuid、base64、rust_decimal 等）被关闭。结合次日重新提交的 #8099 推断，这是因上游依赖（如 uuid）在窗口期内又发新版（1.26.0 → 1.26.1），dependabot 以新 PR 替代旧 PR，属常规轮替而非人工拒绝信号。
- **[#8099](https://github.com/nearai/ironclaw/pull/8099) [待合并]** — 新一轮 Rust 依赖批量升级（25 项），是今日唯一新增 PR，替代 #8097。

今日无功能性合并，项目在功能维度无净推进；进展主要体现在依赖面的持续保鲜。

## 4. 社区热点

今日**无任何社区讨论**：0 条 Issue 更新，PR 评论数据为空，👍 反应均为 0。无热点可分析。这一信号本身值得留意——连续的零 Issue 活跃可能意味着：用户群较小、问题反馈渠道在其他平台（如 Discord/论坛），或项目处于稳定期。

## 5. Bug 与稳定性

今日**无新报告的 Bug、崩溃或回归问题**。依赖升级 PR 中也未附带破坏性修复说明，无 fix PR 需标注。

## 6. 功能请求与路线图信号

今日无新功能请求。可从依赖维度间接观察路线图信号：

- **[#8078](https://github.com/nearai/ironclaw/pull/8078)** 升级 tower-http 与 tokio-tungstenite，表明项目持续投资于 HTTP/WebSocket 服务能力，异步网络栈是活跃维护方向。
- **[#7834](https://github.com/nearai/ironclaw/pull/7834)** 升级 wasmtime/wit-component 等 wasm 工具链，且带有 `size: L, risk: medium` 标签，说明 WASM 沙箱/插件运行时是项目的重量级长期方向，值得用户关注其插件生态演进。
- **[#8079](https://github.com/nearai/ironclaw/pull/8079)** 中 anthropics/claude-code-action 从 1.0.183 升至 1.0.221，暗示仓库在 CI 中使用 AI 辅助自动化流程。

## 7. 用户反馈摘要

今日无 Issue 评论数据，无法提炼用户痛点或使用场景反馈。建议维护者核查是否存在 Issue 活动外流（社区论坛、社交渠道）的情况。

## 8. 待处理积压

以下 PR 长期处于待合并状态，建议维护者关注：

| PR | 状态 | 积压时长 | 说明 |
|---|---|---|---|
| [#7834](https://github.com/nearai/ironclaw/pull/7834) | OPEN | **约 3 周**（08-23 创建） | wasm 组 4 项升级，标记 `size: L, risk: medium`，积压时间最长、风险最高，建议优先评审，避免与后续依赖 PR 产生冲突 |
| [#8078](https://github.com/nearai/ironclaw/pull/8078) | OPEN | 8 天 | tokio 生态升级（tower-http、tokio-tungstenite） |
| [#8079](https://github.com/nearai/ironclaw/pull/8079) | OPEN | 8 天 | GitHub Actions 升级（6 项，含 setup-node 大版本 4→7，可能有 CI 配置兼容性风险） |

**健康度提醒**：目前共 4 条待合并依赖 PR 呈滚动积压趋势。#8097 的关闭/重开循环说明合并节奏落后于依赖发布节奏，长期如此会放大合并冲突成本。建议集中批量处理一轮依赖 PR，恢复「dependabot 提交 → 快速验证合并」的正常循环。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报（2026-09-14）

## 1. 今日速览

- 过去24小时共 4 条 Issue 更新（全部仍为 OPEN）、4 条 PR 更新（全部待合并），**无任何 Issue 关闭或 PR 合并**，也无新版本发布。
- 值得注意的是，今日活跃的 3 条 Issue（#1041、#1046、#1047）和全部 4 条 PR 均被标记为 `[stale]` 且创建于 2026-03-30，属于批量自动更新触发（stale bot 互动），并非真实社区新增活动。
- 唯一的真实新内容是 [#2660](https://github.com/netease-youdao/LobsterAI/issues/2660)——一条关于持久化用户/工作区记忆的功能提案，来自外部公司创始人。
- 综合判断：**项目当前处于低活跃/维护停滞状态**，社区贡献（尤其含 P0 安全修复的 PR #1042）长期未被合并，健康度需引起关注。

## 2. 版本发布

今日无新版本发布，最近亦无 Release 记录。省略。

## 3. 项目进展

**今日无任何 PR 合并、无 Issue 关闭，项目代码线零推进。**

当前积压的 4 条待合并 PR（均创建于 2026-03-30，已 stale 近半年）：

| PR | 内容 | 状态 |
|---|---|---|
| [#1038](https://github.com/netease-youdao/LobsterAI/pull/1038) | 修复流式响应 ReadableStream reader 异常时泄漏（资源泄漏） | 待合并，stale |
| [#1042](https://github.com/netease-youdao/LobsterAI/pull/1042) | 修复两个 P0 安全漏洞（SSRF + 任意文件读取） | 待合并，stale |
| [#1044](https://github.com/netease-youdao/LobsterAI/pull/1044) | Windows NSIS 安装器根目录路径规范化 | 待合并，stale |
| [#1045](https://github.com/netease-youdao/LobsterAI/pull/1045) | Agent 设置面板切换时未保存更改提示 | 待合并，stale |

## 4. 社区热点

- **[#2660 持久化用户与工作区记忆提案](https://github.com/netease-youdao/LobsterAI/issues/2660)**（今日唯一真实新帖，1 条评论）
  来自 MemCode 创始人 Vivek Gupta 的提案：指出 LobsterAI 覆盖研究、文档、幻灯、视频、网页等多任务场景，“上下文连续性”问题尤为突出——用户偏好、常用工作区、历史来源、未完成的决策应能跨会话保留。这反映了重度用户对**长期记忆能力**的核心诉求，且带有明显的商业合作/生态推广背景（MemCode 为记忆类产品）。
- **[#1041 SSRF 与任意文件读取安全漏洞](https://github.com/netease-youdao/LobsterAI/issues/1041)**（今日因 stale 更新再次浮现）
  报告 `api:fetch`/`api:stream` IPC 可探测内网、请求云 metadata 窃取 IAM 凭证，`readFileAsDataUrl` 可读取任意本地文件。虽有对应修复 PR #1042，但长期未合并，是当前最紧迫的风险点。

## 5. Bug 与稳定性（按严重程度）

1. **🔴 P0 安全漏洞**：[#1041](https://github.com/netease-youdao/LobsterAI/issues/1041) — SSRF + 任意本地文件读取。**已有 fix PR：[#1042](https://github.com/netease-youdao/LobsterAI/pull/1042)**，但未合并。
2. **🟠 资源泄漏**：[#1038](https://github.com/netease-youdao/LobsterAI/pull/1038)（PR 直接修复，无独立 Issue）— 网络中断、用户停止会话等场景下 ReadableStream reader 永久泄漏，持有底层 TCP 连接。**修复 PR 即该 PR 本身，待合并。**
3. **🟡 功能性 Bug**：[#1047](https://github.com/netease-youdao/LobsterAI/issues/1047) — 已清除的技能在切换 Agent 后仍然存在（数据未真正清除，可能涉及状态同步/持久化问题）。无关联 fix PR。
4. **🟡 配置问题**：[#1046](https://github.com/netease-youdao/LobsterAI/issues/1046) — 上下文窗口被硬限制为 200K，而 Qwen3.5-Plus 官方支持 1M，文档缺失且无用户侧配置项。无关联 fix PR。

今日无崩溃/回归类新报告。

## 6. 功能请求与路线图信号

- **持久化记忆**（[#2660](https://github.com/netease-youdao/LobsterAI/issues/2660)）：今日新增，属外部提案。结合当前维护节奏，短期内纳入可能性存疑，但“跨会话记忆”是 AI 助手赛道的高频需求，值得纳入路线图评估。
- **上下文窗口可配置**（[#1046](https://github.com/netease-youdao/LobsterAI/issues/1046)）：诉求明确（解锁模型原生 1M 上下文 + 补充文档），实现成本低、用户价值高，是较易落地的改进项。
- **未保存更改提示**（PR [#1045](https://github.com/netease-youdao/LobsterAI/pull/1045)）：社区已自行实现并提交，合并即可获得，与 Issue #1047（技能清除失效）同属 Agent 设置持久化体验问题。

## 7. 用户反馈摘要

- **数据丢失是真实痛点**：#1047（技能清除后“复活”）与 PR #1045（切换 Agent 丢失未保存修改）共同指向——用户在多 Agent 工作流中对**设置变更未可靠持久化**感到困扰。
- **进阶用户受限于硬编码参数**：#1046 反映接入大上下文模型（Qwen3.5-Plus 1M）的用户被 200K 上限卡住，且文档未解释原因，产生挫败感。
- **安全意识用户表示担忧**：#1041 报告者提供了详尽的漏洞复现与代码定位，说明有技术型用户在认真审计 Electron IPC 面，但修复迟迟未合并可能消耗社区信任。
- **生态合作意向**：#2660 显示外部 AI 记忆产品希望与 LobsterAI 集成或共建，侧面印证项目在多任务 Agent 场景的用户基础。

## 8. 待处理积压 ⚠️

以下条目均已 stale 约 5.5 个月，**建议维护者优先处理**：

1. **🔴 最紧急**：PR [#1042](https://github.com/netease-youdao/LobsterAI/pull/1042)（P0 安全修复）及 Issue [#1041](https://github.com/netease-youdao/LobsterAI/issues/1041) — 涉及 SSRF 与任意文件读取，拖得越久风险越大。
2. PR [#1038](https://github.com/netease-youdao/LobsterAI/pull/1038)（reader 泄漏修复）— 长期泄漏可能导致连接耗尽。
3. Issue [#1047](https://github.com/netease-youdao/LobsterAI/issues/1047)（技能清除失效）— 无任何修复进展。
4. Issue [#1046](https://github.com/netease-youdao/LobsterAI/issues/1046)（上下文窗口限制）— 至少应补充文档说明。
5. PR [#1044](https://github.com/netease-youdao/LobsterAI/pull/1044)、PR [#1045](https://github.com/netease-youdao/LobsterAI/pull/1045) — 低风险体验改进，作者注明未在本地完整测试，需维护者验证后合并。
6. Issue [#2660](https://github.com/netease-youdao/LobsterAI/issues/2660) — 今日新开，建议及时回复以维持社区/合作方好感。

---
**健康度小结**：今日表面活跃（8 条更新）实为 stale 机器人和一条外部提案驱动；项目核心问题在于**高质量社区贡献（尤其安全修复）长期无人响应**。若此状态持续，建议社区关注项目维护状态并评估依赖风险。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw 项目日报 — 2026-09-14

## 1. 今日速览

今日 TinyClaw 项目整体活跃度处于**低位平稳**状态：过去 24 小时无 PR 更新、无版本发布，仅有 1 条新开 Issue（#296），讨论尚无后续评论。该 Issue 由第三方公司创始人发起，围绕“跨 agent-team 运行的持久化记忆/上下文保留”展开，属于战略性功能讨论而非缺陷报告。总体来看，项目代码层面今日无推进，社区侧出现一个高质量外部合作信号，值得维护者跟进。

## 2. 版本发布

今日无新版本发布。最新 Releases 记录为空，建议关注仓库 tag/Release 页面获取后续动态。

## 3. 项目进展

今日无 PR 合并或关闭，代码库无实质推进。功能迭代节奏暂无法从本日数据评估，需结合多日趋势观察。

## 4. 社区热点

- **[#296 [OPEN] Could TinyAGI preserve approved context across agent-team runs?](https://github.com/TinyAGI/tinyagi/issues/296)** — 今日唯一活跃讨论（创建于 2026-09-13，0 评论，0 👍）。
  - 发起者：@memcodeoff（自称 MemCode 创始人兼 CEO Vivek Gupta）
  - 诉求分析：TinyAGI 面向“一人公司”编排 agent 团队，角色设定、委派任务、运行偏好与已验证成果天然会在多次运行间重复。用户希望引入**持久化记忆（durable memory）**，使团队跨运行保持一致性，而无需每次重新展开（expand）上下文。这既是功能请求，也隐含了潜在的商务/生态合作信号（MemCode 为记忆类产品），维护者可借此评估内置记忆层或第三方记忆集成的路线。

## 5. Bug 与稳定性

今日无新增 Bug、崩溃或回归报告。无待修复问题，无关联 fix PR。

## 6. 功能请求与路线图信号

- **持久化/跨运行上下文记忆**（来源：[#296](https://github.com/TinyAGI/tinyagi/issues/296)）
  - 当前状态：仅有 Issue，无对应 PR。
  - 判断：该需求切中 agent 编排产品的共性痛点（角色一致性、偏好记忆、成果沉淀），且与 TinyAGI“agent 团队”定位高度契合。若维护者认可，可能以“approved context / memory store”形式进入下一阶段路线图；但今日无任何 PR 前置工作，短期内落地概率低，建议先在 Issue 中回应以明确方向。

## 7. 用户反馈摘要

- **使用场景**：一人公司（one-person company）场景下用 TinyAGI 编排多 agent 团队，任务委派与角色分工是核心使用模式。
- **痛点**：跨运行的一致性问题——每次运行需重复建立角色、偏好、已验证成果等上下文，成本高且易不一致。
- **期望**：以“经批准的上下文（approved context）”形式持久复用，而非简单扩大上下文窗口。
- 注：该 Issue 暂无其他用户附议（0 评论、0 👍），代表性有限，需持续观察是否形成共鸣。

## 8. 待处理积压

- **[#296](https://github.com/TinyAGI/tinyagi/issues/296)**（2026-09-13 创建，尚无维护者回复）：虽然仅开立一天，但该 Issue 兼具功能讨论与外部合作属性，且直指产品核心竞争力方向，建议维护者尽早回应，避免错失社区/生态机会。后续若持续无响应，将纳入积压跟踪。

---
*数据来源：TinyAGI/tinyagi GitHub 仓库，统计窗口 2026-09-13 至 2026-09-14。本报告由自动化分析生成，建议结合多日数据判断项目健康度趋势。*

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 · 2026-09-14

> 数据来源：github.com/moltis-org/moltis 过去 24 小时

---

## 1. 今日速览

Moltis 今日保持稳定的中等活跃度：过去 24 小时共 3 条 Issue 更新（新开 1、关闭 2）、5 条 PR 更新（合并/关闭 4、待合并 1），并发布 1 个新版本 `20260913.02`。核心贡献者 [@penso](https://github.com/penso) 依然是最主要的驱动力，今日关闭了多项功能与修复 PR。Issue 关闭速度快于新增，积压呈净下降趋势，项目健康度良好。

---

## 2. 版本发布

- **[20260913.02](https://github.com/moltis-org/moltis/releases)**（发布于 2026-09-13）
  - Release Note 未附详细说明，但从当日合入的 PR 推断，本版本大概率包含：默认推理等级持久化（#1266）、Telegram 共享聊天工具策略控制（#1265）、`max` 推理等级（#1253）及依赖更新（#1263）。
  - 暂未见破坏性变更公告；升级后建议关注 `chat.reasoning_default` 新配置项及 Telegram `untrusted_audience` / `untrusted_tools` 相关行为变化。

---

## 3. 项目进展

今日关闭 4 个 PR，功能与修复双线推进：

| PR | 内容 | 意义 |
|---|---|---|
| [#1266](https://github.com/moltis-org/moltis/pull/1266) | 持久化可配置的默认推理等级（closes #1259） | 补齐会话间配置持久化体验 |
| [#1265](https://github.com/moltis-org/moltis/pull/1265) | Telegram 暴露共享聊天工具策略控制（fixes #1264） | 对齐 Slack 的安全策略能力，修复 Telegram 工具失效问题 |
| [#1253](https://github.com/moltis-org/moltis/pull/1253) | 新增 `max` 推理等级，含 `@reasoning-max` 后缀解析 | 与 #1266 共同完善推理等级体系 |
| [#1263](https://github.com/moltis-org/moltis/pull/1263) | dependabot 批量依赖更新（babel、astro、js-yaml 等） | 例行安全维护 |

**待合并**：[#1267](https://github.com/moltis-org/moltis/pull/1267)（fix(hooks): 派发 agent 与出站消息生命周期事件，fixes #1255）——引入 `AgentEnd` / `MessageSending` 事件并在最终发布前支持内容重写与拦截，是 hooks 体系的重要补强，建议维护者优先评审。

**评估**：推理等级体系（#1253 + #1266）与多渠道安全策略（#1265）两条主线今日均闭环，配合新版本发布，项目整体向前推进明显。

---

## 4. 社区热点

今日最值得关注的是新开 Issue：

- **[#1268](https://github.com/moltis-org/moltis/issues/1268)**「Could Moltis expose an optional advanced memory provider?」——由 MemCode 创始人 @memcodeoff 提出，建议 Moltis 暴露可选的高级记忆提供者接口。这反映了商业生态方希望基于 Moltis 的持久化/跨会话记忆能力做扩展集成的诉求，属于典型的**插件化/开放接口**信号，值得维护者尽早回应以明确项目边界（是否接受商业 provider 集成）。

其余 Issue/PR 今日评论均为 0，无大规模讨论热点，社区互动集中在贡献者的代码流层面。

---

## 5. Bug 与稳定性

- 🔴 **[已修复] #1264**「Tools stop working in shared Telegram channels」（[@stratus-ss](https://github.com/moltis-org/moltis/issues/1264)）——Telegram 共享频道工具全部失效，根因是 Telegram 继承了网关的 deny-all 工具上限但未暴露 Slack 已有的配置项。**已有 fix：[#1265](https://github.com/moltis-org/moltis/pull/1265)，已关闭并随版本发布。**
- 🟡 **进行中**：[#1255 相关] PR [#1267](https://github.com/moltis-org/moltis/pull/1267) 修复 agent/出站消息生命周期事件缺失问题，尚待合并。

今日无崩溃或回归类报告。

---

## 6. 功能请求与路线图信号

- **#1259「可配置默认推理等级并跨会话持久化」→ 已通过 [#1266](https://github.com/moltis-org/moltis/pull/1266) 实现并关闭**，配合 #1253 的 `max` 等级，推理等级体系已完整落地，预计随 `20260913.02` 提供。
- **#1268「可选高级记忆 provider」**：尚处提案阶段、无代码进展。若维护者认可，或成为记忆子系统插件化的路线图项。
- 信号总结：近期路线聚焦**推理控制精细化**与**渠道安全策略统一**，#1267 合并后 hooks 生命周期也将更完整。

---

## 7. 用户反馈摘要

- 用户对**推理等级无法持久化**（#1259）表达了明确的易用性痛点，现已解决，反映团队响应用户体验反馈较快。
- Telegram 共享频道用户（#1264）暴露出**多渠道能力不对齐**的痛点——Slack 有的安全开关 Telegram 没有；#1265 表明团队正系统性拉平各渠道功能。
- 外部商业方（MemCode）主动寻求集成（#1268），侧面印证 Moltis 在本地化、安全沙箱、记忆持久化方面的定位获得社区认可。

---

## 8. 待处理积压

- **[#1267](https://github.com/moltis-org/moltis/pull/1267)**（OPEN）：修复 #1255 的 hooks 生命周期事件，今日创建待评审，建议尽快处理。
- **[#1268](https://github.com/moltis-org/moltis/issues/1268)**（OPEN）：尚无任何回应（0 评论 / 0 👍），涉及生态合作方向，建议维护者 48 小时内给出初步态度，避免错失外部集成机会。

整体积压情况健康，无长期（>7 天）未响应的遗留项。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报（2026-09-14）

## 1. 今日速览

项目今日保持高活跃度：过去 24 小时内 Issues 更新 17 条（新开/活跃 16，关闭 1），PR 更新 25 条（待合并 22，合并/关闭 3），无新版本发布。社区反馈集中在 **2.2.x 升级后的稳定性问题**——MCP 连接、会话丢失、服务端卡死等 Bug 报告密集出现，且多数已配套修复 PR，显示问题响应链路健康但 2.2.x 质量仍需收敛。多位首次贡献者提交 PR（i18n、providers、Telegram、MCP 等），社区外延贡献生态活跃。整体判断：**问题多但闭环快，处于版本后修复冲刺期**。

---

## 2. 版本发布

今日无新 Release。当前用户报告主要集中在 2.2.0 / 2.2.1 版本，下一版本预计将以稳定性修复为主。

---

## 3. 项目进展

今日合并/关闭 3 个 PR，以文档修正为主：

- **#7675 [CLOSED]** [docs(mcp)](https://github.com/agentscope-ai/QwenPaw/pull/7675)：修正中文 MCP 文档中错误的 `agent.json` 字段名（`tools.builtins` → `tools.builtin_tools`）。
- **#7706 [CLOSED]** [docs(multi-agent)](https://github.com/agentscope-ai/QwenPaw/pull/7706)：删除文档中不存在的 `qwenpaw providers` CLI 命令，统一为 `qwenpaw models`。

待合并队列（22 个）中有多个高质量修复，几乎逐条对应今日 Bug 报告：

- **#7742** [Creator 1.3.0 大版本插件升级](https://github.com/agentscope-ai/QwenPaw/pull/7742)：OpenCode Zen/Go endpoints、并行素材理解、风格锚点版本化、多集生产强化，体量最大。
- **#7725** [fix(workspace)](https://github.com/agentscope-ai/QwenPaw/pull/7725)：将阻塞式 `watchfiles.awatch` SSE 监听替换为线程化轮询，修复大仓库卡死整服务的问题（对应 #7721）。
- **#7734** [pt-BR 翻译补全](https://github.com/agentscope-ai/QwenPaw/pull/7734)：修复 #4009 遗留缺陷，从 3860/4275 key 补齐到完全对齐。

整体看，项目在 **稳定性修复 + Creator 功能扩展 + 国际化** 三条线并行推进。

---

## 4. 社区热点

- **#7571 [Agent 记忆遗忘问题]**（5 评论，持续 9 天）[链接](https://github.com/agentscope-ai/QwenPaw/issues/7571)：用户反复强调的开发路径约束（TODO 文件位置、源码目录）仍被 Agent 遗忘，甚至导致脚本部署时用旧代码覆盖运行时。核心诉求：**长期记忆/规则持久化机制不可靠**，是重度用户的最痛之处。
- **#7724 [会话丢失]**（4 评论）[链接](https://github.com/agentscope-ai/QwenPaw/issues/7724)：Windows 桌面端重部署插件后整个会话 + 模型配置丢失，用户称“反复遇到”（关联 #7708），涉及**数据持久化可靠性**。
- **#7722 [三路径叠加内存耗尽]**（2 评论）[链接](https://github.com/agentscope-ai/QwenPaw/issues/7722)：高质量报告，附受控复现 + 最小修复方案，涵盖无界流缓冲、keep-alive 实例堆叠、doom-loop 门控逃逸，技术含量高，值得维护者优先处理。
- **#7728 [Java MCP SDK 兼容]**（2 评论）[链接](https://github.com/agentscope-ai/QwenPaw/issues/7728)：非标准 `jsonRpcError` 信封导致 Driver 构建失败，已有对应修复 PR #7729。

---

## 5. Bug 与稳定性（按严重程度）

| 严重度 | Issue | 问题 | Fix PR |
|---|---|---|---|
| 🔴 高 | [#7721](https://github.com/agentscope-ai/QwenPaw/issues/7721) | 文件浏览器打开大仓库导致**整个服务冻结**，所有渠道停摆 | ✅ [#7725](https://github.com/agentscope-ai/QwenPaw/pull/7725) |
| 🔴 高 | [#7722](https://github.com/agentscope-ai/QwenPaw/issues/7722) | 三路径叠加内存耗尽（~1MB/s 增长 → OOM） | 部分（#7723 相关） |
| 🔴 高 | [#7724](https://github.com/agentscope-ai/QwenPaw/issues/7724) | 会话 + 模型配置丢失，数据不可恢复 | ❌ 暂无 |
| 🟠 中 | [#7716](https://github.com/agentscope-ai/QwenPaw/issues/7716) | 2.2.x 升级后 MCP 无法连接注册（2.1.1b3-hub 正常，疑似回归） | ✅ [#7735](https://github.com/agentscope-ai/QwenPaw/pull/7735) |
| 🟠 中 | [#7728](https://github.com/agentscope-ai/QwenPaw/issues/7728) | Java MCP SDK 服务端 500 信封不识别，Driver 构建失败 | ✅ [#7729](https://github.com/agentscope-ai/QwenPaw/pull/7729) |
| 🟠 中 | [#7726](https://github.com/agentscope-ai/QwenPaw/issues/7726) | ACP `trusted: true` 回退到交互式确认 | ✅ [#7732](https://github.com/agentscope-ai/QwenPaw/pull/7732) |
| 🟠 中 | [#7727](https://github.com/agentscope-ai/QwenPaw/issues/7727) | 工作区外写入拦截对 kimi-code Write 工具“失明”（**安全相关**） | ❌ 暂无 |
| 🟡 中 | [#7693](https://github.com/agentscope-ai/QwenPaw/issues/7693) | Creator 多图生成期间用户审批导致任务永久卡 RUNNING | ❌ 暂无 |
| 🟡 中 | [#7730](https://github.com/agentscope-ai/QwenPaw/issues/7730) | 插件目录离线回退失效 | ❌ 暂无 |
| 🟡 低 | [#7709](https://github.com/agentscope-ai/QwenPaw/issues/7709) | 定时任务输出被折叠/丢失 | ❌ 暂无 |
| 🟡 低 | [#7705](https://github.com/agentscope-ai/QwenPaw/issues/7705) | 默认工作目录设置不生效，回退旧值 | ❌ 暂无 |

**关注点**：#7727 是安全边界类问题（沙箱逃逸风险），且暂无修复 PR，建议优先排期。

---

## 6. 功能请求与路线图信号

- **#7733 [Agent 自主上下文管理]** [链接](https://github.com/agentscope-ai/QwenPaw/issues/7733)：提议在 context eviction 前给 Agent 预警与自主交接能力，与 PR [#7719（ReMeLight 记忆写入独立模型）](https://github.com/agentscope-ai/QwenPaw/pull/7719) 同属**记忆/上下文架构演进**方向，两者结合预示下一阶段可能在记忆系统上做大动作。
- **#7740 [Hub 管理员重置密码]** [链接](https://github.com/agentscope-ai/QwenPaw/issues/7740)：与 PR [#7696（本地管理员引导）](https://github.com/agentscope-ai/QwenPaw/pull/7696) 互补，Hub 运维功能在持续补齐，很可能被纳入。
- **#7739 [历史对话移至右侧]**、**#7707 [安卓换行支持]**：Web/移动端 UX 打磨需求，与已提交的 [#7741（Console 自定义主题色）](https://github.com/agentscope-ai/QwenPaw/pull/7741) 显示前端定制化是活跃方向。
- **#7702 [bot-manager 统一多渠道机器人管理插件]** [链接](https://github.com/agentscope-ai/QwenPaw/pull/7702)：覆盖微信/钉钉等多渠道统一管理，社区插件生态在扩展。

---

## 7. 用户反馈摘要

- **长期记忆不可靠是最大痛点**：#7571、#7705 均反映“反复强调的规则仍被遗忘”，说明当前记忆机制对**持久性约束规则**支持不足，用户已产生不信任感（“我不知道怎么解决了”）。
- **数据丢失零容忍**：#7724 的会话丢失直接摧毁数小时工作成果，且无恢复手段；用户此前已报告过模型配置丢失（#7708），属同类复现。
- **2.2.x 升级体验下滑**：#7716 明确指出 2.1.1b3-hub 正常而 2.2.x 回归，升级路径质量问题影响社区信心。
- **正面信号**：移动端 Web 体验被评为“已经比较好”（#7707）；报告质量普遍很高（附复现步骤、根因分析、最小修复），说明吸引到了深度技术用户。

---

## 8. 待处理积压

- **#7571**（9 天，5 评论，无官方结论）[链接](https://github.com/agentscope-ai/QwenPaw/issues/7571)：Agent 规则遗忘问题反复追问，需维护者给出明确的解决方案或 workaround。
- **#7724**（关联 #7708 长期存在的模型/会话丢失）[链接](https://github.com/agentscope-ai/QwenPaw/issues/7724)：数据可靠性问题多次复发且无修复 PR，建议系统性排查持久化层。
- **#7722 / #7727**：高严重度（OOM / 安全边界），报告质量高但尚无维护者响应痕迹，建议优先认领。
- **PR #7211**（8 月 21 日提交，ready-for-human-review，超 3 周）[链接](https://github.com/agentscope-ai/QwenPaw/pull/7211)：注入上下文持久化修复等待人工审查，存在流失风险。
- **#3429**（今日关闭）：Docker 镜像预装 CLI 工具的 5 个月老 Issue 已关闭，建议确认是已实现还是被搁置。

---

**健康度小结**：Issue→PR 闭环率良好（约 5/11 的 Bug 已有对应修复 PR），但**数据丢失、安全边界、长期记忆**三类高敏感问题缺修复方案，是下一版本发布前必须收敛的风险点。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目日报 · 2026-09-14

## 1. 今日速览
- 过去 24 小时项目整体活跃度**偏低**：仅 1 条 Issue 新开/活跃，0 条 PR 更新，0 个新版本发布。
- 唯一的活动来自外部商业团队创始人（MemCode CEO）发起的关于**持久化记忆与本地优先边界**的讨论（[#678](https://github.com/qhkm/zeptoclaw/issues/678)），属于生态合作/功能探讨信号，而非用户报障。
- 无代码合入、无版本迭代，项目处于平稳维护状态。健康度需结合后续维护者响应情况观察。

## 2. 版本发布
今日无新版本发布。（省略详情）

## 3. 项目进展
- 过去 24 小时无 PR 合并或关闭，无功能推进或修复落地。
- 项目核心能力（工具循环、记忆、channels、providers、沙箱化自主执行的单二进制 Rust 实现）保持现状，无破坏性变更。

## 4. 社区热点
- **[#678 [OPEN] Could ZeptoClaw offer durable memory without weakening its local-first boundary?](https://github.com/qhkm/zeptoclaw/issues/678)**
  - 作者：@memcodeoff（自称 MemCode 创始人兼 CEO Vivek Gupta），创建于 2026-09-13，暂无评论、无 👍。
  - 诉求分析：发帖者认可 ZeptoClaw 将工具、记忆、通道、Provider 与沙箱自主能力整合进“小型本地优先 Rust 二进制”的定位，但指出对于**长期运行的个人助手**，记忆的持久化质量与边界清晰度同样关键。问题核心是：能否在**不弱化本地优先（local-first）边界**的前提下提供持久化记忆。
  - 背景：外部记忆产品（MemCode）主动接触，可能存在集成/合作意向，值得维护者关注并明确官方立场。

## 5. Bug 与稳定性
- 今日无新增 Bug、崩溃或回归报告。无需要按严重程度排列的条目，也无待关联的 fix PR。

## 6. 功能请求与路线图信号
- **持久化记忆（durable memory）** — 来自 [#678](https://github.com/qhkm/zeptoclaw/issues/678)：
  - 关键约束：方案必须保持本地优先架构，不引入云端依赖或边界弱化。
  - 判断：目前**无相关 PR** 在推进，短期内纳入下一版本的信号不足；但该话题触及个人 AI 助手产品的核心竞争力（长期记忆），建议维护者将其纳入路线图讨论。可能的方向包括：本地向量存储、结构化记忆压缩/检索、可选的第三方记忆 Provider 接口。

## 7. 用户反馈摘要
- 样本量较小（仅 1 条），且来自潜在合作伙伴而非普通用户：
  - **正面**：ZeptoClaw 的“单二进制、本地优先、沙箱自主”的产品形态获得认可，被认为是适合长期运行的个人助手框架。
  - **痛点/期望**：当前记忆能力可能不足以支撑长期运行的助手场景，社区期望**记忆质量与工具循环同等重要**的定位被正视。

## 8. 待处理积压
- **[#678](https://github.com/qhkm/zeptoclaw/issues/678)**（2026-09-13 创建，尚无维护者回应）：涉及战略方向（记忆架构 + 可能的商业合作），建议维护者尽快回复以明确边界与意图，避免外部期待落空。
- 今日无长期未响应的 PR 积压；建议后续持续关注 Issue 响应时长指标以评估维护健康度。

---
*数据来源：ZeptoClaw GitHub 仓库（qhkm/zeptoclaw），统计窗口为过去 24 小时。*

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*