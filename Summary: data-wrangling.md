# Data Wrangling Module Summary

## Overview

Data wrangling (also known as data preprocessing or data cleaning) is a necessary step in data analysis that involves converting or mapping data from one raw form into another format to make it ready for further analysis. This module covers essential techniques for preparing data for machine learning and statistical modeling.

---

## 1. Pre-processing Data in Python

**What is Data Preprocessing?**

Data preprocessing is the process of converting raw data into a format suitable for analysis. It involves several key operations performed on data frames, typically along columns where each row represents a sample (e.g., a different used car in a database).

**Key Topics Covered:**
- Identifying and handling missing values
- Data formatting and standardization
- Data normalization
- Data binning
- Converting categorical variables to numeric variables

**Basic Operations:**
- Access columns by specifying the column name
- Each column is a Pandas series
- Operations can be performed on entire columns (e.g., adding a value to each entry)

---

## 2. Dealing with Missing Values in Python

**What are Missing Values?**

A missing value occurs when no data value is stored for a feature in a particular observation. Missing values typically appear as:
- Question marks (?)
- N/A
- Zero (0)
- Blank cells
- NaN (Not a Number)

**Strategies for Handling Missing Values:**

1. **Check with data collectors** - Verify if the actual value can be retrieved
2. **Remove data** - Drop the variable or specific entries with missing values
3. **Replace data** - Substitute missing values with estimated values
4. **Leave as missing** - Keep the observation even with missing features

**Python Implementation:**

**Dropping Missing Values:**
```python
# Drop rows with missing values
dataframe.dropna(axis=0, inplace=True)

# Drop columns with missing values
dataframe.dropna(axis=1, inplace=True)
```

**Replacing Missing Values:**
```python
# Calculate mean of the column
mean_value = df['column_name'].mean()

# Replace NaN with mean
df['column_name'].replace(np.nan, mean_value, inplace=True)
```

**Best Practices:**
- For numerical variables: Use mean or median
- For categorical variables: Use mode (most common value)
- Consider domain knowledge when choosing replacement strategy
- Setting `inplace=True` modifies the dataframe directly

---

## 3. Data Formatting in Python

**What is Data Formatting?**

Data formatting brings data into a common standard of expression, allowing meaningful comparisons. It ensures data consistency and easy understanding, especially when data is collected from different sources by different people.

**Common Issues:**
- Different units (e.g., miles per gallon vs. liters per 100 km)
- Different conventions (e.g., N.Y., Ny, NY, New York)
- Incorrect data types (e.g., numbers stored as objects/strings)

**Python Implementation:**

**Unit Conversion:**
```python
# Convert miles per gallon to liters per 100 km
df['city-L/100km'] = 235 / df['city-mpg']

# Rename column
df.rename(columns={'city-mpg': 'city-L/100km'}, inplace=True)
```

**Data Type Conversion:**
```python
# Check data types
df.dtypes

# Convert data type
df['price'] = df['price'].astype('int')
```

**Common Pandas Data Types:**
- **object**: Letters or words (strings)
- **int64**: Integers
- **float64**: Real numbers

**Key Methods:**
- `dataframe.dtypes` - Check data types
- `dataframe.astype()` - Convert data types
- `dataframe.rename()` - Rename columns

---

## 4. Data Normalization in Python

**What is Data Normalization?**

Normalization is the process of bringing data into a similar range to enable fairer comparison between different features. It ensures all features have similar influence on statistical models.

**Why Normalize?**
- Different features may have vastly different ranges
- Features with larger values can disproportionately influence models
- Makes statistical analyses easier
- Important for computational efficiency

**Example:**
Age ranges from 0 to 100, while income ranges from 0 to 500,000. Without normalization, income would have 1,000x more influence on a linear regression model than age.

**Three Normalization Methods:**

**1. Simple Feature Scaling**
- Formula: \(x_{new} = \frac{x_{old}}{x_{max}}\)
- Range: 0 to 1
- Python: `df['length'] = df['length'] / df['length'].max()`

**2. Min-Max Normalization**
- Formula: \(x_{new} = \frac{x_{old} - x_{min}}{x_{max} - x_{min}}\)
- Range: 0 to 1
- Python: `df['length'] = (df['length'] - df['length'].min()) / (df['length'].max() - df['length'].min())`

**3. Z-Score (Standard Score)**
- Formula: \(x_{new} = \frac{x_{old} - \mu}{\sigma}\)
- Range: Typically -3 to +3 (centered around 0)
- Python: `df['length'] = (df['length'] - df['length'].mean()) / df['length'].std()`

**Key Pandas Methods:**
- `.max()` - Maximum value
- `.min()` - Minimum value
- `.mean()` - Average value
- `.std()` - Standard deviation

---

## 5. Binning in Python

**What is Binning?**

Binning is the process of grouping numerical values into bins or categories. It transforms continuous numerical data into discrete categorical data.

**Benefits:**
- Can improve accuracy of predictive models
- Provides better understanding of data distribution
- Useful for comparing groups of data
- Simplifies complex numerical ranges

