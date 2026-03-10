# Executive Summary — Waze Churn Prediction

## Objective
The goal of this project was to analyze monthly user churn for Waze, identify the main behavioral factors associated with churn, and build predictive models to support retention strategy.

## Business Context
Waze leadership wanted to better understand which users are most likely to churn, why they churn, and whether user behavior data could support a predictive model for proactive retention efforts.

## Project Scope
This end-to-end project combined work completed across five stages:
- data inspection and problem framing
- exploratory data analysis
- data visualization
- hypothesis testing
- machine learning modeling and evaluation

## Dataset
- 14,999 total rows
- 13 original columns
- target variable: `label` (`retained` / `churned`)
- 700 missing labels removed for supervised modeling
- final labeled dataset: 14,299 rows

Class balance:
- retained: 82.3%
- churned: 17.7%

## Key Analytical Findings
- Users who churned tended to show lower engagement frequency.
- Higher driving intensity per active day was associated with higher churn risk.
- Device type did not show a statistically significant difference in mean drives.
- Behavioral features were more informative than device-related differences.

## Feature Engineering
Several engineered features improved the modeling process, including:
- `km_per_driving_day`
- `percent_sessions_in_last_month`
- `professional_driver`
- `total_sessions_per_day`
- `km_per_hour`
- `km_per_drive`
- `percent_of_sessions_to_favorite`

These features captured user behavior more effectively than raw activity counts alone.

## Models Built
Three classification approaches were used during the project:
- Logistic Regression
- Random Forest
- XGBoost

## Model Performance

### Logistic Regression (test)
- Accuracy: 0.8238
- Precision: 0.518
- Recall: 0.091
- F1: 0.160

### Random Forest (validation)
- Precision: 0.4688
- Recall: 0.1183
- F1: 0.1890
- Accuracy: 0.8199

### XGBoost (validation)
- Precision: 0.3807
- Recall: 0.1322
- F1: 0.1962
- Accuracy: 0.8080

### XGBoost (test)
- Precision: 0.4489
- Recall: 0.1558
- F1: 0.2313
- Accuracy: 0.8164

## Final Model Choice
The final selected model was XGBoost because it achieved the strongest recall among the tested models.

## Interpretation
Although XGBoost outperformed the logistic regression baseline and the Random Forest model on recall, overall churn detection remained limited. The model still missed a large share of actual churners.

This means the current model should not be used as a standalone production tool for churn intervention, but it is still useful for:
- identifying directional churn patterns
- prioritizing future feature development
- informing retention analysis

## Recommendations
Recommended next steps:
- improve recall through threshold tuning
- test class weighting or resampling methods
- collect richer behavioral and product-related features
- incorporate month-over-month usage trends
- add variables related to app performance, notifications, and user experience

## Conclusion
This project successfully delivered an end-to-end churn analysis and modeling workflow. It showed that churn can be partially explained by engagement and driving behavior, but also highlighted the limitations of the available data for highly accurate churn prediction.

The strongest value of this project lies not only in the final model, but in the full analytical process: business framing, EDA, hypothesis testing, feature engineering, model comparison, and stakeholder-focused interpretation.
