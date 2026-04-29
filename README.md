Student Dropout Risk Prediction: An Early-Warning System for Educational Institutions

Project Overview
Student dropout leads to lost tuition revenue, reduced graduation rates, and negative student outcomes. Drawing parallels to customer retention and churn prevention in Customer Success Management, this project develops a machine learning-based early-warning system to identify at-risk students before disengagement leads to dropout.

By providing a calibrated dropout risk score, this system enables academic advisers, financial counselors, and retention teams to prioritize limited intervention resources effectively—routing students to the right support (financial aid, tutoring, counseling) at the right time.


Business Problem & Success Metrics
Problem Statement: Academic institutions need to identify students at risk of dropping out early enough to intervene, but intervention resources (adviser time, counseling programs, financial aid) are limited. A data-driven triage system is needed to rank students by dropout probability and route them to appropriate support services.

Primary Technical Metric: Recall at the top 15% risk threshold (maximizing capture of actual dropouts while aligning with adviser capacity constraints).

Secondary Metrics: Precision, F1-Score, PR-AUC, ROC-AUC, and Brier Score (calibration).

Business KPIs:

Retention uplift among flagged + intervened students (vs. baseline/control)
ROI = (Tuition protected from avoided dropouts) - (Intervention costs)
Operational feasibility via flag rate aligned to adviser capacity

Dataset
Source: Higher education predictors of student retention (Kaggle) Kaggle Dataset

Size: 4,424 students | 35 features
Target Variable: Binary Classification (Dropout y=1 vs. Non-Dropout y=0)
Class Distribution: 32.1% Dropouts | 67.9% Non-Dropouts (Graduate + Enrolled)


Why This Dataset is High-Quality
The dataset combines:

Demographics (gender, age at enrollment, nationality)
Socioeconomic proxies (parental education/occupation, scholarship holder)
Financial risk signals (debtor status, tuition payment status)
Early academic performance (1st semester curricular units approved/credited)
Macroeconomic context (unemployment rate, inflation, GDP)
All of these are plausible drivers of student retention and available early enough for actionable intervention.

Data Preprocessing & Feature Engineering
Data Quality:

Duplicates: 1 duplicate record removed
Missing Values: None detected
Outliers: IQR-based detection applied to systematically handle extreme values without assuming normality
Transformations:

Yeo-Johnson power transformations for right-skewed features (e.g., curricular units)
StandardScaler normalization for distance-based model baselines

Model Selection & Experimentation
Extensive experimentation was conducted across:

Baseline: Logistic Regression (F1: 0.850, Accuracy: 0.855)
Tree-based: Decision Trees (F1: 0.820), Random Forest (F1: 0.855), XGBoost (F1: 0.862)
Kernel methods: SVM with RBF kernel (F1: 0.860, but slower training)
Deep Learning: Neural networks (F1: 0.862, but computationally expensive)

Final Model: XGBoost
Performance:

Accuracy: 0.864
F1-Score: 0.862
Training Time: 0.37 seconds

Why XGBoost?

Best balance of predictive power and computational efficiency
Built-in feature importance for interpretability
Effective handling of class imbalance through gradient boosting
Regularization prevents overfitting
Significantly faster than deep learning without sacrificing performance

Explainability & Ethical AI
Trust is critical for stakeholder adoption. We utilized SHAP (Shapley Additive exPlanations), Partial Dependence Plots (PDPs), and Individual Conditional Expectation (ICE) plots to ensure transparency.

Key Drivers of Dropout Risk
SHAP analysis reveals the top predictors:

Financial Stress:

Debtor = 1 (outstanding institutional debt)
Tuition fees up to date = 0 (payment delinquency)
Academic Performance:

Low Curricular units 1st sem (approved) (fewer than 3 units approved = dramatically higher risk)
Protective Factors:

Scholarship holder = 1 (significantly reduces dropout probability)
Non-Traditional Students:

Age at enrollment ≥ 25 (increased risk due to work-life balance challenges)

Actionable Insights for Interventions
For any flagged student, advisers can see exactly why they were identified as at-risk:
This enables routing to the right intervention:

Financial issues → Financial Aid Office
Academic struggles → Tutoring/Academic Advising
Engagement issues → Student Success Programs


