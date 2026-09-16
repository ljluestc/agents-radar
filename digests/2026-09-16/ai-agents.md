# OpenClaw 生态日报 2026-09-16

> Issues: 500 | PRs: 500 | 覆盖项目: 14 个 | 生成时间: 2026-09-16 03:55 UTC

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

# OpenClaw 项目动态日报 — 2026-09-16

## 1. 今日速览

- 项目保持**高活跃度**：过去 24 小时 Issues 更新 500 条（新开/活跃 338，关闭 162），PR 更新 500 条（待合并 341，已合并/关闭 159），吞吐健康，关闭率约 32%。
- **无新版本发布**，最新 stable 仍为 2026.9.4（3a9d69d），`latest` 与 `beta` 同指该版本。
- 今日 PR 活动以**维护者驱动的修复与质量工程**为主（@steipete、@vincentkoc、@shakkernerd 等提交了 20+ 个待审 PR），聚焦 Gateway 性能、Codex 集成、移动端 Cloudflare Access 接入与 CI 稳定性。
- 社区侧**会话状态（session-state）与消息丢失（message-loss）类 Bug** 仍是最大痛点，多个 P0/P1 长期议题持续发酵。

---

## 2. 版本发布

今日无新版本发布。以下为近期版本线上状态的观察：2026.9.2–2026.9.4 是近期多个回归问题的关联版本（详见第 5 节）。

---

## 3. 项目进展

今日以“待合并 PR 密集提交”为主，修复面广但合并节奏偏保守，代表性进展：

