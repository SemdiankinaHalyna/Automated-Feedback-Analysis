# University-review-analysis

### 📝 Project Overview
In this project, I identified the key issues of universities based on open feedback from students and graduates, and explored the dynamics of their reputation by analyzing ratings, sentiment, and review content.

### 🎯 Project Goal
  
This project is intended solely for educational and research purposes and does not represent any official evaluation or ranking of the institutions.
For privacy reasons, the universities are anonymized and referred to by numbers (e.g., University_1, University_2).

## 📊 Data Description

Number of universities: 21

Data volume: over 6,000 open reviews

Sources: collected from 3 public platforms

Data structure:

University Name

Reviews Count

Average Rating

Review Date

Review Rating

Review Text


## 📂 Project Structure
1. **Data Collection & Preprocessing – gathered and preprocessed textual and numerical review data.**

2. **Rating Distribution Analysis – built distribution and density plots to analyze the tendency towards positive/negative reviews.**

3. **Sentiment Analysis – applied BERT model for sentiment classification and compared results with star ratings.**

4. **University Ranking – created a ranking of universities based on review sentiment.**

5. **Temporal Sentiment Trends – visualized year-by-year sentiment change as a heatmap.**

6. **[In Progress] Problem Classification Model – developing a multi-class classification model to automatically identify key issues in negative reviews.**



1. **Data Collection & Preprocessing – gathered and preprocessed textual and numerical review data.**
   
This project includes a demonstration of basic web scraping techniques used to collect student reviews of universities from publicly available websites.
To preserve privacy and comply with ethical standards:
-	The URLs of the data sources are intentionally omitted.
-	The scraping code is presented for educational purposes only, as part of a natural language processing (NLP) pipeline.[Scraping Code](https://github.com/SemdiankinaHalyna/University-review-analysis/blob/main/university_reviews_scraper.ipynb)
  
The script extracts basic information such as:
- University name (anonymized)
- Number of reviews
- Average rating
- Individual review text, date, and star rating

## Technologies

