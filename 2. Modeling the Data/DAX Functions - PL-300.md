### `CALCULATE()` & `CALCULATABLE` functions

[CALCULATE function (DAX) - DAX | Microsoft Learn](https://learn.microsoft.com/en-us/dax/calculate-function-dax)
## Filter modification functions 

| Function              | Syntax                                  | What It Does                                                        | Behavior                                                                                             | When to Use It                                                                                                                                                                                                                                                                    |
| --------------------- | --------------------------------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`KEEPFILTERS()`**   | `KEEPFILTERS(<filter_expression>)`      | Adds a filter, return a boolean expressions                         | **INTERSECTS** the visual context AND the DAX filter.                                                | When a calculation should only apply if it aligns with the current visual context.<br>They:<br>- Cannot reference columns from multiple tables<br>- Cannot reference a measure<br>- Cannot use nested `CALCULATE` functions<br>- Cannot use functions that scan or return a table |
| **`ALL()`**           | `ALL(<table> or <column>, ...)`         | Removes all filters, return a table                                 | **IGNORES** the entire visual context on the specified table/column(s).                              | To calculate grand totals or percentages of a grand total.                                                                                                                                                                                                                        |
| **`ALLEXCEPT()`**     | `ALLEXCEPT(<table>, <column1>, ...)`    | Removes all but specified filters,  return a table                  | **REPSPECT** specific column filters while ignoring others on the same table.                        | To calculate percentages of a subtotal (e.g., % of parent category).                                                                                                                                                                                                              |
| **`ALLSELECTED()`**   | `ALLSELECTED(<table> or <column>, ...)` | Removes internal filters                                            | **IGNORES** the visual's internal context but **RESPECTS** external filters like slicers.            | To calculate percentages based on what the user has selected outside the visual.                                                                                                                                                                                                  |
| **`FILTER()`**        | `FILTER(<table>, <filter_expression>)`  | Iterates and applies a complex condition, return a table            | **RESPECTS** the existing context by default while evaluating a row-by-row condition.                | For filtering based on conditions that are too complex for a simple `column = value` argument or complex column comparison involves measure, other columns, `OR` operator                                                                                                         |
| **`REMOVEFILTERS()`** | `REMOVIEFILTERS(<table> or <column>)`   | Remove filters from one or more columns or all columns from a table | **IGNORES** existing filter context for the specified column or table, allowing full data evaluation | Use when you want to ignore slicers or visual filters on a column or table—especially useful for calculating totals, benchmarks, or comparisons unaffected by user selections                                                                                                     |

### **Example:**

|                           | Create a measure sale amount of Red product (with ```Sale Amount = SUM('Sales'[Amount])```) | Explanation                                                                                                                                                                  | A matrix visual of "Month" columns                                                                                                                            | A matrix visual of "Product Color" column                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Based formular            | ```CALCULATE([Sale Amount],'Product'[Color] = "Red")```                                     | The `CALCULATE` function modifies the context expression `[Sale Amount]`                                                                                                     | Return Sale amount of Red products for each month, month with no Red product sold will not appear or return blank.                                            | Return the same value of Red product sales **_for all rows_**.                                               |
| Using `FILTER` with `ALL` | ```CALCULATE([Sale Amount],FILTER(ALL('Product'),'Product'[Color] = "Red"))```              | `ALL` function inside `FILTER` removes any filters from `Product` table (columns `Color` ) and `FILTER` only choose the rows which `'Color' = "Red"` from the unfiltered set | Return Sale amount of Red products for each month, month with no Red product sold will not appear or return blank.                                            | Return the same value of Red product sales **_for all rows_**. `ALL` remove filters from the visual context. |
| Using `FILTER`            | ```CALCULATE([Sale Amount],FILTER('Product','Product'[Color] = "Red"))```                   | `FILTER` returns a table of only one row of "Red" and this context will intersect with the current visual context                                                            | Return Sale amount of Red products for each month, month with no Red product sold will not appear or return blank.                                            | Return **_only one_** row for "Red" color and its sale amount.                                               |
| Using `KEEPFILTERS`       | ```CALCULATE([Sale Amount],KEEPFILTERS('Product'[Color] = "Red"))```                        | `KEEPFILTERS` intersects the matrix visual context and the DAX filter (`'Color' = "Red"`)                                                                                    | Return Sale amount of Red products for each month, month with no Red product sold will not appear or return blank (if `Show items with no data` is selected). | Return **_only one_** row for "Red" color and its sale amount.                                               |
# 2. `RELATED()` vs. `LOOKUPVALUE()`
You should almost always use `RELATED()` when an active relationship exists between your tables, as it's simpler and performs better.
### **Core Difference**
The main difference is that **`RELATED()` requires a pre-existing, active relationship** between the tables in your data model, while **`LOOKUPVALUE()` does not**.
- **`RELATED()` 🤝:** Traverses an existing relationship to fetch a value from the "one" side. It's fast and efficient.
- **`LOOKUPVALUE()` 🔍:** Scans an entire column to find a matching value, much like `VLOOKUP` in Excel. It's more flexible but can be slower on large tables.

| Feature            | `RELATED()`                                                                                                               | `LOOKUPVALUE()`                                                                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Relationship**   | **Requires** an active, one-to-many relationship.                                                                         | Does **not** require a relationship.                                                                                                           |
| **Performance**    | Faster and more efficient.                                                                                                | Can be slower, especially on large tables.                                                                                                     |
| **Syntax**         | Simple: `RELATED(<column>)`                                                                                               | More complex: `LOOKUPVALUE(<result_column>, <search_column>, <search_value>)`                                                                  |
| **Direction**      | Only works from the "many" side to the "one" side.                                                                        | Can look up a value in any table, from any table.                                                                                              |
| **When to Use It** | ✅ **Your primary choice.** Use it whenever a relationship exists to bring columns from a dimension table to a fact table. | ⚠️ **Your fallback option.** Use it only when there is no relationship, to handle multiple lookup criteria, or for specific complex scenarios. |
### **Common use cases**
`RELATED()` is your primary tool for using columns from a dimension (the "one" side) in a calculated column or measure based on a fact table (the "many" side) and to mostly to create calculated columns where usually the other table's columns is ambiguous. 

|Use Case|DAX Formula Example|Explanation|
|---|---|---|
|**Conditional Logic (IF)**|`IF(RELATED('Product'[Category]) = "Bikes", [Sales Amount] * 0.1, 0)`|**Applies a 10% commission only to bike sales.** It retrieves the product category for each sales transaction and uses it in an `IF` statement.|
|**Text Concatenation**|`[Customer Name] & " (" & RELATED('Customer'[Country]) & ")"`|**Creates a new column combining customer name and country.** For example, "John Smith (USA)". It fetches the `Country` from the related Customer table.|
|**Math Operations**|`[Quantity] * RELATED('Product'[List Price])`|**Calculates the total list price for a sales line.** It multiplies the `Quantity` from the Sales table by the `List Price` from the related Product table.|
|**Grouping/Segmentation (SWITCH)**|`SWITCH(TRUE(), RELATED('Product'[Color]) = "Red", "Group A", RELATED('Product'[Color]) = "Blue", "Group B", "Other")`|**Categorizes sales into groups based on product color.** `RELATED()` brings the `Color` into the Sales table so `SWITCH` can evaluate it.|
|**Filtering in Measures (CALCULATE)**|`CALCULATE([Total Sales], RELATED('Product'[Category]) = "Bikes")`|This is a less common use in a measure, but it **calculates total sales, filtering the context to only include bikes.** Note: A direct filter like `'Product'[Category] = "Bikes"` is more standard.|
#### Common Use Cases for `LOOKUPVALUE()`
`LOOKUPVALUE()` is the fallback you use for the same scenarios when **no active relationship exists** between the tables. Notice the syntax is more complex as you have to manually define the lookup columns.

|Use Case|DAX Formula Example|Explanation|
|---|---|---|
|**Conditional Logic (IF)**|`IF(LOOKUPVALUE('Product'[Category], 'Product'[ProductKey], [ProductKey]) = "Bikes", [Sales Amount] * 0.1, 0)`|**Applies a 10% commission to bike sales without a relationship.** It manually searches for the `Category` in the Product table for each sale.|
|**Text Concatenation**|`[Customer Name] & " (" & LOOKUPVALUE('Customer'[Country], 'Customer'[CustKey], [CustomerKey]) & ")"`|**Combines customer name and country.** It looks up the `Country` based on the matching customer key in the unrelated Customer table.|
|**Math Operations**|`[Quantity] * LOOKUPVALUE('Product'[List Price], 'Product'[ProductKey], [ProductKey])`|**Calculates the total list price.** It finds the `List Price` from the Product table by matching the `ProductKey` from the Sales table.|
### **`RELATEDTABLE()`**
`RELATEDTABLE()` is a DAX function that follows a one-to-many relationship from the "one" side to the "many" side to retrieve a table of all the related rows.
Because it returns a table, `RELATEDTABLE()` is almost always used inside an iterator function like `COUNTX`, `SUMX`, `AVERAGEX`, etc., to perform an aggregation on the returned rows.
# 3. Time Functions

|Function|Purpose|Syntax|Example|
|---|---|---|---|
|**`EDATE`**|Returns a date that is a specified number of months **before or after** a start date.|`EDATE(<start_date>, <months>)`|`EDATE("2025-09-08", 3)` returns `2025-12-08`.|
|**`DATE`**|Creates a valid date from supplied year, month, and day integers.|`DATE(<year>, <month>, <day>)`|`DATE(2025, 9, 8)` returns the date `September 8, 2025`.|
|**`DATEVALUE`**|Converts a date formatted as **text** into a proper datetime format.|`DATEVALUE(<date_text>)`|`DATEVALUE("9/8/2025")` returns the date `September 8, 2025`.|
|**`EOMONTH`**|Returns the **last day of the month**, a specified number of months before or after a start date.|`EOMONTH(<start_date>, <months>)`|`EOMONTH("2025-09-08", 0)` returns `2025-09-30`.|
# 4. Time Series Functions 
### The #1 Prerequisite: A Proper Date Table
Time intelligence functions will **not work** without a well-formed **Date table**. Before you do anything else, you must have a table in your model that meets these criteria:
- It must have a column with a **date data type**.
- The date column must contain **unique values** (no duplicate dates).
- The date column must **not have any blank values**.
- It must contain a **full, continuous range of dates** (e.g., from January 1st to December 31st for every year in your data). There can be no missing days, even if you had no sales on those days.
- It must be marked as the **official Date table** in your model.
### **4.1. YTD, QTD, MTD Functions (Running Totals)**
These functions calculate a running total from the beginning of a period (year, quarter, or month) up to the current date in the filter context.

|Function|What It Does|Common DAX Pattern|
|---|---|---|
|**`TOTALYTD`**|Calculates the Year-to-Date value of an expression.|`Sales YTD = TOTALYTD(SUM(Sales[Sales Amount]), 'Date'[Date])`|
|**`TOTALQTD`**|Calculates the Quarter-to-Date value.|`Sales QTD = TOTALQTD(SUM(Sales[Sales Amount]), 'Date'[Date])`|
|**`TOTALMTD`**|Calculates the Month-to-Date value.|`Sales MTD = TOTALMTD(SUM(Sales[Sales Amount]), 'Date'[Date])`|

**Real-Life Use:** In a table showing sales by month, the "Sales YTD" measure for March would show the sum of sales from January, February, and March. For April, it would show the sum from January through April.
### **4.2. Period-over-Period Comparisons**
These are the most common time intelligence functions. They shift the date context to a previous period to allow for comparisons, such as this year's sales versus last year's.

|Function|What It Does|Common DAX Pattern|
|---|---|---|
|**`SAMEPERIODLASTYEAR`**|Returns a table of dates shifted back exactly one year.|`Sales Last Year = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))`|
|**`DATEADD`**|Returns a table of dates shifted by a specified interval (day, month, quarter, year).|`Sales Previous Month = CALCULATE([Total Sales], DATEADD('Date'[Date], -1, MONTH))`|
|**`PARALLELPERIOD`**|Returns a table of dates that is parallel to the current context, shifted by an interval.|`Sales Last Year (Parallel) = CALCULATE([Total Sales], PARALLELPERIOD('Date'[Date], -1, YEAR))`|
### **4.3. Date Aggregations & Filters**
These functions are often used inside `CALCULATE` to create custom date filters or are used as helper functions inside other measures.

| Function                              | What It Does                                                                                                                             | Common DAX Pattern                                                                                                                            |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **`DATESBETWEEN`**                    | Returns a table containing a column of dates between a start and end date.                                                               | `Sales Last 30 Days = CALCULATE([Total Sales], DATESBETWEEN('Date'[Date], TODAY() - 30, TODAY()))`                                            |
| **`DATESINPERIOD`**                   | Returns a table that contains a column of dates that begins with a given start date and continues for the specified number of intervals. | `Sales Last 30 Days = CALCULATE( SUM(Sales[Amount]), DATESINPERIOD('Date'[Date], TODAY(), -30, DAY))<br>                                      |
| **`STARTOFMONTH`** / **`ENDOFMONTH`** | Returns the first or last date of the month in the current context.                                                                      | `Sales on Last Day of Month = CALCULATE([Total Sales], ENDOFMONTH('Date'[Date]))`                                                             |
| **`FIRSTDATE`** / **`LASTDATE`**      | Returns the first or last date in the current context.                                                                                   | Often used inside `DATESBETWEEN` or other functions to define a dynamic date range.                                                           |
| **`DATESYTD`**                        | Returns a single-column table that contains dates fir the YTD in the current filter context                                              | Fiscal year-to-date sales  (fiscal year ends at June 30th)<br>`Fiscal YTD Sale = CALCULATE(SUM('Sale'[Amount]),DATESYTD('Date'[Date],"6/30")` |


### **4.4`PREVIOUS` Functions vs. Other Time Intelligence Functions**
The key difference between the `PREVIOUS...` functions and functions like `SAMEPERIODLASTYEAR` or `DATEADD` is how they handle a partial period selection.
- **`PREVIOUS...` functions:** Always return the **entire** immediately preceding period.
- **`SAMEPERIODLASTYEAR` / `DATEADD`:** Return an **equivalent range** of dates shifted back.

| Function                 | Outcome Type | Behavior in a Partial Period Context (e.g., March 10-20)                              | When to Use It                                                                        |
| ------------------------ | ------------ | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **`PREVIOUSYEAR`**       | **Table**    | Returns the **entire previous year** (e.g., all of 2024).                             | When you need to compare a period to the entirety of the prior year.                  |
| **`PREVIOUSQUARTER`**    | **Table**    | Returns the **entire previous quarter** (e.g., all of Q4 2024).                       | When you need to compare a period to the entirety of the prior quarter.               |
| **`PREVIOUSMONTH`**      | **Table**    | Returns the **entire previous month** (e.g., all of February 2025).                   | When you need to compare a period to the entirety of the prior month.                 |
| **`SAMEPERIODLASTYEAR`** | **Table**    | Returns the **exact same date range**, one year prior (e.g., March 10-20, 2024).      | For standard year-over-year (YoY) comparisons.                                        |
| **`DATEADD`**            | **Table**    | Returns an **equivalent date range**, shifted by an interval (e.g., Feb 10-20, 2025). | For flexible period-over-period comparisons (e.g., vs. last month, vs. 3 months ago). |
### **Best Practices**
- **`CALCULATE` is Your Best Friend:** Almost all time intelligence calculations involve `CALCULATE`. The time intelligence function (e.g., `SAMEPERIODLASTYEAR`) acts as a filter argument that modifies the date context for the calculation
- **Implicit vs. Explicit Measures:** Functions like `TOTALYTD` are "syntactic sugar" – they are a convenient shorthand. The longhand version is `CALCULATE([Total Sales], DATESYTD('Date'[Date]))`. Understanding this helps you see that these functions are just special filters.
- **Handling Incomplete Periods:** When comparing a partial period (like the current month-to-date) to a full prior period, your numbers can be misleading. A common pattern is to only show prior period values up to the same point in time.

# 5. Ranking and Top/Bottom Values

| Function / Pattern                 | Purpose                                                                                           | Syntax                                                    | Returns                                 | Common Use Case / Example                                                                                                                                                                                                 |
| ---------------------------------- | ------------------------------------------------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`RANKX`**                        | To calculate the rank for each row in a table based on an expression.                             | `RANKX(<table>, <expression>, [value], [order], [ties])`  | Scalar (the rank number, e.g., 1, 2, 3) | **To create a rank measure for a visual:** Create a measure that ranks each product based on its total sales. <br> `Product Rank = RANKX(ALLSELECTED('Product'), [Total Sales])`                                          |
| **`TOPN`**                         | To return a table containing the top or bottom N rows from another table, based on an expression. | `TOPN(<n_value>, <table>, <orderBy_expression>, [order])` | Table                                   | **To calculate a measure for a subset of data:** Calculate the total sales generated by only the top 10 customers. <br> `Sales of Top 10 Customers = CALCULATE([Total Sales], TOPN(10, 'Customer', [Total Sales], DESC))` |
| **`MAXX` / `MINX`**                | To iterate through a table and find the single highest (or lowest) value of an expression.        | `MAXX(<table>, <expression>)`                             | Scalar (the single top/bottom value)    | **To find the single best or worst performance:** Find the value of the highest-selling day in the selected period. <br> `Highest Daily Sales = MAXX(VALUES('Date'[Date]), [Total Sales])`                                |
| **Get Name of Top Item (Pattern)** | To retrieve a text attribute (like a name) of the top-ranked item, not just its value.            | `CALCULATE(SELECTEDVALUE(<name_column>), TOPN(1, ...))`   | Scalar (the name of the top item)       | **To display the name of the top performer in a card visual:** <br> `Top Selling Product = CALCULATE(SELECTEDVALUE('Product'[Product Name]), TOPN(1, 'Product', [Total Sales], DESC))`                                    |
# 6. Examine Filter Context 
```DAX
VALUES(<TableNameOrColumnName>)
```
- When you pass in a table reference, it returns a table object with the same columns that contain rows for what's in filter context. 
- When you pass in a column reference, it returns a single-column table of unique values that are in filter context.

| Function              | Syntax                                           | What It Does (Outcome)                                                                  | Behavior                                                                                            | When to Use It                                                                                                                                                    |
| --------------------- | ------------------------------------------------ | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`VALUES()`**        | `VALUES(<TableNameOrColumnName>)`                | Returns a table of unique values in filter context (column) or filtered rows (table)    | Always returns a table object; reflects current filter context                                      | Use to retrieve distinct values or rows currently in filter context—ideal for dynamic filtering, iteration, or conditional logic                                  |
| **`HASONEVALUE()`**   | `HASONEVALUE(<ColumnName>)`                      | Returns `TRUE` if the column is filtered to a single value                              | Evaluates whether `VALUES()` returns exactly one row                                                | Use when you need to check if a slicer or visual has narrowed a column to one value—often used in conditional formatting or branching logic                       |
| **`SELECTEDVALUE()`** | `SELECTEDVALUE(<ColumnName>, <AlternateResult>)` | Returns the single value in filter context, or BLANK/alternate if multiple values exist | Simplifies extraction of a single value from filter context; avoids errors from multiple selections | Use when you want to display or calculate based on a single selected value—especially useful in titles, labels, or dynamic measures that depend on user selection |
# 7. Aggregation and Statistical

### 1. Aggregation Functions

These are the most common DAX functions, used to summarize the data in a column into a single value. They are the building blocks of most measures.

|Function|What It Does|Example Usage|
|---|---|---|
|**`SUM`**|Adds up all the numbers in a column.|`Total Sales = SUM(Sales[SalesAmount])`|
|**`AVERAGE`**|Calculates the average (arithmetic mean) of all numbers in a column.|`Avg Price = AVERAGE(Sales[UnitPrice])`|
|**`MIN`**|Finds the smallest numeric value in a column.|`Lowest Price = MIN(Product[ListPrice])`|
|**`MAX`**|Finds the largest numeric value in a column.|`Highest Price = MAX(Product[ListPrice])`|
|**`COUNT`**|Counts the number of cells in a column that contain a number, text, or date (non-blank).|`Number of Sales = COUNT(Sales[SalesOrderNumber])`|
|**`DISTINCTCOUNT`**|Counts the number of **unique** (distinct) values in a column.|`Unique Customers = DISTINCTCOUNT(Sales[CustomerKey])`|
|**`COUNTROWS`**|Counts the total number of rows in a table.|`Total Transactions = COUNTROWS(Sales)`|
|**`COUNTBLANK`**|Counts the number of blank cells in a column.|`Missing Emails = COUNTBLANK(Customer[EmailAddress])`|

Export to Sheets

**Note on "X" Functions:** Most aggregation functions have an iterator version ending in "X" (e.g., `SUMX`, `AVERAGEX`, `COUNTX`). These versions perform a calculation for **each row** of a table and then aggregate the results. They are more powerful and are used for more complex, row-level calculations.

### 2. Statistical Functions

These functions go beyond simple summaries to perform more advanced statistical analysis, such as finding the median, ranking values, or calculating variance.

| Function      | What It Does                                                                                                                   | Example Usage                                                             |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| **`MEDIAN`**  | Finds the median (the middle value) of the numbers in a column. It's less affected by outliers than `AVERAGE`.                 | `Median Income = MEDIAN(Demographics[AnnualIncome])`                      |
| **`MEDIANX`** | The iterator version of `MEDIAN`. It evaluates an expression for each row of a table and then finds the median of the results. | `Median Order Total = MEDIANX(Sales, Sales[Quantity] * Sales[UnitPrice])` |
| **`RANKX`**   | Returns the ranking of a value within a list. This is the primary function for ranking items.                                  | `Product Sales Rank = RANKX(ALL(Product), [Total Sales])`                 |
| **`STDEV.P`** | Calculates the standard deviation of an entire population. Measures how spread out the values are from the average.            | `StDev of Product Price = STDEV.P(Product[ListPrice])`                    |
| **`VAR.S`**   | Estimates the variance based on a sample of a population.                                                                      | `Sample Variance of Test Scores = VAR.S(ExamResults[Score])`              |
# 8. Addictive / Semi-addictive functions 
| **Function**              | **Purpose**                                                                                                     | **Syntax**                                   | **Example (Use Case & Formula)**                                                                                                                                                                                                                                                                                                          |
| ------------------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`LASTNONBLANK`**        | Returns a table with the **last date that has a non-blank value** for an expression.                            | `LASTNONBLANK(<dates>, <expression>)`        | **Use Case:** To find the closing inventory balance at the end of any period (month, quarter, year). This is the **correct function for most semi-additive measures**. **Formula:** `Closing Balance = CALCULATE([Inventory Count], LASTNONBLANK('Date'[Date], [Inventory Count]))`                                                       |
| **`FIRSTNONBLANK`**       | Returns a table with the **first date that has a non-blank value** for an expression.                           | `FIRSTNONBLANK(<dates>, <expression>)`       | **Use Case:** To find the opening employee headcount at the beginning of any period. **Formula:** `Opening Headcount = CALCULATE([Headcount], FIRSTNONBLANK('Date'[Date], [Headcount]))`                                                                                                                                                  |
| **`LASTDATE`**            | Returns a table with the **last calendar day** in the current context, regardless of whether that day has data. | `LASTDATE(<dates>)`                          | **Use Case:** To get a value specifically on the last calendar day of a period. <br>**⚠️ Warning:** This will return BLANK if there's no data on that specific last day (e.g., a weekend), making it unsuitable for most semi-additive measures. <br> ```Value on Last Calendar Day = CALCULATE([Total Sales], LASTDATE('Date'[Date]))``` |
| **`FIRSTDATE`**           | Returns a table with the **first calendar day** in the current context.                                         | `FIRSTDATE(<dates>)`                         | **Use Case:** To get a value specifically on the first calendar day of a period. <br>```Value on First Calendar Day = CALCULATE([Total Sales], FIRSTDATE('Date'[Date]))```                                                                                                                                                                |
| **`CLOSINGBALANCEMONTH`** | A specialized function that evaluates an expression at the **last calendar day of the month**.                  | `CLOSINGBALANCEMONTH(<expression>, <dates>)` | **Use Case:** A simpler way to get the end-of-month bank account balance, but it has the same limitation as `LASTDATE`. **Formula:** `EOM Account Balance = CLOSINGBALANCEMONTH(SUM(Accounts[Balance]), 'Date'[Date])`                                                                                                                    |
| **`OPENINGBALANCEMONTH`** | A specialized function that evaluates an expression at the **first calendar day of the month**.                 | `OPENINGBALANCEMONTH(<expression>, <dates>)` | **Use Case:** To get the beginning-of-month bank account balance. **Formula:** `BOM Account Balance = OPENINGBALANCEMONTH(SUM(Accounts[Balance]), 'Date'[Date])`                                                                                                                                                                          |
**Note:** The `CLOSINGBALANCE...` and `OPENINGBALANCE...` functions also have `...QUARTER` and `...YEAR` versions (e.g., `CLOSINGBALANCEYEAR`) that work in the same way for their respective time periods.
# 9. PATH DAX functions 
A parent-child hierarchy is a way of representing a hierarchy in a single table, where each row has a key and a reference to its parent's key. A common example is an `Employee` table with an `EmployeeKey` and a `ManagerKey`. While this is efficient for storage, it's difficult for DAX to analyze. The goal is to "flatten" this into a standard table with a fixed number of columns representing each level of the hierarchy (e.g., `Level 1`, `Level 2`, `Level 3`, etc.).

The primary DAX functions for this are the **PATH** functions.

---
## 1. The Key Functions: `PATH`, `PATHITEM`, and `LOOKUPVALUE`

| Function           | What It Does                                                                                | Syntax                                                          | Outcome                                                      |
| ------------------ | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------ |
| **`PATH`**         | Creates a delimited text string of all the parents for the current row.                     | `PATH(<ID_column>, <parent_ID_column>)`                         | A **scalar** text value (e.g., "1)                           |
| **`PATHITEM`**     | Extracts a specific item from a `PATH` string.                                              | `PATHITEM(<path>, <position>, [<type>])`                        | A **scalar** value (the key of the parent at that position). |
| **`PATHCONTAINS`** | Return a boolean to check if a item exists within a path string                             | `PATHCONTAINS(<Path_Expression>, <Item_To_Find>)`               | A **boolean** value **True/False**                           |
| **`LOOKUPVALUE`**  | Fetches a value from another table where columns match.                                     | `LOOKUPVALUE(<result_column>, <search_column>, <search_value>)` | A **scalar** value (the name or attribute you want).         |
| **`PATHLENGTH`**   | Returns the number of parents to the specified item in a given PATH result, including self. | `PATHLENGTH(<path>)`                                            | A **scalar** value                                           |

---
## 2. How to Flatten a Parent-Child Hierarchy (Step-by-Step)

Let's use an `Employee` table as our example.
**Source Table (`Employee`):** 

| EmployeeKey | EmployeeName   | ManagerKey |
|-------------|----------------|------------|
| 10          | CEO            | (blank)    |
| 20          | VP Sales       | 10         |
| 30          | Sales Manager  | 20         |
| 40          | Salesperson    | 30         |
### Step 1: Create the Path

First, you create a calculated column that builds the hierarchy path for each employee. This path is the "map" of the hierarchy from the top level down to the current employee.
Code snippet

```DAX
Path = PATH('Employee'[EmployeeKey], 'Employee'[ManagerKey])
```

**Outcome (`Employee` table with `Path` column):**

| EmployeeKey | EmployeeName  | ManagerKey | Path        |
| ----------- | ------------- | ---------- | ----------- |
| 10          | CEO           | (blank)    | 10          |
| 20          | VP Sales      | 10         | 10-20       |
| 30          | Sales Manager | 20         | 10-20-30    |
| 40          | Salesperson   | 30         | 10-20-30-40 |
### Step 2: Extract Each Level's Key

Next, you create a new calculated column for each level of the hierarchy you want to flatten. `PATHITEM` is used to pull the key from the `Path` string at each position.

- **Level 1 (the CEO):**
    Code snippet
``` DAX
 Level 1 Key = PATHITEM([Path], 1)
```
- **Level 2 (the VP):**
    Code snippet
```DAX
Level 2 Key = PATHITEM([Path], 2)
```

- ...and so on for as many levels as you need.

**Outcome (`Employee` table with `Level Key` columns):** 

| EmployeeKey | Path           | Level 1 Key | Level 2 Key | Level 3 Key |
|-------------|----------------|-------------|-------------|-------------|
| 10          | 10             | 10          | (blank)     | (blank)     |
| 20          | 10-20          | 10          | 20          | (blank)     |
| 30          | 10-20-30       | 10          | 20          | 30          |
| 40          | 10-20-30-40    | 10          | 20          | 30          |
### Step 3: Look Up the Name for Each Level

The `Level Key` columns only give you the ID. The final step is to use `LOOKUPVALUE` to fetch the actual employee name for each of those keys.

```DAX
Level 1 Name = LOOKUPVALUE('Employee'[EmployeeName], 'Employee'[EmployeeKey], [Level 1 Key])
Level 2 Name = LOOKUPVALUE('Employee'[EmployeeName], 'Employee'[EmployeeKey], [Level 2 Key])
```
**Final Flattened Table:** 

| EmployeeName   | Level 1 Name | Level 2 Name | Level 3 Name |
|----------------|--------------|--------------|--------------|
| CEO            | CEO          | (blank)      | (blank)      |
| VP Sales       | CEO          | VP Sales     | (blank)      |
| Sales Manager  | CEO          | VP Sales     | Sales Manager|
| Salesperson    | CEO          | VP Sales     | Sales Manager|

This final table is now a standard, flattened hierarchy that is easy to use in visuals, slicers, and DAX measures.

---
## 3. Other Examples

This pattern is useful for any data structured as a parent-child hierarchy:
- **Chart of Accounts:** Where an account rolls up to a parent account.
- **Product Categories:** Where a subcategory belongs to a parent category.
- **Organizational Structures:** Where a business unit belongs to a larger division.
---
## 4. `EXCEPT()` and `CROSSJOIN`

While `EXCEPT` and `CROSSJOIN` are not used in the process of _creating_ the flattened hierarchy (that's the job of `PATH` and `PATHITEM`), they can be powerful tools for **analyzing the flattened hierarchy** once it's built.
### Using `EXCEPT` with a Flattened Hierarchy
You can use `EXCEPT` to find members of the hierarchy that belong to one group but not another.

| Function        | What It Does                                                                                                                       | Syntax                                 | Outcome                                                                        |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | ------------------------------------------------------------------------------ |
| **`EXCEPT`**    | Find the difference between two lists by returning a table of rows from the first table that do **not** appear in the second table | `PATH(<ID_column>, <parent_ID_column>` | A **table** with excluded values from another table                            |
| **`CROSSJOIN`** | Return the **Cartesian product** of all rows from two or more tables provided                                                      | `CROSSJOIN(<table1>, <table2>, ...)`   | A new **table** with every possible combination of rows from the input tables. |
##### Use Case: Find All Mid-Level Managers
Let's say you want a list of all managers who are **not** at the top level (i.e., they are not the CEO). Using the flattened `Employee` table from our previous example, you can achieve this.
**Flattened `Employee` Table (for reference):** 

| EmployeeName   | Level 1 Name | Level 2 Name |
|----------------|--------------|--------------|
| CEO            | CEO          | (blank)      |
| VP Sales       | CEO          | VP Sales     |
| Sales Manager  | CEO          | VP Sales     |

**DAX Formula:**
```DAX
Mid-Level Managers =
-- Step 1: Get a table of all managers (anyone who is in Level 1 or Level 2)
VAR AllManagers =
    UNION (
        VALUES ( 'Employee'[Level 1 Name] ),
        VALUES ( 'Employee'[Level 2 Name] )
    )

-- Step 2: Get a table of only the top-level managers
VAR TopLevelManagers = VALUES ( 'Employee'[Level 1 Name] )

-- Step 3: Subtract the top-level managers from the list of all managers
RETURN
    EXCEPT ( AllManagers, TopLevelManagers )
```

**Outcome:** This formula returns a table containing only the names of managers who are not at the very top of the hierarchy (e.g., "VP Sales" and "Sales Manager").

---
### Using `CROSSJOIN` with a Flattened Hierarchy
You can use `CROSSJOIN` to create a complete and exhaustive combination of hierarchy levels and members, which is useful for ensuring your reports show all possibilities, even those with no data.
##### Use Case: Create a Matrix of All Employees Under All Departments
Imagine you want to create a matrix visual that shows every single employee on the rows and every top-level department (represented by the Level 2 managers, the VPs) on the columns. If you just use the natural hierarchy, an employee will only show up under their own department. `CROSSJOIN` can create a table that has a row for every possible combination.

**DAX Formula:**

```DAX
Employee-Department Scaffold =
CROSSJOIN (
    VALUES ( 'Employee'[Level 2 Name] ), -- A list of all unique departments (VPs)
    VALUES ( 'Employee'[EmployeeName] )   -- A list of all unique employees
)
```

**Outcome:** This creates a "scaffold" or "template" table with every possible combination of an employee and a department.

|Level 2 Name|EmployeeName|
|---|---|
|VP Sales|CEO|
|VP Sales|VP Sales|
|VP Sales|Sales Manager|
|VP Sales|Salesperson|
|_(...and so on for every other department/VP)_|_(...)_|

==This scaffold table can be used in a matrix visual and create a measure that checks if an employee actually belongs to that department.== This guarantees that every employee and every department appears in the matrix, even if the value is zero, which is something the natural hierarchy might hide.
# 10. `SUMMARIZE` functions
[SUMMARIZE function (DAX) - DAX | Microsoft Learn](https://learn.microsoft.com/en-us/dax/summarize-function-dax)
[GROUPBY function (DAX) - DAX | Microsoft Learn](https://learn.microsoft.com/en-us/dax/groupby-function-dax)
Both `SUMMARIZE` and `GROUPBY` are powerful DAX functions used to create summary tables by grouping rows based on specified columns and performing aggregations. However, they have key differences in how they perform calculations and their primary use cases.
### Comparison Table

| **Feature**              | **SUMMARIZE**                                                                                                                                                                | **GROUPBY**                                                                                                                                                                                                                                                                     |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Primary Purpose**      | To create a **summary table** by grouping rows and calculating aggregated values.                                                                                            | Similar to `SUMMARIZE`, but primarily used to perform aggregations over **intermediate results** from DAX table expressions. Optimized for multiple aggregations in a single scan.                                                                                              |
| **Syntax**               | `SUMMARIZE(<table>, <groupBy_columnName>..., [<name>, <expression>]...)`                                                                                                     | `GROUPBY(<table>, <groupBy_columnName>..., [<name>, <X_aggregator_expression>]...)`                                                                                                                                                                                             |
| **Aggregation Behavior** | Performs an **implicit `CALCULATE`** for each `<expression>`. This means the expression is evaluated in a context where the table is filtered by the current group's values. | **Does NOT perform an implicit `CALCULATE`**. The `<expression>` must explicitly use an **iterator function** (like `SUMX`, `AVERAGEX`, `MAXX`) combined with the special **`CURRENTGROUP()`** function to define the aggregation over the rows belonging to the current group. |
| **Return Value**         | Table                                                                                                                                                                        | Table                                                                                                                                                                                                                                                                           |
| **Example Use Case**     | Create a table summarizing total `Sales Amount` and `Discount Amount` grouped by `Calendar Year` and `Product Category`.                                                     | Find the `Maximum Sales` within each `Country`, using an intermediate table (`SalesByCountryAndCategory`) as input.                                                                                                                                                             |
| **Example Formula**      | ```SUMMARIZE( Sales, 'Date'[Year], Product[Category], "Total Sales", SUM(Sales[Sales Amount]) )<br>```                                                                       | ```GROUPBY( SalesSummary, Geography[Country], "Max Sales", MAXX(CURRENTGROUP(), [Total Sales]) )```                                                                                                                                                                             |
| **DirectQuery Support**  | Not supported in calculated columns or RLS rules.                                                                                                                            | Not supported in calculated columns or RLS rules.                                                                                                                                                                                                                               |
## `ROLLUP`-Related Functions (Used within `SUMMARIZE`)

These functions modify the behavior of `SUMMARIZE` by adding subtotal and grand total rows or by identifying which rows are subtotals. They can only be used within the `groupBy_columnName` arguments of a `SUMMARIZE` expression.

| **Function**              | **Purpose**                                                                                                                                                                         | **Syntax Context**                                                                          | **Example**                                                                                                                                                                                                                                           |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`ROLLUP`**              | Adds **subtotal and grand total rows** to the output table based on the specified group-by columns.                                                                                 | `SUMMARIZE(<table>, ROLLUP(<groupBy_col1>, <groupBy_col2>...), ...)`                        | Get Sales by Year and Category, with subtotals for each Year and a grand total. <br>```SUMMARIZE( Sales, ROLLUP( 'Date'[Year], Product[Category] ), "Total Sales", SUM(Sales[Sales Amount]) )```                                                      |
| **`ROLLUPGROUP`**         | Used **inside `ROLLUP`** to prevent partial subtotals from being generated for the columns within it. It groups columns together so subtotals are only created _outside_ the group. | `SUMMARIZE(<table>, ROLLUP(ROLLUPGROUP(<groupBy_col1>, <groupBy_col2>...)), ...)`           | Get Sales by Year and Category, but ONLY show the grand total, NOT subtotals for each year. <br>`SUMMARIZE( Sales, ROLLUP(ROLLUPGROUP( 'Date'[Year], Product[Category] )), "Total Sales", SUM(Sales[Sales Amount]))`                                  |
| **`ISSUBTOTAL`**          | Creates a **new boolean column** in the `SUMMARIZE` output that returns `TRUE` if the row represents a subtotal for the specified column, and `FALSE` otherwise.                    | `SUMMARIZE(<table>, ROLLUP(...), ..., "Subtotal Flag", ISSUBTOTAL(<groupBy_col_to_check>))` | Get Sales by Year and Category, -- add subtotals, -- and add a column to flag Year subtotals. <br>`SUMMARIZE( Sales, ROLLUP( 'Date'[Year], Product[Category] ), "Total Sales", SUM(Sales[Sales Amount]), "IsYearSubtotal", ISSUBTOTAL('Date'[Year]))` |
| **`ROLLUPADDISSUBTOTAL`** | Similar to `ROLLUP`, but **automatically adds** an `ISSUBTOTAL` boolean column for each group-by column included.                                                                   | `SUMMARIZE(<table>, ROLLUPADDISSUBTOTAL(<groupBy_col1>, <groupBy_col2>...), ...)`           |                                                                                                                                                                                                                                                       |

**Note:** The functions `ROLLUPADDISSUBTOTAL` and `ROLLUPISSUBTOTAL` are less commonly documented and used compared to `ROLLUP`, `ROLLUPGROUP`, and `ISSUBTOTAL`. They provide more granular control over subtotal behavior but are often superseded by the simpler combination of `ROLLUP` and `ISSUBTOTAL`.