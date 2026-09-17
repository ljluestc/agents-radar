# Hugging Face 热门模型日报 2026-09-17

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-09-17 04:00 UTC

---

# 🤗 Hugging Face 热门模型日报
**日期：2026-09-17**

---

## 📌 今日速览

Qwen3.8-27B 以超过 766 万周下载量、1.5 万点赞成为本周绝对焦点，其 GGUF 量化版本（unsloth、ISTA-DASLab）同样霸榜，显示端侧部署需求旺盛。国产阵营集体发力：DeepSeek-V4.1-Flash、MiniMax-H3、GLM-5.3-Flash、ZDTaichu5.0 等新模型密集上榜。视频生成赛道 LTX-2.5 与 MiniMax-H3 双雄并立，音频领域 YuE2 音乐生成和腾讯 AuK 零样本 TTS 带来惊喜。社区量化与“解对齐”微调（如 DavidAU、dealignai）围绕头部新模型快速跟进，生态响应速度极快。

---

## 🔥 热门模型

### 🧠 语言模型

- **[Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)**
  作者：Qwen ｜ 👍 15,421 ｜ ⬇️ 7,667,556
  本周榜单位居第一的多模态对话旗舰，下载量惊人，是当前开源社区的事实性基准模型。

- **[deepseek-ai/DeepSeek-V4.1-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash)**
  作者：deepseek-ai ｜ 👍 2,874 ｜ ⬇️ 366,459
  DeepSeek 最新轻量级多模态模型，发布即登趋势榜，延续高性价比路线。

- **[Qwen/Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next)**
  作者：Qwen ｜ 👍 5,316 ｜ ⬇️ 689,347
  Qwen3.8 家族的高速推理变体，采用全新 qwen4_exp 架构，社区期待值高。

