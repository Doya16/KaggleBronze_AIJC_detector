<!-- README language switch -->
[![中文](https://img.shields.io/badge/%E4%B8%AD%E6%96%87-555555?style=for-the-badge)](README.md) [![English](https://img.shields.io/badge/English-1677ff?style=for-the-badge)](README.en.md)
<!-- /README language switch -->

# 🥉 KaggleBronze_AIJC_detector

This project documents my journey in a unique Kaggle competition, where I earned my **first Kaggle medal** — a 🥉 **bronze medal** — after participating in many contests!

---

## 📘 Competition overview

The provided dataset was highly **imbalanced**:

- 🧠 **AI-generated texts**: only 3 samples available.
- 👥 **Human-written texts**: many samples available.

I used several **popular large language models (LLMs)** to generate **synthetic data** and balance the dataset.

---

## ⚠️ Competition challenges

### 1. 🪤 Artificial spelling errors

The organizers **manually altered** AI-generated texts and added **spelling mistakes**.

- My cross-validation score reached **0.99**, while the public leaderboard score was only **0.8**.

---

### 2. 🕵️‍♂️ Prompt trap

- The training set had **2 prompts**, while the public test set had **5 unknown prompts**.
- This required inferring the prompts through submissions and their results.

---

### 3. 🧠 Transformer overfitting

- BERT and deBERTa performed poorly.
- They likely struggled with the spelling perturbations.

---

## 🔧 My solution pipeline

- The competition allowed only **one notebook** for both training and inference.
- I used `leven_search` to build **`sentence_correcter()`**, correcting spelling errors and removing substantial noise.

---

## 🧪 Data collection and cleaning

- Sourced training data from Kaggle discussions.
- ✅ Deduplicated and normalized the data.

### 🧼 Normalization details

- Removed samples with **known harmful prompts**.
- Applied **Unicode NFC** normalization, retained case sensitivity, and used a custom BPE tokenizer.

---

## 🧠 Tokenization strategy

I built a custom **Byte-Pair Encoding (BPE)** tokenizer to handle misspellings.

- Avoided default tokenizers that could mishandle spelling errors.

---

## 🔢 TF-IDF vectorization

- Assigned TF-IDF weights to tokens to form feature vectors.
- Used `min_df = 0` to retain rare words, including misspellings.

---

## 🤖 Models used

I trained and combined:

- 📊 Naive Bayes
- ⚙️ SGD Classifier
- 🔥 LightGBM Classifier

Final predictions used **weighted voting**.

---

## 🏆 Result

Out of **2,175 teams**, I finished in the **top 9%** 🥳 and earned my first Kaggle bronze medal 🥉.

---

## 🙏 Final thoughts

Through this challenge, I practiced:

- LLM data augmentation 🤖
- Building robustness to perturbations 🧨
- Model generalization and understanding the gap between validation and leaderboard scores 📉

Thanks for reading! Feedback and discussion are welcome!
