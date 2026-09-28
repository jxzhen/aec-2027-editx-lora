# Weights Release — ICASSP 2027 Audio Editing Challenge

> 本 Release 的发布时间由 GitHub 平台记录（`published_at`），是组委会 2026-09-17 回信
> 第 5 条要件④承认的**平台侧公开证据**。本次公开时间**早于 2026-10-01**。

## 本版本（`v1.0`）

- **首次公开时间（UTC）**：`2026-09-28T16:30:20+00:00`
- **提交标识（commit ID）**：`b6d1621d583e6109ccc09f3e2dbe67b8d1820494`
- **权重实体**：见下方附件（Assets）
- **主载体（Hugging Face）**：`https://huggingface.co/jxzhen/aec-2027-editx-lora`
- **第二载体（本 GitHub Release）**：本页
- **作者**：Jianxi Zheng

## 合规声明（对应挑战赛组委会 2026-09-17 回信第 3、5 条）

本版本权重**已在本 Release 发布之时公开发布**，该时间**早于 2026-10-01**，
满足 Agent Track 对"所用全部模型组件（含自训 / 微调 / 蒸馏组件）的实际权重
必须在 2026-10-01 之前已公开发布"的要求。

**本 Release 针对的权重版本**：

- 完整文件清单（含全部 shard 与任何额外 LoRA / adapter）：`MANIFEST.json`
- 逐文件 SHA-256：`SHA256SUMS.txt`
- `SHA256SUMS.txt` 自身 sha256：`5ccf47797f9a5b8abe3ff5524ae8f7f24c1a1631027c8186cfdd94c33be76c7f`

> 组委会可自行抓取本 Release 附件并重算 SHA-256，与最终提交比对。
>
> **双载体声明**：本版本权重在**两个独立平台**同时公开 —— Hugging Face 主载体
> （`https://huggingface.co/jxzhen/aec-2027-editx-lora`）与本 GitHub Release。
> 两处附件**逐字节一致**，SHA-256 见上表与 `SHA256SUMS.txt`。
> 任一平台的记录均可单独作为"截止日前已公开可得"的证据。
>
> **建议以 Hugging Face 侧为主取用**：该侧保留 `files/` 目录结构，第三方可直接
> `sha256sum -c SHA256SUMS.txt` 通过；本 Release 的附件是平铺下载的，需先按下方
> 校验方法建好 `files/` 子目录再校验。

## 校验方法（任何第三方可独立复现）

```bash
# SHA256SUMS.txt 内的相对路径以 weights/ 为基准（写作 files/<name>）。
# Release 附件是平铺下载的，故先建 files/ 子目录再放入三个权重文件：
mkdir -p files
mv adapter_model.safetensors adapter_config.json README.md files/
sha256sum -c SHA256SUMS.txt
```

## 不可逆约束（提示后续维护者）

1. **必须保存原始权重文件。** 重新保存或转换会改变 checksum（即使张量数值未变）。
2. **任何格式转换须事先向组委会说明。**
3. **不要删除或修改本 Release。** 它是公开时间的证据本体。
   若必须发布修正版本，请**新建 tag**，并保持本版本可访问。

## 附件清单（Assets）

| Release 附件名 | 仓库内路径 | 大小 | SHA-256（前 16 位） |
|---|---|---|---|
| `adapter_model.safetensors` | `weights/files/adapter_model.safetensors` | 108,062,920 | `e0f145514f2d7ea8` |
| `adapter_config.json` | `weights/files/adapter_config.json` | 1,183 | `ec0b340cc8fd1687` |
| `README.md` | `weights/files/README.md` | 2,187 | `b9fc268ed54a90ed` |
| `MANIFEST.json` | `weights/MANIFEST.json` | 1,876 | `056b60e003026259` |
| `SHA256SUMS.txt` | `weights/SHA256SUMS.txt` | 272 | `5ccf47797f9a5b8a` |

> **附件名说明**：GitHub Release 的附件名**不带目录前缀**（上传时取 basename 平铺），
> 故左侧一列即下载后看到的文件名。
>
> **注意**：`MANIFEST.json` 的 sha256 会在**回填 `commit_id` 并置 `state=FINAL` 之后变化**
> （清单内容是哈希的输入）。上表是**2026-09-28 改定 `repo_url` 之后的快照**；
> 回填完成后须重算并同步本文件。
> `SHA256SUMS.txt` 只列上面三个权重文件，**不受清单改动影响**。
>
> **`repo_url` 已于 2026-09-28 定稿**：`https://huggingface.co/jxzhen/aec-2027-editx-lora`
> （此前清单里是未实测的占位值 `huggingface.co/JianxiZheng/aec-editx-lora-sandbox`，
> 账号、仓库名、后缀三处全错，已更正）。

## 许可

`Apache-2.0`

## 联系方式

Jianxi Zheng ｜ `hunan08182026@126.com`
