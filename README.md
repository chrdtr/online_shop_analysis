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

<p align="center" width="100%">
    <img width="60%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/b5f5f342-57bb-486f-9645-92fca1bd4d20"> 
</p>

<p align="center" width="100%">
    <img width="10%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/77373af2-43fb-43e1-9662-c0d467e8274c"> 
</p>

2. The distribution of the sentiment scores and the statistical measures show, that overall sentiment tends to be positive.
   A **mean of 0.21** and a **median of 0.18** on a scale between -1 and 1 confirm the histogram. This implies, that customer
   overall sentiment is slight positive.

         count    1980.000000
         mean        0.209914
         std         0.263265
         min        -1.000000
         25%         0.033333
         50%         0.177436
         75%         0.360483
         max         1.000000

<p align="center" width="100%">
    <img width="60%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/2bb90329-73b7-4012-b8fd-03a49e792cdf"> 
</p>

3. As there are 200 affiliated products for the reviews provided, we can calculate the average review score for each product
   and visualize it. **Top3 products** are 9119, 9080, 4619. **Flop3 products** are 9597, 1459, 2795. The distribution shows
   a standard-shaped pattern, but we can identify some outliers with very high and low ratings.
   
<p align="center" width="100%">
  <img width="40%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/bed63344-928b-42a1-af5a-91be3518e848">
  <img width="42%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/329d11f6-8bc7-4534-be3b-74c5869fae58">
</p>

<p align="center" width="100%">
    <img width="45%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/37e8a5be-58d1-4b7b-a69d-a66892d90a6f"> 
</p>

4. To investigate possible correlations and decide on further analyses, categorical columns "gender" and "education" have been
   transformed to numerical values. Analysis of correlations did not indicate any relationships between the variables, as they
   were distributed closely around 0. Therefore it was decided not to deploy further models like regression.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/375621bd-7090-4dec-b5a7-e5cd3cf0f5aa"> 
</p>

5. The 20 comments with the lowest and highest sentiment ratings have been displyed. The comments did confirm the respective
   sentiments and did not show any surprises.
