## Prediction and Decision Making

**Prediction and Decision Making** focuses on how to validate whether a regression model is correct by making predictions and ensuring the results are sensible. The process involves several key steps:

**Making Predictions and Validating Results**

When a trained model makes predictions, the first validation step is ensuring the results make sense. For example, if predicting car price from highway miles per gallon, a prediction of \$13,771 for 30 MPG is reasonable—not negative, impossibly high, or unrealistically low. The model's coefficients reveal the relationship between variables. In this case, each 1-unit increase in highway MPG corresponds to approximately a \$821 decrease in car price, which aligns with market expectations.

**Issues with Invalid Predictions**

Sometimes models produce unrealistic values. If a model predicts negative car prices for highway MPG values between 0-100, this typically indicates one of three problems: the variable range isn't realistic for the data domain, the linear assumption is incorrect, or the model lacks training data for that range. Visualization is essential here—by plotting predictions across the expected range, you can identify when the model extends beyond valid boundaries.

**Evaluation Approaches**

The comprehensive evaluation framework includes three essential methods:

1. **Visualization Methods**: Regression plots show how well the fitted line matches actual data trends. Residual plots reveal non-linear behavior through curvature patterns. Distribution plots are particularly useful for multiple linear regression, highlighting accuracy issues in specific value ranges.
2. **Numerical Measures**: Mean Squared Error (MSE) and R-squared quantify model performance numerically rather than visually.
3. **Model Comparison**: Comparing different regression approaches (Simple Linear Regression vs. Multiple Linear Regression vs. Polynomial Regression) helps determine which best suits the data.

<p style="text-align:center">
    <img src="images/Model evaluation and decision-making framework.png">
</p>

Model evaluation and decision-making framework

**Important Caution About Model Comparison**

A critical insight: lower MSE doesn't always indicate a better model. Multiple Linear Regression (MLR) produces lower MSE than Simple Linear Regression (SLR) simply because adding more variables reduces error, not necessarily because the model is superior. Similarly, polynomial regression will have lower MSE than linear regression. The same inverse relationship applies to R-squared values. Therefore, direct numerical comparison between different model types requires careful consideration of complexity and overfitting risk.

## Measures for In-Sample Evaluation

**In-Sample Evaluation** provides numerical methods to assess how well a regression model fits the training data. Two fundamental metrics are **Mean Squared Error (MSE)** and **R-squared (Coefficient of Determination)**.

**Mean Squared Error (MSE)**

MSE quantifies prediction error by calculating the average of squared differences between actual and predicted values. The calculation process involves three steps:

1. Find the difference between actual value (y) and predicted value (ŷ)
2. Square this difference
3. Average all squared differences across all samples

For example, if the actual value is 150 and predicted value is 50, the difference is 100, which when squared gives 10,000. After computing this for all samples and averaging, you get the MSE.

In Python, you can use:

```python
from sklearn.metrics import mean_squared_error
mse = mean_squared_error(actual_values, predicted_values)
```

As MSE increases, predictions deviate further from actual values. A lower MSE indicates better model fit.

<p style="text-align:center">
    <img src="images/Mean Squared Error (MSE) calculation visualization.png">
</p>

Mean Squared Error (MSE) calculation visualization

**R-Squared (Coefficient of Determination)**

R-squared measures how close the actual data lies to the fitted regression line, essentially comparing your regression model against a naive baseline model (simply using the mean of all data points). If your independent variable is a good predictor, the regression model should significantly outperform just using the average.

**R-squared Formula and Interpretation:**

$R^2 = 1 - \frac{\text{MSE of regression line}}{\text{MSE of the average}}$

The metric ranges from 0 to 1 (though negative values indicate overfitting):

- **R² ≈ 1**: Excellent fit. The regression line is much better than the mean. The squared error area under the regression line is much smaller than under the mean line.
- **R² ≈ 0**: Poor fit. The regression line performs similarly to just using the data mean, suggesting the independent variable has little predictive power.
- **Negative R²**: Indicates overfitting or model problems requiring investigation.

**Practical R-squared Interpretation:**

An R-squared of 0.49659 means approximately 49.66% of the price variation is explained by the simple linear model—the remaining 50% depends on other factors. The acceptable threshold for R-squared varies by field; some researchers suggest values should be ≥ 0.10.

<p style="text-align:center">
    <img src="images/R-squared comparison.png">
</p>
R-squared comparison: Good fit (R² ≈ 1) versus poor fit (R² ≈ 0)
***

**Visual Summary:**

<p style="text-align:center">
    <img src="images/Residual plots for assessing model assumptions and detecting non-linear patterns.png">
</p>


Residual plots for assessing model assumptions and detecting non-linear patterns

These evaluation measures form the foundation for rigorous model assessment, ensuring predictions are both statistically sound and practically meaningful. When combined with visualization techniques and proper model comparison methodology, they provide comprehensive insight into regression model performance.

