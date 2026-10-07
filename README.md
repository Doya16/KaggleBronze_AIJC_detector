<!-- README language switch -->
[![中文](https://img.shields.io/badge/%E4%B8%AD%E6%96%87-1677ff?style=for-the-badge)](README.md) [![English](https://img.shields.io/badge/English-555555?style=for-the-badge)](README.en.md)
<!-- /README language switch -->

# 🥉 KaggleBronze_AIJC_detector

This project documents my journey in a unique Kaggle competition, where I earned my **first Kaggle medal** – a 🥉 **bronze medal**, after participating in many contests!  
本项目记录了我在一场独特的 Kaggle 比赛中的经历，这是我参与多场比赛后，获得的第一块 🥉 **铜牌**！

---

## 📘 Competition Overview / 比赛概览

The dataset provided was highly **imbalanced**:  
官方提供的数据集非常 **不平衡**：

- 🧠 **AI-generated texts**: Only 3 available  
  仅包含 3 篇由 AI 生成的文本  
- 👥 **Human-written texts**: A lot  
  而人类撰写的文本非常多

So I used **popular LLMs** to generate **pseudo data** to balance the dataset.  
因此我使用了多个主流大语言模型（LLM）来生成伪数据，补足 AI 样本数量。

---

## ⚠️ Competition Challenges / 竞赛难点

### 1. 🪤 Artificial Spelling Errors / 人为拼写错误

Organizers **manually altered** AI texts and added **spelling mistakes**.  
主办方 **人为修改** 了 AI 文本并添加了拼写错误。

- CV score was **0.99**, but public leaderboard only **0.8**  
  本地交叉验证可达 0.99，排行榜却仅有 0.8

---

### 2. 🕵️‍♂️ Prompt Trap / Prompt 陷阱

- Train set had **2 prompts**, public test had **5 unknown**  
  训练集仅包含 2 个提示词，而测试集包含 **5 个未知 prompt**
- Required guessing & mining via uploads  
  需要选手通过上传测试结果来反推出这些 prompt

---

### 3. 🧠 Overfitting Transformers / Transformer 过拟合

- BERT, deBERTa performed poorly  
  主流模型如 BERT、deBERTa 效果很差
- Likely failed due to misspellings  
  原因是无法适应拼写错误扰动

---

## 🔧 My Solution Pipeline / 我的解决方案

- Limited to **one notebook** (train + inference)  
  比赛仅允许一个 notebook 包含训练和推理

- Used `leven_search` to build **sentence_correcter()**  
  利用 `leven_search` 库构建函数纠正拼写错误  
  移除了大量噪声和干扰

---

## 🧪 Data Collection / 数据收集与清洗

- Sourced data from Kaggle discussion  
  训练数据来自讨论区分享  
- ✅ Deduplicated & normalized  
  进行去重与标准化处理

### 🧼 Normalization specifics / 标准化细节：

- Removed samples with **known harmful prompts**  
  删除了带有有害 prompt 的样本
- Applied **Unicode NFC**, case sensitivity, BPE tokenizer  
  使用 NFC 统一字符编码、自建 BPE 分词器等

---

## 🧠 Tokenization Strategy / 分词策略

Built a custom tokenizer using **Byte-Pair Encoding (BPE)**  
我自建了一个 BPE 分词器，专门应对拼写错乱问题。

- Avoided using default tokenizers  
  避免使用通用 tokenizer 混淆错别字

---

## 🔢 TF-IDF Vectorization / 向量化

- Assigned each token a TF-IDF score  
  每个 token 通过 TF-IDF 映射成向量  
- Used `min_df = 0` to keep rare typo words  
  设置 `min_df = 0`，保留拼写错误等稀有词

---

## 🤖 Models Used / 模型使用

Trained and ensembled:  
我训练并融合了以下模型：

- 📊 Naive Bayes
- ⚙️ SGD Classifier
- 🔥 LightGBM Classifier

Used **weighted voting** for final prediction.  
最终结果使用加权投票融合输出。

---

## 🏆 Result / 比赛结果

Out of **2,175 teams**, I ranked in the **top 9%**  
在 **2,175 支队伍** 中，我成功进入了前 9% 🥳

并获得了人生第一枚 Kaggle 铜牌 🥉

---

## 🙏 Final Thoughts / 最后感想

Through this challenge, I practiced:  
通过本次比赛，我深入了解并实践了：

- LLM data augmentation 🤖 大模型生成伪数据
- Adversarial robustness 🧨 抗干扰建模能力
- Model generalization 📉 模型泛化与排行榜差距

Thanks for reading! 欢迎交流！
