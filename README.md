# Automated Issue Detection in Feedback Systems
### Case Study: Higher Education

![Python](https://img.shields.io/badge/Python-3.10-blue)
![ML](https://img.shields.io/badge/Machine%20Learning-NLP-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)
![Model](https://img.shields.io/badge/Model-Multi--Label%20Classification-purple)

## 📘 Project Overview

This project focuses on analyzing large-scale user feedback to extract actionable insights from unstructured text data. It addresses the challenge of transforming raw reviews into structured information that can support decision-making through sentiment analysis and issue detection.

Although demonstrated using higher education reviews, the proposed approach can be applied to feedback systems in various industries, including finance, e-commerce and customer support.

💡  **Note:**  
**This project demonstrates a feedback analytics methodology** using higher education reviews as an example. It is not intended to provide an official evaluation or ranking of educational institutions.  
**For privacy reasons, the universities are anonymized** and referred to by numbers (e.g., University_1, University_2).

---

## Business Problem

Organizations receive large volumes of user feedback through reviews and surveys. Manual analysis is time-consuming, subjective, difficult to scale and often delays the identification of recurring or emerging issues.

## Solution

Developed an end-to-end feedback analytics pipeline that automatically collects reviews, analyzes sentiment, identifies key issues using NLP and machine learning, and provides actionable insights through interactive dashboards. 

## Expected Business Value

- Reduces manual effort required to analyze large volumes of feedback.
- Enables early detection of emerging issues.
- Supports data-driven decision making.
- Helps prioritize improvement initiatives based on the frequency and trends of reported issues.


## Methodology

The project follows a structured end-to-end pipeline for processing and analyzing user feedback, combining NLP and machine learning techniques.
![Pipeline](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/pipeline.png)

## Skills
- Data Collection 
- Data Preparation 
- Natural Language Processing 
- Machine Learning 
- Data Visualization 
- Business Reporting

## Key Results

- Collected and processed 6,000+ student reviews from multiple public sources. 
- Issue categories identified (Attitude Towards Students, Campus Conditions, Corruption, Academic Process Management, Education Quality)
- Developed a multi-label classification model for automatic issue detection (F1 micro = 0.79) and demonstrated reliable performance across major issue categories.
- Built an interactive dashboard for monitoring sentiment, comparing universities and tracking issue trends.




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


![Analytical Excel Dashboard](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Dashboard.png)


---

## 🛠 Technologies 

**Data Collection & Processing:**  
`Selenium`, `BeautifulSoup`, `Pandas`, `NumPy`, `langdetect`, `re`, `stanza`, `pymorphy2`,  
`collections.Counter`, `PyTorch`)`

**Machine Learning & NLP:**  
`PyTorch`, `Scikit-learn (Logistic Regression, TF-IDF Vectorizer)`,  
`Sentence Transformers (SBERT — sentence-transformers/paraphrase-multilingual-mpnet-base-v2)`,  
`Transformers / Hugging Face (BertTokenizer, BertForSequenceClassification, nlptown/bert-base-multilingual-uncased-sentiment)`,  
`SciPy`, `OS`, `Joblib`

**Visualization & Clustering:**  
`Matplotlib`, `Seaborn`, `Plotly`, `UMAP`, `WordCloud`,  
`K-means`, `HDBSCAN`, `BERTopic`


