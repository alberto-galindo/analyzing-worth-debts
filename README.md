# 🏦 Bank Recovery Analysis: Regression Discontinuity

## 📋 Project Overview

This project applies the **Regression Discontinuity Design (RDD)** technique to determine if a bank's debt recovery strategies are cost-effective. After a debt is declared "uncollectable," the bank assigns different recovery effort levels based on an **Expected Recovery Amount** score.

The primary goal is to validate whether the jump in the actual recovered amount at the **$1000 threshold** (transition from Level 0 to Level 1) justifies the additional **$50** cost per customer.

### Business Question:

> Does the extra amount recovered at the higher strategy level exceed the additional $50 in costs? In other words, is there a "discontinuity" of more than $50?

[Image of regression discontinuity graph]

-----

## 📊 Dataset Structure

The dataset `bank_data.csv` contains information on "charged-off" accounts:

  * `expected_recovery_amount`: The amount the bank estimates it can recover (Assignment Variable).
  * `actual_recovery_amount`: The amount actually received (Outcome Variable).
  * `recovery_strategy`: The level of effort applied (Level 0, Level 1, etc.).
  * `age` & `sex`: Demographic variables used for robustness checks.

-----

## 🛠️ Methodology

### 1\. Robustness Checks (Continuity Analysis)

To ensure the RDD is valid, we verify that other factors (Age, Sex) do not jump accidentally at the $1000 threshold. If they are smooth across the threshold, we can attribute the jump in recovery to the strategy itself.

  * **Age:** Tested via Kruskal-Wallis ($p > 0.05$).
  * **Sex:** Tested via Chi-Square ($p > 0.05$).
  * *Result:* The groups just above and below $1000 are statistically similar.

### 2\. Graphical Exploratory Data Analysis

We focus on the window between **$900 and $1100** to visualize the relationship between expected and actual recovery.

### 3\. Statistical Modeling (OLS Regression)

We build Linear Regression models to quantify the impact:

  * **Model 1 (No Threshold):** Analyzes the general correlation.
  * **Model 2 (True Threshold):** Adds an indicator variable ($0$ for $<\$1000$, $1$ for $\ge\$1000$) to measure the size of the discontinuity.

-----

## 🚀 Key Findings

The regression analysis confirms a significant discontinuity at the $1000 mark:

| Analysis Window | Estimated Impact (Coefficient) | Incremental Cost | Result |
| :--- | :--- | :--- | :--- |
| $900 - $1100 | **~$278\*\* | $50 | ✅ Highly Profitable |
| $950 - $1050 | **Significant** | $50 | ✅ Highly Profitable |

**Conclusion:** The Level 1 recovery strategy is highly effective. The incremental recovery (approx. $278) far exceeds the $50 cost of implementation.
