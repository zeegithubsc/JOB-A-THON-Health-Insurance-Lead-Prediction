# JOB-A-THON-Health-Insurance-Lead-Prediction (Rank 71 Solution)

## Problem Statment

Your Client FinMan is a financial services company that provides various financial services like loan, investment funds, insurance etc. to its customers. FinMan wishes to cross-sell health insurance to the existing customers who may or may not hold insurance policies with the company. The company recommend health insurance to it's customers based on their profile once these customers land on the website. Customers might browse the recommended health insurance policy and consequently fill up a form to apply. When these customers fill-up the form, their Response towards the policy is considered positive and they are classified as a lead.
Once these leads are acquired, the sales advisors approach them to convert and thus the company can sell proposed health insurance to these leads in a more efficient manner.
Now the company needs your help in building a model to predict whether the person will be interested in their proposed Health plan/policy given the information about:

•	Demographics (city, age, region etc.)

•	Information regarding holding policies of the customer

•	Recommended Policy Information


## Data Dictionary

### Train Data


Variable|Definition
|---|---|
ID|Unique Identifier for a row
City_Code|Code for the City of the customers
Region_Code|Code for the Region of the customers
Accomodation_Type|Customer Owns or Rents the house
Reco_Insurance_Type|Joint or Individual type for the recommended insurance  
Upper_Age|Maximum age of the customer 
Lower _Age|Minimum age of the customer
Is_Spouse|If the customers are married to each other (in case of joint insurance) 
Health_Indicator|Encoded values for health of the customer
Holding_Policy_Duration|Duration (in years) of holding policy (a policy that customer has already subscribed to with the company)
Holding_Policy_Type|Type of holding policy
Reco_Policy_Cat|Encoded value for recommended health insurance
Reco_Policy_Premium|Annual Premium (INR) for the recommended health insurance
Response (Target)|0 : Customer did not show interest in the recommended policy, 1 : Customer showed interest in the recommended policy

### Test Data

Variable|Definition
|---|---|
ID|Unique Identifier for a row
City_Code|Code for the City of the customers
Region_Code|Code for the Region of the customers
Accomodation_Type|Customer Owns or Rents the house
Reco_Insurance_Type|Joint or Individual type for the recommended insurance  
Upper_Age|Maximum age of the customer 
Lower _Age|Minimum age of the customer
Is_Spouse|If the customers are married to each other (in case of joint insurance) 
Health_Indicator|Encoded values for health of the customer
Holding_Policy_Duration|Duration (in years) of holding policy (a policy that customer has already subscribed to with the company)
Holding_Policy_Type|Type of holding policy
Reco_Policy_Cat|Encoded value for recommended health insurance
Reco_Policy_Premium|Annual Premium (INR) for the recommended health insurance


### Sample Submission

This file contains the exact submission format for the predictions. Please submit CSV file only.

Variable|	Definition
|---|---|
ID|	Unique Identifier for a row
Response|	(Target) Probability of Customer showing interest (class 1)

## Evaluation
The evaluation metric for this competition is roc_auc_score across all entries in the test set.

## Public and Private Split
Test data is further divided into Public 40% and Private 60%

•	Your initial responses will be checked and scored on the Public data.

•	The final rankings would be based on your private score which will be published once the competition is over.

## Rank 71 Solution Description

The solution is an ensemble of two catboost models. One with basic features and another with a more elaborate feature engineering

### Model 1 (catboost_4)

This catboost model uses  basic features. Below categorical features were label encoded and used in the model.

['City_Code', 'Region_Code', 'Accomodation_Type',  'Reco_Insurance_Type','Is_Spouse',
  'Health Indicator', 'Holding_Policy_Duration','Holding_Policy_Type',  'Reco_Policy_Cat']

### Model 2 (catboost_2)

This catboost model uses  a more elaborate feature engineering. Statistical features (mean, median, standard deviations were created) for the numeric variable - Lower_Age, Upper_Age, Reco_Policy_Premium based on the groupings for Reco_Policy_Cat, Region_Code and combination of Reco_Policy_Cat and Region_Code.

### Ensemble
Simple weighted average with equal weights were taken for the output of Model 1 and Model 2.

### Execution sequence
Execute notebooks in the below order
Catboost_2.ipynb --> catboost_4.ipynb -->  ensemble.ipynb

### Environment

Below are versions of the main packages used

  * Pandas = 1.1.3
  
  * Numpy = 1.19.2
  
  * Catboost = 0.24.4

  * Sklearn = 0.23.2

