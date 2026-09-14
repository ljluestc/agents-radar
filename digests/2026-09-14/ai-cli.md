# AI CLI 工具社区动态日报 2026-09-14

> 生成时间: 2026-09-14 03:57 UTC | 覆盖工具: 11 个

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
**日期：2026-09-14 | 数据窗口：过去 24 小时 GitHub 公开动态**

---

## 一、生态全景

AI CLI 工具已全面进入 **Agent 编排时代**——各工具的重心从“单轮对话”转向 subagent、多 agent 并发、后台任务与长会话生命周期管理，但随之而来的是**可靠性、成本与安全三类系统性债务的集中爆发**。Windows 平台普遍是“二等公民”（Claude Code 置顶/锁死、Codex 沙箱重构、Qwen BOM 重置配置、OpenCode 终端面板禁用），构成跨工具的最大质量洼地。token 经济学成为高频议题：prompt caching 失效、缓存重写浪费、agent 无预算失控，在 Claude Code、Copilot CLI、CodeWhale、oh-my-pi 四个社区均有深度取证报告。同时，**安全防护静默失效**（glob 不匹配、白名单绕过、hooks 失效）正在取代功能缺失，成为用户信任的最大威胁。社区贡献活跃度显著分化：Qwen Code、Pi、OpenCode 呈现健康的社区共建生态，而部分头部工具仍以官方单向维护为主。

---

## 二、各工具活跃度对比

| 工具 | Issues 动态 | PR 动态 | Release | 今日焦点 |
|---|---|---|---|---|
| **Claude Code** | ~10 条热点（含 241👍 置顶 issue） | 6 条 | ❌ 无 | Windows 置顶/锁死；271 起事故复盘系列；cache 取证 |
| **OpenAI Codex** | ~14 条 | 13 条（全部合入，机器人） | ❌ 无 | 配额重置失败；Windows MXC 沙箱重构合入 |
| **Gemini CLI** | ~50 条（约 20 条 subagent 相关） | ~11+ 条 | ✅ nightly | subagent 可靠性；Auto Memory 安全打磨 |
| **Copilot CLI** | 5 条 | 0 | ❌ 无 | v1.0.83 回归（.mcp.json 失效、Linux 语音崩溃） |
| **Kimi Code CLI** | 1 条 | 1 条 | ❌ 无 | 极平淡；多 Agent 限流 issue 关闭 |
| **OpenCode** | ~10 条 | ~10 条 | ❌ 无 | encrypted_content 恢复失败（双修复 PR）；UI 改版争议 |
| **Qwen Code** | ~10 条 | ~10 条 | ✅ 2 个（nightly + cua-driver） | TUI React 崩溃；ACP 权限队列当日闭环修复 |
| **CodeWhale** | ~15 条 | 6 条 | ✅ v0.9.13 | Sub-agent 九缺陷全修复；品牌迁移至 codewhale |
| **Pi** | ~43 条更新 | ~17 条 | ❌ 无 | 错误路径一致性；transcript 架构级重构 |
| **oh-my-pi** | ~10 条 | 10 条 | ✅ v18.1.20 | Antigravity 429 根因定位（paidTier 缺失） |
| **DeepSeek Harness** | 0 | 0 | ❌ | 无活动 |

**活跃度梯队**：第一梯队 Gemini CLI、Pi（Issue 讨论量）；第二梯队 Qwen Code、CodeWhale、Claude Code、Codex、OpenCode、oh-my-pi（Issue+PR+修复闭环均衡）；第三梯队 Copilot CLI（回归待修）、Kimi CLI（平静）；停滞 DeepSeek Harness。

---

## 三、共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **多 Agent / Subagent 可靠性** | Gemini CLI（20/50 条 issue）、CodeWhale（九缺陷修复）、Codex（#13491 意图误读）、Claude Code（scratchpad 隔离）、Kimi（并发限流） | 挂起、结果误报、交付验证缺失、深度/预算失控、并发配额 |
| **Token 成本与缓存透明** | Claude Code（#94177 缓存取证）、Copilot CLI（#4829）、CodeWhale（#6122/6130）、oh-my-pi（#11961）、Pi（#9442） | 缓存失效归因、agent 硬预算、缓存重写浪费、成本可观测 |
| **Windows 平台质量** | Claude Code、Codex、Qwen、OpenCode、Copilot CLI | 更新锁死、沙箱兼容、BOM 配置重置、测试基线 |
| **会话生命周期 / resume 语义** | Pi（transcript 持久化）、OpenCode（压缩失败）、Codex（compaction 丢目标）、oh-my-pi（--resume 被丢弃） | resume 后状态/配置一致性、长会话压缩可靠性 |
| **安全防护真实性与静默失败** | Qwen（白名单绕过、hooks 失效）、Claude Code（glob 缺陷）、oh-my-pi（脱敏遗漏）、Gemini CLI（Memory 先上模型后脱敏） | 安全规则需失效告警，静默失败需可诊断 |
| **本地化 / 中文体验** | Codex、CodeWhale（输入法、文档中文化）、OpenCode | 翻译不完整、IME 适配缺失 |

---

## 四、差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线特点 |
|---|---|---|---|
| **Claude Code** | 企业级深度集成（mods、hooks、Skills、插件测试体系） | 重度专业开发者 | 生态封闭但打磨深；桌面端质量拖后腿 |
| **OpenAI Codex** | 沙箱安全与 Windows 系统层（MXC、token group 校验） | ChatGPT 订阅用户、企业 | Rust 重构、机器人大批量高频合入 |
| **Gemini CLI** | subagent 框架 + Auto Memory + AST 检索 | 开源社区、扩展开发者 | 开放贡献模式（help wanted PR 多） |
| **Copilot CLI** | 语音输入、IDE 联动 | GitHub 生态用户 | 功能面广但回归测试薄弱 |
| **Qwen Code** | 渠道集成（钉钉）、沙箱（bwrap）、多模型 wire API | 国内开发者、多模型用户 | 问题-修复当日闭环，安全建设提速 |
| **OpenCode** | 多 provider 网关兼容、开源可定制 | BYOK / 多模型用户 | 社区贡献量大，UI 改版激进引发反弹 |
| **CodeWhale** | 多 agent fan-out（预算、血缘、交付验证） | agent 重度运维用户 | 桌面化+多端（browser/Apple/Android）野心明显 |
| **Pi / oh-my-pi** | 架构可编程性（transcript、ephemeral turns、扩展 API） | 框架级开发者、tinkerer | 高质量个人主导（mitsuhiko 等），错误路径治理意识最强 |

---

## 五、社区热度与成熟度

- **最活跃**：Gemini CLI（Issue 量最大且团队主动开跟踪 issue）、Pi（43 条讨论 + 17 条 PR，社区共建最健康）
- **快速迭代**：Qwen Code（当日 P1 当日修）、CodeWhale（blocker 全清后发版）、oh-my-pi（根因分析驱动修复）
- **成熟但负重**：Claude Code（生态最深但 Windows 长尾 issue 积压、bot 误判引发不满）、Codex（机器人密集合入但热点计费 issue 两月未解）
- **响应滞后**：Copilot CLI（回归无修复 PR）、Kimi CLI（issue 六个月才关闭）
- **注意**：Codex 全部 13 个 PR 来自机器人 copyberry，人类社区贡献通道不明显。

---

## 六、值得关注的趋势信号

1. **“绿灯 ≠ 正确”成为共识**：Claude Code 的 271 起事故复盘（44% 关键 bug 通过自检）与 CodeWhale 的“4.5M token 零产出”共同指向——**agent 工作流必须有独立验证线和交付验证器**，不能信任模型自检。
2. **成本可观测性是下一个刚需**：从缓存取证、per-step 审计到 agent 硬预算，多工具社区同步涌现论文级成本分析，预示“token 账单仪表盘”将成为标配功能。
3. **安全配置需要“失效告警”语义**：glob 不匹配、白名单绕过、hooks 停效均属静默失效——安全声明与实际生效之间的一致性校验，是工具选型的新评估维度。
4. **resume/compaction 是长任务自动化的最后短板**：几乎所有工具都在此失分，谁先解决会话状态一致性，谁就赢得自动化流水线场景。
5. **Windows 支持质量是选型硬约束**：跨 6 个工具的 Windows 痛点集群表明，Windows 重度团队应将平台成熟度置于功能列表之前。
6. **开源社区贡献成为护城河**：Pi、Gemini CLI、Qwen Code 的快速修复能力来自社区，而机器人单向合入（Codex）或官方响应缓慢（Copilot、Kimi）的工具，修复节奏明显受限。

**对开发者的建议**：生产环境采用任何 agent 编排前，建立独立的输出验证与 token 监控；依赖项目级 MCP 配置或 Windows 环境的团队，暂缓升级 Copilot CLI v1.0.83 并关注 Claude Code 的 Windows 修复进展。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告
（数据截止 2026-09-14，来源：github.com/anthropics/skills）

---

## 一、热门 Skills 排行（按社区关注度）

> 注：本批 PR 数据中评论数字段缺失，排序综合 Issue 关联度、跨周期活跃度与影响力判断。

