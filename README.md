# SemEval Polarization Task – Turkish (Subtask-1 & Subtask-2)

## Project Overview

This repository contains our solutions for **Subtask-1** and **Subtask-2** of the **SemEval Polarization Task**, focusing exclusively on **Turkish (monolingual)** social media texts.

The main objectives of this project are:
1. To detect whether a given text is **polarized** or **non-polarized** (Subtask-1).
2. For polarized texts, to identify the **type(s) of polarization** expressed (Subtask-2).

All experiments were conducted in **Google Colab Pro**, with a strong emphasis on reproducibility, robust evaluation strategies, and threshold-aware optimization.

---

## Task Definitions

### Subtask-1: Polarization Detection (Binary Classification)

**Objective:**  
Classify a Turkish text as *polarized* (`1`) or *non-polarized* (`0`).

**Task characteristics:**
- Binary classification
- Highly context-dependent
- Presence of class imbalance
- Model performance is sensitive to decision threshold selection

---

### Subtask-2: Polarization Type Classification (Multi-label Classification)

**Objective:**  
For texts identified as polarized, determine which **polarization category or categories** apply.  
Each text may belong to **multiple categories simultaneously**.

**Target labels:**
- `political`
- `racial/ethnic`
- `religious`
- `gender/sexual`
- `other`

**Task characteristics:**
- Multi-label classification
- Strong label imbalance
- Requires label-wise decision threshold tuning

---

## Modeling Approaches

Two main modeling strategies were explored for both subtasks.

### Baseline Models (Non-Transformer)

- **Subtask-1**
  - TF-IDF representations (word and character n-grams)
  - Logistic Regression
  - Fixed decision threshold (0.5)

- **Subtask-2**
  - TF-IDF representations
  - One-vs-Rest Logistic Regression
  - Multi-label classification setup

These baseline models provide strong classical reference points but are limited in capturing semantic context and long-range dependencies in complex social media texts.

---

### Transformer-based Models (BERT)

For both subtasks, a transformer-based approach was employed with the following configuration:

- **Model:** `dbmdz/bert-base-turkish-cased`
- **Framework:** HuggingFace Transformers (custom training loop without using Trainer)
- **Maximum sequence length:** 256 tokens
- **Optimizer:** AdamW with linear warm-up scheduling

Additional enhancements include:
- Task-specific loss functions
- Best-epoch selection based on validation performance
- Threshold tuning to optimize Macro-F1
- Fine-grained label-wise threshold optimization for the multi-label task

---

## Experimental Results

### Subtask-1 Results (Polarization Detection)

| Model | Threshold Strategy | Dev Micro-F1 | Dev Macro-F1 |
|------|------------------|-------------:|-------------:|
| TF-IDF + Logistic Regression | Fixed (0.5) | 0.5785 | 0.3239 |
| **BERT (Turkish)** | **Tuned (~0.27)** | Improved | **0.803** |

The BERT-based model significantly outperforms the baseline, particularly in terms of **Macro-F1**, indicating more balanced performance across classes.  
Threshold tuning proved to be critical, as the optimal decision boundary differed substantially from the default value.

---

### Subtask-2 Results (Polarization Type Classification)

| Model | Configuration | Dev Micro-F1 | Dev Macro-F1 |
|------|--------------|-------------:|-------------:|
| TF-IDF + LR | Fixed threshold (0.5) | 0.5785 | 0.3239 |
| **BERT (TR)** | **len=256, epoch=4, grid=0.01–0.99** | **0.7117** | **0.6058** |

Increasing the input sequence length and applying fine-grained, label-specific threshold tuning led to substantial improvements, especially for underrepresented labels.

---

## Key Findings

- Transformer-based models consistently outperform classical TF-IDF baselines on both subtasks.
- Threshold optimization is crucial for both binary and multi-label polarization tasks.
- Longer input sequences improve the model’s ability to capture implicit and contextual polarization cues.
- Treating Subtask-1 and Subtask-2 as separate tasks results in more robust and interpretable solutions.

---

## Repository Structure

