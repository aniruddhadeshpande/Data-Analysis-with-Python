# Exploratory Data Analysis in Python - Summary

## Overview

**Exploratory Data Analysis (EDA)** is an approach to analyze data in order to:
- Summarize main characteristics of the data
- Gain better understanding of the dataset
- Uncover relationships between different variables
- Extract important variables for the problem being solved

The primary question addressed in this module: **What are the characteristics that have the most impact on car price?**

---

## 1. Descriptive Statistics

Descriptive statistical analysis helps describe basic features of a dataset and obtains a short summary about the sample and measures of the data.

### Key Methods

#### `describe()` Function
- Automatically computes basic statistics for all numerical variables
- Provides:
  - Mean
  - Total number of data points
  - Standard deviation
  - Quartiles (25th, 50th, 75th percentiles)
  - Extreme values (min and max)
- NaN values are automatically skipped

#### `value_counts()` Function
- Used to summarize categorical variables
- Categorical variables can be divided into different categories or groups with discrete values
- Example: Drive system categories (forward wheel-drive, rear wheel-drive, four wheel-drive)

### Visualization Techniques

#### Box Plots
Box plots are excellent for visualizing numeric data distributions.

**Key Features:**
- **Median**: Middle data point (50th percentile)
- **Upper Quartile**: 75th percentile
- **Lower Quartile**: 25th percentile
- **Inter-Quartile Range (IQR)**: Data between upper and lower quartiles
- **Lower Extreme**: 1.5 × IQR below the 25th percentile
- **Upper Extreme**: 1.5 × IQR above the 75th percentile
- **Outliers**: Individual dots outside the extremes

**Benefits:**
- Easy to spot outliers
- Visualize distribution and skewness
- Compare between groups effectively

#### Scatter Plots
Used to visualize relationships between continuous variables.

**Components:**
- **Predictor Variable**: Variable used to predict an outcome (typically on x-axis)
- **Target Variable**: Variable being predicted (typically on y-axis)
- Each observation is represented as a point
- Implementation: Use Matplotlib's `scatter()` function

**Best Practices:**
- Always label axes
- Include a general plot title
- Example: Engine size (predictor) vs. Price (target) shows positive linear relationship

---

## 2. GroupBy in Python

The `groupby()` method is used to group data and perform aggregate operations.

### Purpose
- Groups data by categorical variables
- Creates subsets according to different categories
- Enables comparison between groups
- Can group by single or multiple variables

### Example Use Case
**Question**: How do different drive systems (forward, rear, four-wheel) relate to vehicle price?

**Process:**
1. Select relevant columns (drive wheels, body style, price)
2. Group data by categorical variables
3. Apply aggregate function (e.g., mean)
4. Analyze average price differences across subcategories

**Finding**: Rear-wheel drive convertibles and hardtops have highest value, while four-wheel drive hatchbacks have lowest value.

### Pivot Tables

Transform grouped data into a more readable format:
- One variable displayed along columns
- Another variable displayed along rows
- Creates rectangular grid of data
- Similar to Excel pivot tables
- Use `pivot()` method in Pandas

### Heat Maps

Visual representation of pivot tables:
- Rectangular grid with color intensity based on data values
- Great for plotting target variable over multiple variables
- Provides visual clues about relationships
- Implementation: Use `pyplot.pcolor()` method
- Color intensity indicates value magnitude
- Helps identify patterns across categories

---

## 3. Correlation

**Correlation** is a statistical metric measuring the extent to which different variables are interdependent.

### Key Concepts

- When one variable changes, how does it affect the other variable?
- Variables can be positively or negatively correlated
- **Important**: Correlation doesn't imply causation

### Types of Correlation

#### Positive Correlation
- As one variable increases, the other increases
- Example: Engine size vs. Price
- Steep upward slope on scatter plot
- Both variables move in the same direction

#### Negative Correlation
- As one variable increases, the other decreases
- Example: Highway miles per gallon vs. Price
- Steep downward slope on scatter plot
- Variables move in opposite directions

#### Weak Correlation
- No clear relationship between variables
- Example: Peak RPM vs. Price
- Cannot reliably predict one variable from the other
- Scattered data points with no clear pattern

### Visualization
- Use scatter plots with regression lines
- Regression line indicates relationship direction and strength
- Steeper slope = stronger relationship
- Implementation: Use `seaborn.regplot()` function

---

## 4. Correlation Statistics

Advanced statistical methods to measure correlation strength and certainty.

### Pearson Correlation

Measures the strength of correlation between continuous numerical variables.

#### Returns Two Values:

**1. Correlation Coefficient**
- **Close to +1**: Large positive correlation
- **Close to -1**: Large negative correlation
- **Close to 0**: No correlation

**2. P-Value** (measures certainty)
- **< 0.001**: Strong certainty about the correlation
- **0.001 to 0.05**: Moderate certainty
- **0.05 to 0.1**: Weak certainty
- **> 0.1**: No certainty of correlation

### Strong Correlation Criteria
A strong correlation exists when:
- Correlation coefficient is close to +1 or -1, **AND**
- P-value is less than 0.001

### Example: Horsepower vs. Car Price
- Correlation coefficient ≈ 0.8 (close to 1)
- P-value << 0.001 (very small)
- **Conclusion**: Strong positive correlation with high certainty

### Implementation
Use `scipy.stats` package for easy calculation:
```python
from scipy import stats
pearson_coef, p_value = stats.pearsonr(df['horsepower'], df['price'])
```

### Correlation Heat Maps

Visual representation of correlations between all variables.

**Features:**
- Shows correlation between each pair of variables
- Color scheme indicates Pearson correlation coefficient
- Diagonal line shows perfect correlation (variables with themselves = 1)
- Provides overview of how different variables relate to each other
- Helps identify which variables are most strongly related to the target (price)

**Benefits:**
- Quick visual assessment of all correlations
- Identify multicollinearity issues
- Determine most important predictor variables
- Guide feature selection for modeling

---

## Key Takeaways

1. **Start with descriptive statistics** to understand data distribution and basic features
2. **Use grouping and aggregation** to uncover patterns across categorical variables
3. **Visualize relationships** using appropriate plots (box plots, scatter plots, heat maps)
4. **Measure correlation strength** using statistical methods like Pearson correlation
5. **Validate findings** with p-values to ensure statistical significance
6. **Remember**: Correlation doesn't imply causation

## Tools and Libraries Used

- **Pandas**: Data manipulation, grouping, and descriptive statistics
- **Matplotlib**: Creating scatter plots and visualizations
- **Seaborn**: Advanced plotting with regression lines
- **SciPy**: Statistical calculations including Pearson correlation
- **Pyplot**: Creating heat maps

---

## Practical Applications

This EDA approach helps answer critical business questions such as:
- Which features most impact product pricing?
- How do categorical variables influence outcomes?
- Which continuous variables are strong predictors?
- What relationships exist between different features?
- Which features should be prioritized for predictive modeling?

By following these EDA techniques, data scientists can make informed decisions about feature engineering, model selection, and hypothesis testing before building complex machine learning models.