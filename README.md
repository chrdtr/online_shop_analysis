# Analysis report: Online shop analysis

### Overview:

Data of an online retail business has been provided. The business wants to gain insights to improve
their strategy based on the findings of the analysis. The following questions were posed by management:

1. What is the customer sentiment based on written reviews?
2. How do customers accumulate loyalty points?
3. Are we able to identify customer groups based on their income and spending with the company?


# 1. Sentiment analysis using TextBlob
sa_customer_reviews.ipynb

What is the customer sentiment based on their reviews? What value can we extract from the sentiment?

**Analytical approach:**

- Data has been imported and cleaned: Redundant columns have been dropped, columns have been renamed
  and data was checked for NaNs and duplicates. 20 review column duplicates have been deleted
- Review column has been pre-processed: all punctuation has been reomved, all text was changed to lower case,
  only alphanumerical characters have been kept and column text has been tokenized
- Stopwords have been removed from tokens, all tokenized words were converted into a string variable and, for exploratory
  anylsis a wordcloud has been created, showing the most common words in the reviews
- Stopwords were also removed from the original reviews column and polarity (sentiment) scores have been calculated
  using TextBlob. A sentiment_r column was created, containing the afiliated sentiment scores
- Sentiment distribution was visualized and statistically described
- Data contained 200 distinct products. Sentiment scores wre averaged and grouped by product to find out
  which products receive the highest and lowest ratings
- A list of the 20 most positive and negative reviews has been created to sense-check the results
- Lastly, potential correlations between the sentiment and other variables were investigated by
  transforming categorical variables to numerical values, asking: What influences the review sentiment?

**Findings:**

1. The wordcloud provides us with an overview of the most common words. As this viz is only for exploratory
   analysis, a lsit has been created. Most of the words seem to have a positive sentiment, but we are
   not able to infer anything from the output.

   ![Screenshot 2023-06-29 at 13 32 59](https://github.com/chrdtr/online_shop_analysis/assets/124095561/b5f5f342-57bb-486f-9645-92fca1bd4d20)

