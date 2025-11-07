A parent-child hierarchy is a way of representing a hierarchy in a single table, where each row has a key and a reference to its parent's key. A common example is an `Employee` table with an `EmployeeKey` and a `ManagerKey`. While this is efficient for storage, it's difficult for DAX to analyze. The goal is to "flatten" this into a standard table with a fixed number of columns representing each level of the hierarchy (e.g., `Level 1`, `Level 2`, `Level 3`, etc.).

The primary DAX functions for this are the **PATH** functions.

---
## 1. The Key Functions: `PATH`, `PATHITEM`, and `LOOKUPVALUE`

| Function              | What It Does                                                                                  | Syntax                                                          | Outcome                                                              |
| --------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------- | -------------------------------------------------------------------- |
| **`PATH`**            | Creates a delimited text string of all the parents for the current row.                       | `PATH(<ID_column>, <parent_ID_column>)`                         | A **scalar** text value (e.g., "1)                                   |
| **`PATHITEM`**        | Extracts a specific item from a `PATH` string.                                                | `PATHITEM(<path>, <position>, [<type>])`                        | A **scalar** value (the key of the parent at that position).         |
| **`PATHITEMREVERSE`** | Extracts a specific item from a `PATH` string backward (the highest hierarchy is marked as 1) | `PATHITEMREVERSE(<path>, <position>, [<type>])`                 | A **scalar** value (the key of the parent at that reversed position) |
| **`PATHCONTAINS`**    | Return a boolean to check if a item exists within a path string                               | `PATHCONTAINS(<Path_Expression>, <Item_To_Find>)`               | A **boolean** value **True/False**                                   |
| **`LOOKUPVALUE`**     | Fetches a value from another table where columns match.                                       | `LOOKUPVALUE(<result_column>, <search_column>, <search_value>)` | A **scalar** value (the name or attribute you want).                 |

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

- **Level 1 Name:**
    Code snippet
```DAX
Level 1 Name = LOOKUPVALUE('Employee'[EmployeeName], 'Employee'[EmployeeKey], [Level 1 Key])
```
- **Level 2 Name:**
    Code snippet
```DAX
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