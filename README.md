# University Reviews Analysis and Issue Detection

## 📘 Project Overview

This project analyzes student reviews of Ukrainian universities using Natural Language Processing (NLP).

The system performs two tasks:

- **Sentiment Classification** (Positive, Neutral, Negative)
- **Multi-label Issue Classification** for negative reviews

Detected issue categories:

- Attitude Towards Students
- Campus Conditions
- Corruption
- Academic Process Management
- Education Quality

---

**Note:**  
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

University reviews were collected from public online sources.

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

### Sentiment Distribution

![Sentiment Distribution](images/sentiment_distribution.png)

### Issue Frequency

![Issue Frequency](images/issue_frequency.png)

### University-Level Analysis

![University Analysis](images/university_analysis.png)

---

## Example Predictions

### Education Quality

![Education Quality Example](images/example_education_quality.png)

### Corruption

![Corruption Example](images/example_corruption.png)

### Academic Process Management

![Academic Process Example](images/example_academic_process.png)

---

## Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Sentence Transformers
- Matplotlib
- Seaborn
- Plotly

---

## Future Improvements

- Increase the size of the labeled dataset
- Experiment with transformer-based classifiers
- Improve classification of overlapping issue categories
- Develop an interactive dashboard for university comparison
   


## 1. 🌐 Data Collection
   
This project includes a demonstration of basic web scraping techniques used to collect student reviews of universities from publicly available websites.
To preserve privacy and comply with ethical standards:
-	The URLs of the data sources are intentionally omitted.
-	The scraping code is presented for educational purposes only, as part of a natural language processing (NLP) pipeline [Scraping Code](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/university_reviews_scraper.ipynb)

  To collect textual reviews from students about universities, an automated parser was implemented using Selenium and BeautifulSoup.

Key steps:
- Opened the university page and hid advertisement blocks.
- Dynamically clicked on “Show all reviews” and “Read full review” buttons.
- Extracted university name, date, full text, and star rating.
- Processed HTML to extract structured data.
- Saved results to .txt files for further processing.

## 2. ⚙ Preprocessing️

### 1️⃣ Initial Data Preparation 🌐
- Collected reviews from all sources were **merged into a single DataFrame**.  
- **Removed records** with missing review text.  
- Since data came from different platforms, inconsistencies were found in:  
  - University names  
  - Date formats  
  - Number of reviews  
  - Average ratings  
- **Standardized university names** (consistent abbreviations, removed extra spaces/symbols).  
- **Excluded universities with fewer than 100 reviews** to ensure statistical significance.  
- **Updated “Number of Reviews”** column considering data from all sources.  
- **Calculated average ratings** as the arithmetic mean of star ratings per university.  
- **Added a Timestamp column** for consistent date handling in later analysis.

---

### 2️⃣ Data Preprocessing 🗂️
- **Harmonized** column names, data types, and value formats.  
- **Converted** all data to strings for consistency.  
- **Safely replaced** `NaN`, lists, numbers, or unusual formats:  
  - Numbers stored as **Num** (e.g., `123 → "Num"`)  
  - Time values stored as **Time** (e.g., `12:30 → "Time"`)  
- **Removed** completely empty records.  
- Prepared a **clean, structured DataFrame** for NLP processing.

---

### 3️⃣ NLP Text Cleaning 🧹
- Converted all text to **lowercase**.  
- **Removed** unwanted punctuation and normalized spaces.  
- **Filtered** non-letter tokens (kept only alphabetic words).  
- **Lemmatized** words to their base form.  
- **Removed stopwords** (common non-informative words).  
- **Filtered by language:** kept only **Ukrainian** and **Russian** reviews.  
- **Removed extremely long reviews** (outliers by word count).  
- **Removed very short reviews** (less than 3 words after cleaning).  
- Saved **cleaned, ready-to-use text files** for further modeling 

---

![Word Cloud](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/WordCloud.png)

---

### 4️⃣ Data Augmentation 🔁

