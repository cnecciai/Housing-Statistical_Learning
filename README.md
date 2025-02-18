# Housing Data Science Project

## Technical Report
**Date:** 15 April 2023  
**Prepared by:** Clark P. Necciai Jr.

## Introduction
This project aims to analyze historical house price data to develop a reliable predictive model that aligns with PA Reality’s business strategy for identifying over- and underpriced homes. Our approach included:

1. **Exploratory Data Analysis (EDA)** – Understanding relationships and complexities within the dataset.
2. **Model Fitting & Evaluation** – Assessing model performance based on various metrics.
3. **Results & Recommendations** – Summarizing key findings and proposing future improvements.

---

## Exploratory Data Analysis (EDA)
We explored relationships, patterns, and anomalies within the dataset:

- **Data Inspection**: Used `glimpse()` to review variables and data types. No missing values (`is.na()` confirmed this).
- **Response Variable (`price`)**: Right-skewed; log transformation (`log()`) applied for normalization.
- **Key Findings**:
  - **Skewed Distributions**: Most observations were single-family homes (85%) with common exterior (brick/frame) and roof type (shingle, 84%).
  - **Location & Basement Bias**: 65% of homes were outside the city, and 94% had basements, impacting model generalization.
  - **Odd Data Points**:
    - Unique `stories` values (1.7, 2.8) retained due to lack of context.
    - `lotarea = 0` for 29 observations; left unchanged due to data uncertainty.
  - **Variable Relationships**:
    - Strongest predictors of `price`: `totalrooms`, `bedrooms`, `bathrooms`, `fireplaces`, and `sqft`.

---

## Methods & Model Selection
**Performance Metric:** Root Mean Square Error (RMSE) for easy interpretability. 
- **Validation Strategy:** 10-fold cross-validation, repeated 5 times for stable estimates.

### Models Considered:

1. **Simple Linear Regression**
   - High variance inflation (VIF) detected; `rooftype`, `totalrooms`, and `location` removed.
   - **Top Variables:** `yearbuilt`, `sqft`, `bathrooms`, `bedrooms`, `avgincome`.

2. **Ridge & Lasso Regression**
   - Prevent overfitting by shrinking coefficients toward zero.
   - **Ridge Top Variables:** `sqft`, `yearbuilt`, `bathrooms`, `bedrooms`, `avgincome`.
   - **Lasso Top Variables:** `sqft`, `yearbuilt`, `bathrooms`, `bedrooms`, `rooftypeSLATE`.

3. **Stepwise Linear Regression**
   - Model selection via AIC to prioritize smaller models.
   - **Top Variables:** `sqft`, `bathrooms`, `totalrooms`, `bedrooms`, `lotarea`.

4. **PCA & PLS Regression**
   - Address high variance and dimensionality reduction.
   - **PCA Top Variables:** `sqft`, `bathrooms`, `totalrooms`, `bedrooms`, `lotarea`.
   - **PLS Top Variables:** `bathrooms`, `sqft`, `totalrooms`, `bedrooms`, `fireplaces`.

5. **Random Forest (Best Performing Model)**
   - High predictive accuracy with non-parametric approach.
   - **Top Variables:** `sqft`, `bathrooms`, `lotarea`, `yearbuilt`, `totalrooms`.

---

## Results Summary
- **Random Forest Model** outperformed all others on RMSE, R², and Mean Absolute Error (MAE).
- Consistent top predictors across models: **`sqft`, `bathrooms`, `bedrooms`**.
- All models performed within one standard deviation of each other, confirming model stability.

---

## Key Takeaways & Recommendations
- **Challenges:** Skewed variable distributions reduced predictive capability.
- **Mitigation Strategies:**
  - **Avoided overfitting** by using simpler models.
  - **Future Improvements:**
    - Collect a more balanced dataset with proportional variable distributions.
    - Increase sample size to capture variability in underrepresented home types.

---

## Conclusion
Our **Random Forest Model** provides the most reliable price predictions. However, future data collection efforts should focus on mitigating skewed distributions to further enhance model performance.