**Example:**
Car prices ranging from $5,188 to $45,400 (201 unique values) can be categorized into three bins:
- Low price
- Medium price
- High price

**Python Implementation:**

```python
import numpy as np
import pandas as pd

# Create bins with equal width
bins = np.linspace(min(df['price']), max(df['price']), 4)

# Create bin labels
group_names = ['Low', 'Medium', 'High']

# Segment data into bins
df['price-binned'] = pd.cut(df['price'], bins, labels=group_names, include_lowest=True)
```

**Key Functions:**
- `np.linspace()` - Creates equally spaced dividers
- `pd.cut()` - Segments and sorts data into bins

**Visualization:**
Use histograms to visualize the distribution of binned data and understand the frequency of values in each bin.

---

## 6. Turning Categorical Variables into Quantitative Variables in Python

**Why Convert Categorical to Quantitative?**

Most statistical models cannot accept objects or strings as input - they only work with numerical values. Categorical variables must be encoded as numbers for model training.

**One-Hot Encoding**

One-hot encoding creates new binary features for each unique category:
- Create a new column for each unique value
- Set to 1 when that value occurs
- Set to 0 otherwise

**Example:**
Fuel type with two values (gas, diesel):

| Original | gas | diesel |
|----------|-----|--------|
| diesel   | 0   | 1      |
| gas      | 1   | 0      |
| diesel   | 0   | 1      |
| gas      | 1   | 0      |

**Python Implementation:**

```python
# Convert categorical variable to dummy variables
dummy_variable = pd.get_dummies(df['fuel-type'])

# The method automatically creates binary columns for each category
```

**Key Method:**
- `pd.get_dummies()` - Converts categorical variables to dummy/indicator variables

**Use Cases:**
- Fuel type (gas/diesel)
- Color categories
- Geographic regions
- Any categorical feature with discrete values

---

## Summary

Data wrangling is essential for preparing raw data for analysis. The key techniques covered include:

1. **Handling missing values** - Drop or replace with appropriate values
2. **Formatting data** - Standardize units, formats, and data types
3. **Normalizing data** - Scale features to similar ranges
4. **Binning** - Group numerical values into meaningful categories
5. **Encoding categorical variables** - Convert text categories to numerical format

These preprocessing steps ensure data quality, consistency, and compatibility with machine learning algorithms and statistical models.

Here is a clean **Markdown-formatted analysis** of your content with bullet styling, proper structure, and clarity:

---

## 📌 **Data Formatting & Pre-Processing Concepts (Analysis Summary)**

Data formatting and preprocessing are essential steps before performing statistical analysis or building machine-learning models. The key ideas from the content are summarized below:

---

### ✅ **1. Importance of Data Formatting**

* Ensures consistency and comparability of data collected from different sources.
* Makes raw input usable for analysis and modeling.

---

### ✅ **2. Unit Conversion**

* Real-world datasets may contain different measurement units.
* Python can be used to convert units (e.g., **city MPG ➝ city L/100 km**) for easier cross-comparison.
* Unit conversion prevents misinterpretation and ensures uniform analysis.

---

### ✅ **3. Correcting Data Types**

* Columns can have incorrect formats (e.g., numeric values stored as strings).
* Python (pandas) allows:

  * Converting strings to numeric types
  * Parsing dates
  * Fixing categorical vs. continuous fields
* Correct data types are necessary for accurate **statistics, visualization, and modeling**.

---

### ✅ **4. Data Normalization**

* Normalization makes variables **comparable in scale**, reducing bias in statistical and ML models.
* Common techniques:

  * **Feature Scaling**
  * **Min-Max Normalization**
  * **Z-Score Standardization**
* Pandas can apply these methods directly on numerical columns.

---

### ✅ **5. Binning (Data Discretization)**

* Converts continuous variables (like *price*) into categorical groups (bins).
* Helps:

  * Simplify models
  * Improve readability
  * Enhance visualization
* Python tools:

  * `numpy.linspace`
  * `pandas.cut`

---

### ✅ **6. Visualization with Histograms**

* After binning, histograms help visualize:

  * Data distribution
  * Frequency patterns
  * Outliers or skewness

---

### ✅ **7. Handling Categorical Variables**

* Many models only accept **numeric inputs**, not text labels.
* Categories (e.g., *fuel type*) must be encoded.
* Solution: **One-Hot Encoding** using `pandas.get_dummies()`

  * Converts categories into binary indicator columns
  * Makes data machine-learning ready

---

### 🎯 **Overall**

The content highlights the essential preprocessing pipeline in Python:

| Step            | Technique             | Purpose                     |
| --------------- | --------------------- | --------------------------- |
| Unit Conversion | MPG → L/100km         | Standardize units           |
| Fix Data Types  | Convert columns       | Accurate stats & processing |
| Normalization   | Min-Max, Z-Score      | Comparable scales           |
| Binning         | `cut()`, `linspace()` | Group continuous data       |
| Encoding        | One-Hot Encoding      | Prepare categorical data    |


