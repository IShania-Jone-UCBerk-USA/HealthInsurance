# Advanced Data Cleaning & Preprocessing — US Health Insurance Dataset

An end-to-end data processing workflow executed on the **US Health Insurance Dataset**. This project demonstrates advanced data imputation, custom encoding strategies, robust outlier handling via Winsorization, and power transformations for skewed continuous features.

---

## Process Overview

### 1. Data Exploration
* Analyzed missing values (`isnull().sum()`), statistical distributions (`describe()`), and schema data types (`info()`).
* Synthetically injected missing values and multi-sigma outliers into continuous columns (`charges`, `age`, `bmi`) to test advanced cleaning protocols.

### 2. Missing Value Imputation
* **Group-based Conditional Imputation**: Imputed missing `bmi` entries using median values stratified by demographic subgroups (`sex` and `smoker`).
* **Multivariate Imputation (MICE / Iterative Imputer)**: Used `IterativeImputer` from `scikit-learn` to estimate missing `age` values by leveraging predictive relationships across numeric features.

### 3. Feature Encoding
* **Binary Encoding**: Mapped binary categorical variables (`sex` and `smoker`) into $0$ and $1$.
* **Frequency Encoding**: Enriched continuous space by mapping `region` categories to their global relative frequency.
* **One-Hot Encoding**: Converted nominal `region` values into indicator dummy variables while dropping the first level to avoid multicollinearity.

### 4. Outlier Detection & Capping (Winsorization)
* Generated `seaborn` boxplots to visually evaluate the dispersion of `charges` and `bmi`.
* Applied the **Interquartile Range (IQR)** method to bound extreme values instead of dropping rows:
  $$\text{Lower Bound} = Q1 - 1.5 \times \text{IQR}$$
  $$\text{Upper Bound} = Q3 + 1.5 \times \text{IQR}$$
* Values outside bounds were capped at the corresponding boundary threshold.

### 5. Feature Transformation & Scaling
* **Yeo-Johnson Power Transformation**: Applied `PowerTransformer` to normalize heavily skewed continuous features (`charges`).
* **Robust Scaling**: Scaled continuous numerical features using `RobustScaler` (median and IQR) to ensure model stability without residual outlier bias.

---

