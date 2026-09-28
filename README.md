---
language:
  - en
  - zh
license: apache-2.0
license_name: Apache License 2.0
tags:
  - audio
  - audio-editing
  - icassp2027
  - agent-track
library_name: pytorch
---

# Model Card — ICASSP 2027 Audio Editing Challenge (GC-4) weights

> **状态（2026-09-28 22:5x）**：许可（Apache-2.0 + NOTICE 归属声明）、仓库标识
> （owner/repo = `jxzhen/aec-2027-editx-lora`，tag `v1.0`）、校验值、**第 1 节权重来源**
> （产出方式／训练数据／训练代码／教师模型与其许可）、**第 5 节使用示例**、**第 6 节限制声明**
> **均已填真**。
> 仍带 `<>` 的字段**只剩"发布那一刻才产生"的事实**：**首次公开时间（UTC）+ 40 位 commit ID**
> （第 3 节表内、第 4 节末行）—— 这是唯一必须由人工在发布时回填的部分。
> `tools/stage_weights.py` **不会**改写本文件，`tools/preflight_release.py` 也只检查必备段是否齐全、
> **查不出**残留的尖括号占位符 —— 发布前务必人工逐项核对。

## 1. 权重来源（Source of weights）

- **产出方式**：**蒸馏（自蒸馏）**。本产物是在上游基座 `stepfun-ai/Step-Audio-EditX`
  之上训练的 **LoRA adapter**（**不是**全量权重）。训练目标（"编辑后"音频的离散声学编码）
  由**基座自身**在给定的（源音频, 编辑指令）对上**在线合成**得到（self-distillation），
  再以这些自蒸馏样本微调 LoRA。
- **训练数据**：源音频池共 **68 条**，其中 **60 条**取自公开语料 **LibriSpeech**
  （OpenSLR SLR12；许可证 **CC BY 4.0**；https://www.openslr.org/12 ）的 `clean` 配置
  **dev-clean** 子集（16 kHz、时长 1.5–15 s，落盘目录 `data/libri60/`），其余为上游仓库自带示例音频；
  **编辑对**（源音频 → 编辑后音频）**全部由教师模型在线合成**，**未使用任何私有数据**。
  本次 LoRA 训练**实际使用其中 12 条编辑对**（编辑类型为情感类：fear / happy / sad / angry），
  训练 **24 步**（配置：LoRA r=16 ｜ α=32 ｜ dropout=0.05 ｜ lr=1e-4 ｜ 8 epoch × 3 step ｜ max_seq=1280）。
- **训练代码**：**未随本仓库单独公开发布**。可运行的复现包（**Docker 镜像 + 运行脚本（sh）
  + 固定随机种子 `20260928`**）将于 **2026-12-07 复现检查**时提交组委会
  （官方答复第 13 条：届时另行收集）；如需提前获取，请联系作者。
- **若为蒸馏**：教师模型 = **`stepfun-ai/Step-Audio-EditX`**（公开标识即上游基座本身，
  对应官方答复第 5 条"蒸馏教师只需公开标识"）
  ｜ 该教师模型的**许可类型**：上游仓库的**代码**以 **Apache-2.0** 发布
  （已实测：其模型卡 `license` 字段为空、仓库内无独立 `LICENSE` 文件 —— 许可口径见第 2 节）
  ｜ **兼容性判断**：**同基座自蒸馏**（教师与学生同源），**不引入任何新的上游依赖**，
  与本产物的 Apache-2.0 声明一致，**无许可相容性冲突**。
- **作者**：Jianxi Zheng

## 2. 许可（License）

- **本权重采用**：**Apache License 2.0**（全文见 `LICENSE`；归属声明见 `NOTICE`）。
- **选择依据**：本产物是**在 `stepfun-ai/Step-Audio-EditX` 之上训练的 LoRA adapter**，
  属派生作品。已实测确认的事实是：该上游仓库的**代码**以 Apache-2.0 发布
  （API `cardData.license` 字段为空；仓库内 raw `LICENSE` 请求返回 404）。
  因此我们采取的做法是：**沿用 Apache-2.0 作为本产物的许可**，并在 `NOTICE` 中
  明确写出上游出处、上游代码的 Apache-2.0 许可，以及上游 model card 的
  Usage Disclaimer（禁止未授权声音克隆等）**同样适用于本派生产物**。
  本仓库**不重新分发**任何上游基座权重或第三方权重，只分发我们自己训练的 adapter。

> 注意：蒸馏或微调产物是**派生作品**，其分发许可能受上游模型许可约束。

