# OpenClaw 生态日报 2026-09-19

> Issues: 500 | PRs: 500 | 覆盖项目: 14 个 | 生成时间: 2026-09-19 03:44 UTC

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

# OpenClaw 项目动态日报 — 2026-09-19

## 1. 今日速览

OpenClaw 今日保持极高活跃度：过去 24 小时内 Issues 更新 500 条（新开/活跃 394，关闭 106），PR 更新 500 条（待合并 306，已合并/关闭 194），并发布了新版本 **v2026.9.5**。核心贡献者 @steipete 单日提交了大量性能优化与修复 PR，节奏非常密集。社区关注焦点集中在 **Gateway 稳定性（内存泄漏、事件循环阻塞、SQLite WAL 膨胀）** 与 **子代理（subagent）完成投递链路的消息丢失** 问题。整体看项目迭代速度快、维护响应积极，但 P0 级稳定性问题积压仍需持续消化。

## 2. 版本发布

### v2026.9.5 ([Release](https://github.com/openclaw/openclaw/releases))

- **更安全的升级与历史保留**：Doctor 现在会保留会话历史与重复修复状态；可完成带有无效保留历史的升级；避免反复拖延/停止仍在启动中的 Gateway（#149741, #149956, #148901, #149308 等）。
- **迁移注意**：本次主要修复升级路径问题。注意 #150201（Windows 更新快照失败，2026.9.3）已关闭，但 Windows 用户升级前建议先备份数据库；同时留意 #152252 报告的 config 迁移键导致旧 Gateway 启动失败（exit 78）问题。

## 3. 项目进展

今日 PR 活动以性能优化和修复合入/推进为主（合并+关闭 194 条），亮点包括：

