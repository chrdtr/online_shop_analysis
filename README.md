# Analysis report: Online shop analysis

### Analytical approach:

Data of an online retail business has been provided. The business wants to gain insights to improve
their strategy based on the findings of the analysis. The following questions were posed by management:

1. What is the general customer sentiment based on written reviews?
2. How do customers accumulate loyalty points?
3. Are we able to identify customer groups based on their income and spending with the company?




# 1. Sentiment analysis using TextBlob
sa_customer_reviews.ipynb

What is the customer sentiment based on their reviews? What value can we extract from the sentiment?

- Data has been imported and cleaned: Redundant columns have been dropped, columns have been renamed
  and data was checked for NaNs and duplicates. 20 review column duplicates have been deleted
- Review column has been pre-processed: all punctuation has been reomved, all text was changed to lower case,
  only alphanumerical characters have been kept and column text has been tokenized
- For exploratory analysis, stopwords have been removed and a wordcloud was created
  





A dataset has been provided for analysis, containing different features which all have been measured during breast
cancer scans. The features have been computed from digitised images of a fine needle aspiration (FNA) of a breast mass.
These features are radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry and fractal dimension.
They have been recorded using the mean, standard error and largest of these features for each image, resulting in 30 features. (10*3)

The data which was used for the development of the different algorithms was provided by London School of 
Economics and Political Science (LSE) for research purposes. Data has already been preprocessed.

The main goal is to make predictions whether or not potential features could lead to a diagnosis of breast cancer. To 
achieve this, it was decided to train and test different machine learning models on the data provided. After validation,
the model delivering the best predictions should be chosen. 

As false negative (FN) predictions will have the most critical influence (predicting healthy, is cancer), the
main goal besides achieving a high accuracy is to minimize FNs.

As the output variable is binary, we are facing a classification problem:
  
  y = M or 1 = malignant, or<br>
  y = B or 0 = benign

To make and compare predictions, the following machine learning models have been selected:

  1. Binary logistic regression (BLR)
  2. Support vector machines (SVM)
  3. Decision trees (DT)
  4. Random forests (RF)

The models have been developed as follows:

# 1. Binary logistic regression (BLR)
  ### Accuracy: 76% (v2: 63%)
  ### False negatives: 20 (v2: 2)
  
   - Data has been imported, sense-checked and statistically described
   - One redundant column was dropped and the regression model was fitted on the
     whole dataset to check for regression assumptions
   - VIF values indicated multicollinearity, as all variables showed VIF values > 10
   - Only the five varialbes with the lowest VIF factos were kept, leading to VIF < 10
   - As data was imbalanced, SMOTE was applied for balancing. y-variable then showed 249
     results for each diagnosis
   - The logistic regression model was fitted and then evaluated on the test data
   - It delivered an accuracy of <b>76.02%</b>. As the false negatives (20) matter the most in this specific
     case, it was tried to reduce them by altering the threshold for the prediction
   - This alternative delivered low false negatives (3), but came at the cost of further
     decreasing accuracy to 62.57%.

<b>In this context, the predictive power of the model is not sufficient.</b>

 # 2. Support vector machines (SVM)
   ### Accuracy: 98.25%
   ### False negatives: 2

   - Data has been imported, sense-checked and statistically described, one redundant column was dropped
   - As data was imbalanced, SMOTE was applied for balancing. y-variable then showed 249
     results for each diagnosis
   - The linear kernel SVM-model was fitted and then evaluated on the test data
   - It delivered an accuracy of <b>96.49%</b> and 3 false negative results.
   - To further improve the model, an alternative was created, scaling the data that
     has been used with the min-max-normalization method
   - It delivered an accuracy of <b>98.25%</b> and 2 false negative results.

<b>The updated SVM-model provides a high accuracy of 98.25% and only 2 FN predictions.</b>
 
 # 3. Decision trees (DT)
   ### Accuracy: 96.49%
   ### False negatives: 3

  - Data has been imported, sense-checked and statistically described, one redundant column was dropped
  - Data was imbalanced, but as decision tree models are robust to unequal y-distributions, it was
    decided to deploy the model without the further use of balancing methods
  - The model was fitted and delivered a <b>94.15%</b> accuracy on the test data.
  - In the next step the tree was pruned, resulting in a accuracy of <b>96.49%</b> and 3 false negative results.

<b>The decision tree model provides a high accuracy of 96.49% and only 3 FN predictions.</b>

 
 # 4. Random forests (RF)
   ### Accuracy: 98.25%
   ### False negatives: 1
   
- Data has been imported, sense-checked and statistically described, one redundant column was dropped
- Data was imbalanced, but just like decision trees, as random forests are robust to unequal y-distributions,
  it was decided to deploy the model without the further use of balancing methods
- The model was fitted and delivered a <b>97.08%</b> accuracy on the test data and 4 false negative results.
- To further improve the model, an alternative was created, scaling the data that
  has been used with the min-max-normalization method
- It delivered an accuracy of <b>98.25%</b> and 1 false negative results.

<b>The random forest model provides a high accuracy of 98.25% and only 1 FN predictions.</b>

# Limitations:

- The different models were trained on a dataset containing only 569 records. To increase reliability of
  the predictions, the dataset should be continuously expanded and models further tested on unseen data
- Data quality has not been an issue. In a real-life scenario, different data issues should be regarded:
    - Where is the data coming from? From a single hospital or doctor, or more than one?
    - Are there different measurement techniques?
    - Does different measuring equipment produce different results?
    - How should we tread missing values?
- Before joining different datasets, how is the balance of the target variable distributed over different datasets?
  Are distributions the same, or do they differ between different sources?
- Do the sources themselves difffer? Are we facing different demographies in different datasets, which might could
  lead to different results in measuring the cancer cells?









