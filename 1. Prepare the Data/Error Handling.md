## Prepare The Data 
### Common Power BI Data Import Errors

|Error Message|When It Happens / Reason|Solution|
|---|---|---|
|**"Query timeout expired"** ⏳|Your query to a relational database (like SQL Server) is taking too long to run and exceeds the time limit set by the administrator. This is usually caused by requesting too much data or running a very complex query.|**Reduce the amount of data** you are importing by filtering rows and columns as early as possible in Power Query or in a native SQL statement. You can also import data in smaller chunks and merge them in Power Query.|
|**"We couldn't find any data formatted as a table"** 📋|You are importing from an Excel file where the data is in a simple range of cells and has **not been formatted as an official Excel Table**.|Open the Excel file, select your data range, and press **Ctrl+T** to format it as a table. Then, re-import the file into Power BI.|
|**"Couldn't find file"** 📁|The source file (like an Excel or CSV file) has been **moved to a new location, renamed**, or your permissions to access the file have been changed.|In the Power Query Editor, select the query with the error, click the gear icon (⚙️) next to the **Source** step in the "Applied Steps" pane, and **update the file path** to the new location.|
|**Data type errors** 🔢 (Often appear as blank columns)|Power BI fails to correctly interpret the data type of a column from the source. This commonly happens when a column contains a mix of text and numbers, but you've tried to set its type to a whole number.|The best solution is to **fix the data type at the source**. If using SQL, use a `CAST` or `CONVERT` function in your query to explicitly define the column's data type (e.g., as `varchar`) before it is imported into Power BI.|
#### Unstable Data types
[Exception Reporting in Power BI: Catch the Error Rows in Power Query - RADACAD](https://radacad.com/exception-reporting-in-power-bi-catch-the-error-rows-in-power-query/)
When you refresh your data, new rows are added. If a new row contains a value that doesn't match the data type you've set for a column (e.g., text like "Pending" appears in a column you've set as a `Whole Number`), the entire refresh for that query can fail, or those specific rows will turn into errors.
The solution is to create an **exception reporting** system directly within Power Query. This process splits your original query into two separate paths: one for the clean data and one for the errors. 
##### Step 1: Create two Referenced Queries (The First Step)
Start with your main query after you have applied the transformation step that might cause an error (e.g., the **Changed Type** step).
1. In the Queries pane, **right-click** your main query (e.g., `Sales Data`).
2. Select **Reference**. A new query will be created.
3. Rename this new query to `Valid Rows` - this is the new table that would be cleaned with no errors and loaded to the report.
4. **Right-click** the original main query (`Sales Data`) again and create a second **Reference**.
5. Rename this second new query to `Error Rows`.
##### Step 2: Remove Errors from table `Valid Rows`
Configure the `Valid Rows` query to only keep the clean data.
1. Select the `Valid Rows` query.
2. Select the column that contains potential errors.
3. Go to the **Home** tab, click the **Remove Rows** dropdown, and select **Remove Errors**.
"**Remove Errors**" will be a step in the data transformation steps and when the data type change causes an error, the next step after will be "Remove Errors". But the original table `Error Rows` still contained error rows, therefore, we need to uncheck Enable Load. 
You now have a base query and two new queries that depend on its output.
##### Step 3: Add a Step to Catch Errors in the Exception Table (`Error Rows`) Before They Happen
The key is to check for errors _before_ the "Changed Type" step that might fail.
1. Click on the `Error Rows` query to choose this table 
2. Go to the **Add Column** tab and select **Custom Column**.
3. Create a column to check for errors using the ==`try...otherwise`== expression. This attempts a transformation and lets you define what happens if it fails.
``` M
// Custom column formula
= try Number.From([Value]) 
```

- **`try Number.From([Value])`**: Power Query attempts to convert the `Value` column to a number for each row. The `try` keyword return a record containing the error details (e.g. `HasError`, `Error`).
- **`otherwise "Error"`**: If the conversion fails (e.g., because the value is text), it will place the word "Error" in this new custom column instead of failing the whole step.
4. The newly created `Custom` column will contain Record which have two fields `HasError` (which most likely be `TRUE`) and `Error`. Click on Expand on this column.
5. In the output column named Error, click on Expand again and Select all columns in the drop-down list. Keep the "Use original column name as prefix" option enabled.
##### Step 4: Remove the column that contains errors - `Value` from this `Error Rows` query.
##### Optional Step: Exception Report
 `Error Rows` is the table that you can use for exception reporting. The exception report is the report that can be used for troubleshooting and will list all the errors to users for further investigation. Make sure that there is no relationship between these two tables.
### Error Handling in Power Query
#### 1. Step-Level Errors
A **step-level error** stops the entire query from loading and displays the error message in a yellow pane. You should analyze the **error reason**, **error message**, and **error detail** to understand the cause.

| Error Reason / Message                                                     | Common Cause                                                                                                                                    | Solution                                                                                                                                                                             |
| -------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **`DataSource.Error`** or **`DataSource.NotFound`** ("Couldn't find file") | The data source has been moved, renamed, is inaccessible, or you don't have the correct credentials.                                            | In the Query Settings pane, click the gear icon (⚙️) next to the **Source** step and **update the file path** or credentials.                                                        |
| **`Expression.Error`** ("The column... of the table wasn't found")         | A step in your query refers to a column name that no longer exists, often because it was changed or removed in the source file.                 | Review your applied steps. If a column was renamed at the source, you can either **remove the unnecessary "Rename" step** in your query or edit the step to use the new column name. |
| **`Formula.Firewall`**                                                     | Data is being combined from sources with conflicting **Data Privacy Levels** (e.g., trying to merge a "Private" source with a "Public" source). | Go to **File > Options and settings > Data source settings**. Review and adjust the privacy levels for the sources involved to allow them to share data.                             |

#### 2. Cell-Level Errors
A **cell-level error** does not stop the query from loading. Instead, it displays the value **`Error`** in the specific cells where the problem occurred. You can identify these errors using the **Column Quality** bar at the top of the column.
When you encounter cell-level errors, you have three main ways to handle them:

|Handling Method|Action|Where to Find It (UI)|
|---|---|---|
|**Remove Errors**|Deletes the entire row containing the error.|**Home** tab > **Remove Rows** > **Remove Errors**.|
|**Replace Errors**|Replaces the `Error` value with a fixed, static value that you specify (e.g., 0 or null).|**Transform** tab > **Replace Values** > **Replace Errors**.|
|**Keep Errors**|Deletes all rows that do _not_ have an error. This is useful for auditing and isolating the problematic rows.|**Home** tab > **Keep Rows** > **Keep Errors**.|
##### Common Causes of Cell-Level Errors
- **Data Type Conversion Errors:** This is the most common cause. It happens when a value in a column cannot be converted to the selected data type (e.g., trying to convert the text "N/A" to a Whole Number).
- **Operation Errors:** Occurs when you try to apply an operation that isn't supported, such as multiplying a text value by a number.
###