**Gateway / 运行时性能**
- [#149388](https://github.com/openclaw/openclaw/pull/149388) avoid full session scans during Gateway admission（XL，P2）——消除启动时全量会话校验导致的卡顿，直击 #91588 内存/性能类投诉。
- [#149663](https://github.com/openclaw/openclaw/pull/149663) Bun 支持打开超过 4 个 SQLite store——修复多 agent 部署下存储上限。
- [#149420](https://github.com/openclaw/openclaw/pull/149420) 插件 blob 读取去除二次拷贝，降低大文件内存开销。

**Codex 集成**
- [#149614](https://github.com/openclaw/openclaw/pull/149614) 时钟跳变下保持请求预算；[#149647](https://github.com/openclaw/openclaw/pull/149647) 修复指令变更后远程会话无法恢复；[#149662](https://github.com/openclaw/openclaw/pull/149662) 恢复 provider 归一化后的 MCP 工具发现（接续被路由保留的 #149522）。

**插件系统 / 稳定性**
- [#149646](https://github.com/openclaw/openclaw/pull/149646) + [#149644](https://github.com/openclaw/openclaw/pull/149644)（@Patrick-Erichsen）：插件热重载复用编译产物、释放旧注册表——与 #136311（19GB 孤儿 reindex 临时库）和 #139710（插件热重载杀死进行中 turn）直接相关，是内存泄漏治理的一层。

**移动端**
- Android/iOS 的 Cloudflare Access 浏览器会话验证三连 PR（[#147061](https://github.com/openclaw/openclaw/pull/147061)、[#147305](https://github.com/openclaw/openclaw/pull/147305)、[#147238](https://github.com/openclaw/openclaw/pull/147238)），均 XL 且带 compatibility/security-boundary 合并风险标记，是移动端受保护 Gateway 连接的重要铺路。

**质量工程**
- [#149665](https://github.com/openclaw/openclaw/pull/149665) 修复 compact CI 长尾任务（30+ 分钟单 bin）；[#149641](https://github.com/openclaw/openclaw/pull/149641) 修复 macOS 测试挂起。

**总体评价**：单日 30+ 个 ready-for-maintainer-look PR，修复方向集中在性能、插件生命周期与移动端安全接入，项目推进节奏快，但合并积压值得注意。

---

## 4. 社区热点

| Issue | 评论 | 热点核心 |
|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) 工具调用间文本泄漏到消息渠道（P1，💎） | 40 | 自 2 月开着，Slack/iMessage 用户持续受内部处理文本打扰，涉及安全审查，长期无 fix PR |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) hook/工具子进程僵尸累积 | 30 | 回归类，运行时劣化，用户要求 reap 机制 |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) Gateway 内存泄漏 350MB→15.5GB | 25 | 长期 OOM 崩溃，今日仍有更新，社区持续追加复现数据 |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) Codex PreToolUse hook 100% CPU 卡死 RPC（P0） | 24 | P0 级稳定性问题开放 3 个月 |
| [#119720](https://github.com/openclaw/openclaw/issues/119720) 同步持久化阻塞 Gateway 事件循环 | 20 | 已有部分修复落地（#140231、#138984），社区跟进讨论中 |

**诉求分析**：热点高度集中在 **Gateway 资源治理（内存/CPU/进程）** 和 **会话状态正确性**。用户普遍认可修复在推进（#119720 的分阶段修复被正面提及），但对 P0/P1 议题“needs-maintainer-review”标签长期挂着不满。

---

## 5. Bug 与稳定性（按严重程度）

**P0**
- [#148866](https://github.com/openclaw/openclaw/issues/148866) ✅已关闭 — `gateway.bind=lan` 下 Gateway 永久重启循环（2026.9.1/9.4），Ubuntu/systemd，创建当日即关闭，响应迅速。
- [#143524](https://github.com/openclaw/openclaw/issues/143524) — Agent SQLite WAL 数天涨至 1.4–2.8GB，阻塞 Windows 上 Gateway 启动（ux-release-blocker）。**无 fix PR**。
- [#146637](https://github.com/openclaw/openclaw/issues/146637) — 2026.9.3→9.4 npm 升级在 Linux Mint 全局安装 swap 步骤失败（ux-release-blocker）。**无 fix PR**。
- [#145929](https://github.com/openclaw/openclaw/issues/145929) ✅已关闭 — auth profile logout 永久失败 "lock-may-be-busy"。
- [#115642](https://github.com/openclaw/openclaw/issues/115642) — 计费冷却 5 小时 TTL 覆盖故障恢复期，订阅用户被误禁。**无 fix PR**。

**P1 回归（2026.9.2–9.4 引入，社区集中反馈）**
- [#139847](https://github.com/openclaw/openclaw/issues/139847) 回复进行中到达的消息被丢弃（"no active tool authority snapshot"），已有 queueable-fix 标签；同族 [#148707](https://github.com/openclaw/openclaw/issues/148707)（9.4 回归）、[#144809](https://github.com/openclaw/openclaw/issues/144809)（长 turn 且回复）。
- [#111897](https://github.com/openclaw/openclaw/issues/111897) 同一 session lane 并发 run 产生重复回复。
- [#144911](https://github.com/openclaw/openclaw/issues/144911) MCP server 初始化超时触发未处理 rejection 导致 Gateway 整体崩溃。
- [#136311](https://github.com/openclaw/openclaw/issues/136311) memory-core reindex 锁永不释放，索引不可修复，19GB 临时库堆积。
- [#143632](https://github.com/openclaw/openclaw/issues/143632) iMessage 消息重复投递 2-3 次且去重失效。
- [#143278](https://github.com/openclaw/openclaw/issues/143278) Heartbeat 内部输出泄漏到 Telegram 用户聊天。

**观察**：clawsweeper 机器人已对多数新 Bug 打上 `queueable-fix` / `fix-shape-clear` 标签形成修复队列，但 P0 类（WAL 膨胀、升级失败、计费冷却）尚无关联 fix PR。

---

## 6. 功能请求与路线图信号

- **移动端受保护接入是明确路线图方向**：Android/iOS Cloudflare Access 三大 XL PR 待合并（见第 3 节），预计下一版本落地，与 [#46058](https://github.com/openclaw/openclaw/issues/46058)（社区 Android fork 讨论 upstreaming）形成呼应。
- [#86881](https://github.com/openclaw/openclaw/issues/86881) ✅已关闭（stale）— Gateway-lite 无 AI 模式；关闭方式为 stale 而非拒绝，方向未定。
- [#51441](https://github.com/openclaw/openclaw/issues/51441) 暴露 resolved backend model — [#149344](https://github.com/openclaw/openclaw/pull/149344)（session model selection provenance）已部分响应，下版本可期。
- [#44309](https://github.com/openclaw/openclaw/issues/44309) A2A 单向 dispatch 模式 — 仍待产品决策。
- [#56692](https://github.com/openclaw/openclaw/issues/56692) 群聊多 agent 上下文归属 — 无对应 PR。

---

## 7. 用户反馈摘要

**痛点集中区**
- **可靠性**：长时运行部署（OOM、僵尸进程、WAL 膨胀）是自托管生产用户最大痛点，[#91588](https://github.com/openclaw/openclaw/issues/91588) 用户提供了详尽的 RSS 曲线。
- **消息丢失**：`no active tool authority snapshot` 一族错误在 9.2/9.4 用户中广泛出现，用户反馈“模型输出几分钟的回复被整段丢弃”体验极差。
- **升级路径**：[#123799](https://github.com/openclaw/openclaw/issues/123799) 生产用户（2026.5.12）请求安全升级/回移植指导未获回复；[#146637](https://github.com/openclaw/openclaw/issues/146637) npm 全局升级失败。
- **渠道体验**：Telegram/iMessage 的重复消息、进度条重复首段（[#116512](https://github.com/openclaw/openclaw/issues/116512)）、内部文本泄漏。

**正面信号**
- Issue 模板质量高（Bug type、beta-blocker 判定、环境信息完整）， clawsweeper 自动分诊（priority/impact/rating）被社区接受。
- #119720 中部分修复落地后用户积极更新进展，说明修复沟通渠道有效。

---

## 8. 待处理积压（维护者关注建议）

| Issue | 开放时长 | 状态 |
|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) 文本泄漏（P1+安全） | ~7 个月 | 40 评论，needs-security-review 未动 |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) Codex hook CPU（P0） | ~3 个月 | 无 fix PR |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) Gateway OOM | ~3 个月 | #149388/#149646 间接相关，需明确关联 |
| [#115367](https://github.com/openclaw/openclaw/issues/115367) ✅已关闭 — 读权限门禁与外部插件不兼容 | — | 关闭但设计矛盾值得复盘 |
| [#123799](https://github.com/openclaw/openclaw/issues/123799) 生产升级指导请求 | ~1 个月 | 完全无维护者响应 |
| [#115642](https://github.com/openclaw/openclaw/issues/115642) 计费冷却（P0，release-blocker） | ~7 周 | 无 fix PR |

**PR 积压**：341 个待合并 PR 中约 20+ 标注 "ready for maintainer look"，含多个 XL/compatibility 风险项，建议维护者优先排期评审，避免积压放大合并冲突。

---

*数据来源：openclaw/openclaw GitHub，2026-09-16 快照。*

---

## 横向生态对比

# 个人 AI 助手/智能体开源生态横向对比分析报告

**日期：2026-09-16 | 基于 12 个项目的社区动态快照**

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态已进入**“规模扩张后的稳定性收敛期””：头部项目（OpenClaw、Hermes Agent、Zeroclaw、NanoClaw、CoPaw）日均 Issue/PR 活动均达 50-100 条，但普遍呈现“PR 提交多于合并、修复多于新功能”的债务清偿特征。生态格局明显分化为三层：OpenClaw 作为事实标准占据核心生态位（LobsterAI 直接以 OpenClaw 兼容层方式构建产品）；NanoBot/NanoClaw/CoPaw 等快速迭代挑战者活跃度高；Moltis/ZeptoClaw/PicoClaw 等长尾项目处于低活跃维护状态。共性痛点高度趋同——**长会话上下文管理、消息投递可靠性、升级路径安全、多渠道（Telegram/Slack/WhatsApp/QQ/微信）接入质量**，表明这些问题是品类级挑战而非单项目缺陷。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500（新/活跃 338，关闭 162） | 500（待合并 341，合并/关闭 159） | 无（stable 2026.9.4） | 🟢 规模最大；⚠️ PR 积压 341、P0 无 fix PR |
| **Hermes Agent** | 50（35/15） | 50（47 待合并，仅 3 合并） | 无（v0.21.3） | 🟡 修 bug 期，审查吞吐是瓶颈 |
| **Zeroclaw** | 50（38/12） | 50（40 待合并） | 无 | 🟢 架构收敛期；⚠️ XL stacked PR 依赖链 |
| **NanoClaw** | 5（2/3） | 40（19/21） | 无 | 🟢 合并节奏健康、响应快 |
| **CoPaw** | 20（6/14） | 50（24/26） | 无（2.2.x 蓄力中） | 🟢 收敛效率高，关闭率 > 新开 2 倍 |
| **LobsterAI** | 3 | 30（20 合并） | Release 分支已合入 | 🟢 发布冲刺，单日修复 10+ 回归 |
| **NanoBot** | 3 | 20（10/10） | ✅ v0.3.5 | 🟢 高频发布、修复当日跟进 |
| **PicoClaw** | 2 | 4（3 待合并） | 无 | 🔴 主要贡献者单一、全员 stale |
| **Moltis** | 1 | 1（待合并） | 无 | 🔴 稳定但低活跃，7 月诉求无响应 |
| **ZeptoClaw** | 0 | 18（全 dependabot） | 无 | 🔴 纯自动化活跃，无人工推进 |
| **NullClaw / IronClaw / TinyClaw / EasyClaw** | 0 | 0 | 无 | ⚪ 无活动 |

---

## 3. OpenClaw 在生态中的定位

**优势：**
- **规模与品牌**：单日 1000 条 Issue/PR 活动，是第二梯队项目（Zeroclaw/Hermes）的 10 倍，社区贡献梯队和自动化分诊（clawsweeper 机器人）成熟。
- **生态虹吸效应**：LobsterAI（网易有道）以 OpenClaw 为运行时内核构建产品并跟进 2026.8.1 升级；NanoClaw 的 Codex 集成、Zeroclaw 的兼容性讨论均围绕其存在——事实上游标准。

**技术路线差异：**
- **OpenClaw**：全渠道消息型个人助手（Slack/iMessage/Telegram 优先），Gateway 集中式架构，痛点集中在 Gateway 资源治理与消息可靠性。
- **Zeroclaw**：Rust 技术栈，走 WASM 插件化 + 强安全边界（RPC peercred、egress 管控、emergency-stop RFC）路线，home-lab/自托管安全敏感用户为主。
- **Hermes Agent**：多 agent 编排（Kanban/Cron/fleet）+ Nous Portal 订阅计费，偏生产化多机部署。
- **NanoBot/NanoClaw/CoPaw**：轻量快速迭代，中国渠道（QQ/飞书/微信/POPO）覆盖深。

**对比短板**：OpenClaw 的 P0/P1 长尾（OOM 3 个月、文本泄漏 7 个月、计费冷却 7 周无 fix）在生态中最为突出；341 PR 积压远超同类的 40-47 条，反映规模带来的治理成本。

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **长会话上下文压缩** | OpenClaw（消息丢失回归族）、Hermes（#112482 压缩活锁）、Zeroclaw（PR #9535 锚定模型窗口）、LobsterAI（#2684 输出预算饿死、#2678 摘要格式） | 压缩不得丢工作成果、不得死锁、预算分配需可预期——5/12 项目同日相关活动，是品类第一痛点 |
| **升级/回滚事务可靠性** | NanoClaw（#3828 cutover 死锁、#3684 rollback 符号链接）、Hermes（安装/自更新 bug 族）、OpenClaw（#146637 npm 升级失败）、CoPaw（2.2.x MCP 回归）、LobsterAI（上游升级收口） | 静默成功比失败更可怕；自托管用户对 rollback 数据完整性要求极高 |
| **多 agent 间协作（A2A）** | OpenClaw（#44309 单向 dispatch）、Zeroclaw（A2ATool RFC accepted）、Hermes（fleet/Kanban）、NanoClaw（agent 间投递 #3813） | 从单助手向 agent 编排演进是共同路线 |
| **消息投递可靠性/去重** | OpenClaw（iMessage 重复 2-3 次）、Hermes（幽灵会话）、NanoBot（#4798 并发写截断）、NanoClaw（tools-only 投递 + 回执） | 渠道消息 exactly-once 是未解难题 |
| **插件生态与供应链安全** | OpenClaw（热重载内存泄漏）、Zeroclaw（WASM load-verify + OCI 插件仓库）、Hermes（插件目录机制）、CoPaw（插件目录 CDN 容错）、NanoBot（商业 provider 接入边界） | 插件化 + 安装时验证是共识方向 |
| **安全加固** | NanoBot（SSRF/邮件验证）、Zeroclaw（emergency-stop、RUSTSEC）、NanoClaw（Mattermost 认证）、CoPaw（HTTP 网关默认无鉴权）、PicoClaw（密钥静默丢失） | 渠道回调认证、出站 SSRF 管控成为标配需求 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Zeroclaw | Hermes Agent | NanoBot | NanoClaw | CoPaw | LobsterAI |
|---|---|---|---|---|---|---|---|
| **功能侧重** | 全渠道个人助手 | 安全优先的本地 agent | 多 agent 任务编排 | 跨端会话延续 | 语音/邮件渠道扩展 | Console + Hub 多租户 | 开箱即用桌面产品 |
| **目标用户** | 海外 IM 用户、自托管生产 | home-lab、安全敏感极客 | 单操作员/多机生产 | 个人跨端用户 | 自托管爱好者 | 中文社区、企业团队 | 非技术小白 |
| **架构** | Gateway 集中式 | Rust + WASM 插件 | Python + fleet/Kanban | Python + TUI/WebUI | 容器化 host | Python + Docker | Electron + OpenClaw 内核 |
| **独特信号** | 移动端 Cloudflare Access | computer-use RFC | 订阅计费生态 | 发布节奏最快 | OTel 可观测性 | Hub 用量看板 | OpenClaw 商业化封装验证 |

关键洞察：**LobsterAI 的存在证明了 OpenClaw 内核的产品化可行性**，也暴露上游升级对下游产品的传导风险（单日 10+ 兼容修复）。

---

## 6. 社区热度与成熟度分层

- **快速迭代扩张期**：**NanoBot**（v0.3.5 当日发布、当日修复跟进）、**NanoClaw**（语音/邮件/网关多线并进）、**CoPaw**（Hub 多租户蓄力、关闭率 2 倍于新开）。
- **规模庞大、质量巩固期**：**OpenClaw**（修 bug 为主、341 PR 积压）、**Hermes Agent**（47/50 PR 待合并、47 条审查瓶颈）、**Zeroclaw**（XL stacked PR 依赖链，从功能堆叠转向架构收敛）。
- **发布冲刺**：**LobsterAI**（Release/2026.9.15 分支已合入）。
- **低活跃维护期**：PicoClaw（贡献者单一 + stale）、Moltis（7 个月诉求无 triage）、ZeptoClaw（仅 dependabot 活动）、NullClaw/IronClaw/TinyClaw/EasyClaw（零活动，存在度存疑）。

成熟度悖论：活跃度最高的三个项目（OpenClaw/Hermes/Zeroclaw）恰恰积压最重，说明规模超过维护带宽是头部项目的共性问题。

---

## 7. 值得关注的趋势信号

1. **可靠性 > 功能成为竞争主线**：全生态今日无一项目发布“新能力型”大版本，头部项目活动几乎全部围绕内存治理、消息丢失、升级安全——用户已从“能做什么”转向“能不能一直做”。对开发者的启示：** Gateway 资源治理和投递语义（exactly-once/幂等）应作为一等架构公民设计，而非后期补丁**。

2. **静默失败是最大体验杀手**：NanoClaw #3338（10 分钟无响应）、Hermes（cron 静默跳过、Slack 状态静默消失）、NanoBot（Dream 死循环）反复被点名。趋势：心跳/进度事件契约、OTel 追踪（NanoClaw #3796）将从加分项变为必选项。

3. **安全边界工程化**：Zeroclaw 的 emergency-stop RFC、computer-use bounded approval、NanoBot 双安全修复、OpenClaw 移动端 Cloudflare Access——高危能力（桌面控制、文件系统、网络出口）配套硬边界是社区强共识，值得所有 agent 项目前置设计。

4. **渠道生态地域分化**：海外项目押注 Telegram/Slack/WhatsApp/邮件（Proton/AgentMail 双方案并行），中文项目深耕 QQ/微信/飞书/POPO；WhatsApp 官方风控（Zeroclaw #8627）提示**封闭渠道的接入风险应计入选型**，XMPP/自托管渠道需求上升是去平台依赖信号。

5. **插件商业化开始敲门**：NanoBot 的 aimlapi 50/50 分成提议、NanoClaw/CoPaw 的厂商主动接入（Keenable、AgentMail）——插件目录正成为商业分发入口，项目方需尽早明确商务边界与审查流程。

6. **OpenClaw 内核化**：LobsterAI 模式若成功，将开启“内核 + 发行版”分层生态；但下游单日消化 10+ 兼容修复的成本说明，**上游需要建立稳定的兼容性契约与 LTS 通道**（OpenClaw #123799 生产升级指导无人响应正是此缺口）。

---

*数据来源：各项目 2026-09-15 至 2026-09-16 GitHub 动态快照；本报告为横向分析，单日数据存在波动，建议结合多日趋势判断。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-09-16

## 1. 今日速览

NanoBot 今日发布 **v0.3.5** 正式版，核心亮点是将工作台带入终端并实现浏览器/终端/聊天应用间的无缝会话延续。过去 24 小时共 20 条 PR 更新（10 合并/关闭、10 待合并）、3 条 Issue 更新，发布节奏与修复吞吐保持高频，项目处于**高度活跃、快速迭代**状态。本周期合并 PR 覆盖安全加固（SSRF、邮件验证）、provider 修复、WebUI 体验优化等多个维度，显示出成熟的发布前置修复流程。

## 2. 版本发布

**[v0.3.5](https://github.com/HKUDS/nanobot/releases/tag/v0.3.5)**

- **核心更新**："one agent, more places to work" — 原生终端客户端 `nanobot` 与浏览器端 `nanobot webui` 使用同一 agent，跨端继续会话更顺畅。
- **打包改进**：配套 PR [#5787](https://github.com/HKUDS/nanobot/pull/5787) 将原生 TUI 打包进五个平台 wheel，用户安装后无需首跑下载 GitHub 资产或另装 Bun。
- **迁移注意**：无明确破坏性变更；但注意 `dream.maxIterations` 被标记 deprecated（见下文 Bug 部分），依赖该配置的用户升级后行为可能变化。

## 3. 项目进展（已合并/关闭 PR）

- **[#5787](https://github.com/HKUDS/nanobot/pull/5787) build: 原生 TUI 打包进平台 wheel** — 显著改善首次安装体验，是 v0.3.5 的关键基础设施。
- **[#5783](https://github.com/HKUDS/nanobot/pull/5783) fix(providers): 保留含 tool_calls 的 assistant content** — 修复历史消息被错误剥离导致的多轮工具调用回归，兼容 Mistral 等 provider。
- **[#5775](https://github.com/HKUDS/nanobot/pull/5775) fix(tools): read_file 去重限定到模型上下文** — 修复压缩/裁剪上下文后 read_file 返回 stub 的问题。
- **[#5778](https://github.com/HKUDS/nanobot/pull/5778) fix(email): 强制可信认证结果** — 收紧入站邮件发件人验证，安全加固。
- **[#5697](https://github.com/HKUDS/nanobot/pull/5697) fix(qq): 防范入站附件下载 SSRF** — URL 校验、禁重定向、仅接受 HTTP 200，安全修复。
- **[#5782](https://github.com/HKUDS/nanobot/pull/5782) fix(dream): 强制配置的迭代上限** — 响应 Issue #5781 的修复（已关闭但对应 Issue 仍 OPEN，需确认是否合并入版）。
- **[#5768](https://github.com/HKUDS/nanobot/pull/5768) fix(feishu): QR 登录用 /page/cli 验证 URL**（p1）— 修复 v0.3.0 起飞书扫码登录必然失效的阻断性 Bug。
- **[#5757](https://github.com/HKUDS/nanobot/pull/5757) fix(session): 搜索历史会话更早分页**、**[#5786](https://github.com/HKUDS/nanobot/pull/5786) WebUI 分段控件动画重构**、**[#5785](https://github.com/HKUDS/nanobot/pull/5785) 发布准备**。

整体评估：一个发布周期内完成 2 项安全修复、多项 p1/p2 修复与体验打磨，前进幅度可观。

## 4. 社区热点

- **[#5781](https://github.com/HKUDS/nanobot/issues/5781) Dream 任务死循环（3 评论）**：定时 Dream 整合运行 25–111 分钟、最多 200 次工具调用，反复重读相同文件；`dream.maxIterations` 已被标记 deprecated 且被忽略。**诉求**：后台自动化任务的资源可控性与配置可预期性。
- **[#5788](https://github.com/HKUDS/nanobot/issues/5788) v0.3.5 发布庆祝帖**：社区对新版本情绪积极。
- **[#5666](https://github.com/HKUDS/nanobot/pull/5666) aimlapi.com 提供商接入 PR**：商业方主动接入并提出 50/50 分成合作，反映项目对 provider 生态的吸引力，但也考验维护者的商务/审核边界。

## 5. Bug 与稳定性

| 严重度 | 问题 | 状态 |
|---|---|---|
| 高 | [#5781](https://github.com/HKUDS/nanobot/issues/5781) Dream 死循环，配置失效，资源大量浪费 | 已有 fix PR [#5782](https://github.com/HKUDS/nanobot/pull/5782)（独立上限默认 15） |
| 中 | [#5784](https://github.com/HKUDS/nanobot/issues/5784) QQ 渠道压缩通知作为普通消息刷屏 | 已有 fix PR [#5780](https://github.com/HKUDS/nanobot/pull/5780)（待合并） |
| 中 | [#4798] 并发会话文件写截断/丢失（待合并） | PR [#5779](https://github.com/HKUDS/nanobot/pull/5779) |
| 中 | [#5747] 批量边界间进程退出导致工具进度丢失 | PR [#5748](https://github.com/HKUDS/nanobot/pull/5748)（待合并） |
| 低 | [#5770] 手机端抽屉焦点抢占 | PR [#5777](https://github.com/HKUDS/nanobot/pull/5777)（待合并） |

## 6. 功能请求与路线图信号

- **copy_file / move_file 文件系统工具**（[#5626](https://github.com/HKUDS/nanobot/pull/5626)）：补齐文件原语，避免模型 read→write 链式操作；与 Dream 循环问题（反复读写文件）相关联，很可能进下一版本（目前 conflict 需解冲突）。
- **签名直投 Webhook**（[#5652](https://github.com/HKUDS/nanobot/pull/5652)）：面向 CI/监控/账单的确定性通知通道，跳过 agent 循环，是企业场景刚需信号。
- **Provider 选择器搜索**（[#5776](https://github.com/HKUDS/nanobot/pull/5776)）与**稳定工具调用上下文 API**（[#5750](https://github.com/HKUDS/nanobot/pull/5750)）：均为 p2，方向明确。
- Dream 迭代上限修复（#5782）若未进 v0.3.5，将是 v0.3.6 首要候选。

## 7. 用户反馈摘要

- **痛点 1 — 后台任务失控**（#5781）：自托管用户观察到 Dream 整合长时间空转、重复读同一文件，对 token/算力成本敏感。
- **痛点 2 — 生命周期通知噪音**（#5784、#5780）：“Compressing context…” 等系统提示直接推给终端用户，自托管 QQ 用户认为体验粗糙，与 #5719 同类问题，属于系统性 UX 债。
- **满意点**：跨端会话延续（终端/WebUI/聊天应用）是明确受期待的能力；社区对新版本响应迅速、修复 PR 当日跟进，用户信任度较高。

## 8. 待处理积压

- **[#5652](https://github.com/HKUDS/nanobot/pull/5652) 签名 Webhook**（9-04 开启，带 conflict/security 标签）：跨 12 天待审，建议维护者优先评审。
- **[#5666](https://github.com/HKUDS/nanobot/pull/5666) aimlapi 接入**（9-04 开启）：涉及商业合作与安全审查，需明确接受/拒绝立场，避免社区观望。
- **[#5626](https://github.com/HKUDS/nanobot/pull/5626) copy/move_file**（9-01 开启，15 天）：功能价值高但存在 conflict，建议尽快 rebase。
- **Issue #5781**：fix PR 已关闭，但 Issue 仍 OPEN，需验证修复是否已随 v0.3.5 发布，并回复用户。

---
*数据来源：GitHub HKUDS/nanobot，统计窗口 2026-09-15 至 2026-09-16。*

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报 — 2026-09-16

## 1. 今日速览

Zeroclaw 今日保持高活跃度：过去 24 小时共有 50 条 Issue 更新（新开/活跃 38，关闭 12）和 50 条 PR 更新（待合并 40，已合并/关闭 10），无新版本发布。讨论焦点集中在 **Anthropic 多模态/图像处理的一连串 bug**（单日新增 4+ 个相关 issue）以及 **安全与架构类 RFC 的持续推进**。社区多位核心贡献者（@JordanTheJet、@Audacity88、@vrurg）均有大型 PR 更新，项目处于“功能并行推进、待合并体量较大”的阶段。

## 2. 版本发布

今日无新版本发布。最新代码仍停留在上一 Release，大量已 accepted 的 RFC 与 stacked PR 待合并，推测在为下一个版本累积变更。

## 3. 项目进展

今日 PR 侧更新 50 条，其中 10 条已合并/关闭，主要进展：

- **CI 效率优化落地推进**：[#10874](https://github.com/zeroclaw-labs/zeroclaw/pull/10874) 解决所有 Quality Gate 任务排队等待 `fmt` 作业的问题（曾因 runner 短缺等待 70 分钟），配套的 [#10896](https://github.com/zeroclaw-labs/zeroclaw/pull/10896)（今日新开）进一步固定编译作业的 runner 标签。CI 吞吐量显著改善。
- **WASM 插件体系强化**：三个连续 PR 持续推进——[#10746](https://github.com/zeroclaw-labs/zeroclaw/pull/10746)（安装时对插件做 load-verify）、[#10752](https://github.com/zeroclaw-labs/zeroclaw/pull/10752)（`plugin list --verify` 报告真实加载状态）、[#10750](https://github.com/zeroclaw-labs/zeroclaw/pull/10750)（channel 插件 egress 管控）。配合 [#8850](https://github.com/zeroclaw-labs/zeroclaw/issues/8850)（feature flags → 运行时插件迁移），插件化路线图正稳步兑现。
- **安全/RPC 体系堆叠推进**：[#10259](https://github.com/zeroclaw-labs/zeroclaw/pull/10259)（RPC 认证 principal + peercred，#8289 stage 3）与 [#10824](https://github.com/zeroclaw-labs/zeroclaw/pull/10824)（config/set-many 按路径 selector 门控）形成安全堆叠链，认证授权模型逐步成形。
- **Zerocode 收尾类工作**：[#10120](https://github.com/zeroclaw-labs/zeroclaw/pull/10120)（移除不可达 TUI 代码）、[#9876](https://github.com/zeroclaw-labs/zeroclaw/pull/9876)（OSC 终端标题/进度上报，已关闭）等持续打磨 CLI 体验。

总体看，今日为“清扫与堆叠”日：CI 债务清理 + 插件/安全主线纵深推进，无破坏性变更落地。

## 4. 社区热点

**最活跃讨论：**

1. **[#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) — RFC：Computer-use 桌面屏幕交互与输入控制**（16 评论）。维护者已接管并发布 Revision 2，明确 bounded approval units、执行时重验证、session arming、sidecar 信任模型等安全边界。诉求：让 agent 安全地操作桌面 GUI，但社区对高风险能力的安全框架反复打磨。
2. **[#9106](https://github.com/zeroclaw-labs/zeroclaw/issues/9106) — RFC：A2A 出站客户端（A2ATool）**（11 评论）。A2AServer 已随 v0.8.2 发布，出站能力是补齐 agent 间协作的最后一块拼图，状态已 accepted。
3. **[#9346](https://github.com/zeroclaw-labs/zeroclaw/issues/9346) — 统一 package/capability/config/runtime-state 目录契约**（9 评论）。整合 integrations、built-ins、可安装插件的统一产品级目录，是插件生态的关键架构决策。
4. **[#8583](https://github.com/zeroclaw-labs/zeroclaw/issues/8583) — channel/source 共享边界清理 Tracker**（6 评论），新 channel 开发须复用统一的生命周期/schema/信任/配置层。

**热点信号**：讨论高度集中在**安全边界**（emergency-stop、egress 管控、硬件能力门控）与**插件/目录生态**两条主线上，显示项目正从“功能堆叠”转向“架构收敛”。

## 5. Bug 与稳定性

按严重程度排列（今日报告/活跃）：

**S1（工作流阻断）：**
- [#8627](https://github.com/zeroclaw-labs/zeroclaw/issues/8627) WhatsApp Web 设备 linking 被 WhatsApp 新的 passkey/SHORTCAKE 门控破坏，**长期无修复，P1**，影响所有 Web 模式用户。
- [#10659](https://github.com/zeroclaw-labs/zeroclaw/issues/10659) 预算超限的 Code turn 在 session restore 后丢失可见进度，ZeroCode TUI 体验阻断。

**P1 安全：**
- [#5869](https://github.com/zeroclaw-labs/zeroclaw/issues/5869) rumqttc v0.25.1 钉住旧版 rustls-webpki/pemfile，触发 4 条 RUSTSEC 通告集群，**blocked 状态**。
- [#9882](https://github.com/zeroclaw-labs/zeroclaw/issues/9882) 图像 marker 绕过 `run_model_query` 直连路径的内容校验（in-progress）。
- [#9802](https://github.com/zeroclaw-labs/zeroclaw/issues/9802) emergency-stop 对在途操作与网络出口的完整强制（blocked）。

**S2（今日新增，Anthropic 多模态集中爆发）：**
- [#10885](https://github.com/zeroclaw-labs/zeroclaw/issues/10885) tool 返回的图像在同一 turn 内因无关 tool call 而消失（今日新开）。
- [#10888](https://github.com/zeroclaw-labs/zeroclaw/issues/10888)（已关闭）stale tool-result 图像剥离导致 cache prefix 失效，是 #10778 的姊妹机制。
- [#10889](https://github.com/zeroclaw-labs/zeroclaw/issues/10889)（今日新开）最后消息以 image block 结尾时滚动 cache 断点丢失。
- [#10887](https://github.com/zeroclaw-labs/zeroclaw/issues/10887)（今日新开）非视觉模型对“marker 形状文本”硬性失败，导致整 turn 丢失。
- 修复 PR 方向已有 [#10480](https://github.com/zeroclaw-labs/zeroclaw/pull/10480)（从被拒图像请求中恢复），覆盖部分上述场景。

**测试/CI 稳定性：**
- [#10883](https://github.com/zeroclaw-labs/zeroclaw/issues/10883)（今日新开，P1）Telegram media-group 测试在并行 CI 中超时。
- [#10272](https://github.com/zeroclaw-labs/zeroclaw/pull/10272)（已关闭）Hailo 日志断言在并行测试下的非确定性失败。

**观察**：Anthropic provider 的图像/缓存路径是当前 bug 密度最高的区域，一日内 4 个新 issue，值得专项治理。

## 6. 功能请求与路线图信号

已 accepted 且有对应 PR 在途、大概率进入下一版本：

- **A2A 出站客户端**（[#9106](https://github.com/zeroclaw-labs/zeroclaw/issues/9106)）——入站已发布，出站是明确下一步。
- **运行时插件迁移**（[#8850](https://github.com/zeroclaw-labs/zeroclaw/issues/8850)）+ 插件安装验证三连 PR（#10746/#10750/#10752）——插件生态接近可用。
- **Anthropic OAuth 存储配置**（[#9464](https://github.com/zeroclaw-labs/zeroclaw/issues/9464) ↔ PR [#9420](https://github.com/zeroclaw-labs/zeroclaw/pull/9420)）——契约文档与实现同步推进，needs-author-action 中。
- **流式回复默认开启**（[#10166](https://github.com/zeroclaw-labs/zeroclaw/issues/10166)，`stream_mode` 默认 `off` → `partial`）——accepted，属体验级改进，落地成本低。
- **上下文压缩锚定模型窗口比例**（PR [#9535](https://github.com/zeroclaw-labs/zeroclaw/pull/9535)）与 **web_research 委托工具**（PR [#9833](https://github.com/zeroclaw-labs/zeroclaw/pull/9833)）均为大型已审查变更。

仍在讨论/优先级较低：
- **OCI 插件仓库**（[#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497)，blocked/P3）——cosign 供应链验证的愿景好，但排序靠后。
- **硬件 WASI host functions**（[#8187](https://github.com/zeroclaw-labs/zeroclaw/issues/8187)）、**原生 XMPP channel**（[#9814](https://github.com/zeroclaw-labs/zeroclaw/issues/9814)）——面向 home-lab/边缘场景的差异化需求。

## 7. 用户反馈摘要

- **多模态体验痛点突出**：图像在长 turn 中“时有时无”（#10885）、上下文预算计对图像严重低估后飙超 100%（#9332）、缓存频繁失效导致成本上升（#10888/#10889）——重度使用图像工具的用户最受影响。
- **自托管/home-lab 用户群体活跃**：XMPP/Prosody（#9814）、GPIO/SPI 硬件访问（#8187）、WhatsApp Web 被官方风控阻断（#8627）等需求均来自希望摆脱大平台依赖的用户。
- **安全意识强的社区氛围**：用户主动报告 RUSTSEC 依赖集群（#5869）、要求 emergency-stop 覆盖网络出口（#9802），社区对"agent 高危能力须有硬边界"有强烈共识。
- **体验细节诉求**：开箱即流式输出（#10166）、ZeroCode 中可展开查看 subagent 活动与完整工具结果（#8763）、按类别共享兄弟 agent 记忆（#8983，已关闭但方向被认可）。

## 8. 待处理积压

提醒维护者关注：

| 项目 | 问题 | 链接 |
|---|---|---|
| WhatsApp linking 破损 | P1/S1，7 月报告，依赖上游（wa-rs/WhatsApp 协议），长期无进展 | [#8627](https://github.com/zeroclaw-labs/zeroclaw/issues/8627) |
| rumqttc RUSTSEC 集群 | P1 安全，blocked 于上游发版，建议跟踪临时缓解 | [#5869](https://github.com/zeroclaw-labs/zeroclaw/issues/5869) |
| Emergency-stop 完整强制 | P1 RFC，blocked，是安全承诺的关键缺口 | [#9802](https://github.com/zeroclaw-labs/zeroclaw/issues/9802) |
| PostgreSQL CI 服务容器 | accepted 但 blocked，session backend 缺真实 DB 测试覆盖 | [#9318](https://github.com/zeroclaw-labs/zeroclaw/issues/9318) |
| 超大 PR 积压 | 40 个待合并 PR 中多个 size:XL（#9420、#9535、#10259、#10407 等），部分标记 needs-author-action/needs-maintainer-review，合并吞吐可能成为瓶颈 | 见 PR 列表 |

**健康度小结**：Issue 关闭率（12/50）与 PR 合并节奏（10/50）相对均衡，社区贡献者梯队（distinguished/principal/trusted contributor 标签体系）运转良好。主要风险为 Anthropic 多模态路径的 bug 密集区与 XL 级 stacked PR 的合并依赖链。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 · 2026-09-16

## 1. 今日速览

Hermes Agent 今日保持高活跃度：过去 24 小时共 **50 条 Issue 更新**（新开/活跃 35，关闭 15）和 **50 条 PR 更新**（待合并 47，合并/关闭 3）。项目当前处于**修 bug 为主、版本打磨期**——今日无新版本发布，社区贡献以稳定性修复、安装/更新链路修补和文档补全为主。Kanban/Cron 调度器相关缺陷依然是 Issue 聚集最多的领域，值得维护者优先关注。桌面端（Desktop/TUI）的新报告也明显增多，显示用户群正在向图形化使用场景扩展。

## 2. 版本发布

今日无新版本发布（上一版本为 v0.21.3，2026.9.11 前后发布）。

## 3. 项目进展

今日合并/关闭的 PR 仅 3 条，主要关闭项包括：

- [PR #102256](https://github.com/NousResearch/hermes-agent/pull/102256)（CLOSED）`fix(web): decode keyless MCP responses as UTF-8 when no charset declared` — 修复 `mcp_call` 在 CJK/emoji 等非 ASCII 页面上的解析崩溃，属于中文用户体感明显的修复。
- 其余 47 条 PR 处于待合并状态，其中贡献者 @33hodl 今日集中提交了**三条 CLI 文档补全 PR**（[#112553](https://github.com/NousResearch/hermes-agent/pull/112553) update 的 12 个 flag、[#112555](https://github.com/NousResearch/hermes-agent/pull/112555) sessions 的 5 个子命令、[#112556](https://github.com/NousResearch/hermes-agent/pull/112556) skills 的 5 个子命令），文档与实现差距正在系统性收窄。
- 新提交的功能性 PR 值得关注：[#112488](https://github.com/NousResearch/hermes-agent/pull/112488) 将社区插件 **hermes-filebox**（Desktop 文件浏览器，含拖拽、缩略图、3D 模型预览）提交至插件目录；[#111861](https://github.com/NousResearch/hermes-agent/pull/111861)（P1）修复 checkpoint 安全恢复的 ledger 键不匹配问题。

整体看，今日主线推进有限（合并量低），但待合并管道充裕，下一版本预计将消化大量 P1/P2 修复。

## 4. 社区热点

1. **[Issue #87093](https://github.com/NousResearch/hermes-agent/issues/87093)**（CLOSED，28 评论）Debian 安装链路损坏（uv.lock & npm install 失败），P0 级安装阻断问题，持续一个月后于今日关闭——安装可靠性始终是用户第一触点，社区讨论热烈。
2. **[Issue #68592](https://github.com/NousResearch/hermes-agent/issues/68592)**（OPEN，15 评论）Cron agent 未设置 `HERMES_KANBAN_TASK` 却被注入 Kanban 协议导致报错，反映调度协议注入逻辑需要按上下文精确裁剪。
3. **[Issue #110912](https://github.com/NousResearch/hermes-agent/issues/110912)**（CLOSED，14 评论）Nous Portal 订阅额度用尽后部分模型路由（glm-flash/kimi）按原价计费，疑似折扣路由 bug。计费透明度问题是付费用户的核心诉求。
4. **[Issue #112482](https://github.com/NousResearch/hermes-agent/issues/112482)**（OPEN，今日新开，3 评论）大 session（~200K+ tokens）下上下文压缩**活锁**：no-op 条目持续挤掉已完成的工作候选，压缩永远无法落地。属今日最有价值的新报告。
5. **[Issue #110374](https://github.com/NousResearch/hermes-agent/issues/110374)**（OPEN，4 👍）slack-sdk ≥ 3.44 后状态指示静默失效，依赖兼容性问题的典型代表。

## 5. Bug 与稳定性

按严重程度排列（今日新增/活跃）：

| 级别 | Issue | 摘要 | Fix 状态 |
|---|---|---|---|
| P0 | [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) | Debian 安装损坏 | 已关闭，视为已修复 |
| P1 | [#112482](https://github.com/NousResearch/hermes-agent/issues/112482) | 压缩活锁，大 session 无法收敛 | 无 fix PR |
| P1 | [#111414](https://github.com/NousResearch/hermes-agent/issues/111414) | Cron 定时触发被静默跳过，无错误记录（已关闭） | 已关闭 |
| P1 | [#85957](https://github.com/NousResearch/hermes-agent/issues/85957) | api_server 路径下 delegate 完成事件在父会话结束后以用户轮次自 POST（已关闭） | 已关闭 |
| P2 | [#111999](https://github.com/NousResearch/hermes-agent/issues/111999) | 网络错误恢复产生 source=unknown 幽灵会话（已关闭） | 已关闭 |
| P2 | [#111417](https://github.com/NousResearch/hermes-agent/issues/111417) | uv.lock 过期致 SQLite 漏洞运行时无法被 update 修复（已关闭） | 已关闭 |
| P2 | [#111689](https://github.com/NousResearch/hermes-agent/issues/111689) | macOS launchd 下 update 后 dashboard 端口冲突死循环（已关闭） | 已关闭 |
| P2 | [#112534](https://github.com/NousResearch/hermes-agent/issues/112534) | `probe_api_models` 在裸数组 /models 响应上崩溃（已关闭） | 已关闭 |
| P2 | [#112501](https://github.com/NousResearch/hermes-agent/issues/112501) | Desktop steer 消息与进行中回复渲染顺序错乱 | 无 fix PR |
| P2 | [#112135](https://github.com/NousResearch/hermes-agent/issues/112135) | opencode-go 拒绝 tool-result 消息上的 "name" 字段（HTTP 400） | 无 fix PR |
| P2 | [#73997](https://github.com/NousResearch/hermes-agent/issues/73997) | `hermes mcp login` 重试自撞固定 redirect_port，掩盖真实认证错误；关联 [PR #112569](https://github.com/NousResearch/hermes-agent/pull/112569) 修复同类缓存 OAuth 崩溃 | 部分 fix 在途 |
| P2 | [#93827](https://github.com/NousResearch/hermes-agent/issues/93827) | Desktop 并发会话切换后模型问题选项不显示 | 无 fix PR |
| P3 | [#111719](https://github.com/NousResearch/hermes-agent/issues/111719) | 零 bot 配置下每分钟 2 次投递轮询告警（91.5% 的 WARNING 日志，已关闭） | 已关闭 |
| P3 | [#111698](https://github.com/NousResearch/hermes-agent/issues/111698) | pip wheel 缺失 whatsapp-bridge 脚本（已关闭） | 已关闭 |

**今日 15 条 Issue 关闭中约半数为 9/15–9/16 两日内快速处置**，响应速度良好；但多中心会话状态（session-state）类 bug 反复出现，提示该子系统需要系统性加固。

## 6. 功能请求与路线图信号

- **插件生态扩张**：[#112488](https://github.com/NousResearch/hermes-agent/pull/112488)（hermes-filebox）表明插件目录机制运转正常，Desktop 插件（尤其文件管理/预览类）是活跃需求方向。
- **CLI 文档体系化**：@33hodl 的三条文档 PR 显示项目正在为下个版本前的“文档对齐实现”做准备，可能预示一次面向易用性的版本。
- **Fleet/多机管理**：[#112467](https://github.com/NousResearch/hermes-agent/pull/112467)（fleet systemd scope 校验）与 [#87283](https://github.com/NousResearch/hermes-agent/issues/87283)（Kanban 插件未声明 gateway 依赖、auto-dispatch 需 opt-in）共同指向：**自动化行为（Kanban dispatcher、fleet）的显式声明与用户可控性**是下一阶段的重要信号，[#87283] 的“未声明即自动派发”诉求很可能被纳入。
- **上下文工程**：#112482 压缩活锁 + PR #109599 静默标记处理，说明大规模 session 的上下文压缩管道是持续投入领域。

## 7. 用户反馈摘要

- **痛点集中区**：① 安装与自更新链路（Debian/Windows/macOS/WSL 各有专属 bug，是 Issue 最高的类别之一）；② Kanban worker 退出码语义混乱——`rc=0` 被误判为 `protocol_violation`，多个独立用户（[#44812](https://github.com/NousResearch/hermes-agent/issues/44812) 270 事件/160 阻塞任务的生产数据、[#91177](https://github.com/NousResearch/hermes-agent/issues/91177)、[#80456](https://github.com/NousResearch/hermes-agent/issues/80456)）反复撞墙；③ 计费透明度（#110912 费用 3 倍跳涨）。
- **典型使用场景**：多 profile 生产化部署（10+ claimer 主机）、Telegram/Slack/WhatsApp 单操作员客服 copilot（#68911 需要透传 E.164 号码）、macOS launchd / systemd 常驻服务。
- **满意点**：维护者对高优先级新报告的关闭速度较快（#112534、#111719 当日/次日关闭）；社区贡献者（@33hodl 等）产出质量高、覆盖面广。
- **不满意点**：静默失败类 bug（cron 不触发、Slack 状态静默消失）缺乏可观测性，用户只能靠日志挖掘；部分 fix 不彻底（#77394：#73684 的修复未覆盖 respawned gateway 场景）。

## 8. 待处理积压

以下高价值 Issue 长期 OPEN，建议维护者优先跟进：

- **[#77394](https://github.com/NousResearch/hermes-agent/issues/77394)**（8/3 起）Windows 更新仍失败，已有修复不覆盖 respawned gateway — Windows 用户持续受阻 6 周。
- **[#68911](https://github.com/NousResearch/hermes-agent/issues/68911)**（7/21 起）Gateway 强制脱敏 E.164 号码，无 trusted-profile 例外，阻断客服类场景。
- **[#80280](https://github.com/NousResearch/hermes-agent/issues/80280)**（8/6 起）Kanban 超时 worker 进程组残留，新旧进程并发修改同一 worktree——**存在数据一致性风险**。
- **[#81437](https://github.com/NousResearch/hermes-agent/issues/81437)** + [#41805](https://github.com/NousResearch/hermes-agent/issues/41805)（6/8 起）：quota 墙 + 误分类组合导致任务**永久阻塞**与事件日志无限增长，已积压 3 个月。
- **[#73997](https://github.com/NousResearch/hermes-agent/issues/73997)**（7/29 起）MCP login 重试端口自撞，掩盖真实认证错误。
- PR 积压方面，@33hodl 的系列修复（[#89008](https://github.com/NousResearch/hermes-agent/pull/89008)、[#89009](https://github.com/NousResearch/hermes-agent/pull/89009)、[#100332](https://github.com/NousResearch/hermes-agent/pull/100332)、[#111861](https://github.com/NousResearch/hermes-agent/pull/111861) 等）待审时间已近一个月，**47 条待合并 PR 的审查吞吐是当前项目最大的流程瓶颈**。

---
*数据来源：GitHub（过去 24 小时）；链接均指向 NousResearch/hermes-agent。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报
**日期：2026-09-16 | 仓库：[sipeed/picoclaw](https://github.com/sipeed/picoclaw)**

---

## 1. 今日速览

- 过去 24 小时项目整体活跃度**中等偏低**：2 条 Issue 更新（均为已有 Issue 的活跃，无新增）、4 条 PR 更新（3 待合并、1 已关闭），**无新版本发布**。
- 活跃贡献仍集中在核心贡献者 [@sting8k](https://github.com/sting8k) 身上，其提交的 config 安全性相关 Bug 与修复 PR（#3373、#3374、#3375、#3372）是当前主要工作线，但多项均处于 `[stale]` 状态，合并进度受阻。
- 值得关注的是，关闭了一个挂起近半年的 QQ 渠道稳定性增强 PR（#1780），渠道生态方向的社区贡献未能落地。
- 无新 Bug 报告、无崩溃类反馈，整体稳定性无恶化信号。

---

## 2. 版本发布

过去 24 小时**无新版本发布**，最新 Releases 列表为空。无迁移或破坏性变更需要关注。

---

## 3. 项目进展

**已关闭：**
- [PR #1780](https://github.com/sipeed/picoclaw/pull/1780) `Qq connection stability`（作者 @xiang33，创建于 2026-03-19）— 该 PR 旨在使 QQ 渠道的重连间隔、重试次数、速率限制等参数可通过配置文件或环境变量自定义并保持向后兼容。挂起近 6 个月后被**关闭（未合并）**，意味着 QQ 渠道稳定性配置化的社区贡献未能进入主线，相关需求仍待官方实现。

**待合并（3 条）：**
- [PR #3375](https://github.com/sipeed/picoclaw/pull/3375) — 修复敏感数据缓存并发初始化的竞态问题（对应 Issue #3374）。
- [PR #3372](https://github.com/sipeed/picoclaw/pull/3372) — 使 `reaction` 工具可配置化，补齐 `ToolsConfig` 缺失的 `reaction` 字段。
- [PR #3370](https://github.com/sipeed/picoclaw/pull/3370) — 新增 Keenable 无 API Key 网页搜索提供商（来自外部企业贡献者 @ilya-bogin-keenable）。

**总体评估：** 今日无代码合并进入主线，项目推进停滞于 review 阶段，进展有限。

---

## 4. 社区热点

今日无高评论量新讨论，活跃点集中在已有条目的 stale 标记更新：

- [Issue #3374](https://github.com/sipeed/picoclaw/issues/3374)（👍 0，评论 1）— 敏感数据缓存数据竞态。诉求：核心配置模块的并发安全加固，直接影响日志脱敏功能可靠性。
- [Issue #3373](https://github.com/sipeed/picoclaw/issues/3373)（👍 0，评论 1）— `SaveConfig` 静默丢失多 api_key。诉求：**配置持久化的数据完整性**，属于“静默数据丢失”级别的高风险问题。
- [PR #3370](https://github.com/sipeed/picoclaw/pull/3370) — Keenable 搜索提供商集成，反映社区对**开箱即用（零 API Key）工具生态**的持续兴趣。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | Fix PR |
|---|---|---|---|
| 🔴 高 | [#3373](https://github.com/sipeed/picoclaw/issues/3373) | `LoadConfig → SaveConfig` 往返后，`model_list` 中第一个之后的所有 `api_keys` 被静默删除，且残留指向不存在模型的 `fallbacks` 引用——**用户 API 密钥静默丢失** | ❌ 暂无对应修复 PR |
| 🟠 中高 | [#3374](https://github.com/sipeed/picoclaw/issues/3374) | `Config.initSensitiveCache` 懒初始化无同步，`sync.Once` 形同虚设；并发场景下可返回 nil replacer 导致 `FilterSensitiveData` panic | ✅ [PR #3375](https://github.com/sipeed/picoclaw/pull/3375)（待合并） |

**提醒：** #3373 涉及用户密钥数据丢失，尚无修复 PR，建议维护者优先跟进。

---

## 6. 功能请求与路线图信号

- **Keenable 搜索提供商**（[PR #3370](https://github.com/sipeed/picoclaw/pull/3370)）：零配置即可启用的 web_search 提供商，符合项目“降低使用门槛”的方向，若 review 通过有望进入下一版本。
- **reaction 工具可配置化**（[PR #3372](https://github.com/sipeed/picoclaw/pull/3372)）：补齐工具开关体系的一致性缺口，属低风险增强，纳入可能性较高。
- **QQ 渠道连接参数可配置**：随 #1780 关闭，该需求退回待办状态，是否由官方接手值得关注。

---

## 7. 用户反馈摘要

从现有 Issue/PR 可提炼的痛点：

- **多密钥配置不可靠**：配置多把 API Key 的用户在保存后密钥静默丢失（#3373），影响多供应商故障切换场景，是最直接的用户痛点。
- **并发场景稳定性**：高并发下敏感数据脱敏 panic（#3374），影响生产环境日志安全能力。
- **工具配置粒度不足**：`reaction` 等工具无法通过配置关闭（#3372），用户希望对 Agent 工具集有更精细的控制。
- **搜索工具接入门槛**：外部贡献者积极接入免 Key 搜索服务（#3370），反映用户希望减少第三方 API 依赖。

---

## 8. 待处理积压

以下条目均已被标记 `[stale]` 且今日仍处于开放状态，提醒维护者关注：

- [Issue #3374](https://github.com/sipeed/picoclaw/issues/3374) — 数据竞态 Bug，**已有修复 PR #3375 待 review**，建议尽快合并闭环。
- [Issue #3373](https://github.com/sipeed/picoclaw/issues/3373) — API 密钥静默丢失，**尚无修复 PR**，优先级建议最高。
- [PR #3375](https://github.com/sipeed/picoclaw/pull/3375)、[PR #3372](https://github.com/sipeod/picoclaw/pull/3372)（正确链接：[sipeed/picoclaw#3372](https://github.com/sipeed/picoclaw/pull/3372)）、[PR #3370](https://github.com/sipeed/picoclaw/pull/3370) — 三条 PR 均处于 stale + 待合并状态，其中 #3370 由外部企业贡献者提交，长期搁置可能挫伤社区贡献积极性。
- **趋势警示：** 当前主要贡献者单一（@sting8k），且其修复工作全部停滞在 review 阶段，建议维护团队提升 review 吞吐以维持项目健康度。

---

*数据来源：GitHub API（过去 24 小时窗口）。本报告由自动化分析生成，链接均指向对应 Issue/PR 页面。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-09-16

## 1. 今日速览

过去 24 小时 NanoClaw 保持高活跃度：共 40 条 PR 更新（19 待合并 / 21 已合并或关闭）与 5 条 Issue 更新（2 新开或活跃 / 3 关闭），无新版本发布。开发重心集中在**性能优化（host 会话并发、跨会话 fan）、渠道安全（Mattermost 认证）和 provider 生态扩展（Iron 网关、语音渠道）**。Issue 侧新增两个 `/update-nanoclaw` 相关缺陷（#3684、#3828），暴露出更新/回滚事务链路仍有可靠性短板。整体看，项目处于快速迭代期，合并节奏健康，核心团队（@glifocat、@gavrielc、@zvi-fried 等）响应迅速。

## 2. 版本发布

无新版本发布。无迁移事项。

## 3. 项目进展

今日已合并/关闭的 21 个 PR 中，重点包括：

- **性能与稳定性**
  - [#3829](https://github.com/nanocoai/nanoclaw/pull/3829) `perf(cross-session-context)`：将跨会话 echo fan 移出唤醒关键路径并限定在热集，唤醒延迟不再随兄弟会话数线性增长。
  - [#3830](https://github.com/nanocoai/nanoclaw/pull/3830) `test(webhook)`：改为内核分配空闲端口，消除 `EADDRINUSE` 测试抖动。
  - [#3832](https://github.com/nanocoai/nanoclaw/pull/3832)（仍开放）`perf(host)`：会话 reconcile 与 drain 并发化、投递轮询改固定频率——若合并，host tick 时间将不再随 会话数 × 邮箱延迟 放大。

- **Provider 契约体系**
  - [#3826](https://github.com/nanocoai/nanoclaw/pull/3826)：providers 可在运行时契约中声明默认 tone 与原生 settings 映射。
  - [#3827](https://github.com/nanocoai/nanoclaw/pull/3827)：Codex 接入该 tone 契约（简化重构）。
  - [#3813](https://github.com/nanocoai/nanoclaw/pull/3813)（已关闭）：durable handoff ledger 与 Slack 结构化 agent 间投递——大型架构 PR，关闭原因值得复盘（是否重构后再来）。

- **杂项**：[#3822](https://github.com/nanocoai/nanoclaw/pull/3822) 忽略 `.worktrees/`。

整体判断：性能与 provider 契约两条主线均取得实质推进，配合 #3781/#3713（tools-only 投递 + delivery_mode 配置）持续活跃，多 agent 投递可靠性体系正在成形。

## 4. 社区热点

- **[#3338](https://github.com/nanocoai/nanoclaw/issues/3338)**（OPEN，3 评论）：Codex WebSocket 空闲重试对 NanoClaw 不可见，导致 Telegram 请求静默 10 分钟直到轮次超时。诉求是**故障可观测性**——Codex CLI 内部 5 分钟空闲重试不向 app-server 上报，NanoClaw 无从感知。建议关注 provider 心跳/进度事件契约。
- **[#3828](https://github.com/nanocoai/nanoclaw/issues/3828)**（新开）：`/update-nanoclaw` cutover 死锁——先停 host 再等容器退出，而唯一能停容器的是 host 本身，排空永不成功。属更新事务设计级缺陷。
- **PR 讨论热度集中在多 agent 投递链**：[#3781](https://github.com/nanocoai/nanoclaw/pull/3781) / [#3713](https://github.com/nanocoai/nanoclaw/pull/3713)（tools-only 投递与 delivery_mode）持续更新，反映社区对“final-text 隐私 + 可靠回执”的强烈需求。

## 5. Bug 与稳定性（按严重程度）

1. **高：[#3828](https://github.com/nanocoai/nanoclaw/issues/3828)** — update cutover 排空逻辑结构性死锁，升级在有 agent 容器运行时无法完成。尚无对应 fix PR（#3832 的 drain 并发化部分相关但非直接修复）。
2. **高：[#3684](https://github.com/nanocoai/nanoclaw/issues/3684)**（已关闭）— 快照捕获符号链接而非内容，rollback 会恢复指向已前向迁移数据的链接，静默成功掩盖数据风险。已关闭，推测已修复（建议确认关联 fix PR）。
3. **中：[#3338](https://github.com/nanocoai/nanoclaw/issues/3338)** — Codex WebSocket 卡顿静默 10 分钟，用户体验为“无响应”。开放中，无 fix PR。
4. **中：[#3823](https://github.com/nanocoai/nanoclaw/pull/3823)**（fix PR，OPEN）— Mattermost 回调未认证 + 外部按钮集成可获取共享密钥，**安全类修复**，含 timingSafeEqual 与密钥轮换指引（配套 #3831），建议优先评审。
5. **低（已修复关闭）：[#1981](https://github.com/nanocoai/nanoclaw/issues/1981)、[#3354](https://github.com/nanocoai/nanoclaw/issues/3354)** — headless/非登录 SSH 安装下 systemd 误判、0 字节 channel 文件等，均于今日关闭。

## 6. 功能请求与路线图信号

待合并 PR 勾画的下一阶段方向：

- **语音交互**：[#3764](https://github.com/nanocoai/nanoclaw/pull/3764) `/add-voice` 全双工浏览器通话（GPT-Live-1 + agent 记忆/工具）——渠道矩阵的重要一极。
- **邮件渠道竞赛**：[#3726](https://github.com/nanocoai/nanoclaw/pull/3726)（Proton Mail Bridge）与 [#3743](https://github.com/nanocoai/nanoclaw/pull/3743)（AgentMail API）两个独立方案并行，短期内“agent 邮箱”需求明显。
- **网关/凭证统一**：[#3824](https://github.com/nanocoai/nanoclaw/pull/3824) provider 凭证连接接口 + [#3825](https://github.com/nanocoai/nanoclaw/pull/3825) OpenCode 经 Iron Proxy 认证——解耦 provider 与网关管理 API 的架构铺垫。
- **可观测性**：[#3796](https://github.com/nanocoai/nanoclaw/pull/3796) `/add-telemetry` OpenTelemetry 全链路追踪（含成本/token），企业化信号强烈。
- **外部生态**：[#3697](https://github.com/nanocoai/nanoclaw/pull/3697) Keenable 搜索 MCP 工具 skill。

判断：delivery_mode + tools-only（#3713/#3781）、tone 契约（已合并 #3826/#3827）大概率随下个版本落地；语音与邮件渠道处于评审中，取决于核心团队带宽。

## 7. 用户反馈摘要

- **部署环境痛点集中**：headless / 非 SSH 登录环境（Hetzner、树莓派）反复出问题（#1981、#3354、#3726 的 ARM 缺 binary）——用户群以自托管爱好者为主，对“一键脚本在任何 shell 环境下都能跑”期望很高。
- **升级可靠性是信任核心**：#3684/#3828 均指向 `/update-nanoclaw` 事务——用户看重 rollback 能真正回滚数据，静默成功比失败更可怕。
- **静默无响应最伤体验**：#3338 的“发消息十分钟没反应”是典型不满来源；用户希望有中间进度/心跳反馈而非黑盒等待。
- **满意度信号**：关闭的 3 个 issue 平均在数日内响应处理，贡献者从核心团队延伸到外部（Keenable、AgentMail 厂商），生态吸引力良好。

## 8. 待处理积压

- **[#3338](https://github.com/nanocoai/nanoclaw/issues/3338)**：已开放近一个月（8/18 创建），仅 3 评论，仍无修复方向确认——建议维护者明确 provider 超时/心跳契约方案。
- **[#3828](https://github.com/nanocoai/nanoclaw/issues/3828)**：昨日新开、0 评论，属升级阻断级问题，应尽快认领。
- **[#3764](https://github.com/nanocoai/nanoclaw/pull/3764)**（9/11）与 **[#3726](https://github.com/nanocoai/nanoclaw/pull/3726)**、**[#3743](https://github.com/nanocoai/nanoclaw/pull/3743)**：大型渠道 PR 悬置多日，建议给出评审时间表，避免社区贡献者流失。
- **[#3724](https://github.com/nanocoai/nanoclaw/pull/3724)**：已退役模型 id 的小修（一行改动）9/5 至今未合并，属低成本可即时处理项。

---
*数据来源：GitHub API（Issues/PR/Releases），统计窗口 2026-09-15 至 2026-09-16。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报（2026-09-16）

## 1. 今日速览

LobsterAI 今日呈现**高强度发布冲刺**状态：过去 24 小时 PR 活跃度显著（30 条更新，其中 20 条已合并/关闭），围绕 **Release/2026.9.15** 版本（[#2687](https://github.com/netease-youdao/LobsterAI/pull/2687)）完成了大批 OpenClaw 兼容性与稳定性修复。Issues 端相对平静（3 条更新，2 条为 stale 自动关闭），无新版本 Release tag 发布，但合入的发布分支 PR 预示正式版即将放出。整体项目健康度良好，维护者（@fisherdaddy、@btc69m979y-dotcom 等）响应迅速，多在创建当天即完成合并。

## 2. 版本发布

无正式 Release 发布。但 **Release/2026.9.15 分支 PR #2687 已于今日关闭/合入**，涉及 renderer、build、docs、main、openclaw、cowork 多个区域，预计正式 tag 即将发布，用户可持续关注 Releases 页面。

## 3. 项目进展

今日合并的核心工作几乎全部聚焦 **OpenClaw v2026.8.1 升级后的兼容性与修复**，共 10+ 个修复 PR 落地：

**OpenClaw 运行时与构建**
- [#2683](https://github.com/netease-youdao/LobsterAI/pull/2683) openclaw 兼容性修复（fisherdaddy）
- [#2686](https://github.com/netease-youdao/LobsterAI/pull/2686) / [#2685](https://github.com/netease-youdao/LobsterAI/pull/2685) 修复 `pnpm pack` 丢失本地补丁依赖问题，保证打包后的 OpenClaw runtime 包含补丁代码
- [#2679](https://github.com/netease-youdao/LobsterAI/pull/2679) 升级后网关状态自动修复：备份引擎数据、运行官方 doctor 修复、恢复损坏的记忆索引与内置插件

**稳定性与错误恢复**
- [#2684](https://github.com/netease-youdao/LobsterAI/pull/2684) 修复启发式输出预算饿死——长会话输出 tokens 被错误压缩至 1 导致推理模型无正文
- [#2682](https://github.com/netease-youdao/LobsterAI/pull/2682) 历史会话回放字段校验，防止损坏记录导致任务反复失败
- [#2681](https://github.com/netease-youdao/LobsterAI/pull/2681) 启动时隔离损坏的旧版 `memory/.dreams/` JSON，避免阻断网关启动
- [#2678](https://github.com/netease-youdao/LobsterAI/pull/2678) 统一长会话压缩摘要格式，保留审计事实
- [#2677](https://github.com/netease-youdao/LobsterAI/pull/2677) 恢复错误卡片中的技术异常详情展示
- [#2664](https://github.com/netease-youdao/LobsterAI/pull/2664) 修复 POPO SDK 加载竞态导致插件加载失败

**仍在待合并（10 条）**，值得关注的如 [#2680](https://github.com/netease-youdao/LobsterAI/pull/2680)（配置同步保留模型迁移策略）。

整体看，项目在一天内完成了对上游 OpenClaw 升级引发的近 10 类回归问题的系统性收口，是明显的版本稳定化里程碑。

## 4. 社区热点

- **[#2342](https://github.com/netease-youdao/LobsterAI/issues/2342)「左下角广告能否彻底关闭」**（OPEN）—— 用户 @PYUDNG 反馈 v2026.7.15 新增侧边栏广告且无永久关闭开关，是当前最受关注的用户侧话题。社区已有响应：PR [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) 添加永久隐藏广告的设置项，但仍处 OPEN 状态，维护者可考虑加速评审。
- 批量 stale 关闭（#1149、#1151 等 3 月末的贡献 PR/Issue）属于例行自动化清理，实际社区讨论热度较低。

## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 |
|---|---|---|
| 高 | 长会话输出 tokens 被压缩至 1，推理无正文且续答无法恢复（[#2684](https://github.com/netease-youdao/LobsterAI/pull/2684)） | ✅ 已修复并合并 |
| 高 | 损坏的历史记录导致任务反复无法继续（[#2682](https://github.com/netease-youdao/LobsterAI/pull/2682)） | ✅ 已修复 |
| 高 | 网关启动被损坏的 memory JSON 阻断（[#2681](https://github.com/netease-youdao/LobsterAI/pull/2681)） | ✅ 已修复 |
| 中 | 打包 runtime 丢失本地补丁（[#2685](https://github.com/netease-youdao/LobsterAI/pull/2685) / [#2686](https://github.com/netease-youdao/LobsterAI/pull/2686)） | ✅ 已修复 |
| 中 | POPO SDK 竞态导致账号监听失效（[#2664](https://github.com/netease-youdao/LobsterAI/pull/2664)） | ✅ 已修复 |
| 中 | 配置同步反复误写迁移后的模型策略（[#2680](https://github.com/netease-youdao/LobsterAI/pull/2680)） | ⏳ PR 待合并 |
| 低 | Gemini `/v1` baseURL 拼接 off-by-one（[#1151](https://github.com/netease-youdao/LobsterAI/issues/1151)） | 已随 stale 关闭 |

今日无新报告的崩溃类 Bug，主要工作为修复存量问题。

## 6. 功能请求与路线图信号

- **广告永久关闭开关**（[#2342](https://github.com/netease-youdao/LobsterAI/issues/2342) + PR [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374)）：已有完整实现（Settings → General 开关），是最可能进入下一版本的社区功能。
- **隐藏 OpenClaw 内部会话**（[#1181](https://github.com/netease-youdao/LobsterAI/pull/1181)）：解决主 agent 心跳会话出现在用户会话列表的困惑，长期 OPEN，需要维护者评审。
- 被关闭的社区贡献 PR（快捷创建技能 #1142、任务上次执行时间 #1144、团队配置模板 #1145 等）反映社区对**技能管理、定时任务可观测性、团队配置分发**的兴趣，可作为路线图参考信号。

## 7. 用户反馈摘要

- **广告植入不满**：用户明确表达了对 v2026.7.15 新增侧边栏广告的反感（“能不能以后就彻底不弹出”），且找不到设置开关，体验预期落差明显。
- **升级后稳定性焦虑**：多个修复 PR 源自用户日志排查（网关启动失败、错误详情丢失、任务无法继续），说明 **OpenClaw 2026.8.1 升级对部分存量用户造成了实际可用性影响**，今日的批量修复正是对这一痛点的集中回应。
- **长会话用户受影响**：输出预算压缩 bug 直接影响重度（长对话）用户的推理结果为空，属高价值用户群痛点。

## 8. 待处理积压

- **[#2374](https://github.com/netease-youdao/LobsterAI/pull/2374)** 广告永久关闭 PR：OPEN 近 2 个月（2026-07-21 创建），且对应高关注度 Issue #2342，建议优先评审。
- **[#1181](https://github.com/netease-youdao/LobsterAI/pull/1181)** 隐藏内部会话 PR：OPEN 超 5 个月，涉及用户可见的会话列表体验。
- **[#2680](https://github.com/netease-youdao/LobsterAI/pull/2680)** 配置同步保留模型策略：今日新开，属发布后应尽快跟进的兼容性问题。
- **[#1277](https://github.com/netease-youdao/LobsterAI/pull/1277)** Electron 43.5→44.3 依赖升级：dependabot PR 挂起超 5 个月，注意安全补丁滞后风险。
- 建议维护者关注批量 stale 关闭的 3 月社区贡献 PR（#1142–#1146），其中部分功能价值较高，关闭前可考虑引导贡献者 rebase。

---
*数据来源：GitHub API，统计窗口为 2026-09-15 至 2026-09-16。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 · 2026-09-16

## 1. 今日速览

- 过去 24 小时项目活跃度**低至中等**：1 条 Issue 更新、1 条新开 PR，无版本发布、无合并/关闭动作。
- 工程侧唯一的动态来自核心贡献者 [@Bergmann89](https://github.com/Bergmann89) 提交的构建优化 PR #1270，聚焦 CI/镜像构建效率，属于基础设施层面的改进。
- 社区侧，长期悬置的增强请求 Issue #205 在沉寂约 7 个月后于 2026-09-15 再度更新，值得关注是否有人接手。
- 整体判断：项目处于**稳定维护期**，无紧急风险信号，但社区功能诉求响应速度偏慢。

## 2. 版本发布

今日无新版本发布，无迁移注意事项。

## 3. 项目进展

今日无 PR 合并或关闭，**项目功能面无净推进**。

唯一进展信号是待合并 PR：

- **[#1270](https://github.com/moltis-org/moltis/pull/1270) feat(build): cache cargo across image builds, and script building the image**（@Bergmann89，2026-09-15 新开）
  - 将 cargo target 目录与 crate registry 改为 BuildKit cache mounts，解决“任意源码变更导致依赖树全量重编译”的问题。
  - 据作者描述，冷构建耗时显著，此改动可大幅缩短 CI/发布构建时间，属于**对开发迭代效率有实际收益的工程改进**。
  - 当前状态：OPEN，尚无评论，等待 review。

## 4. 社区热点

- **[#205](https://github.com/moltis-org/moltis/issues/205) [Feature]: Allow setting body parameters for custom OpenAI endpoints (and per-model)**（@TheGoddessInari，2 条评论，2026-09-15 更新）
  - 诉求：为自定义 OpenAI 兼容端点（乃至按模型粒度）配置请求 body 参数。这反映了使用第三方/代理 LLM 网关（如 OneAPI 类中转、自建 vLLM）的用户，因网关要求额外参数而无法直接接入的痛点。
  - 该 Issue 创建于 2026-02-22，至今约 7 个月仍为 OPEN，是今日唯一活跃的社区讨论，**长期未由维护者正式回应**。

今日无 Bug 报告、无崩溃/回归类 Issue，无高互动内容。

## 5. Bug 与稳定性

- 过去 24 小时**无新增 Bug 报告**，无崩溃或回归问题，稳定性面无警报。
- （前提：Issue #205 为 enhancement 标签，非缺陷。）

## 6. 功能请求与路线图信号

| 功能请求 | 状态 | 可能性评估 |
|---|---|---|
| [#205](https://github.com/moltis-org/moltis/issues/205) 自定义 OpenAI 端点/按模型的 body 参数配置 | OPEN，7 个月，2 评论 | **尚无关联 PR**，短期内纳入下一版本的可能性不明。鉴于 9-15 刚有活动，可能重新进入维护者视野。 |

- 今日工程资源集中于构建基础设施（PR #1270），未投向新功能，下一版本预计以**工程效率与内部质量**为主基调。

## 7. 用户反馈摘要

- 从 #205 可提炼的真实痛点：部分用户依赖 **OpenAI 兼容的第三方端点/中转网关**，这些网关常要求自定义 body 参数，当前 Moltis 的连接配置灵活性不足，成为接入障碍。
- 使用场景：自托管、多模型混接、成本敏感（走代理降低 API 费用）的用户群体。
- 今日样本量过小（1 Issue / 2 评论），不足以做整体满意度评估。

## 8. 待处理积压

- ⚠️ **[Issue #205](https://github.com/moltis-org/moltis/issues/205)**：enhancement 请求，**约 7 个月无维护者响应**（2026-02-22 创建，9-15 才有社区侧更新）。建议维护者至少给出 triage 结论（接受/搁置/拒绝），避免功能诉求长期失联挫伤社区积极性。
- **[PR #1270](https://github.com/moltis-org/moltis/pull/1270)**：今日新开，属高价值构建优化，建议尽快安排 review，缩短合并周期。

---

*数据来源：Moltis GitHub 仓库过去 24 小时 Issues/PR/Release 统计。总体健康度：稳定，无风险信号，但需改善对社区功能请求的响应速度。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-09-16

## 1. 今日速览

CoPaw 今日整体活跃度处于**高位**：过去 24 小时共 70 条 Issue/PR 更新（Issues 20 条，PR 50 条），其中 PR 合并/关闭 26 条、待合并 24 条，Issue 关闭 14 条，关闭效率显著高于新开量（6 条），表明维护团队处于**集中清偿债务、快速收敛问题**的阶段。社区贡献热情旺盛，多个 first-time-contributor PR 被快速迭代合并。无新版本发布，但从 PR 活动看，团队正为 2.2.x 后续版本（含 QwenPaw Hub 多租户版）密集蓄力。需要关注的是 subAgent 超时、MCP 连接回归等 2.2.x 升级引入的稳定性问题。

## 2. 版本发布

今日无新版本发布。注：社区讨论中多次提及 2.2.0 / 2.2.1，Hub 多租户能力正通过 PR #7779 推进，预计进入下一版本。

## 3. 项目进展

今日合并/关闭的重点 PR：

- **#7763** [fix(plugins) 处理插件目录 CDN 读取失败](https://github.com/agentscope-ai/QwenPaw/pull/7763)（关闭 Issue #7730）— 补齐 ConnectionResetError / IncompleteRead 等异常的离线回退，官方插件目录在弱网下不再抛服务器错误。
- **#7741** [feat(console) 自定义主题色](https://github.com/agentscope-ai/QwenPaw/pull/7741)（关闭 Issue #7406）— Console 支持持久化主题配置、实时预览、6 套内置配色，摆脱了用户手改 index.html 的 hack 方式。
- **#7636** [fix(agents) PDF document block 序列化修复](https://github.com/agentscope-ai/QwenPaw/pull/7636)（关闭 Issue #7689）— 修复 #7621 仅覆盖文本模型的问题，OpenAI 兼容 chat-completions 端点对多模态模型不再收到被拒绝的 `{"type":"file"}` 内容块。
- **#7735** [fix(mcp) 保留解码后的 HTTP 错误响应](https://github.com/agentscope-ai/QwenPaw/pull/7735)（修复 #7716）— 修复 2.2.x 升级后 MCP 无法连接注册的回归，过滤过期 framing 头避免二次解压。
- **#7737 / #7736** — 多智能体协作触发词扩展、DeepSeek V4 Flash 能力条目等新贡献者 PR 已关闭（#7795 / #7794 为其重开版本，继续评审中）。

**整体评价**：今日一次解决了 4 个用户可直接感知的痛点（插件目录弱网、主题定制、PDF 多模态、MCP 2.2.x 回归），进度扎实；Hub 治理、语音、录音回放等大型 feature PR 仍在评审管道中。

## 4. 社区热点

- **[#7318 QwenPaw Hub 多租户版 2.2.0 征集意见](https://github.com/agentscope-ai/QwenPaw/issues/7318)**（27 评论，👍 4）— 最热讨论。社区长期诉求团队/多用户部署，官方以 Hub 作答并公开征集下一步方向，是多租户路线图的官方信号。
- **[#7678 [Bug] spawn subAgent 全部超时失败](https://github.com/agentscope-ai/QwenPaw/issues/7678)**（7 评论）— Windows 2.2.0 用户报告所有 subAgent 任务超时，用户自行贴出调试记录求助，反映 subAgent 链路的稳定性焦虑。
- **[#7650 频道参数透传给 MCP 工具](https://github.com/agentscope-ai/QwenPaw/issues/7650)** — 企业集成场景诉求：QQ 号/工号等会话元数据希望透传至 MCP，标记 wontfix 但仍有追问。

## 5. Bug 与稳定性（按严重程度）

1. **🔴 高：[#7786 云/NFS 部署下打开工作区文件浏览器导致整个进程冻结 5–6 分钟](https://github.com/agentscope-ai/QwenPaw/issues/7786)** — 事件循环上的阻塞文件 I/O 使 WebUI 完全无响应，属架构级问题，**尚无 fix PR**。
2. **🔴 高：[#7792 微信音视频附件以 file:// URL 原样发给 OpenAI 兼容 API → 400 错误](https://github.com/agentscope-ai/QwenPaw/issues/7792)** — 多模态通道数据未正确上传转存，**尚无 fix PR**。
3. **🟠 中高：[#7678 spawn subAgent 全部超时](https://github.com/agentscope-ai/QwenPaw/issues/7678)** — 相关诊断 PR [#7796](https://github.com/agentscope-ai/QwenPaw/pull/7796) 已提交（修复 subagent 模型 override 被静默吞掉的问题），可关注是否同源。
4. **🟡 已修复：#7716（MCP 2.2.x 连接回归）→ PR #7735；#7689（PDF file block）→ PR #7636；#7730（插件目录离线回退）→ PR #7763。**
5. **🟡 已修复（历史清理）：#3871 SSE 流未关闭导致无限 "Thinking" 气泡、#5872 Docker 内 browser_use dbus 启动失败。**

## 6. 功能请求与路线图信号

- **[#7797 产物只输出目标文件，不要中间/临时文件](https://github.com/agentscope-ai/QwenPaw/issues/7797)** — 新开，Agent 产物整洁度诉求，暂无对应 PR。
- **[#7746 skills 限定适用 channel 列表](https://github.com/agentscope-ai/QwenPaw/issues/7746)**（已关闭，可能已有方案或被纳入后续）+ **[#7650 频道参数透传 MCP](https://github.com/agentscope-ai/QwenPaw/issues/7650)** — 企业多通道治理方向明确。
- **可能进入下一版本的 PR（Under Review / 活跃）**：
  - [#7779 Hub 模型网关、成员治理与用量看板](https://github.com/agentscope-ai/QwenPaw/pull/7779) — 直接落实 #7318 的 Hub 路线图
  - [#7785 实时语音对话](https://github.com/agentscope-ai/QwenPaw/pull/7785)、[#7798 录制回放工作流](https://github.com/agentscope-ai/QwenPaw/pull/7798)
  - [#7569 Advisor Mode 双模型协作模式](https://github.com/agentscope-ai/QwenPaw/pull/7569)
  - [#7790 统一 Chat Workbench 右侧面板](https://github.com/agentscope-ai/QwenPaw/pull/7790)、[#7744/#7739 布局改进诉求](https://github.com/agentscope-ai/QwenPaw/issues/7739) 已被响应关闭

## 7. 用户反馈摘要

- **满意点**：问题响应快（14/20 Issue 当期关闭）；新贡献者 PR 被积极引导重提；主题定制、文件预览 401 等反馈被快速落地。
- **痛点**：
  - 2.2.0/2.2.1 升级引入回归（MCP 连接、subAgent 超时），多用户在升级路径上受阻；
  - 小屏笔记本上 Web 控制台布局拥挤（#7739/#7700），UI 空间分配是高频反馈；
  - Agent 产出文件杂乱（#7797），用户期望“只交付最终成果”；
  - 企业/团队场景诉求强烈：多用户治理、成员模型网关（#7318、#7779）、私有 IMAP/SMTP（[#7791](https://github.com/agentscope-ai/QwenPaw/pull/7791)）、通道元数据透传（#7650）。
- **使用场景信号**：Docker 自部署 + OpenAI 兼容端点（vLLM/DeepSeek/newapi）是主流部署形态，兼容性 Bug 占比高。

## 8. 待处理积压

- **[#7318 Hub 路线图讨论](https://github.com/agentscope-ai/QwenPaw/issues/7318)** — 27 评论仍 OPEN，建议官方给出阶段性结论以对齐社区预期。
- **[#7786 NFS 文件浏览冻结](https://github.com/agentscope-ai/QwenPaw/issues/7786)**、**[#7792 微信附件 file:// 泄漏](https://github.com/agentscope-ai/QwenPaw/issues/7792)**、**[#7678 subAgent 超时](https://github.com/agentscope-ai/QwenPaw/issues/7678)** — 今日新报，需优先分派。
- **[#4037 HTTP 网关默认无鉴权（安全）](https://github.com/agentscope-ai/QwenPaw/issues/4037)** — 已关闭但属安全类议题，建议确认修复状态并在文档中显式提示。
- **长期 PR**：[#7637 QwenPaw-Data 0.3](https://github.com/agentscope-ai/QwenPaw/pull/7637)、[#7569 Advisor Mode](https://github.com/agentscope-ai/QwenPaw/pull/7569)、[#6399 Reranker UI](https://github.com/agentscope-ai/QwenPaw/pull/6399)（7 月底至今）评审周期较长，建议维护者推进或给出排期。

---
*数据来源：agentscope-ai/CoPaw GitHub 仓库，统计窗口为 2026-09-15 至 2026-09-16。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# 📊 ZeptoClaw 项目动态日报

**日期：2026-09-16** | 仓库：[qhkm/zeptoclaw](https://github.com/qhkm/zeptoclaw)

---

## 1️⃣ 今日速览

- 过去 24 小时项目共产生 **18 条 PR 更新（全部为待合并状态），0 条 Issue 更新，0 个新版本发布**。
- 所有 18 条 PR 均来自 `@dependabot[bot]` 的自动化依赖升级，**无人工提交的功能性或修复性代码**，覆盖 Rust、JavaScript、GitHub Actions 和 Docker 四个依赖维度。
- 项目今日活跃度属于**纯自动化维护型活跃**，缺乏社区讨论与人工开发推进，PR 合并进度停滞（18 条待合并、0 条被合并/关闭）。
- 依赖升级中包含 **astro 6.x → 7.x、base64 0.22 → 0.23 等跨大版本变更**，需要维护者评估兼容性风险。

---

## 2️⃣ 版本发布

今日无新版本发布。最近亦无 Release 记录。

---

## 3️⃣ 项目进展

今日**无任何 PR 被合并或关闭**，项目功能层面无实质推进。18 条待合并 PR 均为依赖维护类，按生态分类如下：

| 类别 | PR | 变更内容 |
|---|---|---|
| Rust 依赖 | [#690](https://github.com/qhkm/zeptoclaw/pull/690) | clap 4.6.1 → 4.6.6 |
| Rust 依赖 | [#694](https://github.com/qhkm/zeptoclaw/pull/694) | base64 0.22.1 → 0.23.1 ⚠️ 跨大版本 |
| Rust 依赖 | [#692](https://github.com/qhkm/zeptoclaw/pull/692) | rustls 0.23.39 → 0.23.43 |
| Rust 依赖 | [#688](https://github.com/qhkm/zeptoclaw/pull/688) | async-trait 0.1.89 → 0.1.92 |
| Rust 依赖 | [#685](https://github.com/qhkm/zeptoclaw/pull/685) | tokio-serial 5.4.5 → 5.5.0 |
| 前端依赖 | [#695](https://github.com/qhkm/zeptoclaw/pull/695) / [#686](https://github.com/qhkm/zeptoclaw/pull/686) | astro 6.3.7 → 7.2.2 ⚠️ 跨大版本（两处文档站） |
| 前端依赖 | [#696](https://github.com/qhkm/zeptoclaw/pull/696) / [#689](https://github.com/qhkm/zeptoclaw/pull/689) | @astrojs/starlight 0.39.2 → 0.41.10（两处文档站） |
| 前端依赖 | [#693](https://github.com/qhkm/zeptoclaw/pull/693) / [#691](https://github.com/qhkm/zeptoclaw/pull/691) | sharp 0.34.5 → 0.35.4（两处文档站） |
| CI/Actions | [#687](https://github.com/qhkm/zeptoclaw/pull/687) | docker/login-action 4.2.0 → 4.6.0 |
| CI/Actions | [#683](https://github.com/qhkm/zeptoclaw/pull/683) | rust-cache 2.9.1 → 2.9.2 |
| CI/Actions | [#684](https://github.com/qhkm/zeptoclaw/pull/684) | cargo-deny-action 2.0.18 → 2.1.1 |
| CI/Actions | [#681](https://github.com/qhkm/zeptoclaw/pull/681) | action-gh-release 3.0.0 → 3.0.3 |
| CI/Actions | [#682](https://github.com/qhkm/zeptoclaw/pull/682) | taiki-e/install-action 2.79.7 → 2.87.6 |
| Docker 基镜像 | [#680](https://github.com/qhkm/zeptoclaw/pull/680) | debian 基础镜像 digest 更新 |
| Docker 基镜像 | [#679](https://github.com/qhkm/zeptoclaw/pull/679) | rust 基础镜像 digest 更新 |

> 💡 值得注意：仓库中存在 `landing/zeptoclaw/docs` 与 `landing/r8r/docs` 两个文档站目录，说明项目文档采用多站点 Astro/Starlight 架构。

---

## 4️⃣ 社区热点

今日无任何 Issue 更新，所有 PR（均为 bot 产生）**评论数与 👍 反应均为 0**，社区热度处于冰点，无热点讨论可供分析。

---

## 5️⃣ Bug 与稳定性

- 今日**无新报告的 Bug、崩溃或回归问题**（0 条 Issue）。
- 间接的稳定性信号：**rustls 0.23.39 → 0.23.43**（[#692](https://github.com/qhkm/zeptoclaw/pull/692)）与 **base64 0.23.1**（[#694](https://github.com/qhkm/zeptoclaw/pull/694)）等安全相关依赖均有更新待合并，建议维护者优先处理 TLS 与编解码库升级，其中 base64 为 API 破坏性大版本，需人工验证。

---

## 6️⃣ 功能请求与路线图信号

今日无用户提出的功能请求。从依赖结构可侧面观察的信号：

- 依赖 `tokio-serial`（串口通信，[#685](https://github.com/qhkm/zeptoclaw/pull/685)）暗示项目可能涉及**本地硬件/嵌入式设备交互能力**；
- Rust + Astro 文档站 + Docker 发布流水线的组合，表明项目处于**多平台分发（二进制 + 容器）+ 完善文档体系**的建设阶段。

---

## 7️⃣ 用户反馈摘要

今日无 Issue 评论数据，无法提炼用户痛点或使用场景反馈。

---

## 8️⃣ 待处理积压

⚠️ **维护者重点关注事项：**

1. **18 条 dependabot PR 全部积压待审**（#679–#696），无一被合并。建议尽快分批处理，优先级建议：
   - 🔴 高：[#692](https://github.com/qhkm/zeptoclaw/pull/692)（rustls，安全修复）、[#694](https://github.com/qhkm/zeptoclaw/pull/694)（base64，破坏性变更）
   - 🟡 中：[#695](https://github.com/qhkm/zeptoclaw/pull/695)、[#686](https://github.com/qhkm/zeptoclaw/pull/686)（astro 7 大版本升级，可能涉及文档站构建配置调整）
   - 🟢 低：CI Actions 与 Docker digest 类机械性升级，可直接批量合并
2. Docker 类 PR（[#679](https://github.com/qhkm/zeptoclaw/pull/679)、[#680](https://github.com/qhkm/zeptoclaw/pull/680)）出现 "Cooldown could not be applied" 警告，属 dependabot 正常提示，但建议核对镜像 digest 更新来源可靠性。

---

### 📈 项目健康度小结

| 指标 | 状态 |
|---|---|
| 自动化维护 | ✅ 良好（dependabot 覆盖全面） |
| 开发活跃度 | ⚠️ 今日无人工提交 |
| 社区互动 | 🔴 冷淡（0 Issue / 0 评论） |
| PR 处理效率 | ⚠️ 18 条积压待合并 |

**建议：** 维护者集中一次 CI 验证 + 批量合并低风险依赖 PR，并重点审查 astro 7 与 base64 0.23 两个破坏性升级，避免技术债累积。

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*