To address **class imbalance** among categories, data augmentation was applied:

- Categories with the most **mixed or underrepresented labels** were expanded.  
  Only reviews with a **single label** were selected for augmentation to preserve semantic clarity.  
- Augmentation was performed via **machine translation**, using the `langdetect` library for language identification:  
  - If a review was written in **Ukrainian**, it was translated into **Russian**.  
  - If a review was written in **Russian**, it was translated into **Ukrainian**.  
- This approach helped **increase the training dataset size** and achieve a **better linguistic balance**, improving model robustness across both languages.  
- The **original (non-augmented) dataset** was preserved and used for **hyperparameter tuning with cross-validation**,  
  in order to **avoid data leakage** and ensure fair model evaluation [Preprocessing Code](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/NLP_files/Text_preprocessing_clean.ipynb)



## 3. 📊 Exploratory Data Analysis (EDA)

![Distribution of review counts over time](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Years.png)

The chart shows how the number of reviews changed over time. **User activity** peaked **between 2017 and 2021**, likely reflecting a growing interest in education quality discussions

 **Built distribution and density plots to analyze users’ tendency toward positive or negative reviews.**
 
 ![CDF](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/PDF.png)


![CDF](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/CDF.png)

- **56%** of reviews have **high** ratings
- **7%** of reviews have **neutral** ratings
- **37%** of reviews have **low** ratings

![Avarage_Rating](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Avarage_Rating.png)

## 4. 🤖 Sentiment Analysis with BERT
### Sentiment Analysis

Using **Hugging Face Transformers (BERT)**, the sentiment of each review was analyzed and stored in a separate column.  
The **BERT output** was converted into categorical labels:

- 🟥 **Negative**  
- 🟨 **Neutral**  
- 🟩 **Positive**

To evaluate model consistency, **BERT-predicted sentiment** was compared with the **original star ratings**.  
Agreement metrics were calculated, including **accuracy** and a **confusion matrix**.

**Overall agreement:** **73.31%** between star ratings and BERT-predicted sentiment.


![Confusion Matrix](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Confusion_Matrix.png)

### Confusion Matrix Results

- 🟩 **Positive reviews:**  
  BERT performs fairly well at predicting positive sentiment — **2,687 matches out of 3,533** (≈**76%**).

- 🟥 **Negative reviews:**  
  Also show good alignment — **1,866 matches out of 2,329** (≈**80%**).

- ⚠️ **Misclassified positives:**  
  The biggest confusion occurs with **positive ratings** that BERT classified as **negative** — **664 cases** (≈**19%** of all positive ratings).

- 🟨 **Neutral reviews:**  
  Have the **lowest accuracy** and the **fewest examples**, which is expected since this category is the most ambiguous.

### Handling Mismatched Reviews

An analysis of mismatched reviews showed that discrepancies arose due to either **BERT misclassification** or the nature of the review itself, such as:  
- Presence of **irony or sarcasm**  
- Subjective ambiguity (neutral or mixed opinions that are hard to classify clearly)

To ensure reliable sentiment scores, only reviews where **BERT sentiment matched the star rating** (**73.31% of all reviews**) were retained for determining the overall sentiment of a university.

A thorough filtering was performed:  
- For the final analysis, only reviews with matching star ratings and predicted sentiment were used  
- This approach reduces classification errors  
- The loss of approximately **27% of reviews** did not critically affect the results, as the excluded reviews were **evenly distributed across years and universities**

![Heat Map](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Heat_Map.png)
### Sentiment Scoring and Visualization

To quantify sentiment, **sentiment index values** were assigned:  
- 🟥 **Negative:** -1  
- 🟨 **Neutral:** 0  
- 🟩 **Positive:** 1  

This allowed sentiment to be treated as a **numeric score**, enabling further analysis.  
The **average sentiment score** was calculated for each university.

