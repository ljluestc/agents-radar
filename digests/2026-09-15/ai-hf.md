# Hugging Face 热门模型日报 2026-09-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-09-15 03:57 UTC

---

# 🤗 Hugging Face 热门模型日报（2026-09-15）

## 📰 今日速览

今日榜单由 **Qwen3.8-27B** 强势领衔（7.7M 下载、1.5 万+ 点赞），其社区量化生态（unsloth GGUF、ISTA-DASLab GSQ、DavidAU 混合微调）全面爆发，形成“一超多强”格局。**DeepSeek-V4.1-Flash** 以多模态文本生成登上周点赞榜首，**MiniMax-H3** 视频生成模型热度飙升并带动 ComfyUI 适配。端侧推理持续升温：Edge0 35B-A3B MoE、MiniCPM5-2B 均以低资源部署为核心卖点。经典基座模型（MiniLM、GPT-2、BERT）下载量依旧坚挺，构成生态底层基础设施。

---

## 🔥 热门模型

### 🧠 语言模型

| 模型 | 作者 | 👍 / ⬇️ | 一句话点评 |
|---|---|---|---|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 15,159 / 7,703,400 | 本周绝对王者，多模态对话旗舰，下载与社区衍生双料冠军 |
| [deepseek-ai/DeepSeek-V4.1-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash) | deepseek-ai | 2,480 / 288,414 | 周点赞第一，图文多模态文本生成，延续 DeepSeek 高性价比路线 |
| [zai-org/GLM-5.3-Flash](https://huggingface.co/zai-org/GLM-5.3-Flash) | zai-org | 2,336 / 1,770,038 | 智谱 Flash 轻量旗舰，多模态对话场景下载表现强劲 |
| [openbmb/MiniCPM5-2B](https://huggingface.co/openbmb/MiniCPM5-2B) | openbmb | 1,402 / 206,774 | 2B 端侧小钢炮，下载量证明端侧部署需求旺盛 |
| [XHToken/Spark-X2.5-4B](https://huggingface.co/Xwen...) | XHToken | 1,176 / 24,084 | 4B 文本生成新秀，社区关注度初显 |
| [TokenRhythm/NeoHorse-1-4B](https://huggingface.co/TokenRhythm/NeoHorse-1-4B) | TokenRhythm | 1,830 / 9,520 | 主打 agentic（智能体）能力的 4B 新模型 |
| [Edge0/Edge0-35B-A3B-preview](https://huggingface.co/Edge0/Edge0-35B-A3B-preview) | Edge0 | 2,121 / 8,109 | 基于 Qwen3.5-MoE 架构的 35B-A3B 稀疏模型，面向 edge-inference，点赞高说明社区对 MoE 端侧化期待极大 |
| [meta-llama/Llama-3.1-8B-Instruct](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct) | meta-llama | 7,606 / 5,620,539 | 长青标杆，仍是无数微调项目的起点 |

### 🎨 多模态与生成

| 模型 | 作者 | 👍 / ⬇️ | 一句话点评 |
|---|---|---|---|
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 5,292 / 4,827,156 | 文/图生视频旗舰，本周视频赛道最大赢家 |
| [Qwen/Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) | Qwen | 5,232 / 645,881 | Qwen4_exp 架构预览版，下一代 Flash 探路 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 3,877 / 1,559,653 | 图/文/视频多入口视频生成，单文件 diffusion 部署友好 |
| [WarmBloodAban/Minimax-h3_Singularity](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity) | WarmBloodAban | 398 / 141,057 | MiniMax-H3 社区衍生，蹭上视频生成东风 |
| [m-a-p/YuE2-3B](https://huggingface.co/m-a-p/YuE2-3B) | m-a-p | 479 / 5,186 | 音乐生成升级版，新增符号规划与 agentic 编辑能力 |
| [tencent/AuK](https://huggingface.co/tencent/AuK) | tencent | 224 / 1,928 | 腾讯零样本 TTS + 语音克隆新作 |

### 🔧 专用模型

| 模型 | 作者 | 👍 / ⬇️ | 一句话点评 |
|---|---|---|---|
| [sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) | sentence-transformers | 5,970 / **252,806,720** | 嵌入界“水电煤”，2.5 亿下载无人能敌 |
| [google/timesfm-3.0-pytorch](https://huggingface.co/google/timesfm-3.0-pytorch) | google | 791 / 826,017 | 时序预测基础模型 3.0，企业预测场景刚需 |
| [openai/clip-vit-base-patch32](https://huggingface.co/openai/clip-vit-base-patch32) | openai | 1,529 / 21,349,787 | 零样本图像分类经典，2 千万级下载常青树 |
| [facebook/mms-300m](https://huggingface.co/facebook/mms-300m) | facebook | 536 / 19,486 | 多语言语音预训练基础模型 |
| [google-bert/bert-base-uncased](https://huggingface.co/google-bert/bert-base-uncased) / [distilbert-base-uncased](https://huggingface.co/distilbert/distilbert-base-uncased) / [gpt2](https://huggingface.co/openai-community/gpt2) | 各家 | 合计 6 千万+ 下载 | 老牌基座，教学与轻量场景仍不可替代 |

### 📦 微调与量化

| 模型 | 作者 | 👍 / ⬇️ | 一句话点评 |
|---|---|---|---|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 4,104 / **10,077,938** | 本周下载榜第一，Qwen3.8 事实上的本地运行标准发行版 |
| [ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF) | ISTA-DASLab | 1,055 / 819,784 | GSQ+RCO 混合精度量化，学术系量化前沿落地 |
| [DavidAU/...TURBO-...-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-TURBO-Fable-Cold-Fusion-735-882-Heretic-Uncensored-NEO-CODER-MAX-MTP-GGUF) | DavidAU | 687 / 875,703 | 命名即风格：无审查+代码强化的社区“缝合怪”，下载意外能打 |
| [nex-agi/Nex-N2.5-Pro](https://huggingface.co/nex-agi/Nex-N2.5-Pro) / [N2.5-mini](https://huggingface.co/nex-agi/Nex-N2.5-mini) | nex-agi | 634 / 30,489；781 / 4,543 | 基于 Qwen3.5-MoE 的多模态微调双子星 |
| [dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8](https://huggingface.co/dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8) | dealignai | 175 / 3,868 | DeepSeek 新王发布即被"UNCENSORED"，FP8 量化 |
| [Alissonerdx/Minimax-H3-ComfyUI](https://huggingface.co/Minimax-H3-ComfyUI) | Alissonerdx | 155 / 13,295 | H3 的 ComfyUI LoRA 适配，工作流生态跟进速度极快 |

---

## 📈 生态信号

**Qwen 家族一家独大**：Qwen3.8-27B 及其衍生（unsloth、ISTA-DASLab、DavidAU、nex-agi）合计下载超 1900 万，衍生生态规模远超其他家族；Qwen3.5-MoE 架构还被 Edge0 等第三方用作基座，说明 Qwen 的架构本身已成开源基础设施。**开源权重持续碾压**：榜单前列几乎全部为可下载权重模型，DeepSeek、MiniMax、智谱等中国团队贡献了本周最热的新发布。**量化活动活跃**：GGUF 仍是本地部署主流，GSQ/RCO、FP8 等新量化格式开始抢份额；“uncensored”社区微调（DavidAU、dealignai）热度不减。**端侧+MoE** 是本周关键词，视频生成生态（ComfyUI LoRA）对新模型的响应速度已缩短至发布当周。

---

## 💎 值得探索

1. **[Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) + [unsloth GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)**：本周生态中心，无论研究还是本地部署都是首选起点。
2. **[Edge0-35B-A3B-preview](https://huggingface.co/Edge0/Edge0-35B-A3B-preview)**：35B 总参 / 3B 激活的 MoE + MLX 格式，代表端侧推理的新方向，点赞/下载比极高，值得关注其正式版。
3. **[ISTA-DASLab GSQ-RCO 量化](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF)**：学术前沿量化方案（GSQ + 混合精度 RCO），适合想压榨极限显存的进阶用户研究对比。

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*