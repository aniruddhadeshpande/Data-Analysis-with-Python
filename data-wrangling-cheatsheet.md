# Data Wrangling Cheat Sheet

A quick reference guide for essential data wrangling operations in Python using Pandas and NumPy.

---

## 📊 Handling Missing Values

### Replace Missing Data with Frequency (Mode)
Replace missing values with the most frequently occurring entry in the column.

```python
MostFrequentEntry = df['attribute_name'].value_counts().idxmax() 
df['attribute_name'].replace(np.nan, MostFrequentEntry, inplace=True)
```

**Use Case:** Categorical variables or discrete numerical data

---

### Replace Missing Data with Mean
Replace missing values with the average of all entries in the column.

```python
AverageValue = df['attribute_name'].astype(<data_type>).mean(axis=0)
df['attribute_name'].replace(np.nan, AverageValue, inplace=True)
```

**Use Case:** Continuous numerical data

---

## 🔧 Data Type Management

### Fix Data Types
Convert column data types to appropriate formats.

```python
df[['attribute1_name', 'attribute2_name']] = \
df[['attribute1_name', 'attribute2_name']].astype('data_type')

# Common data types: 'int', 'float', 'str', 'bool'
```

**Example:**
```python
df[['price', 'mileage']] = df[['price', 'mileage']].astype('float')
```

---

## 📏 Data Normalization

### Normalize Data (0 to 1 Range)
Scale values to be between 0 and 1 using simple feature scaling.

```python
df['attribute_name'] = df['attribute_name'] / df['attribute_name'].max()
```

**Other Normalization Methods:**

**Min-Max Normalization:**
```python
df['attribute_name'] = (df['attribute_name'] - df['attribute_name'].min()) / \
                       (df['attribute_name'].max() - df['attribute_name'].min())
```

**Z-Score Normalization:**
```python
df['attribute_name'] = (df['attribute_name'] - df['attribute_name'].mean()) / \
                       df['attribute_name'].std()
```

---

## 📦 Binning

### Create Bins for Data
Group continuous numerical data into discrete bins.

```python
bins = np.linspace(min(df['attribute_name']), 
                   max(df['attribute_name']), n)
# n is the number of bins needed

GroupNames = ['Group1', 'Group2', 'Group3']
df['binned_attribute_name'] = pd.cut(df['attribute_name'], 
                                     bins, 
                                     labels=GroupNames, 
                                     include_lowest=True)
```

**Example:**
```python
bins = np.linspace(min(df['price']), max(df['price']), 4)
GroupNames = ['Low', 'Medium', 'High']
df['price_binned'] = pd.cut(df['price'], bins, labels=GroupNames, include_lowest=True)
```

---

## 🏷️ Column Management

### Change Column Name
Rename dataframe columns.

```python
df.rename(columns={'old_name': 'new_name'}, inplace=True)
```

**Multiple Columns:**
```python
df.rename(columns={'old_name1': 'new_name1', 
                   'old_name2': 'new_name2'}, inplace=True)
```

---

## 🔢 Categorical to Numerical

### Create Indicator Variables (One-Hot Encoding)
Convert categorical variables into binary dummy variables.

```python
dummy_variable = pd.get_dummies(df['attribute_name'])
df = pd.concat([df, dummy_variable], axis=1)
```

**Example:**
```python
# Convert 'fuel_type' column with values ['gas', 'diesel']
fuel_dummies = pd.get_dummies(df['fuel_type'])
df = pd.concat([df, fuel_dummies], axis=1)

# Result: Two new columns 'gas' and 'diesel' with binary values
```

**With Prefix:**
```python
dummy_variable = pd.get_dummies(df['attribute_name'], prefix='attribute')
df = pd.concat([df, dummy_variable], axis=1)
```

---

## 📋 Additional Useful Operations

### Drop Missing Values
```python
# Drop rows with any missing values
df.dropna(axis=0, inplace=True)

# Drop columns with any missing values
df.dropna(axis=1, inplace=True)
```

### Check for Missing Values
```python
# Count missing values per column
df.isnull().sum()

# Check if any missing values exist
df.isnull().any()
```

### Data Type Information
```python
# View all column data types
df.dtypes

# Get detailed dataframe info
df.info()
```

### Basic Statistics
```python
# Statistical summary of numerical columns
df.describe()

# Include all columns (categorical too)
df.describe(include='all')
```

---

## 💡 Quick Tips

- Always use `inplace=True` to modify the dataframe directly, or reassign: `df = df.method()`
- Check data types before operations: `df.dtypes`
- Verify changes after operations: `df.head()`
- Use `axis=0` for row operations, `axis=1` for column operations
- Import required libraries: `import pandas as pd` and `import numpy as np`

---

## 📦 Required Imports

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt  # For visualization
```

---

**Last Updated:** October 25, 2025