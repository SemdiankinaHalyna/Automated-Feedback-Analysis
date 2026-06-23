# University Reviews Analysis and Issue Detection

![Python](https://img.shields.io/badge/Python-3.10-blue)
![ML](https://img.shields.io/badge/Machine%20Learning-NLP-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)
![Model](https://img.shields.io/badge/Model-Multi--Label%20Classification-purple)

## 📘 Project Overview

This project analyzes student reviews of universities using **Natural Language Processing (NLP)** and machine learning.

It combines:
- Sentiment analysis
- Multi-label issue detection
- Topic discovery via clustering
- Model evaluation and error analysis

The goal is to understand **what problems students report most frequently and how they vary across universities**.

Detected issue categories:

- Attitude Towards Students
- Campus Conditions
- Corruption
- Academic Process Management
- Education Quality

---

💡  **Note:**  
**This project is intended solely for educational and research purposes** and does not represent any official evaluation or ranking of the institutions.  
**For privacy reasons, the universities are anonymized** and referred to by numbers (e.g., University_1, University_2).

## 📋 Data Description:

- Number of universities: 21
- Data volume: over 6,000 open reviews
- Sources: collected from 3 public platforms
- Data structure:
- University Name
- Reviews Count
- Average Rating
- Review Date
- Review Rating
- Review Text

## 🔁 Project Workflow

### 1. Data Collection 🌐

University reviews were collected from public online sources using Selenium and BeautifulSoup.

### 2. Data Preparation 🧹

The reviews were cleaned, filtered, and prepared for analysis.

### 3. Topic Identification 🔍

Clustering and topic modeling techniques (K-Means, DBSCAN, UMAP, and BERTopic) were used to explore recurring themes in student reviews.

The discovered patterns helped define the final issue categories, which were then manually annotated and used to train the multi-label classification model.

### 4. Text Embeddings 🤖

Each review was converted into a numerical representation using multilingual sentence embeddings:

`paraphrase-multilingual-mpnet-base-v2`

### 5. Multi-label Classification 🧠

A One-vs-Rest Logistic Regression model predicts which issues are mentioned in a review.

### 6. Threshold Optimization 🎯

Class-specific thresholds were optimized using Out-of-Fold (OOF) validation predictions to improve issue detection performance.

### 7. Review Analysis 📊

Applied the trained model to unlabeled reviews to extract insights on sentiment distribution, issue frequency, and university-level patterns.

Built an interactive Excel dashboard (Pivot Tables, Pivot Charts, slicers) to visualize sentiment trends, issue categories, and temporal dynamics across universities.

---

## 🧾 Model Pipeline

```text
Review Text
    ↓
Sentence Embeddings
    ↓
One-vs-Rest Logistic Regression
    ↓
Class Probabilities
    ↓
Threshold Optimization
    ↓
Predicted Issue Categories
    ↓
Analytical Excel Dashboard	
```

---

## 📈 Results

### Validation Performance

| Metric | Score |
|----------|----------|
| Micro-F1 | 79 |
| Macro-F1 | 79 |

### 🔍 Error Analysis

The model was evaluated using:

- Per-class confusion matrices
- Pairwise class confusion analysis
- Manual review of prediction examples

---

## 📊 Visualizations

### 📉 Class Imbalance

Shows distribution of sentiment and issue categories.

![Class Imbalance](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/%D1%81lass_imbalance.png)

### 🎯 Precision-Recall Curve

Evaluates model performance across different thresholds.

![Precision-Recall Curve](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/precision_recall_curve.png)

### 🧩 Confusion Matrix

Shows which classes the model confuses most.

![Confusion Matrix](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/confusion_matrix.png)

---

## Random prediction examples

![Random prediction examples](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/random%20prediction%20examples.png)

---

## 📊 Analytical Excel Dashboard

### Sentiment Distribution 
Distribution of review sentiments across the dataset (positive, neutral, negative).

![Sentiment Distribution](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/sentimet_distribution.png)

### Issue Frequency 📈
Most common issue categories identified in student reviews.

![Issue Frequency](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/imagesissue_frequency.png)

### University-Level Analysis 🏫
Differences in review patterns across universities.

![University Analysis](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/university_analysis.png)

---

## 🛠 Technologies 

**Data Collection & Processing:**  
`Selenium`, `BeautifulSoup`, `Pandas`, `NumPy`, `langdetect`, `re`, `stanza`, `pymorphy2`,  
`collections.Counter`, `PyTorch`, `transformers (MarianMTModel, MarianTokenizer)`

**Machine Learning & NLP:**  
`PyTorch`, `Scikit-learn (Logistic Regression, TF-IDF Vectorizer)`,  
`Sentence Transformers (SBERT — sentence-transformers/paraphrase-multilingual-mpnet-base-v2)`,  
`Transformers / Hugging Face (BertTokenizer, BertForSequenceClassification, nlptown/bert-base-multilingual-uncased-sentiment)`,  
`SciPy`, `OS`, `Joblib`

**Visualization & Clustering:**  
`Matplotlib`, `Seaborn`, `Plotly`, `UMAP`, `WordCloud`,  
`K-means`, `HDBSCAN`, `BERTopic`


