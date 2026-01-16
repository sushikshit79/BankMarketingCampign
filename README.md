# Client Term Deposit Subscription Modeling

Location of Practical Application 3 Repository: [https://github.com/sushikshit79/BankMarketingCampign](https://github.com/sushikshit79/BankMarketingCampign)

## Overview
The objective of this exercise is to evaluate and compare the performance of multiple classification models like K-Nearest Neighbors (KNN), Logistic Regression, Decision Trees, and Support Vector Machines (SVM), using a dataset derived from a bank’s phone-based marketing campaigns. 

## Business Objective
The objective of this task is to evaluate how effectively client and campaign attributes from phone based marketing interactions can be used to predict whether a client will subscribe for a term deposit. This will be assessed  by comparing the which of the  K- Nearest Neighbors(KNN), Logistic Regression, Decision Trees and Support Vector MAchines(SVM) classification models can accurately predict term deposit subscription, also identify and use models based on their performance and their characteristics like interpretability, multi colinearity.

### Data Understanding & Observations

* No missing values are present in the dataset. Therefore, no records need to be dropped during preprocessing.
* The target attribute is highly imbalanced with 4640 count for yes responses and 36,458 count for no responses.
* The dataset exhibits a strong class imbalance, with only a small proportion of clients subscribing to a term deposit. As a result, model evaluation should prioritize recall, precision, and F1-score over accuracy to ensure meaningful predictive performance.
* After carefully looking at the data of all the attributes, they can be dividied in to client attributes, campaign communication, campaign history and economic indicator attributes
* Client  profile attributes(age,job,marital,education,default,housing,loan)- Provides client information on who accepted the term deposit
* Campaign communication attrubutes (contact, month, day_of_week, duration) - Helps understand how were subscribers engaged previously
* Duration attribute is only  availablea t the time of client engagement and highly predictive, this feature cannot be used as we will not have future calls duration data
* Campaign history attributes (campaign, pdays, previous, poutcome) - Provides what happened before
* Economic indicators (emp.var.rate, cons.price.idx, cons.conf.idx, euribor3m, nr.employed) - Provides What ecomomic conditions were favourable. Also, interesting would be to know if there is any multicolineraity introduced based on economic indicators
* Below are categorical and numeric features that are identified from the dataset
    * Categorical features: job, marital, education, default, housing, loan, contact, month,day_of_week, poutcome
    * Numeric features: age, campaign, pdays, previous,emp.var.rate, cons.price.idx,cons.conf.idx, euribor3m, nr.employed
* Visualization of multiple features in relation to subscription
  * [https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/data_understanding_visuals.png](https://github.com/sushikshit79/BankMarketingCampign/blob/main/images/data_understanding_visuals.png)

## Data Preparation


## Modeling

### Dummy Modeling

### Simple Modeling

#### Modeling with Hyperparameters

#### Modeling with Hyperparameters and Feature Engineering 1

#### Modeling with Hyperparameters and Feature Engineering 2

#### Modeling with Hyperparameters and Feature Engineering including 1 and 2

#### Model Coefficient Evaluation

### Modes Evaluation

### Final Model Execution and Metrcis
