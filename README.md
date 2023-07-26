# Analysis report: Online shop analysis

### Overview:

Data of an online retail business has been provided. The business wants to gain insights to improve
their strategy based on the findings of the analysis. The following questions were posed by management:

1. What is the customer sentiment based on written reviews?
2. How do customers accumulate loyalty points?
3. Are we able to identify customer groups based on their income and spending with the company?


# 1. Sentiment analysis using TextBlob
sentiment_analysis.ipynb

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

# 2. Multiple linear regression using scikit-learn

regression_analysis.ipynb

How do customers accumulate loyalty points? Based on the given dataset, are we able to identify any relationships?

**Analytical approach:**

- Data was imported and cleaned, redundant columns were dropped and columns were renamed 
- Data was then checked for missing values and duplicates. No missing values have been identified,
  but 203 duplicates were recognized and deleted
- Potential relationships between variables have been identified using a correlation matrix, pointing
  towards spending_score and remuneration (income) as potential regressors
- Histograms and describe() showed a skewness of regressor distributions, Shapiro-Wilk normality test
  with low p-values indicated normal distribution is not given, which violates a LM assumption
- To improve normality, regressors have been transformed using log- and boxcox-transformation, however,
  the outcomes did not deliver the intended results as further Shapiro-Wilk-testing and histograms did
  not confirm a normal distribution of the newly created transformation variables, therefore, it was
  decided to continue with the initial analysis, having the non-normal-distribution in mind
- Remuneration and spending_score showed a positive linear relationship and were decided to use for
  building the MLR model. The LM model has been fitted, trained and tested. Multicollinearity and
  Homoscedasticity have been investigated after deploying the model
- Other variables age, education and gender have also been investigated, showing no clear linear
  relationship against loyalty points. It was decided to implement age variable in a second model.
  The model was also fitted, trained, tested and assumptions have been checked.
- The last step included the random selection of three test set observations and comparison of
  the predictions of both models that have been created.

**Findings:**

1. Only **spending_score (0.67)** and **remuneration (0.62)** columns showed a significant correlation with our response
   variable loyalty points. This initial check indicates that these should be the variables to investigate further.
   
<p align="center" width="100%">
    <img width="60%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/0c8ca1c0-af32-4954-8061-7178f4313ba8"> 
</p>

2. **MLR Model 1 results:** Fitting both spending_score and remuneration in a first regression model, it produced a 0.83 R^2 on the
   training set and indicated low p-values. The variance in loyalty points can be explained by both regressors by nearly 83%.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/deeb7306-7988-46d7-8e48-4ec10fdb38cf"> 
</p>

3. **MLR Model 2 results:** Adding a third regressor age, improved the model slightly, leading to a R^2 of 0.84 on training data,
   also producing low p-values for all regressors. However, age did not show a linear relationship with loyalty points.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/48d7b0ac-c4ce-4891-b8e0-4c13756f94f0"> 
</p>   

4. Besides testing the model on the test data, three single observation have been randomly extracted from the test data set
   to visualize the actual predictions of both models. Compared to the original y values of **701, 1355, 3218**, the models
   produced the following predictions:

<p align="center" width="100%">
    <img width="40%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/5096f9c7-9215-4fe6-9f89-a3e8bde08934"> 
</p>

<p align="center" width="100%">
    <img width="40%" src="https://github.com/chrdtr/online_shop_analysis/assets/124095561/d2ac81e5-6c1d-4fb7-a719-235e3bc63e73"> 
</p>

5. **Summary and Limitations**: Different variables have been investigated to predict and deconstruct the accumulation of loyalty points.
   Although Model 2 produced slightly better results in the form of its R^2, the decision was made to use **Model 1**. This can be
   justified by approaching simplicity (R^2 only improved minimally) and the fact, that there was no linear relationship between age and
   loyaly points in advance. Although the predictions of **Model 1** were quite solid, other factors should be researched and external
   data should might be considered.

   The limitations and potential drawbacks of the model are the violation of normality assumption for the regressor variables, as both
   logarithmic and boxcox transformation did not produce normal distributed data. Although VIF factors indicated no multicollinearity,
   both models were facing heteroscedasticity issues, which violates one of the main assumptions in linear regression. This must be
   considered when using the model and should also be a starting point for future improvements. 




   
