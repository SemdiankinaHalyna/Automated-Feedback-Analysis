# Automated Feedback Analysis for Decision Support
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

### Prediction Examples

![Random prediction examples](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/random%20prediction%20examples.png)


### 📊 Analytical Excel Dashboard
![Analytical Excel Dashboard](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Dashboard.png)

## Key Dashboard Insights

Insights are presented from an organizational perspective, focusing on relative shares, issue distribution, and temporal trends to support decision-making

### Sentiment Distribution
- 🟢 **Positive:** 55.5%
- 🔴 **Negative:** 36.4%
- ⚪ **Neutral:** 8.1%

### Main Issue Areas
- Quality of education (largest share)
- Academic process management
- Attitude towards students

### Issue Distribution (Top vs Bottom)
- 📈 Quality of education: **28%** (highest)
- 📉 Campus conditions: **11%** (lowest)

### Temporal Trend (2009–2023)
- Steady increase in issue-related feedback over time

### Post-2023 Shift
- 📉 Decrease in corruption-related mentions
- 📈 Increase in academic process management concerns

## 💡 Limitations

Results should be interpreted with caution, as online reviews may not fully represent the entire student population.
The approach is most valuable when applied to large-scale feedback collected from trusted and consistent sources, such as official university feedback platforms or customer review systems maintained by organizations. In such settings, automated sentiment and topic analysis enables continuous monitoring of user feedback and early detection of emerging issues.

## 🚀 Future Improvements

- 📊 Integrate additional feedback sources to improve data coverage and representativeness.  
- 🧠 Expand labeled dataset to improve model performance and enable more advanced architectures such as XLM-RoBERTa.  
- ⚙️ Transition to real-time pipeline with automated data collection, inference, and dashboard updates.  
- 🚨 Implement automated monitoring and alerting for emerging issues and sentiment shifts.  
---

## 🛠 Technologies 

**Data Collection & Processing:**  
`Selenium`, `BeautifulSoup`, `Pandas`, `NumPy`, `langdetect`, `re`

**Machine Learning & NLP:**  
`PyTorch`, `Scikit-learn (Logistic Regression, TF-IDF Vectorizer)`,  
`Sentence Transformers (SBERT — sentence-transformers/paraphrase-multilingual-mpnet-base-v2)`,  
`Transformers / Hugging Face (BertTokenizer, BertForSequenceClassification, nlptown/bert-base-multilingual-uncased-sentiment)`,  
`SciPy`, `OS`, `Joblib`

**Visualization & Clustering:**  
`Excel`, `Matplotlib`, `Seaborn`, `Plotly`, `UMAP`,  
`K-means`, `HDBSCAN`, `BERTopic`


