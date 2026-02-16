#  Predicting Customer Satisfaction Score Using  Classification
<img width="1536" height="1024" alt="download" src="https://github.com/user-attachments/assets/e0bc02cd-48c8-4f28-b2e7-a8a0931f52f7" />



---

# Predicting Flipkart Customer Satisfaction (CSAT) Score Using Machine Learning

## Business Problem Overview

In today’s fast-paced e-commerce environment, customer satisfaction is critical for business growth. Companies measure service performance using CSAT (Customer Satisfaction Score).

The challenge is that CSAT is collected after the customer interaction is completed. If the score is low, it is already too late to fix the experience.

This project aims to predict customer satisfaction before the feedback is given, enabling proactive support improvements.

---

## About the Company

![Image](https://images.openai.com/static-rsc-3/RAtuJbpj3Csb4i9ISMHilrMsRNlt0Pj88D3PeflCSN6J-QJ6lBqsvshSPUQm9yBvcpyTSEVZ8Kf_psY9P9o2tmZKMMIyu9HJuk7c-KBQRZ8?purpose=fullsize\&v=1)


Flipkart is one of India’s largest e-commerce platforms, handling millions of customer interactions every month through call, chat, and email channels.

Understanding the drivers of customer satisfaction helps improve service quality, reduce churn, and increase long-term profitability.

---

## Project Objective

The goal of this project is to build a Machine Learning classification model that predicts CSAT score (1 to 5) using customer interaction details such as:

* Communication Channel
* Query Category and Sub-Category
* Product Category
* Agent Information
* Response Time
* Customer Remarks

---

## Dataset Information

* Total Records: 85,907
* Total Features: 20
* Time Period: 2022 to 2023
* Target Variable: CSAT (1 to 5)

### Important Columns

`channel_name`, `customer_query_category`, `customer_query_sub_category`, `Customer_Remarks`, `Product_category`, `Item_price`, `Agent_name`, `Supervisor`, `Manager`, `Agent Shift`, `Tenure Bucket`, `CSAT`

### Missing Values

Some columns contained high missing values:

* `connected_handling_time` (99.72 percent) and was dropped
* `Customer_City` approximately 80 percent
* `Product_category` approximately 80 percent
* `Item_price` approximately 80 percent
* `Customer_Remarks` approximately 66 percent

No duplicate rows were found in the dataset.

---

# Project Workflow

## 1. Data Understanding and Exploration

* Checked data structure and column types
* Identified missing values
* Verified duplicates
* Converted date columns to datetime format

---

## 2. Data Wrangling, EDA and Hypothesis Testing

### Data Cleaning

* Dropped columns with extremely high null values
* Used mean, mode, and constant imputation
* Created a new feature `response_time_minutes`

### Exploratory Data Analysis

Key insights:

* Faster response time was associated with higher CSAT
* App and Website related categories showed higher satisfaction
* Gift Cards and Furniture categories showed lower satisfaction
* Experienced agents and balanced workload improved CSAT

### Hypothesis Testing

* One Sample T-Test
* ANOVA Test

These tests validated whether CSAT significantly differed across communication channels and price segments.

---

## Feature Engineering and Preprocessing

* Created features such as:

  * `is_long_response`
  * `avg_csat_by_agent`
  * `agent_ticket_count`
  * `product_popularity`

* Handled outliers using IQR and percentile capping

* Applied One-Hot Encoding, Label Encoding, and Ordinal Encoding

* Selected important features using Random Forest Importance and SelectKBest

* Applied MinMax Scaling

* Used SMOTE to handle class imbalance

---

## Model Implementation

Tested multiple algorithms:

* Random Forest
* CatBoost
* XGBoost

### Final Model: XGBoost

XGBoost was selected because it handled class imbalance effectively and provided the best balance between precision and recall.

### Final Performance

* Training Accuracy: 76 percent
* Testing Accuracy: 70 percent
* Weighted F1 Score: 0.63

The model showed good generalization and did not overfit.

---

## Feature Importance Insights

The most important drivers of CSAT prediction were:

* Response Time
* Customer Sentiment
* Product Popularity
* Agent Workload
* Agent Past Performance

Customers with longer response times and negative sentiment were more likely to give lower satisfaction scores.

---

## Real-World Testing

The saved XGBoost model was tested on unseen data and performed consistently.

However, prediction performance for CSAT classes 2 and 3 was lower due to class imbalance. Future improvements can focus on collecting more balanced data to enhance performance.

---

## Business Impact

This model enables Flipkart to:

* Identify potentially dissatisfied customers before feedback submission
* Speed up responses for high-risk cases
* Assign better agents to critical tickets
* Reduce churn
* Improve customer retention
* Increase overall profitability

---

## Tech Stack

* Python
* Pandas and NumPy
* Matplotlib and Seaborn
* Scikit-Learn
* XGBoost
* CatBoost
* SHAP
* SMOTE

---

## Conclusion

This project demonstrates how Machine Learning can transform customer support from reactive to proactive.

By predicting dissatisfaction early, businesses can take preventive actions and significantly improve overall customer experience.