A **heatmap** was created to visualize sentiment dynamics over the years.  
- Most universities showed **predominantly positive sentiment** up until 2014–2015  
- After 2014–2015, sentiment **began to decline** in more than half of the universities

 
## 5. 📂 Training Classification Model

To build the **classification model**, **510 negative student reviews** about universities were **manually labeled**.

Each review could belong to **one or more problem categories** simultaneously, making this a **multi-label classification task**. In total, **700 labels** were assigned.

The problem categories are:

- **Attitude_Towards_Students**
- **Campus_conditions**
- **Corruption**
- **Academic_Process_Management**
- **Education_Quality**

---

## 🧠 ML Pipeline Overview

### 1. 📦 Load Necessary Libraries  
Import all required Python packages for data processing, model training, and evaluation.

### 2. 📂 Load Datasets 
Datasets were **pre-cleaned and pre-processed**:  
- `train_df` — labeled data for training  
- `val_df` — labeled data for validation (hyperparameter tuning)  
- `test_df` — labeled data for final evaluation  
- `unlabeled_df` — unlabeled data for inference

### 3. TF-IDF Pipeline

1. **Feature Extraction**  
   - Vectorized text using TF-IDF with n-grams.  
   - Applied feature selection to remove uninformative features.  

2. **Model Training**  
   - Trained a `One-vs-Rest Logistic Regression` classifier (`OneVsRestClassifier(LogisticRegression)`) on TF-IDF features.  
   - Performed hyperparameter tuning with cross-validation (`min_df`, `C`, `l1_ratio`).  

3. **Threshold Optimization**  
   - Optimized decision thresholds per class to maximize F1-score.  

4. **Evaluation Metrics**  
   - Precision, Recall, F1-score  
   - Micro, Macro, Weighted, and Samples averages  

5. **Example Metrics** (train/test)  

**Train Set**

| Class                         | Precision | Recall | F1-score | Support |
|-------------------------------|----------|--------|----------|--------|
| Attitude_Towards_Students     | 0.87     | 0.92   | 0.90     | 205    |
| Campus_conditions             | 0.85     | 0.96   | 0.90     | 108    |
| Corruption                     | 0.88     | 0.97   | 0.92     | 133    |
| Academic_Process_Management    | 0.86     | 0.94   | 0.90     | 190    |
| Education_Quality              | 0.83     | 0.95   | 0.88     | 184    |

**Aggregated F1-scores:**  
- Micro F1: 0.899  
- Macro F1: 0.901  

---

**Test Set**

| Class                         | Precision | Recall | F1-score | Support |
|-------------------------------|----------|--------|----------|--------|
| Attitude_Towards_Students     | 0.59     | 0.65   | 0.62     | 31     |
| Campus_conditions             | 0.80     | 0.69   | 0.74     | 29     |
| Corruption                     | 0.79     | 0.59   | 0.68     | 37     |
| Academic_Process_Management    | 0.65     | 0.56   | 0.60     | 39     |
| Education_Quality              | 0.80     | 0.65   | 0.72     | 57     |

**Aggregated F1-scores:**  
- Micro F1: 0.672  
- Macro F1: 0.671  


### 4. Sentence-Transformers Pipeline

1. **Embeddings**  
   - Fine-tuned `sentence-transformers/paraphrase-multilingual-mpnet-base-v2` on the labeled dataset.  
   - Extracted sentence embeddings for all texts.  

2. **Feature Engineering**  
   - Applied `VarianceThreshold` to remove low-variance features.  

3. **Model Training**  
   - Trained a `One-vs-Rest Logistic Regression` classifier (`OneVsRestClassifier(LogisticRegression)`) on sentence embeddings.  
   - Performed hyperparameter tuning using cross-validation (`C`, `l1_ratio`, feature thresholds).  

4. **Threshold Optimization**  
   - Optimized decision thresholds per class to maximize F1-score.  

5. **Evaluation Metrics**  
   - Precision, Recall, F1-score  
   - Micro, Macro, Weighted, and Samples averages  