- **Gateway 服务定义修复**：[#152120](https://github.com/openclaw/openclaw/pull/152120) 修复升级后遗留的过期 systemd/Windows 服务定义（关联 2026.9.4 Discord 上报的 `KillMode=mixed` 缺失），P1，已可由维护者审阅。
- **会话扩展性**：[#152366](https://github.com/openclaw/openclaw/pull/152366) 让 usage 报告在大量会话下保持响应；[#152399](https://github.com/openclaw/openclaw/pull/152399) 重构 agent 运行时准备与分发路径。
- **安全加固**：[#82950](https://github.com/openclaw/openclaw/pull/82950)（防止 exec/cron 正则灾难性回溯挂起授权）、[#119702](https://github.com/openclaw/openclaw/pull/119702)（compileSafeRegex 守护 patternProperties）持续推进。
- **发布工程**：[#152434](https://github.com/openclaw/openclaw/pull/152434)、[#152432](https://github.com/openclaw/openclaw/pull/152432) 修复 npm/ClawHub 发布重试被孤儿 run 阻塞的问题——2026.9.5 发布过程中实际遇到过。
- **语音/Talk**：[#152428](https://github.com/openclaw/openclaw/pull/152428)、[#152427](https://github.com/openclaw/openclaw/pull/152427) 修复 gateway-relay 语音会话的中断/过早结束问题。
- **Telegram**：[#151911](https://github.com/openclaw/openclaw/pull/151911) mention 门控群组保留历史讨论而不淹没上下文。

## 4. 社区热点

| Issue | 评论 | 核心诉求 |
|---|---|---|
| [#97616](https://github.com/openclaw/openclaw/issues/97616) hook/tool 子进程僵尸泄漏（P1） | 30 | 长期运行退化，仍缺修复 PR |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) Gateway 内存泄漏 350MB→15.5GB 致 OOM（P1） | 26 | 3 个月未修复，生产部署痛点 |
| [#149361](https://github.com/openclaw/openclaw/issues/149361) WebUI 性能与稳定性 Umbrella | 22 | 维护者主导的系统性梳理 |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) steer 模式无法中途注入消息（P1） | 20 | 已有 linked PR，等待合入 |
| [#149538](https://github.com/openclaw/openclaw/issues/149538) 632-agent 集群 Gateway ready 后事件循环饿死（P0） | 19 | 大规模部署可用性 |

**趋势解读**：社区最大声量集中在**长时间运行稳定性**与**subagent 消息投递丢失**（#137332、#143334、#121187、#118018、#138632 形成一个问题簇），反映 OpenClaw 已被大量用于 7×24 生产/集群场景，长尾生命周期 bug 成为最大摩擦源。

## 5. Bug 与稳定性（按严重度）

**P0**
- [#149538](https://github.com/openclaw/openclaw/issues/149538) main 分支 Gateway ready 后 `/health` 全部超时、RSS 持续攀升（632-agent 集群）— 无 fix PR
- [#143524](https://github.com/openclaw/openclaw/issues/143524) Windows SQLite WAL 增长至 2.8GB、阻塞启动 — 无 fix PR
- [#126821](https://github.com/openclaw/openclaw/issues/126821) 重建后 SQLite 15–24h 内再次损坏，出现“瘫痪但不退出”模式 — 无 fix PR
- [#143334](https://github.com/openclaw/openclaw/issues/143334) subagent 完成投递丢失，请求方卡死、用户消息饿死 — 无 fix PR
- [#152252](https://github.com/openclaw/openclaw/issues/152252)（新）config 写入迁移标记导致旧 Gateway 启动失败 exit 78 — 无 fix PR ⚠️ 升级风险
- [#142586](https://github.com/openclaw/openclaw/issues/142586)（已关闭）Doctor 检出孤儿外键但无恢复路径，曾阻塞 2026.7→2026.9.3 升级

**P1**
- [#148529](https://github.com/openclaw/openclaw/issues/148529)（已关闭）2026.9.4 集群启动 2s→12 分钟回归
- [#112423](https://github.com/openclaw/openclaw/issues/112423) 大型 SQLite transcript 清理阻塞事件循环 — 无 fix PR
- [#134993](https://github.com/openclaw/openclaw/issues/134993) 文件系统发现 busy-loop 打满单核
- [#152252 相关] [#126315](https://github.com/openclaw/openclaw/issues/126315) Apple 原生客户端会话路由 unowned 失败

## 6. 功能请求与路线图信号

- **动态模型发现**（[#10687](https://github.com/openclaw/openclaw/issues/10687)，👍3）：OpenRouter 等快速变动目录的完全动态化，社区呼声高但标记 needs-product-decision。
- **插件级密钥投影管控**（PR [#152161](https://github.com/openclaw/openclaw/pull/152161)）：exec 工具密钥环境变量的策略插件细粒度控制，属安全路线图方向，处于 needs proof。
- **备份排除模式**（[#40786](https://github.com/openclaw/openclaw/issues/40786)，已关闭）与 **日志轮转策略**（[#75380](https://github.com/openclaw/openclaw/issues/75380)）：运维可管理性诉求，后者仍未解决。
- **压缩/摘要语义保真观测**（PR [#152385](https://github.com/openclaw/openclaw/pull/152385)）：stacked PR 链（#152234→#152236→#152237），暗示 compaction 质量度量是下一阶段重点。
- **无障碍 TUI 选项**（[#9637](https://github.com/openclaw/openclaw/issues/9637)）与 **maxTurns 限制**（[#9912](https://github.com/openclaw/openclaw/issues/9912)）：长期开放的小型增强，有望随 #152429（ quieter settings UI）一类的 UX 批次纳入。

## 7. 用户反馈摘要

- **痛点集中在生产长期运行**：OOM/内存泄漏（#91588）、WAL 无限膨胀（#143524）、僵尸进程（#97616）是 Windows/WSL2 和 macOS 用户共同的高频抱怨。
- **升级路径信任不足**：2026.9.3/9.4 升级后 Windows 启动阻塞（#150201）、Doctor 阻塞迁移（#142586）让用户对升级持观望态度——2026.9.5 正是针对此发布。
- **消息丢失影响业务**：subagent 完成结果丢失（#143334、#138632）、steer 模式失效（#48003）、Discord 回复异常（#81484）直接打击 Telegram/Discord 集成用户。
- **正面信号**：维护者（@vyctorbrzezowski 等）主动建 Umbrella issue 梳理 WebUI 问题，PR 描述质量高（问题/影响/原因分明），社区报告附详细复现数据，生态协作成熟。

## 8. 待处理积压（提醒维护者）

- [#91588](https://github.com/openclaw/openclaw/issues/91588) 内存泄漏 — 6/09 开启，3 个月无 fix PR，标记 needs-maintainer-review
- [#97616](https://github.com/openclaw/openclaw/issues/97616) 僵尸进程 — 6/29 开启，仅 needs-info
- [#84983](https://github.com/openclaw/openclaw/issues/84983) cron 任务打满事件循环 — 5/21 开启，stale
- [#56217](https://github.com/openclaw/openclaw/issues/56217) 1Password 崩溃循环耗尽速率限制（P0）— 3/28 开启
- PR 侧：[#82950](https://github.com/openclaw/openclaw/pull/82950)（4 个月，P1 安全修复）、[#75299](https://github.com/openclaw/openclaw/pull/75299)（饥饿防护，stale）、[#119702](https://github.com/openclaw/openclaw/pull/119702)（等待作者）——三个安全/稳定性 PR 长期未合入，建议优先评估。

---
*数据来源：GitHub API（过去 24 小时窗口）。统计基于返回的 500 条 Issue/PR 更新样本。*

---

## 横向生态对比

# 个人 AI 助手/智能体开源生态横向对比分析报告

**数据日期：2026-09-19**

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态已进入**规模化生产采用与稳定性偿还期**：头部项目（OpenClaw、Zeroclaw、CoPaw）单日 Issue/PR 更新量达数百条，且社区反馈高度集中在 7×24 长期运行、集群部署、IM 渠道集成等生产场景。各项目普遍从“功能扩张”转向“可靠性、安全边界、成本控制”三条主线，提示这一品类已越过早期尝鲜阶段。同时生态出现明显分层：约三分之一项目（NullClaw、TinyClaw、EasyClaw 等）无活动或低活跃，市场正在向头部集中。安全治理（审批绕过、提示注入、暴力破解防护）首次在多个项目同步成为 P0/S0 级议题，标志着行业对 agent 执行权限边界的共识性焦虑。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | Release | 合并/关闭 | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 500（394 新/活跃） | 500（306 待合并） | ✅ v2026.9.5 | 194 | ⭐⭐⭐⭐ 活跃极高，但 P0 稳定性积压严重 |
| **CoPaw** | 20 | 43 | ✅ v2.2.2-beta.1 | 13 | ⭐⭐⭐⭐⭐ 响应闭环率最高，节奏紧凑 |
| **Zeroclaw** | 24 | 50 | ❌ | 8 | ⭐⭐⭐⭐⭐ 架构化推进（RFC/S0 审计），最稳健 |
| **Hermes Agent** | 50 | 50 | ❌ | 7 | ⭐⭐⭐⭐ 维护者深度参与，治理严谨 |
| **LobsterAI** | 6 | 21 | 🔄 release 分支推进中 | 7 | ⭐⭐⭐⭐ 企业驱动，修复合入率高 |
| **NanoBot** | 5 | 14 | ❌ | 5 | ⭐⭐⭐⭐ Bug 当天闭环，但贡献者单点风险 |
| **NanoClaw** | 7（新开） | 4 | ❌ | 0 | ⭐⭐ 输入活跃、消化停滞，高风险积压 |
| **ZeptoClaw** | 0 | 2 | ❌ | 1 | ⭐⭐⭐ 低强度高质量，单人维护 |
| **PicoClaw** | 1 | 4 | ❌ | 0 | ⭐⭐ stale 蔓延，review 滞后 |
| **IronClaw** | 0 | 2 | ❌ | 0 | ⭐⭐⭐ 低活跃但主线（沙箱隔离）持续推进 |
| **Moltis** | 0 | 1 | ❌ | 0 | ⭐ 社区接近冰点 |
| **NullClaw / TinyClaw / EasyClaw** | 0 | 0 | ❌ | 0 | — 无活动 |

**关键观察**：OpenClaw 的绝对量级（单日 500 条 Issue 更新）是第二名 Hermes 的 10 倍，但“关闭/新开比”仅约 0.27，消化能力反而弱于 CoPaw（0.43）和 Zeroclaw（0.5）。

---

## 3. OpenClaw 在生态中的定位

**优势：**
- **规模与生态位**：社区规模、issue 量级、外部集成（Telegram/Discord/语音 relay）覆盖面均为生态第一，已是事实上的“参照系”项目——LobsterAI 甚至在 PR 中直接处理 "OpenClaw workspace 初始化"，PicoClaw 新增 `opencode-go` provider，说明其他项目正在围绕 OpenClaw 做兼容层。
- **迭代速度**：核心贡献者 @steipete 单日高密度产出，v2026.9.5 针对升级路径问题快速响应发布。
- **使用深度**：632-agent 集群、fleet 部署等报告表明已被用于最激进的规模化场景。

**劣势/风险：**
- **P0 积压最重**：内存泄漏（#91588，3 个月无 fix）、WAL 膨胀（#143524）、subagent 消息丢失（#143334）等生产级问题无修复 PR，而同日 Zeroclaw 的 S0 审批绕过已闭环。
- **技术路线差异**：OpenClaw 走“大而全快速迭代”路线；Zeroclaw 走“架构先行”（RFC 原语、WASM 插件化、gateway 分离）；Hermes/CoPaw 介于两者之间；NanoBot/ZeptoClaw 走轻量单进程路线。
- **对比结论**：OpenClaw 赢在生态网络效应，但在长期运行稳定性的工程纪律上已被 Zeroclaw 反超，升级路径信任不足（#142586、#152252 exit 78）是其最大软肋。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **上下文压缩/淘汰的语义保真** | OpenClaw（compaction 观测 PR 链 #152385）、CoPaw（scroll eviction 丢用户轮次 #7836/#7872、base64 无界累积 #7853）、NanoClaw（PreCompact OOM #3716）、NanoBot（压缩通知可配置 #5780） | 长会话下压缩不应静默丢失关键信息，agent 应有预警/参与权 |
| **Subagent 可靠性与身份传递** | OpenClaw（投递丢失问题簇 #143334 等 5 个）、Hermes（委派通知滞留 #114456）、NanoBot（子代理架构重构 #5811）、Zeroclaw（#10963 会话身份转发）、LobsterAI（子代理可见性 #2703） | 多智能体编排的完成投递、结果透出、身份链路是全生态最普遍的痛点 |
| **执行安全与审批边界** | Zeroclaw（git 审批绕过 S0 两连）、CoPaw（持久性提示注入 #7859）、OpenClaw（正则回溯、密钥投影）、NanoBot（Jev Shell 预检 #5815）、ZeptoClaw（登录限速） | shell/git 命令分类器绕过、注入持久化、暴力破解防护——安全已成独立工程线 |
| **Token 成本与缓存** | Zeroclaw（缓存 TTL + 稳定前缀 #10959/#10960）、Hermes（prompt cache 失效、158 次视觉调用烧 4M tokens）、OpenClaw（usage 报告 #152366） | 细粒度预算控制与缓存命中率是重度用户核心诉求 |
| **运维可管理性**（存储/日志/升级） | NanoClaw（conversations/ 无限增长 #3735）、OpenClaw（WAL 2.8GB、日志轮转 #75380）、Hermes（fleet 重启标记残留 #109573）、LobsterAI（残留数据启动失败 #2719） | retention/rotation 策略与可信赖的升级路径是 7×24 部署的普遍缺口 |
| **Windows/多语言环境兼容** | Zeroclaw（PowerShell UTF-8 三连 PR）、Hermes（WSLg/退出码）、LobsterAI（PS 5.1/安全软件拦截）、OpenClaw（Windows 更新快照） | 非 Unix/非英文场景长期是二等公民，社区正在自发补齐 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Zeroclaw | CoPaw | Hermes | 其他 |
|---|---|---|---|---|---|
| **功能侧重** | 全渠道网关 + 集群规模化 | 审批安全 + SOP 可靠性原语 | Console/桌面体验 + 多租户 Hub | 桌面端 + Kanban 自动调度 | — |
| **目标用户** | 生产/fleet 运维者 | 安全敏感企业场景 | 个人→团队扩展 | 自托管 + 本地模型用户 | NanoBot/ZeptoClaw 面向轻量个人用户 |
| **架构** | Gateway 中心化 + subagent 群 | 编译期安全边界 → WASM 插件化 + gateway 分离（v0.9） | 插件生态 + Hub 多租户 | Fleet + 调度器 | LobsterAI/IronClaw 偏企业内部驱动（网易/NEAR） |

关键差异点：**Zeroclaw 是唯一以“人机交互可靠性原语”（提问原语、投递回执 RFC）为架构核心的项目**；**CoPaw 是多租户方向最激进的**（Hub 2.2.0 已落地）；**Hermes 是本地/自托管模型兼容投入最多的**（MoA、600k 默认值修正）；LobsterAI 和 IronClaw 带有明显企业背景，社区外部贡献通道相对不畅（内网 registry 构建卡死 6 个月未解）。

---

## 6. 社区热度与成熟度分层

- **超高频迭代层**：OpenClaw——功能与问题同步爆炸，处于“规模领先但稳定性债务偿还中”的成熟期阵痛。
- **高质量快速迭代层**：CoPaw、Zeroclaw、Hermes、NanoBot——Bug 响应闭环快（NanoBot 当天 4/4 闭环、CoPaw 约半数新 Bug 同日有 fix PR），处于**质量巩固期**，是当前生态健康度标杆。
- **企业驱动稳定层**：LobsterAI、IronClaw——版本节奏受内部发布分支驱动，社区外部参与弱。
- **消化瓶颈/维护滞后层**：NanoClaw（零关闭零合并、生产 OOM 无响应）、PicoClaw（stale 蔓延、半年 PR 被关闭）——贡献者流失风险已现。
- **静默层**：NullClaw、TinyClaw、EasyClaw、Moltis——无活动或接近冰点，预计将进一步边缘化。

---

## 7. 值得关注的趋势信号

1. **“静默失败”是全生态最强的用户抱怨**：消息丢失（OpenClaw #143334、Hermes #101380）、空回复（ZeptoClaw #703）、exit 0 假成功（NanoClaw #3855）、失败无原因（Zeroclaw #10759）——**可观测性与显式失败语义应成为智能体产品的默认设计**，而非可选功能。
2. **多智能体编排的“最后一公里”问题浮出水面**：五个项目同日报出 subagent 投递/身份/可见性问题，说明 agent 编排框架本身已成熟，瓶颈转移到**完成通知、结果透出、会话身份链路**这类分布式语义上。Zeroclaw 的投递回执 RFC 值得所有项目参考。
3. **安全从“沙箱”演进为“审批分类学”**：Zeroclaw 连续两个 git 全局选项绕过 S0、CoPaw 的跨会话持久注入，说明攻击面正从单次调用转向**持久化状态与命令解析边缘**——agent 框架需要系统性的命令分类审计，而非点状补丁。
4. **压缩/上下文管理进入“质量度量”阶段**：OpenClaw 建 compaction 保真观测、CoPaw 讨论淘汰平滑移交——单纯 token 阈值触发的压缩已被证明不够，**带语义保真度量的自适应压缩**是下一个竞争点。
5. **7×24 运维能力（retention/rotation/升级信任）是留存生产用户的分水岭**：各项目的最高严重度积压几乎全是此类问题；对开发者的启示是——个人 agent 产品的主要流失点不在功能，而在第三周的磁盘膨胀和第一次失败升级。
6. **生态向头部集中 + 互操作萌芽**：OpenClaw 成为事实兼容目标（LobsterAI、PicoClaw 主动适配），Agent Skills `.well-known` 标准化（Zeroclaw #4853 跟随 Cloudflare/Vercel）预示 skill 分发将像 npm 一样标准化，早接入者将获得生态红利。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报（2026-09-19）

## 1. 今日速览

过去24小时 NanoBot 保持较高活跃度：14 条 PR 更新（9 待合并、5 已合并/关闭）配 5 条 Issue 更新（4 新开/活跃、1 关闭），显示维护者响应速度良好——多个新报告的 Bug 当天即有对应 fix PR 提出。今日工作重心集中在 **WebUI 交互修复、多会话/生命周期正确性、Discord 渠道补齐** 三条线。无新版本发布。贡献者 @chengyongru 今日高产，提交 5 个 PR 并关闭 3 个，是社区核心推动力量。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日关闭/合并的 PR 共 5 个：

- **#5794** [fix] 跨会话响应串扰修复 — 修复用户在 Session A 发消息后快速切换到 Session B 时响应错投的问题（agent loop `_dispatch` 根因），直接对应 Issue #5798 的用户反馈。([PR #5794](https://github.com/HKUDS/nanobot/pull/5794))
- **#5800** Discord `replyToMessage` 与 Telegram 对齐 — 新增 `channels.discord.replyToMessage` 配置（默认关闭），覆盖普通/附件/流式响应的原生回复。同时关闭了 3 月提出的 Issue #1663。([PR #5800](https://github.com/HKUDS/nanobot/pull/5800))
- **#5810** WebUI 仅启用 WebUI 渠道时正确展示全部渠道目录。([PR #5810](https://github.com/HKUDS/nanobot/pull/5810))
- **#5812** 显式恢复续跑消息可达 agent turn processor，修复 WebUI 恢复动作失效。([PR #5812](https://github.com/HKUDS/nanobot/pull/5812))
- **#5495** [已关闭，标注 conflict] 原生 Linear Agent 渠道 — 该大型 feature PR（OAuth+PKCE、webhook 持久化队列、WebUI 面板）被关闭，存在冲突，后续可能需重新提交。([PR #5495](https://github.com/HKUDS/nanobot/pull/5495))

**净进展评估**：跨会话串扰修复 + Discord 回复功能落地是最实质的推进；Linear 渠道 PR 关闭是本日唯一明显挫折。

## 4. 社区热点

- **Issue #5798（会话串扰）**：用户报告 v0.3.5 出现回复串到不相干会话的回归（v0.3.0 无此问题），Windows + Python 3.12 环境。PR #5794 已合并，预计随下版本发布修复。([Issue #5798](https://github.com/HKUDS/nanobot/issues/5798))
- **PR #5780（上下文压缩通知）**：贡献者质疑 #5656 引入的后台自动压缩通知是否符合设计意图，改为静默处理并保留 `/compact` 提示，引发关于默认行为可配置性的讨论。([PR #5780](https://github.com/HKUDS/nanobot/pull/5780))
- **PR #5803（Telegram 改进）**：单 PR 包含富文本换行、`topic_id` 暴露、typing 状态尊重 topic 三项改进。([PR #5803](https://github.com/HKUDS/nanobot/pull/5803))

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | 问题 | 状态 |
|---|---|---|
| 高 | **#5798** 会话串扰（跨会话回复错投，v0.3.5 回归） | ✅ fix PR #5794 已合并 |
| 高 | **#5808** `/stop` 后 WebUI follow-up 在网关重启后被恢复日志错误重放 | ✅ fix PR #5809 已提出 |
| 中 | **#5806** Discord 停止后 reaction 任务泄漏（`_working_emoji_tasks` / `_pending_reactions` 未清理） | ✅ fix PR #5807 已提出 |
| 中 | **#5771** iOS 移动端会话列表需点两次才能打开 | ✅ fix PR #5805 已提出（隐藏操作区拦截点击） |
| 低 | PR #5814 修复 WebUI 中间回答页脚空隙 | 待合并 |

值得肯定的是：**4 个新 Bug 全部当天有对应 fix PR**，维护响应链路非常健康。

## 6. 功能请求与路线图信号

- **#5815 Jev Shell 防护（exec 安全预检）**：可选 `tools.exec.jevGuard`，基于 OpenRouter Decisions API 批量预检 exec 调用——表明项目在向 **执行安全/沙箱防护** 方向扩展。([PR #5815](https://github.com/HKUDS/nanobot/pull/5815))
- **#5811 子代理架构重构**：子代理改走私有会话 + 共享 AgentLoop 与压缩路径，移除独立 runner——核心架构层面的收敛，可能为后续子代理功能铺路。([PR #5811](https://github.com/HKUDS/nanobot/pull/5811))
- **Issue #1663 已随 PR #5800 关闭**，渠道功能对齐（Telegram ↔ Discord）是明确方向；Linear 原生渠道（#5495）虽关闭但需求真实，预计会以新 PR 形式回归。

## 7. 用户反馈摘要

- **多会话并发的可靠性是核心痛点**：#5798 / #5794 均指向用户同时使用多个会话时响应错投，说明多会话已是主流使用方式。
- **移动端 WebUI 体验欠佳**：#5771 反映 iOS 上 UI 响应性问题，用户直接感知为“列表无反应”。
- **通知噪音引发不满**：#5780 中用户直言自动压缩通知“相当烦人”，希望有配置开关——提示默认 UX 应更克制。
- **版本回归敏感**：用户能精确指出 v0.3.0→v0.3.5 的行为差异，说明存在粘性高的长期用户群。

## 8. 待处理积压

- **PR #5495（Linear Agent 渠道）**：历时近一个月、功能完整的大 PR 被关闭（冲突），建议维护者明确后续路径，避免贡献者流失。
- **Issue #5798**：fix 已合并但 Issue 仍为 OPEN，建议确认修复后关闭并注明修复版本，安抚受影响用户。
- **PR #5780 / #5803**：待合并且涉及行为变更（通知、Telegram 渲染），建议尽快评审合入，避免与主线冲突累积。

---

**健康度小结**：Bug 响应闭环快（当天报告→当天 fix PR）、贡献者活跃集中但结构略有单点风险（@chengyongru 承担今日大部分 PR），整体处于健康的快速迭代期。建议下版本（预计 0.3.6）重点打包会话串扰与 WebUI 稳定性修复。

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目日报 · 2026-09-19

## 1. 今日速览

项目整体处于**高活跃度、稳健推进**状态。过去 24 小时 Issues 更新 24 条（新开/活跃 16、关闭 8），PR 更新 50 条（待合并 42、已合并/关闭 8），无新版本发布。今日主线清晰：**安全类修复持续落地**（git 命令审批绕过两大 S0 漏洞）、**Agent Skills 生态标准化推进**（`.well-known` 发现索引）、以及两条重量级 RFC（出站消息回执、人机问答原语）进入维护者评审。核心贡献者 @Audacity88、@JordanTheJet 产出密集，社区新面孔 @eppofahmi、@NiuBlibing、@iceHub82 带来高质量贡献，社区健康度良好。

## 2. 版本发布

今日无新版本发布。v0.8.6 / v0.9.0 的交付进度由 tracker [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) 持续追踪（Phase 2 runtime 与 Phase 3 gateway 分离）。

## 3. 项目进展

今日关闭的 8 个 Issue / PR 中，值得关注：

- **#9627（已关闭）** [git 写操作通过 `-C` / `--git-dir` 全局选项绕过风险分类器](https://github.com/zeroclaw-labs/zeroclaw/issues/9627) — S0 级安全漏洞（审批门禁绕过）完成修复，这是 shell/git 安全边界的重大补强。
- **#10877（已关闭）** [sops/run-detail 返回保留的 run 级失败原因](https://github.com/zeroclaw-labs/zeroclaw/pull/10877) — 对应关闭 #10759，SOP 运行详情不再返回“失败但无解释”的空步骤。
- **#10736（已关闭）** [流式输出前失败时跳过非流式回退](https://github.com/zeroclaw-labs/zeroclaw/issues/10736) — Reliable provider 回退路径修复落地。
- **#10853（已关闭）** [OpenCode session header 跟进事项](https://github.com/zeroclaw-labs/zeroclaw/issues/10853) — #10604 评审遗留的三项非阻塞跟进全部完成。
- **#10667（已关闭）** [ZeroCode 流式响应重复渲染](https://github.com/zeroclaw-labs/zeroclaw/issues/10667) — TUI 客户端体验类 S2 修复。
- **#10772（已关闭）** [zeroclaw-eval 归档测试与 workspace fixtures 解耦](https://github.com/zeroclaw-labs/zeroclaw/issues/10772) — 发布物测试边界明确化。

**进展评估**：安全审批链路（#9627 + 今日新报 #10966 说明团队正在系统性审计 git 全局选项解析）、SOP 可观测性、provider 回退韧性三条线均向前推进，节奏稳定。

## 4. 社区热点

- **[#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853) 从 `.well-known` agent-skills 发现索引安装 skills**（8 评论，进行中）— 跟随 Agent Skills 组标准化进程（Cloudflare 内部使用、Vercel 已在 npm 支持），对应 XL 级 PR [#10944](https://github.com/zeroclaw-labs/zeroclaw/pull/10944) 已开、锁定 schema 0.2.0。诉求：让 skill 分发像 npm 包一样标准化。
- **[#10930](https://github.com/zeroclaw-labs/zeroclaw/issues/10930) RFC：agent 向人类提问的统一持久原语** 与 **[#10929](https://github.com/zeroclaw-labs/zeroclaw/issues/10929) RFC：出站消息投递回执** — @JordanTheJet 连发两份架构级 RFC，均基于已有的 SOP 审批门持久化机制做泛化。信号明确：项目正在为**长生命周期人机交互可靠性**打地基，很可能构成 v0.9 gateway 阶段的核心语义。
- **[#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) v0.8.6/v0.9.0 交付 tracker** 持续活跃，是路线图的单一事实来源。

## 5. Bug 与稳定性（按严重程度）

| 严重度 | Issue | 状态 | Fix PR |
|---|---|---|---|
| **S0** | [#10966](https://github.com/zeroclaw-labs/zeroclaw/issues/10966) `git --attr-source` 可将变更型子命令藏匿于审批分类之外（**今日新报**） | OPEN / accepted | 尚无，但与 #9627 同域，修复路径清晰 |
| **P1** | [#10908](https://github.com/zeroclaw-labs/zeroclaw/issues/10908) 工具结果文本中的图像标记被无溯源提升为附件，原始文本被剥离 | OPEN / blocked | [#10938](https://github.com/zeroclaw-labs/zeroclaw/pull/10938)（XL，改为显式声明 tool attachments） |
| **P1** | [#10643](https://github.com/zeroclaw-labs/zeroclaw/issues/10643) 有界子代理循环继承工具时审批管理器缺失，fail-closed 未生效 | in-progress | 进行中 |
| S2 | [#10952](https://github.com/zeroclaw-labs/zeroclaw/issues/10952) seam sanitizer 重写签名 reasoning，Anthropic 拒绝重放 thinking | in-progress | [#10953](https://github.com/zeroclaw-labs/zeroclaw/pull/10953) 已开 |
| S2 | [#10950](https://github.com/zeroclaw-labs/zeroclaw/issues/10950) `cost.warn_at_percent` 预算警告被运行时忽略 | OPEN | 待修 |
| S2 | [#10951](https://github.com/zeroclaw-labs/zeroclaw/issues/10951) ZeroCode Config 保存后重复刷新字段列表 | in-progress | [#10964](https://github.com/zeroclaw-labs/zeroclaw/pull/10964) 已开 |
| S2 | [#10948](https://github.com/zeroclaw-labs/zeroclaw/issues/10948) interruption-scope key 跨组件边界碰撞 | in-progress | [#10958](https://github.com/zeroclaw-labs/zeroclaw/pull/10958)（长度前缀编码）已开 |

**稳定性提示**：[#10965](https://github.com/zeroclaw-labs/zeroclaw/pull/10965) 表明 master 上存在 detached peer turns 嵌套 cost scope 导致测试栈溢出的问题，该 XS PR 正在修复，建议优先合并。

## 6. 功能请求与路线图信号

- **Runtime 插件化（#8850）**：从编译期 feature 迁移到 WASM 运行时插件，配套 [#9134](https://github.com/zeroclaw-labs/zeroclaw/pull/9134)（精确字节准入 + SHA-256 绑定）持续推进 — 二进制瘦身 + 免重编译扩展是明确方向。
- **通道溯源（[#10891](https://github.com/zeroclaw-labs/zeroclaw/issues/10891)）**：#6971 契约的首个实现切片，属于消息可信度基础建设。
- **Delegate 增强**：[#10963](https://github.com/zeroclaw-labs/zeroclaw/issues/10963)（向子代理转发会话身份）、[#10962](https://github.com/zeroclaw-labs/zeroclaw/issues/10962)（gateway /ws/chat 流携带工具结果 payload）— 来自社区新贡献者，直接改善多代理与客户端可观测体验，采纳概率高。
- **Shell/编码健壮性三连**（@NiuBlibing）：[#10955](https://github.com/zeroclaw-labs/zeroclaw/pull/10955)（输出编码检测）、[#10956](https://github.com/zeroclaw-labs/zeroclaw/pull/10956)（平台默认 shell 探测）、[#10954](https://github.com/zeroclaw-labs/zeroclaw/pull/10954)（PowerShell UTF-8）— 对 Windows/非英文用户价值显著。
- **Anthropic 缓存优化**（@iceHub82）：[#10960](https://github.com/zeroclaw-labs/zeroclaw/pull/10960)（`ZEROCLAW_CACHE_TTL`）+ [#10959](https://github.com/zeroclaw-labs/zeroclaw/pull/10959)（tool specs 排序稳定缓存前缀）— 直击成本问题，cache-write 1.25x 溢价场景。

## 7. 用户反馈摘要

- **成本可见性是痛点**：#10950 预算警告失效、#10959/#10960 缓存无法命中，反映重度用户对 token 成本敏感，希望细粒度预算控制和缓存复用真正生效。
- **Windows / 多语言环境体验欠缺**：编码检测、PowerShell UTF-8、默认 shell 解析三个 PR 均由社区自发提交，说明官方对非 Unix/非英语场景覆盖不足。
- **客户端可观测性不足**：#10962 用户抱怨 /ws/chat 只看到工具“开始/结束”帧而拿不到结果，#10759 用户遇到“运行失败但无任何原因”，说明**失败原因与工具结果的透出**是普遍诉求。
- **多代理场景身份丢失**：#10963 指出 delegate 子代理只拿到 LLM 撰写的 context，会话身份不传递，实际使用中子代理“不知道自己为谁工作”。

## 8. 待处理积压

- **[#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853)**（3 月开，标记 blocked/parking-lot）— 依赖上游 agentskills 标准化 PR #254，建议关注上游进展及时解冻。
- **[#10084](https://github.com/zeroclaw-labs/zeroclaw/pull/10084)**（8 月开，XL）— WhatsApp passkey 门禁修复，长期待审，阻塞 WhatsApp 设备链接用户，建议维护者安排评审。
- **[#9134](https://github.com/zeroclaw-labs/zeroclaw/pull/9134)**（7 月开，needs-author-action）— 插件字节准入，插件化主线关键件。
- **[#10801](https://github.com/zeroclaw-labs/zeroclaw/pull/10801)**（XL，needs-maintainer-review）— ZeroCode 通知延迟会话重载，涉高风险客户端行为变更。
- **[#8691](https://github.com/zeroclaw-labs/zeroclaw/issues/8691)** — ADR 清点 tracker，文档债需要持续投入。

**健康度小结**：Issue 关闭/新开比 0.5，PR 合并比 0.16（待合并池较大，含多个 XL 长周期 PR 属正常），S0 漏洞响应迅速且正在做系统性审计，整体呈健康的高强度开发态。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-09-19

## 1. 今日速览

Hermes Agent 今日保持高度活跃：过去 24 小时内 Issues 更新 50 条（新开/活跃 27，关闭 23），PR 更新 50 条（待合并 43，已合并/关闭 7），无新版本发布。项目当前处于**高强度修复与治理阶段**：维护者 @teknium1 正在逐行复核社区贡献的 PR 分类/清理表格（#113887、#114510），显示团队对 issue 队列质量的高度重视。新增 Bug 集中在**桌面端（WSLg/Windows）、会话状态（sessions）与压缩配置**三大方向，同时出现了 1 个 P1 级数据库完整性问题（#115571）。修复 PR 产出速度良好，今日新开的多个 P2 Bug 已在同日有对应修复 PR 提交。

## 2. 版本发布

今日无新版本发布。（最近版本仍为 v0.21.3，2026-09-14）

## 3. 项目进展

今日已合并/关闭的关键 PR：

- **[PR #114968](https://github.com/NousResearch/hermes-agent/pull/114968)**（已关闭）：桌面端群聊消息窗口溢出时，Bot Mode 成员现在能看到“…省略了 N 条历史消息”的提示，房间 `ui_meta` 镜像记录被裁剪的条目，替代静默丢弃历史。
- **[PR #114961](https://github.com/NousResearch/hermes-agent/pull/114961)**（已关闭）：修复 WSLg 下 v0.21.3 强制 Wayland 导致桌面窗口无法打开的问题——renderer 启动失败时自动回退 X11 重启一次（对应 Issue #114615）。
- **[PR #102365](https://github.com/NousResearch/hermes-agent/pull/102365)**（已关闭）：性能优化——Sessions 侧边栏启动阻塞 ~41 秒的问题，`list_profiles()` 不再递归扫描每个 profile 的 skills 树。
- **[PR #114589](https://github.com/NousResearch/hermes-agent/pull/114589)**（已关闭）：Kanban 调度器获得独立 review-lane 失败预算、终端 provider 错误快速熔断、Windows 退出码解码（实现 #114587 提案）。

今日新提交的重要待合并 PR（含核心维护者产出）：

- **[PR #115626](https://github.com/NousResearch/hermes-agent/pull/115626)**：修复第二个 Codex 账号的凭据被第一个账号覆盖的问题——多账号 credential pool 关键修复。
- **[PR #115606](https://github.com/NousResearch/hermes-agent/pull/115606)**：MoA 聚合器在严格交替对话模板（llama.cpp/vLLM）下的 400 错误恢复。
- **[PR #115608](https://github.com/NousResearch/hermes-agent/pull/115608)**：Weixin 限流发送正确归类为 flood_control，触发 delivery ledger 重投递。
- **[PR #115614](https://github.com/NousResearch/hermes-agent/pull/115614)**：TUI 网关 deferred/cold resume 在 launch-profile 作用域下解析覆盖项（修 #115607）。

**整体评估**：今日推进约 7 个合并/关闭 + 多个高质量修复 PR，稳定性与桌面端体验持续改善，进度节奏健康。

## 4. 社区热点

- **[#113887](https://github.com/NousResearch/hermes-agent/issues/113887)**（9 评论，已关闭）：社区贡献者 @cervantesh 的 PR 分类重构表（268 行），经 @teknium1 对 113 条“被取代”记录逐条复核后修正。反映项目 issue 量级已大到需要系统化清理流程，维护者亲自复核体现治理严谨。
- **[#109573](https://github.com/NousResearch/hermes-agent/issues/109573)**（8 评论，P2）：遗留的 `fleet_restart_pending` 标记文件在重启义务已履行后仍报“未完成重启”——影响 fleet 运维用户的升级可靠性。
- **[#69495](https://github.com/NousResearch/hermes-agent/issues/69495)**（6 评论，P2，7 月至今）：cron 注入的 `[SILENT]` 前导指令导致 LLM 直接不执行任务且**无法自定义**——长期未决，诉求是给用户关闭/定制 cron preamble 的能力。
- **[#114526](https://github.com/NousResearch/hermes-agent/issues/114526)**（5 评论，已关闭）：`hermes plugins install` 克隆公开插件仓库时 git 误发认证提示——插件生态可用性受阻，已处理。

## 5. Bug 与稳定性（按严重程度）

| 级别 | Issue | 描述 | Fix PR |
|---|---|---|---|
| **P1** | [#115571](https://github.com/NousResearch/hermes-agent/issues/115571) | v0.21.0 worker transcript 写入失败，`messages` 表结构损坏（行 ID 乱序）、索引损坏 | ❌ 暂无 |
| **P0** | [#114456](https://github.com/NousResearch/hermes-agent/issues/114456) | 异步委派完成通知滞留 ~24 分钟；`/stop` 不重启队列处理；历史中插入消息使 prompt cache 失效 | ❌ 暂无 |
| P2 | [#115572](https://github.com/NousResearch/hermes-agent/issues/115572) | `_apply_live_compression_config` NameError：`is_truthy_value` 未定义，**所有压缩引擎的实时配置生效均崩溃**（今日新报） | ❌ 暂无 |
| P2 | [#115609](https://github.com/NousResearch/hermes-agent/issues/115609) | Windows 桌面附件预览 ENOENT，home 相对路径不回退到附件目录（今日新报） | ❌ 暂无 |
| P2 | [#115556](https://github.com/NousResearch/hermes-agent/issues/115556) | 非终态委派批次在桌面 UI 渲染为幽灵“子代理运行中”（今日新报） | ❌ 暂无 |
| P2 | [#115623](https://github.com/NousResearch/hermes-agent/issues/115623) | `build_models_payload` 在内置与自定义 provider 指向同一上游时清空内置行模型（今日新报） | ❌ 暂无 |
| P2 | [#101380](https://github.com/NousResearch/hermes-agent/issues/101380) | 微信语音附件静默丢弃，`send_voice` 拒绝 `is_voice` 参数 | 部分（#115608 相邻域） |

今日关闭的稳定性修复：cron 外部 worker 符号链接解析失败（#112729）、CI sqlite 段错误（#113186）、anthropic provider 误报 content_filter（#113689）、Codex OAuth token 竞态（#114012，配套 fix PR #115626 已提交）。

## 6. 功能请求与路线图信号

- **移动端 App**（[#50745](https://github.com/NousResearch/hermes-agent/issues/50745)）：iOS 远程接续桌面会话的需求，评论活跃但被标记 duplicate——官方似已有内部规划。
- **cron preamble 可定制化**（#69495）：用户需要控制注入指令；结合近期 cron 模块的大量重构（#113887、#114510），可能随 cron 治理批次落地。
- **本地模型友好默认值**（[#114645](https://github.com/NousResearch/hermes-agent/issues/114645)，已关闭）：`background_review.max_input_tokens` 默认 600k 对本地模型过大——与 #115606（MoA 本地模型兼容）共同表明**本地/自托管模型支持**是明确方向。
- **Kanban 调度增强**（PR #114589 已关闭/落地）：独立 review-lane 预算等三项改进，显示自动化代理调度是活跃演进区。

## 7. 用户反馈摘要

- **痛点集中于“静默失败”**：多个高评论 Issue 描述无报错的功能失效——语音附件静默丢弃（#101380）、Langfuse 占位 key 零上报（#110053）、群聊历史静默截断（PR #114968 修复）。用户强烈期望**可观测性与明确报错**。
- **升级/安装路径脆弱**：Windows Scheduled Task 误识别（#100645）、fleet 重启标记残留（#109573）、TrueNAS Docker 升级后配置不可用（#114697）——自托管与 Windows 用户是升级问题重灾区。
- **成本敏感**：#112095 中子代理 15 分钟内 158 次视觉调用烧掉 ~4M input tokens（已关闭），用户对重复调用防护和 prompt cache 失效（#114456）高度敏感。
- **正面信号**：企业用户（如 SSCITServices fleet 运维，#111910）在生产环境使用 Kanban 调度，表明项目已有实际生产采用。

## 8. 待处理积压

- **[#69495](https://github.com/NousResearch/hermes-agent/issues/69495)**（P2，7-22 开启至今近 2 个月，needs-decision）：cron [SILENT] 注入问题——建议维护者尽快给出决策。
- **[#50745](https://github.com/NousResearch/hermes-agent/issues/50745)**（6 月开启）：移动端需求长期挂起，建议明确状态（规划中/拒绝）。
- **[#109573](https://github.com/NousResearch/hermes-agent/issues/109573)**（P2，8 条评论）：fleet 重启标记问题影响升级可靠性，尚无关联 fix PR。
- **[#114456](https://github.com/NousResearch/hermes-agent/issues/114456)**（P0）：异步委派通知滞留 + cache 失效，涉及三个风险标签（session-state/message-delivery/caching），应优先排期。
- 长期 PR：**[#74440](https://github.com/NousResearch/hermes-agent/pull/74440)**（7-29，needs-decision）、**[#82935](https://github.com/NousResearch/hermes-agent/pull/82935)**（8-10，飞书位置消息）、**[#86053](https://github.com/NousResearch/hermes-agent/pull/86053)**（8-14，nanoid 安全升级 GHSA-2v37-7h3g-55p8——安全类建议尽快合并）。

---
**健康度小结**：Issue 关闭率（23/50）与 PR 吞吐良好，维护者深度参与复核；风险点为 P1 数据库损坏报告（#115571）无修复、以及“静默失败”类 Bug 的系统性 UX 缺口。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报（2026-09-19）

## 1. 今日速览

PicoClaw 今日整体活跃度处于**中等偏低**水平：过去 24 小时内共 1 条 Issue 更新、4 条 PR 更新、无新版本发布。值得注意的是，今日动态中有多条记录被标记为 `[stale]`（Issue #3355、PR #3371），显示部分贡献和问题正面临自动过期关闭的风险。PR #1349（QQ 频道附件增强）在创建半年后被关闭，是今日最重要的一条动态。项目维护节奏偏慢，社区贡献的待合并 PR 积压达 3 条。

## 2. 版本发布

今日无新版本发布。最新可用版本仍为 nightly 构建系列（用户报告使用 `nightly-50-gbbf6893c`）。

## 3. 项目进展

**已关闭：**
- [PR #1349](https://github.com/sipeed/picoclaw/pull/1349) `feat(qq): support parsing and replying to more attachment types` — 该 PR 创建于 2026-03-11，历经半年后于今日被关闭（未合并）。其内容包括：解析 QQ 频道 emoji 结构、处理语音/图片/视频/文件消息、回复本地附件（先上传后发送）、优先使用 Markdown 回复并降级。关闭原因未在摘要中说明，半年未合并即被关闭可能意味着方向调整或代码已过时，QQ 频道的附件能力增强需求仍未落地。

**待合并（3 条，均处于 OPEN 状态）：**
- [PR #3347](https://github.com/sipeed/picoclaw/pull/3347) 修复 Web UI 大量文本时的卡顿问题，已实测有效（桌面+移动端 Brave 浏览器），属高价值体验修复。
- [PR #3371](https://github.com/sipeed/picoclaw/pull/3371) 新增 `opencode-go` provider，带 session header 支持，⚠️ 已标记 stale。
- [PR #3222](https://github.com/sipeed/picoclaw/pull/3222) DeltaChat 通道重构，净减 200 行代码，包括重命名 `invite_link` → `join_invite_link`（含轻微 API 破坏性变更）。

**整体评估：** 今日无合并，项目实质进展有限，主要动态是清理过期贡献。

## 4. 社区热点

- [Issue #3355](https://github.com/sipeed/picoclaw/issues/3355) `[BUG] 连接飞书报错 - 附解决方案` 是今日唯一活跃 Issue（2 条评论）。用户 @ttghub 报告配置飞书通道时出现 `config.json contains unknown field(s): channel_list.feishu.app_id` 错误，并**自行附上了解决方案**。该 Issue 于 09-01 创建，今日更新但被标记 `[stale]`。背后诉求：飞书通道配置字段校验与文档/实际 schema 不一致，用户容易踩坑；附解决方案的高质量报告未获官方确认回应，反映飞书用户群体（企业协作场景）的支持缺口。

今日无高 👍、高评论的热门讨论，社区热度整体平淡。

## 5. Bug 与稳定性

按严重程度排列：

1. **🟡 飞书通道配置报错（Issue #3355）** — `unknown field: channel_list.feishu.app_id`，导致用户无法接入飞书。用户已给出 workaround，但尚无官方 fix PR。影响面：飞书用户无法完成通道初始化。链接：https://github.com/sipeed/picoclaw/issues/3355
2. **🟡 Web UI 长文本卡顿（PR #3347）** — 聊天区文本量大时界面卡顿，影响桌面与移动端。**已有 fix PR（#3347）待合并**，社区测试通过。链接：https://github.com/sipeed/picoclaw/pull/3347

今日无崩溃或回归类报告。

## 6. 功能请求与路线图信号

- **OpenCode Go provider 支持（PR #3371）**：为绕过 OpenCode Go 的 endpoint 变化而新增专用 provider，自动按模型 ID 路由并携带 `x-opencode-session` header。该需求直接源于上游服务变更，具备明确用户场景，但已 stale，若不处理可能流失相关用户。
- **QQ 频道富媒体消息（PR #1349，已关闭）**：附件/语音/视频/Markdown 回复能力，需求真实但贡献被关闭，建议维护者说明是否以其他方式重做，或引导原作者重提。
- **DeltaChat 简化（PR #3222）**：去除遗留特性和硬编码密码配置（改为 jsonrpc secrets），体现安全加固方向，信号积极。

**下一版本可能的候选：** PR #3347（UI 性能修复）和 #3222（重构减码）合并风险低、收益明确，最可能先行。

## 7. 用户反馈摘要

- **飞书接入用户（@ttghub）**：按文档配置即报错，体验受挫，但主动贡献解决方案，说明用户粘性高、愿意协作；痛点在于配置 schema 与报错信息不够友好。
- **Web UI 用户（@iMilnb，PR #3347 作者）**：长对话场景下界面明显卡顿，影响日常使用；其自行定位并修复问题（虽自述非 TS/Node 开发者），反映社区动手能力强。
- **多 provider 用户**：依赖 OpenCode Go 的用户需要专用 provider 才能继续使用，反映 PicoClaw 用户对模型来源灵活性的高诉求。

## 8. 待处理积压

| 条目 | 状态 | 建议 |
|---|---|---|
| [PR #1349](https://github.com/sipeed/picoclaw/pull/1349) QQ 附件增强 | 已关闭（未合并），历时 6 个月 | 建议维护者说明关闭原因，避免社区贡献流失 |
| [PR #3371](https://github.com/sipeed/picoclaw/pull/3371) opencode-go provider | ⚠️ stale，待 review | 时效性强（上游已变更），建议尽快 review |
| [PR #3222](https://github.com/sipeed/picoclaw/pull/3222) deltachat 重构 | 待合并近 3 个月 | 含命名变更，需明确迁移说明后合并 |
| [Issue #3355](https://github.com/sipeed/picoclaw/issues/3355) 飞书配置报错 | ⚠️ stale，用户已附方案 | 建议官方确认方案并落文档/fix |

**健康度小结：** 社区贡献意愿良好（多个高质量外部 PR/Issue 附方案），但 review 与合并节奏明显滞后，stale 标记增多是健康度预警信号，建议维护者集中处理积压。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报 — 2026-09-19

## 1. 今日速览

今日 NanoClaw 处于**社区问题密集上报期**：过去 24 小时新增 7 条 Issue、4 条待合并 PR，无版本发布，也无 Issue 关闭或 PR 合并。新增 Issue 集中在 v2.3.0 的 CLI 配置校验缺失与 `CLAUDE.md` 生成产物管理问题，而长期悬置的 `conversations/` 目录无限增长系列问题（#3735、#3716、#3714）今日仍有活动但无官方响应。待合并 PR 主要来自外部贡献者，聚焦 Codex 传输层可靠性与 Slack token 轮换，质量较高但尚无 core team 审查迹象。整体看，项目**输入活跃、消化滞后**，积压问题正在累积。

## 2. 版本发布

过去 24 小时无新版本发布。（最新公开 Issue 提及版本为 2.3.0）

## 3. 项目进展

今日无 PR 合并、无 Issue 关闭，**主线代码无净推进**。但待合并队列中有 4 个 PR 值得关注：

- **PR #3851 / #3850**（[@ionescu77](https://github.com/nanocoai/nanoclaw/pull/3851)）：修复 Codex Responses 传输层在代理环境下 WebSocket 不可靠的问题，提供可配置/HTTP SSE 回退方案，是对 Issue #3338 的响应，覆盖 7 个 area 标签，是当前影响面最大的候选修复。
- **PR #3852**（[@samueldg](https://github.com/nanocoai/nanoclaw/pull/3852)）：修复 Slack 应用配置 token 12 小时过期导致 direct-mode 配置失败的问题，补齐 `tooling.tokens.rotate` 调用。
- **PR #3420**（[@gavrielc](https://github.com/nanocoai/nanoclaw/pull/3420)）：macOS 状态栏插件适配新 slug 命名（`com.nanoclaw-v2-<installSlug>`），修复旧安装上监视不存在的服务的问题，自 8-20 开放至今未合并。

若这批 PR 合入，将显著改善代理环境部署与 Slack 集成两条路径的稳定性。

## 4. 社区热点

讨论最活跃的是 **`conversations/` 归档无限增长问题群**，三条相关 Issue 今日均有更新：

- [#3735](https://github.com/nanocoai/nanoclaw/issues/3735)：每次 compaction 写入 markdown 归档，无保留策略、无上限，fleet 规模部署下持续膨胀（3 条评论）。
- [#3716](https://github.com/nanocoai/nanoclaw/issues/3716)：PreCompact hook 每次触发全量重写对话历史文件，被报告为**生产环境 OOM 崩溃循环的根因**（3 条评论）。
- [#3714](https://github.com/nanocoai/nanoclaw/issues/3714)：三个运维端环境变量（auto-compact 窗口、transcript 轮换）从未透传进 session 容器，是 #1820 的回归性后续。

**诉求共性明确**：多实例/长生命周期部署的运维用户（如 @TO-maschenborn 的 fleet、@DawoudIO 的生产环境）需要磁盘/内存上限控制与配置透传能力。这是当前社区最强烈且尚未被满足的信号。

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 摘要 | Fix PR |
|---|---|---|---|
| 🔴 高 | [#3716](https://github.com/nanocoai/nanoclaw/issues/3716) | PreCompact 全量重写归档导致生产 OOM 崩溃循环 | ❌ 无 |
| 🔴 高 | [#3455](https://github.com/nanocoai/nanoclaw/issues/3455) | host-sweep claim-stuck 看门狗（60s）误杀合法长任务，会话永久阻塞且无法自愈，重试复现同一失败 | ❌ 无 |
| 🟠 中 | [#3735](https://github.com/nanocoai/nanoclaw/issues/3735) | conversations/ 归档无限增长 | ❌ 无 |
| 🟠 中 | [#3714](https://github.com/nanocoai/nanoclaw/issues/3714) | 运维 env 覆盖未透传至 session 容器 | ❌ 无 |
| 🟡 低 | [#3855](https://github.com/nanocoai/nanoclaw/issues/3855) | `groups config update --model` 不校验任意字符串，且无法发现合法模型名 | ❌ 无 |
| 🟡 低 | [#3854](https://github.com/nanocoai/nanoclaw/issues/3854) | 编辑生成产物 `groups/<folder>/CLAUDE.md` 被静默丢弃，`groups restart` 无提示 | ❌ 无 |

**今日报告的 3 个新 Bug（#3853–#3855）均无修复 PR**；高严重度两_issue（#3716、#3455）长期未响应，值得维护者优先介入。

## 6. 功能请求与路线图信号

- **存储保留策略/轮换机制**（#3735、#3716）：社区对 `conversations/` 目录的 retention/cap/rotation 有明确需求，目前无对应 PR，是下一版本最可能的规划方向之一。
- **配置透传**（#3714）：需要宿主 → session 容器的 env 转发机制，属基础设施级改造。
- **CLI 校验与可发现性**（#3855）：`--model` 参数校验 + 模型列表发现命令，属低成本高体验改进。
- **传输层可配置性**：PR #3850/#3851 已在推进 Codex HTTP SSE/可配置 transport，与 Issue #3338 呼应，若合入将成为下一版本确定的可靠性改进项。

## 7. 用户反馈摘要

- **运维/多实例用户**（fleet 部署）：最不满的是磁盘与内存缺乏上限治理（#3735 “directory grows for the lifetime of the agent group”），“生产 OOM 崩溃循环”（#3716）表明已影响真实业务。
- **可靠性用户**：代理/企业网络环境下 Codex WebSocket 不稳定是反复出现的痛点（PR #3851 与既有 PR #2672、Issue #3338 同源），说明该场景用户群体在扩大。
- **CLI 用户**：`ncl` 的“静默成功”体验不佳——错误的 model 名 exit 0（#3855）、CLAUDE.md 编辑被无声丢弃（#3854），用户希望失败要可见。
- **贡献者体验**：外部 PR（#3850–#3852）模板规范、area 标签齐全，显示贡献流程成熟，但合并速度慢可能挫伤积极性。

## 8. 待处理积压

⚠️ 建议维护者关注：

1. **#3716 / #3735 / #3714（conversations 目录治理群）**——生产级严重度，最早 9-04 报告，至今无维护者回应或修复 PR。
2. **#3455（看门狗误杀）**——8-23 报告，标注 “can permanently block replies… no self-recovery”，1 条评论后无下文，属最久未解的高严重度问题。
3. **PR #3420（macOS 状态栏 slug 适配）**——开放近一个月未合并，阻塞相关 macOS 用户体验。
4. **#3714 引用的前置 Issue #1820**——同一 env 覆盖问题第二次被报告，存在回归嫌疑，建议根因排查。
5. 今日新报 3 个 Issue（#3853–#3855）尚在 `triage/unresolved` 状态，需分诊。

**健康度小结**：输入管道活跃（7 Issue + 4 PR/日），但零关闭、零合并、零发布表明消化能力是当前瓶颈；两个高严重度生产问题长期无响应是最大风险点。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报（2026-09-19）

## 1. 今日速览

IronClaw 今日整体活跃度处于**低位平稳**状态：过去 24 小时无新开 Issue、无版本发布，仅有 2 条 PR 活跃更新（均为待合并状态，无合并/关闭记录）。不过值得注意的是，两个活跃 PR 均为实质性修复/重构工作，且都在昨日有更新，表明核心开发仍在持续推进，主要是维护节奏而非社区讨论驱动。项目健康度暂无异常信号，但社区侧（Issue/评论/反馈）今日完全静默，需持续观察是否为周期性波动。

## 2. 版本发布

今日无新版本发布。最新 Release 状态：无。

## 3. 项目进展

今日无 PR 被合并或关闭，两条 PR 处于开放评审阶段：

- **PR #8102**（[链接](https://github.com/nearai/ironclaw/pull/8102)）：修复扩展系统中 Gmail / Google Calendar 无法激活的问题——当管理员通过 **Web UI**（而非环境变量）配置 Google OAuth client 时，OAuth 全流程（consent → code → token exchange）均成功，但激活阶段失败。该 PR 改为实时解析 provider-instance readiness，优先读取管理员配置。属面向生产部署的关键可用性修复。
- **PR #7456**（[链接](https://github.com/nearai/ironclaw/pull/7456)）：大型重构（size: XL, risk: medium），涉及 sandbox / CI / docs / dependencies 多个 scope，由核心贡献者推进。将所有 Reborn profile 直接根植于 `IRONCLAW_REBORN_HOME`，实现 profile 无关的 `state/`, `system/`, `workspaces/` 等目录命名空间，并持久化类型化安全信封（security envelope），确保仅在重启时切换 profile 也不会削弱租户与工作区隔离。该 PR 自 2026-08-10 开放至今约 6 周，昨日仍有更新，说明仍在积极迭代，是当前项目最重要的架构级工作。

**整体评估**：今日无落地进展，但 #7456 持续推进表明沙箱隔离与多 profile 架构仍是项目主线方向。

## 4. 社区热点

今日无任何 Issue 或 PR 出现新评论、点赞或讨论，社区互动数据为零。无可识别的热点话题。

（观察：PR #8102 涉及的“管理员 UI 配置 OAuth”场景暗示存在真实部署环境遇到此问题，但今日数据中未见对应的 Issue 讨论。）

## 5. Bug 与稳定性

今日无新报告的 Bug、崩溃或回归问题。但需注意：

- **PR #8102 本身即针对一个生产级 Bug**（Gmail/Google Calendar 激活失败），已有修复 PR 待评审，**尚无关联 Issue 可见**。建议维护者确认是否有对应 Issue 可关联，或补充复现步骤文档。

## 6. 功能请求与路线图信号

今日无新功能请求。从现有 PR 可推断的路线图信号：

- **多 Profile / 多租户架构强化**：PR #7456 的 profile-agnostic 目录结构 + 安全信封表明团队正在为多租户、多 profile 并存的部署形态打地基，预计将纳入后续主要版本。
- **企业级配置体验**：PR #8102 聚焦管理员 Web UI 配置路径的可用性，暗示项目重视非环境变量式的企业部署场景。

## 7. 用户反馈摘要

今日无 Issue 评论数据，无法提炼用户反馈。间接信号：PR #8102 描述中“any deployment whose operator configured... through the Web UI”表明存在多个受影响部署，实际用户遇到了 OAuth 配置生效问题的痛点。

## 8. 待处理积压

- **PR #7456**（[链接](https://github.com/nearai/ironclaw/pull/7456)）：开放约 **40 天**，标记为 XL 体量、medium 风险，涉及沙箱隔离核心安全语义。建议维护者安排专项评审或拆分为更小的可合并单元，以降低长期开放带来的合并冲突与回归风险。
- **PR #8102**（[链接](https://github.com/nearai/ironclaw/pull/8102)）：昨日刚创建，属影响生产可用性的修复，建议尽快评审合并。

---
*数据来源：GitHub API（过去 24 小时窗口）。今日样本量较小，社区活跃度结论建议结合 7 日/30 日趋势综合判断。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报

**日期：2026-09-19** | 数据来源：[netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI)

---

## 1. 今日速览

- 项目处于**高活跃开发期**：过去 24 小时 PR 更新达 21 条（14 条待合并、7 条已合并/关闭），Issues 更新 6 条，主要由 @alison-xx 和 @fisherdaddy 两位核心贡献者集中产出。
- 今日焦点围绕 **`release/2026.9.18` 发布分支**：多个修复 PR 以该分支为目标，涉及 Windows 网关生命周期、启动恢复、数据迁移等稳定性问题，但正式 Release 尚未发布（今日 0 个新版本）。
- 功能侧同步推进：Cowork 模型模式（Auto/Max）、MCP 工具过滤、技能市场体验优化等 PR 密集提交。
- 值得关注的隐忧：**5 条 3 月份的 Issue 被标记为 stale**，其中内网 npm registry 不可达导致外部开发者构建卡死（#1015/#1025）是长期未解的社区痛点。

---

## 2. 版本发布

今日无新版本发布。但 PR [#2715](https://github.com/netease-youdao/LobsterAI/pull/2715) `Release/2026.9.18` 已关闭，多个修复 PR（#2701、#2718、#2717、#2702、#2703）均指向该发布分支，预计正式 Release 即将发布，可持续关注。

---

## 3. 项目进展

### 已合并/关闭的 PR（7 条）

| PR | 内容 | 意义 |
|---|---|---|
| [#2715](https://github.com/netaise-youdao/LobsterAI/pull/2715) | Release/2026.9.18 发版分支 | 版本发布流程推进 |
| [#2696](https://github.com/netease-youdao/LobsterAI/pull/2696) | Cowork 工作区评审、内联问答 Dock、Tasks 面板 | 来自下游 fork 回馈的 Codex 风格会话工作区增强，协作体验显著升级 |
| [#2703](https://github.com/netease-youdao/LobsterAI/pull/2703) | 子代理（subagent）会话可见性 | 提升多智能体场景透明度 |
| [#2701](https://github.com/netease-youdao/LobsterAI/pull/2701) | 启动恢复加固 + 飞书凭据路由修复 | 解决 9.18 排查中可复现的启动阻塞 |
| [#2702](https://github.com/netease-youdao/LobsterAI/pull/2702) | OpenClaw workspace 初始化恢复 | 稳定性修复 |
| [#2717](https://github.com/netease-youdao/LobsterAI/pull/2717) | 定时任务微信送达回执 | IM 集成能力补齐 |
| [#2718](https://github.com/netease-youdao/LobsterAI/pull/2718) | 微信/QQ 扫码登录渠道路由修复 | 登录路径修复 |

### 待合并的重点 PR（节选，14 条）

- **[#2719](https://github.com/netease-youdao/LobsterAI/pull/2719)**：修复旧版本升级残留数据导致每次启动失败，覆盖 Windows 卸载重装场景
- **[#2716](https://github.com/netease-youdao/LobsterAI/pull/2716)**：Cowork 新增 Auto/Max 两种模型模式，自动或使用最强模型路由
- **[#2710](https://github.com/netease-youdao/LobsterAI/pull/2710)**：向 OpenClaw 传递 per-server `toolFilter` 与并行工具调用配置，MCP 精细化控制
- **[#2714](https://github.com/netease-youdao/LobsterAI/pull/2714)**：付费图片/视频生成前校验用户意图，防止误触发扣费，**对商业化体验重要**
- **[#2712](https://github.com/netease-youdao/LobsterAI/pull/2712)**：技能重复导入前询问替换，避免 `id-1`、`id-2` 副本堆积

**整体评估**：项目单日推进约 7 个合并/关闭，修复与功能并重，开发节奏紧凑，健康度良好。

---

## 4. 社区热点

- **[#2654](https://github.com/netease-youdao/LobsterAI/issues/2654)** hooks 配置在 Gateway 重启后丢失 —— 今日唯一活跃的新 Issue（2 条评论），报告者 @maxbxkj 已给出完整根因分析（`getUserPlugins` 未返回 `hooks` 字段）和三步修复建议，质量较高，**尚无对应 fix PR，建议维护者优先认领**。
- 多个 3 月旧 Issue（#1015/#1016/#1023/#1024/#1025）在今日集中被标记 stale，反映社区对**外部开发者体验**（内网 registry、登录态下发、架构拆分）的诉求长期未获官方响应。

---

## 5. Bug 与稳定性（按严重程度）

| 严重度 | 问题 | 状态 |
|---|---|---|
| 🔴 高 | 旧版本数据残留导致每次启动失败（#2719） | ✅ 有 fix PR |
| 🔴 高 | Windows 网关子进程孤儿/IPC 断开处理、启动阻塞（#2701，已关闭） | ✅ 已修复 |
| 🟠 中 | hooks 配置重启后丢失（[Issue #2654](https://github.com/netease-youdao/LobsterAI/issues/2654)） | ❌ 无 PR |
| 🟠 中 | Windows 安全软件拦截 PowerShell 导致 SQLite staging 目录创建失败（[#2709](https://github.com/netease-youdao/LobsterAI/pull/2709)） | ✅ 有 fix PR |
| 🟠 中 | 数据迁移恢复时 Partitions 目录 EBUSY 回滚（[#2705](https://github.com/netease-youdao/LobsterAI/pull/2705)） | ✅ 有 fix PR |
| 🟡 低 | 网关崩溃循环重启不停（[#2707](https://github.com/netease-youdao/LobsterAI/pull/2707)）、延迟重启期间拒绝新会话（[#2708](https://github.com/netease-youdao/LobsterAI/pull/2708)） | ✅ 有 fix PR |
| 🟡 低 | Windows PS 5.1 安装器 Skills 备份失败（[#2706](https://github.com/netease-youdao/LobsterAI/pull/2706)）；付费媒体误生成（[#2714](https://github.com/netease-youdao/LobsterAI/pull/2714)） | ✅ 有 fix PR |

今日稳定性工作量占比很高，且绝大多数 Bug 已有修复 PR 在途，反应速度优秀。⚠️ 注意 #2714 涉及**付费资源误触发**，存在用户资金影响，建议优先合并。

---

## 6. 功能请求与路线图信号

- **[#2716](https://github.com/netease-youdao/LobsterAI/pull/2716)** Cowork Auto/Max 模型模式 + **[#2710](https://github.com/netease-youdao/LobsterAI/pull/2710)** MCP toolFilter —— 表明项目向**智能模型路由与 MCP 细粒度控制**演进，且已在开发中，大概率随下个版本发布。
- **[#2696](https://github.com/netease-youdao/LobsterAI/pull/2696)（已合并）** 来自下游 fork 的回馈，显示项目生态出现二次开发场景，Cowork 工作区是当前投入重心。
- **[#1023](https://github.com/netease-youdao/LobsterAI/issues/1023)** 请求引擎参数自定义（token limit 等）—— 与 #2710 的配置透传方向一致，可能被部分覆盖。
- **[#1024](https://github.com/netease-youdao/LobsterAI/issues/1024)** 请求拆分 `main.ts` —— 属于架构治理诉求，从近期 PR 均带 `area: main` 标签看，主进程模块化已是事实趋势，但正式重构尚未见 PR。

---

## 7. 用户反馈摘要

- **外部开发者构建受阻**（#1015/#1025）：内网 registry `npm.nie.netease.com` 不可达导致 `npm install` 卡死 5 分钟，虽有 `optional: true` 标记但脚本无可达性检查——这是开源社区参与的最大摩擦点，多位用户独立报告。
- **登录体验问题**（#1016）：网易员工 Portal 登录成功但客户端 deep link 未收到 token，登录闭环存在断点。
- **第三方服务兼容性**（#1023）：讯飞 API token limit 限制暴露出引擎参数硬编码问题，用户希望更多可配置项。
- **正面信号**：Issue #2654 报告者主动提交根因分析和修复方案，显示社区存在高质量贡献者；下游 fork 回馈 PR（#2696）也说明项目具备被二次开发的价值。

---

## 8. 待处理积压

以下 Issue 已存续约 6 个月且今日被标记 stale，若无维护者回应将被自动关闭，建议评估：

1. [#1025](https://github.com/netease-youdao/LobsterAI/issues/1025) / [#1015](https://github.com/netease-youdao/LobsterAI/issues/1015) —— 内网 registry 构建阻塞（外部贡献者的核心痛点，**优先级建议最高**）
2. [#1016](https://github.com/netease-youdao/LobsterAI/issues/1016) —— 员工登录态未下发
3. [#1023](https://github.com/netease-youdao/LobsterAI/issues/1023) —— 引擎参数自定义（可与 #2710 路线合并考虑）
4. [#1024](https://github.com/netease-youdao/LobsterAI/issues/1024) —— main.ts 架构拆分

**待合并 PR 积压 14 条**，其中 #2705–#2714 密集集中在 `release/2026.9.18` 分支，建议尽快完成审查以推进版本发布。

---

*本报告基于 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 — 2026-09-19

## 1. 今日速览
今日 Moltis 仓库整体活跃度较低：Issues 无新增/活跃/关闭动态，无新版本发布，仅 1 条新开的待合并 PR。唯一的贡献来自外部开发者 @Kaboka22，提交了对 Groq 模型提供商支持的修复（PR #1276），这是今日唯一实质性的项目进展。整体处于平稳但低活跃状态，社区讨论热度接近冰点，需要关注维护者响应节奏。

## 2. 版本发布
今日无新版本发布（无 Releases）。

## 3. 项目进展
今日无已合并或已关闭的 PR，项目代码主线无变化。

- **待合并**：[PR #1276 Add Groq as OpenAI-compatible provider + fix empty-required strict schemas](https://github.com/moltis-org/moltis/pull/1276)（@Kaboka22，2026-09-19 创建）
  - **问题背景**：Groq 聊天此前基本不可用——Groq 未注册在 `OPENAI_COMPAT_PROVIDERS` 中，导致其落入 genai 回退路径。该回退路径存在三个缺陷：仅注册一个模型、丢弃所有 tool schemas、破坏 model-id 路由。
  - **修复内容**：将 Groq 注册为一等 OpenAI 兼容提供商，并顺带修复了 empty-required strict schemas 相关问题。
  - **意义**：若合并，将显著改善使用 Groq 的用户的兼容性和工具调用（function calling）能力，属于对多提供商架构健壮性的实质性补强。

## 4. 社区热点
今日无评论或反应数据（PR #1276 评论数 undefined、👍 0），无明显的社区讨论热点。唯一值得关注的话题即 Groq 提供商不可用问题，从 PR 描述看，该痛点已存在一段时间但此前无人以 Issue 形式正式报告，由贡献者直接以修复 PR 的方式呈现。

## 5. Bug 与稳定性
今日无新开 Bug Issue，但 PR #1276 隐含披露了以下缺陷（按严重程度排列）：

| 严重程度 | 问题 | Fix PR |
|---|---|---|
| 高 | Groq 提供商落入 genai 回退路径，聊天功能实际不可用 | ✅ [PR #1276](https://github.com/moltis-org/moltis/pull/1276)（待合并） |
| 中 | genai 回退路径丢弃全部 tool schemas，破坏工具调用 | ✅ 同上 |
| 中 | model-id 路由被错误处理 | ✅ 同上 |
| 中 | empty-required strict schemas 问题 | ✅ 同上 |

建议维护者优先审阅该 PR，尽早让修复进入主线。

## 6. 功能请求与路线图信号
- 今日无显式功能请求 Issue。
- 隐含信号：PR #1276 表明社区对**多 LLM 提供商（尤其 OpenAI 兼容生态）一等支持**有实际需求。这暗示 `OPENAI_COMPAT_PROVIDERS` 注册机制可能是后续版本的扩展点，类似提供商（如 DeepSeek、Together 等）的接入需求可能涌现。

## 7. 用户反馈摘要
今日无 Issue 评论可提炼。从 PR #1276 间接可推断的用户痛点：
- 选择 Groq 等非主流提供商的用户此前体验极差（模型注册不全、工具调用失效）；
- 该问题此前未获官方修复，说明该使用场景的用户覆盖或反馈渠道有限。

## 8. 待处理积压
- **[PR #1276](https://github.com/moltis-org/moltis/pull/1276)**：今日新开，尚不构成“长期积压”，但鉴于其修复的是功能性阻断级 Bug，建议维护者在近期内安排审阅与合并，避免修复滞留。
- 今日数据中无其他长期未响应的 Issue/PR，但 Issues 整体活跃度为 0，建议关注是否存在反馈渠道（如 Discord/论坛）分流导致的 GitHub 数据低估。

---
*数据来源：Moltis GitHub 仓库过去 24 小时动态。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw (QwenPaw) 项目日报 — 2026-09-19

## 1. 今日速览

- 项目保持高度活跃：过去 24 小时内 Issues 更新 20 条（新开/活跃 14，关闭 6），PR 更新 43 条（待合并 30，已合并/关闭 13），并发布了 1 个新版本 **v2.2.2-beta.1**。
- 今日新 Issue 集中在 **Console UI 体验、上下文管理（scroll eviction）、模型 Provider 兼容性** 三大方向，社区反馈质量高、复现信息完整。
- 多个安全相关问题（提示注入、技能目录删除攻击 #7859）已有对应修复 PR（#7864）快速跟进，响应链路健康。
- 首次贡献者（first-time-contributor）贡献密集，涵盖性能优化、Console 自愈能力等，社区参与度良好。
- 整体判断：项目处于 **2.2.x 稳定打磨期，向 2.2.2 正式版推进**，节奏紧凑。

---

## 2. 版本发布

### v2.2.2-beta.1
链接：https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.2.2-beta.1

主要变更：
- **feat(console)**: improve grouped chat history（#7665 by @zhaozhuang521）— 改进分组聊天历史展示
- **feat(memory)**: unify ReMe slash commands（#7444 by @jinliyl）— 统一 ReMe 斜杠命令
- **chore**: 版本号提升至 2.2.2b1（@cuiyuebing）

配套的发布验证 Issue [#7849](https://github.com/agentscope-ai/QwenPaw/issues/7849) 已由 github-actions 完成并关闭，说明 Beta 安装验证流程通过。

⚠️ **迁移注意**：社区已报告插件兼容问题 — [#7856](https://github.com/agentscope-ai/QwenPaw/issues/7856) 指出 `qwenpaw-pet 0.1.1` 在 2.2.2b2 下因丢弃 `actor` 参数导致工具审批失效。升级 beta 的桌面用户需检查第三方插件兼容性。

---

## 3. 项目进展

今日合并/关闭的 13 个 PR 中值得关注的推进方向：

- **Provider 目录维护**：[#7223](https://github.com/agentscope-ai/QwenPaw/pull/7223)（DeepSeek 目录按厂商退役情况刷新，移除已下线的 deepseek-chat/reasoner，补充 v4 系列）已关闭，provider 目录数据可靠性提升。
- **SSE 流健壮性**：与 #7813（裸 `null` payload 导致 Console 流冻结）相关的修复线持续推进；配套 PR [#7723](https://github.com/agentscope-ai/QwenPaw/pull/7723)（stream_one 失败时发出错误事件）和 [#7865](https://github.com/agentscope-ai/QwenPaw/pull/7865)（聊天流中途断开的自愈路径）正在 review，Console 流式体验的容错体系逐步成型。
- **v2.2.2-beta.1 发布本身** 吸收了 console 分组历史与 ReMe 斜杠命令统一两项用户可感知改进。

---

## 4. 社区热点

### 🔥 最活跃讨论

- **[#7318] QwenPaw Hub 多租户版 2.2.0 征集方向**（30 评论，👍4）
  https://github.com/agentscope-ai/QwenPaw/issues/7318
  项目从个人 AI 助手向团队/多租户场景扩展的官方路线讨论，关联 #2324（多用户访问与管理员管理的技能）等长期社区诉求。这是目前最能反映**项目战略方向**的讨论，9-18 仍有更新，建议维护者持续汇总。

- **[#7853] ToolResultPruner 跳过媒体块导致 base64 无界累积**（4 评论，9-18 新开）
  https://github.com/agentscope-ai/QwenPaw/issues/7853
  `view_image` 的图片以不可变 base64 存入工具结果且永不裁剪，最终撑爆模型上下文窗口。涉及核心上下文管理机制，与今日 PR #7871（截断旁路修复）同属工具输出治理主题。

- **[#7859] 持久性提示注入：诱导 agent 删除所有技能**（4 评论）
  https://github.com/agentscope-ai/QwenPaw/issues/7859
  跨 20+ 轮会话的 system-reminder 注入攻击，安全敏感度高，已有修复 PR #7864。

---

## 5. Bug 与稳定性（按严重程度排列）

| 严重度 | Issue | 描述 | Fix 状态 |
|---|---|---|---|
| 🔴 高 | [#7859](https://github.com/agentscope-ai/QwenPaw/issues/7859) | 持久性提示注入诱导删除所有技能 | ✅ PR [#7864](https://github.com/agentscope-ai/QwenPaw/pull/7864)（技能目录完整性保护） |
| 🔴 高 | [#7853](https://github.com/agentscope-ai/QwenPaw/issues/7853) | 图片 base64 无界累积撑爆上下文 | ⏳ 部分：PR [#7871](https://github.com/agentscope-ai/QwenPaw/pull/7871) 修复文本截断旁路，媒体块裁剪待跟进 |
| 🔴 高 | [#7876](https://github.com/agentscope-ai/QwenPaw/issues/7876) | DeepSeek 拒绝 `input_audio`（422），audio-fallback 分类器未触发，一个 wav 文件永久杀死会话 | ❌ 暂无 |
| 🟠 中 | [#7856](https://github.com/agentscope-ai/QwenPaw/issues/7856) | qwenpaw-pet 0.1.1 破坏 2.2.2b2 工具审批（丢弃 `actor` 参数） | ❌ 暂无 |
| 🟠 中 | [#7850](https://github.com/agentscope-ai/QwenPaw/issues/7850) | 后台 `reload_driver` 读-改-写竞态覆盖并发策略写入 | ✅ PR [#7854](https://github.com/agentscope-ai/QwenPaw/pull/7854) |
| 🟠 中 | [#7814](https://github.com/agentscope-ai/QwenPaw/issues/7814) | Console SSE 可发出裸 `null` payload；失败时无终止事件 | ✅ 修复线推进中（#7723/#7865，姊妹 Issue #7813 已关闭） |
| 🟠 中 | [#7836](https://github.com/agentscope-ai/QwenPaw/issues/7836) | scroll 淘汰把工具密集区间内的用户轮次一并丢弃，活跃窗口丢失请求 | ✅ PR [#7872](https://github.com/agentscope-ai/QwenPaw/pull/7872) |
| 🟡 低 | [#7866](https://github.com/agentscope-ai/QwenPaw/issues/7866) | 文件区 tab 显示旧内容 | ✅ PR [#7867](https://github.com/agentscope-ai/QwenPaw/pull/7867) |
| 🟡 低 | [#7877](https://github.com/agentscope-ai/QwenPaw/issues/7877) | 会话级工作目录面板 UI 三处缺陷 | ❌ 暂无 |
| 🟡 低 | [#7857](https://github.com/agentscope-ai/QwenPaw/issues/7857) / [#7858](https://github.com/agentscope-ai/QwenPaw/issues/7858) | ACP 关闭回退泄漏事件循环 / 测试未 await 协程警告 | ❌ 暂无 |

已关闭：#7813（SSE null 冻结）、#7838（沙箱缺失时 recall_history_python 静默不注册，配套文档 PR [#7873](https://github.com/agentscope-ai/QwenPaw/pull/7873)）、#7837、#7812（启动后斜杠命令作用于回退会话）、#7570（飞书思考卡自动折叠）、#7599 相关线。

---

## 6. 功能请求与路线图信号

- **[#7733] Agent 自主上下文管理 — 淘汰交接的平滑移交**（Feature）
  https://github.com/agentscope-ai/QwenPaw/issues/7733
  核心诉求：压缩/淘汰不应仅由 token 阈值触发，agent 应有预警与参与权。与今日合并线中的 #7872（保留被中断请求）方向一致，**极可能纳入后续 scroll/context 管理迭代**。
- **[#7318] 多租户 Hub 方向征集** — 2.2.0 已落地 Hub，社区正在定义下一步，是 2.3.x 路线图的直接输入。
- **[#6668] OpenAI Responses prompt caching（GPT-5.6+）** — 8 月开立、9-18 仍活跃，provider 性能方向的长期投入。
- **[#7874](https://github.com/agentscope-ai/QwenPaw/pull/7874) / [#7875](https://github.com/agentscope-ai/QwenPaw/pull/7875) Creator create-video 控制平面（feat + docs spec）** — 主聊天可直接“生成视频”而不暴露项目/元素 ID，是 PawApp 能力边界的实质性扩展。

---

## 7. 用户反馈摘要

- **上下文管理是最大痛点聚集地**：#7836/#7837/#7838 三连反馈（同一深度用户 @chcsyf）显示 scroll 淘汰策略在长工具链任务中的信息丢失问题影响真实工作流；该用户同时报告了 #7877（UI 细节），反馈质量极高，值得重点维护关系。
- **多模态与异构 provider 兼容性不足**：#7876（DeepSeek 拒绝音频块导致会话永久死亡）、#7853（图片累积）表明媒体内容在非 OpenAI provider 上的端到端路径未经充分测试。
- **桌面端插件生态出现兼容裂缝**：#7856 显示插件 API（`actor` 参数）变更未同步生态，2.2.2 正式版前需明确插件兼容策略或版本约束机制。
- **满意点**：#7570（飞书流式卡片）用户自带已验证的本地修复方案提交，说明高级用户对代码库熟悉度高、参与意愿强；飞书 CardKit 流式输出（#3001）被评价“用着不错”。

---

## 8. 待处理积压

| 条目 | 状态 | 建议 |
|---|---|---|
| [#7876](https://github.com/agentscope-ai/QwenPaw/issues/7876) DeepSeek 音频 422 杀死会话 | 新开无响应 | 高严重度，建议优先分派；audio-fallback 分类器未触发是根因线索 |
| [#7856](https://github.com/agentscope-ai/QwenPaw/issues/7856) 插件破坏工具审批 | 新开无响应 | 2.2.2 正式版发布前必须澄清 |
| [#7211](https://github.com/agentscope-ai/QwenPaw/pull/7211) 防止注入上下文持久化（首次贡献者，8-21 开立，已 ready-for-human-review） | 挂起近一个月 | 与 #7859 安全主题相关，建议尽快人工 review |
| [#6381](https://github.com/agentscope-ai/QwenPaw/pull/6381) Driver 能力快照性能优化（7-23 开立） | 长期挂起 | 与今日 #7854（driver 竞态）同模块，可协同 review |
| [#7807](https://github.com/agentscope-ai/QwenPaw/pull/7807) / [#7762](https://github.com/agentscope-ai/QwenPaw/pull/7762) / [#7868](https://github.com/agentscope-ai/QwenPaw/pull/7868) 首次贡献者性能系列 | 待 review | 冷启动导入（飞书 SDK ~5.8s）与请求热路径缓存是用户可感知的性能收益，建议纳入 2.2.2 |

**健康度小结**：Issue→PR 响应闭环率高（今日约半数新 Bug 已有对应 fix PR），发布流程自动化完善；主要风险在于首次贡献者 PR 的 review 周期偏长和多模态/多 provider 兼容性欠账。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目日报 — 2026-09-19

## 1. 今日速览

ZeptoClaw 过去 24 小时整体处于**低强度但高质量推进**状态：无新开 Issues、无版本发布，但维护者 @qhkm 提交并处理了 2 个 PR，其中 1 个已关闭、1 个待合并。两个 PR 分别触及**推理模型兼容性**（providers 层）与**面板登录安全加固**（panel 层），显示项目当前重心在健壮性与安全性打磨，而非新功能扩张。社区侧（Issues/评论/点赞）今日完全静默，互动信号缺失，值得持续观察。

## 2. 版本发布

今日无新版本发布。项目近期 Release 节奏待观察，建议关注 PR #702 合并后是否触发安全类补丁版本。

## 3. 项目进展

- **[#703](https://github.com/qhkm/zeptoclaw/pull/703) [CLOSED] feat(providers): read reasoning-model replies on OpenAI-compatible endpoints**
  解决了 OpenAI 兼容端点上推理模型（reasoning model）的解析缺陷：模型将思考过程写入 `reasoning_content` 字段，且在 token 预算耗尽时 `content` 可能为 null，而 ZeptoClaw 此前仅解析 `content` 并通过 `unwrap_or_default()` 将 null 静默转为空字符串，导致用户拿到空回复且无任何提示。该修复让 providers 层对 DeepSeek-R1 类推理模型的支持更加完整，属于实用性较强的兼容性改进。（注：PR 状态为 CLOSED，是否以合并形式落地需在仓库页面确认。）

- **[#702](https://github.com/qhkm/zeptoclaw/pull/702) [OPEN] fix(panel): rate-limit password login attempts**
  针对面板公开密码登录端点无限制暴力尝试的安全隐患：此前唯一减速带是 bcrypt 计算成本。现引入按 socket 对端 IP 的限速——滚动 60 秒窗口内最多 5 次尝试，第 6 次在进入 JSON 解析与密码校验前直接返回 HTTP 429 + `Retry-After: 60`。这是标准且教科书式的暴力破解防护，待合并。

**小结**：单日 2 个 PR 聚焦于“正确性 + 安全”，项目在小步快跑地补齐生产环境短板。

## 4. 社区热点

今日无任何 Issue 更新、评论或点赞互动，无社区热点可分析。PR #702/#703 均为维护者自提交，社区反馈为零。

## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 |
|---|---|---|
| 🔴 高（安全） | 面板登录端点允许无限密码尝试，存在暴力破解风险 | 已有 fix PR [#702](https://github.com/qhkm/zeptoclaw/pull/702)，待合并 |
| 🟡 中 | 推理模型在 token 耗尽时返回 null `content`，被静默解析为空字符串，用户无感知失败 | 已有修复 [#703](https://github.com/qhkm/zeptoclaw/pull/703)（CLOSED） |

无用户报告的崩溃或回归问题。

## 6. 功能请求与路线图信号

- 今日无新功能请求。
- 从 PR 走势可推断的隐性路线图信号：
  - **多模型/推理模型生态兼容**持续推进（#703），后续可能覆盖更多 OpenAI 兼容平台的边缘行为（如流式 reasoning、工具调用 + reasoning 组合）。
  - **面板安全硬化**（#702）可能开启一系列安全加固工作（如登录审计日志、IP 封禁持久化、2FA）。

## 7. 用户反馈摘要

今日 Issues 为 0 条，无用户评论数据，无法提炼真实用户痛点。间接信号：#703 修复的场景（推理模型空回复）暗示已有用户在 OpenAI 兼容端点部署 DeepSeek-R1 类模型时遭遇静默失败。

## 8. 待处理积压

- **[#702](https://github.com/qhkm/zeptoclaw/pull/702)（OPEN）**：安全修复 PR，建议维护者优先 review 并合并，登录限速属于不宜拖延的防护项。
- 暂无长期未响应的 Issue 积压（今日 Issue 流量为 0，历史积压情况本日数据未覆盖）。

---
*数据来源：ZeptoClaw GitHub 仓库过去 24 小时活动快照。*

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*