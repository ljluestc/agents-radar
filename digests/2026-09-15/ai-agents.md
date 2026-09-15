# OpenClaw 生态日报 2026-09-15

> Issues: 439 | PRs: 500 | 覆盖项目: 14 个 | 生成时间: 2026-09-15 03:57 UTC

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

# OpenClaw 项目日报 · 2026-09-15

## 1. 今日速览

- 项目整体活跃度**非常高**：过去 24 小时 Issues 更新 439 条（新开/活跃 268，关闭 171），PR 更新 500 条（待合并 292，已合并/关闭 208），关闭率约 39%/42%，消化能力健康。
- 今日**无新版本发布**，社区焦点仍集中在 **2026.9.3 / 2026.9.4 升级与恢复可靠性**上，存在专门的 P0 追踪 Issue。
- 多位核心维护者（@steipete、@vincentkoc、@sallyom）今日持续提交 PR，主攻方向为 **Gateway 性能优化（同步 I/O 异步化、减少全量 transcript 扫描）**，是一条清晰的主线工程。
- 高热议题集中在：**消息丢失/会话状态（session-state）类回归**、**Gateway 内存泄漏与事件循环阻塞**、以及 **9.x 升级失败（runtime-verification-failed）**。
- 整体判断：项目处于高频迭代期，Bug 输入量大但修复管道（clawsweeper 自动分流 + fix PR）运转顺畅，健康度**中上**，但稳定性债务在累积。

---

## 2. 版本发布