6. **Example Metrics** (train/test)  

**Train Set**

| Class                         | Precision | Recall | F1-score | Support |
|-------------------------------|----------|--------|----------|--------|
| Attitude_Towards_Students     | 0.74     | 0.79   | 0.76     | 205    |
| Campus_conditions             | 0.68     | 0.85   | 0.76     | 108    |
| Corruption                     | 0.71     | 0.86   | 0.78     | 133    |
| Academic_Process_Management    | 0.73     | 0.81   | 0.76     | 190    |
| Education_Quality              | 0.68     | 0.84   | 0.75     | 184    |

**Aggregated F1-scores:**  
- Micro F1: 0.762  
- Macro F1: 0.762  

---

**Test Set**

| Class                         | Precision | Recall | F1-score | Support |
|-------------------------------|----------|--------|----------|--------|
| Attitude_Towards_Students     | 0.63     | 0.61   | 0.62     | 31     |
| Campus_conditions             | 0.71     | 0.76   | 0.73     | 29     |
| Corruption                     | 0.79     | 0.70   | 0.74     | 37     |
| Academic_Process_Management    | 0.63     | 0.82   | 0.71     | 39     |
| Education_Quality              | 0.79     | 0.77   | 0.78     | 57     |

**Aggregated F1-scores:**  
- Micro F1: 0.726  
- Macro F1: 0.718  

  
---

### 5. RoBERTa / Transformer Pipeline

1. **Model Setup**  
- Used `xlm-roberta-base` pre-trained Transformer for multi-label classification.  
- Added classification head with `num_labels` equal to the number of target classes.  
- Froze the first 6 Transformer layers to reduce overfitting.  

2. **Loss & Optimization**  
- Used `BCEWithLogitsLoss` with class weights to handle label imbalance.  
- Optimized with `AdamW` and applied gradient clipping for stable training.  

3. **Training**  
- Trained the model for multiple epochs on the training dataset.  
- Batch size = 8, learning rate = 1e-5.  

4. **Predictions & Evaluation**  
- Predicted labels using fixed threshold = 0.5.  
- Evaluated with Precision, Recall, F1-score (Micro, Macro, Weighted, Samples averages).  

5. **Example Metrics** (train/test)  

**Train Set**

| Class                         | Precision | Recall | F1-score | Support |
|-------------------------------|----------|--------|----------|--------|
| Attitude_Towards_Students     | 0.88     | 0.82   | 0.85     | 205    |
| Campus_conditions             | 0.89     | 0.95   | 0.92     | 108    |
| Corruption                     | 0.61     | 0.89   | 0.72     | 133    |
| Academic_Process_Management    | 0.84     | 0.82   | 0.83     | 190    |
| Education_Quality              | 0.73     | 0.84   | 0.78     | 184    |

**Aggregated F1-scores:**  
- Micro F1: 0.816  
- Macro F1: 0.822  

---

**Test Set**

| Class                         | Precision | Recall | F1-score | Support |
|-------------------------------|----------|--------|----------|--------|
| Attitude_Towards_Students     | 0.81     | 0.71   | 0.76     | 31     |
| Campus_conditions             | 0.73     | 0.93   | 0.82     | 29     |
| Corruption                     | 0.62     | 0.76   | 0.68     | 37     |
| Academic_Process_Management    | 0.61     | 0.64   | 0.62     | 39     |
| Education_Quality              | 0.82     | 0.72   | 0.77     | 57     |

**Aggregated F1-scores:**  
- Micro F1: 0.728  
- Macro F1: 0.730  


### 5. **Model selection**: Evaluate performance and choose the best model based on metrics [Training Code](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/NLP_files/training_model_.ipynb)



## 🧩 **Conclusion**

The goal of this study was to compare three approaches for multi-label text classification: **TF-IDF with Logistic Regression**, **Sentence-Transformers embeddings with Logistic Regression**, and **RoBERTa fine-tuning**.  

