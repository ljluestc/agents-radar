# OpenClaw 生态日报 2026-09-18

> Issues: 500 | PRs: 500 | 覆盖项目: 14 个 | 生成时间: 2026-09-18 03:47 UTC

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

# OpenClaw 项目动态日报 — 2026-09-18

---

## 1. 今日速览

- 项目整体活跃度**极高**：过去 24 小时 Issues 更新 500 条（新开/活跃 397，关闭 103），PR 更新 500 条（待合并 497，仅合并/关闭 3）。
- **合并吞吐量严重偏低**：近千条 PR 活动中只有 3 条合并/关闭，大量带 `👀 ready for maintainer look` 标签的修复 PR 长期滞留，维护者评审带宽成为明显瓶颈。
- 热点集中于 **2026.9.x 系列稳定性回归**：更新失败、消息丢失、Gateway 启动缓慢/事件循环饥饿、SQLite 损坏等 P0/P1 问题持续发酵。
- 今日无新版本发布，Windows 平台更新链路的多条 P0 issue 已关闭，暗示 2026.9.5 修复版本可能在酝酿中。

---

## 2. 版本发布

今日无新 Release。上一个版本 2026.9.4 仍处于问题收敛期，多条 release-blocker 级 issue（#150201、#146719 等）今日关闭，版本修复节奏正常但压力较大。

---

## 3. 项目进展

今日合并/关闭仅 3 条，代表性进展：

