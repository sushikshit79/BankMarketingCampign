# Client Term Deposit Subscription Modeling

Location of Practical Application 3 Repository: [https://github.com/sushikshit79/BankMarketingCampign](https://github.com/sushikshit79/BankMarketingCampign)

## Overview
The objective of this exercise is to evaluate and compare the performance of multiple classification models like K-Nearest Neighbors (KNN), Logistic Regression, Decision Trees, and Support Vector Machines (SVM), using a dataset derived from a bank’s phone-based marketing campaigns. 

## Business Objective
The objective of this task is to evaluate how effectively client and campaign attributes from phone based marketing interactions can be used to predict whether a client will subscribe for a term deposit. This will be assessed  by comparing which of the  K- Nearest Neighbors(KNN), Logistic Regression, Decision Trees and Support Vector MAchines(SVM) classification models can accurately predict term deposit subscription, also identify and use models based on their performance and their characteristics like interpretability, multi colinearity.

### Data Understanding & Observations

* No missing values are present in the dataset. Therefore, no records need to be dropped during preprocessing.
* The target attribute is highly imbalanced with 4640 count for yes responses and 36,458 count for no responses.
* The dataset exhibits a strong class imbalance, with only a small proportion of clients subscribing to a term deposit. As a result, model evaluation should prioritize recall, precision, and F1-score over accuracy to ensure meaningful predictive performance.
* After carefully looking at the data of all the attributes, they can be dividied in to client attributes, campaign communication, campaign history and economic indicator attributes
* Client  profile attributes(age,job,marital,education,default,housing,loan)- Provides client information on who accepted the term deposit
* Campaign communication attrubutes (contact, month, day_of_week, duration) - Helps understand how were subscribers engaged previously
* Campaign history attributes (campaign, pdays, previous, poutcome) - Provides what happened before
* Economic indicators (emp.var.rate, cons.price.idx, cons.conf.idx, euribor3m, nr.employed) - Provides what ecomomic conditions were favourable. Also, interesting would be to know if there is any multicolineraity introduced based on economic indicators
* Duration attribute is only  available for the time of client engagement is completed, this feature cannot be used as we will not have call duration data before the campiagn calls take place.
* Below are categorical and numeric features that are identified from the dataset
    * Categorical features: job, marital, education, default, housing, loan, contact, month,day_of_week, poutcome
    * Numeric features: age, campaign, pdays, previous,emp.var.rate, cons.price.idx,cons.conf.idx, euribor3m, nr.employed
* Visualization of multiple features in relation to subscription
![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/data_understanding_visuals.png](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/data_understanding_visuals.png)

## Data Preparation
* Duration data is only available after a call is complete and not before the call. The goal of the model is to predict whether a client will subscibe before the call and not after the call. Hence, removed duration feature.
* Numerical features (age, campaign, pdays, previous,emp.var.rate, cons.price.idx,cons.conf.idx, euribor3m, nr.employed) are standardized using StandardScaler to ensure they are on a comparable scale.
* Categorical features (job, marital, education, default, housing, loan, contact, month,day_of_week, poutcome) are transformed using One-Hot Encoding to convert discrete categories into a numerical format.


## Modeling

### Dummy Modeling
* Baseline model performance is established using a DummyClassifier, accuracy of the baseline model was approximately 80%. Below are the baseline model metrcis

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Mod17_dummyclassifier_metrcis.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Mod17_dummyclassifier_metrcis.jpg)


### Simple Modeling
Simple model evaluation was done using Logistic Regression. Accuracy of the model is 80%, while Recall is low loosing potential subscribers. Below are the metrics of simple model

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/mod17_simple_model_metrics.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/mod17_simple_model_metrics.jpg)

#### Modeling without Hyperparameters
Comparing the performance of the Logistic Regression model to KNN algorithm, Decision Tree, and SVM models with default setting without hyperparameters. Below are the metrics of the same

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_without_HP.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_without_HP.jpg)

#### Modeling with Hyperparameters (HP)
GridSearchCV was applied to compare Logistic Regression, KNN, Decision Tree, and SVM models using multiple hyperparameter combinations. Key evaluation metrics are shown below.

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_with_HP_Metrics.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_with_HP_Metrics.jpg)

#### Modeling with Hyperparameters and Feature Engineering 1 (HP_FE1)
This approach included combing both Hyperparameter evaluation and consolidation of economic indicators

