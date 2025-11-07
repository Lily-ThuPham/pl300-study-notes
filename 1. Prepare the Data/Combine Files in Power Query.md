[Combine files overview - Power Query | Microsoft Learn](https://learn.microsoft.com/en-us/power-query/combine-files-overview#combine-files-dialog)
Files can come from various sources, such as (but not limited to):
- Local folders
- SharePoint sites
- Azure Blob storage
- Azure Data Lake Storage (Gen1 and Gen2)
### 1. The "Combine Files" Process
Combining files is a three-stage process managed by Power Query.
1. **Table Preview:** You first connect to a source that contains multiple files (like a local folder, SharePoint, or Azure Data Lake). Power Query will display the "file system view," showing metadata for each file. From here, you can either **Combine** immediately or select **Transform Data** to first filter the list of files you want to combine.
2. **Combine Files Dialog:** After starting the combine process, this dialog box appears. Power Query analyzes a **sample file** (by default, the first file in the list) to determine the correct connector to use (e.g., Text/CSV, Excel).
3. **Output and Generated Queries:** Once the process is finished, Power Query automatically creates a set of "helper queries" and applies the logic to every file, appending the results into a single, final table.
### 2. The Helper Queries (What Power Query Creates)
The most important concept to understand is that Power Query automates the combination process by creating a set of linked queries, which are organized into a new group or folder.

| Query Component           | What It Is                                                                                                                           | Your Role / What to Do                                                                                                                                                         |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Transform Sample File** | An **example query** that performs all the required data extraction and transformation steps for a **single file**.                  | **This is where you make your changes.** Any transformation you apply here (like removing header rows) will be automatically applied to _every_ file before they are combined. |
| **Function Query**        | A **parameterized function** that is automatically created based on the "Transform Sample File" query.                               | You generally do not need to edit this. It's the mechanism that applies your sample file logic to all other files.                                                             |
| **Final Output Query**    | The original query you started with, now modified to apply the new function to each file and expand the results into a single table. | This is where you see the final, combined result. You may need to perform final cleanup steps here, like setting data types.                                                   |
#### Disable Helper Queries 
The helper queries are automatically created because Power BI assumes that the goal is to merge the data from all of the files into a single dataset. While this is a common scenario, for this scenario, this is not the desired outcome.

When the Power Query Editor first opens, it displays all of the datasets merged into a single table.
1. First, remove all steps from the **Applied Steps** list except the **Source** step.
	**Note:** The helper queries are no longer applied to the dataset. However, they are still present in the **Queries** pane.
2. Right-click the **Transform File** **from Group** and select **Delete Group**. When prompted, confirm the deletion.
### 3. A Practical Example: Cleaning and Combining CSV Files
This is a common real-life scenario that is frequently tested.
**The Problem:** You have a folder of monthly sales CSV files. Each file has 4 header rows at the top before the actual column names, which are on row 5.
**The Solution:**
1. **Connect** to the folder and click **Combine & Transform Data**.
2. In the "Combine files" dialog, click **Transform Data**.
3. **Select the "Transform Sample File" query** in the Queries pane. This is the critical step.
4. In this sample file query, perform the cleaning steps:
    - Go to **Home > Remove Rows > Remove Top Rows** and enter `4` to get rid of the unnecessary headers.
    - Go to **Home > Use First Row as Headers** to promote the column names correctly.
5. **Go back to the Final Output Query**. You might see an error like "The column 'Column1' of the table wasn't found."
    - **Why?** The final query may have an old "Changed Type" step that is trying to use the original column names (`Column1`, `Column2`, etc.) which no longer exist.
    - **How to Fix:** In the "Applied Steps" pane for the final query, **delete the last "Changed column type" step**.
6. **Set Final Data Types:** In the final output query, manually set the correct data type for each of your columns (e.g., Date, Whole Number, Text).