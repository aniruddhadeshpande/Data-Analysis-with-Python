# Data Analysis with Python - Course Summary

## 1. Importing and Exporting Data in Python

**Data Acquisition Fundamentals**
- Data acquisition involves loading and reading data into notebooks from various sources
- Two critical factors for reading data: **format** (CSV, JSON, XLSX, HDF) and **file path** (local or online)

**Working with Pandas read_csv**
- Use `read_csv()` method to read CSV files into Pandas DataFrame
- Set `header=None` when data lacks column headers
- Assign custom column names using `df.columns = headers`

**Data Inspection Methods**
- `df.head(n)` - displays first n rows
- `df.tail(n)` - displays bottom n rows
- Quick verification ensures data loaded correctly

**Exporting Data**
- Use `df.to_csv()` to export DataFrame to CSV format
- Specify file path and name in the method
- Pandas supports multiple file format imports/exports beyond CSV

## Import and Export Methods for Different Data Formats

| Data Format | Read Method | Save Method |
|-------------|-------------|-------------|
| CSV | `pd.read_csv()` | `df.to_csv()` |
| JSON | `pd.read_json()` | `df.to_json()` |
| Excel | `pd.read_excel()` | `df.to_excel()` |
| SQL | `pd.read_sql()` | `df.to_sql()` |

## Usage Notes

- **CSV**: Most common format for tabular data with comma-separated values
- **JSON**: JavaScript Object Notation, useful for nested/hierarchical data structures
- **Excel**: Supports .xlsx and .xls file formats for spreadsheet data
- **SQL**: Direct database interaction for reading from and writing to SQL databases

## Additional Formats Supported by Pandas

Pandas also supports importing and exporting various other data formats beyond the core four listed above, making it a versatile tool for data interchange across different platforms and systems.
---

## 2. Getting Started Analyzing Data in Python

**Understanding Data Types**
- Pandas data types: **object**, **float**, **int**, **datetime**
- Use `dtype` method to check each column's data type
- Manual correction may be needed for misclassified types (e.g., bore as object instead of numeric)

**Why Check Data Types?**
- Pandas auto-assigns types but may be incorrect
- Knowing types helps determine which Python functions apply to specific columns
- Math functions only work on numerical data

**Statistical Summary with describe()**
- Returns key statistics: count, mean, std, min, max, quartiles
- Add `include='all'` argument to include object-type columns
- Object columns show: unique, top (most frequent), and frequency
- NaN values indicate statistics cannot be calculated for that data type

**Using info() Method**
- Provides concise DataFrame overview
- Shows index dtype, columns, non-null values, and memory usage
- Useful for quick visual inspection

**Identifying Data Issues**
- Statistical summaries reveal outliers and large deviations
- Helps identify potential problems requiring attention

---

## 3. Accessing Databases with Python

**Database Connection Basics**
- Python connects to databases using API calls
- Code typically written in Jupyter Notebook
- Two types of APIs: SQL APIs and Python DB APIs

**SQL API Overview**
- Library function calls for DBMS access
- Pass SQL statements and retrieve query results
- Basic operations: connect → build SQL statement → pass to DBMS → retrieve results → disconnect

**Python DB API**
- Python's standard API for relational databases
- Allows single program to work with multiple database types
- Two main concepts: **Connection Objects** and **Cursor Objects**

**Connection Objects**
- Establish and manage database connections
- Key methods:
  - `cursor()` - returns new cursor object
  - `commit()` - commits pending transactions
  - `rollback()` - rolls back pending transactions
  - `close()` - closes database connection

**Cursor Objects**
- Used to run queries and scroll through results
- Scans through database results similar to text processing cursor

**Database Workflow**
1. Import database module
2. Use `connect()` API to open connection (pass database name, username, password)
3. Create cursor object on connection
4. Run queries and fetch results using cursor
5. Close connection to free resources

**Important**: Always close database connections to avoid unused connections consuming resources

---

## Key Takeaways

- Each line in a dataset is a row, and commas separate the values
- To understand the data, you must analyze the attributes for each column of data
- Python libraries are collections of functions and methods that facilitate various functionalities without writing code from scratch and are categorized into Scientific Computing, Data Visualization, and Machine Learning Algorithms
- Many data science libraries are interconnected; for instance, Scikit-learn is built on top of NumPy, SciPy, and Matplotlib
- The data format and the file path are two key factors for reading data with Pandas
- The read_CSV method in Pandas can read files in CSV format into a Pandas DataFrame
- Pandas has unique data types like object, float, Int, and datetime
- Use the dtype method to check each column's data type; misclassified data types might need manual correction
- Knowing the correct data types helps apply appropriate Python functions to specific columns
- Using Statistical Summary with describe() provides count, mean, standard deviation, min, max, and quartile ranges for numerical columns
- You can also use include='all' as an argument to get summaries for object-type columns
- The statistical summary helps identify potential issues like outliers needing further attention
- Using the info() Method gives an overview of the top and bottom 30 rows of the DataFrame, useful for quick visual inspection
- Some statistical metrics may return "NaN," indicating missing values, and the program can't calculate statistics for that specific data type
- Python can connect to databases through specialized code, often written in Jupyter notebooks
- SQL Application Programming Interfaces (APIs) and Python DB APIs (most often used) facilitate the interaction between Python and the DBMS
- SQL APIs connect to DBMS with one or more API calls, build SQL statements as a text string, and use API calls to send SQL statements to the DBMS and retrieve results and statuses
- DB-API, Python's standard for interacting with relational databases, uses connection objects to establish and manage database connections and cursor objects to run queries and scroll through the results
- Connection Object methods include the cursor(), commit(), rollback(), and close() commands
- You can import the database module, use the Connect API to open a connection, and then create a cursor object to run queries and fetch results
- Remember to close the database connection to free up resources