- **TF-IDF** provided a strong baseline, especially for general topics, but struggled with the class **Attitude_Towards_Students**, likely due to its reliance on surface-level n-gram features.  
- **Sentence-Transformers** improved the capture of semantic relationships and contextual meaning, leading to better overall performance, yet **Attitude_Towards_Students** remained a challenging class.  
- **RoBERTa fine-tuning** achieved the best performance across most classes, including **Attitude_Towards_Students**. This improvement is likely due to the model's pretraining on Facebook-related datasets, which contain similar types of text discussing opinions and attitudes. As a result, RoBERTa is better able to capture nuanced expressions of sentiment and stance in this category.  

Overall, **RoBERTa demonstrated the highest quality predictions**, particularly for classes that require understanding of subtle attitudes and opinions, making it the preferred model for this multi-label classification task.  

## 6. 📊 Inference and University Problem Analysis

Using the trained multi-label classification model to perform **inference on new reviews**  
and **analyze key problem categories** across different universities [Inference Code](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/NLP_files/model_inference_unlabeled.ipynb)

### 📊 Key Insights from Overall Negative Feedback

- **Education Quality:** The largest share of negative feedback is related to **Education Quality**, accounting for **28.6%** of all negative labels.  
- **Attitude Towards Students, Corruption, Academic Process Management:** These three categories have roughly similar shares, each contributing about **19–20%** of negative labels.  
- **Campus Conditions:** The smallest proportion of complaints is related to **Campus Conditions**, accounting for **12.5%**.
 ![Insights_1](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Insights_1.png))

## 📌 Analysis of Key Problems by Universities

- **Attitude Towards Students:** The worst rating was observed in **university_12**.  
- **Campus Conditions:** The poorest conditions were reported in **university_17**.  
- **Corruption:** The highest level of corruption was found in **university_14**.  
- **Academic Process Management:** The least effective management of the academic process was noted in **university_13**.  
- **Education Quality:** The lowest quality of education was recorded in **university_15**.  
> These findings are based on the proportion of negative labels assigned to each category per university.
![Insights_2](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Insights_2.png))

### 📊 Key Insights from Negative Feedback Across Years

- **Attitude Towards Students:** From 2017 onwards, complaints about student treatment have noticeably increased.  
- **Corruption:** The highest frequency of complaints occurred during 2010–2019.  
- **Academic Process Management:** Complaints peaked starting in 2021, reaching a particularly high share of **57.6%** of all reviews, likely related to the organization of the academic process during the war period.  
- **Education Quality:** Throughout all years, there has been a consistently high number of complaints regarding the quality of education.
  ![Insights_3](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Insights_3.png))

  ### 🌐 Language Distribution of Reviews

- Approximately **50% of reviews are in Ukrainian**.  
- Approximately **50% of reviews are in Russian**.  
- There are no other significant languages after removing the single Bulgarian review.
    ![Insights_4](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Insights_4.png))

  # 🗣️ Language Dynamics of Reviews Over Time

- In **2010–2012**, the distribution of review languages was roughly **50/50 between Ukrainian and Russian**.  
- Between **2013 and 2020**, reviews written in **Russian** became more prevalent.  
- Starting from **2022 and onward**, the majority of reviews have been written in **Ukrainian**.  
  This shift likely reflects broader sociolinguistic changes in society, where more users consciously choose to communicate in Ukrainian in the context of recent events and the ongoing war.
      ![Insights_5](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Insights_5.png))
  
## 7. 🤝 Semantic Recommendations

After a user submits a review, the system retrieves the top-5 semantically similar reviews to help users explore shared experiences.

## 8. 📖 Semantic Search

Allows users to search reviews using natural language queries and retrieves the most relevant results using embedding-based search.

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
`Matplotlib`, `Seaborn`, `Plotly`, `NetworkX`, `UMAP`, `WordCloud`,  
`K-means`, `HDBSCAN`, `BERTopic`


