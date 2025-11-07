### 1. Permissions and Security
Before exporting, it's crucial to understand that access is controlled and data can be protected.

- **Who can export:** You must have **permissions to the data** to export it. Report designers and administrators can disable export features for individuals or the entire organization to protect sensitive data. If you can't export, you should contact the report owner or your admin.
- **Data Protection with Sensitivity Labels:** If a report is classified with a **sensitivity label** (from Microsoft Purview Information Protection), those protection settings are applied when you export data to Excel, PowerPoint, or PDF. This means only authorized users will be able to open the protected exported files, ensuring data remains secure even outside of Power BI.

---
### 1. Permissions and Security

Before exporting, it's crucial to understand that access is controlled and data can be protected.

- **Who can export:** You must have **permissions to the data** to export it. Report designers and administrators can disable export features for individuals or the entire organization to protect sensitive data. If you can't export, you should contact the report owner or your admin.
- **Data Protection with Sensitivity Labels:** If a report is classified with a **sensitivity label** (from Microsoft Purview Information Protection), those protection settings are applied when you export data to Excel, PowerPoint, or PDF. This means only authorized users will be able to open the protected exported files, ensuring data remains secure even outside of Power BI.
#### Designer and Admin Controls
Report authors and administrators have control over what data can be exported.
- **Report-Level Setting:** In Power BI Desktop (**File > Options and settings > Options > Report settings**), a designer can choose one of three options for the current file:
    1. Allow export of **summarized data** only.
    2. Allow export of **both summarized and underlying data**.
    3. **Don't allow** any data to be exported.
- **Admin Override:** A Power BI administrator can set a tenant-wide policy that **overrides** the individual report settings.

### 2. Viewing Data Directly Within a Visual
These features are for viewing the data directly in the Power BI interface and are great for quick validation or seeing the raw numbers behind a chart.

|**Feature**|**What It Does**|**Availability**|**How to Access**|
|---|---|---|---|
|**Show as a table**|Displays the **aggregated data** used to create the visual in a table format, either below or next to the visual.|Power BI Desktop & Service|Select the visual's **More options (...)** menu and choose **Show as a table**.|
|**Show records**|Displays the underlying, **unaggregated rows** from the data model that make up a specific data point.|Power BI Desktop only|Select a data point in a visual, then go to the **Visual tools** ribbon and select **Data point table**.|
### 3. Exporting Data from a Dashboard or Report
[Export data from a Power BI visualization - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-export-data?tabs=powerbi-desktop)
This is the most direct way to get a static copy of the data from a specific visual.

| **Source**         | **How to Access**                                                       | **What You Get**                                                                                                                       |
| ------------------ | ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Dashboard Tile** | From the tile's **More options (...)** menu, select **Export to .csv**. | A `.csv` file containing the data from that tile. If the visual was filtered, the export will also be filtered.                        |
| **Report Visual**  | From the visual's **More options (...)** menu, select **Export data**.  | You can choose different formats, including `.csv` and `.xlsx` files containing either **Summarized data** or the **Underlying data**. |
### 4. Exporting and Analyzing Data in Excel
These features are designed to take your governed Power BI data and use it for further analysis in Microsoft Excel. This requires **Build permission** on the semantic model.

| **Feature**                              | **What It Is**                                                                                            | **How to Access**                                                                                                                                                                                                              | **What You Get**                                                                                                                                                                            |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Analyze in Excel**                     | Connects a new Excel file to the **entire semantic model**.                                               | In the Power BI service:<br>- from a report's **Export** menu<br>- from the dataset's **More options (...)** menu in Workspace.                                                                                                | A new Excel workbook with a **live connection** to the full semantic model, ready for you to build PivotTables from scratch using all the tables and measures from the model.               |
| **Export to Excel with live connection** | Exports the **summarized data** from a **single visual** into an Excel table.                             | From a visual's **More options (...) > Export data** menu.                                                                                                                                                                     | An Excel workbook containing the visual's data in a table that maintains a **live, refreshable connection** back to Power BI.                                                               |
| **Power BI Excel Add-in**                | A dedicated add-in within Excel that allows you to discover and connect to your Power BI semantic models. | From the **Insert** ribbon, expand the **PivotTable** and select **From Power BI (Microsoft)**<br>From Data ribbon, expand the **Get Data**, expand **From Power Platform** menu and select **From Power BI (Microsoft)**.<br> | A pane within Excel where you can browse your datasets and insert either a **connected PivotTable** (just like _Analyze in Excel_ does) or a **connected query table** into your worksheet. |
### 5. Downloading the `.pbix` File
This allows you to get a local, editable copy of the report and its data model. This requires at least a **Contributor** role in the workspace.

|**Download Method**|**How to Access**|**Download Modes Available**|
|---|---|---|
|**Download a report as a `.pbix` file**|In the Power BI service, open the report and go to **File > Download this file**.|• **A copy of the report and data:** Downloads the `.pbix` with the imported data included. • **A copy of the report with a live connection:** Downloads a "thin" report that is live connected to the semantic model in the service. This is the only option for reports based on models with incremental refresh or that have been modified by the XMLA endpoint.|
|**Download a `.pbix` file from a semantic model**|In a workspace, go to the semantic model's **More options (...)** menu and choose **Download this file**.|This will download a `.pbix` file containing the data model but with a blank report canvas.|

### Key Limitations
It's important to know that downloading a `.pbix` file is not always possible. Common limitations include:
- You cannot download reports based on a **Direct Lake** semantic model.
- You cannot download semantic models that are configured for **incremental refresh** (you can only download a live-connected version of the _report_).
- You cannot download reports that were originally created in the Power BI service (unless they are saved first).
- The ability to download can be disabled by a Power BI administrator.
- **Row Limits:** There are limits on how many rows you can export: **30,000** for `.csv` and **150,000** for `.xlsx`.
- **DirectQuery Limits:** When using DirectQuery, the maximum amount of data that can be exported is **16 MB** (uncompressed), which may result in fewer rows than the stated limits.
- **Disabled Feature:** Administrators or report designers can disable data export for the entire organization or for specific reports.
- **Unsupported Visuals:** Power BI custom visuals and R visuals are not supported for export.