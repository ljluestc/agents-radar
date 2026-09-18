# Hugging Face 热门模型日报 2026-09-18

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-09-18 03:47 UTC

---

# 📊 Hugging Face 热门模型日报
**日期：2026-09-18**

---

## 一、今日速览

今日榜单呈现“多模态 + 端侧推理”双主线：**Qwen3.8-27B**（15,548 赞、745 万下载）继续统治生态，围绕它的量化与微调版本占据多个席位。视频生成领域迎来爆发，**LTX-2.5** 与 **MiniMax-H3** 双双进入点赞榜前列。**Edge0-35B-A3B**（MoE 架构、MLX 端侧部署）以 3,316 赞登顶周榜，显示 Apple Silicon 本地推理需求旺盛。此外，**DeepSeek-V4.1-Flash**（多模态、39 万下载）和 **GLM-5.3-Flash**（244 万下载）代表国产开源大厂的最新攻势。

---

## 二、热门模型

### 🧠 语言模型

| 模型 | 作者 | 👍 / 📥 | 一句话说明 |
|---|---|---|---|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 15,548 / 7.46M | 本周期绝对王者，多模态对话旗舰，生态衍生版本最多的基础模型 |
| [Qwen/Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) | Qwen | 5,368 / 706K | Qwen3.8 轻量高速版，采用 qwen4_exp 新架构，性价比推理首选 |
| [zai-org/GLM-5.3-Flash](https://huggingface.co/zai-org/GLM-5.3-Flash) | zai-org | 2,428 / 2.45M | 智谱最新 Flash 级多模态模型，下载量证明其生产级采用度 |
| [deepseek-ai/DeepSeek-V4.1-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash) | deepseek-ai | 3,022 / 391K | DeepSeek V4.1 系列图像-文本模型，延续“低价高能”路线 |
| [Edge0/Edge0-35B-A3B](https://huggingface.co/Edge0/Edge0-35B-A3B-preview) | Edge0 | 3,316 / 37K | 周点赞榜第一：35B 总参 / 3B 激活的 MoE，主打 MLX 边缘端推理 |
| [TokenRhythm/NeoHorse-1-4B](https://huggingface.co/TokenRhythm/NeoHorse-1-4B) | TokenRhythm | 2,339 / 20K | 基于 qwen3_5_text 的 Agentic 小模型，4B 尺寸面向 Agent 工作流 |
| [TokenRhythm/NeoHorse-1-9B](https://huggingface.co/TokenRhythm/NeoHorse-1-9B) | TokenRhythm | 879 / 9.9K | NeoHorse 系列 9B 版，同走 agentic 路线 |
| [openbmb/MiniCPM5-2B](https://huggingface.co/openbmb/MiniCPM5-2B) | openbmb | 1,540 / 330K | 面壁第五代 2B 端侧模型，下载量体现移动端部署热度 |
| [XHToken/Spark-X2.5-4B](https://huggingface.co/XHToken/Spark-X2.5-4B) | XHToken | 1,264 / 28K | 4B 级新晋文本模型，社区关注度快速爬升 |
| [meta-llama/Llama-3.1-8B-Instruct](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct) | meta-llama | 7,697 / 5.89M | 常青树基线模型，仍是微调和评测的默认参照 |
| [nex-agi/Nex-N2.5-mini](https://huggingface.co/nex-agi/Nex-N2.5-mini) | nex-agi | 832 / 7.3K | qwen3_5_moe 架构小型多模态模型 |
| [XingChen-AGI/Xing4.0-29B-A4B](https://huggingface.co/XingChen-AGI/Xing4.0-29B-A4B) | XingChen-AGI | 233 / 61 | 29B 总参 / 4B 激活 MoE 新秀，早期热度观察中 |
| [openai-community/gpt2](https://huggingface.co/openai-community/gpt2) | openai-community | 4,138 / 15.6M | 教科书级经典，教育与研究场景持续贡献下载 |

### 🎨 多模态与生成

| 模型 | 作者 | 👍 / 📥 | 一句话说明 |
|---|---|---|---|
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 5,421 / 4.58M | 本周期最强视频生成模型之一，文本/图像到视频，下载量惊人 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 4,243 / 1.60M | 点赞最高的视频模型，支持图/文/视频多入口生成，ComfyUI 生态友好 |
| [m-a-p/YuE2-3B](https://huggingface.co/m-a-p/YuE2-3B) | m-a-p | 732 / 11.6K | 3B 音乐生成模型，主打符号规划与“Agentic 编辑”能力 |
| [Comfy-Org/YuE2](https://huggingface.co/Comfy-Org/YuE2) | Comfy-Org | 169 / 79.3K | YuE2 的 ComfyUI 集成版，下载量远超原版，印证工作流生态力量 |
| [tencent/AuK](https://huggingface.co/tencent/AuK) | tencent | 290 / 3.0K | 腾讯零样本 TTS + 语音克隆，音频赛道新玩家 |
| [WarmBloodAban/Minimax-h3_Singularity](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity) | WarmBloodAban | 481 / 182K | MiniMax-H3 社区改编版，18 万下载显示视频模型二创活跃 |
| [TaichuAI/ZDTaichu5.0-9B](https://huggingface.co/TaichuAI/ZDTaichu5.0-9B) | TaichuAI | 173 / 476 | 9B 视觉语言模型，主打空间推理，早期阶段 |

### 🔧 专用模型

| 模型 | 作者 | 👍 / 📥 | 一句话说明 |
|---|---|---|---|
| [sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) | sentence-transformers | 6,049 / 255.6M | 嵌入领域的“水电煤”，2.5 亿下载量是全站生产力基石 |
| [harshatheg/Qwen-2.5-1B-RLCD](https://huggingface.co/harshatheg/Qwen-2.5-1B-RLCD) | harshatheg | 293 / 0 | 面向 Apple Silicon 的结构化/受限解码实验模型，MLX 生态探索 |

### 📦 微调与量化

| 模型 | 作者 | 👍 / 📥 | 一句话说明 |
|---|---|---|---|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 4,273 / 8.21M | Qwen3.8 官方量化的最强替代品，820 万下载是本地部署热度的直接证据 |
| [ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF) | ISTA-DASLab | 1,266 / 1.03M | 学术团队的 GSQ+RCO 混合精度量化，百万下载显示前沿压缩技术落地迅速 |
| [DavidAU/Qwen3.8-27B-...-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-TURBO-Fable-Cold-Fusion-735-882-Heretic-Uncensored-NEO-CODER-MAX-MTP-GGUF) | DavidAU | 853 / 1.12M | 典型 DavidAU 式“炼丹”合并模型，无审查 + 编码增强，社区需求旺盛 |
| [ukisai/Swift-Qwen3.8-27B](https://huggingface.co/ukisai/Swift-Qwen3.8-27b) / [GGUF](https://huggingface.co/ukisai/Swift-Qwen3.8-27B-GGUF) | ukisai | 398 / 239 + GGUF 73K | 主打"efficient-thinking"的轻推理微调，GGUF 版下载量是原版 20 倍 |
| [prism-ml/Ternary-Bonsai-2-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-2-27B-gguf) | prism-ml | 281 / 0 | 三值（2-bit）极端量化实验，代表极限压缩前沿 |
| [dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8](https://huggingface.co/dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8) | dealignai | 267 / 32K | DeepSeek V4.1 Flash 无审查 FP8 重制版 |
| [Agnes-AI/Agnes-3.0-Flash](https://huggingface.co/Agnes-AI/Agnes-3.0-Flash) | Agnes-AI | 215 / 1.2K | 新晋社区多模态微调，早期观察 |

---

## 三、生态信号

**Qwen3.8 已形成“事实标准”级生态**：本周 30 个热门模型中约 1/3 直接基于 Qwen3.8 或其衍生（unsloth GGUF、ISTA-DASLab GSQ 量化、DavidAU 合并、ukisai 微调），其地位相当于鼎盛时期的 Llama-3。**开源权重持续压倒闭源**：榜单前列清一色为开放权重模型，闭源厂商基本缺席 Hub 热榜。**量化活动异常活跃且技术升级**：从传统 GGUF 到 GSQ-RCO 混合精度、三值量化，说明本地部署需求正推动压缩科学前沿。**MoE + 边缘部署是新叙事**：Edge0-35B-A3B、Xing4.0-29B-A4B、Nex-N2.5-mini 均采用“大总参、小激活”策略，配合 MLX/llama.cpp 打入消费级硬件。**视频生成进入“Qwen 时刻”**：MiniMax-H3 与 LTX-2.5 的下载量级已接近头部 LLM。

---

## 四、值得探索

1. **[Edge0/Edge0-35B-A3B](https://huggingface.co/Edge0/Edge0-35B-A3B-preview)** — 周点赞第一，35B-A3B MoE + MLX 原生支持，是当前“Mac 本地跑大模型”叙事的最佳样本，值得端侧开发者实测激活参数下的吞吐与质量权衡。

2. **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — 458 万下载的视频生成旗舰，且已有活跃社区二创（Singularity 版），生态正反馈明显，适合视频创作者与 AIGC 应用团队评估。

3. **[ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF)** — 学术前沿量化方案（GSQ + RCO 混合精度）快速落地的典范，比标准 GGUF 更省显存，量化研究者与极限压缩玩家不容错过。

---
*数据来源：Hugging Face Hub 周榜（2026-09-18）*

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*