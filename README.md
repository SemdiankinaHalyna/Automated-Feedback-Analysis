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

3. **Find Like-Minded Reviews (Semantic Recommendations)**  
   - **After a user submits a review**, the system uses **NLP embeddings** to identify the **top-5 semantically similar reviews**, helping users connect with others who share similar opinions.

4. **Search Relevant Reviews (Semantic Search)**  
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

5. [**Problem Classification Model**](https://github.com/SemdiankinaHalyna/University-review-analysis#5--problem-classification-model)

6. [**[In Progress]Semantic Recommendations**](https://github.com/SemdiankinaHalyna/University-review-analysis#6--semantic-recommendations)

7. [**[In Progress] Semantic Search**](https://github.com/SemdiankinaHalyna/University-review-analysis#7-semantic-search)

   


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

## 2. 🧹 Preprocessing
- Collected reviews from all sources were combined into a single DataFrame.
- Records with missing review text were removed.
- Since the data came from different platforms, inconsistencies appeared in:

  - university names,
  - date format,
  - number of reviews,
  - average ratings.

- University names were standardized (e.g., consistent abbreviation usage, removal of extra spaces/symbols).
- Universities with fewer than 100 reviews were excluded from the analysis to ensure statistical significance.
- The values in the “Number of Reviews” column were updated considering data from all sources.
- Average ratings were calculated as the arithmetic mean of star ratings for each university.
- A new Timestamp column was added for convenient date handling in further analysis.

## 3. 📊 Exploratory Data Analysis (EDA)
A plot of the distribution of review counts over time was created. The highest user activity was observed during 2017–2021, which may indicate an increased interest in discussing the quality of education during this period

![Distribution of review counts over time](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Years.png)

 Built distribution and density plots to analyze the tendency towards positive/negative reviews
 
 ![CDF](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/PDF.png)

- 0.56% of reviews have high ratings
- 0.07% of reviews have neutral ratings
- 0.37% of reviews have low ratings
![CDF](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/CDF.png)

The top 10 universities with the highest average rating were selected, calculated as the arithmetic mean of user star ratings

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

![Heat Map](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/Images/Heat_Map.png))
 
## 5. 📂 Problem Classification Model

Preparation for topic classification
For problem classification (e.g., teaching quality, accommodation, administration), a manually labeled dataset was created based on reviews with mismatches.
This approach allowed the model to learn from the most ambiguous cases, which is expected to improve its accuracy in the future.

## 6. 🤝 Semantic Recommendations

## 7. 📖 Semantic Search

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

