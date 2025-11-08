
### **Linear & Multiple Linear Regression Summary**

* **Simple Linear Regression (SLR):** Examines the relationship between one independent variable (x) and one dependent variable (y).
* **Multiple Linear Regression (MLR):** Explains the relationship between one continuous target variable and two or more predictors.
* **Visualization Tools:**

  * `regplot` – shows the regression line and data relationship.
  * `residplot` – shows residuals to evaluate model fit and linearity.
* **Residual Analysis:**

  * Residuals should have zero mean, be evenly distributed, and show constant variance.
  * Non-random patterns suggest model adjustment is needed.
* **Distribution Plots:** Useful for comparing predicted vs. actual values in models with multiple features.
* **Polynomial Regression:**

  * Model fit depends on polynomial order.
  * Use `numpy.polyfit()` or scikit-learn’s polynomial features for non-linear data.
* **Feature Transformation & Scaling:**

  * Use `PolynomialFeatures` and `StandardScaler` (from `sklearn.preprocessing`) for better model performance.
* **Pipelines:**

  * Automate sequential steps like normalization, transformation, and prediction.
  * Simplify workflow using `sklearn.pipeline`.
* **Model Evaluation Metrics:**

  * **Mean Squared Error (MSE):** Measures average squared prediction error.
  * **R-squared (R²):** Represents the proportion of variance explained by the model.
  * **Good Model:** High R² (≈1), low MSE.
  * Negative R² can indicate overfitting or poor model performance.
* **Evaluation Techniques:**

  * Combine visual (plots) and numerical (MSE, R²) methods.
  * Compare models using both for reliability.
* **Acceptable R²:** Depends on dataset and context—no universal threshold.

