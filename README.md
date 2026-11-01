## Revisiting the Original Analysis

This project was originally developed while learning dimensionality reduction and feature selection with scikit-learn. Revisiting the notebook revealed several methodological issues, particularly the order of preprocessing operations and the interpretation of feature scaling before PCA.

The revised analysis separates training and testing data before fitting preprocessing transformations. Missing-value imputation, categorical encoding, scaling, and dimensionality reduction are fitted using training data, then applied to the held-out test data.

The project also compares PCA with and without standardization to examine how feature scale influences the resulting components and predictive performance.

### Understanding Feature Scaling

MinMaxScaler transforms each feature according to its observed minimum and maximum, while StandardScaler centers each feature and scales it to unit variance.

Neither transformation is universally preferable. However, StandardScaler provides a useful basis for PCA when predictors have different numerical scales and the goal is to give each feature comparable influence on the variance-based decomposition.

The revised notebook retains an unscaled PCA experiment to illustrate the consequences of applying PCA directly to predictors measured on different scales.

## Model Performance

All four regression models were evaluated using the same 80/20 train/test split of the Ames housing dataset.

| Model | Predictors or Components | R² | RMSE |
|---|---:|---:|---:|
| Baseline Linear Regression | 227 | 0.8786 | $30,509.66 |
| StandardScaler + PCA | 127 | 0.8409 | $34,938.33 |
| MinMaxScaler + VarianceThreshold | 40 | 0.6481 | $51,952.01 |
| Unscaled PCA | 1 | 0.0635 | $84,754.58 |

The baseline regression model achieved the strongest predictive performance. Standardized PCA reduced dimensionality by approximately 44% but produced a moderately higher prediction error.

Unscaled PCA retained only one principal component when configured to preserve 90% of predictor variance. This model performed substantially worse than standardized PCA, illustrating how differences in numerical scale can influence PCA.

MinMaxScaler followed by VarianceThreshold reduced the number of predictors by approximately 82%, but this reduction also decreased predictive performance.

These results demonstrate that reducing dimensionality does not necessarily improve predictive accuracy.

## Techniques Used

- Linear Regression
- Principal Component Analysis (PCA)
- StandardScaler and MinMaxScaler
- VarianceThreshold Feature Selection
- OneHotEncoder for Categorical Features
- SimpleImputer for Missing Values
- ColumnTransformer and scikit-learn Pipelines
- Train/Test Split
- R² and Root Mean Squared Error (RMSE)

## Dataset

The project uses the Ames housing dataset from Kaggle's House Prices: Advanced Regression Techniques competition.

The training dataset contains 1,460 residential property observations and 81 original columns, including the target variable, SalePrice.

After separating predictors and the target, the revised analysis uses an 80/20 train/test split. The preprocessing workflow produces 227 encoded predictors for modeling.

Dataset source: https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data

## Objective

The goal of this project was to evaluate how dimensionality reduction and feature selection influence regression performance while reducing the number of predictors used by the model.

## Project Workflow

1. Load and inspect the Ames housing training dataset.
2. Separate SalePrice from the predictors and create an 80/20 train/test split.
3. Identify columns exceeding 40% missing values using training data only.
4. Fit numerical imputation and categorical encoding on the training predictors.
5. Apply the learned preprocessing transformations to the held-out test predictors.
6. Train and evaluate baseline linear regression.
7. Compare PCA with and without StandardScaler, retaining 90% of predictor variance.
8. Apply MinMaxScaler and VarianceThreshold with a threshold of 0.10.
9. Compare all four models using R² and RMSE.

## Key Findings

- **Baseline performance:** Linear regression using all 227 preprocessed predictors achieved the highest R² and lowest RMSE of the four approaches.
- **Feature scaling and PCA:** Standardized PCA retained 127 components, compared with one component for unscaled PCA, demonstrating the importance of feature scale in variance-based dimensionality reduction.
- **Feature selection:** VarianceThreshold reduced the number of predictors to 40 but did not improve predictive accuracy over the baseline.
- **Interpretation:** Preserving predictor variance does not necessarily preserve information relevant to predicting the target variable.

## Limitations

The models were evaluated using a single train/test split rather than cross-validation. The PCA variance-retention setting, missing-value threshold, and variance-selection threshold were exploratory choices rather than optimized hyperparameters.

The analysis used ordinary linear regression without regularization. Additional evaluation could include cross-validation, residual analysis, and regularized regression models.

## Reproducing the Analysis

1. Clone this repository.
2. Download `train.csv` from the Kaggle competition linked above and place it in the repository's root directory.
3. Install the required Python libraries: pandas, NumPy, scikit-learn, and any plotting libraries imported by the notebook.
4. Open `housing_price_pca_regression.ipynb` in JupyterLab or another compatible notebook environment.
5. Restart the kernel and run all cells.

The Kaggle dataset is not included in this repository.
