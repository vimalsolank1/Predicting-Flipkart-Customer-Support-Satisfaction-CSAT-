

# Predicting Flipkart Customer Satisfaction (CSAT) Using Machine Learning

<img width="1536" height="1024" alt="download" src="https://github.com/user-attachments/assets/e0bc02cd-48c8-4f28-b2e7-a8a0931f52f7" />

## Business Problem Overview

In today’s fast-paced e-commerce environment, customer satisfaction plays a critical role in business growth and retention. Companies measure service performance using CSAT (Customer Satisfaction Score).

However, CSAT is collected after the customer interaction is completed. If a customer gives a low score, it is already too late to fix the experience.

This project focuses on predicting whether a customer is likely to be dissatisfied before the final feedback is submitted, allowing proactive intervention and service improvement.

---

## About the Company
![Image](https://images.openai.com/static-rsc-3/RAtuJbpj3Csb4i9ISMHilrMsRNlt0Pj88D3PeflCSN6J-QJ6lBqsvshSPUQm9yBvcpyTSEVZ8Kf_psY9P9o2tmZKMMIyu9HJuk7c-KBQRZ8?purpose=fullsize\&v=1)

Flipkart is one of India’s largest e-commerce platforms, handling millions of customer interactions through call, chat, and email support channels.

Understanding what drives customer dissatisfaction helps improve service quality, reduce churn, and increase long-term profitability.

---

## Project Objective

The objective of this project is to build a Machine Learning classification model that predicts whether a customer is:

* At-Risk (Dissatisfied)
* Satisfied

The prediction is based on customer interaction details such as:

* Communication channel
* Query category
* Agent information
* Response time
* Customer remarks
* Historical agent performance

The main goal is to detect dissatisfaction early and enable proactive support management.

---

## Dataset Information

* Total Records: 85,907
* Total Features: 20
* Time Period: 2022 to 2023
* Original Target Variable: CSAT (1 to 5)

### Important Columns

`channel_name`, `customer_query_category`, `customer_query_sub_category`, `Customer_Remarks`, `Product_category`, `Item_price`, `Agent_name`, `Supervisor`, `Manager`, `Agent Shift`, `Tenure Bucket`, `CSAT`

### Missing Values

Some columns had high missing values:

* connected_handling_time (99.72 percent) – dropped
* Customer_City approximately 80 percent
* Product_category approximately 80 percent
* Item_price approximately 80 percent
* Customer_Remarks approximately 66 percent

No duplicate rows were found.

---

# Target Transformation

The original CSAT score ranged from 1 to 5 and was highly imbalanced.

To align with the business objective of early dissatisfaction detection, the problem was converted into Binary Classification:

* 1 = At-Risk (CSAT scores 1, 2, 3)
* 0 = Satisfied (CSAT scores 4, 5)

This simplified the modeling task and directly focused on identifying dissatisfied customers.

---

# Project Workflow

## 1. Data Understanding and Exploration

* Inspected dataset structure
* Checked data types
* Identified missing values
* Verified duplicates
* Converted date columns to datetime format

---

## 2. Data Wrangling, EDA and Hypothesis Testing

### Data Cleaning

* Dropped columns with extremely high null values
* Removed negative response times using domain knowledge
* Created `response_time_mins` feature


### Exploratory Data Analysis

Key insights:

* Faster response time leads to higher satisfaction
* Negative sentiment strongly correlates with dissatisfaction
* Certain issue categories have slightly higher dissatisfaction rates
* Agent historical performance significantly impacts outcomes

### Hypothesis Testing

* Pearson Correlation Test confirmed response time significantly impacts CSAT
* One-Way ANOVA confirmed CSAT differs across communication channels

These tests validated the patterns observed in EDA.

---

# Feature Engineering and Preprocessing
* Handle missing value using constant  imputation and Applied log transformation to reduce skewness 
Created meaningful features such as:

* customer_sentiment_score using VADER sentiment analysis
* remark_length
* is_long_response
* Time-based features (hour, weekday, minute)
* agent_ticket_count
* agent_risk_rate (historical dissatisfaction rate of agent)
* supervisor_risk_rate

Agent and supervisor risk features were created after train-test split to prevent data leakage.

### Encoding and Feature Selection

* One-Hot Encoding for low-cardinality variables
* Label Encoding for high-cardinality features
* Removed constant and highly correlated features
* Feature importance using Random Forest
* SelectKBest (ANOVA F-test)
* Applied MinMax Scaling

Class imbalance was handled using class weights and scale_pos_weight in tree-based models.

---

# Model Implementation

Tested multiple algorithms:

* Random Forest
* XGBoost
* LightGBM

Evaluation Metrics Used:

* Precision
* Recall
* F1-Score
* ROC-AUC

Since the business goal is to identify dissatisfied customers, Recall for the At-Risk class was prioritized.

---

# Final Model: LightGBM

LightGBM was selected as the final model because it achieved the highest recall for the At-Risk class while maintaining stable overall performance.

### Final Test Performance

* Accuracy: 73 percent
* Recall (At-Risk): 68 percent
* Weighted F1 Score: 0.76
* ROC-AUC Score: 0.78

Training and testing performance were close, indicating no significant overfitting and good generalization.

---

# Feature Importance Insights

Using Gain-based importance and SHAP analysis, the most influential features were:

* customer_sentiment_score
* agent_risk_rate
* response_time_mins
* remark_length

Key findings:

* Negative sentiment strongly increases dissatisfaction risk
* Longer response times push prediction toward At-Risk
* Agents with high historical dissatisfaction rates increase risk probability

---

# Real-World Testing

The final LightGBM model was saved using joblib and reloaded to simulate deployment. The model was tested on unseen and real-world-like input scenarios, and it produced consistent predictions.

Future improvements can focus on advanced NLP models and improved data quality to further enhance recall and predictive performance.

---

# Business Impact

This solution enables Flipkart to:

* Identify potentially dissatisfied customers before feedback submission
* Prioritize high-risk cases
* Monitor and improve agent performance
* Reduce customer churn
* Improve retention
* Increase long-term profitability

By shifting from reactive feedback analysis to proactive dissatisfaction detection, the company can significantly enhance customer experience.

---

# Tech Stack

* Python
* Pandas and NumPy
* Matplotlib and Seaborn
* Scikit-Learn
* LightGBM
* XGBoost
* SHAP
* VADER Sentiment Analysis

---

# Conclusion

This project demonstrates how machine learning can transform customer support from reactive to proactive.

By predicting dissatisfaction early using behavioral, operational, and sentiment features, the model enables data-driven decision making and proactive customer retention strategies.

The final LightGBM model provides strong recall for dissatisfied customers while maintaining stable overall performance, making it suitable for real-world deployment.
