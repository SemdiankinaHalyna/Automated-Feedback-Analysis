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

### 📊 Analytical Excel Dashboard
![Analytical Excel Dashboard](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Dashboard.png)

### Prediction Examples

![Random prediction examples](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/random%20prediction%20examples.png)

## Key Insights

## Limitations

Results should be interpreted with caution, as online reviews may not represent the full student population. 
The approach is most valuable when applied to large-scale feedback collected from trusted and consistent sources, such as official university feedback platforms or customer review systems maintained by organizations. In such cases, automated sentiment and topic analysis can support continuous monitoring of user feedback and help identify emerging issues at an early stage.

## Future Improvements

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


