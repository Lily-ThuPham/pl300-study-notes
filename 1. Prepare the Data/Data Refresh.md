[Data refresh in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/connect-data/refresh-data#understanding-data-refresh)

### 1. Understanding Data Refresh and Storage Modes
Data refresh is the process of updating the data in your Power BI reports and dashboards. The requirements for refresh are entirely dependent on the **storage mode** of your semantic model.

|Storage Mode|Does it Require Data Refresh?|How it Works|
|---|---|---|
|**Import** 📸|✅ **Yes (Essential)**|Power BI copies data from the source into an in-memory model. A **data refresh** is the only way to update this copied data.|
|**DirectQuery** 📡|❌ **No**|Power BI sends live queries to the data source with every user interaction. The data is always as current as the source.|
|**Live Connection** 📺|❌ **No**|Connects to an external model (like AAS or another Power BI dataset). The refresh is managed at the **source model level**, not in your Power BI report.|
|**Push** 📨|❌ **No**|Data is pushed into the semantic model by an external service. It does not connect to a data source directly.|
Here is a condensed study note based on the provided material, structured to help you memorize the key concepts for data refresh in Power BI.

## Study Note: Data Refresh in Power BI

### 1. Understanding Data Refresh and Storage Modes

Data refresh is the process of updating the data in your Power BI reports and dashboards. The requirements for refresh are entirely dependent on the **storage mode** of your semantic model.

|Storage Mode|Does it Require Data Refresh?|How it Works|
|---|---|---|
|**Import** 📸|✅ **Yes (Essential)**|Power BI copies data from the source into an in-memory model. A **data refresh** is the only way to update this copied data.|
|**DirectQuery** 📡|❌ **No**|Power BI sends live queries to the data source with every user interaction. The data is always as current as the source.|
|**Live Connection** 📺|❌ **No**|Connects to an external model (like AAS or another Power BI dataset). The refresh is managed at the **source model level**, not in your Power BI report.|
|**Push** 📨|❌ **No**|Data is pushed into the semantic model by an external service. It does not connect to a data source directly.|

### 2. The Different Types of Refresh Operations

A "refresh" in Power BI can refer to several distinct processes.

|                                         | Refresh of report visuals                                                                                                                                                                                                                                                                                                                                            | Data refresh                                                                                                                                                                                                                                                                                                                  | Schema refresh                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| What do the different refresh types do? | **Queries used to populate visuals are refreshed.**  <br>  <br>For visuals using DirectQuery tables, the visual will query to get the latest data from the data source.  <br>  <br>For visuals using imported tables, the visual will only query data already imported to the semantic model on the last data refresh.                                               | **Data is refreshed from the data source.**  <br>  <br>Doesn't apply to DirectQuery tables as they are at the visual level and rely on refresh of report visuals.  <br>  <br>For imported tables, the data is refreshed from the source.                                                                                      | **Any data source table structure change since previous refresh will show.**  <br>  <br>For example: To show a new column added to a Power BI Dataflow or SQL Database view.  <br>  <br>Applies to imported, DirectQuery, and Direct Lake tables.                                                                                                                                    |
| In **Power BI Desktop**                 | - **Optimize** ribbon > **Refresh visuals**<br>- **View** ribbon > **Performance Analyzer** button > **Refresh visuals**<br>- Creating and changing visuals causing a DAX query to run<br>- When [Page Refresh](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-automatic-page-refresh) is turned on (DirectQuery only)<br>- Opening the PBIX file | Not available independently from other refresh types                                                                                                                                                                                                                                                                          | Not available independently from other refresh types                                                                                                                                                                                                                                                                                                                                 |
| In the **Power BI service**             | - When the browser loads or reloads the report<br>- Clicking the **Refresh Visuals** top right menu bar button<br>- Clicking the **Refresh** button in edit mode<br>- When [Page Refresh](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-automatic-page-refresh) is turned on (DirectQuery only)                                                  | - Scheduled refresh<br>- Refresh now<br>- Refresh a Power BI semantic model from Power Automate<br>- Processing the table from SQL Server Management Studio (Premium)                                                                                                                                                         | Only available for semantic models in [Direct Lake mode](https://learn.microsoft.com/en-us/fabric/get-started/direct-lake-overview) when using [Edit tables](https://learn.microsoft.com/en-us/fabric/get-started/direct-lake-edit-tables) when [editing a data model in the Power BI service](https://learn.microsoft.com/en-us/power-bi/transform-model/service-edit-data-models). |
| Keep in mind                            | For example, if you open a report in the browser, then the scheduled refresh performs a data refresh of the imported tables, the report visuals in the open browser won't update until a refresh of report visuals is initiated.                                                                                                                                     | Data refresh in the Power BI service will fail when the source column or table is renamed or removed. It fails because the Power BI service doesn't also include a schema refresh. To correct this error, a schema refresh needs to happen in Power BI Desktop and the semantic model needs to be republished to the service. | A renamed or removed column or table at the data source will be removed with a schema refresh, and it can break visuals and DAX expressions (measures, calculated columns, row-level security, etc.), as well as remove relationships that are dependent on those columns or tables.                                                                                                 |
### 3. Configuring Scheduled Refresh
This is the process of automating the **Data Refresh** for an **Import** model.
- **How to Configure:** Go to the semantic model **Settings** in the Power BI service.
- **Refresh Limits:**
    - **Shared Capacity (Pro):** Up to **8** scheduled refreshes per day.
    - **Premium/PPU/Fabric Capacity:** Up to **48** scheduled refreshes per day.
- **On-Demand Refresh:** You can manually trigger a refresh at any time by selecting **"Refresh now."** This does not count towards your scheduled refresh limit.
- **Timing:** Power BI initiates refreshes on a "best-effort" basis. It aims to start within 15 minutes of the scheduled time, but delays of up to an hour can occur.
- **Automatic Deactivation:** The schedule will be disabled after **four consecutive failures** or after **two months of inactivity** (no one viewing the report).
### 4. Data Source Dependencies (Gateways)
No refresh can succeed unless Power BI can access the underlying data sources.
- **Cloud Data Sources:** (e.g., Azure SQL, SharePoint Online) **Do not require a gateway**. Power BI can connect to them directly.
- **On-Premises Data Sources:** (e.g., a SQL Server in your company's server room) **REQUIRE an on-premises data gateway**. The gateway acts as a secure bridge between your private network and the Power BI cloud service.
- **Mixed Sources:** If a single query combines data from an on-premises source and a cloud source, a **gateway is required for both**.
### 5. Monitoring Refresh Status
It's a best practice to periodically check that your refreshes are succeeding.
- **Workspace View:** A small **warning icon** will appear next to a semantic model that has a refresh issue.
- **Refresh History:** In the semantic model's **Settings**, the **Refresh history** page provides a detailed log of past refresh cycles, showing their success or failure status and providing error details for troubleshooting.
- **Fabric Monitoring Hub:** A centralized place in the Fabric service to monitor all refresh activities across your semantic models.

---
### 6. Additional comparison  

| Refresh Type                  | What it Does                                                                                               | Applies To                          | Key Notes                                                                                                                  |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Data Refresh**              | The main refresh type. Imports data from the original data source into an **Import** model.                | Import mode                         | This is what is configured in a **Scheduled Refresh**.                                                                     |
| **OneDrive Refresh**          | Synchronizes the `.pbix` file in the Power BI service with a source file in OneDrive or SharePoint Online. | Files hosted in OneDrive/SharePoint | Occurs automatically about every hour. This is a file sync, not a data source refresh (though it can trigger one).         |
| **Tile Refresh**              | Updates the visuals (tiles), Push dataset tile pinned to a **dashboard**.                                  | Dashboards<br>Push dataset          | Occurs about every hour for DirectQuery/Live Connection. For Import models, it happens automatically after a data refresh. |
| **Refresh of Report Visuals** | Forces the visuals on a report page to re-query the data model.                                            | Live Connection reports             | Relevant when you suspect a report is showing cached data and you want the absolute latest from the source model.          |
| **Query Cache Refresh**       | Clears and rebuilds the query cache after a data refresh.                                                  | Premium capacities                  | The cache stores query results to speed up report loading. It must be rebuilt after the underlying data changes.           |

|Storage mode|Data refresh|OneDrive refresh|Query caches|Tile refresh|Report visuals|
|---|---|---|---|---|---|
|Import|Scheduled and on demand|Yes, for connected semantic models|If enabled on Premium capacity|Automatically and on demand|No|
|DirectQuery|Not applicable|Yes, for connected semantic models|Not applicable|Automatically and on demand|No|
|Live connection|Not applicable|Yes, for connected semantic models|Not applicable|Automatically and on demand|Yes|
|Push|Not applicable|Not applicable|Not applicable|Automatically and on demand|No|