## 3. 公开时间声明（Critical for 2026-10-01）

> **本权重首次公开发布于 `2026-09-28T16:30:20+00:00`（UTC）。**

依据 ICASSP 2027 Audio Editing Challenge 组委会 2026-09-17 回信第 3 条与第 5 条：

- Agent Track 所用**全部模型组件**（含 LLM、分离模型、声码器及任何 LoRA / adapter，
  包括自训 / 微调 / 蒸馏组件）的**实际权重**，必须在 **2026-10-01 之前**已公开发布。
- **2026-10-01 当日或之后才发布的，不得引入 Agent Track 提交。**
- 该版本在截止日前**已公开可得**的证据形式（详见第 4 节）。
- **禁止**在提交截止（2026-11-25）或复现检查（2026-12-07）前才发布权重。

**本仓库的公开时间证据**：

| 载体 | URL | 时间（UTC） |
|---|---|---|
| `huggingface.co` commit（**主载体**） | `https://huggingface.co/jxzhen/aec-2027-editx-lora/commit/b6d1621d583e6109ccc09f3e2dbe67b8d1820494` | `2026-09-28T16:30:20+00:00` |
| GitHub Release（**第二载体**） | `https://github.com/jxzhen/aec-2027-editx-lora/releases/tag/v1.0` | `<UTC>` |

## 4. 完整性校验（SHA-256）

组委会将**自行抓取本仓库权重并重算 SHA-256**，与本仓库声明的值比对。因此：

- 完整文件清单（含全部 shard 与任何额外 LoRA / adapter）：`weights/MANIFEST.json`
- 逐文件校验和（`sha256sum` 格式）：`weights/SHA256SUMS.txt`
- `SHA256SUMS.txt` 自身的 sha256：`5ccf47797f9a5b8abe3ff5524ae8f7f24c1a1631027c8186cfdd94c33be76c7f`

**校验方式**（任何第三方可独立复现）：

```bash
# 拉取本仓库后，在 weights/ 目录内执行：
sha256sum -c SHA256SUMS.txt
```

**重要约束**：

- **必须保存原始权重文件。** 重新保存或转换会改变 checksum，即使张量数值未变。
- **任何格式转换须事先向组委会说明。** 未经报备的转换会使提交证据链断裂。

**本仓库的确切版本标识（commit ID）**：`b6d1621d583e6109ccc09f3e2dbe67b8d1820494`

## 5. 使用方式

```python
# 最小加载示例（需要 transformers + peft）
# 本仓库的 adapter 文件位于 weights/files/（adapter_model.safetensors + adapter_config.json）
from transformers import AutoModelForCausalLM, AutoTokenizer
from peft import PeftModel

BASE  = "stepfun-ai/Step-Audio-EditX"          # 上游基座（本仓库不重分发其权重）
tok   = AutoTokenizer.from_pretrained(BASE, trust_remote_code=True)
model = AutoModelForCausalLM.from_pretrained(BASE, trust_remote_code=True, torch_dtype="bfloat16")
model = PeftModel.from_pretrained(model, "jxzhen/aec-2027-editx-lora", subfolder="weights/files")
model.eval()
```

> 说明：以上只演示**如何把本 adapter 挂到基座上**；音频编辑的端到端推理还需要上游
> `Step-Audio-EditX` 的音频 tokenizer 与声码器（CosyVoice-300M-25Hz），请按其仓库 README 执行。

## 6. 已知限制与伦理声明

- **适用范围**：ICASSP 2027 Audio Editing Challenge（Agent Track）参赛与学术研究；
  面向**英语朗读语音**上的**情感类编辑指令**（fear / happy / sad / angry）。
- **不适用场景**：**禁止**用于未经授权的语音克隆、身份仿冒、欺诈或任何误导性用途；
  不得用于生成对真实人物的未授权模仿音频。
- **潜在偏见与局限**：训练样本极少（**12 条自蒸馏编辑对**），源语音为英语朗读语料，
  覆盖面窄，**不保证**跨语言、含噪、多说话人场景下的效果；本阶段**未做人工听测**，
  不声明任何评测分数，也不声称与任何"官方基线"可比。
- **音频内容来源合规性**：训练源音频为公开语料 LibriSpeech（**CC BY 4.0**）；
  编辑目标由教师模型合成；本仓库**不重新分发**任何上游基座权重或第三方权重。
- 本权重仅用于 ICASSP 2027 Audio Editing Challenge 参赛与学术研究。

## 7. 联系方式

- Jianxi Zheng ｜ `hunan08182026@126.com`
