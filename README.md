# Kickstarter Campaign Success Prediction

## Project Overview

Crowdfunding platforms host thousands of projects every year, yet many campaigns fail to achieve their funding goals. Understanding the factors that contribute to campaign success can help creators design more effective fundraising strategies.

This project analyzes over 331,000 Kickstarter campaigns and develops machine learning models to predict campaign success using only information available before launch. In addition to predictive modeling, statistical testing and feature importance analysis were performed to identify the key drivers of crowdfunding outcomes.

---

## Business Problem

Can we predict whether a Kickstarter campaign will be successful before it launches?

Accurate prediction of campaign success can help creators:

* Set realistic funding goals
* Optimize campaign duration
* Better understand category-specific success rates
* Improve campaign design and planning decisions

---

## Dataset

* Source: Kickstarter Projects Dataset
* Total Records: 378,661 campaigns
* Final Modeling Dataset: 331,675 campaigns
* Target Variable: Campaign Success

  * 1 = Successful
  * 0 = Failed

Campaigns with statuses such as canceled, suspended, live, and undefined were removed from the analysis.

---

## Data Preparation

### Data Quality Assessment

The dataset contained minimal missing data, with only approximately 1% missing values in the `usd pledged` field.

### Leakage Detection

To ensure realistic prediction performance, variables unavailable before campaign launch were removed:

* pledged
* backers
* usd pledged
* usd_pledged_real
* state

This prevented the model from using post-launch information when making predictions.

### Feature Engineering

Several predictive features were engineered:

* CampaignDuration
* LogGoal
* LaunchMonth
* LaunchWeekday
* NameLength

Categorical variables were one-hot encoded prior to modeling.

---

## Exploratory Data Analysis

### Finding #1: Funding Goal Significantly Influences Success

Projects with smaller funding goals were substantially more likely to succeed.

| Goal Quintile | Success Rate |
| ------------- | -----------: |
| $0–$1,500     |        53.3% |
| $20,000+      |        21.4% |

A T-Test confirmed a statistically significant difference between successful and failed campaign funding goals (p < 0.001).

---

### Finding #2: Project Category Significantly Impacts Success

A Chi-Square test identified a statistically significant relationship between project category and campaign outcomes (χ² = 15,455.44, p < 0.001).

Highest-performing categories:

* Dance (65.4%)
* Theater (63.8%)
* Comics (59.1%)
* Music (52.7%)

Lowest-performing categories:

* Technology (23.8%)
* Journalism (24.4%)
* Crafts (27.1%)
* Food (27.6%)

---

### Finding #3: Campaign Duration Influences Outcomes

Campaign duration demonstrated a meaningful relationship with success.

| Campaign Duration | Success Rate |
| ----------------- | -----------: |
| 0–15 Days         |        51.3% |
| 46–60 Days        |        26.7% |

Shorter campaigns generally achieved stronger fundraising outcomes.

---

## Machine Learning Models

Three classification models were developed and evaluated.

| Model               | ROC-AUC |
| ------------------- | ------: |
| Logistic Regression |   0.725 |
| Random Forest       |   0.725 |
| XGBoost             |   0.747 |

### Final Model

XGBoost achieved the strongest predictive performance and was selected as the final model.

**Final XGBoost Performance**

* ROC-AUC: 0.747
* Accuracy: 69%
* Precision: 64%
* Recall: 51%
* F1 Score: 57%

---

## Feature Importance

The most influential predictors identified by the model were:

1. LogGoal
2. CampaignDuration
3. NameLength
4. Tabletop Games Category
5. Music Category

These findings suggest that campaign design decisions made before launch can meaningfully influence crowdfunding outcomes.

---

## Key Business Recommendations

* Set realistic funding goals to maximize the probability of success.
* Consider shorter campaign durations to create urgency and maintain engagement.
* Evaluate category-specific success trends before launching a campaign.
* Invest time in campaign presentation and communication, as campaign title characteristics were associated with campaign outcomes.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-Learn
* XGBoost
* SciPy
* Matplotlib
* Seaborn
* Jupyter Notebook

---

## Project Structure

```text
kickstarter-success-prediction/

│
├── Kickstarter_Success_Prediction.ipynb
├── README.md
├── requirements.txt
├── feature_importance.png
├── confusion_matrix.png
├── roc_curve.png
└── data/
```

---

## Author

Austin Blunt

MBA, Data Analytics | B.S. Applied Mathematics

Focused on machine learning, predictive analytics, statistical modeling, and business intelligence.
