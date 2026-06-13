# Hugging Face 热门模型日报 2026-06-13

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-13 07:10 UTC

---

好的，以下是基于您提供的数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年6月13日**

#### **今日速览**

本周 Hugging Face 生态呈现多点爆发态势。**DeepSeek-V4-Pro** 以近5000点赞和超过338万下载量登顶，巩固了其在开源大模型中的领先地位。**Gemma 4** 系列（12B/26B）全面开花，官方模型、量化版（GGUF）及社区微调版（如 abliterated 版本）均进入榜单，展现出成为新一代“全能基座模型”的潜力。值得关注的是，**NVIDIA 的 LocateAnything-3B** 和**Ideogram 4** 模型家族在特定领域（定位、图像生成）表现强势，同时社区在“去审查”（Uncensored）和“消融”（Abliterated）方向的探索依然活跃。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
  - 作者: deepseek-ai | 点赞: 4,799 | 下载: 3,384,418
  - 说明：DeepSeek 最新一代旗舰语言模型，以惊人的点赞和下载量证明了其在开放权重社区中的绝对吸引力。

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**
  - 作者: CohereLabs | 点赞: 338 | 下载: 4,054
  - 说明：Cohere 推出的代码专用小型MoE模型，专为编程场景优化。

- **[XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)**
  - 作者: XiaomiMiMo | 点赞: 99 | 下载: 2,607
  - 说明：小米推出的新一代移动端大模型，采用FP4量化，主打在终端设备上的高效Agent能力。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
  - 作者: nvidia | 点赞: 1,931 | 下载: 149,206
  - 说明：NVIDIA 推出的通用目标定位模型，能通过文本描述在图像中精准定位任意物体，功能强大且下载量极高。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**
  - 作者: google | 点赞: 977 | 下载: 911,544
  - 说明：Google Gemma 4 系列的指令微调版，支持 any-to-any 多模态输入输出，是当前社区最活跃的基座模型之一。

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**
  - 作者: google | 点赞: 639 | 下载: 20,669
  - 说明：Google 推出的 Diffusion 与 LLM 融合模型，在图像到文本任务中展现了强大的生成能力。

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**
  - 作者: ideogram-ai | 点赞: 505 | 下载: 4,987
  - 说明：Ideogram 第四代文生图模型的 FP8 量化版，在保持高质量生成的同时显著降低了资源需求。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**
  - 作者: bosonai | 点赞: 394 | 下载: 29,347
  - 说明：博深AI推出的第四代语音合成模型，使用Qwen3作为基座，生成了非常自然的语音。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**
  - 作者: nvidia | 点赞: 394 | 下载: 3,551
  - 说明：NVIDIA 推出的流式语音识别模型，专为低延迟实时场景设计。

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**
  - 作者: ByteDance | 点赞: 230 | 下载: 373
  - 说明：字节跳动推出的图像+文本到视频模型，在生成视频的连贯性和一致性上表现突出。

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)**
  - 作者: google | 点赞: 185 | 下载: 6,491
  - 说明：Google Magenta 项目的最新成果，支持实时文本到音频生成，是AI音乐/音频生成领域的重要进展。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**
  - 作者: moonshotai | 点赞: 383 | 下载: 0
  - 说明：月之暗面推出的代码专用模型，采用了压缩张量技术，是Kimi家族在垂直领域的深耕。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 点赞: 1,734 | 下载: 2,393,894
  - 说明：基于Qwen 3.6的社区去审查版MoE模型，下载量巨大，反映了社区对无限制对话模型的强烈需求。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 同上，是社区微调与量化的典型代表，且已提供GGUF格式。

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)**
  - 作者: unsloth | 点赞: 219 | 下载: 17,666
  - 说明：Unsloth 平台为 Google 的大型 Diffusion LLM 提供的GGUF量化版，大幅降低了本地部署门槛。

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**
  - 作者: unsloth | 点赞: 570 | 下载: 836,531
  - 说明：Gemma 4 系列最受欢迎的量化版本，下载量仅次于原版，是社区本地运行的首选。

- **[huihui-ai/Huihui-gemma-4-12B-it-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)**
  - 作者: huihui-ai | 点赞: 148 | 下载: 8,013
  - 说明：社区对Gemma 4进行的“消融”微调版本，旨在移除模型的某些限制，是社区探索的新方向。

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**
  - 作者: Jackrong | 点赞: 125 | 下载: 0
  - 说明：基于Qwen 3.6的代码模型GGUF量化版，带有MTP（多Token预测）特性。

- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)**
  - 作者: unsloth | 点赞: 148 | 下载: 221,174
  - 说明：Unsloth提供的大号Gemma 4模型（26B）的量化版，专为高端消费级显卡优化。

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)**
  - 作者: ideogram-ai | 点赞: 328 | 下载: 2,910
  - 说明：Ideogram 4的NF4 4-bit量化版，追求极致的低显存占用。

---

#### **生态信号**

- **模型家族势头正旺**：**Gemma 4 家族**（包括Diffusion模型）和**Qwen 3.6** 是本周最强大的力量。NVIDIA 在专用模型（定位、ASR）和 Google 在音频生成领域的动作也值得关注。**DeepSeek-V4** 作为独立模型保持了超高热度和影响力。
- **开源权重 vs 闭源**：本周榜单完全由开源/开放权重模型主导。DeepSeek、Google、NVIDIA、月之暗面等公司的坚定开放姿态，进一步巩固了Hugging Face作为AI开源核心阵地的地位。
- **量化与微调活动**：Unsloth 依然是量化领域的绝对赢家，包揽了Gemma 4系列最受欢迎的GGUF版本。社区微调方向呈现出 **“暴力去审查”(Uncensored/Aggressive)** 与 **“精准消融”(Abliterated)** 两种截然不同的流派，表明社区在LLM使用自由度的探索上进入更深层次。

#### **值得探索**

1.  **🌟 [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    - **理由**：这是一个“指哪打哪”的视觉定位模型，可以直接通过文本指令在图像中框出物体，应用场景极广（机器人、图像编辑、数据标注），是本榜单中技术范式创新最明显的模型。

2.  **🌟 [unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**
    - **理由**：如果你只有一块消费级显卡，这是体验Google最新多模态大模型的首选。它是连接前沿研究和个人应用的最佳桥梁。

3.  **🌟 [ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**
    - **理由**：作为少数几个上榜的视频生成模型，它不仅代表了字节跳动在多模态领域的积累，其“图像+文本到视频”的特性也预示着个性化内容创作的未来，值得AI视频创作者体验。

---
*本日报由 [agents-radar](https://github.com/Jatway/agents-radar) 自动生成。*