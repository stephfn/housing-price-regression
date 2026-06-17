# Optimized pipeline using PCA and StandardScaler, boosting $R^2$ from 0.648 to 0.841

# Housing Price Regression with PCA and Feature Selection

## Overview

This project explores dimensionality reduction and feature selection techniques in machine learning using the House Prices dataset. Linear regression models were developed and evaluated before and after applying Principal Component Analysis (PCA) and variance threshold feature selection methods.

The project compares how preprocessing and feature engineering techniques influence regression model performance, interpretability, and dataset dimensionality.

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
