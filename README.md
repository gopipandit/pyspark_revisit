# PySpark Practice Questions

Based on the analysis of your quiz dataset, here are practice questions organized by dataframe and difficulty level.

## Dataset Overview

### storesDF Schema
```
storeId: int
managerName: string
managerFirstName: string
openDate: date
openDateString: string
openTimestamp: timestamp
dayOfYear: int
sqft: int
division: string
productCategories: array<string>
customerSatisfaction: double
```

---

## Section 1: Basic DataFrame Operations (storesDF)

### Question 1: Filter and Select
**Task**: From `storesDF`, select only `storeId`, `managerName`, and `sqft` where `sqft` is greater than 5000.

**Expected Output**: DataFrame with 3 columns

---

### Question 2: Column Renaming
**Task**: Rename the following columns in `storesDF`:
- `storeId` → `store_number`
- `managerName` → `manager_full_name`
- `sqft` → `square_footage`

---

### Question 3: Adding Calculated Columns
**Task**: Add a new column called `size_category` to `storesDF` that categorizes stores as:
- "Small" if sqft < 3000
- "Medium" if sqft between 3000 and 7000
- "Large" if sqft > 7000

---

### Question 4: Date Manipulation
**Task**: From `storesDF`, extract the following from `openDate`:
- `open_year`
- `open_month`
- `open_day`

Add these as new columns.

---

### Question 5: String Operations
**Task**: Split `managerName` into `first_name` and `last_name` columns (assuming format "FirstName LastName").

---

## Section 2: Aggregations and Grouping

### Question 6: Basic Aggregation
**Task**: Calculate the following metrics from `storesDF`:
- Total number of stores
- Average square footage
- Maximum customer satisfaction score
- Minimum customer satisfaction score

---

### Question 7: Group By Division
**Task**: Group `storesDF` by `division` and calculate:
- Count of stores per division
- Average sqft per division
- Average customer satisfaction per division

Sort by average customer satisfaction descending.

---

### Question 8: Multiple Aggregations
**Task**: For each `division` in `storesDF`, find:
- The store with the highest customer satisfaction
- The store with the largest square footage
- The earliest opening date

---

### Question 9: Window Functions
**Task**: Add a column to `storesDF` that shows the rank of each store within its division based on `customerSatisfaction` (highest = 1).

---

### Question 10: Running Totals
**Task**: For each `division`, calculate a running total of `sqft` ordered by `openDate`.

---

## Section 3: Complex Array Operations

### Question 11: Array Contains
**Task**: Filter `storesDF` to show only stores where `productCategories` contains "Electronics".

---

### Question 12: Array Size
**Task**: Add a column `num_categories` that shows the count of product categories for each store.

---

### Question 13: Explode Array
**Task**: Explode the `productCategories` array in `storesDF` so that each product category gets its own row. Keep all other columns.

---

### Question 14: Array Aggregation
**Task**: After exploding `productCategories`, find which product category appears in the most stores.

---

### Question 15: Array Intersection
**Task**: Find stores that sell both "Electronics" AND "Home Goods" (both must be in productCategories).

---

## Section 4: Joins and Relationships

### Question 16: Self Join
**Task**: Find pairs of stores in `storesDF` that:
- Are in the same division
- Have the same manager name
- Are different stores (different storeId)

---

### Question 17: Multiple Condition Join
**Given**: `acquiredStoresDF` with columns: `storeId`, `acquisitionDate`, `previousOwner`

**Task**: Join `storesDF` with `acquiredStoresDF` to find stores that were:
- Acquired (exists in acquiredStoresDF)
- Opened before 2020
- Have customer satisfaction > 4.0

---

### Question 18: Left Anti Join
**Task**: Find stores in `storesDF` that are NOT in `acquiredStoresDF` (i.e., organically opened stores).

---

### Question 19: Cross Join with Filter
**Task**: Find all possible manager pairs (from `storesDF`) where:
- They manage stores in different divisions
- Both have customer satisfaction scores > 4.5

---

## Section 5: UDFs and Custom Functions