- **PR #151350**（已关闭）[fix(ci): restore fs-safe and workflow-routing guard checks](https://github.com/openclaw/openclaw/pull/151350)（@steipete）— 修复 main 分支继承的两处 CI 失败：symlink-race 测试违反 fs-safe 导入边界、workflow-routing 断言缺失 plugin-recovery guard。同日新开姊妹修复 [PR #151339](https://github.com/openclaw/openclaw/pull/151339)（合并文件系统边界 #88、路由 #90、测试清单 #92 三类修复）。**CI 红灯的集中修复是今日主线**，说明 main 分支当前处于修复 CI 的过渡状态。
- **PR #151351** [fix: keep keyboard focus on Logs Refresh](https://github.com/openclaw/openclaw/pull/151351)（@vyctorbrzezowski）— WebUI 可访问性小修复，维护者同日开同日审，属于 WebUI 稳定性伞形计划（#149361）的一部分。
- 多个 P0 Windows 更新问题 issue 关闭：[#150201](https://github.com/openclaw/openclaw/issues/150201)、[#146719](https://github.com/openclaw/openclaw/issues/146719)、[#150452](https://github.com/openclaw/openclaw/issues/150452)。

**整体判断**：项目处于"修复期而非功能期"，前进主要体现为 CI 恢复与升级链路问题收敛，功能面进展有限。

---

## 4. 社区热点

| Issue | 评论 | 主题 |
|---|---|---|
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 31 评论 | **僵尸进程泄漏**：hook/tool 子进程未被 reap，长期运行退化。6 月提出至今仍活跃，与 #86119（孤儿 node worker）同属资源泄漏家族，社区高度共鸣 |
| [#144911](https://github.com/openclaw/openclaw/issues/144911) | 29 评论 | **MCP server 初始化超时导致 Gateway 整体崩溃**：未处理的 promise rejection 打掉整个进程。单个 MCP server 故障不应引发全局崩溃，诉求是隔离性 |
| [#149361](https://github.com/openclaw/openclaw/issues/149361) | 21 评论 | 维护者开立的 **WebUI 性能与稳定性伞形 issue**，今日持续更新，是官方主导的当前工作重心之一 |
| [#139847](https://github.com/openclaw/openclaw/issues/139847) / [#148707](https://github.com/openclaw/openclaw/issues/148707) | 15 / 11 评论 | **"Reply operation has no active tool authority snapshot" 消息丢失**——2026.9.2/9.4 回归，同 session 第二条消息被丢弃，是用户最直接感知的痛点 |
| [#149538](https://github.com/openclaw/openclaw/issues/149538) | 15 评论 | 大规模部署（632-agent 舰队）Gateway ready 后事件循环饥饿、/health 全超时、内存持续增长 |

**背后诉求**：社区核心关切是**2026.9.x 升级后的稳定性回归**（消息丢失、崩溃、升级失败），以及长期积累的**进程/资源生命周期管理缺陷**。

---

## 5. Bug 与稳定性（按严重度）

**P0**
- [#150201](https://github.com/openclaw/openclaw/issues/150201)（已关闭）Windows 更新快照失败 + SQLite 检查超时，升级阻断。
- [#149538](https://github.com/openclaw/openclaw/issues/149538) main 分支 Gateway ready 后不服务、事件循环饥饿（632-agent 规模）。**未见 fix PR，需维护者评审**。
- [#126821](https://github.com/openclaw/openclaw/issues/126821) 全新重建的 SQLite 数据库 15–24 小时内再次损坏，5 天 5 次，出现"瘫痪但不退出"模式。**长期 P0 无 fix PR**。
- [#148529](https://github.com/openclaw/openclaw/issues/148529) 2026.9.4 大舰队启动耗时 12 分钟（旧版 2 秒）。

**P1**
- [#139847](https://github.com/openclaw/openclaw/issues/139847) / [#148707](https://github.com/openclaw/openclaw/issues/148707) 回归导致消息静默丢失（有 `clawsweeper:queueable-fix` 标签，修复已排队）。
- [#144911](https://github.com/openclaw/openclaw/issues/144911) MCP 初始化超时引发 Gateway 崩溃（修复已排队）。
- [#97616](https://github.com/openclaw/openclaw/issues/97616) 子进程僵尸累积（仍 `needs-info`）。
- [#137332](https://github.com/openclaw/openclaw/issues/137332) 混合 settle 批次永久重试；[#141474](https://github.com/openclaw/openclaw/issues/141474) swarm collector 无限挂起。
- [#137729](https://github.com/openclaw/openclaw/issues/137729) 未防护 `.trim()` 崩溃，修复模式已存在于同代码库（queueable-fix）。
- [#148898](https://github.com/openclaw/openclaw/issues/148898)（已关闭）笔记本休眠被 claude-cli watchdog 误判为无输出。

**P2 值得关注**：[#143278](https://github.com/openclaw/openclaw/issues/143278) heartbeat 内部输出泄漏到 Telegram 用户聊天（隐私观感问题）；[#123009](https://github.com/openclaw/openclaw/issues/123009) Codex 订阅误封锁每 5 分钟复发。

---

## 6. 功能请求与路线图信号

- **Skill Capability Manifests v0**（[#74594](https://github.com/openclaw/openclaw/issues/74594)）：技能能力先可见再管控，安全与可发现性方向，等待产品决策。
- **ACP 线程绑定默认预设**（[#79281](https://github.com/openclaw/openclaw/issues/79281)）：WeChat 等第三方渠道各自重复实现 ~870 LOC，抽象诉求强烈；与已开的 [PR #123930](https://github.com/openclaw/openclaw/pull/123930)（thread-bound ACP 回复投递）形成组合，**有机会进入下版本**。
- **Agent 日均消费限额**（[#121729](https://github.com/openclaw/openclaw/issues/121729)）：面向消费级运营成本控制，契合"无人值守 agent"场景。
- **插件生命周期/会话持久化钩子**（[#80674](https://github.com/openclaw/openclaw/issues/80674)）与 **Plugin SDK 结构化 runtime LLM**（[PR #80967](https://github.com/openclaw/openclaw/pull/80967)，XL，已 rebase 到 main）表明**插件生态是明确的路线图方向**，但该 PR 已停 waiting-on-author 状态。
- **嵌套工具 pre-effect 钩子 / 持久化 system prompt**（[#113440](https://github.com/openclaw/openclaw/issues/113440)、[#113442](https://github.com/openclaw/openclaw/issues/113442)）：均有社区 patch 佐证需求真实，但需安全评审。

---

## 7. 用户反馈摘要

- **升级体验是最大痛点**：多个用户报告 2026.7.x → 2026.9.x 升级需数小时到一天的人工修复（[#150452](https://github.com/openclaw/openclaw/issues/150452)：配置迁移失效、Telegram crash-loop、iOS 节点重审批、Usage 页空白）。
- **可靠性信任受损**：[#88087](https://github.com/openclaw/openclaw/issues/88087) 用户因后台任务 UX 差 + cron 静默唤醒失败而**放弃并销毁 Droplet**——真实流失信号。
- **消息丢失类问题情绪最强**：用户明说"回复完全消失、无重试、无并行缓存"（#148707），对 silent failure 的容忍度最低。
- **大规模部署是亮点场景**：632-agent 舰队用户（#148529/#149538）提供了详尽的分阶段性能剖析，社区贡献质量高。
- **正面信号**：维护者（@vyctorbrzezowski、@steipete）今日活跃开 PR/issue，WebUI 伞形计划与 CI 修复显示治理在轨。

---

## 8. 待处理积压

维护者需优先关注：

1. **[#126821](https://github.com/openclaw/openclaw/issues/126821)**（P0，8/20 提出）SQLite 反复损坏，数据安全级问题，无 fix PR。
2. **[#149538](https://github.com/openclaw/openclaw/issues/149538)**（P0）main 分支事件循环饥饿，标注 needs-maintainer-review。
3. **待合并修复 PR 堆积**：497 条 open PR 中大量 `ready for maintainer look`，包括 P0 的 [PR #123457](https://github.com/openclaw/openclaw/pull/123457)（插件节点路由能力门控）、P1 的 [PR #124781](https://github.com/openclaw/openclaw/pull/124781)（onboard --reset 风险确认）、[PR #126237](https://github.com/openclaw/openclaw/pull/126237)（`__proto__` 原型污染修复，安全相关）。
4. **安全类长期挂起**：[#99253](https://github.com/openclaw/openclaw/issues/99253)（assistant 伪造用户轮次并回答）、[#113447](https://github.com/openclaw/openclaw/issues/113447)（npm 包无可验证构建溯源）——均 needs-security-review。
5. **大量 stale issue**：#74594、#53783、#88087、#86119 等带 stale 标签但仍有社区 👍/评论，建议在标记过期前完成分类。

**健康度小结**：社区参与度优秀（问题报告质量高、复现详尽），但 2026.9.x 回归叠加维护者评审带宽不足，使项目处于高活跃/高摩擦状态；短期最关键的是发布稳定性修复版本并疏通 ready-for-review PR 队列。

---

## 横向生态对比

# 个人 AI 助手/智能体开源生态横向对比分析报告

**数据基准日：2026-09-18**

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态已进入**规模化应用与质量收敛并行的阶段**：以 OpenClaw 为核心参照的头部项目日活跃 Issue/PR 更新达数百条量级，632-agent 舰队级部署开始出现，说明产品正从极尝鲜走向生产化。但几乎所有活跃项目共同暴露出**版本回归、消息静默丢失、更新链路失败**等可靠性问题，“高活跃/高摩擦”是当前生态的基调。同时，**插件化、网关/渠道生态、多 agent 安全隔离、上下文压缩治理**成为多条路线图上的共同主轴。生态分层清晰：头部重构期（OpenClaw、Zeroclaw）、质量冲刺期、边缘/垂直定位期各有节奏。

---

## 2. 各项目活跃度对比

| 项目 | Issue 动态 | PR 动态 | Release | 合并/关闭率 | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 500（397 开/103 关） | 500（497 开/3 合） | 无 | ~0.6% PR | ⚠️ 高活跃/高摩擦，评审带宽严重瓶颈 |
| **Hermes Agent** | 50（46/4） | 50（47/3） | 无（v0.21.3 收敛中） | 6% PR | 🟡 P1 响应快，但计费/安全信任问题待闭环 |
| **Zeroclaw** | 50（41/9） | 50（46/4） | 无 | 8% PR | 🟡 深度重构期，XL PR 积压，贡献者集中度高 |
| **CoPaw** | 19（16/3） | 38（21/17） | v2.2.2b2 bump | 45% PR | 🟢 迭代节奏最健康，社区-维护者协作高效 |
| **NanoClaw** | 1（0/1） | 18（14/4） | 无 | 22% PR | 🟢 架构升级窗口期，安装问题当日闭环 |
| **LobsterAI** | 5（2/3） | 19（5/14） | Release/2026.9.16 分支 | 74% PR | 🟡 官方节奏好，但 stale 机制伤害社区管道 |
| **NanoBot** | 4（2/2） | 16（9/7） | 无（0.3.6 酂酿） | 44% PR | 🟢 修复冲刺阶段，自驱修复闭环强 |
| **ZeptoClaw** | 5（1/4） | 7（2/5） | 无 | 71% PR | 🟢 清零速度快；移除 CI 是风险观察点 |
| **Moltis** | 2（2/0） | 3（3/0） | 无（tag 构建有问题） | 0% | 🟡 进多出少，发布 tag 不可复现构建 |
| **IronClaw** | 2（2/0） | 0 | 无 | — | ⚪ 平稳静默，仅讨论无代码推进 |
| **NullClaw / TinyClaw / EasyClaw** | 0 | 0 | 无 | — | ⚪ 无活动 |

---

## 3. OpenClaw 在生态中的定位

**优势**：
- **社区规模量级领先**：日 Issue/PR 更新 500 条，是第二梯队（Hermes/Zeroclaw 50 条）的 10 倍，用户基数与报告质量（632-agent 用户的分阶段性能剖析）代表真实生产渗透率。
- **生态外溢效应**：LobsterAI 直接构建于 openclaw 网关之上（依赖版本合规成为其用户诉求，#1082），NanoClaw 的 Iron Proxy 网关设计亦参照其凭证网关契约——OpenClaw 已具事实标准的部分特征。

**劣势**：
- 合并吞吐量垫底（3/500），多条 P0（#126821 SQLite 反复损坏、#149538 事件循环饥饿）无 fix PR，**治理带宽与规模严重失配**。
- 2026.9.x 回归（消息丢失 #139847/#148707）直接造成用户流失信号（#88087 销毁 Droplet）。
- 安全类 issue（#99253 伪造用户轮次、#113447 构建溯源）长期 needs-security-review 悬置。

**技术路线差异**：Zeroclaw 走事件溯源架构重构（RFC #10526），CoPaw/NanoBot 以小步快跑修复为主，OpenClaw 处于“修复期而非功能期”，功能面（Skill Manifests、插件 SDK）推进受评审瓶颈拖累。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **上下文压缩/淘汰治理** | CoPaw（#7836 scroll 淘汰丢请求、PR #7639）、Zeroclaw（PR #9535 压缩比率、#10780 丢失主动压缩）、NanoBot（#5377 consolidation 丢消息）、IronClaw（#7537 thinking/effort 控制） | 长会话下按模型窗口动态压缩，淘汰时保护用户请求与工具结果完整性 |
| **消息投递确定性/防静默丢失** | OpenClaw（#139847/#148707）、NanoBot（#5798 会话串扰）、Zeroclaw（#10408 重复回复、RFC #10929 送达回执）、Hermes（#114609 终态丢弃） | 跨生态最强共识：silent failure 是用户容忍度最低的缺陷类别 |
| **插件化/组件外置** | Hermes（PR #114569 memory providers 迁插件目录）、OpenClaw（PR #80967 Plugin SDK）、NanoClaw（OneCLI 抽离为 skill #3816）、CoPaw（#7840/#7842 插件隔离） | 核心瘦身 + 插件目录安装 + 隔离契约（同步 I/O 不得冻结宿主） |
| **凭证/审批安全加固** | NanoClaw（#3815 凭证网关契约）、Hermes（#59293 config set 绕过写保护、#107878 fail-closed）、Zeroclaw（shell V1 权限策略 #10610）、Moltis（PR #1272 沙箱 mounts/run_as） | 从 fail-open 转向 fail-closed，审批层不可被 agent 自身绕过 |
| **成本可观测性** | Hermes（#114621 按模型分账、#110912 计费争议）、NanoClaw（#3741 --fresh-session 成本周增 15%）、OpenClaw（#121729 消费限额） | 无人值守 agent 的用量透明与限额成为付费用户刚需 |
| **本地/弱模型支持** | ZeptoClaw（#701 schema 净化 + args 容错）、Zeroclaw（#9453 llama.cpp token 计数）、IronClaw（DeepSeek 参数映射） | 边缘与自托管场景的 provider 兼容性 |

---

## 5. 差异化定位分析

| 维度 | 分化格局 |
|---|---|
| **功能侧重** | OpenClaw/Zeroclaw：全功能 agent 平台（网关+WebUI+渠道+fleet）；NanoBot/CoPaw：IM 渠道代理 + 记忆/压缩深耕；NanoClaw：网关 skill 生态化；ZeptoClaw：边缘运行时（aarch64 7MB 二进制、机器人场景）；Moltis：多 agent 沙箱隔离；LobsterAI：企业 IM（飞书/网易云信）桌面集成 |
| **目标用户** | OpenClaw/Hermes 面向大规模舰队与 power user；NanoBot/CoPaw 以中文自托管 IM 用户为核心画像；ZeptoClaw 锁定 Pi/Jetson 嵌入式；IronClaw 服务多 provider 生产调优用户 |
| **技术架构** | Rust 系（Zeroclaw 事件溯源、ZeptoClaw 边缘、Moltis）vs Node/TS 系（OpenClaw、NanoClaw、LobsterAI）vs Python 系（CoPaw、NanoBot）；架构级重构（Zeroclaw RFC #10526、NanoClaw 网关五连 PR）与小步修复（NanoBot/ZeptoClaw）节奏迥异 |

---

## 6. 社区热度与成熟度分层

- **快速迭代/架构演进期**：NanoClaw（网关重构窗口）、CoPaw（2.2.2 beta 收尾 + 平台化长线）、Zeroclaw（事件溯源重构）
- **质量巩固/修复冲刺期**：NanoBot（0.3.6 回归修复收尾，合并率 44%）、Hermes（fail-closed 哲学落地）、ZeptoClaw（安全加固清零）
- **高规模治理承压期**：OpenClaw——活跃度最高但 497 个 open PR、多条 P0 无 fix，是生态中“规模-治理”矛盾最尖锐的样本
- **贡献管道风险期**：LobsterAI、PicoClaw——stale bot 批量关闭高质量社区贡献（含安全 issue #1031），“自动化替代人工决策”趋势值得警惕
- **静默/早期**：Moltis、IronClaw、NullClaw/TinyClaw/EasyClaw

---

## 7. 值得关注的趋势信号

1. **可靠性 > 功能成为竞争分水岭**：消息静默丢失在 ≥4 个项目中同时成为最痛 issue 类别。对开发者的启示：agent 框架的下一阶段的差异化在投递保证、可审计失败（fail-closed）与显式重试，而非新能力堆叠。

2. **评审带宽是生态普遍瓶颈**：从 OpenClaw（0.6% 合并率）到 Moltis（0 合并），"输入强、消化慢"贯穿所有规模。小团队项目（ZeptoClaw、NanoBot）以快速清零建立信任，大项目需考虑 PR 切片分批合入与评审 SLA。

3. **插件化 + 隔离契约是下一轮架构共识**：Hermes memory 插件化、NanoClaw 网关 skill 化、CoPaw 插件事件循环隔离同期出现——"核心瘦身 + 可插拔 + 沙箱隔离”将成为 agent 框架标准形态。

4. **成本可观测性从 nice-to-have 变为付费门槛**：计费争议（Hermes 账单 3 倍）、成本膨胀（NanoClaw 周 +15%）、消费限额请求，均指向无人值守 agent 的运营财务问责需求。

5. **Agent Skills 标准化互操作萌芽**：`.well-known` 技能发现（Zeroclaw #4853，Cloudflare/Vercel 已支持）值得跟进，跨框架技能复用可能重塑生态边界。

6. **stale 自动化的双刃剑效应**：LobsterAI/PicoClaw/OpenClaw 均出现高价值贡献被 stale 关闭（含安全 issue），提示“贡献者体验”是需要主动治理的资产，而非可自动回收的库存。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报（2026-09-18）

## 1. 今日速览

NanoBot 今日保持较高的社区活跃度：过去 24 小时内共 4 条 Issue 更新（2 开 2 关）和 16 条 PR 更新（9 待合并、7 已合并/关闭），无新版本发布。合并的 PR 集中在稳定性修复（会话消息串扰、上下文压缩通知、consolidation 数据丢失），显示团队正处在一个**修复冲刺阶段**，为下一个版本收敛质量。两个新开 Issue 均为质量类问题（会话串扰、Provider 支持缺口），社区贡献持续以 bugfix + 小型 feature 为主，健康度良好。

## 2. 版本发布

无新版本发布。最近的合并活动（P1 回归修复 #5792、consolidation 修复 #5379）暗示团队可能正在为下一个 minor 版本做收尾，建议关注近期 changelog。

## 3. 项目进展

今日合并/关闭 7 条 PR，主要进展：

- **会话消息串扰修复（重要）**：[#5792](https://github.com/HKUDS/nanobot/pull/5792) `fix(agent): serialize and batch per-session messages`（P1，regression）。为每个会话 worker 安装统一的 FIFO inbox，将 channel 输入、automation turn 和 `/compact` 命令统一走单一准入路径。这直接回应了今日新开的 Issue #5798（会话串扰），修复了 0.3.0 之后引入的回归。这是本日最重要的合并。
- **上下文压缩通知治理**：[#5799](https://github.com/HKUDS/nanobot/pull/5799) 在不支持消息编辑/撤回的渠道（如 QQ）上丢弃压缩过程通知，修复 [#5784](https://github.com/HKUDS/nanobot/issues/5784)。
- **记忆/压缩数据丢失修复**：[#5379](https://github.com/HKUDS/nanobot/pull/5379) `fix(memory): preserve full consolidation input`，历时一个月（8-13 开出，今日关闭），配合关闭了 Issue [#5377](https://github.com/HKUDS/nanobot/issues/5377)。修复了归档截断但指针越界推进导致的消息静默丢失。
- **API 健壮性**：[#5765](https://github.com/HKUDS/nanobot/pull/5765) 强制 `stream` 参数为布尔值（`"stream": "false"` 误触发 SSE）；[#5766](https://github.com/HKUDS/nanobot/pull/5766) 拒绝冲突的 cron 调度字段；[#5762](https://github.com/HKUDS/nanobot/pull/5762) 拒绝过去的 `at` 一次性调度（避免永不触发的僵尸任务）。
- **WebUI**：[#5802](https://github.com/HKUDS/nanobot/pull/5802) 在 AI 初始化未完成前隐藏模型详情，避免泄漏默认 provider。

整体评估：本日合并以**回归修复 + 边界条件加固**为主，尤其在会话隔离和 memory 完整性两个核心可靠性方向取得实质推进。

## 4. 社区热点

- **Issue [#5798](https://github.com/HKUDS/nanobot/issues/5798)（中文社区）**：用户报告 0.3.5 版本中不同会话回复串扰，明确指出“0.3.0 没有这个问题”——直指版本回归，且已有 P1 修复 #5792 合并，用户可期待升级解决。
- **Issue [#5784](https://github.com/HKUDS/nanobot/issues/5784)**（自建 QQ 渠道用户）：压缩通知作为普通消息发送、无法折叠，属于“噪音类”体验问题（关联 #5719），由报告者本人当天提交 PR #5799 并已合并——展现了高质量的“issue + 调查 + 修复”闭环贡献模式。
- **PR [#5800](https://github.com/HKUDS/nanobot/pull/5800)**（Discord replyToMessage 对齐 Telegram）和 **PR [#5803](https://github.com/HKUDS/nanobot/pull/5803)**（Telegram 小修）今日新开，反映渠道生态是社区贡献最活跃的方向。

## 5. Bug 与稳定性（按严重程度）

| 严重度 | 问题 | 状态 |
|---|---|---|
| P1/回归 | 会话消息串扰（#5798），0.3.0 后引入 | ✅ 修复已合并 [#5792](https://github.com/HKUDS/nanobot/pull/5792) |
| 高 | Consolidation 截断输入但推进 `last_consolidated`，导致消息静默丢失（#5377） | ✅ 修复已关闭 [#5379](https://github.com/HKUDS/nanobot/pull/5379) |
| 中 | QQ 渠道压缩通知无法折叠、污染聊天流（#5784） | ✅ 修复已合并 [#5799](https://github.com/HKUDS/nanobot/pull/5799) |
| 中 | 会话 checkpoint 在 metadata 更新后被判过期，重启丢失工具结果与 provider 状态 | 🔧 修复 PR 开放中 [#5801](https://github.com/HKUDS/nanobot/pull/5801) |
| 中 | 并发会话文件写入（write_file/edit_file/apply_patch）无互斥，可能丢更新 | 🔧 修复 PR 开放中 [#5779](https://github.com/HKUDS/nanobot/pull/5779)（fixes #4798） |
| 低 | `stream` 参数真值判断、cron 调度字段冲突/过去时间 | ✅ 均已合并（#5765/#5766/#5762） |

## 6. 功能请求与路线图信号

- **Issue [#5459](https://github.com/HKUDS/nanobot/issues/5459)**：原生 Google Vertex AI provider 支持 Claude 模型。目前 provider 矩阵已覆盖 Anthropic 直连、OpenAI、Azure、Bedrock 等，Vertex AI 是明显的合规场景缺口，讨论持续到 9-17，纳入概率较高。
- **PR [#5718](https://github.com/HKUDS/nanobot/pull/5718)**：OpenRouter 原生图像生成 API 支持，仍在评审，属于 provider 持续扩展信号。
- **PR [#5800](https://github.com/HKUDS/nanobot/pull/5800)**（Discord 回复消息）、**PR [#5562](https://github.com/HKUDS/nanobot/pull/5562)**（流式工具进度事件，closes #3698）均处于活跃推进中，可能进入下一版本。
- 结合本日合并的稳定性修复，下一版本大概率是 **0.3.6：以回归修复 + 渠道体验 + provider 扩展为主线的 patch 版本**。

## 7. 用户反馈摘要

- **企业/合规用户**（#5459）需要 Vertex AI 这类合规入口运行 Claude，反映生产环境部署需求。
- **自托管 IM 用户**（QQ、Telegram、Discord 相关 issue/PR 占本日动态近半）对渠道消息体验（回复引用、通知噪音、换行渲染）敏感，是核心用户画像。
- **可靠性痛点**：消息串扰（#5798）、消息静默丢失（#5377）、checkpoint 丢失（#5801）说明多会话并发与长上下文压缩是当前质量压力点；用户明确以“0.3.0 没这个问题”表达对回归的不满。
- **正面信号**：多个 issue 报告者（如 @AlfredChaos、@dajiaohuang）自己提交并落地修复，社区自驱修复能力较强。

## 8. 待处理积压

- **PR [#5611](https://github.com/HKUDS/nanobot/pull/5611)**（限制 reasoning replay 至最新 assistant turn，8-30 开出，标记 conflict）：涉及每轮 prefill 成本，性能价值高，建议优先解决冲突。
- **PR [#5152](https://github.com/HKUDS/nanobot/pull/5152)**（subagent 部分完成结果标记，7-28 开出）：已积压近两个月，涉及多 agent 编排正确性。
- **PR [#5352](https://github.com/HKUDS/nanobot/pull/5352)**（WebUI 模型 provider 删除功能，8-12 开出）：WebUI 配置管理完善项。
- **Issue [#4798](https://github.com/HKUDS/nanobot/issues/4798)**（并发文件写入丢更新）：对应 PR #5779 已待审数日，涉及数据完整性，建议维护者优先评审。
- **PR [#5562](https://github.com/HKUDS/nanobot/pull/5562)**（标记 conflict）：工具进度流式事件，API 层增强，closes #3698。

---

*数据来源：GitHub HKUDS/nanobot，统计窗口 2026-09-17 至 2026-09-18。*

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报 — 2026-09-18

## 1. 今日速览

Zeroclaw 过去 24 小时保持高活跃度：50 条 Issue 更新（41 新开/活跃、9 关闭）与 50 条 PR 更新（46 待合并、4 合并/关闭），无新版本发布。讨论焦点集中在**多模态图像标记（image marker）安全与误判系列问题**（#10854、#10908、#10887、#10912 构成一条明显的问题链）、**语音/语音路由相关的一批新 Bug**（#10922、#10924、#10925、#10932），以及多个重量级架构 RFC（#10526、#10929、#10930）。46 个待合并 PR 中大量为 XL 规模的核心改造（安全策略、上下文压缩、会话附件、生命周期协调），显示项目正处于深度重构期，审查带宽可能是当前瓶颈。

## 2. 版本发布

无新版本发布（连续无 Release）。结合 #10780 提到 "v0.8.5 无主动 token 预算压缩"，下一个版本预计将集中消化当前积压的 XL 级 PR。

## 3. 项目进展

今日仅 4 条 PR 合并/关闭，整体合并节奏偏慢：

- **[#10664 (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/pull/10664)** — `fix(gateway): sanitize public health errors`：`GET /health` 改为显式公开投影，不再直接序列化诊断快照，减少信息泄露。安全加固落地。
- **[#10953 (OPEN，今日新开)](https://github.com/zeroclaw-labs/zeroclaw/pull/10953)** — 修复 seam sanitizer 整串重写导致签名 reasoning 被破坏的问题，是对 #10894 多模态清理工作的快速跟进。
- **[#10928](https://github.com/zeroclaw-labs/zeroclaw/pull/10928)** — Windows 任务 owner 退出识别修复，配合 #10805 的 control_plane 竞态问题。
- **[#10855](https://github.com/zeroclaw-labs/zeroclaw/pull/10855)** — RFC 投票简化治理文档（stacked on #10677），与 RFC [#10549](https://github.com/zeroclaw-labs/zeroclaw/issues/10549) 呼应，治理流程演进在推进中。

主要在途大型 PR（均今日有更新，等待审查/作者行动）：shell V1 权限策略 [#10610](https://github.com/zeroclaw-labs/zeroclaw/pull/10610)、上下文压缩比率 [#9535](https://github.com/zeroclaw-labs/zeroclaw/pull/9535)、多模型 profile [#9809](https://github.com/zeroclaw-labs/zeroclaw/pull/9809)、持久会话附件 [#10407](https://github.com/zeroclaw-labs/zeroclaw/pull/10407)、agent 生命周期协调 [#10621](https://github.com/zeroclaw-labs/zeroclaw/pull/10621)。

## 4. 社区热点

- **[#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)（15 评论）** — 维护者 RFC/设计决策队列 Tracker，是治理中枢，持续消化待决事项。
- **RFC #10549（12 评论）** — 简化 RFC 投票：取消强制讨论窗口、REVISE 停止当前快照。反映社区对流程摩擦的不满，已有配套文档 PR #10855。
- **RFC #10526（11 评论）** — 追加式会话事件历史 + 确定性状态重放 + 派生 agent 流。高风险架构级提案，触及持久化模型根本重构，是当前最重要的技术讨论。
- **#4853（7 评论）** — 支持从 `.well-known` agent-skills 发现索引安装技能，跟进 Agent Skills 标准化（Cloudflare/Vercel 已支持）。生态互操作诉求明显。
- **#9899（5 评论）** — RUSTSEC-2026-0247：`bitmaps` 无人维护，via `imbl` → Matrix SDK dev-deps，`cargo deny` CI 失败，P1 安全债务。

## 5. Bug 与稳定性

**S1 / P1 高危：**

| Issue | 描述 | Fix 状态 |
|---|---|---|
| [#10854](https://github.com/zeroclaw-labs/zeroclaw/issues/10854) | 工具输出中的字面 image marker 被提升为畸形 provider 图像（S1，阻塞） | 相关 PR [#9819](https://github.com/zeroclaw-labs/zeroclaw/pull/9819)、#10894 在途 |
| [#10908](https://github.com/zeroclaw-labs/zeroclaw/issues/10908) | image marker 无来源提升为附件，剥离/误附源文本（安全域） | in-progress |
| [#10912](https://github.com/zeroclaw-labs/zeroclaw/issues/10912) | 流式文本守卫因散文引用工具协议键而吞掉整条回复，重试 3 次后报格式错误 | in-progress |
| [#10408](https://github.com/zeroclaw-labs/zeroclaw/issues/10408) | 同会话第二条消息触发并行 run → 重复工作/重复回复 | 相关 PR [#10239](https://github.com/zeroclaw-labs/zeroclaw/pull/10239)（修复 alias 读取）在途 |
| [#9899](https://github.com/zeroclaw-labs/zeroclaw/issues/9899) | RUSTSEC-2026-0247 CI 失败 | 待分诊 |
| [#10875](https://github.com/zeroclaw-labs/zeroclaw/issues/10875) | Telegram media-group 测试在无关 PR 上间歇失败，CI 必需门变红（S1） | 定位到 #8955 引入，修复中 |

**S2 中等：** 今日新开一批语音/通道 Bug：[#10922](https://github.com/zeroclaw-labs/zeroclaw/issues/10922)（WhatsApp 忽略 `suppress_voice`）、[#10924](https://github.com/zeroclaw-labs/zeroclaw/issues/10924)（运行时命令回复进入语音路由）、[#10926](https://github.com/zeroclaw-labs/zeroclaw/issues/10926)（Matrix send_via 把用户身份当房间目标）、[#9708](https://github.com/zeroclaw-labs/zeroclaw/issues/9708)（daemon 日志无限增长）。另有 [#10780](https://github.com/zeroclaw-labs/zeroclaw/issues/10780)：v0.8.5 丢失了主动 token 预算压缩能力，长期会话质量受损。

## 6. 功能请求与路线图信号

- **[#10930](https://github.com/zeroclaw-labs/zeroclaw/issues/10930)** — RFC：将 SOP 审批门抽象为通用的“agent 向人类提问”持久原语。方向清晰，复用现有正确实现，采纳概率高。
- **[#10929](https://github.com/zeroclaw-labs/zeroclaw/issues/10929)** — RFC：外发消息送达回执（`SendMessage` 目前无任何 ID）。与 #10526 事件溯源架构天然契合，可能捆绑推进。
- **[#10925](https://github.com/zeroclaw-labs/zeroclaw/issues/10925)** — Matrix `mirror` 语音回复（已 accepted，follow-up）。
- **[#10932](https://github.com/zeroclaw-labs/zeroclaw/issues/10932)** — 语音笔记转录回显（STT echo），已 accepted。
- **[#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853)** — `.well-known` 技能安装，已 accepted 但 blocked/parking-lot，取决于上游标准落地。
- **[#10780](https://github.com/zeroclaw-labs/zeroclaw/issues/10780)** + **PR #9535** 组合信号强烈：上下文压缩按模型窗口比率计算，很可能进入下一版本。

## 7. 用户反馈摘要

- **本地/自托管用户痛点**（#9453、#10780）：llama.cpp 等 OpenAI 兼容 provider 不返回 token 计数导致上下文表空白；失去主动压缩后长会话退化——本地模型用户是活跃且未被充分服务的群体。
- **安装体验**（#5269，已关闭）：`nix run` 路径缺文档、`cargo binstall` 引导不清晰，属典型首次接触摩擦。
- **语音交互可靠性**：今日 4+ 条语音相关 Bug 表明语音功能用户在增长，但 STT 静默出错、TTS 误触发正在伤害信任（#10932、#10922 的诉求核心是“可看见发生了什么”）。
- **消息投递确定性**：重复回复（#10408）与无法确认送达（#10929）反映用户对 IM 场景下 agent 行为确定性的强烈需求。
- **治理与流程**：RFC 参与者（Audacity88、NiuBlibing、JordanTheJet、vrurg 等核心贡献者）反馈流程摩擦大，推动简化（#10549）。

## 8. 待处理积压

- **[#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** — 维护者决策队列持续膨胀（15 评论），需要定期批量裁决，否则阻塞 RFC 管线（#10526 等待 needs-maintainer-review）。
- **[#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853)** — 自 2026-03 开放，blocked 状态近半年，建议明确跟踪上游 agentskills 标准节奏。
- **[#9511](https://github.com/zeroclaw-labs/zeroclaw/issues/9511)** — Semgrep 结果以 PR 评论呈现（parking-lot，7-28 开放），低成本高 contributor 体验收益。
- **[#10780](https://github.com/zeroclaw-labs/zeroclaw/issues/10780)** — parking-lot + needs-maintainer-review，与 PR #9535/#9453 直接相关，建议合并裁决。
- **XL PR 审查积压**：#10610、#9809、#10407、#10621、#10391 等多个 XL PR 长期处于 needs-author-action / needs-maintainer-review，是合并吞吐的主要瓶颈，建议按切片分批合入。

---

**健康度小结**：Issue 关闭率（9/50）与 PR 合并率（4/50）偏低但符合深度重构期特征；新 Issue 质量高（多数含复现与定位）；贡献者集中度高（Audacity88、NiuBlibing 承担大量产出），巴士因子风险需关注。整体呈“输入强、消化慢”态势，瓶颈在维护者审查带宽。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-09-18

---

## 1. 今日速览

今日 Hermes Agent 保持高活跃度：过去 24 小时 Issues 更新 50 条（新开/活跃 46，关闭 4），PR 更新 50 条（待合并 47，已合并/关闭 3），无新版本发布。社区反馈集中在三条主线：**v0.21.3 更新机制引发的 P1 稳定性问题**（SOUL.md 符号链接死循环导致网关无法启动）、**Desktop 端体验与计费透明度问题**（模型选择器静默覆盖默认设置已造成真实经济损失）、以及**记忆系统（memory）的架构演进**（memory providers 向插件目录迁移的 groundwork PR 已出现）。PR 队列以高质量单点修复为主，多人协作节奏健康，但 47 个待合并 PR 与仅 3 个合并/关闭表明维护者评审带宽是当前瓶颈。

---

## 2. 版本发布

今日无新版本发布（最新版本仍为 v0.21.3，2026-09-14 发布）。值得注意的是，v0.21.3 本身引入了多个回归问题（详见第 5 节）。

---

## 3. 项目进展

今日合并/关闭量较小（3 条），但待合并 PR 中有多条高价值修复已就位：

**已关闭的 PR：**
- [PR #114604](https://github.com/NousResearch/hermes-agent/pull/114604) — MCP `ttlMs` 运行时缓存刷新（对应 Issue 同日关闭，社区响应迅速）。
- [PR #113634](https://github.com/NousResearch/hermes-agent/pull/113634) — Desktop 更新提示重复弹窗修复；作者已按 reviewer 要求以严格 1 文件改动重提为 [#114623](https://github.com/NousResearch/hermes-agent/pull/114623)，流程规范。
- [PR #114569](https://github.com/NousResearch/hermes-agent/pull/114569) — **架构信号**：memory providers 移出核心后自动从插件目录安装，是内置记忆组件（Hindsight 等）向维护者仓库 + Plugin Catalog 迁移的地基性工作。

**待合并的重点 PR（代表项目推进方向）：**
- [PR #114601](https://github.com/NousResearch/hermes-agent/pull/114601)（P1）— 修复今日最严重的 update 备份失败仍继续 + SOUL.md 符号链接死循环问题，fail-closed 设计。
- [PR #114621](https://github.com/NousResearch/hermes-agent/pull/114621) — `/usage` 按模型路由分账，覆盖 CLI/TUI/gateway/Desktop 四端，救援自 #96546（@teknium1 亲自提交）。
- [PR #114620](https://github.com/NousResearch/hermes-agent/pull/114620) — WSLg Wayland 渲染失败自动回退 X11，修复 v0.21.3 回归 #114615。
- [PR #107878](https://github.com/NousResearch/hermes-agent/pull/107878) — 凭证缺失时 fail-closed 而非静默走 fallback 计费，直接回应计费透明度痛点。

整体来看，项目在**稳定性加固（fail-closed 哲学）+ 成本可观测性 + 组件插件化**三个方向稳步推进。

---

## 4. 社区热点

**🔥 讨论最热：**

1. [Issue #110912](https://github.com/NousResearch/hermes-agent/issues/110912)（25 评论，已关闭）— **Nous Portal 计费争议**：订阅积分清零后部分模型路由（glm/glm-flash/kimi）被按原价/全价计费，日账单暴涨约 3 倍。社区高度关注，今日关闭，推测已定位为折扣路由 bug 而非积分耗尽。这是涉及真金白银的信任级问题。
2. [Issue #59293](https://github.com/NousResearch/hermes-agent/issues/59293)（14 评论）— **安全设计争议**：`hermes config set` 可绕过 v0.18.0 引入的系统配置写保护，Agent 拥有终端访问权即可关闭审批层。标记 `needs-decision`，暴露了 CLI "前门" 与 shell 审批 "后门" 防护不一致的架构性问题。
3. [Issue #62055](https://github.com/NousResearch/hermes-agent/issues/62055)（3 评论但影响真实）— Desktop composer 模型选择器静默覆盖全局默认模型，有用户因此意外产生费用。与 [Feature #107544](https://github.com/NousResearch/hermes-agent/issues/107544)（请求 "unpin/恢复默认" 操作）共同构成模型选择 UX 的完整诉求链。

**诉求分析**：社区核心焦虑是**"静默行为 + 不可见计费"**——无论是折扣路由失效、模型静默切换还是 fallback 静默计费，用户普遍要求显式、可审计的行为。

---

## 5. Bug 与稳定性（按严重程度排列）

| 级别 | 问题 | 状态 |
|---|---|---|
| **P1** | [#114592](https://github.com/NousResearch/hermes-agent/issues/114592) `hermes update --yes` 备份失败仍继续，SOUL.md 符号链接死循环 → 网关 unbootable（exit 75 重启风暴） | ✅ Fix PR [#114601](https://github.com/NousResearch/hermes-agent/pull/114601) 已提交 |
| **P2** | [#100723](https://github.com/NousResearch/hermes-agent/issues/100723) Windows 下 Desktop 幽灵 WebSocket 重连循环 → auth.json 文件锁冲突 → OAuth 会话被吊销 | 🔍 needs-repro |
| **P2** | [#109215](https://github.com/NousResearch/hermes-agent/issues/109215) 原生 memory 将**已失效**的提案放入审批队列并报 `success: true`，`/memory approve all` 反复失败 | 待修复 |
| **P2** | [#114609](https://github.com/NousResearch/hermes-agent/issues/114609) 多路复用 profile 下异步 delegate 完成消息被**终态丢弃**（读错默认 state.db） | 待修复 |
| **P2** | [#114552](https://github.com/NousResearch/hermes-agent/issues/114552) disk-cleanup 插件对 tracked 目录无保护 rmtree → **误删 $HERMES_HOME/cache 及 kanban 附件**（数据破坏级） | 待修复 |
| **P2** | [#114605](https://github.com/NousResearch/hermes-agent/issues/114605) 非列表型 `custom_providers` 静默清空合并视图，Desktop 显示 "0 endpoints" | 待修复 |
| **P2** | [#114610](https://github.com/NousResearch/hermes-agent/issues/114610) Codex 设备登录：单次瞬时传输错误即放弃 15 分钟轮询，用户浏览器审批作废 | 待修复 |
| **P2** | [#114615](https://github.com/NousResearch/hermes-agent/issues/114615) **v0.21.3 回归**：WSLg 强制 Wayland 导致渲染进程启动失败、无窗口 | ✅ Fix PR [#114620](https://github.com/NousResearch/hermes-agent/pull/114620) |
| **P2** | [#83666](https://github.com/NousResearch/hermes-agent/issues/83666) 视觉能力未知时 `native` 图像输入被静默降级为文本描述 | 待修复 |
| **P3** | [#114543](https://github.com/NousResearch/hermes-agent/issues/114543) Desktop 会话恢复时间线错乱（后到活动嫁接到更早消息上方） | 待修复 |
| **P3** | [#114602](https://github.com/NousResearch/hermes-agent/issues/114602) macOS 打包版全局 hover tooltip 失效 | 待修复 |

**趋势判断**：今日 P1 修复响应极快（Issue 与 Fix PR 同日出现），但 P2 队列中涉及**数据破坏**（#114552）和**消息终态丢失**（#114609）的问题值得优先关注。

---

## 6. 功能请求与路线图信号

结合 Issue 需求与已有 PR，以下方向大概率进入下一版本：

- **每模型用量/成本分账**：[#62055 + #110912](https://github.com/NousResearch/hermes-agent/issues/62055) 的痛点 + PR [#114621](https://github.com/NousResearch/hermes-agent/pull/114621)（@teknium1 提交，跨四端）+ [#96546](https://github.com/NousResearch/hermes-agent/pull/96546) —— 信号极强。
- **模型选择器 UX 补全**：[#107544](https://github.com/NousResearch/hermes-agent/issues/107544)（unpin 操作）与 #62055 互为因果，属低成本高感知修复。
- **Memory 架构演进**：PR #114569（catalog 自动安装）+ Issues [#33638](https://github.com/NousResearch/hermes-agent/issues/33638)（项目级 memory 过滤）+ [#66025](https://github.com/NousResearch/hermes-agent/issues/66025)（长会话 memory 快照过期）—— memory 子系统正在系统性重构，插件化 + 作用域化 + 热更新是清晰路线。
- **长会话/长对话体验**：[#106555](https://github.com/NousResearch/hermes-agent/issues/106555)（虚拟化无限滚动替代手动 "Show earlier"）+ [#102016](https://github.com/NousResearch/hermes-agent/issues/102016)（跳转对话顶部）—— Desktop 渲染预算机制（RENDER_BUDGET=600）的用户可见代价正在累积反馈。
- **桌面常驻体验**：[#114618](https://github.com/NousResearch/hermes-agent/issues/114618)（关闭时最小化到系统托盘）为 duplicate，说明已有内部追踪。

---

## 7. 用户反馈摘要

**真实痛点：**
- 💸 **计费不可见是最大抱怨**：折扣路由失效账单涨 3 倍（#110912）、模型静默切换产生意外费用（#62055）、fallback 静默用付费模型（#107878）——三类问题同源。
- 🖥️ **Desktop 长会话体验差**：手动分页按钮、无法跳顶、时间线错乱、tooltip 失效——GUI 成熟度落后于 CLI 核心。
- 🔁 **更新即风险**：v0.21.3 的 WSLg 回归 + update 备份机制缺陷，让 `hermes update` 被 perceive 为高危操作。
- 🔐 **审批/安全层信任裂缝**：#59293 显示安全意识强的用户在主动审计 approval layer 的绕过面。

**满意点：**
- Issue 报告质量极高（含环境、复现、receipt 日志），社区用户专业度高、参与意愿强。
- 维护者对 P1 响应迅速（同日 fix PR），i18n（印尼语文档 #92192/#93632）等社区贡献持续。

---

## 8. 待处理积压（提醒维护者关注）

| 项目 | 问题 | 建议 |
|---|---|---|
| [#59293](https://github.com/NousResearch/hermes-agent/issues/59293) | 安全问题，7 月开至今，`needs-decision`，14 评论 | 安全类 Issue 长期悬置影响信任，建议尽快决策 |
| [#83047](https://github.com/NousResearch/hermes-agent/issues/83047) | kanban auth 型 respawn guard 永久卡死任务，8 月开至今 | cron/kanban 稳定性积压 |
| [#106678](https://github.com/NousResearch/hermes-agent/issues/106678) | gateway 重启静默 deny 审批 + 丢失提示（durability 提案），9/9 至今无 PR | 与 #114609 同属 session-state 持久化缺口，可合并治理 |
| [#18990](https://github.com/NousResearch/hermes-agent/issues/18990) / [#105650](https://github.com/NousResearch/hermes-agent/issues/105650) | kimi-coding provider 元数据/vision 状态长期滞后 | provider 元数据需要自动同步机制而非手工维护 |
| [#100723](https://github.com/NousResearch/hermes-agent/issues/100723) | Windows OAuth 会话被吊销，`needs-repro` 三周 | Windows 平台专项复现资源不足 |
| PR [#75833](https://github.com/NousResearch/hermes-agent/pull/75833) | cron runtime.db 拆分，8/1 至今待评审，标签多达 8 个风险维度 | 长期大 PR 评审饥饿，建议拆分或指定 owner |

**健康度总评**：项目社区活跃、贡献质量高、P1 响应快；主要风险在 v0.21.x 更新链路回归、47 个待评审 PR 的评审带宽、以及计费/安全两类信任敏感问题的闭环速度。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-09-18

## 1. 今日速览

- 过去 24 小时共有 **15 条动态**（Issues 1 条 + PRs 14 条），其中新开 Issue 0、新开 PR 1（[#3381](https://github.com/sipeed/picoclaw/pull/3381)），整体活跃度处于**中等偏低**水平。
- 值得关注的是，大量 PR/Issue 在昨日（09-17）被批量标记为 `stale` 并关闭，包括 5 个 dependabot 依赖升级 PR 和多个功能 PR，显示出维护者正在进行**积压清理**。
- 无新版本发布，项目处于功能迭代与维护并行的阶段。
- 唯一活跃的 Issue（QQ 频道鉴权失败）已随 stale 流程关闭，社区层面的新问题报告趋于沉寂。

## 2. 版本发布

无新版本发布。（数据中最新 Releases 为空）

## 3. 项目进展

昨日关闭的 PR 多为 stale 自动关闭，实际合并进展有限：

**被关闭的 PR（7 条）：**
- 依赖升级类（全部 stale 关闭，未合并）：[larksuite oapi-sdk-go 3.9.4→3.11.0](https://github.com/sipeed/picoclaw/pull/3360)、[protobuf 1.36.11→1.36.12](https://github.com/sipeed/picoclaw/pull/3361)、[aws-sdk-go-v2 1.42.0→1.45.1](https://github.com/sipeed/picoclaw/pull/3364)、[golang.org/x/term](https://github.com/sipeed/picoclaw/pull/3362)、[ergochat/irc-go 0.6.0→0.7.0](https://github.com/sipeed/picoclaw/pull/3363)
- [#3358](https://github.com/sipeed/picoclaw/pull/3358)（stale 关闭）：修复群聊中机器人回复不引用原消息的问题——该用户体验问题仍未落地。
- [#1158](https://github.com/sipeed/picoclaw/pull/1158)（stale 关闭）：存活超过半年的 anthropic-messages 协议支持 PR 被关闭，意味着 Issue #269 的诉求重新悬空。

**仍在推进的 PR（7 条 OPEN）：**
- 亮点是 [#3381](https://github.com/sipeed/picoclaw/pull/3381)：将 OpenAI provider 切换到 **Responses API**，是当天唯一的新开 PR，反映 LLM 接入层的现代化升级方向。
- [#3368](https://github.com/sipeed/picoclaw/pull/3368)：Parallel Search MCP 集成文档；[#3376](https://github.com/sipeed/picoclaw/pull/3376)：修复 DeltaChat 启动配置校验错误。

**整体判断**：项目今日净进展有限，更多是清理动作；stale 关闭的依赖升级 PR 若不重新打开，可能造成依赖债积累。

## 4. 社区热点

- 讨论最多的是 [Issue #3349](https://github.com/sipeed/picoclaw/issues/3349)（QQ 频道无法连接，401 鉴权错误，5 条评论），Docker 与 Linux x86 均可复现，指向 QQ 官方网关 Authorization 格式变更。该 Issue 已于昨日被 stale 关闭，**问题本身未解决**，建议维护者确认是否需要重新跟进（QQ 渠道在国内用户场景中占比不小）。
- 外部贡献者持续活跃：@georgeatparallel（Parallel Search 集成）、@LinespottingPrivate（Build Remote Agent 配对）、@XenonR（OpenAI Responses API），显示生态集成类需求旺盛。

## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 |
|---|---|---|
| 高 | [Issue #3349](https://github.com/sipeed/picoclaw/issues/3349)：QQ 频道 gateway 401，渠道完全不可用 | 已 stale 关闭，无 fix PR |
| 高 | [PR #3376](https://github.com/sipeed/picoclaw/pull/3376)：deltachat 启动即报 `unknown type "deltachat"`（关联 #3265） | fix PR 待 review |
| 中 | [PR #3358](https://github.com/sipeed/picoclaw/pull/3358)（已关闭）：群聊回复不串联回原消息，繁忙群组可用性差 | fix 被关闭，问题遗留 |
| 低 | [PR #3353](https://github.com/sipeed/picoclaw/pull/3353)：工具反馈动画未限时，可能无限编辑消息 | fix PR 待合并 |

今日无新开 Bug 报告。

## 6. 功能请求与路线图信号

- **LLM 接入现代化**：[#3381](https://github.com/sipeed/picoclaw/pull/3381)（OpenAI Responses API）+ 被关闭的 [#1158](https://github.com/sipeed/picoclaw/pull/1158)（anthropic-messages 原生协议）表明 provider 层是迭代重点；若 #1158 的作者不再跟进，建议维护者接手或重新征集，否则 #269 长期诉求无法闭环。
- **渠道能力扩展**：[#3354](https://github.com/sipeed/picoclaw/pull/3354)（IRCv3 multiline 消息聚合）显示 IRC 渠道在持续打磨。
- **远程/移动端场景**：[#3344](https://github.com/sipeed/picoclaw/pull/3344)（手机配对观看桌面 Agent，gbr/1 协议）体现“个人 AI 助理随身化”方向。
- **代码瘦身**：[#3222](https://github.com/sipeed/picoclaw/pull/3222)（DeltaChat 重构 -200 行，3 个月未动）有被遗弃风险。

## 7. 用户反馈摘要

- **QQ 渠道用户**（#3349）：跨 Docker/Linux 部署均遇鉴权失败，日志详尽且积极互动，属于真实阻断性故障，用户期望官方跟进上游 API 变更。
- **Anthropic 原生 API 用户**（#269/#1158）：使用第三方代理服务（仅支持 `/v1/messages`）无法接入，诉求明确、有现成实现，长期未合并造成挫败感。
- **群聊用户**（#3358）：机器人在群里的回答与提问脱节，反映高频使用场景下的可用性痛点。
- **自托管/隐私敏感用户**（#3368）：希望无账号、无 API key 即可获得网页搜索能力，同时对数据流向（发往 Parallel）要求透明。

## 8. 待处理积压

以下条目长期无响应或已 stale，建议维护者优先处理：

1. [PR #3376](https://github.com/sipeed/picoclaw/pull/3376) — DeltaChat 启动阻断修复，8 天未 review，低成本高价值。
2. [Issue #3349](https://github.com/sipeed/picoclaw/issues/3349) — QQ 渠道完全不可用却被 stale 关闭，建议确认是否需要重开并更新鉴权实现。
3. [PR #3222](https://github.com/sipeed/picoclaw/pull/3222) — DeltaChat 重构，2 个半月 stale，需决定接手或关闭路线。
4. [PR #3344](https://github.com/sipeed/picoclaw/pull/3344) / [#3354](https://github.com/sipeed/picoclaw/pull/3354) / [#3353](https://github.com/sipeed/picoclaw/pull/3353) — 均为质量不错的功能/修复 PR，已 stale，需 review 以免贡献者流失。
5. 5 个被关闭的 dependabot 依赖升级 PR — 建议统一重新生成或合并，避免依赖老化带来的安全与兼容风险。

**健康度小结**：社区贡献意愿良好，但 review 带宽明显不足，stale 自动化正在替代人工决策，若不干预可能出现“贡献流失 + 依赖债”双风险。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 · 2026-09-18

## 1. 今日速览

NanoClaw 今日保持高度活跃：过去 24 小时 PR 更新 18 条（待合并 14 条，已合并/关闭 4 条），Issue 更 1 条（关闭 1 条），无新版本发布。开发重心明显集中在两条主线：**网关架构重构**（OneCLI 抽离为可安装 skill、统一凭证网关契约、新增 Iron Proxy 网关）和**安装引导稳定性修复**（Linux 系统级 Node 环境下的 EACCES 问题）。整体呈现“核心团队密集推进架构演进、社区贡献者持续补充修复”的健康形态，但 14 个待合并 PR 的积压值得维护者关注评审节奏。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

**已关闭/合并的 PR（4 条）：**

- [#3847](https://github.com/nanocoai/nanoclaw/pull/3847) fix(setup): 当全局 bin 目录只读时，将 corepack pnpm 启用至 `~/.local/bin`——解决了系统级 Node 安装（`/usr` 下）非 root 用户 bootstrap 卡死的问题，核心团队出品。
- [#3844](https://github.com/nanocoai/nanoclaw/pull/3844) fix(setup): 用用户级 npm prefix 回退替换失效的 sudo 重试——修复 Fedora/Debian 发行版 Node 包安装时 pnpm 安装永久失败（EACCES）。
- [#3846](https://github.com/nanocoai/nanoclaw/pull/3846) feat(skills): 新增 `/add-typesafe-tool` 与 maintainer agent 模板（已被 #3848 取代迭代）。
- [#3148](https://github.com/nanocoai/nanoclaw/pull/3148) fix: 让 `WEBHOOK_PORT` 遵循 `.env` 配置优先级，关闭长期 Issue #2901。

**今日活跃推进的重点 PR：**

- **网关架构系列**（核心团队 @zvi-fried 等，均为 09-15 创建、09-17 更新）：
  - [#3816](https://github.com/nanocoai/nanoclaw/pull/3816)：将 OneCLI 抽离为可安装 skill——涉及 14 个模块标签的大重构。
  - [#3815](https://github.com/nanocoai/nanoclaw/pull/3815)：集中化凭证网关契约与人工审批生命周期，涉及安全、会话、容器等 12 个区域。
  - [#3817](https://github.com/nanocoai/nanoclaw/pull/3817) / [#3825](https://github.com/nanocoai/nanoclaw/pull/3825)：新增 Iron Proxy 网关 skill 及 OpenCode 通过 Iron Proxy 的认证支持。
- [#3845](https://github.com/nanocoai/nanoclaw/pull/3845)：社区贡献的本地监控 dashboard（`DASHBOARD_SECRET`/`DASHBOARD_PORT`），功能完整度较高，已本地验证。

**评估**：网关重构系列是当前最重的工作流，一旦合并将显著改变安装/认证/审批的架构形态，项目正处在一个大的架构升级窗口期。

## 4. 社区热点

- **Issue #957 [已关闭]** [Suggest supporting Podman as an alternative to Docker](https://github.com/nanocoai/nanoclaw/issues/957)（作者 @fuyb，11 条评论，👍 8，创建于 2026-03-11，今日关闭）
  - 半年来最受关注的功能请求之一。诉求：在文档中提及 Podman 作为 Docker 替代方案，服务 macOS/Linux 上无守护进程/Rootless 场景用户。今日关闭或已落地相关支持，是社区呼声转化为项目能力的信号。

## 5. Bug 与稳定性

今日无新开 Bug Issue，但活跃 PR 修复的问题按严重程度排列：

| 严重度 | 问题 | 状态 |
|---|---|---|
| 高 | 系统级 Node 安装下 bootstrap 卡死 / pnpm EACCES（Linux 发行版用户） | ✅ 已修复：[#3847](https://github.com/nanocoai/nanoclaw/pull/3847)、[#3844](https://github.com/nanocoai/nanoclaw/pull/3844) |
| 高 | Gemini 拒绝序列化的损坏会话历史导致 OpenCode 全部请求失败 | 🔧 修复中：[#3849](https://github.com/nanocoai/nanoclaw/pull/3849) |
| 中 | Codex/OpenCode 的 per-group 远程 MCP 策略与 OneCLI 网关路由未生效 | 🔧 修复中：[#3552](https://github.com/nanocoai/nanoclaw/pull/3552)、[#3551](https://github.com/nanocoai/nanoclaw/pull/3551)（08-26 提出，仍未合并） |
| 中 | 频道附件未以结构化 parts 传递给 providers | 🔧 修复中：[#3156](https://github.com/nanocoai/nanoclaw/pull/3156)（07-30 提出） |
| 低 | webhook 端口恢复测试偶发 EADDRINUSE | 🔧 修复中：[#3803](https://github.com/nanocoai/nanoclaw/pull/3803) |

## 6. 功能请求与路线图信号

- **网关生态化**：#3815/#3816/#3817/#3818/#3825 五连 PR 表明核心团队正将网关层抽象为“可插拔 skill 契约”，Iron Proxy 只是第一个新网关，预计将成为下一版本的核心主题。
- **无状态定时任务**：[#3741](https://github.com/nanocoai/nanoclaw/pull/3741) `--fresh-session`——解决定时任务历史无限增长导致 token 成本逐日上升的真实痛点（作者实测一周增长 15%），方向明确、价值高，很可能被纳入。
- **本地监控面板**：[#3845](https://github.com/nanocoai/nanoclaw/pull/3845) 满足自托管用户可观测性需求。
- **Agent 决策外置**：[#3848](https://github.com/nanocoai/nanoclaw/pull/3848) 将 TypeSafe Jev 决策模型作为容器工具，反映“推理与分类调用分离”的 agent 设计趋势。
- Podman 支持（#957）已关闭，可能已在文档/运行时落地。

## 7. 用户反馈摘要

- **安装体验是最大痛点**：#3844/#3847 均指向同一类问题——使用发行版包管理器安装 Node 的 Linux 用户（Fedora/Debian/Ubuntu）在 bootstrap 阶段反复遭遇权限失败，说明非 nvm/Homebrew 用户占比可观。
- **长期定时任务成本焦虑**：#3741 作者反映相同任务每晚重复执行，会话历史膨胀导致成本每周 +15%，暴露 scheduled tasks 缺乏状态管理选项。
- **多 Provider 兼容性**：Gemini 严格的 turn ordering 与会话历史格式冲突（#3849）说明混合 provider 用户会遭遇难以自愈的会话损坏。
- **容器运行时灵活性**：Podman 请求（8 👍）反映用户对无守护进程、Rootless 容器环境的偏好。

## 8. 待处理积压

- **[#3551](https://github.com/nanocoai/nanoclaw/pull/3551) / [#3552](https://github.com/nanocoai/nanoclaw/pull/3552)**（08-26 提出，23 天未合并）：per-group MCP 策略强制执行——安全相关修复，且与网关重构系列存在耦合，建议优先评审或明确与 #3815 的合并顺序。
- **[#3156](https://github.com/nanocoai/nanoclaw/pull/3156)**（07-30 提出，约 50 天）：频道附件结构化传递——影响多模态使用场景。
- **[#2681](https://github.com/nanocoai/nanoclaw/pull/2681)**（06-03 提出，超过 3 个月）：per-home 加密系统跳过 linger——老 Issue #2680 的修复，长期挂起。
- **[#3741](https://github.com/nanocoai/nanoclaw/pull/3741)**（09-07 提出）：`--fresh-session`——社区呼声强、改动聚焦，建议尽快评审。

**健康度小结**：项目提交节奏稳定、核心团队产出密集、无新 Bug 报告且关键安装问题当日修复闭环，整体健康；主要风险在于 14 个待合并 PR 中的架构级重构与存量修复之间存在潜在冲突，需注意合并编排。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-09-18

## 1. 今日速览
IronClaw 今日整体活跃度较低，无新版本发布、无 PR 更新，Issues 侧有 2 条动态（均为新开/活跃，0 关闭）。讨论焦点集中在 LLM 推理控制能力增强与基准测试失败归因分析两个方向，前者于今日重新活跃，显示社区对 provider 原生参数映射的需求持续存在。项目当前处于功能讨论与质量观测阶段，代码层面的推进今日为零，健康度评估：**平稳但偏静默**。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
今日无 PR 合并或关闭。项目代码层面无可见推进，建议关注后续是否有针对 Issue #7537（thinking/effort 控制）的实现 PR 落地。

## 4. 社区热点
- **[#7537 — generic per-request thinking/effort control](https://github.com/nearai/ironclaw/issues/7537)**（2 评论，今日更新，活跃度最高）
  诉求：为 LLM 请求路径增加**通用的思考/努力级别控制**，支持按请求与按模型默认设置，由各 provider 适配器映射到原生参数。触发场景是 DeepSeek V4 Flash（0731 checkpoint 输出过于冗长）。该 Issue 自 8 月 12 日创建后今日重新活跃，说明用户对跨 provider 统一推理参数控制的呼声仍在持续。
- **[#8101 — Daily failure taxonomy 2026-09-17](https://github.com/nearai/ironclaw/issues/8101)**（昨日创建）
  例行的失败分类日报，覆盖 officeqa 套件 35 个未通过任务，归因多为 DeepSeek-V4-Flash 导航类真实模型质量问题，非框架 Bug。

## 5. Bug 与稳定性
今日无新增 Bug、崩溃或回归报告。
- 值得关注：[#8101](https://github.com/nearai/ironclaw/issues/8101) 中 officeqa 套件 35 个非通过任务，经分类属**模型质量问题**（DeepSeek-V4-Flash 表现），非 IronClaw 框架缺陷，暂无 fix PR 需求，但持续暴露当前默认模型在该类任务上的能力短板。

## 6. 功能请求与路线图信号
- **[#7537 通用 thinking/effort 控制](https://github.com/nearai/ironclaw/issues/7537)**：明确标注 `enhancement, scope: llm`。要求 provider 无关的抽象层 + 原生映射（含 DeepSeek 的 `chat_template_kwargs`）。目前**尚无关联 PR**，但由于触发案例具体、设计边界清晰（per-request + per-model default 两级），是下一版本较有可能纳入的功能方向。建议维护者评估是否进入路线图。

## 7. 用户反馈摘要
- **痛点**：DeepSeek V4 Flash 0731 checkpoint 后输出冗长（verbose），用户缺乏精细化的思考深度控制手段，只能被动接受模型默认行为。
- **使用场景**：通过 NEAR AI 调用多 provider 模型的生产用户，期望统一的推理参数接口而非逐 provider 手动适配。
- **质量观察**：基准用户通过每日 failure taxonomy 持续追踪模型质量，反馈渠道规范、工程化程度高，社区成熟度较好。

## 8. 待处理积压
- [#7537](https://github.com/nearai/ironclaw/issues/7537) 已开 **37 天**（2026-08-12 创建），累计仅 2 条评论，今日虽有更新但仍无维护者明确表态或关联 PR。作为高价值 LLM 层增强需求，建议维护者优先给出 triage 结论（纳入/搁置）。
- 今日无其他长期未响应 Issue/PR。

---
*数据来源：GitHub API，统计窗口 2026-09-17 至 2026-09-18。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报（2026-09-18）

## 1. 今日速览

LobsterAI 今日整体活跃度中等偏上：过去 24 小时 PR 更新 19 条（其中待合并 5 条、已合并/关闭 14 条），Issues 更新 5 条（新开/活跃 2 条，关闭 3 条），无新版本发布。核心维护者团队（@fisherdaddy、@btc69m979y-dotcom、@alison-xx 等）密集推进 openclaw 网关稳定性与 Cowork 体验优化，9 月 17 日已合入 Release/2026.9.16 分支 PR，显示项目正处于版本迭代后的修复收尾阶段。值得注意的是，多条 3 月底社区提交的 Issue/PR 今日被批量标记 stale 并关闭，存在一定的社区贡献流失风险。

## 2. 版本发布

今日无新版本发布。但 [PR #2699 Release/2026.9.16](https://github.com/netease-youdao/LobsterAI/pull/2699) 已于昨日关闭（大概率合入），近期可关注对应的正式 Release 上线。

## 3. 项目进展

今日（含昨日密集更新）合并/关闭的重要 PR：

**Openclaw 运行时与网关稳定性**
- [PR #2691](https://github.com/netease-youdao/LobsterAI/pull/2691)：修复飞书原生插件加载报 `ReferenceError: exports is not defined`，解决升级后渠道注册失败——影响生产可用性的关键修复。
- [PR #2695](https://github.com/netease-youdao/LobsterAI/pull/2695)：浏览器 DNS 失败不再导致网关重启，避免打断 IM 会话。
- [PR #2698](https://github.com/netease-youdao/LobsterAI/pull/2698)：一键修复流程中安全恢复陈旧网关/迁移锁（含 PID 核验），对应 9 月 16 日现场故障反馈。
- [PR #2694](https://github.com/netease-youdao/LobsterAI/pull/2694)：防止 IM 工作负载准备期被误判为空闲而触发配置恢复重启（仅第一阶段）。
- [PR #2700](https://github.com/netease-youdao/LobsterAI/pull/2700)：Pre-audit v1 数据库缺少 `audit_events` 表，在修复租约下初始化 legacy schema——已关闭，待确认是否合入。

**应用体验优化**
- [PR #2693](https://github.com/netease-youdao/LobsterAI/pull/2693)：应用退出即时隐藏窗口、skill 服务轮询真实退出而非固定等待 2s，改善退出体验。
- [PR #2692](https://github.com/netease-youdao/LobsterAI/pull/2692)：Cowork 活动指示器轮换思考阶段文案并显示已完成步骤数，解决长时间静默“看似卡死”的观感问题。

**待合并（社区贡献为主）**
- [PR #2696](https://github.com/netease-youdao/LobsterAI/pull/2696)：来自下游 fork 的 Codex 风格工作区改进（轮次工作区审查、行内提问 dock、Tasks 面板），功能量较大，值得评审关注。
- [PR #2669](https://github.com/netease-youdao/LobsterAI/pull/2669)：dependabot 提议 vite 5.4.21 → 8.3.0 跨 3 个大版本，风险较高，建议拆分评估。

## 4. 社区热点

- [Issue #1082](https://github.com/netease-youdao/LobsterAI/issues/1082)（2 评论，已关闭）：用户询问 `openclaw.version v2026.3.2` 是否支持最新版 openclaw，并援引国家互联网应急中心（CNCERT）的更新合规要求。诉求核心是**依赖版本合规与安全合规**，维护者应关注依赖升级节奏的对外沟通。
- [Issue #1088](https://github.com/netease-youdao/LobsterAI/issues/1088) / [#1089](https://github.com/netease-youdao/LobsterAI/issues/1089)（各 2 评论，均被 stale 关闭）：高质量的并发缺陷报告（prefetch 跨轮次污染、CoworkRunner 无重入保护），报告详细到具体代码行，却被 stale bot 关闭，未见到实质修复，社区贡献者体验受损。

## 5. Bug 与稳定性

| 严重度 | 问题 | 状态 |
|---|---|---|
| 🔴 高 | [Issue #1031](https://github.com/netease-youdao/LobsterAI/issues/1031)（OPEN，stale）：`shell:openExternal` IPC 不校验 URL 协议，可调用 `file://` 等任意协议，**安全风险** | 无对应 fix PR |
| 🔴 高 | [Issue #1026](https://github.com/netease-youdao/LobsterAI/issues/1026)（OPEN）：IM `v2Client` 置空后分块发送崩溃 TypeError | 有社区 fix：[PR #1028](https://github.com/netease-youdao/LobsterAI/pull/1028)（OPEN，stale） |
| 🟡 中 | [Issue #1089](https://github.com/netease-youdao/LobsterAI/issues/1089)（已 stale 关闭）：CoworkRunner 并发导致流式消息损坏/重复 | 无 fix PR |
| 🟡 中 | [Issue #1088](https://github.com/netease-youdao/LobsterAI/issues/1088)（已 stale 关闭）：Prefetch 异步回调不校验 turnToken，跨轮次状态污染 | 无 fix PR |

今日无新开崩溃/回归报告，主要活动为旧 Issue 批量 stale 处理。

## 6. 功能请求与路线图信号

- [PR #2696](https://github.com/netease-youdao/LobsterAI/pull/2696)（官方成员提交）：Codex 风格工作区（审查视图、行内提问、Tasks 面板）已就绪待合并，**极可能进入下一版本**，是当前最明确的功能路线图信号。
- [PR #2692](https://github.com/netease-youdao/LobsterAI/pull/2692) 已合并：活动指示器轮换，表明团队在持续打磨 Cowork 静默期反馈。
- [PR #1078](https://github.com/netease-youdao/LobsterAI/pull/1078)（已 stale 关闭）：定时任务失败推送 IM 告警——需求合理但被关闭，方向可能由团队另行实现。
- [PR #641](https://github.com/netease-youdao/LobsterAI/pull/641)（已 stale 关闭）：双击重命名会话，小而美的 UX 需求，建议复活。

## 7. 用户反馈摘要

- **合规焦虑**：企业用户明确关注 CNCERT 对依赖版本的合规要求（#1082），依赖 openclaw 版本停留在 v2026.3.2 引发升级风险担忧。
- **生产稳定性痛点**：网关锁、配置恢复误判、插件加载失败等现场故障在 9 月 16 日反馈表中集中出现，团队今日的修复 PR 均直接对应此类反馈，响应速度值得肯定。
- **IM 场景依赖度高**：多条报告围绕 IM（网易云信/飞书/POP O/企业微信）在断连、并发下的崩溃问题，IM 网关是稳定性薄弱环节。
- **不满意点**：高质量社区 Bug 报告和 PR（#1026-#1029、#1078-#1089 系列）被 stale 机制批量关闭且无官方回应，社区贡献者可能有挫败感。

## 8. 待处理积压

⚠️ 以下高价值 Issue/PR 长期无官方响应，建议维护者优先关注：

1. [Issue #1031](https://github.com/netease-youdao/LobsterAI/issues/1031) — 安全问题（openExternal 协议校验缺失），不应被 stale 拖延，建议尽快自研修复。
2. [Issue #1026](https://github.com/netease-youdao/LobsterAI/issues/1026) + [PR #1028](https://github.com/netease-youdao/LobsterAI/pull/1028) — 有现成修复方案的崩溃 Bug，6 个月未处理。
3. [PR #1027](https://github.com/netease-youdao/LobsterAI/pull/1027) — 外部开发者构建卡死 5 分钟（内网 registry 不可达），直接阻碍开源社区参与贡献。
4. [PR #2696](https://github.com/netease-youdao/LobsterAI/pull/2696) — 大型功能 PR 待评审，避免积压导致 rebase 成本上升。
5. [PR #1029](https://github.com/netease-youdao/LobsterAI/pull/1029) — PLATFORM_TO_CHANNEL_MAP 自动反转的隐式正确性风险，属低成本防御性修复。

**健康度小结**：官方团队的开发节奏健康、对现场故障响应迅速；但社区贡献管道（Issue/PR 响应率）是当前短板，stale 批量关闭叠加安全 Issue 滞后处理，建议建立安全 Issue 快速通道和社区 PR 评审 SLA。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 · 2026-09-18

## 1. 今日速览

项目整体保持平稳活跃：过去 24 小时新增 2 条 Issue、3 条 PR 更新，无版本发布。社区贡献来源多元（外部贡献者 + Dependabot），沙箱安全能力（PR #1272）和构建可靠性修复（PR #1262）持续推进，但今日无 PR 合并、无 Issue 关闭，消化速度偏慢，出现轻微积压迹象。

## 2. 版本发布

今日无新版本发布。最新 tag 仍为 `20260913.02`，但该 tag 存在 Nix 构建问题（见 Issue #1273），建议关注后续修复与重新发布。

## 3. 项目进展

今日无 PR 合并或关闭，3 条 PR 均处于待合并状态：

- **[PR #1272](https://github.com/moltis-org/moltis/pull/1272)** `feat(sandbox): per-agent mounts, run_as and a forced sandbox`（@Bergmann89，09-16 提出，昨日有更新）。为 agent preset 的 `[sandbox]` 块新增三个配置项：`sandbox.mounts`（额外宿主机 bind mount）、`sandbox.run_as`（容器 uid:gid）、`sandbox.force`（强制该 agent 只能在沙箱内运行）。这是对多 agent 安全隔离能力的实质性增强。
- **[PR #1262](https://github.com/moltis-org/moltis/pull/1262)** `fix(cron): treat active_hours end="24:00" as end-of-day`（@atirna）。修复 chrono `%H` 拒绝解析 "24:00" 导致默认配置解析失败、fail-open 使 agent 全天候运行的问题，活跃时段限制功能恢复正常。

## 4. 社区热点

今日所有条目评论数均为 0 或缺失，暂无高热度讨论。相对值得关注的是：

- **[Issue #1273](https://github.com/moltis-org/moltis/issues/1273)**（@flextiondotorg）：Nix 构建问题的详细报告，来自知名打包/维护贡献者，诉求是让 flake 在发布 tag 上可复现构建，对 Nix 用户群体影响直接。

## 5. Bug 与稳定性

按严重程度排列：

| 等级 | 问题 | 状态 |
|---|---|---|
| 🔴 高 | **[Issue #1273](https://github.com/moltis-org/moltis/issues/1273)**：tag `20260913.02` 的 `packages.default` 无法构建。`cargoLock.outputHashes` 仅 pin `sqlx-core-0.8.6`，缺少 `wacore-0.6.0`、`zvec-rust-0.6.0` 的哈希，且缺 web assets，`nix build .#default` 失败。 | 无修复 PR，**已影响发布 tag 的可复现性** |
| 🟡 中 | **[PR #1262](https://github.com/moltis-org/moltis/pull/1262)**：`active_hours` 的 `end="24:00"` 解析失败 → fail-open → 定时任务全天运行（24×6 触发），既是 bug 也是 fail-open 策略隐患。 | fix PR 已提交，待合并 |

## 6. 功能请求与路线图信号

- **[Issue #1274](https://github.com/moltis-org/moltis/issues/1274)** `[enhancement]` Prepaid search hop for Moltis wasm-web-search?（@iamalanlui）：请求为 wasm web search 模块提供预付费搜索接入，反映用户对低成本、可控配额的搜索后端需求。目前 0 评论、无关联 PR，属早期探索阶段。
- 结合 PR #1272 的沙箱细粒度配置，可看出项目路线图上“**多 agent 安全隔离与运行时控制**”是明确方向，预计随下个版本落地。

## 7. 用户反馈摘要

今日两条 Issue 均为新开且无后续评论，可提炼的信号有限：

- **Nix/NixOS 用户**：依赖项目提供可复现的 flake 构建，发布流程中 vendored crate 哈希和 web assets 的完整性是他们能否使用项目的前提（#1273）。
- **成本敏感用户**：搜索能力（wasm-web-search）的付费模式受关注，希望有预付费/按量选项而非订阅（#1274）。

## 8. 待处理积压

- **[Issue #1273](https://github.com/moltis-org/moltis/issues/1273)**：影响已发布 tag 的构建，建议优先处理并考虑在 CI 中加入 Nix 构建检查，防止回归。
- **[PR #1262](https://github.com/moltis-org/moltis/pull/1262)**（09-07 开启，已 11 天）与 **[PR #1272](https://github.com/moltis-org/moltis/pull/1272)**（09-16 开启）均待 review/合并，建议维护者安排评审，避免功能修复滞后于发布节奏。

---

**健康度小结**：社区输入持续（外部贡献者提交质量较高），但“进多出少”——今日 0 合并/0 关闭，建议加快 review 节奏，尤其优先修复影响发布 tag 可用性的 Nix 构建问题。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 · 2026-09-18

## 1. 今日速览

- 项目保持高活跃度：过去 24 小时 Issues 更新 19 条（新开/活跃 16、关闭 3），PR 更新 38 条（待合并 21、已合并/关闭 17），无新版本正式发布，但版本号 bump 至 **v2.2.2b2** 的 PR 已合并，预示 beta 迭代在推进。
- 今日问题焦点集中在 **scroll 上下文淘汰策略**、**Console SSE 流健壮性** 和 **插件隔离/事件循环阻塞** 三大方向，多位高质量贡献者（@chcsyf、@wjt0321）提交了系统性 bug 报告。
- MCP 生态方面暴露出 OAuth token 刷新被丢弃、streamable_http 驱动激活失败等集成问题。
- 社区反馈整体建设性强，多数 bug 报告附带复现环境与日志，健康度良好。

## 2. 版本发布

今日无正式 Release。但 [PR #7844](https://github.com/agentscope-ai/CoPaw/pull/7844)（chore: bump the version to v2.2.2b2）已关闭/合并，且 [Issue #7847](https://github.com/agentscope-ai/CoPaw/issues/7847) 显示 **2.2.2b1 已在用户手中流通**，可判断 2.2.2 正式版即将发布。

## 3. 项目进展

今日关闭的重要 PR：

- **[PR #7844](https://github.com/agentscope-ai/CoPaw/pull/7844)** — 版本号升至 v2.2.2b2，为下一轮 beta 发布做准备。
- **[PR #6353](https://github.com/agentscope-ai/CoPaw/pull/6353) + [PR #7050](https://github.com/agentscope-ai/CoPaw/pull/7050)** — Cron 任务级模型覆盖功能（后端 + Console UI）双双落地，对应 [Issue #6316](https://github.com/agentscope-ai/CoPaw/issues/6316) 已关闭。这是一个从 7 月底开始、历时近两个月的完整功能闭环。
- **[PR #7760](https://github.com/agentscope-ai/CoPaw/pull/7760)** — CLI 关闭时允许 memory 任务排空，Windows 桌面后端以进程组方式优雅终止。
- **[PR #7831](https://github.com/agentscope-ai/CoPaw/pull/7831)** — Console 后台工具输出按需流式加载（展开时才开 SSE），降低资源消耗。
- **[PR #7488](https://github.com/agentscope-ai/CoPaw/pull/7488)** — PawApp SDK 流资源精确一次性释放，修复取消/中止竞态下的资源泄漏。

整体看，版本迭代节奏稳健，2.2.x 系列以稳定性修复为主，同时长线功能（cron 模型覆盖、QwenPaw-Data、语音聊天）持续推进。

## 4. 社区热点

- **[#7678](https://github.com/agentscope-ai/CoPaw/issues/7678) [Bug] spawn subAgent 全部超时失败** — 评论 10 条，为今日讨论最热 issue。Win 2.2.0 用户报告所有 subAgent 任务超时，且加大 timeout 无效，属核心执行路径问题，仍在排查中。
- **[#7840](https://github.com/agentscope-ai/CoPaw/issues/7840) 插件共享宿主事件循环导致整实例冻结** — @chcsyf 的深度报告：任一插件的同步 I/O 可冻结全部 agent 约 40 秒，指出缺乏隔离契约、监控与沙箱。**响应迅速**：[PR #7842](https://github.com/agentscope-ai/CoPaw/pull/7842) 当日即提交（隔离同步 hook + 事件循环延迟 watchdog），社区-维护者协作效率高。
- **[#7810](https://github.com/agentscope-ai/CoPaw/issues/7810)（已关闭）上下文输入限制设置不生效** — 用户设置 131k 却每次提交 271k，压缩不触发。[PR #7832](https://github.com/agentscope-ai/CoPaw/pull/7832) 揭示根因：模型对话框展示的 `max_input_length` 与运行时五级优先级链解析不一致，修复 PR 已在推进。

## 5. Bug 与稳定性（按严重程度排列）

| 严重度 | 问题 | 状态 |
|---|---|---|
| 🔴 高 | [#7678](https://github.com/agentscope-ai/CoPaw/issues/7678) subAgent spawn 全部超时失败，任务无法推进 | 无 fix PR，需重点关注 |
| 🔴 高 | [#7840](https://github.com/agentscope-ai/CoPaw/issues/7840) 插件同步调用冻结整个实例 | ✅ [PR #7842](https://github.com/agentscope-ai/CoPaw/pull/7842) 已提交 |
| 🔴 高 | [#7839](https://github.com/agentscope-ai/CoPaw/issues/7839) 保留清理报 "database disk image is malformed"，86 个孤儿 session 文件被静默跳过 | 无 fix PR |
| 🟠 中 | [#7836](https://github.com/agentscope-ai/CoPaw/issues/7836) scroll 淘汰把 tool 密集区间连同两侧用户请求一并丢弃，活跃窗口丢失请求 | 相关性能 PR [#7639](https://github.com/agentscope-ai/CoPaw/pull/7639) 在途 |
| 🟠 中 | [#7813](https://github.com/agentscope-ai/CoPaw/issues/7813) / [#7814](https://github.com/agentscope-ai/CoPaw/issues/7814) / [#7815](https://github.com/agentscope-ai/CoPaw/issues/7815) Console SSE 三连报：裸 `null` payload 冻结流、失败时无终结事件、懒加载失败后无法恢复 | 无 fix PR |
| 🟠 中 | [#7847](https://github.com/agentscope-ai/CoPaw/issues/7847) 文件名含字面 `%` 转义可静默发送/预览错误文件（潜在数据安全风险，2.2.2b1 复现） | 无 fix PR |
| 🟡 低 | [#7821](https://github.com/agentscope-ai/CoPaw/issues/7821) MCP 驱动丢弃刷新后的 OAuth access_token；[#7827](https://github.com/agentscope-ai/CoPaw/issues/7827) `server/discover` 裸 500 未识别为旧协议，DashScope MCP 卡永远无法激活 | 无 fix PR |
| 🟡 低 | [#7841](https://github.com/agentscope-ai/CoPaw/issues/7841) 桌面版 Console 在后端就绪前渲染导致面板空白；[#7812](https://github.com/agentscope-ai/CoPaw/issues/7812) 启动后 slash 命令作用于回退会话 | 无 fix PR |

## 6. 功能请求与路线图信号

- **Agent 自主上下文管理**（[#7733](https://github.com/agentscope-ai/CoPaw/issues/7733)）：希望在上下文淘汰时有平滑交接，让 agent 参与决定何时压缩。与 scroll 系列修复方向一致，可能进入 2.3.x 规划。
- **`recall_history_python` 沙箱缺失时静默降级**（[#7838](https://github.com/agentscope-ai/CoPaw/issues/7838)）：要求显式告警而非静默只注册结构化工具，属可快速落地的小改进。
- **`/os` 桌面模式开放应用注册接口**（[#7830](https://github.com/agentscope-ai/CoPaw/issues/7830)）：生态扩展诉求，与 [PR #7833](https://github.com/agentscope-ai/CoPaw/pull/7833)（Hub/Local runtime/PawApp 打通）同属平台化路线。
- 长线 PR 信号：实时语音聊天（[#7785](https://github.com/agentscope-ai/CoPaw/pull/7785)）、QwenPaw-Data 0.3 数据分析应用（[#7637](https://github.com/agentscope-ai/CoPaw/pull/7637)）、插件热更新回滚（[#7565](https://github.com/agentscope-ai/CoPaw/pull/7565)）、AgentScope Platform 内置 Provider（[#7843](https://github.com/agentscope-ai/CoPaw/pull/7843)）——显示路线图正朝**平台化 + 多模态**演进。

## 7. 用户反馈摘要

- **中文桌面用户（Win 2.2.x）痛点集中**：上下文爆表无法压缩（#7810）、subAgent 超时（#7678）、启动后 UI 面板空白（#7841）——桌面端稳定性是流失风险点。
- **高级/托管云用户**对架构健壮性提出系统性批评：插件无隔离（#7840）、scroll 淘汰策略粗暴（#7836/#7837/#7839），说明 power user 已将其用于长周期生产任务。
- **MCP 集成用户**在对接 DashScope 千问 MCP 商店时反复受挫（#7827、#7821），OAuth 与协议探测逻辑影响生态采用。
- 正面信号：bug 报告质量高（含版本、commit、日志、复现步骤），TCM 医疗技能仓库作者主动咨询许可证建议（[#7845](https://github.com/agentscope-ai/CoPaw/issues/7845)，已关闭），显示技能生态在自发生长。

## 8. 待处理积压

- **[#7678](https://github.com/agentscope-ai/CoPaw/issues/7678)（9-11 开启，10 条评论，仍未解决）**：subAgent 超时问题持续一周，影响核心功能，建议维护者优先定位。
- **[PR #7565](https://github.com/agentscope-ai/CoPaw/pull/7565)（9-04）与 [PR #7542](https://github.com/agentscope-ai/CoPaw/pull/7542)（9-04，first-time-contributor）**：插件热更新与 scroll 回看分页两个大 PR 已滞留两周，需 review 推进，以免挫伤社区贡献者。
- **[PR #6399](https://github.com/agentscope-ai/CoPaw/pull/6399)（7-23）**：Reranker UI 配置面板已近两个月未合入，建议明确状态。
- **[PR #7639](https://github.com/agentscope-ai/CoPaw/pull/7639) / [PR #7637](https://github.com/agentscope-ai/CoPaw/pull/7637)（9-08）**：scroll 完整性扫描优化与 QwenPaw-Data 0.3 均为 Under Review，建议在 2.2.2 发布窗口内决策是否纳入。

---
*数据来源：GitHub API（Issues/PR，截至 2026-09-18）*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目日报 — 2026-09-18

## 1. 今日速览

项目今日保持较高维护活跃度，过去 24 小时共 5 条 Issue 更新（1 新开 / 4 关闭）和 7 条 PR 更新（2 待合并 / 5 已合并或关闭），全部Issue/PR 清零速度较快，处理节奏健康。今日主线集中在**安全加固**（面板登录限速、Rustls 安全公告修复）和**本地/弱模型工具调用健壮性**两条线上。值得注意的是，维护者主动移除了全部 GitHub Actions CI 检查，转向本地验证模式，这一工程流程变更值得社区关注。

## 2. 版本发布

过去 24 小时无新版本发布。

## 3. 项目进展

今日关闭的 PR 推进了三条主线：

**🔐 安全修复**
- [PR #692](https://github.com/qhkm/zeptoclaw/pull/692)（已关闭）：将 Rustls 升级至 0.23.45，修复安全公告 RUSTSEC-2026-0285，同步解除 18 个 Dependabot PR 被 Security audit / cargo deny 阻塞的问题。对应 Issue [#697](https://github.com/qhkm/zeptoclaw/issues/697) 已关闭。
- [PR #702](https://github.com/qhkm/zeptoclaw/pull/702)（待合并）：面板密码登录端点此前允许无限次尝试（仅有 bcrypt cost 作为减速带），现加入基于 socket peer IP 的滚动窗口限速（60 秒内 5 次，第 6 次返回 HTTP 429 + `Retry-After: 60`），且限速在 JSON 解析和密码验证之前生效，设计合理。

**🛠️ 本地模型工具调用健壮性**
- [PR #701](https://github.com/qhkm/zeptoclaw/pull/701)（已关闭）：落地 Issue [#698](https://github.com/qhkm/zeptoclaw/issues/698) 的方案——出站方向对所有 `ToolRegistry::definitions*()` 路径的 schema 统一经 `sanitize_schema()` 净化（覆盖外部 MCP 服务器和插件返回的裸 schema）；入站方向对严格/本地后端的模型 tool-args 做强制转换。这对 ZeptoClaw 定位边缘运行时、服务 ollama/local 弱模型的目标是关键能力补齐。

**⚙️ 工程流程变更**
- [PR #700](https://github.com/qhkm/zeptoclaw/pull/700)（已关闭）：按用户明确要求移除全部 GitHub Actions CI 检查（CI、E2E、PR Hygiene），保留 tag 触发的 release 和 Docker 发布，README 移除 CI 徽章，贡献者指南改为要求本地验证。对应 Issue [#699](https://github.com/qhkm/zeptoclaw/issues/699)。
- 多个 Dependabot CI Action 升级 PR（[#682](https://github.com/qhkm/zeptoclaw/pull/682)、[#684](https://github.com/qhkm/zeptoclaw/pull/684)）已关闭——在 CI 被移除的背景下，这些清理动作逻辑自洽。
- 存量 Issue 清理：[#629](https://github.com/qhkm/zeptoclaw/issues/629)（aarch64 7MB 二进制大小门禁）、[#545](https://github.com/qhkm/zeptoclaw/issues/545)（PR CI 编译可选集成特性）均关闭，后者与 CI 移除决策方向一致。

## 4. 社区热点

今日所有条目评论数均为 0，无讨论热点。最值得关注的内容性条目：
- [Issue #698 / PR #701](https://github.com/qhkm/zeptoclaw/pull/701)：本地弱模型工具调用是社区核心诉求（项目自称 edge runtime 却缺乏 schema 净化和 args 容错），维护者当天开 Issue、当天提交 PR 并关闭，响应极快。
- [PR #702](https://github.com/qhkm/zeptoclaw/pull/702)：登录限速是面向公网暴露面板用户的实际安全痛点。

## 5. Bug 与稳定性

| 问题 | 严重度 | 状态 |
|---|---|---|
| [RUSTSEC-2026-0285：Rustls 0.23.39 存在漏洞](https://github.com/qhkm/zeptoclaw/issues/697)（#697，P2-high） | 高 | ✅ 已修复，[PR #692](https://github.com/qhkm/zeptoclaw/pull/692) 升级至 0.23.45 |
| [面板密码登录无限暴力尝试](https://github.com/qhkm/zeptoclaw/pull/702)（#702） | 中-高 | 🔄 修复 PR 待合并 |
| [本地/严格后端工具调用易失败](https://github.com/qhkm/zeptoclaw/issues/698)（#698） | 中（P2-high） | ✅ [PR #701](https://github.com/qhkm/zeptoclaw/pull/701) 已关闭 |

## 6. 功能请求与路线图信号

- **#698（唯一新开 Issue）**：sanitize tool JSON schemas + 强制转换模型 tool-args——已被 #701 落地，表明“本地模型可用性”是当前明确的路线图方向。
- **CI 移除（#699/#700）**：暗示项目将验证责任转移给贡献者本地执行，同时保留 tag 发布流程；此决策可能影响后续 PR 质量保障，观察期信号。
- **战略信号**：#629 中“aarch64 6-7MB 二进制是机器人场景护城河”的表述，表明嵌入式/机器人（Pi/Jetson/Apple silicon）是核心差异化方向，尽管该门禁 Issue 已关闭。

## 7. 用户反馈摘要

今日条目均无评论，无法提炼社区用户反馈。从 Issue 描述可间接推断：
- 维护者本人主导了安全（Rustls、登录限速）和 CI 流程决策，“用户明确要求移除 CI”表明存在直接的用户/运营方输入。
- 弱本地模型工具调用失败是 ollama/local 用户的实际痛点（#698 问题描述详尽，含 MCP wrapper 裸 schema 泄露细节）。

## 8. 待处理积压

- [PR #702](https://github.com/qhkm/zeptoclaw/pull/702)（登录限速，安全修复）：待合并，建议优先处理。
- [PR #683](https://github.com/qhkm/zeptoclaw/pull/683)（rust-cache 2.9.1 → 2.9.2）：Dependabot PR 已挂起 3 天；鉴于 CI workflow 已移除，建议明确关闭或说明保留理由，避免依赖机器人 PR 无限堆积。
- 建议关注：CI 移除后，原本由 #545 提出的“可选集成特性编译漂移”风险将失去自动化防线，建议维护者以本地验证清单形式补偿。

---
*数据来源：GitHub API，统计窗口为过去 24 小时。*

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*