今日无新 Release。当前社区讨论基线为 **2026.9.4**（`latest` 与 `beta` 同指向），升级可靠性问题仍在协调中（见 [#145252](https://github.com/openclaw/openclaw/issues/145252)）。

---

## 3. 项目进展

今日 PR 活动呈现鲜明的 **“性能专项清理”** 特征，核心维护者集中消除 Gateway 中的同步阻塞点：

**性能/稳定性主线（@steipete、@vincentkoc 领衔）**
- [#148713](https://github.com/openclaw/openclaw/pull/148713) `fix(gateway): reduce CPU work in session lists and searches`（已关闭，L）— 会话列表/搜索不再逐行解析插件元数据。
- [#148576](https://github.com/openclaw/openclaw/pull/148576) `refactor(tasks): load fresh owner projections asynchronously`（L）— 媒体任务 owner 查询移出父线程同步 SQLite 读取，直接回应 [#119720](https://github.com/openclaw/openclaw/issues/119720) 的事件循环阻塞问题。
- [#148588](https://github.com/openclaw/openclaw/pull/148588) `fix: avoid full-transcript allocations when resetting long sessions`（XL）— 会话重置不再为 `before_reset` 观察者加载完整 transcript（上限 4096 条 / 8 MiB）。
- [#148748](https://github.com/openclaw/openclaw/pull/148748)、[#148725](https://github.com/openclaw/openclaw/pull/148725) — 会话写入与 cron/恢复检查改用窄数据库读取，避免全量 transcript 扫描。
- [#148004](https://github.com/openclaw/openclaw/pull/148004) `feat(gateway): add admin CPU profile diagnostics`（已关闭）— 管理员可免重启采集 5 秒 CPU profile，为排查 [#91588](https://github.com/openclaw/openclaw/issues/91588) 类内存/CPU问题提供工具。

**功能与修复**
- [#144811](https://github.com/openclaw/openclaw/pull/144811) `fix(update): show the actual health check failure once` — 改善升级失败的可诊断性，直接支撑 9.3/9.4 升级可靠性专项。
- [#148664](https://github.com/openclaw/openclaw/pull/148664) `fix(plugins): load selected CLI backends with built-in model APIs`（P1）— 修复 `Unknown CLI backend` 启动失败。
- [#141004](https://github.com/openclaw/openclaw/pull/141004) `feat(audit): record observed runtime skill usage`（XL）— 技能运行时使用纳入审计面，配合 [#125570](https://github.com/openclaw/openclaw/issues/125570) 的技能路由问题。
- [#148612](https://github.com/openclaw/openclaw/pull/148612) `fix(exec): node approvals no longer reject routed agent sessions`（P1）— 修复路由会话下节点审批身份不匹配。
- [#147294](https://github.com/openclaw/openclaw/pull/147294) `improve(qa): verify Slack delivery across Claude tool turns` — 为旗舰 Issue #25592 建 QA 验证基建。

**整体评估**：今日推进约 208 个 PR 合并/关闭，性能专项已形成连贯 PR 栈（#148574 → #148576 → #148583），表明 Gateway 稳定性重写正系统性落地，而非零散补丁。

---

## 4. 社区热点

| 议题 | 热度 | 链接 |
|---|---|---|
| 工具调用间文本泄漏到消息渠道 | 40 评论（最高） | [#25592](https://github.com/openclaw/openclaw/issues/25592) |
| 僵尸子进程累积致运行时劣化 | 31 评论 | [#97616](https://github.com/openclaw/openclaw/issues/97616) |
| Gateway 内存泄漏 RSS 350MB→15.5GB | 24 评论 | [#91588](https://github.com/openclaw/openclaw/issues/91588) |
| 同步持久化阻塞 Gateway 事件循环 | 20 评论 | [#119720](https://github.com/openclaw/openclaw/issues/119720) |
| 嵌入式 prompt cache 跨边界失效 | 19 评论 | [#102175](https://github.com/openclaw/openclaw/issues/102175) |

**诉求分析**：
- **#25592** 是项目标志性长跑 Issue（2 月开至今，40 条评论），用户不满 agent 的内部处理叙述文本（错误处理、中间确认）被原样发到 Slack/iMessage，属**核心 UX + 安全信任边界**问题；已有 QA 验证 PR #147294 在推进。
- **#97616 / #91588 / #119720** 三者同属**长期运行资源健康**主题——僵尸进程、内存泄漏、事件循环阻塞，均被标记 P1 但修复进展缓慢（`no-new-fix-pr`），是重度自托管用户最大的痛点。
- **#102175**（prompt cache 失效）指向**成本问题**：会话跨 room-event/policy/Responses 边界后缓存复用丢失，模型可见工具清单在 44+ 项间漂移，直接推高 token 开销。

---

## 5. Bug 与稳定性（按严重度排列）

**P0（含 ux-release-blocker）**
- [#146860](https://github.com/openclaw/openclaw/issues/146860) Windows 计划任务（InteractiveToken）下托管更新 handoff 永远拿不到进程启动身份，升级卡死为 `abandoned`。**暂无 fix PR**。
- [#123326](https://github.com/openclaw/openclaw/issues/123326) 多代理 Codex 迁移检测导致 Gateway 启动**崩溃循环**（P0，@steipete 报告）。暂无直接 fix PR。
- [#125333](https://github.com/openclaw/openclaw/issues/125333) totalTokens 膨胀在 2026.8.1-beta.2 仍复现——#123065 修复仅覆盖 `api === "cli"`，memory-flush 路径无防护。暂无新 fix PR。
- [#145072](https://github.com/openclaw/openclaw/issues/145072) ✅ 已关闭 — macOS npm 升级在 global install swap 失败（launcher 指纹含 symlink mode），已有 `queueable-fix` 标记。
- [#148614](https://github.com/openclaw/openclaw/issues/148614) / [#145510](https://github.com/openclaw/openclaw/issues/145510) 2026.9.3→9.4 升级 `runtime-verification-failed`（前者已关闭）；关联 PR #144811 改善报错可读性。

**P1 重点**
- [#144911](https://github.com/openclaw/openclaw/issues/144911) MCP server 初始化超时触发未处理 rejection **整体击穿 Gateway**（16 评论）。已标 `queueable-fix` + `source-repro`，**fix 在队列中**。
- [#139847](https://github.com/openclaw/openclaw/issues/139847) 2026.9.2 回归：reply run 活跃期间新消息被丢弃（"no active tool authority snapshot"）。`queueable-fix`，fix 在队列中。
- [#144809](https://github.com/openclaw/openclaw/issues/144809) claude-cli 长回合（超过 RUN_STALE_TAKEOVER_MS）**整段生成回复被丢弃**。仍处 needs-info。
- [#145152](https://github.com/openclaw/openclaw/issues/145152) 卡死会话恢复误报为 abort、按 session id 释放 reply lane，导致消息排队 80+ 分钟。`queueable-fix`。
- [#146004](https://github.com/openclaw/openclaw/issues/146004) 9.9.3 回归：子代理完成触发无渠道 dashboard heartbeat 回合。待 maintainer review。
- [#108395](https://github.com/openclaw/openclaw/issues/108395) 安全类：模型伪造 "Human: [timestamp]" 用户消息，可**自我授权执行高危动作**，仍未解决。

**P2 值得关注**
- [#125764](https://github.com/openclaw/openclaw/issues/125764) Telegram 出站发送网络失败**单次尝试即永久死信**，announce/完成回复静默丢失，无重试无告警。
- [#144876](https://github.com/openclaw/openclaw/issues/144876) Dashboard 工具会话在长度 finalize 失败后静默终结（HTTP 200 但无回复）。
- [#142336](https://github.com/openclaw/openclaw/issues/142336) 核心 `/dashboard` 命令与 Telegram Mini App 插件冲突，已有 linked PR。

---

## 6. 功能请求与路线图信号

- **群组 room-event steering 可配置化**（[#87584](https://github.com/openclaw/openclaw/issues/87584)，🦞 评级，source-repro）：允许将群组事件作为可注入的 steering 输入而非 followup。处于 needs-product-decision，**社区呼声高，可能进入下一版本讨论**。
- **运行时技能使用审计**（PR [#141004](https://github.com/openclaw/openclaw/pull/141004)，XL，proof sufficient）：已接近就绪，落地后为技能路由修复（#125570）提供数据基础，**大概率随下版本发布**。
- **Admin CPU profile 诊断**（PR [#148004](https://github.com/openclaw/openclaw/pull/148004)，已关闭）：运维可观测性增强，配合内存泄漏排查。
- **升级/恢复可靠性专项**（[#145252](https://github.com/openclaw/openclaw/issues/145252)，maintainer 跟踪）：明确将 update/upgrade/Doctor/rollback 可靠性列为当前发版优先事项，是短期路线图最强信号。
- **"Uncle Jim mode" 家庭代理模式**（[#77567](https://github.com/openclaw/openclaw/issues/77567)）：面向非技术家庭成员的隔离代理模式，仍停留在产品讨论阶段。
- **Bedrock per-agent 成本归因**（[#60602](https://github.com/openclaw/openclaw/issues/60602)，已关闭）：多代理成本可观测性需求反复出现，与 #102175 的缓存成本议题同属“成本透明”主题。

---

## 7. 用户反馈摘要

**主要痛点**
1. **消息丢失是最高频抱怨**：Telegram 静默丢消息（#80520、#125764）、reply run 期间新消息被丢（#139847）、长回合回复被丢（#144809）——用户反复强调“agent 明明做了工作但结果永远发不出来”的挫败感。
2. **升级即踩坑**：2026.9.3→9.4 的 `runtime-verification-failed` 在 macOS/Windows 均有报告（#148614、#145510、#145072），部分用户升级后功能大面积失效（历史上 5.12 也有类似情况 #81934），导致部分用户**对自动更新产生不信任**。
3. **长期运行劣化**：自托管 7×24 用户报告内存泄漏（#91588）、僵尸进程（#97616）、多代理冷启动 10-17s 延迟（#80607），重度用户与轻量用户体验差距明显。
4. **信任边界担忧**：中间文本泄漏到渠道（#25592）和模型伪造用户消息自我授权（#108395）让用户对把 OpenClaw 接入 Slack/iMessage 等真实社交渠道心存顾虑。

**满意点**
- clawsweeper 自动分流标签体系（severity/impact/rating/queueable-fix）获得社区认可，Bug 报告响应流程规范。
- Web Dashboard、多渠道适配（Telegram/飞书/Matrix/Slack）覆盖广，维护者对 P0 响应较快。
- 性能专项 PR 栈的系统性推进让长期性能议题看到解决希望。

---

## 8. 待处理积压（提醒维护者关注）

| Issue/PR | 状态 | 积压时长 | 风险 |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) 文本泄漏到渠道 | OPEN，needs-product-decision/security-review | **约 7 个月** | 旗舰 UX+安全问题，40 条评论 |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) Gateway 内存泄漏 | OPEN（曾 stale），needs-info | **3+ 个月** | 长期运行用户核心痛点 |
| [#102175](https://github.com/openclaw/openclaw/issues/102175) prompt cache 跨边界失效 | OPEN，needs-product-decision/security-review | 2+ 个月 | 直接影响用户 API 成本 |
| [#108395](https://github.com/openclaw/openclaw/issues/108395) 伪造用户消息自我授权 | OPEN | 2 个月 | 安全类，不应长期搁置 |
| [#125570](https://github.com/openclaw/openclaw/issues/125570) Skill Workshop 覆盖 description 致路由失效 | OPEN，needs-product-decision | ~1 个月 | 数据丢失类 |
| [#135838](https://github.com/openclaw/openclaw/pull/135838) workers 权限关闭后停止供给（P1, XL） | OPEN，needs proof | 13 天 | 兼容性+安全边界，合并风险高 |
| [#146860](https://github.com/openclaw/openclaw/issues/146860) Windows 更新 handoff 卡死 | OPEN，**无任何 clawsweeper 处理标签** | 2 天 | P0 发布阻塞项，需尽快分派 |

**建议**：优先分派 #146860 与 #123326 两个 P0 崩溃/卡死问题；对 #108395 安全 Issue 组织专项 review；性能专项 PR 栈（#148574/#148576/#148583）尽快合并以回血 #91588/#119720 的社区信心。

---
*数据来源：GitHub Issues/PR API（过去 24 小时窗口）；链接均为 openclaw/openclaw 仓库。*

---

## 横向生态对比

# 个人 AI 助手/智能体开源生态横向对比分析报告

**数据日期：2026-09-15**

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态已从早期的“概念验证”全面进入**工程化攻坚期**：各项目的竞争焦点不再是模型接入和对话能力，而是长期运行稳定性（内存泄漏、事件循环阻塞、僵尸进程）、消息投递可靠性、多渠道适配（Telegram/Slack/飞书/Matrix）和信任边界安全（审批旁路、信息泄漏）。生态呈现明显的**分层格局**——OpenClaw 以量级最大的 Issue/PR 吞吐（939 条/日）构成事实上的生态核心，多个下游项目（LobsterAI、NanoClaw）直接依赖其运行时；中型项目（NanoClaw、Hermes、Zeroclaw、CoPaw）各自在安全架构、语音、记忆系统上形成差异化深耕；小型项目则处于功能讨论或维护期。值得注意的是，**“Claw 系”命名家族高度密集**，且多个项目共享 clawsweeper 分流、Track/PR 栈等工程实践，暗示生态内部存在方法论扩散。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新(24h) | PR 更新(24h) | Release | 健康度 | 阶段判断 |
|---|---|---|---|---|---|
| **OpenClaw** | 439（关 171） | 500（合并/关 208） | 无 | 中上 | 高频迭代 + 性能专项，稳定性债务累积 |
| **NanoClaw** | 6 | 50（38 关/合并） | 无 | 良好 | 快速迭代，修复闭环极快 |
| **Hermes Agent** | 50（关 4） | 50（关 4） | **v0.21.3** | 良好 | 打磨期，338 PR 打 tag，P1 积压 |
| **Zeroclaw** | 22（开合 1:1） | 50（关 11） | 无 | 良好 | 安全架构大改造 + 质量收尾双轨 |
| **CoPaw** | 44（关 18，41%） | 50（关 11） | 无 | 中上 | 功能堆叠期，3 个高危 Issue 无 fix |
| **NanoBot** | 6（关 1） | 25（关 13） | 无 | 良好 | 质量打磨期，问题-修复当日闭环 |
| **LobsterAI** | 1 | 25 | 无 | 中 | 依赖维护期，核心升级（OpenClaw 8.1 + Electron 43）刚落地 |
| **PicoClaw** | 1 | 3 | 无 | 中 | v0.10.0 sprint 75%，社区响应滞后 |
| **NullClaw** | 4（关 0） | 0 | 无 | 偏低 | 需求讨论期，供给侧静默 |
| **IronClaw** | 1 | 1 | 无 | 平稳 | 例行维护（评测基础设施） |
| **ZeptoClaw** | 1（关 1） | 1（关 1） | 无 | 平稳 | CI 治理收尾 |
| **Moltis** | 0 | 1 | 无 | 平稳 | 维护期，仅测试竞态修复 |
| **TinyClaw / EasyClaw** | 0 | 0 | 无 | — | 静默 |

**关键观察**：只有 Hermes 发布了版本；生态整体呈现“PR 活跃 > Issue 消化”的普遍模式，反映各家都在为下一个版本蓄力。

---

## 3. OpenClaw 在生态中的定位

**规模对比**：OpenClaw 单日 Issue/PR 活动量（939 条）是第二梯队项目（50 条级别）的 **10-18 倍**，且拥有核心维护者团队（@steipete、@vincentkoc、@sallyom）全职节奏推进。LobsterAI 直接将其作为内置运行时升级至 v2026.8.1，NanoClaw、NullClaw 的 provider/CLI 架构（`claude-cli`/`codex-cli` 模式）也与之同构——OpenClaw 已是生态的**上游基座与事实标准**。

**优势**：
- 工程化程度最高：clawsweeper 自动分流、PR 栈式推进（#148574→576→583）、admin CPU profile 等诊断工具链完整；
- 渠道覆盖最广（Telegram/飞书/Matrix/Slack/iMessage）；
- 治理规范（severity/impact/queueable-fix 标签体系）被社区认可。

**技术路线差异**：OpenClaw 主线是 **Gateway 中心化架构 + 性能专项治理**（同步 I/O 异步化、窄 DB 读取）；相比之下 Zeroclaw 走 Rust 安全工程路线（OIDC/PKCE/shell 权限策略），Hermes 押注 A2A 与本地推理（managed llama-server），PicoClaw 主打 libp2p mesh 边缘部署。

**风险**：旗舰问题积压严重——#25592（文本泄漏，7 个月）、#108395（安全自我授权，2 个月）、#91588（内存泄漏）等长期未决，稳定性债务与其生态核心地位形成张力，下游（如 LobsterAI）升级即被动继承其回归。

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **消息投递可靠性/静默丢失** | OpenClaw（#80520/#125764/#139847）、LobsterAI（#1035）、CoPaw（#7709）、Hermes（#110889）、PicoClaw（#3365） | 生态最高频痛点：agent 完成工作但结果永远发不出；单次尝试即死信、去重缓存误判、投递无重试无告警 |
| **提示词缓存失效与成本** | OpenClaw（#102175，44+ 工具清单漂移）、Zeroclaw（#10858，午夜 DateTimeSection 使缓存前缀失效）、Hermes（#110912 计费 11-13x） | 自托管/重度用户对 token 成本不可预测高度敏感，缓存前缀稳定性已成一等工程问题 |
| **长期运行资源健康** | OpenClaw（#91588 内存 350MB→15.5GB、#97616 僵尸进程）、CoPaw（#7722 内存 20GB+）、NanoClaw（#3811 SQLite busy_timeout） | 7×24 自托管场景的内存泄漏、子进程回收、DB 并发是共性工程债 |
| **安全信任边界** | OpenClaw（#108395 伪造用户消息、#25592）、Hermes（#59293 config set 绕过审批）、NanoClaw（#3814 错误文本泄漏至公共频道）、Zeroclaw（#8289 系列、#6613 配对码） | 从“能否拦住”进化到“审批层不可旁路 + 内部叙述不出渠道” |
| **多渠道/跨端会话互通** | Hermes（#41220/#76767）、Zeroclaw（#9772）、CoPaw（#7746 skill 按渠道）、PicoClaw（QQ 频道） | Telegram/Desktop/CLI 间会话可移植、按渠道隔离是核心 UX 诉求 |
| **供应商/搜索端点可配置化** | NullClaw（#993 Firecrawl 端点、#975 grok-cli）、NanoBot（#5666/#4919）、PicoClaw（#3370 Keenable 免密钥） | 自托管 + 成本敏感用户要求摆脱 SaaS 锁定，CLI 登录态接入规避 API 计费 |
| **A2A 多智能体协作** | Hermes（#38275/#38280/#95981）、NanoClaw（#3813 durable handoff、#3719） | agent 间通信可审计、可恢复，Agent 经济层（钱包/信誉）开始进入讨论 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 全渠道个人助手 + 多代理 Gateway | 重度自托管用户/开发者 | 中心化 Gateway，Node/TS，插件生态 |
| **Hermes Agent** | 语音、本地推理、A2A、Bot Mode 生态 | 极客/本地优先用户 | managed llama-server、Footprint Ladder 治理、Nous Portal 商业化 |
| **Zeroclaw** | 安全工程 + 桌面端 + 通道质量 | 安全敏感自托管者 | Rust、九级安全 PR 栈（OIDC/PKCE/shell 权限）、RFC 治理 |
| **NanoClaw** | 渠道 + provider 快速扩展 | Slack/WhatsApp 团队场景 | Docker 化、模板化子 agent、供应链门控（minimumReleaseAge） |
| **NanoBot** | 记忆系统（Dream）+ cron + WebUI | 轻量个人用户 | 学术背景（HKUDS），质量打磨节奏 |
| **CoPaw** | Hub 多租户 + 记忆 + 定时任务 | 团队/组织协作平台 | 组织 token 预算、ACP 协议、上下文压缩 |
| **LobsterAI** | 桌面端体验（Electron） | 网易有道系桌面用户 | 套壳 OpenClaw 运行时 + POPO IM |
| **PicoClaw** | mesh 网络 + 边缘部署 | 家庭实验室/ARM 板用户 | Go + libp2p，低功耗设备 |
| **NullClaw** | 轻量搜索/provider | 极简用户 | Zig 实现 |
| **IronClaw** | agent 评测基础设施 | Near AI 生态开发者 | 失败分类日报、基准驱动 |

---

## 6. 社区热度与成熟度分层

**第一梯队（规模化迭代）**：OpenClaw——唯一具备“平台级”社区体量，但已进入稳定性债务偿还期。

**第二梯队（快速迭代，各有主线）**：
- **Hermes**：发布节奏最规范（338 PR → v0.21.3），RFC 驱动，风险在安全/计费响应速度；
- **NanoClaw**：代码吞吐/合并比最高（38/50），OpenCode provider 集成在途；
- **Zeroclaw**：开合比 1:1 处理效率最优，但 39 个待合并 PR 中 XL 级安全 PR 排队，审查带宽是瓶颈；
- **CoPaw**：Issue 关闭率 41%，维护力量充足，但内存泄漏/停止失效/subAgent 超时三个高危无 fix。

**第三梯队（质量巩固期）**：NanoBot（问题-修复当日闭环，成熟度稳步提升）、LobsterAI（核心升级落地但依赖 PR 积压、社区响应迟缓）。

**第四梯队（维护/讨论期）**：PicoClaw（sprint 有序但社区面 stale）、NullClaw（零 PR 产出）、IronClaw、ZeptoClaw、Moltis、TinyClaw、EasyClaw。

**共性风险**：几乎所有活跃项目都存在“**高危 Issue 无 fix PR**”的缺口（OpenClaw 2 个 P0、CoPaw 3 个高危、Hermes 3 个 P1），说明各团队修复带宽普遍落后于 Bug 输入。

---

## 7. 值得关注的趋势信号

1. **“做了工作但发不出去”是生态第一信任杀手**。消息静默丢失在 6+ 项目反复出现，投递层的重试/死信告警/幂等设计将成为智能体基础设施的标配需求——对开发者：优先建设投递可观测性，而非仅优化 agent 能力。

2. **提示词缓存稳定性 = 成本竞争力**。OpenClaw 的工具清单漂移、Zeroclaw 的午夜缓存前缀失效表明：系统提示中任何动态内容都会摧毁缓存经济性。设计原则——**将时间戳等易变信息移出缓存前缀，冻结工具清单**。

3. **安全从“沙箱”转向“审批层不可旁路 + 信息不出界”**。Hermes 的 config set 旁路、OpenClaw 的模型自我授权、NanoClaw 的错误文本外泄共同指向：智能体的安全边界必须在**所有写入路径和出站通道**上强制执行，CLI/UI/API 前门一致。

4. **CLI 登录态 provider 成为规避 API 计费的普遍模式**（claude-cli/codex-cli/grok-cli/OpenCode，覆盖 NullClaw/NanoClaw/Zeroclaw/Hermes 四个项目）——订阅制套利已是社区明确偏好，但也带来账号标记与合规风险。

5. **自托管 + 隐私取向用户群固化**：XMPP 请求（Zeroclaw）、Firecrawl 端点可配置（NullClaw）、ARM 板部署（PicoClaw）、企业推理 failover（NanoBot NIM）——端点可配置化和低资源适配是真实需求而非边缘诉求。

6. **A2A 与多智能体经济层从讨论走向 PR**：Hermes 的地址系统/钱包信誉、NanoClaw 的 durable handoff 账本，表明 agent 间通信的可审计性是下一个工程前沿。

7. **治理自动化成为中型项目竞争力**：clawsweeper（OpenClaw）、Footprint Ladder（Hermes）、RFC 快速通道（Zeroclaw）——自动化分流与审查流程直接决定项目能否承载高贡献量，值得早期项目借鉴。

8. **对 OpenClaw 的依赖形成单点风险**：LobsterAI 直接内嵌其运行时，下游升级即被动继承上游回归（9.3→9.4 `runtime-verification-failed` 已波及多平台）。下游项目应建立上游版本 pin + 回归验证门控。

---

**总结**：生态整体健康、方向收敛——竞争已从“能跑起来”转向“7×24 跑得稳、发得出、花得省、拦得住”。OpenClaw 体量领先但债务显现，Zeroclaw/Hermes/NanoClaw 在安全/语音/渠道上的深耕构成最有力挑战；对开发者而言，**投递可靠性、缓存经济性、审批层完整性**是当前最具杠杆的三项工程投入。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-09-15

## 1. 今日速览

NanoBot 今日保持高活跃度：过去 24 小时内 Issues 更新 6 条（新开 5 条、关闭 1 条），PR 更新 25 条（待合并 12 条、已合并/关闭 13 条），无新版本发布。社区贡献呈现明显的“修复驱动”特征，@FanouZeng-TT 单日连开 5 个高质量 bug fix PR（cron/API/provider），外部贡献者 @morandot 集中报告了 4 个 WebUI 移动端/PWA 体验问题。整体来看，项目处于功能稳定后的质量打磨期，维护者响应及时、PR 合并节奏健康。

## 2. 版本发布

今日无新版本发布。上一版本为 v0.3.0（从 [PR #5768](https://github.com/HKUDS/nanobot/pull/5768) 描述中提及）。当前积累的已合并修复（cron 稳定性、memory 修复、性能优化）或将在下个版本集中释放。

## 3. 项目进展

今日已合并/关闭 13 个 PR，重点推进：

- **Memory/Agent 稳定性**：[PR #5774](https://github.com/HKUDS/nanobot/pull/5774)（archive 工具调用恢复 + RAW 回退保留）、[PR #5734](https://github.com/HKUDS/nanobot/pull/5734)（明确 Dream prompt 的记忆写入权限边界）、[PR #5730](https://github.com/HKUDS/nanobot/pull/5730)（内部模型调用改用流式 + 空闲超时，修复 Dream 长任务反复超时）。
- **Cron/自动化子系统修复三连**：[PR #5686](https://github.com/HKUDS/nanobot/pull/5686)（任务执行期间延迟重新武装定时器，修复 CancelledError）、[PR #5751](https://github.com/HKUDS/nanobot/pull/5751)（编辑自动化详情时保留待执行任务）、[PR #5762](https://github.com/HKUDS/nanobot/pull/5762)（拒绝过去时间点的一次性调度）——cron 子系统历经一轮系统性加固。
- **性能**：[PR #5728](https://github.com/HKUDS/nanobot/pull/5728) 大幅降低长流式回复的标签扫描与 CLI 重绘开销，本地 CPU 成本不再随回复长度线性增长。
- **工具回归修复**：[PR #5761](https://github.com/HKUDS/nanobot/pull/5761) 修复 `edit_file` 吞换行符导致相邻行合并的数据损坏问题，并统一与 `apply_patch` 的成功摘要与 WebUI diff。
- **文档**：[PR #5684](https://github.com/HKUDS/nanobot/pull/5684) 刷新 README，加入当前 WebUI 功能图集。

**评估**：今日合并集中在记忆系统、定时任务和流式性能三大核心模块，属于深度质量提升，项目整体成熟度显著前进。

## 4. 社区热点

- [Issue #2804](https://github.com/HKUDS/nanobot/issues/2804)（DuckDuckGo web_search 无限挂起阻塞会话）— 评论 4 条，为今日讨论最多的 Issue，今日关闭，说明该长期阻塞问题已解决。
- [Issue #5674](https://github.com/HKUDS/nanobot/issues/5674)（NVIDIA NIM 超时错误导致 agent 停摆）— 已有对应修复 [PR #5769](https://github.com/HKUDS/nanobot/pull/5769) 提交，问题-修复闭环形成，社区协作高效。
- [PR #5666](https://github.com/HKUDS/nanobot/pull/5666)（aimlapi.com 作为内置 provider）— 第三方商业方主动提交并附带合作条件（50/50 分成），持续活跃至今，等待维护者商务/技术决策。

## 5. Bug 与稳定性（按严重程度）

| 严重度 | 问题 | 状态 |
|---|---|---|
| 🔴 高 | [#5674](https://github.com/HKUDS/nanobot/issues/5674) NIM 超时错误被误认为模型输出，agent 永久停止工作 | 有 fix PR [#5769](https://github.com/HKUDS/nanobot/pull/5769) 待合并 |
| 🔴 高 | [#2804](https://github.com/HKUDS/nanobot/issues/2804) DuckDuckGo 搜索挂起阻塞整个会话 | 已关闭（已修复） |
| 🟠 中 | [#5773](https://github.com/HKUDS/nanobot/issues/5773) PWA 冷启动长时间白屏 | 新开，待响应 |
| 🟠 中 | [#5772](https://github.com/HKUDS/nanobot/issues/5772) iOS PWA standalone 模式顶部渲染半透明/模糊 | 新开，待响应 |
| 🟡 低 | [#5771](https://github.com/HKUDS/nanobot/issues/5771) 移动端会话列表需点击两次才能打开 | 新开，待响应 |
| 🟡 低 | [#5770](https://github.com/HKUDS/nanobot/issues/5770) 移动端打开侧栏误触发 "Search ⌘K" tooltip | 新开，待响应 |
| 🟠 中 | 飞书 QR 登录必然失败（"Link expired"）[PR #5768](https://github.com/HKUDS/nanobot/pull/5768)，标记 p1 | fix PR 待合并 |
| 🟠 中 | FallbackProvider 半开探测并发竞争 [PR #5764](https://github.com/HKUDS/nanobot/pull/5764) | fix PR 待合并 |

## 6. 功能请求与路线图信号

- **新 Provider**：aimlapi.com 内置支持（[PR #5666](https://github.com/HKUDS/nanobot/pull/5666)）——涉及商业合作，需维护者决策；NIM 超时 failover（[#5769](https://github.com/HKUDS/nanobot/pull/5769)）大概率进入下版本。
- **Telegram 自定义 Bot API 地址**（[PR #4919](https://github.com/HKUDS/nanobot/pull/4919)，7 月提交今日仍有活动）——面向自托管/企业网关场景，长期未合并，建议关注冲突状态。
- **工具上下文 API**：[PR #5750](https://github.com/HKUDS/nanobot/pull/5750) 暴露稳定的每次调用 ToolInvocationContext，是工具生态扩展的基础设施，可能进入下版本。
- **WebUI 国际化**：波兰语本地化（[PR #5767](https://github.com/HKUDS/nanobot/pull/5767)，覆盖 1536+497 条消息）显示 i18n 社区贡献 pipeline 成熟。

## 7. 用户反馈摘要

- **痛点集中在企业级 provider 与可靠性**：NVIDIA NIM 用户报告超时后 agent 静默死亡（[#5674](https://github.com/HKUDS/nanobot/issues/5674)），反映自托管/企业推理场景用户对 failover 韧性的强烈需求。
- **移动端 WebUI 体验欠佳**：@morandot 一人集中报告 4 个 iOS PWA 问题（白屏、渲染异常、双击、误触发 tooltip），使用场景为 iPhone 主屏图标启动 PWA 日常使用，说明移动端用户基数存在但体验未跟上。
- **数据完整性敏感**：`edit_file` 吞换行符（[#5761](https://github.com/HKUDS/nanobot/pull/5761)）被标记为 regression 并快速修复，用户对 agent 改写文件内容的可靠性高度关注。
- **飞书企业用户受阻**：QR 登录在 v0.3.0 上完全不可用（[#5768](https://github.com/HKUDS/nanobot/pull/5768)），是渠道接入的实际阻断项。

## 8. 待处理积压

- [PR #4919](https://github.com/HKUDS/nanobot/pull/4919)（Telegram 自定义 API base）：7 月 14 日提交，开放两个月未合并，建议维护者给出决策或反馈。
- [PR #5666](https://github.com/HKUDS/nanobot/pull/5666)（aimlapi provider）：9 月 4 日提交，含商业合作诉求，需明确技术/商务边界。
- [PR #5601](https://github.com/HKUDS/nanobot/pull/5601)（WebUI 拒绝消息回滚）：8 月 29 日提交，已标 conflict，需 rebase 后推进。
- [Issue #5674](https://github.com/HKUDS/nanobot/issues/5674)：影响可用性的高严重度问题，fix PR [#5769](https://github.com/HKUDS/nanobot/pull/5769) 待审，建议优先合并。

---
**健康度总评**：✅ 良好。问题-修复闭环效率高（多个 Issue 当日即有对应 PR），外部贡献者活跃且 PR 质量高；短板在于移动端 WebUI 体验和少量长期积压 PR 需维护者加快裁决。

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报（2026-09-15）

---

## 1. 今日速览

过去 24 小时 Zeroclaw 保持了高度活跃的开发节奏：Issues 更新 22 条（新开/活跃 11、关闭 11，开合比 1:1，处理效率优秀），PR 更新 50 条（待合并 39、已合并/关闭 11）。今日无新版本发布，项目仍处于 v0.8.5 稳定化周期后的持续修复与功能堆叠阶段。值得注意的是，今日新报了 **3 个 P1 级高危 Bug**（#10863、#10858、#10857），集中在 Telegram 通道、系统提示缓存与多模态能力探测三个方向。安全相关的多阶段大型 PR（#8289 系列）持续推进，是当前最核心的工程主线。

---

## 2. 版本发布

今日无新版本发布。（v0.8.5 周度稳定化跟踪仍在 [#9459](https://github.com/zeroclaw-labs/zeroclaw/issues/9459) 进行中，8 月 30 日线已过，处于按周切出就绪工作的模式。）

---

## 3. 项目进展

今日合并/关闭 11 个 PR，代表性进展如下：

- **多模态图像验证落地推进**：[#9819](https://github.com/zeroclaw-labs/zeroclaw/pull/9819)（像素级图像校验，防止损坏图片导致 provider 请求失败）持续活跃，配合今日新开的 #10854/#10857 修复，多模态链路正在系统性加固。
- **OpenCode 会话头修复闭环**：#10603（S1 级 Bug）已关闭，配套的后续任务 [#10853](https://github.com/zeroclaw-labs/zeroclaw/issues/10853) 与修复 PR [#10864](https://github.com/zeroclaw-labs/zeroclaw/pull/10864) 今日快速跟进，修复了 pinned header 非法值导致亲和头完全丢失的问题。
- **桌面端守护进程日志治理**：[#10236](https://github.com/zeroclaw-labs/zeroclaw/pull/10236)（有界 daemon 捕获日志）活跃更新，改善桌面版可观测性与升级重启安全。
- **通道能力补齐**：Mattermost 审批提示 [#10358](https://github.com/zeroclaw-labs/zeroclaw/pull/10358)、Telegram 群组按用户分会话 [#9772](https://github.com/zeroclaw-labs/zeroclaw/pull/9772) 持续推进。
- **CI 效率**：[#10607](https://github.com/zeroclaw-labs/zeroclaw/pull/10607) 将 fork PR 也路由至 Blacksmith 并精简 PR 门禁，降低外部贡献门槛。

整体看，项目正处于“安全架构大改造（#8289 九级堆叠 PR）+ 通道/多模态质量收尾”双轨推进阶段，向下一个 minor 版本稳定迈进。

---

## 4. 社区热点

- **[#10549](https://github.com/zeroclaw-labs/zeroclaw/issues/10549)（10 评论，最活跃）**：RFC 提议取消 RFC 强制讨论窗口、REVISE 即冻结当前快照。反映核心团队在治理流程上持续“降摩擦”，已被接受且开发中。
- **[#10366](https://github.com/zeroclaw-labs/zeroclaw/issues/10366)（8 评论）**：RFC 澄清 PR 审查证据、新鲜度警告与作者行为边界，新增快速合并通道。与 #10304（审查政策文档生成）联动，说明审查流程自动化是当前治理焦点。
- **[#10603](https://github.com/zeroclaw-labs/zeroclaw/issues/10603)（3 👍）**：OpenCode 亲和头缺失导致 Go 模型不可用、账号有被标记风险——用户共鸣最强的 Bug，今日已修复关闭。
- **[#9814](https://github.com/zeroclaw-labs/zeroclaw/issues/9814)**：社区请求原生 XMPP/Prosody 通道，面向家庭实验室和低资源自托管场景，已接受待实现。

---

## 5. Bug 与稳定性（按严重度）

**S1 / P1（工作流阻断）**
| Issue | 问题 | 修复状态 |
|---|---|---|
| [#10863](https://github.com/zeroclaw-labs/zeroclaw/issues/10863) | Telegram 被拒语音更新无限重试，阻塞后续消息（生产事故，来自 PR #10640） | 已接受，暂无 fix PR |
| [#10858](https://github.com/zeroclaw-labs/zeroclaw/issues/10858) | 系统提示中 `DateTimeSection` 每日午夜使所有会话的缓存前缀失效（成本影响大） | in-progress |
| [#10857](https://github.com/zeroclaw-labs/zeroclaw/issues/10857) | ZeroCode 向无视觉能力模型附加图片，provider 返回 400 | 已接受，暂无 fix PR |
| [#10854](https://github.com/zeroclaw-labs/zeroclaw/issues/10854) | 工具输出中的字面 `[IMAGE:...]` 标记被提升为畸形 provider 图片 | in-progress |

**P2（降级行为）**
- [#10625](https://github.com/zeroclaw-labs/zeroclaw/issues/10625)：非视觉模型下用户收到字面 `[media attachment]` 占位符（与 #10857 同根因，多模态降级路径需统一治理）。
- [#10842](https://github.com/zeroclaw-labs/zeroclaw/issues/10842)：Telegram reaction 工具静默 no-op（trait 默认实现返回 Ok(())），in-progress。
- [#10585](https://github.com/zeroclaw-labs/zeroclaw/issues/10585)（已关闭）：新日志 sink 与迁移测试在默认并行运行器下竞态。
- [#10794](https://github.com/zeroclaw-labs/zeroclaw/issues/10794)（已关闭）：Advisory Windows nextest 发布契约测试失败。

**P3（轻微）**
- [#10796](https://github.com/zeroclaw-labs/zeroclaw/issues/10796)（已关闭）：ZeroCode 聊天输入框 Delete 键无效——good first issue，已快速解决。

---

## 6. 功能请求与路线图信号

- **安全主线（最可能进入下个大版本）**：#8289 多阶段工程——RPC 认证主体（[#10259](https://github.com/zeroclaw-labs/zeroclaw/pull/10259)）、OIDC token 验证（[#10255](https://github.com/zeroclaw-labs/zeroclaw/pull/10255)）、浏览器 PKCE 与跨表面注册（[#10321](https://github.com/zeroclaw-labs/zeroclaw/pull/10321)）；以及 shell V1 权限策略（[#10610](https://github.com/zeroclaw-labs/zeroclaw/pull/10610)，RFC #7155）。
- **强配对码**：[#6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613)（6 位数字配对码过弱，默认改 32 字符）今日关闭，安全加固已落地。
- **已接受待实现**：原生 XMPP 通道（[#9814](https://github.com/zeroclaw-labs/zeroclaw/issues/9814)）——home-lab 社区诉求明确，尚无 PR。
- **被关闭的提案**：AnySearch 作为内置 web_search_tool provider（[#10336](https://github.com/zeroclaw-labs/zeroclaw/issues/10336)）未获纳入。
- **配置体验**：多模型共享 provider profile（[#9809](https://github.com/zeroclaw-labs/zeroclaw/pull/9809)）、多模态默认上限提升至 20MB（#10588，已关闭）。

---

## 7. 用户反馈摘要

- **真实生产事故驱动修复**：Telegram 语音消息无限重试（#10863）来自 RO-mix 的生产报告，说明已有相当规模的真实部署，长轮询可靠性是运营方核心痛点。
- **成本敏感**：#10858（午夜缓存前缀失效）直接关系 API 成本——提示缓存失效意味着每晚会重新计费全部前缀 token，自托管/重度用户会明显感知。
- **自托管与隐私取向明显**：XMPP/Prosody 请求（#9814）、OpenCode 中继兼容性（#10603，用户担心账号被标记）表明用户群大量使用非官方中继与自建基础设施。
- **安全意识强**：用户主动要求加强配对码强度（#6613）、关注浏览器自动化默认开启的风险（#9830 将全量浏览器自动化改为 opt-in 即是对此的回应）。
- **新手体验**：ZeroCode TUI 的 Delete 键（#10796）、启动诊断本地化（#10789）等小问题被快速处理，good-first-issue 流转健康。

---

## 8. 待处理积压

- **需维护者审查**：[#10236](https://github.com/zeroclaw-labs/zeroclaw/pull/10236)（桌面 daemon 日志，8-21 开启）、[#9638](https://github.com/zeroclaw-labs/zeroclaw/pull/9638)（ACP 默认 agent 选择，8-01 开启）、[#10621](https://github.com/zeroclaw-labs/zeroclaw/pull/10621)（agent 生命周期协调，XL 体量）均挂 `needs-maintainer-review`，审查带宽是当前瓶颈。
- **需作者行动**：[#9713](https://github.com/zeroclaw-labs/zeroclaw/pull/9713)、[#9809](https://github.com/zeroclaw-labs/zeroclaw/pull/9809)、[#9819](https://github.com/zeroclaw-labs/zeroclaw/pull/9819)、[#9971](https://github.com/zeroclaw-labs/zeroclaw/pull/9971)、[#10610](https://github.com/zeroclaw-labs/zeroclaw/pull/10610)。
- **新 P1 尚无 fix PR**：#10863、#10857 建议尽快指派或开跟踪 PR，避免生产用户持续受阻。
- **长期 RFC**：#10549、#10366 均已接受并 in-progress，属主动推进而非积压。

**健康度小结**：开合比 1:1、P1 响应当日跟进、good-first-issue 流转迅速，项目处于健康的高活跃状态；主要风险在于 39 个待合并 PR 中多个 XL 体量安全 PR 的审查排队。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-09-15

---

## 1. 今日速览

今日 Hermes Agent 维持高活跃度：过去 24 小时内 Issues 更新 50 条（新开/活跃 46，关闭 4），PR 更新 50 条（待合并 46，合并/关闭 4），另有 1 个新版本 v0.21.3 发布。社区讨论焦点集中在实时语音接口标准化（RFC #77111）、安全旁路问题（#59293）以及 Nous Portal 计费异常（#110912）。PR 队列以大量 P2 级修复为主，多数由 @teknium1 集中提交，呈现出“批量 salvage + 修复”的工程节奏。整体健康度良好，但 P1 级会话状态（session-state）类 Bug 仍在积压。

---

## 2. 版本发布

### v2026.9.14: Hermes Agent v0.21.3 ([Release](https://github.com/NousResearch/hermes-agent/releases))

- **性质**：Patch 版本，将 v0.21.2 以来合并的约 **338 个 PR** 打成稳定 tag，供下游消费者（Docker 镜像、Hermes Cloud、托管部署）使用。
- **核心动机**：固化 remote-gateway 登录修复。
- **破坏性变更**：Release 说明中未明确标注，属 patch 级，预计无 API 破坏性变更；建议下游部署在升级后验证 remote-gateway 登录链路。

---

## 3. 项目进展

今日合并/关闭数量较少（4 条），但待合并 PR 队列质量高，覆盖多个关键面：

**修复类（多为待合并）**
- **测试安全**：[#111449](https://github.com/NousResearch/hermes-agent/pull/111449) — pytest basetemp 位于 Hermes home 内时不再将测试沙箱变成真实安装，防止测试覆盖真实 `config.yaml`/`.env`。
- **本地推理**：[#111337](https://github.com/NousResearch/hermes-agent/pull/111337)、[#111372](https://github.com/NousResearch/hermes-agent/pull/111372) — 修复 managed llama-server 在 llama.cpp b10964 上的启动失败（`--no-webui` → `--no-ui`，`-dio` → `--load-mode dio`）。
- **认证链路**：[#111442](https://github.com/NousResearch/hermes-agent/pull/111442)（auxiliary ladder 刷新失败后落入 fallback_chain）、[#111451](https://github.com/NousResearch/hermes-agent/pull/111451)（免费 OpenCode 模型 401 死循环）。
- **安全**：[#111450](https://github.com/NousResearch/hermes-agent/pull/111450) — 符号链接父路径下（macOS /tmp、/var）的 HERMES_HOME 正确收紧为 0700。
- **Codex/Responses**：[#111443](https://github.com/NousResearch/hermes-agent/pull/111443)（跨 turn 重复 tool call_id 导致 400）、[#89942](https://github.com/NousResearch/hermes-agent/pull/89942)（app-server 子进程回收）。
- **多 profile 日志隔离**：[#111448](https://github.com/NousResearch/hermes-agent/pull/111448)；**更新器**：[#111445](https://github.com/NousResearch/hermes-agent/pull/111445)。

**功能类**
- **插件目录分货架**：[#111415](https://github.com/NousResearch/hermes-agent/pull/111415) — Plugin Catalog 按 Memory/Desktop/Platforms 等分类陈列。
- **模型白名单选择器**：[#111543](https://github.com/NousResearch/hermes-agent/pull/111543) — 全端（Desktop/TUI/CLI/gateway/dashboard/ACP）支持 allowed model picker。
- **社区插件**：[#111525](https://github.com/NousResearch/hermes-agent/pull/111525)（grill-tab）。

**推进评估**：PR 队列显示项目正处于“打磨期”——大量 P2 修复集中在安装更新、认证、多 profile 隔离与本地推理兼容性，为下一次 minor 版本蓄力。

---

## 4. 社区热点

1. **[#77111](https://github.com/NousResearch/hermes-agent/issues/77111) — RealtimeVoiceProvider ABC RFC（26 评论）**
   四个竞争的双工语音 PR 触发了 AGENTS.md 的 "Footprint Ladder" 规则（3+ 同类 PR 应设计抽象接口而非排队合并）。社区在激烈讨论 TTS/语音 provider 的统一接口设计，这是当前讨论量最高的议题，将直接决定语音栈的架构走向。

2. **[#59293](https://github.com/NousResearch/hermes-agent/issues/59293) — `hermes config set` 绕过系统配置写保护（8 评论，P2 安全）**
   CLI 前门修改 `config.yaml` 不触发危险标志，有终端访问权的 agent turn 可借此**关闭审批层**。安全边界类问题，社区关注度持续。

3. **[#103483](https://github.com/NousResearch/hermes-agent/issues/103483) — Muse Spark 流中途以无关单词截断（7 评论，7 👍）**
   Responses wire 上 `finish_reason=stop` 异常截断，直接影响使用体验，用户共鸣度高。

4. **[#110912](https://github.com/NousResearch/hermes-agent/issues/110912) — Nous Portal deepseek-v4-flash 订阅额度耗尽后计价 ~11-13x（6 评论）**
   计费/商业信任类问题，用户实际付费受损，需官方优先响应。

5. **[#41220](https://github.com/NousResearch/hermes-agent/issues/41220) / [#76767](https://github.com/NousResearch/hermes-agent/issues/76767) — 跨 surface 会话互通（6/5 评论）**
   核心诉求：用户希望 Telegram / Desktop / CLI 之间无缝接续会话（`/resume` 跨来源可见、跨端消息投递不丢失）。

---

## 5. Bug 与稳定性（按严重程度）

### P1
| Issue | 问题 | Fix 状态 |
|---|---|---|
| [#94811](https://github.com/NousResearch/hermes-agent/issues/94811) | Desktop 双连接共享 profile 名时 session RPC 塌缩到主连接（4001） | 未见 fix PR |
| [#76767](https://github.com/NousResearch/hermes-agent/issues/76767) | Desktop 查看 Telegram 会话时回复不投递回 Telegram | 未见 fix PR |
| [#110422](https://github.com/NousResearch/hermes-agent/issues/110422) | 生命周期守卫未对 referenced-script walk 应用 heredoc 掩码 | 未见 fix PR |

### P2
- **[#110912](https://github.com/NousResearch/hermes-research/hermes-agent/issues/110912)** — Portal 计费异常（见热点）。
- **[#103483](https://github.com/NousResearch/hermes-agent/issues/103483)** — Muse Spark 流截断。
- **[#110889](https://github.com/NousResearch/hermes-agent/issues/110889)** — Bot Mode 投递 turn 中用户回复被吞。
- **[#55112](https://github.com/NousResearch/hermes-agent/issues/55112)** — zai vision 硬编码 metered 端点导致静默计费。
- **[#107224](https://github.com/NousResearch/hermes-agent/issues/107224) — `respawn-argv` 重启机制未实现，无 systemd unit 的 serve 永久重挂 restart pending。

### P3 / 已修复
- [#111299](https://github.com/NousResearch/hermes-agent/issues/111299)（macOS 原生测试失败）→ **已有 fix PR [#111450](https://github.com/NousResearch/hermes-agent/pull/111450)**。
- [#109982](https://github.com/NousResearch/hermes-agent/issues/109982)（Windows wake word 崩溃整个 gateway，sentencepiece 0xC0000005）— **已关闭**。
- [#111509](https://github.com/NousResearch/hermes-agent/issues/111509)（desktop gh auth 超时孤儿进程）、[#111497](https://github.com/NousResearch/hermes-agent/issues/111497)（更新回执缺失 SQLite 修复结果）— 新报，待响应。

---

## 6. 功能请求与路线图信号

- **语音统一接口**：[#77111](https://github.com/NousResearch/hermes-agent/issues/77111) RFC 一旦定稿，预计很快落地 ABC + orchestrator——高优先路线图信号。
- **跨 surface 会话互通**：#41220 + #76767 + #94811 共同指向“会话可移植性”主题，多个 sweeper:risk-session-state 标签表明维护者已在系统性梳理。
- **A2A 生态深化**：[#38275](https://github.com/NousResearch/hermes-agent/issues/38275)（Agent 地址系统 + 加密身份）、[#38280](https://github.com/NousResearch/hermes-agent/issues/38280)（Agent 经济层：钱包/信誉账本）、[#95981](https://github.com/NousResearch/hermes-agent/issues/95981)（hermes-gateway A2A transport）——社区对 agent-to-agent 基础设施兴趣浓厚；配合 #91976（A2A v1.0 一致性），A2A 是明确的战略方向。
- **Bot Mode 生态**：[#102269](https://github.com/NousResearch/hermes-agent/issues/102269)（Bot Marketplace）、[#111406](https://github.com/NousResearch/hermes-agent/issues/111406)（群聊上限可配置，已关闭标记 duplicate，说明已在推进）。
- **平台扩展**：#9154（飞书自动 thread）、#35060（HA watch 事件转发）、#51532（Matrix @mention 自动附带）。
- **可能与下版本相关**：#111543（模型白名单）与 #111415（插件目录分类）已具备 PR，落地概率高。

---

## 7. 用户反馈摘要

**痛点**
- **计费透明度**：Portal 订阅额度耗尽后价格跳变（#110912）、zai 硬编码端点静默计费（#55112）——付费用户对成本不可预测高度敏感。
- **多端体验割裂**：Telegram/Desktop/CLI 会话不互通、消息跨端丢失是最反复出现的真实使用场景痛点。
- **后台任务不可见**：[#111522](https://github.com/NousResearch/hermes-agent/issues/111522) “下载 1GB 文件”场景——聊天看似结束但后台工作无状态/进度，用户体验落差明显。
- **Windows 稳定性**：wake word 崩溃（#109982）这类平台级问题影响信任。
- **流式截断**（#103483）直接破坏对话连续性。

**满意点**
- Bot Mode + profile 分发机制被认为“已解决最难的部分”（#102269），社区在此基础上主动提出生态层设计。
- 项目对社区贡献的 salvage/修复响应迅速（大量 "salvage #" PR 引用社区提交）。

---

## 8. 待处理积压（提醒维护者关注）

| 项目 | 问题 | 建议 |
|---|---|---|
| [#77111](https://github.com/NousResearch/hermes-agent/issues/77111) | 4 个语音 PR 阻塞在 RFC 上，已开放 6 周+ | 尽快定稿 ABC 接口，解除合并队列阻塞 |
| [#59293](https://github.com/NousResearch/hermes-agent/issues/59293) | 安全旁路问题，7 月开至今未决 | 安全类应提级处理 |
| [#41220](https://github.com/NousResearch/hermes-agent/issues/41220) | 6 月提出，跨 surface resume | 归入 session-state 系统性重构 |
| [#91976](https://github.com/NousResearch/hermes-agent/issues/91976) | A2A v1.0 一致性缺口（8 月） | 随 A2A 战略一并排期 |
| [#102629 / #111231](https://github.com/NousResearch/hermes-agent/pull/111443) | Codex 重复 call_id 400 已有 fix PR 待合并 | 优先 review |
| P1 三连：#94811 / #76767 / #110422 | 会话状态与投递类 P1 均无 fix PR | 建议专项 sprint 处理 |

**总体判断**：项目发布节奏稳定（v0.21.3 一天内即有大量后续修复排队），贡献活跃、流程规范（salvage 机制、Footprint Ladder 规则运作良好）；主要风险在于安全旁路、计费类问题的响应速度，以及 session-state 类 P1 积压。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-09-15

## 1. 今日速览

PicoClaw 今日整体活跃度中等偏低：过去 24 小时共 1 条 Issue 更新、3 条 PR 更新，无新版本发布。核心维护者 @stpinkie 今日关闭了 mesh 可观测性大 PR（Track 63）及 v0.10.0 sprint 设计文档 PR，表明 **v0.10.0 冲刺周期（Tracks 60–66）正在稳步推进**，按“一 Track 一 PR”的节奏落地。社区侧，QQ 频道 401 鉴权 Bug（#3365）持续发酵但尚无官方修复；Keenable 搜索 PR（#3370）处于 stale 状态，等待维护者审查。

## 2. 版本发布

今日无新版本发布。最新版本仍为既有的 nightly 通道（`--version` 报告 `0.3.1`），正式版 v0.10.0 正处于 sprint 规划与实施阶段（见 [PR #3379](https://github.com/sipeed/picoclaw/pull/3379)）。

## 3. 项目进展

### 今日关闭/合并的 PR（2 条）

- **[PR #3380](https://github.com/sipeed/picoclaw/pull/3380) — feat(mesh): observability（Track 63）** ✅ 已关闭
  大幅增强 mesh 网络可观测性：
  - `PeerStatus` 新增 `conns[]`（remote_multiaddr、方向、经 `/p2p-circuit` 与 quic/tcp 检测的传输层、流数量、opened_at）
  - 新增 `latency_ms`（基于 peerstore `LatencyEWMA`）、`score`（`PeerScoreStore`）、`last_seen`
  - 接入 `libp2p.BandwidthReporter(metrics.NewBandwidthCounter())` 提供带宽统计，并通过 SSE 事件与活动流（activity feed）对外暴露
  **意义**：这是 v0.10.0 sprint 排序（60 → 65 → 61 → 62 → **63** → 64 → 66）中的第 5 个 Track，落地后距离 sprint 完成仅剩 Track 64 与 66，推进度约 **75%**。

- **[PR #3379](https://github.com/sipeed/picoclaw/pull/3379) — docs: v0.10.0 sprint plan** ✅ 已关闭
  将 `.todo.md` 草稿深化为可实施的设计文档，固化于 `docs/design/v0.10.0-sprint.md`，并经代码逐项核对验证。文档的合入（关闭）为后续各 Track PR 提供了明确基准。

### 待合并 PR（1 条）

- **[PR #3370](https://github.com/sipeed/picoclaw/pull/3370) — feat(tools): Keenable web search provider** ⏳ OPEN（stale）
  新增 Keenable 作为 `web_search` 提供方，亮点是**零 API key 即可用**：仅需设置 `tools.web.keenable.enabled: true`，调用其公共端点（需 `X-Keenable-Title` 头）。对降低搜索工具的配置门槛有实际价值。

## 4. 社区热点

- **[Issue #3365](https://github.com/sipeed/picoclaw/issues/3365)** — 今日最活跃话题（2 评论、1 👍、标记 stale）
  **QQ 频道 401 "Authorization参数格式错误”**：用户 @crazysarah 在 Orange Pi 3B（RK3566, aarch64）上使用 nightly 版本复现，根因定位在依赖链 `botgo v0.2.1 + resty >= v2.17` 的不兼容。**诉求分析**：QQ 频道是国内用户的核心接入渠道之一，此 Bug 属于上游依赖回归，用户希望项目通过降级 resty 或替换鉴权封装来快速止血。目前未见 fix PR，且 Issue 被打上 stale 标签，存在被自动关闭风险。

## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 | Fix PR |
|---|---|---|---|
| 🔴 高 | [#3365](https://github.com/sipeed/picoclaw/issues/3365) QQ 频道 401 鉴权失败，阻断该渠道消息收发；根因为 botgo v0.2.1 与 resty ≥ v2.17 不兼容 | OPEN（stale） | ❌ 暂无 |

今日无新增崩溃/回归报告。

## 6. 功能请求与路线图信号

- **v0.10.0 路线图已固化**（[PR #3379](https://github.com/sipeed/picoclaw/pull/3379)）：Tracks 60–66，执行顺序 60 → 65 → 61 → 62 → 63 → 64 → 66。Track 63（mesh 可观测性）已随 [PR #3380](https://github.com/sipeed/picoclaw/pull/3380) 落地，预计**下一批 PR 将覆盖 Track 64 与 66，v0.10.0 正式版可期**。
- **搜索提供方扩展**（[PR #3370](https://github.com/sipeed/picoclaw/pull/3370)）：Keenable 零密钥搜索若被合入，将进一步丰富 `web_search` 生态，是潜在的下版本功能增量。
- **依赖健康度信号**：#3365 暴露的间接依赖（resty）回归，提示项目需建立依赖升级的兼容性验证机制，可能催生 CI 层面的改进。

## 7. 用户反馈摘要

- **部署场景**：用户在低功耗 ARM 板（Orange Pi 3B / RK3566 / aarch64）上运行 nightly 构建，印证 PicoClaw 的边缘设备/个人助手定位。
- **痛点**：
  - QQ 官方频道接入在上游依赖升级后直接不可用（401），且夜间构建通道让用户被动接受依赖回归；
  - 用户自行完成了较深入的根因分析（精确到 botgo + resty 版本组合），社区技术能力较强，但缺少官方响应渠道。
- **期待**：对免配置、开箱即用能力（如 Keenable 免 API key 搜索）存在真实需求。

## 8. 待处理积压

| 条目 | 状态 | 建议动作 |
|---|---|---|
| [Issue #3365](https://github.com/sipeed/picoclaw/issues/3365) QQ 频道 401 | OPEN + **stale**，自 09-04 挂起 11 天 | ⚠️ 高优先级：评估 resty 降级/pin 版本或提交上游 botgo 修复，避免被 stale bot 自动关闭 |
| [PR #3370](https://github.com/sipeed/picoclaw/pull/3370) Keenable 搜索 | OPEN + **stale**，自 09-07 挂起 8 天 | 外部贡献者 @ilya-bogin-keenable 提交，建议维护者尽快 review，保护社区贡献积极性 |

---

**健康度小结**：项目开发节奏稳定（v0.10.0 sprint 按计划推进、约完成 75%），但**社区响应面存在滞后**——两个高价值条目均处 stale 状态，其中 #3365 为功能性阻断 Bug，建议维护者优先处置。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-09-15

## 1. 今日速览

NanoClaw 今日保持高强度开发节奏：过去 24 小时 PR 活动高达 50 条（其中 38 条已合并/关闭，12 条待合并），Issues 更新 6 条（3 开 3 关），无新版本发布。核心团队（@amit-shafnir、@glifocat 等）集中推进了 channels/providers 双分支的批量修复与 OpenCode provider 集成，同时社区贡献者持续报告稳定性与安全问题。整体判断：项目处于快速迭代期，代码吞吐量大、修复闭环速度快，但 SQLite 并发与错误信息泄露等底层稳定性问题开始浮现，值得关注。

## 2. 版本发布

今日无新版本发布。注意 PR #3465/#3470/#3471 显示 Chat SDK 已锁步升级至 4.32.0，并开启了 pnpm `minimumReleaseAge` 供应链安全门控（3 天规则），下一个版本发布时用户可能需要留意依赖行为变化。

## 3. 项目进展

今日合并/关闭的 38 条 PR 中，重点包括：

- **Chat SDK 升级与 Telegram 修复**：[#3465](https://github.com/nanocoai/nanoclaw/pull/3465) 将 Chat SDK 从 4.29.0 锁步升至 4.32.0，并修复 Telegram 中含奇数个 `_`/`*`/`~` 的链接（如 OneCLI connect 链接）发送失败的问题。
- **OpenCode provider 集成推进**（待合并，活跃更新中）：[#3733](https://github.com/nanocoai/nanoclaw/pull/3733) 实现 provider 契约与主机认证，[#3747](https://github.com/nanocoai/nanoclaw/pull/3747) 集成安装向导，[#3746](https://github.com/nanocoai/nanoclaw/pull/3746) 修复 provider 操作中的取消、失败交付与 skill 文件保护。
- **Agent 模板化创建**：[#3396](https://github.com/nanocoai/nanoclaw/pull/3396) 支持在聊天中通过模板创建子 agent；[#3428](https://github.com/nanocoai/nanoclaw/pull/3428) 让 Slack 创建流程正确携带模板引用并配发独立 bot。
- **可观测性**：[#3482](https://github.com/nanocoai/nanoclaw/pull/3482) 暴露结构化主机健康状态，单次只读调用即可判断安装状态。
- **安全加固**：[#3484](https://github.com/nanocoai/nanoclaw/pull/3484) 阻止 setup 向导将 OAuth token/API key 泄露到子进程 argv；[#3483](https://github.com/nanocoai/nanoclaw/pull/3483) 强化卸载的所有权校验与失败处理。
- **供应链与效率**：[#3470](https://github.com/nanocoai/nanoclaw/pull/3470)/[#3471](https://github.com/nanocoai/nanoclaw/pull/3471) 真正启用 pnpm `minimumReleaseAge` 门控（原配置嵌套层级错误导致从未生效）；[#3468](https://github.com/nanocoai/nanoclaw/pull/3468) 声明 WhatsApp Cloud 25 秒 typing 生命周期，将心跳调用从约 15 次/分钟降至 3 次。
- **Setup 增强**：[#3486](https://github.com/nanocoai/nanoclaw/pull/3486) 暴露构建期 preseed 目录（`--catalog-preseeds`），[#3487](https://github.com/nanocoai/nanoclaw/pull/3487) 支持 `--tz` 时区预置。

整体看，今日在渠道稳定性、安全、安装体验三条线上均有实质性推进，OpenCode 作为新 provider 的落地是近期最大的功能增量。

## 4. 社区热点

- **[#3813](https://github.com/nanocoai/nanoclaw/pull/3813) Add durable handoff safety and mission control**（@briankobekim，今日新开）：引入主机侧持久化 handoff 账本（带指纹的 source/reviewer 契约、append-only 事件），并在 bridge 层强制结构化 Slack agent-to-agent 交付——反映了社区对多 agent 协作可靠性的强烈诉求。
- **[#3706](https://github.com/nanocoai/nanoclaw/issues/3706)**（2 评论，今日关闭）：`ncl groups config add-mount` 在 `--container` 传绝对路径时静默生成错误的双重嵌套路径，用户 @DawoudIO 的反馈促使 CLI 路径处理得到修正。
- **[#3814](https://github.com/nanocoai/nanoclaw/issues/3814)**：原始错误文本可能被投递到公共频道——涉及隐私与安全，属于高敏感反馈。

## 5. Bug 与稳定性（按严重程度）

1. **高（安全/隐私）** — [#3814](https://github.com/nanocoai/nanoclaw/issues/3814)：`deliverErrorResult` 将 SDK 原始错误文本原样发回触发频道，不检查目标是否为公共频道；容器内 `claude` 进程中途死亡时可能泄露内部信息。**尚无关联 fix PR**。
2. **高（稳定性）** — [#3811](https://github.com/nanocoai/nanoclaw/issues/3811)：中央 DB（WAL 模式）未设置 `busy_timeout`，瞬时锁竞争直接抛错，表现如数据库损坏。**尚无关联 fix PR**。
3. **高（已修复）** — [#3660](https://github.com/nanocoai/nanoclaw/issues/3660)：Session SQLite 变为只读导致所有出站消息投递失败（Discord 等渠道瘫痪），今日已关闭。
4. **中（已修复）** — [#3706](https://github.com/nanocoai/nanoclaw/issues/3706)：add-mount 绝对路径产生损坏挂载路径，今日已关闭。
5. **中（已修复）** — [#3800](https://github.com/nanocoai/nanoclaw/issues/3800)：update-nanoclaw 文档化的 controller 提取漏掉三个导入脚本导致 controller 无法加载，今日关闭。
6. **中（开放）** — [#3801](https://github.com/nanocoai/nanoclaw/issues/3801)：`update-nanoclaw validate` 的 channel refresh 会覆盖本地 patch skill 修改过的文件，与自定义工作流冲突。**尚无 fix PR**。

## 6. 功能请求与路线图信号

- **OpenCode provider**：[#3733](https://github.com/nanocoai/nanoclaw/pull/3733) + [#3747](https://github.com/nanocoai/nanoclaw/pull/3747) 均为 core-team 标签、今日仍在活跃更新，极可能进入下一版本，届时 NanoClaw 将新增一个完整的多 provider 选项。
- **多 agent 可靠协作**：[#3813](https://github.com/nanocoai/nanoclaw/pull/3813)（durable handoff ledger）与 [#3719](https://github.com/nanocoai/nanoclaw/pull/3719)（A2A 通信失败回报给源 agent）共同指向“agent 间通信可审计、可恢复”的路线图方向。
- **安装自动化**：#3486/#3487 表明团队在为无人值守/预置安装铺路，后续可能支持更多 preseed 参数。

## 7. 用户反馈摘要

- **运维痛点**：#3660 反映 DB 只读故障会直接导致全部渠道消息中断，且故障“约 12 小时前开始”才被发现——用户需要更早的健康告警（#3482 的结构化健康检查正是回应）。
- **CLI 易用性**：#3706 表明用户按直觉使用绝对路径，期望 CLI 要么接受、要么明确报错，而非静默生成坏路径——“静默失败”是反复出现的负面反馈模式。
- **自定义与上游更新冲突**：#3800/#3801 显示深度使用 update-nanoclaw 工作流的用户（如 @foxsky）在本地 patch 与 upstream refresh 之间挣扎，希望更新流程尊重本地修改。
- **隐私意识**：#3814 的报告者关注公共频道场景下的信息泄露，说明用户在多人/公共环境中部署 NanoClaw。

## 8. 待处理积压

- [#3654](https://github.com/nanocoai/nanoclaw/pull/3654)（8 月 29 日开，仍 OPEN）：OneCLI 网关激活时 `host.docker.internal` 上明文 HTTP MCP server 不可达的 NO_PROXY 修复——影响 host 侧 MCP 用户，建议维护者优先 review。
- [#3719](https://github.com/nanocoai/nanoclaw/pull/3719)（9 月 4 日开）：A2A 失败回报机制，与 #3813 主题相关，建议一并评估合并顺序。
- [#3811](https://github.com/nanocoai/nanoclaw/issues/3811)、[#3814](https://github.com/nanocoai/nanoclaw/issues/3814)、[#3801](https://github.com/nanocoai/nanoclaw/issues/3814)：今日新开且暂无 fix PR，其中 #3811（无 busy_timeout）修复成本低、收益高，可作为快速跟进项。

---
*数据来源：GitHub API（过去 24 小时），统计窗口截至 2026-09-15。链接以 nanocoai/nanoclaw 仓库为准。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目日报 · 2026-09-15

## 1. 今日速览

过去 24 小时，NullClaw 项目整体活跃度**偏低但保持社区讨论热度**：无 PR 更新、无新版本发布、无 Issue 关闭，但 4 条 Issue 保持活跃（其中 2 条为今日新开）。讨论焦点集中在 **搜索能力的外部依赖治理**（Firecrawl 端点可配置化、预付费代理方案）与**新模型接入诉求**（grok-cli provider）。项目处于功能讨论期，无代码层面推进。

## 2. 版本发布

今日无新版本发布，最新 Releases 无更新。省略。

## 3. 项目进展

今日**无 PR 合并或关闭**，无 Issue 关闭，代码库无净变化。活跃度主要体现在需求侧（Issues），供给侧（PR）静默。建议关注后续是否有针对 #993 的社区 PR 出现。

## 4. 社区热点

- **[#993](https://github.com/nullclaw/nullclaw/issues/993) — Firecrawl 搜索端点可配置化**（enhancement，2 评论，8/24 提出、今日仍在讨论）
  `src/tools/web_search_providers/firecrawl.zig` 中 API 端点硬编码为 `https://api.firecrawl.dev/v1/search`，自托管 Firecrawl 用户无法使用原生 `search_provider: "firecrawl"`。诉求明确、改动面小（仅需将 endpoint 提升为配置项），是典型的低成本高价值 enhancement。
- **[#998](https://github.com/nullclaw/nullclaw/issues/998) 与 [#997](https://github.com/nullclaw/nullclaw/issues/997) — 预付费搜索中转方案**（均今日新开）
  同一作者 @iamalanlui 推广其 apifare 预付费 MCP 计量代理，针对无密钥 DuckDuckGo 不够用（关联 [#871](https://github.com/nullclaw/nullclaw/issues/871)）的场景，避免在主机配置中存放 Brave/Firecrawl 密钥。**注意：两条 Issue 带有较明显的自荐/推广属性，维护者可酌情标记为 spam/广告并观察。**
- **[#975](https://github.com/nullclaw/nullclaw/issues/975) — grok-cli provider**（2 评论，今日仍有讨论）
  希望沿用 `claude-cli`/`codex-cli`/`gemini-cli` 的子进程登录态模式（`src/provider_probe.zig:43`），通过本地 grok CLI 订阅会话接入 Grok，规避 API 计费。

## 5. Bug 与稳定性

今日**无新增 Bug、崩溃或回归报告**。关联背景：#998 提到的 [#871](https://github.com/nullclaw/nullclaw/issues/871)（弱设备上 DuckDuckGo 默认搜索 vs Brave/SearXNG 的问题）仍为历史遗留 bug 线程，今日无修复 PR。

## 6. 功能请求与路线图信号

| 需求 | 可能性 | 依据 |
|---|---|---|
| Firecrawl 端点可配置（[#993](https://github.com/nullclaw/nullclaw/issues/993)） | **高** | 改动小、契合自托管用户群、已有 2 条讨论持续至今日 |
| grok-cli provider（[#975](https://github.com/nullclaw/nullclaw/issues/975)） | **中** | 与现有 CLI provider 架构模式一致，复用 `provider_probe.zig` 路径，但依赖 grok CLI 稳定性 |
| 预付费代理集成（[#997](https://github.com/nullclaw/nullclaw/issues/997) / [#998](https://github.com/nullclaw/nullclaw/issues/998)） | **低** | 属第三方服务自荐，非社区共识需求 |

## 7. 用户反馈摘要

- **自托管用户**：希望搜索、模型等外部服务端点均可配置（#993），减少对 SaaS 依赖。
- **成本敏感用户**：偏好 CLI 登录态/订阅制接入以规避按 token 计费（#975），或采用预付费中转控制搜索 API 开销（#998/#997）。
- **弱设备用户体验**：#871 反映默认 keyless DuckDuckGo 搜索在低配设备上体验不佳，是搜索相关诉求的底层动因。

## 8. 待处理积压

- **[#975](https://github.com/nullclaw/nullclaw/issues/975)**（7/11 提出，已 2 个月）与 **[#993](https://github.com/nullclaw/nullclaw/issues/993)**（8/24 提出，已 3 周）均无维护者明确回应或关联 PR，建议维护者优先表态，尤其 #993 实现成本低、可直接引导社区贡献。
- **[#871](https://github.com/nullclaw/nullclaw/issues/871)** 弱设备搜索问题作为根源性 bug 长期未解，间接催生了 #997/#998 这类外溢讨论，值得纳入排期。

---
*数据来源：GitHub（过去 24 小时窗口）。总体健康度：社区需求讨论健康，但需警惕推广型 Issue，且 Issue 关闭率与 PR 产出本日均为 0，建议关注维护节奏。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-09-15

## 1. 今日速览

IronClaw 过去 24 小时整体活跃度偏低：1 条 Issue 更新、1 条 PR 更新、无新版本发布。唯一的 Issue 是每日例行的失败分类报告（#8100），PR 活动集中在 9 天前开出的 MCP 诊断修复 PR #8077 的更新。属于典型的“例行维护日”，项目处于稳定运行、无重大事件的状态。

## 2. 版本发布

无新版本发布，本节省略。

## 3. 项目进展

今日无 PR 合并或关闭。唯一活跃 PR：

- **[#8077](https://github.com/nearai/ironclaw/pull/8077) fix(mcp): classify response leak diagnostics**（@linhongyu510，创建于 2026-09-06，今日更新）
  - 关联 Issue #8009，修复 MCP 出口诊断逻辑：将共享的 `response_leak_blocked` 哨兵值集中到 `ironclaw_host_api::http`，并让 MCP 通道对该哨兵进行分类，在保持宿主侧泄漏拦截安全性的同时保留 MCP 可见的独立错误原因。
  - 该 PR 已挂起 9 天仍未合并，是当前待合并队列中唯一的 PR，建议维护者跟进 review。

## 4. 社区热点

今日无高热度讨论：

- **[#8100 Daily ironclaw failure taxonomy — 2026-09-14](https://github.com/nearai/ironclaw/issues/8100)**（@pranavraja99）— 机器人/自动化生成的每日失败分类报告，0 评论 0 👍。报告指出 officeqa suite 本次运行中 43 个未通过任务几乎全部为真实模型质量错误（涉及 DeepSeek-V4-Flash 导航相关失败），而非基础设施或框架问题。这类日报的价值在于持续为模型质量改进提供数据基线，而非社区讨论热点。

## 5. Bug 与稳定性

今日无新的用户报告 Bug。相关信息：

1. **【已有 fix PR】MCP 响应泄漏诊断分类缺陷（#8009 → PR [#8077](https://github.com/nearai/ironclaw/pull/8077)）**：属安全/诊断准确性问题，涉及宿主泄漏拦截与 MCP 错误可见性的边界，fix PR 待合并。
2. **【外部依赖，非代码 Bug】officeqa 43 个未通过任务**（[#8100](https://github.com/nearai/ironclaw/issues/8100)）：确认为底层模型（DeepSeek-V4-Flash）能力问题，非 IronClaw 框架缺陷，无需框架侧修复。

## 6. 功能请求与路线图信号

今日无新增功能请求。可推断的信号：

- PR #8077 显示团队在**强化 MCP 出口安全与诊断可观测性**方向持续投入，若合并，或随下一版本以诊断改进形式发布。
- 每日失败分类日报（#8100 系列）表明项目将**基准测试驱动的模型质量追踪**作为常态化机制，暗示后续迭代会更多围绕 agent 执行可靠性展开。

## 7. 用户反馈摘要

今日 Issue 均为自动化报告，无真实用户评论可供提炼。间接信号：

- 失败分类报告将错误明确归因于模型质量而非框架，反映 IronClaw 作为评测/agent 基础设施的定位清晰，工具本身的稳定性在用户认知中较好。
- PR #8077 的存在（针对泄漏诊断的细化）说明此前用户/开发者对“拦截原因不透明”存在痛点，该 PR 正是对此体验的改进。

## 8. 待处理积压

- **PR [#8077](https://github.com/nearai/ironclaw/pull/8077)**：开 PR 已 9 天，今日有更新但仍待合并，且关闭的 #8009 依赖此修复。**建议维护者优先 review 并推进合并。**
- Issue #8100 为当日新建的例行报告，尚无积压风险，但需确认该系列日报是否有人定期消化归档。

---

**健康度小结**：项目无紧急问题，框架侧稳定；主要行动项为合并 PR #8077。建议明日关注该 PR 的 review 进展及失败分类日报中模型质量错误的趋势变化。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目日报 · 2026-09-15

## 1. 今日速览

- 过去 24 小时项目共更新 **1 条 Issue + 25 条 PR**，无新版本发布，整体处于**依赖维护与小步迭代阶段**，无重大功能落地。
- PR 活动以 **dependabot 依赖升级为主**（约 20/25 条），其中出现大量“关闭旧 PR → 重开新 PR”的循环，反映依赖升级合并节奏偏慢。
- 值得关注的实质进展是 **#2665（OpenClaw v2026.8.1 + Electron 43 升级）已于昨日合并**，是近期最大的一次运行时升级。
- Issue 侧近乎沉寂，仅一条 3 月份的 IM 消息丢失 Bug（#1035）被 stale 机制触碰，暴露社区反馈响应存在滞后。

## 2. 版本发布

今日无新 Release。

## 3. 项目进展

**已合并/关闭的重要 PR：**

- **[#2665](https://github.com/netease-youdao/LobsterAI/pull/2665)** `feat: upgrade OpenClaw to v2026.8.1 and improve artifact workflows`（@fisherdaddy）— 今日最重要进展。将内置 OpenClaw 运行时从 v2026.6.1 升级至 **v2026.8.1**，Electron 从 40.2.1 升级至 **43.5.0**，同时改进 Markdown 编辑、Library 组织与应用内浏览器，并优化构建产物工作流。这是一次跨渲染层/主进程/IM/协作多模块的大版本升级。
- **[#2664](https://github.com/netease-youdao/LobsterAI/pull/2664)** `fix(openclaw): avoid POPO SDK loading races` — 修复 OpenClaw 升级后 POPO 2.1.13 在 ESM import 未完成时同步 require 引发的 `ERR_REQUIRE_ESM_RACE_CONDITION`，避免重启后 POPO 账号监听器失效（仍为 OPEN，待合并）。

**依赖维护（关闭旧的、重开新的）：**

| 依赖 | 旧 PR（已关闭） | 新 PR（待合并） |
|---|---|---|
| mermaid | #2587 | [#2672](https://github.com/netease-youdao/LobsterAI/pull/2672) |
| react-dom | #2464 | [#2671](https://github.com/netease-youdao/LobsterAI/pull/2671)（19.3.0） |
| @types/react-dom | #2582 | [#2670](https://github.com/netease-youdao/LobsterAI/pull/2670) |
| vite | #2586 | [#2669](https://github.com/netease-youdao/LobsterAI/pull/2669)（5→8 大版本） |
| trufflehog | #2583 | [#2667](https://github.com/netease-youdao/LobsterAI/pull/2667) |

另有 CI 工具链升级 [#2666](https://github.com/netease-youdao/LobsterAI/pull/2666)（actions/labeler v5→v7）、typebox [#2668](https://github.com/netease-youdao/LobsterAI/pull/2668)。

**总体评估：** 项目实质推进集中在 #2665 的运行时升级落地，相当于迈出了“下一版本基座”的关键一步；其余为例行依赖轮换，合并速度有待提升。

## 4. 社区热点

- **[#2673](https://github.com/netease-youdao/LobsterAI/pull/2673)** `feat(auth): align login introduction with portal showcase`（@btc69m979y-dotcom，今日新开）— 新装桌面端将展示与官方门户一致的登录引导页：左侧十个图文用例、右侧欢迎文案与登录入口，支持 X/Esc 跳过。体现团队正在**打磨首次使用体验与品牌一致性**，属于 UX 精细化阶段。
- Issue 侧无新增讨论，#1035（见下文）为唯一活跃条目。

## 5. Bug 与稳定性

**🔴 高（未修复）：**
- **[#1035](https://github.com/netease-youdao/LobsterAI/issues/1035)** `NimGateway 重连后消息去重缓存未清空，导致正常消息被静默丢弃` — `processedMessages` 为模块级全局 Map，所有实例共享；网络抖动重连（stop+start）后，TTL 未到期的旧消息 ID 导致新会话同 ID 消息被误判为重复而**静默丢弃，用户无感知**。属数据丢失级缺陷，且已被标记 stale（创建于 2026-03-30，超过 5 个月未处理）。**尚无对应 fix PR。**

**🟡 中（已有 fix PR 待合并）：**
- POPO SDK 加载竞态导致重启后账号监听器缺失 — 已由 [#2664](https://github.com/netease-youdao/LobsterAI/pull/2664) 修复，随 #2665 升级产生，说明大版本升级引入的回归正在被快速跟进。

## 6. 功能请求与路线图信号

- 今日无新功能请求。
- 从 PR 流向可推断路线图：**OpenClaw v2026.8.1 + Electron 43 已合并**，登录引导页（#2673）在途，预示下一版本重点是**运行时现代化 + 新用户引导**；React 19 / Vite 8 等前端栈大版本升级（#2671/#2669/#2670）若合并，将成为后续渲染层重构的基础。

## 7. 用户反馈摘要

- 今日无新用户评论。可提炼的既有痛点：
  - **消息可靠性**：IM 消息静默丢失（#1035）是典型可靠性痛点——用户“无任何感知”，此类问题对助手类产品信任度伤害最大。
  - **稳定性场景**：POPO 竞态 Bug 表明用户遭遇“重启后 POPO 账号失联”，反映多网关场景下的初始化健壮性需求。

## 8. 待处理积压

| 条目 | 状态 | 建议 |
|---|---|---|
| [Issue #1035](https://github.com/netease-youdao/LobsterAI/issues/1035) IM 消息静默丢弃 | 5+ 个月未响应，已 stale | **数据丢失级 Bug，建议优先修复**（方案：将 Map 移入实例或在 stop() 中清空） |
| [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277) electron 43→44 升级 | 挂起 5+ 个月 | #2665 已落 Electron 43，此 PR 目标变为 44，可更新重测 |
| [PR #2459](https://github.com/netease-youdao/LobsterAI/pull/2459) js-x-ray 14→16（跨大版本） | stale | 涉及安全扫描能力，建议评估后合并或关闭 |
| [PR #2461](https://github.com/netease-youdao/LobsterAI/pull/2461) eslint-plugin-react-hooks 5→7 | stale | 与 React 19 升级（#2671）绑定，建议同批处理 |

**健康度小结：** 核心开发（@fisherdaddy、@btc69m979y-dotcom）仍活跃，大版本升级能力在线；但依赖 PR 积压严重、社区 Issue 响应迟缓（尤其数据丢失类 Bug 长期无回应）是需要关注的健康度信号。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-09-15

## 1. 今日速览

今日 Moltis 仓库整体活跃度**偏低**。过去 24 小时无新开或活跃 Issue（0 条）、无版本发布，仅收到 1 条待合并 Pull Request。值得关注的是，该 PR（#1269）针对 OAuth 认证流程中的测试稳定性问题，属于 CI/测试基础设施的质量提升，表明维护者仍在持续打磨核心认证模块的可靠性。整体来看，项目处于**平稳维护期**，无紧急事件或回归风险。

## 2. 版本发布

今日无新版本发布。最新 Releases 列表为空，项目暂未采用常规 release 节奏（或依赖 CI 构建产物分发）。

## 3. 项目进展

今日无已合并/关闭的 PR，**净进展为 0**，但有一项待合并工作：

- **[#1269](https://github.com/moltis-org/moltis/pull/1269) `test(oauth): remove success-popup timing race`**（@penso，OPEN）
  - 修复 CI 失败问题（对应任务 moltis-064r，源自 [Actions run #32917698826](https://github.com/moltis-org/moltis/actions/runs/32917698826/jobs/98024870973)）
  - 核心改动：在 PKCE 登录成功与断开连接测试中，不再依赖“立即关闭的回调弹窗”的 `page/close` 事件，改为等待主页面持久的认证状态，消除时序竞态
  - 意义：提升 OAuth（PKCE）相关 E2E 测试的确定性，减少 CI 误报，属于测试基础设施的稳健性改进

## 4. 社区热点

今日无任何 Issue 活跃，也无 PR 评论互动（#1269 评论数为 0，👍 0）。**社区讨论热度为零**，暂无可提炼的社区诉求。这可能与项目处于维护阶段、或用户反馈渠道不在此仓库有关，建议关注后续是否有讨论回流。

## 5. Bug 与稳定性

今日**无用户报告的新 Bug**。但有一条来自 CI 的内部问题被处理：

| 问题 | 严重程度 | 状态 |
|---|---|---|
| OAuth PKCE 成功/断开测试因弹窗时序竞态导致 CI 偶发失败（[CI 日志](https://github.com/moltis-org/moltis/actions/runs/32917698826/jobs/98024870973)） | 低（仅影响测试稳定性，非生产 Bug） | ✅ 已有 fix PR：[#1269](https://github.com/moltis-org/moltis/pull/1269) |

无崩溃或回归报告。

## 6. 功能请求与路线图信号

今日无新功能请求。从 #1269 可推断的间接信号：

- 维护者当前精力集中在 **认证模块（OAuth/PKCE）的测试可靠性**上，短期内相关 QA 工作可能继续，而非新功能开发
- 无足够信息判断下一版本的功能范围

## 7. 用户反馈摘要

今日无 Issue 评论数据，**无法提炼用户反馈**。建议持续观察后续 Issues 与 PR 评论的回流情况。

## 8. 待处理积压

- 当前唯一待处理项：**PR [#1269](https://github.com/moltis-org/moltis/pull/1269)** 今日刚创建，尚在合理等待期内，建议维护者尽快 review 合并，以恢复 CI 绿色状态
- 由于今日数据中无长期未响应的 Issue/PR 记录，无法识别历史积压；建议维护者定期梳理 stale Issues，保持项目健康度

---

**健康度小结**：今日项目活动量极低（1 PR / 0 Issue / 0 Release），无生产风险信号。唯一动作是修复 CI 测试竞态，属于预防性维护。建议关注 #1269 的合并进展及后续社区活跃度变化。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-09-15

## 1. 今日速览

CoPaw 今日保持高活跃度：过去 24 小时内 Issues 更新 44 条（新开/活跃 26，关闭 18），PR 更新 50 条（待合并 39，已合并/关闭 11），无新版本发布。社区讨论焦点集中在**记忆系统可靠性**（遗忘、索引不同步、内存泄漏）与**任务执行稳定性**（停止失效、subAgent 超时、定时任务无输出）。开发者侧 PR 流水线健康，Hub 多租户能力（#7779）、cron 任务增强（#7776）等重量级功能正在推进中。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 及重要进展：

- **[PR #7703](https://github.com/agentscope-ai/QwenPaw/pull/7703)（已关闭）** — Visual Compact 重构：稳定图片批处理、原文回溯、更易读的压缩预设，直接回应用户对上下文压缩体验的抱怨（关联 #5122）。
- **[PR #7753](https://github.com/agentscope-ai/QwenPaw/pull/7753)（已合并）** — make-skill 升级到 v2.1：强制先持久化 plan 再创建草稿，堵住 QA 中发现的跳过规划漏洞，提升技能生成健壮性。

仍在审查中的重点 PR：

- **[PR #7779](https://github.com/agentscope-ai/QwenPaw/pull/7779)** — Hub 托管模型、邀请机制与组织/成员月度 token 预算，面向团队部署场景的战略性功能。
- **[PR #7776](https://github.com/agentscope-ai/QwenPaw/pull/7776)** — cron 定时任务配置增强、执行历史保留、收件箱结果改进，直接对应 Issue #7709 的痛点。
- **[PR #7732](https://github.com/agentscope-ai/QwenPaw/pull/7732)** — ACP 权限选项按协议 `kind` 匹配，修复 #7726 描述的 `trusted: true` 回退交互提示问题。
- **[PR #7637](https://github.com/agentscope-ai/QwenPaw/pull/7637)** — QwenPaw-Data 0.3.0 集成，数据分析引擎能力扩展。

整体看，项目在**Hub/多租户、定时任务、ACP 协议兼容、上下文压缩**四个方向同步推进，节奏稳健。

## 4. 社区热点

- **[#7567](https://github.com/agentscope-ai/QwenPaw/issues/7567)（7 评论）** — 点击“停止”后 UI 显示已停止，但任务实际仍在执行，导致后续指令 409 冲突。执行状态与前端展示不同步是用户信任度的核心问题。
- **[#7709](https://github.com/agentscope-ai/QwenPaw/issues/7709)（6 评论）** — 定时任务输出被折叠进 thinking 或干脆丢失，用户无法看到结果。已有 PR #7776 针对性修复中。
- **[#7678](https://github.com/agentscope-ai/QwenPaw/issues/7678)（6 评论）** — spawn subAgent 全部 timeout 失败，子代理派生是 Agent 框架的核心能力，此问题阻断多代理工作流。
- **[#7571](https://github.com/agentscope-ai/QwenPaw/issues/7571)（6 评论）** — Agent 记不住用户规定的工作路径约定，反映长期记忆写入/召回机制的薄弱，与多个已关闭的记忆类 Issue（#4220、#3995）同源。
- **[#7749](https://github.com/agentscope-ai/QwenPaw/issues/7749)（4 评论）** — 用户找不到 2.2.1 模型故障切换的配置入口，暴露新功能文档/可发现性不足。

## 5. Bug 与稳定性（按严重程度）

| 级别 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| 🔴 高 | [#7722](https://github.com/agentscope-ai/QwenPaw/issues/7722) | 后端长期运行内存涨至 20GB+（运行时累积） | 相关分析见 #7722 下讨论 |
| 🔴 高 | [#7722 关联 #7722 分析](https://github.com/agentscope-ai/QwenPaw/issues/7722) / [#7722 复合路径分析](https://github.com/agentscope-ai/QwenPaw/issues/7722) | 内存耗尽三路径复合：无界流缓冲、keep-alive 实例堆叠、doom-loop 绕过闸门（含最小修复方案） | 社区已给出修复建议，待官方 PR |
| 🔴 高 | [#7567](https://github.com/agentscope-ai/QwenPaw/issues/7567) | 停止按钮 UI/执行状态不同步 | 暂无 fix PR |
| 🟠 中 | [#7678](https://github.com/agentscope-ai/QwenPaw/issues/7678) | subAgent 派生全部超时失败 | 暂无 fix PR |
| 🟠 中 | [#7708](https://github.com/agentscope-ai/QwenPaw/issues/7708) | 使用中大模型配置莫名丢失 | 暂无 fix PR |
| 🟠 中 | [#7767](https://github.com/agentscope-ai/QwenPaw/issues/7767) | 插件构建批次 Bug：附件陈旧 blob、一次性 cron 误丢弃、on_acting 不触发 | 暂无 fix PR |
| 🟡 低 | [#7727](https://github.com/agentscope-ai/QwenPaw/issues/7727) | 越界写入拦截无法识别 kimi-code 的 Write 工具路径字段，安全闸门失效 | 相关 PR #7732 同域 |
| 🟡 低 | [#7726](https://github.com/agentscope-ai/QwenPaw/issues/7726) | ACP trusted 回退交互提示 | ✅ [PR #7732](https://github.com/agentscope-ai/QwenPaw/pull/7732) 修复中 |
| 🟡 低 | [#7715](https://github.com/agentscope-ai/QwenPaw/issues/7715) | Daily Paper 静默失败，错误信息掩盖真实原因（代理不可达） | 暂无 fix PR |
| 🟡 低 | [#7771](https://github.com/agentscope-ai/QwenPaw/issues/7771) | 压缩/新对话产生空白会话标题 | 暂无 fix PR |

## 6. 功能请求与路线图信号

- **工具显式调用**（[#7778](https://github.com/agentscope-ai/QwenPaw/issues/7778)/[#7780](https://github.com/agentscope-ai/QwenPaw/issues/7780)，当日开当日关）— 通过 `//` 模糊搜索明确调用工具。快速关闭可能意味着已有实现或纳入计划，值得关注关闭原因。
- **历史对话移至右侧**（[#7739](https://github.com/agentscope-ai/QwenPaw/issues/7739)）— 已有 [PR #7704](https://github.com/agentscope-ai/QwenPaw/pull/7704)（文件抽屉右侧化）在审，UI 右侧化趋势明确，大概率被采纳。
- **Skill 按渠道限定**（[#7746](https://github.com/agentscope-ai/QwenPaw/issues/7746)）— 自定义 channel 的 skill 可见性控制，符合多渠道架构方向。
- **Hub 托管模型 + token 预算**（[PR #7779](https://github.com/agentscope-ai/QwenPaw/pull/7779)）— 释放出项目向**团队/组织协作平台**演进的明确信号，可能成为下个大版本主打。
- **记忆系统重构信号**：reranker UI（[PR #6399](https://github.com/agentscope-ai/QwenPaw/pull/6399)）、auto-memory 索引同步（#4220 已关闭）、ReMe4 路线图（#6840 已关闭）共同指向记忆子系统是下阶段投入重点。

## 7. 用户反馈摘要

**痛点：**
- **记忆不可靠是最高频抱怨**：用户反复强调的约定（文件路径规范）两天后就被遗忘（#7571），甚至导致错误覆盖运行时代码，用户表示“我不知道怎么解决了”。
- **结果可见性差**：定时任务、正常对话的结果被折叠进 thinking 或丢失（#7709）；send_file_to_user 文件藏在折叠步骤里（PR #7750 修复中）。
- **桌面端稳定性**：模型配置丢失（#7708）、安装失败（#7660）、上下文压缩产生空白会话（#7771），Windows 桌面用户体验问题集中。
- **生态兼容**：newapi 代理（#7772）、Cloudflare 403 HTML 页面误报（PR #7684 修复中）、OpenAI 兼容层 kwargs 拒收（PR #7738 修复中）——用户大量使用第三方代理/网关。

**满意点：**
- 社区贡献质量高：多位用户提交带复现步骤和最小修复方案的深度报告（#7722 复合路径分析、#7726/#7727 ACP 系列）。
- 首次贡献者活跃（PR #7738、#7773、#7774），项目对新人友好度良好。

## 8. 待处理积压

- **[#7222](https://github.com/agentscope-ai/QwenPaw/issues/7222)** — 后端内存增长至 20GB+，8-23 开启至今未关闭，属最严重的运行时资源问题，且已有社区深度分析（#7722 复合路径），建议优先排期修复 PR。
- **[#7567](https://github.com/agentscope-ai/QwenPaw/issues/7567)** — 停止按钮失效，9-04 报告，7 条评论仍无官方响应迹象。
- **[#7678](https://github.com/agentscope-ai/QwenPaw/issues/7678)** / **[#7571](https://github.com/agentscope-ai/QwenPaw/issues/7571)** — subAgent 超时与记忆遗忘，均超 4 天、6 条评论，核心功能阻断，需维护者介入。
- **[PR #6399](https://github.com/agentscope-ai/QwenPaw/pull/6399)**（7-23 开启，至今在审近两月）与 **[PR #7382](https://github.com/agentscope-ai/QwenPaw/pull/7382)**（8-28 开启）审查周期偏长，建议加快评审避免贡献者流失。

---

**健康度小结**：Issue 关闭率（18/44 ≈ 41%）与 PR 吞吐（39 待合并/11 完成）显示项目维护力量充足；但**内存泄漏、任务停止失效、subAgent 超时**三个高严重度 Issue 尚无对应 fix PR，是当前项目稳定性风险的 主要来源。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目日报 · 2026-09-15

## 1. 今日速览

过去 24 小时，ZeptoClaw 项目整体活跃度**较低但聚焦**：共 1 条 Issue 更新（关闭 1 条）、1 条 PR 更新（关闭 1 条），无新版本发布。项目今日动态完全集中在 CI 安全审计链路的修复上——维护者 @qhkm 关闭了 Issue #676 及对应修复 PR #677，表明 rustsec 安全审计报告无法发布的权限问题已得到处理。无新增 Bug 或功能请求，社区讨论热度平淡，属于典型的维护性收尾日。

## 2. 版本发布

今日无新版本发布，最近亦无 Release 记录。

## 3. 项目进展

- **PR #677 [已关闭] fix(ci): allow rustsec audit check reporting**（[链接](https://github.com/qhkm/zeptoclaw/pull/677)）
  修复了 `rustsec/audit-check` 在 CI 中因 job token 缺少 check-run 写权限而无法发布审计结果的问题。修复方案遵循最小权限原则：仅对审计 job 授予 `contents: read` 和 `checks: write`，权限严格限定在 job 范围内。
  - **影响评估**：属于 CI 基础设施质量改进，不影响运行时功能。主分支安全审计本身一直通过（"No vulnerabilities were found"），此修复仅确保审计结果能正确上报，对保障后续依赖漏洞的持续可见性有价值。

## 4. 社区热点

今日无高热度讨论。唯一动态来自维护者本人：

- **Issue #676 [chore, P2-high] chore(ci): grant rustsec audit job checks write permission**（[链接](https://github.com/qhkm/zeptoclaw/issues/676)），0 评论、0 👍，已于今日关闭。该 Issue 详细记录了问题现场：audit 审计成功后，创建 check run 时报 `Resource not accessible by integration`。
  - **诉求分析**：这是一条自驱动的 CI 治理任务，反映维护者对 CI 安全流水线可靠性和权限最小化的重视，而非社区外部反馈。

## 5. Bug 与稳定性

今日**无新报告的 Bug、崩溃或回归问题**。

相关已处理问题：
- ~~CI rustsec 审计无法上报结果~~（Issue #676，P2-high，已由 PR #677 修复并关闭）

## 6. 功能请求与路线图信号

今日无新功能请求，无法据此推断路线图变化。从近期动态看，维护者当前精力集中在 **CI/安全工程化**（审计权限、依赖漏洞扫描），暗示下一阶段可能继续强化安全与质量基础设施，而非新功能开发。

## 7. 用户反馈摘要

今日 Issues/PR 均由维护者 @qhkm 发起且评论数为 0，**无外部用户反馈可提炼**。项目近期用户声音处于静默期。

## 8. 待处理积压

当前可见范围内无长期未响应的 Issue 或 PR。建议维护者：

- 关注 PR #677 中最小权限方案落地后的实际 CI 运行效果，确认 audit check run 能稳定发布；
- 用户反馈渠道近一周期较为沉寂，可考虑通过示例、文档或 Roadwaymap 更新激活社区参与度，提升项目外部可见性。

---

**健康度小结**：今日项目呈“低流量、高自律”状态——无版本、无社区噪音，但安全审计链路完成闭环修复，工程质量持续在线。

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*