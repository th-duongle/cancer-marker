# 🧠 Predicting Cancer Outcomes Using Support Vector Machines (SVM)

## Overview

This project applies Support Vector Machine (SVM) models to predict the presence of cancer using demographic and diet data from a nationally representative U.S. health survey. The goal is to evaluate how well these factors can predict disease outcomes, and to compare the performance of different SVM kernels.

---

## Dataset

The dataset comes from the **2022 National Health Interview Survey (NHIS)**, accessed via IPUMS Health Surveys.

It includes:

* Demographics (e.g., age, sex)
* Health outcomes (cancer, heart disease, diabetes, etc.)
* Behavioral variables (diet, physical activity, sleep, alcohol use)

For this project, the focus is on:

* **Target variable:** Cancer (binary: 0 = no, 1 = yes)
* **Predictors:** Selected demographic and die variables

---

## Data Preprocessing

* Removed rows with missing target values
* Imputed missing predictor values using **median imputation**
* Standardized all features (mean = 0, std = 1)
* Encoded variables as:

  * Binary (0/1)
  * Continuous numerical values

---

## Models

Three SVM models were implemented and compared:

* **Linear Kernel**
* **Polynomial Kernel**
* **Radial Basis Function (RBF) Kernel**

### Hyperparameter Tuning

* Grid search with cross-validation (3–5 folds)
* Parameters tuned:

  * `C` (regularization strength)
  * `gamma` (kernel coefficient)
  * `degree` (for polynomial kernel)

### ⚖️ Class Imbalance Handling

* Used `class_weight='balanced'` to adjust for skewed class distribution

---

## 📈 Results

| Kernel | Train Accuracy | Test Accuracy | ROC-AUC | Precision (1) | Recall (1) | F1-score (1) |
| ------ | -------------- | ------------- | ------- | ------------- | ---------- | ------------ |
| Linear | 0.665          | 0.671         | 0.787   | 0.25          | 0.81       | 0.38         |
| Poly   | 0.679          | 0.679         | 0.781   | 0.25          | 0.79       | 0.38         |
| RBF    | 0.666          | 0.660         | 0.776   | 0.24          | 0.81       | 0.37         |

### Key Findings

* All kernels performed similarly (ROC-AUC ≈ 0.78)
* Polynomial kernel achieved slightly higher accuracy
* Linear kernel achieved the best ROC-AUC
* Models showed:

  * **High recall (~0.80)** → good at identifying cancer cases
  * **Low precision (~0.25)** → many false positives

---

## Feature Insights

From the polynomial kernel:

* **Age** was the dominant predictor (≈ 0.85 importance)
* Secondary factors:

  * Tomato sauce consumption (0.10)
  * Sex (0.05)
* Minor contributors:

  * Alcohol and sports drink consumption (~0.02)
* Coffee consumption showed a slight negative association (~ -0.10)

This suggests that cancer prediction is largely driven by age, with lifestyle variables contributing marginally.

---

## Limitations

* Strong class imbalance (few positive cancer cases)
* Reliance on self-reported survey data
* Cross-sectional dataset (no causal inference)
* Limited predictive signal from behavioral variables

---

## Future Work

* Apply resampling techniques (SMOTE, undersampling)
* Explore ensemble models (Random Forest, Gradient Boosting)
* Incorporate additional or longitudinal data
* Perform deeper feature engineering

---

## Tech Stack

* Python
* pandas, numpy
* scikit-learn
* matplotlib, seaborn

---
