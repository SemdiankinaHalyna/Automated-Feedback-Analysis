# NLP_Analysis_of_University_Reviews

### 📘 Project Overview

In this project, I analyzed open feedback from students and graduates to identify key issues of universities and explore the dynamics of their reputation. Using **NLP techniques**, the project combines **sentiment analysis, multi-label classification, and semantic search** to extract insights from **review content**, **star ratings**, and **textual feedback**.

### 🎯 Project Goal

1. **Sentiment Analysis of Reviews**  
   - **Analyze student reviews** by combining **star ratings** with **text sentiment** using a pre-trained BERT model: `nlptown/bert-base-multilingual-uncased-sentiment`.  
   - **Goal:** Automatically classify reviews as **positive, neutral, or negative**.

2. **Identify Key University Issues**  
   - **Perform multi-label classification** to detect major issues highlighted in reviews.  
   - **Approach:** **TF-IDF + fine-tuned embeddings** (`sentence-transformers/paraphrase-multilingual-mpnet-base-v2`) with **logistic regression**.  
   - **Goal:** Extract **actionable insights** about university performance and student concerns.
     
3.  To examine **language trends** in student reviews  
   — to determine **which language (Ukrainian or Russian) predominates** (using *langdetect*)  
   — and how the **linguistic distribution has changed over time** (visualized with a **heatmap**).

4. **Find Like-Minded Reviews (Semantic Recommendations)**  
   - **After a user submits a review**, the system uses **NLP embeddings** to identify the **top-5 semantically similar reviews**, helping users connect with others who share similar opinions.

5. **Search Relevant Reviews (Semantic Search)**  
   - **Users can input a query**, and the system leverages **semantic search** to retrieve the **most relevant reviews** matching the query.

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