##### Economic Indicators
The employment variation rate(emp.var.rate), Euribor rate (euribor3m), and number of employed individuals(nr.employed)  are highly correlated as they jointly reflect the underlying economic cycle. Including all three introduces multicollinearity (highly correlated), requiring feature consolidation to ensure stable and interpretable model coefficients. Fetaure consolidtaion included comibing all three variation rate, Euribor rate and employed individuals features into one feature. Key evaluation metrics are shown below.

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_HP_FE1_Metrcis.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_HP_FE1_Metrcis.jpg)

#### Modeling with Hyperparameters and Feature Engineering 2 (HP_FE2)
This approach included combining both Hyperparameter evaluation and reduction of client profile dimensionality.

##### Client Profile Dimensionality Reduction
Feature Engineering(FE2) reduces client profile dimensionality by grouping job categories and education levels into economically meaningful tiers, minimizing sparsity and improving coefficient stability. A quadratic age term is introduced to capture non-linear age effects. This approach simplifies feature representation and enhances interpretability without materially increasing model complexity. Key evaluation metrics are shown below.

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_HP_FE2_Metrics.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_HP_FE2_Metrics.jpg)

#### Modeling with Hyperparameters and Feature Engineering including 1 and 2 (HP_FE12)
This approach combined  all Hyperparameter evaluation, consolidation of economic indicators and reduction of client profile dimensionality. Key evaluation metrics are shown below.

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_HP_FE12_Metrics.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Model_HP_FE12_Metrics.jpg)

#### Model Coefficient Evaluation
#### Logistic Regression
* Provides a direct and interpretable relationship between features and the outcome, with explicit coefficient magnitudes indicating the direction and strength of impact. Hence, Logistic Regression is preferred for interpretation due to its stable and directly explainable coefficients, unlike the other models that are evaluated.
#### KNN
* Predictions depend on nearby data points and do not provide a clear explanation of individual feature impact.
#### SVC
* Decisions are made in a complex mathematical space, making feature-level interpretation difficult and less transparent.
#### Decision Tree
* Overall performance metrics are not comparable to Logistic Regression for this problem, and decision paths and feature importance can change across runs, reducing interpretability. Based on these limitations, decision trees were not used for coefficient-level interpretation.

Below is the visualization plot for top 10 feature comparison aross feature engineering variants

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/top10_feature_comparison_across_FEs.png](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/top10_feature_comparison_across_FEs.png)

## Modes Evaluation

Below are the key evaluation metrics for 16 model configurations, covering individual evaluations of hyperparameter tuning alone, Feature Engineering 1, Feature Engineering 2, and the combined approach.

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Combined_Metrics.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Combined_Metrics.jpg)

### Model by Model Interpretation

#### Logistic Regression

* Consistently achieves the best ROC–AUC across Base, FE1, FE2, and FE12, indicating the strongest ranking ability.
* Maintains high recall, effectively capturing most potential subscribers, which aligns with the business objective.
* Fastest model in both training and inference across all feature sets.
* Provides clear coefficient interpretability, making it suitable for explaining drivers of subscription behavior.
* Feature engineering marginally improves stability but does not materially change performance.

#### SVC

* Achieves competitive F1 scores and high recall, indicating good classification strength.
* ROC–AUC is consistently strong but does not outperform Logistic Regression.
* Significantly slower in both training and prediction.
* Limited interpretability and high computational cost reduce its practical appeal despite comparable performance with Linear calssification model.

#### Decision Tree

* Suffers from low recall, missing a large portion of actual subscribers.
* Training and inference are fast, but performance remains relatively unchanged across feature engineering variants.
* Suitable for rule extraction, but not optimal for the primary goal of subscriber identification.

#### KNN
* Very low recall, making it ineffective for identifying subscribers, though accuracy is high and comparable with other classifiers.
* Accuracy is misleading given the class imbalance.
* Lower ROC–AUC compared to Logistic Regression, Decision Trees, and SVC.

#### Overall Interpretation
Across all models, Logistic Regression provides the best balance of ranking ability, subscriber recall, interpretability, and computational efficiency. While SVC has comparable predictive strength but performs poorly in terms of execution time. Decision Trees and KNN perform adequately on some metrics but overall fall short on the primary business goal of identifying potential subscribers.

### Conclusion
Logistic Regression emerges as the best-performing model for this dataset. Within Logistic Regression, the FE12 model with hyperparameters (C = 0.1, penalty = L2, class_weight = balanced) is the preferred choice. FE12 consolidates multicollinear economic indicators and aggregates sparse client profile features, resulting in improved coefficient stability, strong recall, and consistent ranking performance. Below are the key evaluation metrics of Logistic Regression model, including results from **fine tuned hyperparameters and Featured Engineering 1 & 2**.

![https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Final_LogReg_Metrcis.jpg](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/Final_LogReg_Metrcis.jpg)