### Question 20: Simple UDF
**Task**: Create a UDF that converts `sqft` to square meters (1 sqft = 0.092903 sqm). Apply it to create a new column `sqm`.

---

### Question 21: String Processing UDF
**Task**: Create a UDF that takes `managerName` and returns initials (e.g., "John Smith" → "J.S.").

---

### Question 22: Complex UDF with Array
**Task**: Create a UDF that takes the `productCategories` array and returns a concatenated string with categories separated by " | ".

---

### Question 23: Conditional UDF
**Task**: Create a UDF that takes `customerSatisfaction` and returns:
- "Excellent" if >= 4.5
- "Good" if >= 3.5
- "Average" if >= 2.5
- "Poor" if < 2.5

---

### Question 24: Date UDF
**Task**: Create a UDF that takes `openDate` and returns the number of years since opening (as of today).

---

## Section 6: Performance and Optimization

### Question 25: Caching
**Task**: You need to perform multiple aggregations on `storesDF`. Write the code to:
1. Cache the dataframe
2. Perform 3 different aggregations
3. Unpersist when done

---

### Question 26: Partitioning
**Task**: Repartition `storesDF` by `division` with 4 partitions. Verify the partition count.

---

### Question 27: Coalesce vs Repartition
**Task**: `storesDF` currently has 100 partitions but only 1000 rows. Reduce it to 10 partitions using the most efficient method.

---

### Question 28: Broadcast Join
**Given**: `divisionsDF` with 5 rows (division, region, budget)

**Task**: Join `storesDF` with `divisionsDF` using a broadcast join.

---

## Section 7: Data Quality and Cleaning

### Question 29: Null Handling
**Task**: In `storesDF`, fill null values:
- `managerName` → "Unknown Manager"
- `customerSatisfaction` → division average
- `sqft` → 0

---

### Question 30: Duplicate Detection
**Task**: Find duplicate stores in `storesDF` based on `storeId`. Show the count of duplicates.

---

### Question 31: Data Validation
**Task**: Create a quality report for `storesDF` showing:
- Count of nulls per column
- Count of negative sqft values
- Count of customer satisfaction scores outside 0-5 range

---

### Question 32: Outlier Detection
**Task**: Find stores where `sqft` is more than 3 standard deviations from the mean.

---

## Section 8: Advanced Transformations

### Question 33: Pivot
**Task**: Create a pivot table showing count of stores by `division` (rows) and `size_category` (columns).

---

### Question 34: Unpivot/Melt
**Given**: DataFrame with columns: `storeId`, `sales_2023`, `sales_2024`, `sales_2025`

**Task**: Transform to long format: `storeId`, `year`, `sales`

---

### Question 35: Window Lag/Lead
**Task**: For each division in `storesDF`, add columns showing:
- Previous store's customer satisfaction (ordered by openDate)
- Next store's customer satisfaction (ordered by openDate)

---

### Question 36: Percentile Calculation
**Task**: Calculate the 25th, 50th, and 75th percentile of `sqft` for each division.

---

## Section 9: Complex Scenarios

### Question 37: Time Series Analysis
**Task**: For each month since January 2020, calculate:
- Number of stores opened (from openDate)
- Cumulative total stores
- Average sqft of stores opened that month

---

### Question 38: Manager Performance
**Task**: For each manager in `storesDF`, calculate:
- Number of stores managed
- Average customer satisfaction across their stores
- Total square footage managed
- Rank managers by average customer satisfaction

---

### Question 39: Division Comparison
**Task**: Create a comparison report showing:
- Division name
- Store count
- Average customer satisfaction
- Difference from overall company average satisfaction
- Rank by performance

---

### Question 40: Product Mix Analysis
**Task**: After exploding `productCategories`:
1. Find the most common product category
2. Find which division has the most diverse product mix (most unique categories)
3. Find product categories that appear in all divisions

---

## Section 10: SQL-Style Operations

### Question 41: SQL Query
**Task**: Register `storesDF` as a temp view and write a SQL query to find:
- Top 5 stores by customer satisfaction
- Include storeId, managerName, division, customerSatisfaction
- Filter to stores opened after 2021

