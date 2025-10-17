# Thesis

# Polarization Detection Baseline (Turkish Social Media)

This repository implements a baseline pipeline for polarization detection in Turkish social media texts.  
All analyses and models are developed **exclusively in Python** (Jupyter/Colab notebooks and standard ML/DL libraries).  
**No Kotlin, Java, or non-Python technologies are used at any stage.**

---

## Baseline Pipeline Summary

- **Data Filtering:** Only Turkish (`lang == "tur"`) entries are selected from the dataset.
- **Exploratory Analysis:** Label distribution, text length, and most frequent terms are examined.
- **Classical Baseline:**  
  - TF-IDF (unigram & bigram) features are extracted.  
  - Logistic Regression classifier with balanced class weights is used.
  - Model is evaluated via hold-out and cross-validation.
- **Transformer-based Model:**  
  - The BERTurk (`dbmdz/bert-base-turkish-cased`) pre-trained language model is fine-tuned for binary classification.
  - Training settings are optimized for small data (early stopping, batch size, learning rate scheduling, threshold tuning).
- **Threshold Tuning:** The decision threshold is optimized on the validation set for best macro-F1 score.
- **Inference:** A prediction function is provided using the optimal threshold.

All results, code, and model artifacts are Python-based and can be fully reproduced and extended within the Python ecosystem.

---

## Minimal Roadmap / Pipeline

1. **Filter Turkish data and perform EDA**
2. **Train and evaluate TF-IDF + Logistic Regression baseline**
3. **Fine-tune BERTurk model for binary classification**
4. **Tune threshold on validation set**
5. **Compare and report results**

---

## Directory Structure

