## **1. Context and DAX measures** 
[context influences measures in DAX](https://learn.microsoft.com/en-us/training/modules/create-measures-dax-power-bi/2-context)
The context in which your calculations are executed can give rise to variations in data.
DAX Custom calculations are context sensitive,  meaning they can vary based on the level of data being evaluated, the structure of the data model, and the visual representation used.
## **2. Implicit measure**
**Implicit measures** are automatic aggregations that Power BI creates when you use a data column in a visual. They are a quick way to summarize data but have significant limitations compared to explicit (DAX) measures.
### Identifying and Using Implicit Measures
- **Identification:** In the **Data pane**, a column that can be implicitly summarized is marked with a **sigma symbol (∑)** next to its name. This symbol indicates that the column is numeric and will be aggregated by default.
- **Default Summarization:** Power BI automatically applies a default aggregation when you add a field to a visual. As the data modeler, you can control this by setting the **Summarization** property for each column.
    - For columns like `Sales Amount`, the default is **Sum**.
    - For columns that are rates, like `Unit Price`, the default should be set to **Average**, as summing them together would be misleading.
- **Changing Aggregation:** A report author can easily change the aggregation type for an implicit measure directly in the visual's field well (e.g., from Sum to Average, Min, Max, or Count).
### Summarizing Non-Numeric Columns
Even though they don't have a sigma symbol, non-numeric columns (like text or dates) can also be summarized using specific aggregation functions:
- **Text columns:** Can be summarized by `First`, `Last`, `Count`, or `Count (Distinct)`
- **Date columns:** Can be summarized by `Earliest`, `Latest`, `Count`, or `Count (Distinct)`.
#### How to Configure the Default Summarization
As the data modeler, you can control the default aggregation behavior for each column. This is a crucial step to guide report creators and prevent incorrect analysis (like summing unit prices).
###### In Power BI Desktop
1. Navigate to the **Model view** or **Data view**.
2. Select the column you want to configure from the **Data pane**.
3. The **Column tools** contextual ribbon will appear.
4. In the "Properties" section of the ribbon, find the **Summarization** dropdown.
5. Select the desired default aggregation (e.g., `Sum`, `Average`, `Count`, or `Don't summarize`).
    - **Don't summarize:** This is the best option for columns that should never be aggregated, like ID keys or year values. It removes the sigma symbol from the column in the Data pane.
###### In the Power BI Service (Editing a Data Model)
1. Open the workspace and find the semantic model.
2. Select the **More options (...)** menu and choose **Open data model**.
3. Select the column you want to configure from the **Data pane**.
4. The **Properties** pane will appear on the right.
5. Expand the **Advanced** section and find the **Summarize by** dropdown
6. Select the desired default aggregation.

> [!Note] **Implicit measures** can select from one of nine aggregations when placed in the Values well of a visual. **Both Implicit and Explicit measures** can be used as a Drillthrough field, to create quick measures, and with Field Parameters.
### Advantages vs. Disadvantages

| **Advantages ✅**                                                                                                 | **Disadvantages ❌**                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ease of Use:** They are created automatically by dragging and dropping a field, requiring no DAX code.         | **Risk of Misleading Results:** Report authors can change the aggregation to something that doesn't make business sense (e.g., summing unit prices).                                                       |
| **Flexibility for Authors:** Report creators can quickly change the aggregation type to suit their visual needs. | **Limited to Simple Scenarios:** They can only perform a single aggregation on a single column. They **cannot** handle any complex business logic or calculations that involve multiple fields or filters. |
| **Reduced Development Time:** The data modeler spends less time creating basic explicit measures.                | **Not Reusable:** The logic is tied to a single visual and has to be reconfigured for every new visual.                                                                                                    |
## **3. Additivity- Type of measures**

**Additive measures (+ / -):** allow for data aggregation across any dimension.
	- **Sales Amount:** The total sales can be summed across different product categories, regions, or time periods without affecting the accuracy of the result.
	- **Cost:** The total cost can be summed across different departments, projects, or time periods.
**Non-additive measures:** cannot be meaningfully aggregated across dimensions. 
	- **Percentage:** Percentages cannot be summed across different categories or time periods.
	- **Average Unit Price:** The average unit price cannot be summed across different products or time periods.
**Semi-additive measures**: allow for data aggregation across some by not all dimension, typically not over time. 
	- **Inventory:** The total inventory can be summed across different product categories but not across time periods (as inventory levels change over time).
	- **Average Sales:** The average sales can be summed across different product categories but not across time periods (as average sales may change over time).

## **4. Using Quick Measures for Common Calculations**
### How to Create a Quick Measure
1. In the **Data** pane, right-click any item or select the ellipsis (**...**) and choose **New quick measure**.
2. In the **Quick measures** window, choose a calculation from the dropdown list (e.g., "Year-over-year change").
3. Drag the appropriate fields from your Data pane into the input boxes (e.g., `Total Sales` into "Base value" and `Date` into "Date").
4. Select **Create**.
### Categories of Calculations
Quick measures are organized into several categories to help you find the calculation you need:
- **Aggregate per category:** (e.g., Average, Max, Min per category)
- **Filters:** (e.g., Filtered value, Sales from new customers)
- **Time intelligence:** (e.g., Year-to-date total, Year-over-year change, Rolling average)
- **Totals:** (e.g., Running total)
- **Mathematical operations:** (e.g., Addition, Division, Percentage difference)
- **Text:** (e.g., Star rating, Concatenated list of values)
### The Key Benefit: Learning DAX
A major advantage of quick measures is that they serve as an excellent learning tool. When you create a quick measure, you can select it and view the **auto-generated DAX formula** in the formula bar.
This allows you to see how complex calculations are structured, helping you to understand DAX and eventually write or modify your own measures from scratch.
### Considerations and Limitations
- **Model Modification:** Quick measures are only available if you can modify the data model. They work with Import mode and most live connections to SQL Server Analysis Services (SSAS), but have limitations.
- ==**DirectQuery Limitation:**== You **cannot** create **time intelligence** quick measures when working in **DirectQuery mode**. The DAX functions they use do not perform well when translated to the source query language.
> [!Note] **Date Table:** For time intelligence quick measures to work correctly, you must have a proper date table in your model that has been **marked as a date table** and the **Date** value has to come from the table on the _one side_. Otherwise, you need a primary date column or column with date hierarchy.
## **5. Organizing Your Measures**
### Home Table
- **What it is:** Every measure has a **Home table**, which is the table where it is stored and displayed in the Data pane.
- **How to change it:** You can change a measure's Home table by selecting the measure and then, in the **Measure tools** ribbon, choosing a different table from the "Home table" dropdown list.
### Display Folders
You can group related measures and columns into folders within a table to keep your Data pane organized.
- **How to create:**
    1. Go to the **Model view**.
    2. In the Data pane, select the measure(s) or column(s) you want to group (you can multi-select with Ctrl or Shift).
    3. In the **Properties** pane, type a name into the **Display folder** box.
* * _**Display folder** can also be used to store columns, calculated columns.
- **Creating Subfolders:** Use a **backslash (`\`)** to create a nested folder structure. For example, typing `Sales\YTD Measures` will create a "YTD Measures" folder inside a "Sales" folder.
- **Placing in Multiple Folders:** Use a **semicolon (`;`)** to make a field appear in more than one folder.
### Creating a Dedicated Measure Table (Best Practice)
A highly recommended practice is to create a special table that contains only measures. This table will automatically appear at the top of your Data pane, making your measures easy to find.
1. On the **Home** ribbon, select **Enter Data**.
2. Create a table with a single column. You don't need to add any data to it. Give the table a name, like `_Measures` or `Key Measures`.
3. Click **Load**. The new, empty table will appear in your Data pane.
4. Move all of your measures into this new table by changing their **Home table**.
5. Once all measures are moved, **hide the placeholder column** you created in step 2 (right-click the column in the Data pane and select "Hide"). Do **not** hide the table itself.
## **6. Custom Dynamic Format Strings**
[Use custom format strings in Power BI Desktop - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-custom-format-strings#add-a-visual-level-format-string)
This is an advanced feature that allows you to customize how a measure's value is displayed in visuals by conditionally applying a format string with a separate DAX expression. For example, you could show a value as `"$1.2M"` for millions but `"$500K"` for thousands, all within the same measure.

Format strings exist on three levels:

| **Level** | **Impacts**                                           | **Available for**                      |
| --------- | ----------------------------------------------------- | -------------------------------------- |
| Element   | Selected element of the selected visual               | Measures, Columns, Visual Calculations |
| Visual    | Selected visual                                       | Measures, Columns, Visual Calculations |
| Model     | All visuals, all pages, all reports on the same model | Measures, Columns                      |
#### How to configure a dynamic format string in Model view 
1. In **Model View**, select the Measures in the **Data pane** -> **Model** tab. 
2. In the **Properties pane** -> **Formatting** section, click the dropdown menu and select **Dynamic** at the bottom of the list.
3. Select **Edit** button, formula bar will appear, write a expression that must return a **text string** representing the desired format 
#### How to configure a dynamic format string in Data or Report View 
1. Select the measure you want to format in the **Data pane**.
2. The **Measure tools** ribbon will appear.
3. In the "Formatting" section, click the dropdown menu that usually says "General" or "Currency".
4. Select **Dynamic** at the bottom of the list.
5. A new formula bar will appear to the left. Here, you write a DAX expression that must return a **text string** representing the desired format.
### Custom Format syntax
#### Supported Date and Time Symbols (VBA-Style)

| **Date Symbols** | **Meaning / Output**            | **Time Symbols** | **Meaning / Output**               |
| ---------------- | ------------------------------- | ---------------- | ---------------------------------- |
| **`d`**          | Day of month (1-31)             | **`h`**          | Hour (0-23 or 1-12 with AM/PM)     |
| **`dd`**         | Day with leading zero (01-31)   | **`hh`**         | Hour with leading zero (00-23)     |
| **`m`**          | Month number (1-12)             | **`n`**          | Minute (0-59)                      |
| **`mm`**         | Month with leading zero (01-12) | **`nn`**         | Minute with leading zero (00-59)   |
| **`mmm`**        | Abbreviated month name (Jan)    | **`s`**          | Second (0-59)                      |
| **`mmmm`**       | Full month name (January)       | **`ss`**         | Second with leading zero (00-59)   |
| **`yy`**         | Two-digit year (99)             | **`AM/PM`**      | AM/PM designator for 12-hour clock |
| **`yyyy`**       | Four-digit year (1999)          |                  |                                    |
**Tip:** Always prefer using **`n`** or **`nn`** for minutes to avoid confusion with the month symbol **`m`**.
#### Supported Number Symbols (VBA-Style)

|**Symbol**|**Description**|
|---|---|
|**`0`**|Digit placeholder. Displays a digit or a zero if no digit exists.|
|**`#`**|Digit placeholder. Displays a digit or nothing if no digit exists.|
|**`.`**|Decimal placeholder.|
|**`,`**|Thousands separator. Also used for number scaling (see below).|
|**`%`**|Percentage placeholder. Multiplies the value by 100 and adds a % sign.|
|**`"text"`**|Displays any characters inside the double quotes as literal text.|
#### Adding Unicode or Special Symbols
To include a special symbol (like °, €, µ, ²) in your format, you must insert the **actual Unicode character** itself into the format string, often enclosed in double quotes. Escape sequences like `\uXXXX` are **not** supported.

|**Goal**|**Format String**|**Example Output**|**Notes**|
|---|---|---|---|
|Append Celsius with a space|`0.0" °C"`|`23.4 °C`|The space inside the quotes is preserved.|
|Add a currency symbol|`#,##0.00" €"`|`1,234.00 €`|The Euro symbol is added as a literal.|
|Show a unit label|`0" µs"`|`15 µs`|The micro symbol (µ) is pasted directly.|
|Add a superscript|`0" m²"`|`25 m²`|The superscript 2 character (²) is pasted directly.|
#### Formatting Based on Value (Positive, Negative, Zero)
A number format string can have up to three sections separated by semicolons to define the format for **positive values**, **negative values**, and **zero**, respectively.
**Structure:** `<POSITIVE>;<NEGATIVE>;<ZERO>`
This is extremely useful for applying conditional formatting to numbers.

|**Value**|**Format String: #,##0;(#,##0); "Zero"**|**Format String: "[Green]▲ "#,##0;"[Red]▼ "#,##0;"-"**|
|---|---|---|
|`1234`|`1,234`|`▲ 1,234` (in Green)|
|`-1234`|`(1,234)`|`▼ 1,234` (in Red)|
|`0`|`"Zero"`|`-`|
#### Number Scaling (K, M, B)
There are two ways to apply scaling suffixes (like K for thousands, M for millions) to your numbers.
##### 1. Automatic Scaling (Visual Setting)
- **What it is:** This is the default behavior in many Power BI visuals. The **Display units** property is set to "Auto," causing Power BI to automatically add a K, M, or B suffix to large numbers.
- **This is NOT controlled by your custom format string.**
- **How to Turn it Off:** To gain full control, select the visual, go to the **Format pane**, find the relevant value section (e.g., `Callout value` or `Data labels`), and change **Display units** from **Auto** to **None**.
##### 2. Manual Scaling (Format String)
- **What it is:** You can use the comma (`,`) as a scaling operator within your format string. Each comma placed before the decimal point (or at the end of the number) divides the number by 1000.
- **How it Works:**
    - **One comma (`,`)**: Divides by 1,000.
    - **Two commas (`,,`)**: Divides by 1,000,000.
    - **Three commas (`,,,`)**: Divides by 1,000,000,000.

|**Original Value**|**Format String**|**Displayed Result**|
|---|---|---|
|`1,234,567`|`#,##0.0," K"`|`1,234.6 K`|
|`1,234,567`|`#,##0.0,," M"`|`1.2 M`|
|`5,432,109,876`|`#,##0.0,,," B"`|`5.4 B`|