---

### Question 42: Complex SQL Join
**Task**: Using SQL on temp views of `storesDF` and `acquiredStoresDF`:
- Find stores that were acquired within 1 year of opening
- Show acquisition details and store details

---

### Question 43: Subquery in SQL
**Task**: Write a SQL query to find stores where customer satisfaction is above the division average.

---

### Question 44: Union and Distinct
**Given**: `storesDF` and `closedStoresDF` with same schema

**Task**: Combine both dataframes and find all unique manager names across both.

---

## Section 11: Real-World Scenarios

### Question 45: Store Expansion Analysis
**Task**: Identify the best division for opening a new store based on:
- Highest average customer satisfaction
- Most consistent performance (lowest standard deviation)
- Has opened at least 5 stores

---

### Question 46: Manager Reassignment
**Task**: Find stores where:
- Customer satisfaction < 3.0
- Manager manages only 1 store
These stores need new managers assigned.

---

### Question 47: Seasonal Opening Patterns
**Task**: Analyze `openDate` to find:
- Which quarter (Q1-Q4) has the most store openings
- Which day of week is most common for openings
- Average customer satisfaction by opening quarter

---

### Question 48: Size vs Satisfaction
**Task**: Analyze the relationship between `sqft` and `customerSatisfaction`:
- Create size buckets (every 1000 sqft)
- Calculate average satisfaction per bucket
- Determine if there's a correlation

---

### Question 49: Data Pipeline
**Task**: Create a complete data pipeline that:
1. Reads `storesDF`
2. Filters to stores opened in last 2 years
3. Adds calculated columns (size category, years open)
4. Removes outliers (satisfaction < 1 or > 5)
5. Aggregates by division
6. Sorts by performance
7. Writes to parquet with partitioning by division

---

### Question 50: Comprehensive Report
**Task**: Create an executive summary report that shows:
- Total stores and average satisfaction by division
- Top 3 and bottom 3 stores by satisfaction
- Manager leaderboard (managers with multiple stores)
- Growth trend (stores opened per year)
- Product category distribution
- Stores requiring attention (satisfaction < 3.0)

---

## Bonus Challenge Questions

### Challenge 1: Dynamic Pivoting
**Task**: Create a dynamic pivot where column names are derived from unique values in `division`, and each cell shows average customer satisfaction for that division's product category.

---

### Challenge 2: Graph Analysis
**Task**: Consider managers who have worked at multiple stores over time. Model this as a graph and find:
- Managers with the longest career path
- Most common division transitions

---

### Challenge 3: Anomaly Detection
**Task**: Build an anomaly detection system that flags stores where:
- Customer satisfaction significantly deviates from similar stores (same division, similar size)
- Opening date patterns are unusual
- Product mix is significantly different from division norm

---

### Challenge 4: Optimization Problem
**Task**: You need to close 10% of stores. Create a scoring system that considers:
- Customer satisfaction (weight: 40%)
- Square footage cost (weight: 30%)
- Years in operation (weight: 20%)
- Product diversity (weight: 10%)

Identify which stores to close and why.

---

## Answer Template

For each question, structure your answer as:

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from pyspark.sql.window import Window

spark = SparkSession.builder.appName("Practice").getOrCreate()

# Your solution here

# Show results
result_df.show()
```

## Tips for Practice

1. **Start Simple**: Begin with Section 1 and progress sequentially
2. **Test Incrementally**: Run each transformation step-by-step
3. **Use explain()**: Check query plans for complex operations
4. **Verify Results**: Always validate output with .show() or .count()
5. **Optimize**: After getting correct results, think about performance
6. **Handle Nulls**: Always consider edge cases and null values
7. **Document**: Add comments explaining your approach

## Additional Resources

- Create sample data for testing using `spark.createDataFrame()`
- Use `.printSchema()` to understand data types
- Use `.describe()` for quick statistics
- Use `.explain()` to see physical execution plan
- Practice with different file formats (parquet, CSV, JSON)

Good luck with your practice! 🚀