| # | PR | Skill | 功能与热点 | 状态 |
|---|----|----|----|----|
| 1 | [#1298](https://github.com/anthropics/skills/pull/1298) | **skill-creator 评估修复** | 修复 `run_eval.py` 恒报 0% recall 的核心缺陷（关联 [#556](https://github.com/anthropics/skills/issues/556)，10+ 独立复现）。当前描述优化循环实际在“对噪声优化”，是社区最痛的 bug。2026-06 提交后持续更新至 9 月，讨论热度最高 | OPEN |
| 2 | [#486](https://github.com/anthropics/skills/pull/486) | **ODT 文档 Skill** | OpenDocument（.odt/.ods）创建、模板填充及转 HTML，补齐开源/ISO 标准文档格式空白，需求呼声高 | OPEN |
| 3 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | AI 生成文档的排版质控：孤行、寡段、编号错位等通病。论点“用户不会主动要求好排版，但每次都受影响”引发共鸣 | OPEN |
| 4 | [#1628](https://github.com/anthropics/skills/pull/1628) | **Hivemind 多智能体编排** | 将机械性工作委托给运行免费模型的 headless opencode worker，Claude Code 仅做规划/审查/合并——直击“昂贵上下文是稀缺资源”痛点 | OPEN |
| 5 | [#1742](https://github.com/anthropics/skills/pull/1742) | **mcp-builder 兼容修复** | 适配 `mcp>=2` 的 `streamable_http_client` 重命名与自定义 header，修复 [#1668](https://github.com/anthropics/skills/issues/1668)；同期 [#1390](https://github.com/anthropics/skills/issues/1390)、[#1724](https://github.com/anthropics/skills/pull/1724) 显示 mcp-builder 评估链问题密集 | OPEN |
| 6 | [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality / skill-security analyzer** | 两个“元 Skill”：对 Skill 本身做质量五维评估与安全扫描，呼应社区对 Skill 供应链安全的担忧（见 Issue #492） | OPEN |
| 7 | [#1367](https://github.com/anthropics/skills/pull/1367) | **self-audit 质量门禁** | 机械文件验证 + 四维推理审计的交付前自检，与作者同期提案 [#1385](https://github.com/anthropics/skills/issues/1385) 形成完整质量门禁管线 | OPEN |
| 8 | [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design 改进** | 提升官方前端设计 Skill 的可执行性与内部一致性，属早期高影响力改进型 PR | OPEN |

---

## 二、社区需求趋势（从 Issues 提炼）

1. **信任与安全边界**（[#492](https://github.com/anthropics/skills/issues/492)，43 评论，最热 Issue）：社区 Skill 冒用 `anthropic/` 命名空间构成信任滥用，强烈呼吁签名/命名空间隔离机制。
2. **组织级 Skill 分发**（[#228](https://github.com/anthropics/skills/issues/228)）：期望组织内共享 Skill 库，替代目前 Slack 传文件 + 手动上传的原始流程。
3. **Agent 记忆与状态压缩**（[#1329](https://github.com/anthropics/skills/issues/1329)）：compact-memory——用符号记法压缩长程 Agent 状态，节省上下文。
4. **上下文经济性**（[#1487](https://github.com/anthropics/skills/issues/1487)）：claude-api Skill 单次注入 ~156k token 打爆上下文，社区要求 Skill 按需/分层加载。
5. **Skill 开发工具链可靠性**（[#556](https://github.com/anthropics/skills/issues/556)、[#1390](https://github.com/anthropics/skills/issues/1390)、[#202](https://github.com/anthropics/skills/issues/202)）：评估脚本在 Windows/真实 MCP 服务器上系统性失效，skill-creator 需按最佳实践重写。
6. **AI 治理与输出审计**（[#412](https://github.com/anthropics/skills/issues/412)、[#1385](https://github.com/anthropics/skills/issues/1385)）：策略执行、对抗性审查、交付验证等“AI 管 AI”方向。
7. **平台兼容性**（[#29](https://github.com/anthropics/skills/issues/29)）：Bedrock 等企业部署场景的 Skill 支持需求。

---

## 三、高潜力待合并 Skills（活跃但未合并）

- [#1298](https://github.com/anthropics/skills/pull/1298) skill-creator 评估修复——修复 10+ 人复现的核心 bug，合并动机最强，且与 [#1099](https://github.com/anthropics/skills/pull/1099)（Windows 崩溃修复）存在整合预期。
- [#1742](https://github.com/anthropics/skills/pull/1742) mcp-builder mcp>=2 兼容——9 月新提、更新频繁，直接对应开放 Issue #1668。
- [#525](https://github.com/anthropics/skills/pull/525) Pyxel 复古游戏开发——2026-03 提交后 9 月仍活跃，作者即 Pyxel 引擎维护者，背书强。
- [#1607](https://github.com/anthropics/skills/pull/1607) claude-api 模型退役更新——小而明确，对应已关闭节奏的 #1603。
- [#1602](https://github.com/anthropics/skills/pull/1602) 多 Skill 可靠性/编码/指标修复——打包修复 mcp-builder 序列化等痛点，命中 #1390。

⚠️ 风险提示：前 20 热 PR **全部为 OPEN、零合并**，反映官方对社区 PR 的合并门槛较高或审核积压严重。

---

## 四、生态洞察（一句话总结）

**社区最集中的诉求是“让 Skills 的信任与质量基础设施跟上其爆发式增长”——即解决命名空间安全、评估工具链失效和上下文经济性三大结构性问题，而非单纯增加新 Skill 数量。**

---

# Claude Code 社区动态日报 · 2026-09-14

## 一、今日速览

今日无新版本发布。Windows 桌面端依然是重灾区：**置顶窗口无法关闭**（#85891，241 👍）与**静默更新导致孤儿进程锁死 AppX 容器、重启才能恢复**（#89680 / #89599 / #93783）两大问题持续发酵。此外，@jane1030 一口气提交了 5 篇基于 **271 起生产事故复盘**的模型行为模式报告，质量很高，值得所有重度用户阅读。

## 二、版本发布

过去 24 小时无新 Release。

## 三、社区热点 Issues

1. **[#85891](https://github.com/anthropics/claude-code/issues/85891)** Windows 11 桌面端窗口始终置顶，无任何开关可关闭。241 👍、101 评论，是当前呼声最高的桌面端问题；与 #89467、#66516 同源，影响面广。

2. **[#42776](https://github.com/anthropics/claude-code/issues/42776)** Windows 桌面端因孤儿进程文件锁无法重新启动。183 评论的老牌问题，至今未修，被标记 invalid 引发社区不满。

3. **[#53247](https://github.com/anthropics/claude-code/issues/53247)** Windows 上 App 崩溃后遗留 Silo/Job Object（HRESULT 0x80070020），只能注销/重启恢复。82 评论，与 #89680、#93783 构成同一故障族。

4. **[#94168 ~ #94172](https://github.com/anthropics/claude-code/issues/94168)** 271 起生产事故的 5 篇系列复盘：44% 关键 bug 通过了 Claude 的类型/测试自检、HTTP 200+[] 空结果不被怀疑、自写测试替代被测代码、一次性授权被泛化为永久授权等。对构建 Agent 工作流极具参考价值。

5. **[#89680](https://github.com/anthropics/claude-code/issues/89680)** 静默更新后旧 AppX 容器被孤儿进程占用，新版本启动报 0x80070020，需重启。Windows 更新链路的核心 bug 之一。

6. **[#94177](https://github.com/anthropics/claude-code/issues/94177)** 30 个真实会话的 prompt-cache 取证：缓存写入的 68% 来自 36 个事件（TTL 过期、微压缩、resume），并附论文级缓解方案。今日新提交的硬核成本分析。

7. **[#70315](https://github.com/anthropics/claude-code/issues/70315)** 2.1.186 仍复现：Opus 4.8 幻觉出伪造的用户/系统轮次（stop_reason=null），原作者称该 bug 已使其无法使用 Opus。曾被 bot 误判为重复关闭后重提。

8. **[#87243](https://github.com/anthropics/claude-code/issues/87243)** 同级 subagent 共享同一个 scratchpad 目录，通用文件名会互相静默覆盖——与系统提示宣称的“会话级隔离”不符，影响多 agent 编排正确性。

9. **[#85439](https://github.com/anthropics/claude-code/issues/85439)**（已关闭）隐藏 Skills 不减少总上下文：token 从 Skills 行 1:1 转移到 System tools 行。已确认修复（reproduced）。

10. **[#94166](https://github.com/anthropics/claude-code/issues/94166)** 安全过滤器误伤合法的微控制器缓冲区溢出调试工作，直接中止会话。cyber 分类误报的又一案例。

## 四、重要 PR 进展

1. **[#94184](https://github.com/anthropics/claude-code/pull/94184)** mods/diff：停靠面板与内置 /diff 完全对齐——固定头部/文件列表、滚轮路由、支持 ctrl/opt+↑↓ 与 ctrl+x b 快捷键。
2. **[#93951](https://github.com/anthropics/claude-code/pull/93951)**（已合并）将 diff、sec-default、telemetry 三个 mod 的行为测试迁移至 `mods/<mod>/tests/`，由 `claude plugin test` 统一运行。
3. **[#87079](https://github.com/anthropics/claude-code/pull/87079)** 修复 security-guidance 插件 `**` glob 不匹配零层级路径的问题（对应 issue #86545，属安全规则的静默失效，优先级高）。
4. **[#89404](https://github.com/anthropics/claude-code/pull/89404)** 修复 `validate-agent.sh` 在 `set -e` 下首个 warning 即中止、误报有效 agent 的问题（修复 #83803）。
5. **[#79148](https://github.com/anthropics/claude-code/pull/79148)** 为示例规则文件补上必需的 `hookify.` 前缀，避免照文档复制后被静默忽略。
6. **[#41621](https://github.com/anthropics/claude-code/pull/41621)**（已关闭）补充 CLI 构建基础设施与 esbuild 打包配置。

其余 PR 今日无显著更新。

## 五、功能需求趋势

- **Windows 平台质量**：置顶窗口、更新锁死、通知（#67220 原生 toast）等诉求集中爆发，是当前最大痛点集群。
- **成本与缓存可控性**：#94177 反映社区对 prompt-cache 计费、TTL 行为透明的强烈需求（area:cost）。
- **上下文管理**：Skills 隐藏不降 token（#85439）、上下文占用透明化持续受关注。
- **多 Agent 隔离**：subagent scratchpad 隔离（#87243）指向编排场景的正确性需求。
- **交互细节**：斜杠命令中途补全（#89720）、菜单点击行为细粒度配置（#75599）、UI 本地化（#31413）。
- **可观测性**：桌面端本地状态 feed 供第三方做 "Claude needs you" 提示（#92288）。

## 六、开发者关注点

1. **进程/生命周期管理不可靠**：孤儿进程（更新残留、Bash 子进程 #93996、remote-control 会话丢失 #91087/#90581）是跨平台的系统性问题。
2. **Agent 自检≠行为正确**：jane1030 系列指出 44% 关键 bug 通过类型检查和自写测试——需要独立验证线，而非信任 Claude 的"绿灯"。
3. **安全规则静默失效**：glob 匹配缺陷导致安全规则不生效且无告警（#86545/#87079），安全类配置亟需失效提示。
4. **Windows 用户体验受损**：强制置顶 + 更新即重启，重度用户日常工作流被打断，负面情绪在多个长尾 issue 中累积。
5. **token 经济学**：缓存读占 API 等效成本 64%，事件级缓存失效（resume/microcompact）是主要浪费源，值得重度用户自行监控。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-09-14** | 数据来源：github.com/openai/codex

---

## 1. 今日速览

今日无新版本发布。社区焦点集中在 **配额重置失败（reset 浪费）**、**多模型容量不足（"Selected model is at capacity"）** 以及 **Windows 平台沙箱/浏览器控制问题** 三大类问题。PR 方面，copyberry 机器人密集合入了多个 **Windows MXC 沙箱重构** 与 **TUI 交互改进** 的变更，显示 Windows 沙箱架构正在进行系统性演进。

---

## 2. 版本发布

过去 24 小时无新 Release。（当前最新 CLI 版本为 0.154.0，Desktop 为 26.908.x 系列）

---

## 3. 社区热点 Issues

| # | Issue | 关注理由 | 社区反应 |
|---|-------|---------|---------|
| 1 | [#31606 Reset failed, did not apply and 1 reset is wasted](https://github.com/openai/codex/issues/31606) | Pro 用户的配额重置操作失败但计数器仍被扣减，直接造成付费权益损失，是最受关注的计费类 bug | **59 评论 / 65 👍**，持续两个多月未解决，情绪明显不满 |
| 2 | [#43375 Multiple GPT-5/GPT-6 models return "Selected model is at capacity"](https://github.com/openai/codex/issues/43375) | 容量错误横跨多个模型，非单点问题，疑似服务端容量调度问题 | 22 评论 / 11 👍，影响面广 |
| 3 | [#44781 Editing and resending a queued message triggers "queued follow-up no longer exists"](https://github.com/openai/codex/issues/44781) | Windows Desktop 队列消息编辑后触发错误，属高频核心交互路径 | 24 评论 / 29 👍，高认同度 |
| 4 | [#43410 Windows Browser control fails with API-key authentication](https://github.com/openai/codex/issues/43410) | API Key 认证下浏览器控制直接不可用（`unsupported Codex auth method: apikey`），阻断 BYOK 用户工作流 | 26 评论 / 16 👍，定位清晰的系统性缺口 |
| 5 | [#44720 ChatGPT hit a snag bug reproduce](https://github.com/openai/codex/issues/44720) | 可复现的 Desktop 崩溃类 bug，今日关闭 | 34 评论，官方已跟进处理 |
| 6 | [#13491 Forked Worker Inherits Parent User Intent](https://github.com/openai/codex/issues/13491) | Subagent 架构缺陷：forked worker 将父级用户意图误读为直接指令，导致递归委托，长期未修 | 12 评论 / 11 👍，multi-agent 用户核心痛点 |
| 7 | [#28361 Windows: app-server and child MCP servers are never reaped](https://github.com/openai/codex/issues/28361) | Windows 上 MCP server 进程泄漏，累积至数百个，严重的资源管理缺陷 | 10 评论，与今日多个 Windows 沙箱 PR 高度相关 |
| 8 | [#36586 Subagent task payload invisible to non-OpenAI providers](https://github.com/openai/codex/issues/36586) | DeepSeek 等自定义 provider 下 subagent 收不到任务（encrypted_content 被丢弃），阻碍多模型生态 | 11 评论 / 6 👍 |
| 9 | [#32922 Goal context is discarded during compaction](https://github.com/openai/codex/issues/32922) | 上下文压缩时目标信息丢失，破坏长任务连续性，影响所有长会话用户 | 6 评论，长期存在的设计缺陷 |
| 10 | [#43163 GPT-6 Astra returns invalid_prompt for harmless prompts](https://github.com/openai/codex/issues/43163) | 同账号多台 PC 上无害提示词被误判，疑似模型端误拦截 | 13 评论 / 3 👍 |

**其他值得留意**：[#44802](https://github.com/openai/codex/issues/44802) / [#45335](https://github.com/openai/codex/issues/45335) 简体中文界面翻译不完整（两例，跨国平台反馈）；[#45179](https://github.com/openai/codex/issues/45179) Windows 每次更新后解压耗时 15+ 分钟；[#37725](https://github.com/openai/codex/issues/37725) macOS arm64 二进制未通过严格 codesign 校验。

---

## 4. 重要 PR 进展

今日 13 个 PR 全部来自 copyberry[bot]，**全部已合入（CLOSED）**，主线集中在 Windows 沙箱重构与 TUI/会话体验：

1. **[#45176 Wire the Windows MXC sandbox into command execution](https://github.com/openai/codex/pull/45176)** ⭐
   将新的 MXC 沙箱后端接入命令执行路径，是本轮沙箱架构演进的核心。
2. **[#45312 Extract Windows sandbox configuration preparation into a helper](https://github.com/openai/codex/pull/45312)**
   抽取沙箱配置准备逻辑，保持配置模式与有效沙箱层级的分离。
3. **[#45178 Split Windows sandbox cleanup into preparation and completion phases](https://github.com/openai/codex/pull/45178)**
   两阶段沙箱清理，停用沙箱账户并持有 setup lock——与 Issue #28361 进程泄漏问题方向一致。
4. **[#45182 Validate Windows sandbox token groups before copying SIDs](https://github.com/openai/codex/pull/45182)**
   修复 token group 遍历越界读取的安全隐患。
5. **[#45169 Extract Windows sandbox setup into the library](https://github.com/openai/codex/pull/45169)**
   沙箱 setup 逻辑迁移至 `codex-windows-sandbox` 库，模块化收敛。
6. **[#45276 Add worktree session creation to the agents overview](https://github.com/openai/codex/pull/45276)**
   Agents 总览中新增 `w` 快捷键创建 worktree 会话，改进多 agent 工作流。
7. **[#45255 Open new sessions directly from the command center](https://github.com/openai/codex/pull/45255)**
   Command center 支持直接开新会话，不打断运行中的 agent。
8. **[#45271 Preserve terminal scrollback when growing the TUI viewport](https://github.com/openai/codex/pull/45271)**
   修复 TUI 视口增长时历史回滚内容丢失。
9. **[#45262 Route pastes into the active history search query](https://github.com/openai/codex/pull/45262)**
   `Ctrl+R` 搜索中粘贴文本直接进入查询，修复交互细节。
10. **[#45248 Use captured step settings for request metadata and tool hooks](https://github.com/openai/codex/pull/45248)**
    修复回合内切换模型/推理强度后元数据仍报告初始设置的问题，提升可观测性准确性。

其余：[#45224](https://github.com/openai/codex/pull/45224)（卸载所有权提前注册）、[#45185](https://github.com/openai/codex/pull/45185)（工具调用元数据与输出绑定）、[#45180](https://github.com/openai/codex/pull/45180)（网络配置 helper 抽取）。

---

## 5. 功能需求趋势

- **Windows 平台稳定性**：Issue 与 PR 双向印证，Windows 沙箱（MXC、ACL、进程管理）是当前开发与投诉的双重重心，约占热点 Issue 的一半。
- **多 Agent / Subagent 可靠性**：任务派发失败、意图误读、fork 行为异常（#13491、#36586），随着 multi-agent 使用增长成为新痛点。
- **浏览器/Computer Use 自动化**：API Key 认证不支持、`cua.getState`/`listTabs` 失败频发（#43410、#45340、#45249），浏览器控制是高需求但高故障率区域。
- **自定义模型/第三方 Provider**：DeepSeek 等接入的兼容性问题持续存在（#36586）。
- **本地化**：中文界面翻译不完整两例上报，国际化覆盖不足。
- **会话/上下文管理**：#40429 请求按线程的上下文窗口配置选择器，#32922 反映压缩丢失目标，长任务上下文连续性是持续需求。

---

## 6. 开发者关注点

1. **计费与配额信任危机**：reset 扣减但未生效（#31606、#35116）叠加模型容量错误（#43375），付费用户可用性保障是最强呼声。
2. **Windows 体验差距**：沙箱 setup 卡死（#35349）、更新后无窗口启动（#41523）、更新解压超慢（#45179）——Windows Desktop 安装/更新链路问题密集，今天合入的沙箱 PR 群或为响应。
3. **长任务可靠性**：compaction 丢上下文（#32922、#42896 WebSocket 超时）导致目标丢失，影响自动化工作流的可信度。
4. **进程/资源泄漏**：MCP server 与 app-server 不回收（#28361），长期运行用户需要手动清理。
5. **安全与合规细节**：macOS codesign 校验失败（#37725）、沙箱 token 越界（PR #45182），企业环境采用者关注分发链完整性与沙箱正确性。

---
*本报告基于过去 24 小时 GitHub 公开数据自动整理，评论数为生成时快照。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-14

## 📌 今日速览

Gemini CLI 发布 v0.61.0-nightly.20260914.g9c1b0a610 每日构建版。社区讨论焦点集中在**子代理（Subagent）稳定性**与 **Auto Memory 系统的安全与质量**两大方向，Google 团队成员 @SandyTao520 集中提交了一批 Memory 系统问题跟踪。同时多名社区贡献者的修复 PR 持续推进，覆盖 SDK 流式解析、A2A 服务器、UI 渲染等多个模块。

---

## 🚀 版本发布

**v0.61.0-nightly.20260914.g9c1b0a610**（每日自动构建）
- [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260913.g9c1b0a610...v0.61.0-nightly.20260914.g9c1b0a610)
- 配套版本 PR：[#29321](https://github.com/google-gemini/gemini-cli/pull/29321)

---

## 🔥 社区热点 Issues（Top 10）

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)** [P1] 子代理达到 MAX_TURNS 后被错误上报为 GOAL 成功，掩盖了实际中断 — 终止原因误报直接影响主代理对子任务结果的判断，13 条评论讨论热烈。

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)** [P1] Generalist agent 无限挂起 — 用户反馈简单操作（如建文件夹）挂起超过 1 小时，禁用子代理后可恢复，8 👍 说明影响面较广。

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)** [P1] Shell 命令执行完毕后卡在 "Waiting input" — 简单命令完成后状态未正确回收，长时间困扰用户的稳定性问题。

4. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873)** [P2] 利用 Gemini 3 原生 bash 能力：零依赖 OS 沙箱 + 执行后意图路由 — 大型增强提案，探讨在安全前提下释放模型对 POSIX 工具链的原生偏好，标记 effort/large。

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)** [P2] 评估 AST 感知的文件读取/搜索/代码库映射 — EPIC 级调研，目标是精确读取方法边界、降低 token 噪声，配套子任务 [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)。

6. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)** [P2] Auto Memory 增加确定性脱敏并减少日志 — 当前“先入模型上下文再脱敏”的设计存在安全隐患，是 Memory 安全性的关键问题。

7. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)** [P2] Auto Memory 对低信号会话无限重试 — 低价值会话被反复浮出，浪费资源；配套的还有 [#26523](https://github.com/google-gemini/gemini-cli/issues/26523)（无效 inbox patch 的静默跳过）和 [#26516](https://github.com/google-gemini/gemini-cli/issues/26516)（Memory 问题汇总跟踪）。

8. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)** [P2] Gemini 几乎不主动使用 Skills 和子代理 — 需用户显式指示才调用，反映工具触发策略的可靠性问题。

9. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)** [P1] Browser 子代理在 Wayland 下失败 — Linux 桌面用户的代表性兼容性问题，同样存在 Termination Reason 误报为 GOAL 的情况。

10. **[#29314](https://github.com/google-gemini/gemini-cli/issues/29314)** [P1] ShellProcessor 忽略 abort 信号，挂起的自定义命令阻塞提示管道 — 昨日新报的 P1，代码级定位到 `shellProcessor.ts:171-178` 每次注入都创建未关联的 AbortController。

---

## 🔧 重要 PR 进展（Top 10）

1. **[#29321](https://github.com/google-gemini/gemini-cli/pull/29321)** — 自动化 nightly 版本号提升（今日发布配套）。

2. **[#29319](https://github.com/google-gemini/gemini-cli/pull/29319)** [P2] **SDK 修复**：`sendStream` 中对 tool-call 参数的 `JSON.parse` 加保护，畸形 JSON 不再杀死整个流。

3. **[#29320](https://github.com/google-gemini/gemini-cli/pull/29320)** [P2] **A2A 服务器修复**：将 `express.json()` 移至 A2A 路由之前注册，JSON-RPC 处理器终于能拿到解析后的 body。

4. **[#29304](https://github.com/google-gemini/gemini-cli/pull/29304)** **UI 修复**：截断文本时避免拆分 UTF-16 代理对，防止 emoji 被静默丢弃。

5. **[#29229](https://github.com/google-gemini/gemini-cli/pull/29229)** **设置编辑器修复**：拒绝 `1e309` 等非有限数输入，防止设置被静默序列化为 `null` 而损坏。

6. **[#29286](https://github.com/google-gemini/gemini-cli/pull/29286)** [P1] 在 RobustAutonomousAgent 中实现 Google 搜索工具。

7. **[#28963](https://github.com/google-gemini/gemini-cli/pull/28963)** **文档修复**：纠正 `excludeTools` 示例 — 原示例写法根本无法匹配，可能误导扩展作者产生虚假安全感。

8. **[#27863](https://github.com/google-gemini/gemini-cli/pull/27863)** [P1, help wanted] 工具调用优先使用结构化显示标题，修复非交互模式的输出展示。

9. **[#27862](https://github.com/google-gemini/gemini-cli/pull/27862)** [P2, help wanted] 修复子代理工具调用在 UI 中执行时消失的问题。

10. **[#29134](https://github.com/google-gemini/gemini-cli/pull/29134)** [已关闭] 保护当前活跃会话不被 `--delete-session` 误删，含回归测试；同期 [#29131](https://github.com/google-gemini/gemini-cli/pull/29131)/[#29132](https://github.com/google-gemini/gemini-cli/pull/29132) 修复了 CRLF 文件导致 diff 摘要退化为全文 diff 的问题（Windows 用户痛点）。

另：dependabot 的大批量依赖更新 PR [#29137](https://github.com/google-gemini/gemini-cli/pull/29137)（77 个 npm 包，含 MCP SDK 升级）仍在进行中。

---

## 📈 功能需求趋势

- **子代理体系成熟化**：今日 50 条 Issues 中约 20 条与 subagent 相关（挂起、误报成功、不主动调用、轨迹不可见、配置覆盖失效），是最集中的方向。团队正在推进本地子代理 Sprint（[#20195](https://github.com/google-gemni/gemini-cli/issues/20195)）。
- **Auto Memory 安全与质量**：Google 团队集中提交脱敏、重试、patch 校验等问题，Memory 子系统进入打磨期。
- **代码检索智能化**：AST 感知工具（#22745/#22746）与 "Tactful Extraction" 节省 token 策略（#19561），指向更精准、更低 token 成本的代码理解。
- **Browser Agent 健壮性**：会话接管、锁恢复（#22232）、Wayland 兼容（#21983）、配置覆盖（#22267）。
- **终端 UI 性能**：resize 闪烁、渲染性能优化（#21924）。

---

## ⚠️ 开发者关注点（痛点）

1. **子代理可靠性是最大痛点**：挂起、结果误报、不主动触发三类问题叠加，用户被迫手动禁用子代理（#21409、#21968）。
2. **命令执行生命周期管理**：命令完成后卡住（#25166）、abort 信号被忽略（#29314）、交互式提示挂死（#22465），反映 shell 集成的状态回收存在系统性问题。
3. **Token 成本与上下文膨胀**：每回合 ~36.6k token 基线 + 全文 diff 回灌（CRLF bug）加剧成本焦虑。
4. **安全防护的真实性**：文档中无效的 `excludeTools` 示例、Memory 先上模型后脱敏、破坏性命令（`git reset --force`）缺乏约束，安全边界需要收紧（#28963、#26525、#22672）。
5. **配置生效问题**：settings.json 覆盖被 Browser Agent 忽略、symlink 子代理不被识别、`/compress` 不持久化——配置一致性是反复出现的主题。

---

*数据来源：google-gemini/gemini-cli GitHub 仓库（过去 24 小时）*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-14 | 数据来源：github.com/github/copilot-cli**

---

## 一、今日速览

今日无新版本发布，社区活跃度集中在 v1.0.83 的稳定性问题上。两个高影响 Bug 值得警惕：**工作区 `.mcp.json` 完全失效**（#4832）和 **语音模式在 Linux 上直接崩溃**（#4833）。此外，Subagent 长任务链导致 prompt caching 失效、token 消耗激增的问题（#4829）引发了对成本控制的讨论。

---

## 二、版本发布

过去 24 小时无新 Release。

---

## 三、社区热点 Issues

今日共 5 条 Issue 更新，以下为全部值得关注条目：

### 1. 🔴 [Bug] Subagent 长工具调用链导致 prompt caching 失效、token 复合消耗（#4829）
- **状态**：OPEN | 作者：@gcapnias | 👍 0 | 💬 1
- **环境**：v1.0.83 / Windows 11 / Gemini 3.8 Flash
- **为何重要**：自主 Subagent 在单轮内执行数百次工具调用时，破坏了 prompt caching 机制，token 消耗按轮次复合增长。这直接影响重度 Agent 用户的**成本与可用性**，是 Agent 化工作流的核心痛点。
- 链接：github.com/github/copilot-cli/issues/4829

### 2. 🔴 [Bug] 工作区 .mcp.json 在 v1.0.83 中完全不被加载（#4832）
- **状态**：OPEN | 作者：@ryan-knopp-elanco
- **为何重要**：`copilot mcp list` 只显示 User servers，仓库根目录的 `.mcp.json` 被忽略，MCP 服务器根本未启动。这不是展示问题而是**功能性回归**，会阻断依赖项目级 MCP 配置的团队工作流。建议受影响用户临时将配置迁移至用户级。
- 链接：github.com/github/copilot-cli/issues/4832

### 3. 🔴 [Bug] 语音模式触发 ONNX Runtime 断言崩溃（#4833）
- **状态**：OPEN | 作者：@r-o-x
- **环境**：v1.0.83 / Manjaro Linux x64
- **为何重要**：本地 Nemotron ASR 模型处理音频时触发 `SIGABRT` 崩溃并 core dump，**语音输入在 Linux 上完全不可用**。
- 链接：github.com/github/copilot-cli/issues/4833

### 4. 🟡 [FR] 后台 Sub-agent 实时进度流式展示（#2254）
- **状态**：OPEN | 创建于 2026-03-24，长期悬而未决 | 💬 1
- **为何重要**：多阶段编排 Agent（plan → implement → deliver → review）运行时，`/tasks` 只显示工具调用次数，缺乏可观测性。Agent 可观测性是社区长期诉求，该 Issue 已存活近半年仍未获官方回应。
- 链接：github.com/github/copilot-cli/issues/2254

### 5. ✅ [Bug] 工具调用被拒绝后应触发全局重规划（#1029）— 已关闭
- **状态**：CLOSED | 创建于 2026-01-20 | 于 2026-09-14 关闭
- **内容**：用户对某个工具调用给出拒绝/反馈后，期望模型据此重规划后续所有工具调用，而非逐个确认。历时近 8 个月后关闭，或意味着行为已改进或已按设计关闭，值得查看关闭说明。
- 链接：github.com/github/copilot-cli/issues/1029

---

## 四、重要 PR 进展

过去 24 小时无 PR 更新。今日 Issue 中暴露的回归问题（MCP 工作区配置加载、Linux 语音崩溃）尚无对应修复 PR 出现，修复节奏值得关注。

---

## 五、功能需求趋势

从近期 Issue 提炼的社区关注方向：

| 方向 | 信号来源 | 热度 |
|---|---|---|
| **Agent 可观测性** | #2254（后台任务实时进度流）、#4829（token 消耗不可见） | ⭐⭐⭐ |
| **成本与 token 效率** | #4829（prompt caching 失效 + 复合消耗） | ⭐⭐⭐ |
| **MCP 生态稳定性** | #4832（工作区配置回归） | ⭐⭐ |
| **多模态/语音输入** | #4833（Linux 语音崩溃） | ⭐ |
| **Agent 交互模型优化** | #1029（批量反馈触发重规划） | ⭐ |

**核心结论**：随着 Subagent/编排式 Agent 成为主流用法，社区重心已从“功能有无”转向 **规模化运行下的可观测性、成本控制与交互效率**。

---

## 六、开发者关注点

1. **v1.0.83 回归风险**：今日 3 个新 Bug 均出现在 v1.0.83，其中 MCP 工作区加载失效影响面最广。生产环境依赖项目级 `.mcp.json` 的团队建议暂缓升级或降级。
2. **Agent 成本焦虑**：#4829 揭示的 prompt caching 失效意味着长时间自主任务的实际开销可能远超预期，重度用户需监控用量。
3. **平台差异**：Linux 端语音功能（本地 Nemotron ASR + ONNX Runtime）成熟度明显落后。
4. **长期 Issue 响应偏慢**：#2254（存活约半年）、#1029（存活近 8 个月后才关闭），功能诉求类 Issue 的官方跟进节奏有待提升。

---
*本日报基于过去 24 小时 GitHub 公开数据自动整理，仅含 5 条 Issue，无 Release 与 PR 动态。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-09-14 | 数据来源：[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)**

---

## 1. 今日速览

今日社区整体较为平静：无新版本发布，过去 24 小时仅更新了 1 条 Issue 和 1 条 PR。最值得关注的动态是关于**会员多 Agent 并发受限**的 Issue #1383 今日被关闭，同时一条改进 OpenAI 兼容配置文档的 PR #2641 仍在推进中。

---

## 2. 版本发布

过去 24 小时无新 Release 发布，省略。

---

## 3. 社区热点 Issues

> ⚠️ 今日数据源中仅 1 条 Issue 更新，如实呈现如下，不做扩充。

### [#1383] [bug] 会员权益称支持多 Agent，但两个 Agent 并发思考即触发限制
- **状态：** 已关闭（CLOSED）
- **作者：** @asecret | 创建于 2026-03-10，今日（09-14）更新关闭 | 💬 6 条评论
- **为什么重要：** 该 Issue 直接触及会员权益兑现问题——用户在 openclaw 上使用 API，只要两个 Agent（用户昵称“小龙虾”）持续对话，就会触发 `API rate limit` 限制。这反映了社区对**多 Agent 并发场景下配额与限流策略透明度**的强烈关注，也涉及订阅档位（Allegretto）权益边界的界定。
- **社区反应：** 共 6 条评论，历时半年后于今日关闭，说明官方已有处理结论，但此类配额类问题在多 Agent 使用场景下仍具普遍参考价值。
- **链接：** [MoonshotAI/kimi-cli Issue #1383](https://github.com/MoonshotAI/kimi-cli/issues/1383)

---

## 4. 重要 PR 进展

> ⚠️ 今日数据源中仅 1 条 PR 更新，如实呈现如下，不做扩充。

### [#2641] docs(providers): 明确 OpenAI 兼容配置说明
- **状态：** OPEN | 作者：@QIU-Guanzong | 创建并更新于 2026-09-13
- **内容：**
  - 明确自定义 OpenAI 兼容 Provider 需要提供 API-root base URL 及服务方接受的 model ID；
  - 说明 `OPENAI_BASE_URL` 与 `OPENAI_API_KEY` 非空时，会覆盖 `openai_legacy` 和 `openai_responses` 两种 Provider 的配置字段；
  - 同步更新中英文文档。
- **价值：** 降低用户接入第三方 OpenAI 兼容服务时的配置踩坑成本，属于高价值文档改进。
- **链接：** [MoonshotAI/kimi-cli PR #2641](https://github.com/MoonshotAI/kimi-cli/pull/2641)

---

## 5. 功能需求趋势

基于今日有限的更新数据，可提炼出两个方向：

1. **多 Agent 并发与配额策略**：Issue #1383 表明用户对会员权益中的多 Agent 支持有真实需求，但当前限流机制与宣传权益之间存在理解落差。社区期望更清晰的并发额度说明或更宽松的限流策略。
2. **OpenAI 兼容生态接入**：PR #2641 反映大量用户通过自定义 OpenAI 兼容端点使用 Kimi CLI，对配置文档的准确性需求较高。

---

## 6. 开发者关注点

- **配额/限流透明度**：多 Agent 场景下的 rate limit 触发条件缺乏明确说明，容易引发权益纠纷类反馈（如 #1383）。建议官方在文档或产品内展示实时配额状态。
- **环境变量与 Provider 配置优先级**：`OPENAI_BASE_URL` / `OPENAI_API_KEY` 覆盖 Provider 字段的隐式行为是常见踩坑点，文档澄清（#2641）正是对这一痛点的回应。
- **Issue 处理周期偏长**：#1383 从创建到关闭历时约 6 个月，社区可能期望更及时的官方响应。

---

*数据统计窗口：过去 24 小时 | Release: 0 | Issue 更新: 1 | PR 更新: 1*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-14

## 📌 今日速览

今日无新版本发布。最突出的动态是 **Muse Spark 系列模型在 Zen 上因 `encrypted_content` 鉴权问题导致会话恢复失败**，一天内涌入多个相关 Issue（#48741、#48805、#48915），并已出现两个竞争性修复 PR（#48908、#48918）。同时，**新版 UI 布局引发的社区不满持续发酵**，多位用户要求恢复经典双栏侧边栏。

---

## 🔥 社区热点 Issues

1. **#1764 输入框支持 Vim 快捷键**（35 评论 / 187 👍）
   长期高需求，对标 Claude Code，已关闭，关注是否已落地实现。
   [链接](https://github.com/anomalyco/opencode/issues/1764)

2. **#48741 [2.0] Muse Spark 系列模型在收到图片/工具调用时触发 Zen 严重错误**（25 评论）
   `reasoning encrypted_content was not issued to this caller`，今日最热新 Issue，涉及多模型、多场景。
   [链接](https://github.com/anomalyco/opencode/issues/48741)

3. **#48882 要求恢复带持久左侧栏的经典 UI**（9 评论）
   针对侧边栏改版 #20242 的回退请求，UI 改版争议的代表性反馈。
   [链接](https://github.com/anomalyco/opencode/issues/48882)

4. **#48888 布局被强制替换为单会话上下文界面**（7 评论）
   多项目/多会话用户对新布局的强烈不满，情绪化表达反映真实痛点。
   [链接](https://github.com/anomalyco/opencode/issues/48888)

5. **#48915 Muse Spark 1.3 空闲后恢复会话失败**（2 评论）
   与 #48741 同根因的会话恢复场景复现，已直接催生修复 PR #48918。
   [链接](https://github.com/anomalyco/opencode/issues/48915)

6. **#17340 会话压缩失败："context exceeds model limit"**（5 评论 / 3 👍）
   128k 上下文模型会话膨胀至 145k 后无法压缩，长期未解决的稳定性问题。
   [链接](https://github.com/anomalyco/opencode/issues/17340)

7. **#23114 会话标题由注入的记忆/系统上下文而非真实用户消息生成**（6 评论）
   标题生成将完整消息历史传给标题模型，MCP 注入内容污染标题，影响记忆系统可信度。
   [链接](https://github.com/anomalyco/opencode/issues/23114)

8. **#48447 任务完成后 AI 对同一消息重复应答**（3 评论）
   用户消息被重复投递，中文社区报告，涉及插件平台集成场景。
   [链接](https://github.com/anomalyco/opencode/issues/48447)

9. **#35112 6MB 请求体限制阻断 Qwen3.7Plus 合法图片输入**（5 评论）
   OpenCode Go 图片附件被硬性大小限制拦截，影响多模态使用体验。
   [链接](https://github.com/anomalyco/opencode/issues/35112)

10. **#16100 VS Code 1.110 集成终端中数字小键盘失效**（33 评论）
    已关闭，但作为 IDE 集成场景的高频交互 Bug 值得关注是否彻底修复。
    [链接](https://github.com/anomalyco/opencode/issues/16100)

---

## 🔧 重要 PR 进展

1. **#48908 / #48918 修复过期加密推理内容（encrypted reasoning）**
   双 PR 并行解决 Muse Spark / OpenAI Responses 模型会话续传失败问题，是今日最紧迫的修复方向。
   [链接](https://github.com/anomalyco/opencode/pull/48908)

2. **#48901 拆分 Provider 与 Model 注册表（核心重构）**
   解决各 location 重复维护完整模型目录的问题，架构层面的重要清理。
   [链接](https://github.com/anomalyco/opencode/pull/48901)

3. **#48498 SQLite 长期记忆持久化（teach / recall / learn）**
   社区贡献的重量级新功能：基于 SQLite 的长期记忆系统，含教学、召回与学习三种操作。
   [链接](https://github.com/anomalyco/opencode/pull/48498)

4. **#43165 消息日志器（Message logger）**
   通过 `experimental.log_messages` 提供 LLM 请求/响应分级日志（info/debug/trace），利好调试与可观测性。
   [链接](https://github.com/anomalyco/opencode/pull/43165)

5. **#48862 保留 OpenAI Chat 图片 URL**
   修复将 HTTP 图片 URL 误当 base64 处理的问题，多模态链路关键修复。
   [链接](https://github.com/anomalyco/opencode/pull/48862)

6. **#48863 序列化未定义的历史工具输入**
   将显式 undefined 的历史 tool input 序列化为 `{}`，避免 schema 校验失败。
   [链接](https://github.com/anomalyco/opencode/pull/48863)

7. **#48914 移除终端面板设置（TUI 重构）**
   持久终端面板在 Linux/macOS 默认可用，Windows 暂缓，简化配置面。
   [链接](https://github.com/anomalyco/opencode/pull/48914)

8. **#48339 被中断回合后继续处理排队中的提示**
   修复停止当前回合后排队的 prompt 被丢弃的问题，改善交互流畅度。
   [链接](https://github.com/anomalyco/opencode/pull/48339)

9. **#48886 Vertex service tier 映射为请求头**
   将 Gemini `serviceTier` 正确映射到 Vertex AI 的专有 header，适配企业级吞吐配置。
   [链接](https://github.com/anomalyco/opencode/pull/48886)

10. **#48913 恢复 typecheck 状态检查**
    工作流改名导致所有 PR 永久 pending 的 CI 阻塞修复，虽小但影响全体贡献者。
    [链接](https://github.com/anomalyco/opencode/pull/48913)

---

## 📈 功能需求趋势

- **UI 布局回退诉求集中爆发**：#20242 侧边栏改版后，#48882、#48888、#48893 等多个 Issue 要求恢复经典双栏布局或提供可选模式。
- **长期记忆与上下文管理**：SQLite 记忆 PR（#48498）、会话压缩失败（#17340）、标题生成污染（#23114）共同指向上下文/记忆体系是下一阶段核心战场。
- **多模态（图片输入）稳定性**：图片 URL 序列化（#48862）、6MB 限制（#35112）、图片触发模型错误（#48741）表明图片链路仍是最脆弱环节之一。
- **模型兼容性广度**：Vertex 映射、Muse Spark / DeepSeek / GLM / Qwen 等模型的 reasoning 兼容问题，社区对多供应商稳定支持期待高。
- **可观测性与调试**：消息日志 PR（#43165）与 `/visualize` 命令（#48605）反映对调试工具的需求上升。

---

## ⚠️ 开发者关注点

1. **Zen 网关的 encrypted_content 鉴权链路脆弱**：同会话切换模型、空闲后恢复、图片/工具调用等多个场景均触发失败，建议官方尽快合并 #48908/#48918 并推送热修复。
2. **新 UI 强制迁移引发信任危机**：缺乏可配置回退选项的改版正在累积负面情绪，多项目用户工作流被打断。
3. **会话体积管理是长期隐患**：压缩失败、恢复卡死（#36537）、消息重复投递（#48447）均与长会话状态管理相关。
4. **Windows 体验仍为二等公民**：终端面板禁用（#48914）、控制台窗口闪烁（#42440）、Git worktree 问题（#31686）持续存在。
5. **贡献流程需注意**：v2 ruleset 依赖 `typecheck` 状态名（#48913 已修复），外部贡献者提交 PR 前建议确认 CI 检查项齐全。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-09-14

## 一、今日速览

今日社区焦点集中在 **TUI React #185 崩溃问题**（多 Issue 聚集、P1 级）和 **ACP 权限队列跨会话阻塞的严重生产事故**（#11795，当日提交修复 PR #11802）。同时发布 v0.23.3-nightly 与 cua-driver-rs v0.20.6，多个安全类 Issue（Bash 白名单绕过、logs.json 隐私残留）值得关注。

## 二、版本发布

### v0.23.3-nightly.20260913 ([链接](https://github.com/QwenLM/qwen-code/releases))
- refactor(dingtalk): 移除过时的后台响应聚合逻辑（PR #11570）
- feat(channels)!: breaking change，移除 "me" 相关功能

### cua-driver-rs v0.20.6 ([链接](https://github.com/QwenLM/qwen-code/releases))
- 预编译二进制发布：macOS 通用二进制已签名+公证（含 QwenCuaDriver.app）；Linux x86_64/arm64（glibc ≥ 2.31）；Windows UIAccess worker + 原生 SDK payload

## 三、社区热点 Issues

1. **#11795 [P1] ACP 权限队列按连接而非会话隔离，一个空闲会话的未响应提示会无限静默阻塞 daemon 上所有会话** — 下游发行版生产事故，已在 main 分支独立复现验证，当日即有修复 PR（#11802）跟进。[链接](https://github.com/QwenLM/qwen-code/issues/11795)

2. **#11500 [P1] 多个后台 Agent 接连完成时 TUI 静默退出，Ink useBoxMetrics 布局监听 setState 死循环触发 React #185** — 12 条评论为今日最高，与 #5199、#11756、#11783 共同指向同一渲染层根因，是当前最紧迫的稳定性问题。[链接](https://github.com/QwenLM/qwen-code/issues/11500)

3. **#11764 [P1/安全] Bash 白名单规则可被绕过：命令以单引号内反斜杠结尾时，第二条无关命令免确认执行** — 权限模型安全漏洞，配套修复 PR #11765 已提交。[链接](https://github.com/QwenLM/qwen-code/issues/11764)

4. **#11803 [P1] Windows 下带 UTF-8 BOM 的 settings.json 被判为损坏并静默重置为 {}** — 影响 PowerShell 5.1 / 旧版记事本用户，配置丢失风险高。[链接](https://github.com/QwenLM/qwen-code/issues/11803)

5. **#11762 [P2/隐私] /delete 不清理 ~/.qwen/tmp/<hash>/logs.json，且无法禁用** — 完整对话内容（含工具输出）持续残留磁盘，数据隐私痛点。[链接](https://github.com/QwenLM/qwen-code/issues/11762)

6. **#11019 [P2] AUTO 模式下用户确认无法到达分类器（block 不可覆盖），会话重建时审批模式还会回退为 AUTO** — 涉及 API 驱动场景下的生产数据变更安全，标记 need-discussion。[链接](https://github.com/QwenLM/qwen-code/issues/11019)

7. **#11590 [P1] 非 Qwen 厂商模型经 DashScope 聚合网关调用时因顶层 metadata 字段 400 报错，模型完全不可用** — 第三方模型兼容性硬阻断，已修复关闭。[链接](https://github.com/QwenLM/qwen-code/issues/11590)

8. **#11180 [P1/安全] Skill 的 PreToolUse 安全门在 `--continue` 后停止生效，但指令仍留在上下文中** — 安全防护静默失效，属高危行为一致性缺陷。[链接](https://github.com/QwenLM/qwen-code/issues/11180)

9. **#11777 [P3] CI 必跑 Test job 在全部用例通过后于 workspace→test:scripts 交接点被外部 SIGTERM 间歇性击杀** — 与 #10490 共同反映共享 Runner 的 CI 稳定性问题。[链接](https://github.com/QwenLM/qwen-code/issues/11777)

10. **#11717 [P3] WebShell create action 30s 超时，而顺序的默认 SDK 请求仍有效** — 经实测本地 SDK 修正了原始推断，聚焦超时预算与取消层交互。[链接](https://github.com/QwenLM/qwen-code/issues/11717)

## 四、重要 PR 进展

1. **#11802 fix(cli): 将 ACP 权限队列作用域改为会话级** — 直接修复今日 P1 事故 #11795，问题-修复当日闭环。[链接](https://github.com/QwenLM/qwen-code/pull/11802)

2. **#11765 fix(core): 命令切分时将单引号内反斜杠按字面处理** — 修复 #11764 的 Bash 白名单绕过漏洞。[链接](https://github.com/QwenLM/qwen-code/pull/11765)

3. **#11614 feat(cli): 新增 Linux bwrap 内核级沙箱后端** — 无需容器运行时/root/镜像即可隔离 Agent，opt-in 设计，默认行为不变。[链接](https://github.com/QwenLM/qwen-code/pull/11614)

4. **#11538 feat: 按模型选择 OpenAI wire API（chat-completions / responses）** — 覆盖 CLI、ACP、daemon、Web Shell、VS Code 全链路，显著改善第三方模型兼容性。[链接](https://github.com/QwenLM/qwen-code/pull/11538)

5. **#10183 feat(memory): 结构化按需记忆召回** — 从扁平 prompt 演进为 push/pull 召回协议，记忆变更推送两级树、相关轮次推送元数据子树 + 专用召回工具。[链接](https://github.com/QwenLM/qwen-code/pull/10183)

6. **#11800 fix(dingtalk): 移除后台 Agent 结果的生成式标题**（已合并）— Agent 结果首行直接作为消息/卡片标题，配合 nightly 的 channels 重构。[链接](https://github.com/QwenLM/qwen-code/pull/11800)

7. **#11787 fix(ci): 恢复 Windows 测试基线** — 运行时路径与文件系统断言可移植化，tokenizer 启用 WASI 降级。[链接](https://github.com/QwenLM/qwen-code/pull/11787)

8. **#11575 ci(desktop): CLI 发版时同步发布桌面应用** — 对齐 VS Code 伴侣扩展的发布节奏，默认由仓库变量门控（inert 合入）。[链接](https://github.com/QwenLM/qwen-code/pull/11575)

9. **#11798 ci(lint): 禁止 cli 包从 core 包根新增值导入** — 架构边界守护，推进 monorepo 模块化。[链接](https://github.com/QwenLM/qwen-code/pull/11798)

10. **#9466 refactor: rewind 映射锚定稳定的 prompt 身份** — 使回退映射在会话恢复、headless、重排序表面下均能存活。[链接](https://github.com/QwenLM/qwen-code/pull/9466)

## 五、功能需求趋势

- **后台 Agent / 自动化**：社区高度关注（#11500、#5540、roadmap/background-automation 标签密集），核心诉求是后台任务的稳定性、可恢复性（revive completed agent）与多 Agent 并发渲染健壮性。
- **DingTalk / 渠道集成**：交互卡片、Workspace 渠道、语音转写 voiceBridge（#6443、#8935、#6575）持续迭代，今日 release 与多个 PR 均聚焦此方向。
- **多模型兼容**：第三方模型经聚合网关的兼容性（#11590）与 per-model wire API（PR #11538）成为热点。
- **MCP 生态**：项目级 .mcp.json 审批语义（#4615，已关闭）、Windows STDIO 连接、AppImage Python 环境泄漏（#11718）等问题陆续落地修复。
- **沙箱与安全**：Linux bwrap 内核沙箱、Bash 白名单加固、hooks 权限门一致性，安全建设明显提速。

## 六、开发者关注点

1. **TUI 稳定性是最大痛点**：React #185（Maximum update depth exceeded）在 4+ 个 Issue 中反复出现，均与后台任务/虚拟化历史渲染相关，多 Agent 工作流下近乎必现。
2. **会话与权限管理健壮性**：ACP 权限队列阻塞（#11795）、AUTO 模式确认失效（#11019）、hooks 门失效（#11180）表明长生命周期/多会话场景下的状态一致性仍需加强。
3. **隐私与数据清理**：logs.json 无限累积且 /delete 不覆盖（#11762），遥测错误文本脱敏缺少值级 pin（#11760），开发者对本地数据残留敏感。
4. **CI 抖动影响贡献体验**：共享 Runner 非确定性失败（#10490、#11777）、Windows 基线失守，社区正在推进重试、可移植化与基线修复。
5. **跨平台细节**：Windows（BOM、MCP 连接、测试基线）与 Linux 打包（AppImage 环境变量泄漏）问题占比高，是质量投入的重点方向。

---
*数据来源：QwenLM/qwen-code GitHub（过去 24 小时 Releases / Issues / PRs）*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI（现更名 Codewhale / CodeWhale）社区动态日报
**日期：2026-09-14**

---

## 1. 今日速览

v0.9.13 正式发布，同时项目品牌从 DeepSeek-TUI 迁移至 Shannon Labs 旗下产品 **Codewhale**，旧 npm 包 `deepseek-tui` 已停止维护。今日最密集的活动是 **0.9.13 发布前阻塞的 Sub-agent 运行时九项缺陷（#6121~#6130）全部修复关闭**，多智能体 fan-out 体验大幅改善。此外，颇具特色的“音频视觉宠物（Pet）”功能两条 PR 已合并落地。

---

## 2. 版本发布

### v0.9.13
- `codewhale` 成为正式命令名 / npm 包名 / release 资产名（[Release Notes](https://github.com/Hmbown/DeepSeek-TUI/releases)）
- 旧包 `deepseek-tui` **deprecated**，不再发布新版本
- 包含 Sub-agent 运行时九项修复、模型选择器性能优化、会话指标审计修正等（详见下文 Issues）
- v0.9.14 已开始规划：[Milestone #68](https://github.com/Hmbown/CodeWhale/milestone/68)，入口 Issue [#6094](https://github.com/Hmbown/CodeWhale/issues/6094)

---

## 3. 社区热点 Issues

| # | 主题 | 关注理由 |
|---|------|---------|
| [#6121](https://github.com/Hmbown/CodeWhale/issues/6121) | Sub-agent 运行时九项缺陷（0.9.13 blocker，已关闭） | 六 worker fan-out 实测暴露的系统性问题，已全部修复并随 0.9.13 发布，是多智能体功能的里程碑 |
| [#6122](https://github.com/Hmbown/CodeWhale/issues/6122) | 无法验证 worker 产出声明的交付物（已关闭） | 六个 worker 烧掉 4.5M tokens 却零文件产出，暴露交付验证缺失，是 agent 可信度的核心问题 |
| [#6128](https://github.com/Hmbown/CodeWhale/issues/6128) | fan-out 未真正受限，孙 agent 越过 max_spawn_depth（已关闭） | 隐形孙 worker 消耗 664k tokens 且不可预算，是安全与成本双重隐患 |
| [#6129](https://github.com/Hmbown/CodeWhale/issues/6129) | agent() 缺少单次调用预算（已关闭） | “到 N tokens 停下并交回已有结果”是运维多 agent 的刚需 |
| [#6130](https://github.com/Hmbown/CodeWhale/issues/6130) | status 紧凑投影返回 ~50k tokens（已关闭） | 文档承诺的 compact 路径实际返回完整引擎事件日志，token 浪费严重 |
| [#5860](https://github.com/Hmbown/CodeWhale/issues/5860) | 对话持续自学习 / 自动技能演化（开放） | 让 Skills System 从静态 SKILL.md 进化为自动模式提取，社区讨论热烈（5 评论） |
| [#4955](https://github.com/Hmbown/CodeWhale/issues/4955) | 请求 zero-sandbox / --no-sandbox 模式（开放） | 内核级 Seatbelt 沙箱破坏日常 shell 命令，本地开发者强烈诉求（5 评论） |
| [#5976](https://github.com/Hmbown/CodeWhale/issues/5976) | Provider 计费/定价覆盖不完整致 cost: unknown（已关闭） | 除 Concentrate 外可能还有多个 provider 存在同样缺口，缺少防护机制 |
| [#5482](https://github.com/Hmbown/CodeWhale/issues/5482) | 文档全面中文化 EPIC（开放） | 中文用户群持续增长，文档陈旧且机器翻译质量差，与 #2323 中文输入法问题共同反映本地化短板 |
| [#2323](https://github.com/Hmbown/CodeWhale/issues/2323) | 未适配中文输入法（开放） | 拼音输入时提示不隐藏、字母串入输入区，长期未解决，中文用户核心痛点 |

其他值得留意：[#2342](https://github.com/Hmbown/CodeWhale/issues/2342)（输出文件点击预览）、[#6156](https://github.com/Hmbown/CodeWhale/issues/6156)（拖选复制保留 Markdown 源码，今日新建）、[#5618](https://github.com/Hmbown/CodeWhale/issues/5618)（用 gix 替换内部 git CLI 调用）。

---

## 4. 重要 PR 进展

| PR | 状态 | 内容 |
|----|------|------|
| [#6154](https://github.com/Hmbown/CodeWhale/pull/6154) | 已关闭 | `/pet` 模式：宠物接管终端，turn 完成后揭示真实回复，Escape 返回 |
| [#6110](https://github.com/Hmbown/CodeWhale/pull/6110) | 已关闭 | 宠物持久化世界与工作驱动的点阵形态：980 个点跨 browser/Apple/Android/TUI 共享同一确定性世界 |
| [#6111](https://github.com/Hmbown/CodeWhale/pull/6111) | 已关闭 | 文件级恢复端点 + 修复整树回滚两处缺陷，解决 VSCode 插件 per-file Revert 被撤回的问题 |
| [#6120](https://github.com/Hmbown/CodeWhale/pull/6120) | 已关闭 | Runtime API 新增 `GET /v1/workspace/files/search` 工作区文件建议端点 |
| [#6134](https://github.com/Hmbown/CodeWhale/pull/6134) | 开放中 | Computer Use 0.3.0 专业化：独立 helper 路由本地操作、fail-closed、权限设置与人工暂停 |
| [#6105](https://github.com/Hmbown/CodeWhale/pull/6105) | 开放中 | dependabot：rustls 0.23.43 → 0.23.44 |

配套关闭的 Issue 系列（构成 0.9.13 Sub-agent 修复主体）：
- [#6123](https://github.com/Hmbown/CodeWhale/issues/6123) 写作用域冲突误判兄弟子路径
- [#6124](https://github.com/Hmbown/CodeWhale/issues/6124) 交付验证器把 path:LINE 引用误判为编辑
- [#6125](https://github.com/Hmbown/CodeWhale/issues/6125) parking 事件恢复提示 `resume_from` 与 `followup` 语义不一致
- [#6126](https://github.com/Hmbown/CodeWhale/issues/6126) Resume 逐个执行且产生孤儿 agent id，无批量 followup
- [#6127](https://github.com/Hmbown/CodeWhale/issues/6127) 回应操作者与保活 worker 互斥（wait 超时 vs park-on-turn-end）
- TUI 相关：[#5974](https://github.com/Hmbown/CodeWhale/issues/5974)（MCP 重认证冻结整个 TUI）、[#5975](https://github.com/Hmbown/CodeWhale/issues/5975)（模型选择器卡顿）、[#5977](https://github.com/Hmbown/CodeWhale/issues/5977)（tok/s 分母审计）均已修复关闭

---

## 5. 功能需求趋势

1. **多智能体 / Sub-agent 编排**：预算控制、交付验证、深度限制、批量恢复、血缘追踪 —— 当前最高强度投入方向
2. **本地化与中文体验**：文档中文化（#5482）、中文输入法适配（#2323）、中文 issue 持续出现
3. **桌面化与产品化**：一等公民桌面应用（#4986）、Computer Use 专业化（PR #6134）
4. **沙箱灵活性与安全**：zero-sandbox 模式（#4955）、MCP secret 作用域设计（#5637）
5. **可观测性与成本透明**：per-step 事件粒度审计（#5581）、provider 定价覆盖（#5976）
6. **平台广度**：FreeBSD 支持（#1097）
7. **架构内部现代化**：gix 替换 git CLI（#5618）、mid-turn guidance（#5625）

---

## 6. 开发者关注点

- **Token 成本失控风险**：多 agent fan-out 场景中不可预算的孙进程、50k token 的 status 响应、4.5M token 零产出，成本可观测与硬预算是最强烈的诉求
- **沙箱摩擦**：内核级沙箱破坏日常 shell 工作流，本地开发者希望有可信赖的关闭开关
- **错误信息可操作性**：非官方路由返回 Google 原始 400（#6048）、cost: unknown（#5976）等，用户要求“可诊断、可行动”的错误提示
- **UI 响应性**：模型选择器卡顿、MCP 重认证冻结 TUI、事件仅在 TurnComplete 更新导致界面“假死”感
- **迁移提醒**：所有用户应尽快从 `deepseek-tui` npm 包迁移至 `codewhale`，旧包不再更新

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 社区动态日报 · 2026-09-14

## 1. 今日速览

今日无新版本发布。社区活跃度集中在 Issue 讨论端（43 条更新），其中 `PI_OFFLINE` 未文档化行为争议（#8684）与多项 TUI 渲染性能问题持续发酵。PR 方面有 17 条更新，焦点在 AI 层的健壮性修复（工具参数解析、stop reason 映射）和会话状态管理，包括 mitsuhiko 提出的“对话中系统消息持久化”架构级改动（#9548）。

## 2. 版本发布

过去 24 小时无新 Release。

## 3. 社区热点 Issues

1. **#8684 — `PI_OFFLINE` 静默禁用所有 provider 模型发现**（8 评论）
   文档只声明其影响启动时的网络操作，实际却禁用整个会话的模型目录发现，属“文档与行为背离”类问题，讨论热度最高。[链接](https://github.com/earendil-works/pi/issues/8684)

2. **#8720 — 空白输出工具结果导致会话永久卡死（HTTP 400）**
   工具只返回 `"\r\n"`（Windows bash 常见）时，OpenAI 兼容 provider 拒绝该消息且坏消息留在历史中，后续请求全部失败。属高危会话损坏问题。[链接](https://github.com/earendil-works/pi/issues/8720)

3. **#9306 — 中止/出错回合留下未匹配的 toolCall 块**
   `stopReason: "error"/"aborted"` 时已流式输出的 toolCall 未被匹配，下一次 continuation 被 provider 拒绝。与 #8720 同属上下文一致性隐患。[链接](https://github.com/earendil-works/pi/issues/9306)

4. **#9255 — 长转录触发全屏重绘风暴**
   变更行高于视口顶部时几乎每帧走全量渲染路径，长会话中界面剧烈跳动、文字重影。社区对 TUI 性能问题的又一实锤。[链接](https://github.com/earendil-works/pi/issues/9255)

5. **#9075 — 压缩摘要继承会话 thinking 级别，高 effort 下确定性撞输出上限**
   自适应思考模型的 thinking token 计入 `max_tokens`，compaction 在高 effort 下必然截断。影响长会话核心流程，获 3 👍。[链接](https://github.com/earendil-works/pi/issues/9075)

6. **#9074 — Anthropic 中途 fallback 失败整个回合而非记录切换**
   server-side fallback 在流中段发生时整个 turn 报错，未利用 API 的 handoff 标记。可靠性类问题，获 2 👍。[链接](https://github.com/earendil-works/pi/issues/9074)

7. **#9211 — `vercelGatewayRouting` 配置实际无效**
   文档化的路由配置只有 openai-completions 适配器发送，而 vercel-ai-gateway 目录全部走 anthropic-messages，“配置失效”类问题。[链接](https://github.com/earendil-works/pi/issues/9211)

8. **#9298 — Grok 403 被错误标注为 "OpenAI API error"**
   openai-responses formatter 的错误归因混淆，影响用户排障体验。[链接](https://github.com/earendil-works/pi/issues/9298)

9. **#9474 — Codex 传输缺少不可重置的单请求总超时**
   周期性心跳/keep-alive 事件会不断重置 idle timeout，导致挂起的流永不超时。[链接](https://github.com/earendil-works/pi/issues/9474)

10. **#9566 — models.json 中同名模型导致上下文大小回落到 128k 默认值**
    用户自定义模型条目与 provider 已暴露模型 id 冲突时，cost/maxTokens 等元数据被错误默认值覆盖。[链接](https://github.com/earendil-works/pi/issues/9566)

## 4. 重要 PR 进展

1. **#9548 — 对话中系统消息纳入转录**（@mitsuhiko）
   架构级改动：系统提示与工具变更成为 transcript 一部分，支持 resume/分支导航后状态还原，并保留 prompt 缓存前缀。[链接](https://github.com/earendil-works/pi/pull/9548)

2. **#9569 — 修复 JSON 双重编码的工具参数**（@rsaryev）
   模型把 object/array 参数多引一层 JSON 时自动矫正，提升工具调用成功率。[链接](https://github.com/earendil-works/pi/pull/9569)

3. **#9570 — Gemini `TOO_MANY_TOOL_CALLS` 映射为错误 stop reason**（@rsaryev）
   修复 @google/genai@2.21.0 新增枚举导致的 unhandled stop reason 异常。[链接](https://github.com/earendil-works/pi/pull/9570)

4. **#9488 — 增加 Codex 规范化 turn 归因元数据**（@dannote）
   补齐 session/thread/turn/request-kind 元数据，使工具续跑、重试、steering 可靠归因。[链接](https://github.com/earendil-works/pi/pull/9488)

5. **#9442 — 允许兼容代理接收 `prompt_cache_key`**（@dannote）
   新增 `compat.supportsPromptCacheKey` 开关，第三方代理也能利用会话级 prompt 缓存。[链接](https://github.com/earendil-works/pi/pull/9442)

6. **#9222 — 拒绝在活跃会话操作期间重载扩展**（@acmerfight）
   RPC 模式下工具运行中重载扩展会拿到失效 runner，现增加 `isStreaming` 检查。[链接](https://github.com/earendil-works/pi/pull/9222)

7. **#9459 — resume 时优先采用已记录的 model_change**（@petrroll）
   修复恢复会话后模型选择不准确的读取侧问题。[链接](https://github.com/earendil-works/pi/pull/9459)

8. **#9461 — 流式工具参数延迟解析**（@petrroll）
   不再每个 delta 全量重解析累积 JSON，改为按需缓存解析。作者本人对必要性存疑，值得评审讨论。[链接](https://github.com/earendil-works/pi/pull/9461)

9. **#9126 — 销毁前先落盘工具结果**（@acmerfight）
   shutdown 前等待 `session.abort()`，确保被中断的工具结果先持久化再移除监听器。[链接](https://github.com/earendil-works/pi/pull/9126)

10. **#9531 — 会话树支持永久删除分支**（已关闭）（@moisestohias）
    `pruneBranch()` + `/tree` 界面 shift+d 交互，含子树清理与标签重链。[链接](https://github.com/earendil-works/pi/pull/9531)

## 5. 功能需求趋势

- **会话健壮性与状态一致性**：空白工具结果卡死、未匹配 toolCall、中断结果丢失（#8720/#9306/#9126）——社区最强烈的诉求，错误路径下的上下文完整性是重灾区。
- **TUI 渲染性能**：重绘风暴、大转录逐帧全量渲染、resize 重放整个 transcript（#9255/#9549），性能问题集中爆发。
- **启动性能预算**：对标 jcode 的延迟/内存基准（#7739）及 jiti 缓存不可写导致的重复编译（#9565）。
- **Provider 兼容性**：Grok 错误归因、Vercel Gateway 路由失效、Azure Foundry、server-side tools 声明（#9298/#9211/#9558/#9556）。
- **会话管理增强**：`/new` 继承模型设置、flush 待写条目、exit 工具、分支删除、外观主题（#9054/#9574/#9544/#9531/#9573）。

## 6. 开发者关注点

1. **文档与实现脱节**：`PI_OFFLINE`（#8684）与 `vercelGatewayRouting`（#9211）都是“按文档配置但实际无效”，削弱用户对配置面的信任，建议系统性审计 compat/环境变量项。
2. **错误/中止路径是 bug 温床**：多条高危 Issue 均发生在 abort、error、fallback 等非快乐路径上，与今日多个 PR（#9126/#9222/#8635）形成呼应，值得作为专项治理方向。
3. **多用户/受限环境下可用性**：`/tmp/jiti` 缓存权限（#9565）、Windows bash 输出格式（#8720）表明 Linux 多用户与 Windows 支持仍是薄弱环节。
4. **流式渲染的算法性瓶颈**：长转录下的渲染问题非局部修补可解（#9255/#9549 各自独立报告单核饱和），可能需要 viewport/diff 渲染策略重构。
5. **Agent 工具链扩展诉求**：serverTools、exit 工具、RPC 预算授权（#9556/#9544/#9568）显示 pi 正被当作可编程 agent 框架使用，API 面的扩展性需求上升。

</details>

<details>
<summary><strong>oh-my-pi</strong> — <a href="https://github.com/can1357/oh-my-pi">can1357/oh-my-pi</a></summary>

# 📰 oh-my-pi 社区动态日报（2026-09-14）

## 一、今日速览

今日发布 **v18.1.20**，修复了 Windows 升级后 OAuth 登录持续失败的顽固问题。社区最热话题依然是 **Antigravity（Google AI Pro）429 假配额耗尽**问题——虽有修复但 #11809 报告在 v18.1.18 上仍可复现，#11963 更是挖出了根因：OMP 的 CCA 客户端从未发送 paidTier 参数。此外，#12007 一份涵盖 1448+ 个 dump 文件的深度普查报告揭示了 6 大类可修复的 400 错误及潜在 API key 泄露风险，值得关注。

---

## 二、版本发布

### v18.1.20（@oh-my-pi/pi-ai）
- **修复**：Windows OAuth 登录在升级后持续失败的问题。旧二进制遗留的 stale 原生回调注册此前未被识别为“自有”，导致恢复被阻塞；现在会正确识别并回滚这些 handler。（[#11967](https://github.com/can1357/oh-my-pi/issues/11967)）

---

## 三、社区热点 Issues

### 🔥 1. Antigravity 429 假配额耗尽（主战场）
**#11689** [CLOSED] | 97 评论 | 👍 18
Google AI Pro 用户持续遭遇错误的 429 `RESOURCE_EXSNAUSTED`，即使配额健康。此 issue 已关闭但引发的后续讨论仍在持续。
🔗 [Issue #11689](https://github.com/can1357/oh-my-pi/issues/11689)

### 2. 429 在 v18.1.18 上仍可复现（后续追踪）
**#11809** [OPEN] | 28 评论
用户报告 `gemini-3.8-flash-high` 在最新版上依然立即失败，说明修复不彻底。
🔗 [Issue #11809](https://github.com/can1357/oh-my-pi/issues/11809)

### 3. 根因疑似找到：CCA 客户端未发送 paidTier
**#11963** [OPEN] | 8 评论 | 👍 2
关键发现：OMP 调用 Cloud Code Assist API 时**未选择加入 Google One/AI Ultra 积分**，而官方 `agy` CLI 在同一登录下可以正常工作。这可能就是 429 问题的真正根因，对修复方向有直接指导意义。
🔗 [Issue #11963](https://github.com/can1357/oh-my-pi/issues/11963)

### 4. Antigravity 大面积不可用（今日新增）
**#12019** [OPEN] | 2 评论
今日新报：账户使用率为 0% 且官方端正常，OMP 中却持续 429。标记为 duplicate，但反映受影响用户面仍在扩大。
🔗 [Issue #12019](https://github.com/can1357/oh-my-pi/issues/12019)

### 5. HTTP 400 全面普查 + 潜在 API key 泄露
**#12007** [OPEN] | 4 评论 | prio:p2
对 1571 个 dump 文件的普查归纳出 **6 大类共 53 个可修复的 400 错误**，并指出 `x-goog-api-key` 未列入 dump 脱敏器的 SENSITIVE_HEADERS（18.1.20 上明文泄露未复现）。报告质量极高，是本日最有工程价值的 issue 之一。
🔗 [Issue #12007](https://github.com/can1357/oh-my-pi/issues/12007)

### 6. Advisor 子系统遇 429 即永久“变砖”
**#11947** [OPEN] | 5 评论 | prio:p2
主 agent 和 subagent 每天遭遇上百次 429 都能通过 ~50 秒退避恢复，但 Advisor 遇到第一次就永久死亡——瞬时限流被错误分类为致命错误。
🔗 [Issue #11947](https://github.com/can1357/oh-my-pi/issues/11947)

### 7. Hindsight 心智模型刷新导致缓存前缀反复重写
**#11961** [OPEN] | 5 评论
Hindsight 的 5 分钟 TTL 刷新不断改写 `omp-system` 前缀，导致长会话反复回退到 23,807 token 缓存底线，单次重写 266K–580K token，成本影响显著。
🔗 [Issue #11961](https://github.com/can1357/oh-my-pi/issues/11961)

### 8. auth-gateway 启动后导入的凭据不可见
**#11934** [OPEN] | 6 评论
provider 集合在启动时一次性计算，后续导入的凭据需要重启才能生效，`/v1/models` 返回空列表。
🔗 [Issue #11934](https://github.com/can1357/oh-my-pi/issues/11934)

### 9. `--no-session` 静默丢弃 `--resume`
**#12008** [OPEN] | 3 评论 | prio:p2
组合使用时 `--resume` 被静默忽略，无任何警告，模型看不到历史对话——属于典型的“静默失败”类 UX 陷阱。
🔗 [Issue #12008](https://github.com/can1357/oh-my-pi/issues/12008)

### 10. eval cell 超时引发未捕获异常杀死整个会话
**#11707** [CLOSED] | 7 评论 | prio:p1
持有 in-flight 浏览器桥接调用的 JS eval cell 在 watchdog 触发时抛出逃逸到顶层的 `InvalidStateError`，直接杀死整个会话。p1 级别，已修复关闭。
🔗 [Issue #11707](https://github.com/can1357/oh-my-pi/issues/11707)

---

## 四、重要 PR 进展

### 1. Firefox WebDriver BiDi 浏览器中继支持
**#10295** [feat] | review:p2
通过 Firefox 原生 WebDriver BiDi 端点接入浏览器：可接管现有标签页、观察交互页面内容、截图、管理多命名标签页。显著扩展浏览器工具的浏览器覆盖面。
🔗 [PR #10295](https://github.com/can1357/oh-my-pi/pull/10295)

### 2. 向扩展暴露临时 turn（ephemeral turns）
**#11657** [feat] | review:p2
新增 `ctx.runEphemeralTurn()`，扩展可发起不进入聊天历史的侧 turn，支持 `tools: false` 及 token/context 上限——为扩展生态打开轻量推理能力。
🔗 [PR #11657](https://github.com/can1357/oh-my-pi/pull/11657)

### 3. 会话内热刷新 skills/rules/settings/MCP
**#10288** [feat] | review:p2
免去“改配置必重启”的痛点，正在 Discord 进行功能范围讨论。
🔗 [PR #10288](https://github.com/can1357/oh-my-pi/pull/10288)

### 4. snapcompact 按字节预算限制出站图片
**#10286** [fix] | review:p1
长视觉会话累积的多个小快照帧虽各自不超限，但总量可超预算；此 PR 在请求整形阶段增加 per-provider 字节级钳制。
🔗 [PR #10286](https://github.com/can1357/oh-my-pi/pull/10286)

### 5. MCP 网关冷启动空 tools/list 恢复
**#10222** [fix] | review:p1
修复“成功但为空”的 `tools/list` 在 warmup 期间被缓存为权威结果、污染整个及后续会话的问题，并新增 `/mcp refresh` 手动恢复命令。与今日 #11950（MCP connect 竞态）issue 呼应。
🔗 [PR #10222](https://github.com/can1357/oh-my-pi/pull/10222)

### 6. TODO HUD 关闭状态跨 resume 持久化
**#11194** [fix] | review:p1
修复已完成的 TODO 计划在 resume 后“复活”的问题，将关闭/展开元数据独立持久化。
🔗 [PR #11194](https://github.com/can1357/oh-my-pi/pull/11194)

### 7. `--reapply-config`：resume 时采用当前配置
**#11177** [feat] | review:p2
解决“resume 旧会话时被烘焙的旧 model/thinking/tier 静默套用”的问题，与 #12008 同属 resume 语义改进方向。
🔗 [PR #11177](https://github.com/can1357/oh-my-pi/pull/11177)

### 8. 浏览器中继孤儿 debugger 附件回收
**#9009** [fix] | review:p1
修复 relay 进程死亡后 `chrome.debugger` 附件（及 Chrome 调试提示条）永久残留的问题。
🔗 [PR #9009](https://github.com/can1357/oh-my-pi/pull/9009)

### 9. Advisor 作用域控制与继承禁用
**#11207** [feat] | review:p2
三窗格统一编辑 project/global advisor 配置，支持逐 advisor 启停、状态栏显示、父级禁用向子进程传播。与 #11947（Advisor 变砖）相关，值得关注合并后是否顺带提升健壮性。
🔗 [PR #11207](https://github.com/can1357/oh-my-pi/pull/11207)

### 10. auth-broker 新增 Prometheus /metrics 端点
**#10290** [feat] | review:p2
带 scrape-token 认证的可观测性端点，面向自托管 auth-gateway 运维场景。
🔗 [PR #10290](https://github.com/can1357/oh-my-pi/pull/10290)

---

## 五、功能需求趋势

1. **Provider 健壮性与正确性（最大热点）**：Antigravity 429 系列（#11689/#11809/#11963/#12019）+ auth-gateway 热加载（#11934）+ LiteLLM 视觉误判（#11979），反映社区对多 provider 兼容性的强烈诉求。
2. **TUI/UX 打磨**：Markdown 代码块边框（#9527）、命令建议弹窗（#11946）、内联模型选择器（#11958）、subagent 活动行（#11210）——一批高质量的 opt-in UI 增强 PR 活跃推进中。
3. **会话生命周期与 resume 语义**：#12008、#11177、#9843 显示“resume 时行为可预测”是持续痛点。
4. **上下文/缓存成本优化**：Hindsight 缓存重写（#11961）、agent 自主 compact 工具（#10287）、Venice `prompt_cache_retention`（#8844）。
5. **可观测性与运维**：Prometheus metrics（#10290）、tui.stateFile（#11830）、`/usage` 账户卡片（#11208）。
6. **网络韧性**：断点续传更新（#7733）、Windows 网络环境下的下载可靠性。

---

## 六、开发者关注点

- **Antigravity 用户持续流失风险**：429 问题历经多版本未根治，#11963 的 paidTier 根因分析是当前最高优先级的修复线索，维护者应尽快验证。
- **静默失败模式频发**：`--no-session` 丢弃 `--resume`（#12008）、零字节 heap snapshot（#11785）、auth-gateway 空 models（#11934）——社区反复抱怨“无报错、无警告”的失败路径，建议建立静默失败审计清单。
- **错误分类与恢复策略不统一**：Advisor 遇 429 即死（#11947）vs 主 agent 百次自愈，瞬态/致命错误的分类逻辑需要统一框架。
- **安全相关**：dump 脱敏器遗漏 `x-goog-api-key`（#12007）虽未在最新版复现，但 SENSITIVE_HEADERS 的覆盖机制值得系统性加固；Bedrock 原生认证被安全预检误拒（#12013）也需关注。
- **Windows/WSL 体验仍是薄弱环节**：TUI 无限滚动（#9783）、ranged read 间歇失败（#11284）、WSL 模型搜索（#11953）等问题长期悬挂。

</details>

<details>
<summary><strong>DeepSeek Harness</strong> — <a href="https://github.com/deepseek-ai/deepseek-harness">deepseek-ai/deepseek-harness</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*