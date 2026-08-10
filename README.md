[README_1.md](https://github.com/user-attachments/files/30895248/README_1.md)
# Qwen3-VL-8B Bangla Fine-Tune 🇧🇩

**Colab Code Link:** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/17eKGU7oXZz9lmAgHm2AgkqqJESDCQE3g?usp=sharing)

Fine-tuning **Qwen3-VL-8B-Instruct** (a vision-language model) on Bangla data using **Unsloth** and **QLoRA (4-bit)** — a full, working, beginner-friendly pipeline from raw data to a deployed model, built as part of the **LLM Lab - Billah** video series.

This repo contains the exact notebook used in the video, including every real bug encountered and fixed live — dependency conflicts, wrong dataset schemas, multi-GPU crashes, and more — so viewers can follow along and reproduce it themselves.

---

## 🎥 What This Project Does

Starting from a base vision-language model, this pipeline:
1. Loads and prepares Bangla training data (visual question-answering + text instructions)
2. Fine-tunes the model using parameter-efficient LoRA adapters (only ~0.5% of parameters trained)
3. Tracks training loss in real time
4. Evaluates the fine-tuned model on held-out examples
5. Lets you test the model on your own image
6. Pushes the final model to the Hugging Face Hub
7. Spins up a simple Gradio web demo

It's designed as a **compact, end-to-end demo** — not a production-scale training run — so it trains in minutes on a free-tier GPU (Kaggle T4 / Colab T4).

---

## 🧠 Model & Method

| | |
|---|---|
| **Base model** | [`unsloth/Qwen3-VL-8B-Instruct`](https://huggingface.co/unsloth/Qwen3-VL-8B-Instruct) (4-bit quantized) |
| **Fine-tuning method** | QLoRA (r=16, alpha=16) via [Unsloth](https://github.com/unslothai/unsloth) |
| **Trainable parameters** | ~43.6M out of 8.8B (0.5%) |
| **Frameworks** | `transformers`, `trl`, `peft`, `unsloth` |
| **Hardware** | Single T4 GPU (Kaggle or Google Colab, free tier) |

## 📊 Datasets

| Portion | Source | Content |
|---|---|---|
| **VQA** | [`Remian9080/Bangla-Bayanno-Full`](https://huggingface.co/datasets/Remian9080/Bangla-Bayanno-Full) | Bangla image question-answer pairs |
| **Text-Instruction** | [`ai4bharat/indic-align`](https://huggingface.co/datasets/ai4bharat/indic-align) (Dolly_T config, Bengali) | Bangla instruction/response pairs |

A small sample (20 examples per portion) is used to keep this a fast, reproducible demo. Captioning and OCR portions were investigated but dropped — no confirmed Bangla dataset with clean image+text columns could be verified at the time of recording.

## 🚀 Results

- Training loss decreased across all steps (~9.6% improvement on the VQA portion)
- The fine-tuned model produces fluent, grammatically correct Bangla output
- Object-recognition accuracy is limited, as expected from a ~20-sample demo — this is a **pipeline demonstration**, not a production-accuracy benchmark

## 📓 Notebooks

Two versions are provided — pick whichever platform you prefer:

| Platform | Access | Paths | HF Token |
|---|---|---|---|
| **Kaggle** | `.ipynb` file in this repo (see below) | `/kaggle/working/` | Kaggle Secrets |
| **Google Colab** | [Open in Colab](https://colab.research.google.com/drive/17eKGU7oXZz9lmAgHm2AgkqqJESDCQE3g?usp=sharing) | `/content/` | Colab Secrets (🔑 icon) |

- **Kaggle notebook file:** [`Qwen3-VL-Bangla-Finetune.ipynb`](./Qwen3-VL-Bangla-Finetune.ipynb) *(upload the file to this repo and update this link with its actual filename)*
- **Colab notebook:** click the link above — no download needed, runs directly in your browser

**Steps to run either version:**
1. Open the notebook (Kaggle: upload the file and open it; Colab: click the link above)
2. Enable a GPU runtime (T4)
3. Run cells top to bottom
4. Add your Hugging Face token as a secret named `HF_TOKEN` before the deploy cell
5. Set `HF_REPO` to your own Hugging Face username/repo name

## 🔗 Links

- **Fine-tuned model (LoRA adapter):** [billahaiml/qwen3-vl-8b-bangla-lora](https://huggingface.co/billahaiml/qwen3-vl-8b-bangla-lora)
- **Base model:** [unsloth/Qwen3-VL-8B-Instruct](https://huggingface.co/unsloth/Qwen3-VL-8B-Instruct)
- **Built with:** [Unsloth](https://github.com/unslothai/unsloth)

## ⚠️ Disclaimer

This is an educational demo trained on a small sample for speed and reproducibility. It is **not** intended to represent production-grade Bangla VQA accuracy. For real-world use, scale up the sample size per portion significantly (1,000+ examples recommended) and consider adding captioning/OCR data once verified sources are available.

---

*Part of the LLM Lab - Billah YouTube series.*
