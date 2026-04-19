# Fairness Assessment of NYPD Stop-and-Frisk Data

## 📌 Project Overview
This project conducts a fairness and bias assessment of a machine learning model trained on NYPD Stop, Question, and Frisk (SQF) 2024 data. The goal is to evaluate whether predictive models used in high-stakes policing contexts treat demographic groups equitably and to explore mitigation strategies when disparities are identified.

The project was completed as part of IS671: Responsible AI.

## 🎯 Problem Statement
Stop-and-Frisk policies have historically exhibited racial and demographic disparities. When predictive models are trained on such data, they risk reinforcing or amplifying these biases.

## Objectives:

Train a model to predict whether a police stop results in an arrest
Audit the model for fairness across protected demographic groups
Identify proxy features that encode protected attributes
Apply and evaluate bias mitigation techniques

## Target Variable:
SUSPECT_ARRESTED_FLAG

## 📊 Dataset
Source: NYPD Stop, Question and Frisk – 2024
Records: 25,386
Features: 81
Protected Attributes
Race
Sex
Age
Suspected Proxy Features
Location data
Crime description
Physical characteristics (e.g., height, weight)
🤖 Modeling Approach
Model: XGBoost Classifier
Features Used: 29
Test Set Size: 9,783 records
Baseline Performance
Metric	Value
Accuracy	78.28%
Precision (Arrested)	71.25%
Recall (Arrested)	60.18%
⚖️ Fairness Evaluation
Fairness Metric: Separation (Equalized Odds)
Rationale:

Ensures equal treatment for individuals who will and will not be arrested
Avoids over-correction associated with Independence
Addresses false positives, which are particularly harmful in policing contexts
Disparity Results
Protected Attribute	Groups Compared	Eq-Odds Value	Severity
Age	18–24 vs 35–44	0.259	Highest
Sex	Male vs Female	0.180	Moderate
Race	Black vs White	0.163	Moderate
Key Insight:
Age-based disparity requires the most urgent mitigation.

🔍 Proxy Feature Detection
Method Used: Mutual Information

Identified Proxy Features
Age: Weight, time, crime type, build
Gender: Height, weight, crime, action
Race: Stop location, time, crime, action
Finding:
Removing protected attributes alone is insufficient—proxy features leak sensitive information and perpetuate bias.

🧠 Model Explainability
ALE (Accumulated Local Effects) plots for feature-level interpretation
SHAP global explanations to identify most influential predictors
Top contributing features include:

Search conducted
Crime group (weapon/property)
Force level
Stop duration
Stop location (borough)
🛠 Bias Mitigation Techniques
1. Reweighing
Baseline Eq-Odds: 0.259
Post-Reweighing Eq-Odds: 0.15
Advantaged Group: Age 35–44
Disadvantaged Group: Age 18–24
✅ Result: Significant fairness improvement with minimal performance degradation.

2. Additive Counterfactual Fairness (ACF)
Eq-Odds After ACF: 0.379
⚠️ Result: Did not improve fairness and increased disparity for this task.

✅ Key Takeaways
Fairness auditing is essential when modeling historically biased data
Proxy features can undermine naive fairness interventions
Reweighing proved effective for mitigating age-based bias
Fairness techniques must be evaluated contextually—no single method fits all cases
