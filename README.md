# Housing Price Regression with PCA and Feature Selection

## Overview

This project explores dimensionality reduction and feature selection techniques in machine learning using the House Prices dataset. Linear regression models were developed and evaluated before and after applying Principal Component Analysis (PCA) and variance threshold feature selection methods.

The project compares how preprocessing and feature engineering techniques influence regression model performance, interpretability, and dataset dimensionality.

---

## 🔄 Refactoring & Major Breakthrough

While reviewing this pipeline, a deep dive into the mathematical assumptions of preprocessing data transformations revealed a critical methodology flaw in the initial version: **the use of `MinMaxScaler` immediately prior to Principal Component Analysis (PCA).**

### The Discovery: Bounded vs. Variance-Preserving Scaling
* **The Problem:** PCA operates entirely on identifying and maximizing geometric variance across orthogonal axes. Because this dataset features high-dimensional housing data (229 predictors) with extreme outliers, `MinMaxScaler` compressed the feature spaces into a tight boundary (0 to 1). This squashed the data's natural variance, forcing PCA to calculate components based on a distorted feature space.
* **The Fix:** The pipeline was refactored to utilize **`StandardScaler`**, centering the features around a mean of 0 and a standard deviation of 1. This preserved the true relative variance structure across all 229 features while safely eliminating magnitude imbalances.

### 📈 Performance Impact
Swapping to a variance-preserving preprocessing framework completely transformed the downstream Linear Regression model's predictive capabilities:

| Metric | Baseline Model (229 Features) | Refactored PCA Model (127 Components) | Improvement |
| :--- | :--- | :--- | :--- |
| **Dimensionality** | 229 Features | 127 Principal Components | **~45% reduction in complexity** |
| **R² Score** | 0.648 | **0.841** | **+19.3% variance explained** |
| **RMSE** | 51,973.14 | **34,938.50** | **-$17,034.64 in average error** |

This adjustment effectively eliminated noise and multi-collinearity from the high-dimensional feature space, proving that a model's performance is heavily contingent upon aligning preprocessing transformations with an algorithm's core mathematical assumptions.

---

## Techniques Used

- Linear Regression
- Principal Component Analysis (PCA)
- Variance Threshold Feature Selection
- Dummy Variable Encoding
- Missing Value Imputation
- MinMax Scaling
- Train/Test Split
- R² and RMSE Evaluation Metrics

---

## Dataset

The House Prices dataset was used to predict home sale prices based on multiple housing characteristics and engineered numerical features.

---

## Objective

The goal of this project was to evaluate how dimensionality reduction and feature selection impact machine learning model performance while reducing dataset complexity.

---

## Project Workflow

1. Load and inspect housing dataset
2. Clean and preprocess missing values
3. Encode categorical variables using dummy variables
4. Split dataset into training and testing sets
5. Train baseline linear regression model
6. Apply PCA while retaining 90% variance
7. Apply variance threshold feature selection
8. Compare model performance using R² and RMSE
9. Interpret the impact of dimensionality reduction techniques

---

## Key Findings

- PCA successfully reduced dimensionality while retaining 90% of dataset variance.
- Variance threshold feature selection slightly improved regression performance by removing low-variance features.
- Dimensionality reduction does not always improve predictive performance despite reducing complexity.
- Feature engineering and preprocessing decisions significantly influence regression model effectiveness.

---

## Tools and Libraries

- Python
- pandas
- NumPy
- scikit-learn
- matplotlib

---

## Repository Contents

```text
housing-price-regression/
│
├── README.md
└── housing_price_pca_regression.ipynb
```

---

## Author

Stephanie Nord  
Master’s Student in Data Science