## 📝 Project Structure
1. [**Data Collection**](https://github.com/SemdiankinaHalyna/University-review-analysis#1--data-collection)
   
2. [**Preprocessing**](https://github.com/SemdiankinaHalyna/University-review-analysis#2-preprocessing)

3. [**EDA**](https://github.com/SemdiankinaHalyna/University-review-analysis#3--exploratory-data-analysis-eda)

4. [**Sentiment Analysis with BERT**](https://github.com/SemdiankinaHalyna/University-review-analysis#4--sentiment-analysis-with-bert)

5. [**Training Classification Model**](https://github.com/SemdiankinaHalyna/University-review-analysis#5--training-classification-model)

6. [**Inference and University Problem Analysis**](https://github.com/SemdiankinaHalyna/University-review-analysis#6--inference-and-university-problem-analysis)

7. [**[In Progress]Semantic Recommendations**](https://github.com/SemdiankinaHalyna/University-review-analysis#7--semantic-recommendations)

8. [**[In Progress] Semantic Search**](https://github.com/SemdiankinaHalyna/University-review-analysis#7-semantic-search)

   


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

## 2. Preprocessing ⚙️

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

The chart shows how the number of reviews changed over time. User activity peaked between 2017 and 2021, likely reflecting a growing interest in education quality discussions

 **Built distribution and density plots to analyze users’ tendency toward positive or negative reviews.**
 
 ![CDF](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/PDF.png)


![CDF](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/CDF.png)

- **56%** of reviews have **high** ratings
- **7%** of reviews have **neutral** ratings
- **37%** of reviews have **low** ratings

![Avarage_Rating](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Avarage_Rating.png)

## 4. 🤖 Sentiment Analysis with BERT
Using Hugging Face Transformers (BERT), the sentiment of each review was determined and stored in a separate column. The BERT output was converted into categorical labels: negative / neutral / positive.
Compared BERT-predicted sentiment with star ratings.
Calculated agreement metrics (accuracy and confusion matrix). The overall agreement between star ratings and BERT sentiment was 73.31%.

![Confusion Matrix](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Confusion_Matrix.png)

Confusion matrix results:

- BERT performs fairly well at predicting positive reviews — 2,687 matches out of 3,533 (≈76%).

- Negative reviews also show good alignment — 1,866 matches out of 2,329 (≈80%).

- The biggest confusion is with positive ratings that BERT classified as negative — 664 cases (≈19% of all positive ratings).

- Neutral sentiment has the lowest accuracy and the fewest examples — which is expected, as it is the most ambiguous category.
  
An analysis of the mismatched reviews showed that discrepancies arose either due to BERT misclassification or the nature of the review itself — presence of irony/sarcasm, or subjective ambiguity (neutral or mixed opinions that are hard to classify clearly).
Therefore, for determining the overall sentiment of a university, only the reviews where BERT sentiment matched the star rating (73.31% of all reviews) were retained, ensuring that the sentiment score is reliable and trustworthy.

A thorough filtering was performed: for the final analysis, only reviews where the star rating matched the predicted sentiment were used — this approach helps reduce error.
The loss of a portion of reviews (~27%) did not have a critical impact: the analysis showed that these excluded reviews were evenly distributed across years and universities.

I assigned sentiment index values (negative: -1, neutral: 0, positive: 1)(this allowed us to work with sentiment as a numeric score) and calculated the average sentiment score for each university.
A heatmap was created to visualize sentiment dynamics over the years. The chart revealed that most universities had predominantly positive sentiment up until 2014–2015, after which sentiment began to decline in more than half of them

![Heat Map](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Heat_Map.png)
 
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

1. **Load necessary libraries**
2. **Load datasets** – datasets were **pre-cleaned and pre-processed**  
3. **Label-based fine-tuning of Transformer model**  
   (`sentence-transformers/paraphrase-multilingual-mpnet-base-v2`)  

### Block 1: Train on Fine-Tuned Embeddings Only

- **Grid Search** for hyperparameter tuning using cross-validation  
- **Train Logistic Regression** on **fine-tuned embeddings** (`sentence-transformers/paraphrase-multilingual-mpnet-base-v2`) using  
  `OneVsRestClassifier(LogisticRegression())`  
- **Evaluate model** with metrics:  
  - Precision  
  - Recall  
  - F1-score  
  - Micro average  
  - Macro average  
  - Weighted average  
  - Samples average  

### Block 2: Train on Fine-Tuned Embeddings + TF-IDF

- **Grid Search** for hyperparameter tuning using cross-validation  
- **Train Logistic Regression** on **fine-tuned embeddings + TF-IDF** (`sentence-transformers/paraphrase-multilingual-mpnet-base-v2`) using  
  `OneVsRestClassifier(LogisticRegression())`  
- **Evaluate model** with metrics:  
  - Precision  
  - Recall  
  - F1-score  
  - Micro average  
  - Macro average  
  - Weighted average  
  - Samples average  

**Model selection:** Evaluate performance and choose the best model based on metrics [Training Code](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/NLP_files/training_model_.ipynb)



## 🧩 **Conclusion**

> **💡 Note:**  
> Training on the **hybrid feature set** combining *TF-IDF* and *SentenceTransformer embeddings*  
> yields **better performance** than training on **embeddings alone**.

- **Hybrid model** achieves **Micro F1 ≈ 0.72** and **Macro F1 ≈ 0.72**  
- **Embeddings only:** Micro F1 ≈ 0.72, Macro F1 ≈ 0.71  

**Category-level insights:**
- **Academic_Process_Management:** notable improvement — F1-score increased from **0.62 → 0.71**  
- **Attitude_Towards_Students:** remains the most challenging category (**F1 ≈ 0.60**).  
  This category includes **diverse linguistic expressions** and shows **complex semantic overlap** with other problem types.  
  Further improvement may require applying **more advanced architectures such as LLM-based models** capable of deeper contextual understanding.

Overall, the **hybrid model** demonstrates **robust generalization** across categories and provides a **strong baseline** for further refinement.

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

## 8. 📖 Semantic Search

## 🛠 Technologies 
- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Hugging Face Transformers (Bert)
- Scikit-learn
- PyTorch

