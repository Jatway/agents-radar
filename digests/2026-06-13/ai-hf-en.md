# Hugging Face Trending Models Digest 2026-06-13

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-13 07:10 UTC

---

Here is the structured **Hugging Face Trending Models Digest** for **June 13, 2026**.

---

### 1. Today's Highlights

DeepSeek continues its reign, with **DeepSeek-V4-Pro** dominating the week with nearly 4,800 likes and over 3.3 million downloads, signaling the market’s insatiable appetite for high-capacity open-weight conversational models. Google’s **Gemma 4 family** is the most prolific ecosystem this week, spawning numerous quantizations (GGUF, QAT) and community fine-tunes like the "Obliterated" and "Abliterated" variants, demonstrating peak activity around accessible, mid-scale any-to-any models. Nvidia’s **LocateAnything-3B** stands out as a specialist success, breaking into the top three with strong downloads for a targeted image-feature-extraction model. Hugging Face is seeing a notable surge in **unified multimodal models** (text, image, audio in one pipeline), marking a clear shift away from single-modality backbones.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | Likes: 4,799 | Downloads: 3,384,418  
  DeepSeek's flagship MoE conversational model is the top trending model this week, driven by its massive scale, strong benchmark performance, and open-weight availability.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — google | Likes: 977 | Downloads: 911,544  
  Google's efficient any-to-any instruction-tuned model sees explosive adoption due to its small footprint and unified multimodal pipeline.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs | Likes: 338 | Downloads: 4,054  
  A compact MoE code-generation model from Cohere, trending for its promise of efficient coding assistance with a low parameter count.

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — unsloth | Likes: 570 | Downloads: 836,531  
  The most popular community quantization of the Gemma-4-12B-it, allowing broad deployment on consumer hardware.

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — OBLITERATUS | Likes: 259 | Downloads: 43,578  
  An "uncensored" fine-tune of Gemma-4-12B, trending in the adult/uncensored model niche.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — google | Likes: 639 | Downloads: 20,669  
  A diffusion-based multimodal model combining Gemma’s LLM backbone with image generation, trending as a novel hybrid architecture.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | Likes: 1,931 | Downloads: 149,206  
  Nvidia’s image-feature-extraction model for object detection and localization is hugely popular for its speed and accuracy in vision workflows.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — ideogram-ai | Likes: 505 | Downloads: 4,987  
  Ideogram v4 in FP8 quantization, trending for high-quality text-to-image generation with reduced memory requirements.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai | Likes: 394 | Downloads: 29,347  
  A 4B parameter TTS model fine-tuned on Qwen3, noted for natural prosody and low latency.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — ByteDance | Likes: 230 | Downloads: 373  
  ByteDance’s image-to-video renderer, attracting attention for realistic animation from a single image.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — google | Likes: 185 | Downloads: 6,491  
  Google’s real-time text-to-audio model for music generation, trending among AI music creators.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | Likes: 383 | Downloads: 0  
  A compressed vision-language model specialized for code, notable for achieving strong coding performance in a small package.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | Likes: 394 | Downloads: 3,551  
  A lightweight streaming ASR model from Nvidia, trending for real-time speech recognition applications.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | Likes: 1,734 | Downloads: 2,393,894  
  The most-downloaded uncensored GGUF variant of the Qwen 3.6 vision MoE, widely used for roleplay and unfiltered generation.

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — unsloth | Likes: 219 | Downloads: 17,666  
  Unsloth’s GGUF quantization of the DiffusionGemma model, enabling diffusion transformers on CPU/edge devices.

- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — unsloth | Likes: 207 | Downloads: 208,889  
  A quantization-aware training (QAT) GGUF variant of Gemma-4-12B-it, trending for optimized inference on low-resource hardware.

- **[huihui-ai/Huihui-gemma-4-12B-it-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)** — huihui-ai | Likes: 148 | Downloads: 8,013  
  An "abliterated" (refusal-removed) fine-tune of Gemma-4-12B-it, popular in the community for unrestricted conversations.

---

### 3. Ecosystem Signal

The dominant trend this week is the **rise of unified any-to-any models**, spearheaded by Google’s **Gemma 4 family** (12B and 26B MoE). These models accept and produce text, images, and audio through a single pipeline, and the sheer volume of downstream quantizations (GGUF, QAT, FP8) from Unsloth indicates a community that wants to run these on consumer GPUs and edge devices. **DeepSeek-V4-Pro** remains the absolute leader in downloads and likes, confirming that large MoE conversational models are the top consumer choice despite requiring significant hardware.

Open-weight models continue to dominate the top 30; no proprietary API-only models broke into this week’s rankings. The **uncensored/abliterated** sub-ecosystem is highly active, with variants for Qwen 3.6, Gemma 4, and older architectures. Additionally, **ideogram-4** quantizations (FP8, NF4) suggest a growing demand for high-quality open image generation models that compete with closed services like DALL·E or Midjourney.

---

### 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — An excellent model to study for production-grade vision pipelines: it’s small, fast, and achieves strong localization accuracy. Perfect for downstream tasks like object detection or visual grounding.

2. **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — A unique combination of a Gemma language model with diffusion image generation in a single architecture. This represents the future of "native" generation, where models create images without a separate decoder.

3. **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — For anyone working on video generation, this Apache 2.0 licensed image-to-video model is worth trying for its high-quality animation from a single image, opening up new creative and scientific applications.

---
*This digest is auto-generated by [agents-radar](https://github.com/Jatway/agents-radar).*