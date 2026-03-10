# Waze Churn Prediction | End-to-End Analytics and Machine Learning Project

## Overview
This project analyzes monthly user churn for Waze and brings together the full workflow completed across five courses of the Google Advanced Data Analytics Certificate.

The objective was to understand user churn behavior, identify the strongest drivers of churn, and build predictive models to support retention strategy.

This project covers:
- data inspection and problem framing
- exploratory data analysis
- data visualization
- hypothesis testing
- logistic regression
- tree-based machine learning models
- stakeholder communication and recommendations

## Business Problem
Waze leadership wants to reduce monthly churn by identifying users who are likely to stop using the app and understanding the behavioral patterns associated with churn.

A successful solution should help answer:
- Who is most likely to churn?
- What behavioral patterns are associated with churn?
- Which variables are most useful for prediction?
- How reliable are the resulting models?

## Dataset
**Source:** `waze_dataset.csv`  
**Rows:** 14,999  
**Original columns:** 13  
**Target variable:** `label` (`retained` or `churned`)

### Key dataset notes
- 700 rows had missing values in `label`
- These missing labels were treated as likely random based on prior analysis
- Labeled subset used for supervised modeling: **14,299 rows**
- Class balance on labeled data:
  - retained: **82.3%**
  - churned: **17.7%**

## Project Structure by Course

### Course 1 — Data Inspection and Initial Analysis
Main tasks completed:
- loaded and inspected the dataset
- checked structure, data types, and missingness
- compared rows with missing labels vs. non-missing labels
- compared churned vs. retained users
- created initial behavioral ratio features

Key findings:
- missing labels did not show strong evidence of systematic bias
- churned users appeared to drive longer distances and durations, but on fewer active days
- early signs suggested that engagement frequency was more important than raw usage volume

### Course 2 — Exploratory Data Analysis and Visualization
Main tasks completed:
- built histograms and boxplots for major numeric features
- checked categorical distributions
- explored relationships between churn and behavioral variables
- created engineered features such as `km_per_driving_day`
- built Tableau views and dashboard elements

Key findings:
- many variables were right-skewed with outliers
- churn increased as `km_per_driving_day` increased
- churn decreased as the ratio of `driving_days / activity_days` increased
- device type showed little practical difference in churn behavior

### Course 3 — Hypothesis Testing
Business question:
- Do iPhone and Android users differ significantly in mean number of drives?

Method:
- Welch’s two-sample t-test

Results:
- iPhone mean drives ≈ 67.86
- Android mean drives ≈ 66.23
- p-value ≈ 0.143

Conclusion:
- no statistically significant difference in mean drives by device

### Course 4 — Logistic Regression
Main tasks completed:
- created additional engineered features
- handled multicollinearity
- encoded categorical variables
- trained a logistic regression model
- evaluated model performance

Key findings:
- `activity_days` was the strongest predictor
- longer tenure and professional-style usage were associated with lower churn
- model accuracy was acceptable, but recall for churn was very low

Test performance:
- Accuracy: **0.8238**
- Precision: **0.518**
- Recall: **0.091**
- F1: **0.160**

Conclusion:
- the baseline logistic regression model was interpretable, but not strong enough for churn targeting

### Course 5 — Random Forest and XGBoost
Main tasks completed:
- engineered additional features
- split data into train / validation / test sets (60/20/20)
- tuned Random Forest with GridSearchCV
- tuned XGBoost with GridSearchCV
- selected the best model based on recall
- evaluated champion model on test data

## Feature Engineering
Features engineered during the project included:
- `km_per_driving_day`
- `percent_sessions_in_last_month`
- `professional_driver`
- `total_sessions_per_day`
- `km_per_hour`
- `km_per_drive`
- `percent_of_sessions_to_favorite`

These engineered features were important because they captured user behavior more effectively than raw counts alone.

## Modeling Approach

### Evaluation metric
Because the dataset is imbalanced and the business cost of missing churners is relatively high, **recall** was used as the main model selection metric.

### Train / validation / test split
- training: 60%
- validation: 20%
- test: 20%

### Models built
- Logistic Regression
- Random Forest
- XGBoost

## Final Model Results

### Random Forest (cross-validation)
- Precision: **0.4740**
- Recall: **0.1071**
- F1: **0.1747**
- Accuracy: **0.8205**

### Random Forest (validation)
- Precision: **0.4688**
- Recall: **0.1183**
- F1: **0.1890**
- Accuracy: **0.8199**

### XGBoost (validation)
- Precision: **0.3807**
- Recall: **0.1322**
- F1: **0.1962**
- Accuracy: **0.8080**

### XGBoost (test)
- Precision: **0.4489**
- Recall: **0.1558**
- F1: **0.2313**
- Accuracy: **0.8164**

## Champion Model
The final selected model was **XGBoost**, because it achieved the highest recall on validation data and outperformed both Random Forest and the earlier logistic regression baseline on churn detection.

## Confusion Matrix Insight
On the test set, the XGBoost model still missed most actual churners.

This means:
- the model is useful for directional analysis
- the model is not yet strong enough for production use as a standalone churn targeting system

## Feature Importance
Feature importance analysis showed that engineered behavioral features played a major role in the final model.

This reinforces a key lesson from the project:
**feature engineering was one of the biggest contributors to improved model performance.**

## Key Business Insights
- engagement frequency is strongly associated with retention
- users who drive intensely on fewer days are more likely to churn
- device type is not a meaningful driver of churn differences
- engineered behavioral features provide more signal than raw volume metrics alone
- the available data contains some predictive signal, but not enough for a highly reliable production churn model

## Recommendations
I would not recommend deploying the current model as a production churn decision tool.

Instead, I would recommend:
- using the model as a directional analytical tool
- improving recall through further tuning and threshold adjustment
- testing class weighting or resampling methods
- collecting richer features related to app experience and user behavior over time

## Additional Features That Could Improve the Model
Useful future features could include:
- app crash or performance data
- push notification exposure
- month-over-month activity trends
- trip purpose or route complexity
- geographic context
- traffic conditions
- customer support interactions
- in-app satisfaction indicators

## Tools Used
- Python
- pandas
- NumPy
- matplotlib
- seaborn
- scikit-learn
- XGBoost
- Tableau

## Files in This Repository
Suggested repository contents:
- Jupyter notebook with full workflow
- executive summary
- screenshots of model outputs
- Tableau dashboard screenshots
- README

## Final Takeaway
This project demonstrates an end-to-end analytics and machine learning workflow, from business framing and exploratory analysis to statistical testing, predictive modeling, and stakeholder recommendations.

More importantly, it shows that good analytics work is not just about building models. It is also about understanding the problem, selecting appropriate metrics, interpreting limitations honestly, and communicating useful business insights.