- **[zai-org/GLM-5.3-Flash](https://huggingface.co/zai-org/GLM-5.3-Flash)**
  作者：zai-org ｜ 👍 2,394 ｜ ⬇️ 2,244,085
  智谱新一代轻量多模态模型，下载量已破 220 万，国产开源竞争力持续增强。

- **[openbmb/MiniCPM5-2B](https://huggingface.co/openbmb/MiniCPM5-2B)**
  作者：openbmb ｜ 👍 1,509 ｜ ⬇️ 324,322
  2B 端侧小模型迭代，下载量扎实，是移动端部署的热门选择。

- **[TokenRhythm/NeoHorse-1-4B](https://huggingface.co/TokenRhythm/NeoHorse-1-4B)**
  作者：TokenRhythm ｜ 👍 2,132 ｜ ⬇️ 16,163
  基于 Qwen3.5-Text 的 Agentic 专用 4B 模型，反映了智能体微调的社区热度。

- **[Edge0/Edge0-35B-A3B-preview](https://huggingface.co/Edge0/Edge0-35B-A3B-preview)**
  作者：Edge0 ｜ 👍 3,150 ｜ ⬇️ 27,759
  35B 总参数 / 3B 激活的 MoE 边缘推理模型，提供 MLX 格式，主打 Apple 生态本地部署。

- **[XHToken/Spark-X2.5-4B](https://huggingface.co/XHToken/Spark-X2.5-4B)**
  作者：XHToken ｜ 👍 1,236 ｜ ⬇️ 27,191
  社区自研 4B 通用模型，进入趋势榜显示中小型社区原创力量崛起。

- **[TaichuAI/ZDTaichu5.0-9B](https://huggingface.co/TaichuAI/ZDTaichu5.0-9B)**
  作者：TaichuAI ｜ 👍 155 ｜ ⬇️ 213
  强调空间推理的 9B 视觉语言模型，刚发布，值得关注后续表现。

### 🎨 多模态与生成

- **[Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5)**
  作者：Lightricks ｜ 👍 4,122 ｜ ⬇️ 1,616,663
  图生视频 / 文生视频 / 视频到视频全能模型，本周生成类最热发布之一。

- **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)**
  作者：MiniMaxAI ｜ 👍 5,385 ｜ ⬇️ 4,689,062
  国产视频生成旗舰，下载近 470 万，与 LTX-2.5 形成本周视频赛道双雄。

- **[m-a-p/YuE2-3B](https://huggingface.co/m-a-p/YuE2-3B)**
  作者：m-a-p ｜ 👍 650 ｜ ⬇️ 9,391
  音乐生成模型，新增符号规划与 Agentic 编辑能力，音频生成创新代表。

- **[tencent/AuK](https://huggingface.co/tencent/AuK)**
  作者：tencent ｜ 👍 272 ｜ ⬇️ 2,753
  腾讯零样本 TTS 与语音克隆模型，刚上榜的新秀。

- **[Comfy-Org/YuE2](https://huggingface.co/Comfy-Org/YuE2)**
  作者：Comfy-Org ｜ 👍 152 ｜ ⬇️ 59,231
  YuE2 的 ComfyUI 集成版本，体现工具链对音乐生成的快速适配。

### 🔧 专用模型

- **[sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)**
  作者：sentence-transformers ｜ 👍 6,025 ｜ ⬇️ 256,481,161
  嵌入模型长青之王，周下载 2.56 亿，是 RAG 与语义检索的默认选择。

- **[openai/clip-vit-base-patch32](https://huggingface.co/openai/clip-vit-base-patch32)**
  作者：openai ｜ 👍 1,547 ｜ ⬇️ 21,790,053
  零样本图像分类经典，下载量依然恐怖，多模态应用的基石。

- **[facebook/mms-300m](https://huggingface.co/facebook/mms-300m)**
  作者：facebook ｜ 👍 554 ｜ ⬇️ 22,119
  多语言语音预训练模型，覆盖千余语言的语音任务底座。

- **[google-bert/bert-base-uncased](https://huggingface.co/google-bert/bert-base-uncased)**
  作者：google-bert ｜ 👍 3,354 ｜ ⬇️ 47,693,504
  教科书级 NLP 基座，下载量长期霸榜，工业界仍是常客。

- **[distilbert/distilbert-base-uncased](https://huggingface.co/distilbert/distilbert-base-uncased)**
  作者：distilbert ｜ 👍 1,459 ｜ ⬇️ 7,410,664
  BERT 蒸馏版，轻量 NLP 任务的性价比之选。

- **[openai-community/gpt2](https://huggingface.co/openai-community/gpt2) ｜ [meta-llama/Llama-3.1-8B-Instruct](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct)**
  下载量 1,558 万 / 586 万。两代开源里程碑模型，长尾使用需求持续。

### 📦 微调与量化

- **[unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)**
  作者：unsloth ｜ 👍 4,224 ｜ ⬇️ 8,856,150
  本周下载量最高的模型（885 万），量化版甚至超过原版，端侧需求可见一斑。

- **[ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF)**
  作者：ISTA-DASLab ｜ 👍 1,201 ｜ ⬇️ 956,964
  学术机构出品的 GSQ+RCO 混合精度量化方案，下载近百万，量化研究实用化代表。

- **[DavidAU/Qwen3.8-27B-TURBO-...-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-TURBO-Fable-Cold-Fusion-735-882-Heretic-Uncensored-NEO-CODER-MAX-MTP-GGUF)**
  作者：DavidAU ｜ 👍 802 ｜ ⬇️ 1,049,586
  经典“命名艺术”风格的无审查融合微调 + GGUF，下载破百万，社区口味独特。

- **[ukisai/Swift-Qwen3.8-27B-GGUF](https://huggingface.co/ukisai/Swift-Qwen3.8-27B-GGUF) / [Swift-Qwen3.8-27b](https://huggingface.co/ukisai/Swift-Qwen3.8-27b)**
  作者：ukisai ｜ 👍 189/334 ｜ ⬇️ 55,309/2,753
  主打 "efficient-thinking"（高效思考）的 Qwen3.8 微调及量化版。

- **[WarmBloodAban/Minimax-h3_Singularity](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity)**
  作者：WarmBloodAban ｜ 👍 451 ｜ ⬇️ 164,451
  MiniMax-H3 的社区微调变体，视频模型微调开始流行。

- **[dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8](https://huggingface.co/dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8)**
  作者：dealignai ｜ 👍 233 ｜ ⬇️ 6,826
  DeepSeek-V4.1-Flash 发布即被"解对齐”+ FP8 量化，社区反应速度极快。

---

## 🌐 生态信号

本周生态呈现三大特征。**其一，Qwen3.8 家族一家独大**：原版、Flash-Next、unsloth GGUF、GSQ 量化、DavidAU 融合版、社区微调版多点开花，形成“发布—量化—微调”的 48 小时生态闭环，Qwen 已成为开源 LLM 的事实标准底座。**其二，中国厂商新模型密集发布**（DeepSeek、MiniMax、智谱、腾讯、面壁、TaichuAI），覆盖 LLM、视频、TTS、音乐全模态，开源权重策略持续对闭源 API 施压。**其三，量化技术走向精细化**：ISTA-DASLab 的 GSQ-RCO 混合精度方案下载近百万，unsloth GGUF 超 885 万下载，证明端侧/本地推理是当下最强需求牵引；同时“解对齐”微调（UNCENSORED、Heretic）围绕每个头部新模型快速出现，社区对模型可控性的诉求持续存在。

---

## 💎 值得探索

1. **[Qwen/Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next)** — 全新 qwen4_exp 架构的首个公开实现，可能是下一代 Qwen 架构的风向标，研究者和早期采用者不应错过。

2. **[ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF)** — GSQ+RCO 混合精度量化是当前前沿压缩技术，对比 unsloth 常规 GGUF 可评估新型量化在精度-体积上的实际收益，适合本地部署玩家深度测试。

3. **[m-a-p/YuE2-3B](https://huggingface.co/m-a-p/YuE2-3B)** — 音乐生成 + 符号规划 + Agentic 编辑的组合非常新颖，且已有 ComfyUI 集成版（[Comfy-Org/YuE2](https://huggingface.co/Comfy-Org/YuE2)），上手门槛低，是多模态生成领域最具实验价值的方向之一。

---
*本日报由 [agents-radar](https://github.com/rollysys/agents-radar) 自动生成。*