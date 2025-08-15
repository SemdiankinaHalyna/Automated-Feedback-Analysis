# University-review-analysis

### 📝 Project Overview
In this project, I identified the key issues of universities based on open feedback from students and graduates, and explored the dynamics of their reputation by analyzing ratings, sentiment, and review content.

### 🎯 Project Goal
  
This project is intended solely for educational and research purposes and does not represent any official evaluation or ranking of the institutions.
For privacy reasons, the universities are anonymized and referred to by numbers (e.g., University_1, University_2).

## 📊 Data Description:

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


## 📂 Project Structure
1. **Data Collection - data was collected from three public platforms using Selenium + BeautifulSoup parsers.**
   
2. **Preprocessing – preprocessed textual and numerical review data.**

3. **EDA – A plot of the distribution of review counts over time was created and built distribution and density plots to analyze the tendency towards positive/negative reviews. The top 10 universities with the highest average review ratings**

4. **Sentiment Analysis – applied BERT model for sentiment classification and compared results with star ratings.**

5. **University Ranking – created a ranking of universities based on review sentiment.**

6. **Temporal Sentiment Trends – visualized year-by-year sentiment change as a heatmap.**

7. **[In Progress] Problem Classification Model – developing a multi-class classification model to automatically identify key issues in negative reviews.**



   # 1. Data Collection
   
This project includes a demonstration of basic web scraping techniques used to collect student reviews of universities from publicly available websites.
To preserve privacy and comply with ethical standards:
-	The URLs of the data sources are intentionally omitted.
-	The scraping code is presented for educational purposes only, as part of a natural language processing (NLP) pipeline.[Scraping Code](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/university_reviews_scraper.ipynb)

  To collect textual reviews from students about universities, an automated parser was implemented using Selenium and BeautifulSoup.

Key steps:
- Opened the university page and hid advertisement blocks.
- Dynamically clicked on “Show all reviews” and “Read full review” buttons.
- Extracted university name, date, full text, and star rating.
- Processed HTML to extract structured data.
- Saved results to .txt files for further processing.

# 2. Preprocessing
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

# 3. 📊 Exploratory Data Analysis (EDA)
A plot of the distribution of review counts over time was created. The highest user activity was observed during 2017–2021, which may indicate an increased interest in discussing the quality of education during this period.

## 🛠 Technologies

