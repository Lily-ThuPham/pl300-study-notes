You can import data into Power BI from local files, SharePoint, or Azure. For multiple files with the same structure, use the **Combine Files** feature to merge them into a single table. Power BI's query editor provides a rich set of tools for cleaning and transforming this data before loading it into your model.
[Data sources in Power BI Desktop - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-data-sources)
## Summary of Power BI data connectors

| Connector              | Description                                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SQL Server**         | Connects to Microsoft SQL Server databases, allowing users to import data from SQL databases into Power BI.                                                                                                                                                                                                                                                                               |
| **Excel**              | Enables the import of data from Excel files. This is particularly useful for businesses that store data in Excel spreadsheets.                                                                                                                                                                                                                                                            |
| **SharePoint**         | **_SharePoint folder - SharePoint Online list - SharePoint list_**<br>Provides connectivity to SharePoint lists, enabling users to use SharePoint data for their analytics and reports in Power BI.<br>[connecting a SharePoint Online list](https://learn.microsoft.com/en-us/power-query/connectors/sharepoint-online-list#connect-to-a-sharepoint-online-list-from-power-query-online) |
| **Azure SQL Database** | Connects to Azure's cloud-based SQL database, allowing users to access and analyze data stored in Azure.<br>[connecting Azure SQL database](https://learn.microsoft.com/en-us/power-query/connectors/azure-sql-database)                                                                                                                                                                  |
| **Google Analytics**   | Allows users to import data from Google Analytics, which is useful for analyzing website traffic and other digital analytics data.                                                                                                                                                                                                                                                        |
| **Salesforce**         | Connects to Salesforce to allow the import of sales and customer data into Power BI for more detailed analysis.                                                                                                                                                                                                                                                                           |
| **Dynamics 365**       | Connecting to Microsoft Dynamics 365 CRM enables users to create reports and analyze data from Dynamics 365 applications.                                                                                                                                                                                                                                                                 |
| **MySQL Database**     | Connects to MySQL databases, a popular open-source database, especially used in web applications.                                                                                                                                                                                                                                                                                         |
| **Oracle Database**    | Allows connections to Oracle databases widely used in enterprise environments.                                                                                                                                                                                                                                                                                                            |
| **CSV Files**          | Enables users to import data from CSV (Comma Separated Values) files, a common format for exporting and sharing data.                                                                                                                                                                                                                                                                     |
| **Web**                | Connecting to data source via a URL. The available authentication methods are *Anonymous*, *Windows*, *Basic*, *Web API*, *Organization account*                                                                                                                                                                                                                                          |
| **Exchange Online**    | [Power BI connects to Exchange Servers](https://learn.microsoft.com/en-us/power-query/connectors/microsoft-exchange)<br>Data connector to extract data related to email activities, such as email volume, response times, resolution rates, etc.                                                                                                                                          |

## Local Datasets vs. Shared Datasets

| Feature                           | Local Datasets                                                                                                                      | Shared Datasets                                                                                                                                              |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Data Control & Security**       | The business has **total control** over the data, making it more secure from external access.                                       | Requires **data governance** to control and manage usage, involving setting permissions and access levels for different users.<br>**Single source of truth** |
| **Access Speed**                  | **Faster access** because it's not dependent on the internet or limited by bandwidth constraints.                                   | Access speed is **dependent on internet connectivity** and data transfer speed, which can be slower. Requires report optimization.                           |
| **Remote Access & Collaboration** | **Problematic** for remote teams or traveling executives. Requires IT setup for secure internal network access, which can be slow.  | **Easier collaboration** as multiple individuals can access the data from anywhere. Ideal for remote teams and executives on the go.                         |
| **Scalability**                   | **Limited storage capacity** based on the purchased computer or server hardware. Can present issues with large historical datasets. | **Highly scalable**. Cloud resources can be used for complex calculations and large datasets without being limited by local device capacity.                 |


---
## 1. Connecting to Local Files

This is the most common method for importing data from your own computer.
- **Supported File Types:** Excel workbooks (`.xlsx`, `.xls`), Comma Separated Value (`.csv`), XML, Text (`.txt`), and JSON files.
- **How to Connect:**
    1. From the Power BI Desktop ribbon, select **Get Data**.
    2. Choose the appropriate connector (e.g., **Excel workbook**, **Text/CSV**).
    3. Browse to the file on your computer and select it.
- **The Navigator Window:** After connecting, the Navigator window appears.
    - For Excel, it will show you a list of all worksheets and tables within the workbook.
    - For CSV, it will show you a preview of the single table.
- **Key Decision:** In the Navigator, you must choose between:
    - **Load:** Loads the data directly into your data model as-is.
    - **Transform Data:** Opens the Power Query Editor, allowing you to clean, shape, and filter the data **before** it gets loaded. (This is the recommended best practice).

---
## 2. Combining Files from a Folder

This is a powerful feature for when your data is split across multiple files that all share the **exact same structure** (i.e., the same columns in the same order).
- **Use Case:** You receive a separate sales report file for each month of the year (Jan.csv, Feb.csv, Mar.csv, etc.). You want to analyze the entire year's worth of data in a single table.
- **How to Connect:**
    1. From the ribbon, select **Get Data > More...**.
    2. ==Select the **Folder** connector.==
    3. Browse to the folder containing your files.
- **The Combine Files Dialog:** Power BI will show you a list of the files in the folder. Click the **Combine** button.
    - Power BI will automatically create a **sample query** based on the first file to determine the import steps.
    - It then applies these same steps to every file in the folder and appends them all into one large table.
    - A new column, **Source.Name**, is automatically added so you can identify which file each row came from.
---
## 3. Connecting to SharePoint & OneDrive Files

This is the best practice for collaborative projects, as the files are stored in a central, cloud-based location.

- **The Connector:** Use the **SharePoint folder** connector for both SharePoint and OneDrive for Business (as your OneDrive is essentially a personal SharePoint site).
- **How to Connect:**
    1. Select **Get Data > More... > SharePoint folder**.
    2. Provide the root **Site URL** (e.g., `https://yourcompany.sharepoint.com/sites/YourSiteName`). Do **not** provide the full folder path here.
    3. In the Navigator, browse to the specific folder and file(s) you need.
- **Authentication:** You will need to sign in with your organizational credentials to access the files.
- A SharePoint folder is the only connector that will allow the import of multiple Excel (or CSV) files stored in a OneDrive for Business folder, **==without using a data gateway==**.
- A SharePoint list connector only connects to SharePoint lists and cannot connect to Excel files.
- If you want to connect to an Excel document hosted in SharePoint, you can do so via the [Web](https://learn.microsoft.com/en-us/power-query/connectors/web/web) connector in Power BI Desktop, Excel, and Dataflows, and also with the Excel connector in Dataflows.
> [!Note]  
> - **A personal OneDrive account** provides the ability to automatically synchronize flat files residing in a user's OneDrive and Power BI datasets. Since it relies on OneDrive access, it requires the user's credentials of the corresponding Microsoft account. The OneDrive - Business option uses Azure Active Directory credentials. 
> - The SharePoint – Team Sites option uses the same Azure Active Directory credentials as the ones used to access SharePoint Online. For the local file option, no additional credentials are required to access them.

> [!Note] The shared folder on a local network will require a gateway as it is not available to the internet. SharePoint Online, OneDrive, and OneDrive for Business all can be refreshed as cloud data sources without a gateway.

### Connecting Power BI to a SharePoint Online List
You can connect Power BI to a SharePoint Online list in two different ways: a quick, direct method from the **Power BI service**, or a more powerful and customizable method using **Power BI Desktop**.
#### Comparison of Methods

|**Feature**|**Method 1: Create from Service (Quick Create)**|**Method 2: Connect from Desktop (Full Control)**|
|---|---|---|
|**Where It's Done**|In your web browser (**SharePoint Online** & **Power BI Service**)|In the **Power BI Desktop** application|
|**How to Start**|In SharePoint, select **Export > Export to Power BI** on the actions bar.|In Power BI Desktop, select **Get Data > SharePoint Online List**.|
|**What It Creates**|A **semantic model** directly in the Power BI service.|A `.pbix` file containing a semantic model and report pages, which you then publish.|
|**Data Transformation**|**None.** The data is loaded as-is.|**Full control.** You can use the **Power Query Editor** to clean, transform, and model the data.|
|**Best For...**|Quickly creating a simple semantic model from a single, clean list.|Building a proper, well-modeled report, combining the list with other data sources, or when the data needs cleaning.|
|**Limitations**|- Won't be created if the list has numbers with > 4 decimal places. - Does not support B2B or service principal authentication.|- Requires you to build the report and model manually.|
#### Method 1: Create a Semantic Model from the Power BI Service (Quick Create)
This is the fastest way to get your SharePoint list data into Power BI.
1. **Start from SharePoint:** In your SharePoint Online list, select **Export > Export to Power BI** from the actions bar.
2. **Name and Save:** Power BI will open in your browser. You will be asked to name the new semantic model and choose a workspace to save it in (Free users can only save to "My Workspace").
3. **Authentication:**
    - If you've connected to this SharePoint site before, Power BI will ask you to choose which credentials to use.
    - This is important because the data you see in the semantic model will be based on the permissions of the account you select.
4. **Result:** A new semantic model is created in your workspace. You can then use this model to create new reports, analyze in Excel, or set up a scheduled refresh.
#### Method 2: Connect from Power BI Desktop (Standard Method)
This is the traditional and most flexible method, giving you full control over the data model and report.
1. **Get Data:** Open Power BI Desktop and select **Get Data > Online Services > SharePoint Online List**.
2. **Enter Site URL:** You will be prompted for the **Site URL**. This is the root URL of the SharePoint site, _not_ the full URL of the list itself.
    - _Example:_ `https://yourcompany.sharepoint.com/sites/YourSiteName`
3. **Authenticate:** Select **Microsoft Account** and sign in with your organizational (Microsoft 365) credentials.
4. **Use the Navigator:** The **Navigator** window will appear, showing you _all_ the lists on that SharePoint site. Select the checkbox next to the list(s) you want to import.
5. **Transform or Load:**
    - **Transform Data (Recommended):** This opens the Power Query Editor, where you can clean, shape, and transform your data before loading it into the model.
    - **Load:** This loads the list data directly into your data model.
6. **Build and Publish:** You can now model the data, change data types (e.g., set numeric columns to `Decimal Number`), create your visuals, and **Save** and **Publish** the `.pbix` file to the Power BI service.

---
## 4. Key Data Transformation Steps

Once you open the Power Query Editor, you can perform hundreds of transformations. Here are some of the most common and essential ones for file-based data:
- **Remove Rows:** Remove top/bottom rows (e.g., report headers or footers) or remove blank rows.
- **Use First Row as Headers:** Promotes the first row of data to become the column headers. This is a very common step.
- **Change Data Types:** Ensure each column is set to the correct type (e.g., Whole Number, Decimal Number, Date, Text). Power BI often gets this right, but you should always verify.
- **Filter Data:** Remove unnecessary values from columns (e.g., filter out a "Test" category or remove `null` values).
- **Split Column:** Split a single column into multiple columns based on a delimiter (e.g., splitting a "Full Name" column into "First Name" and "Last Name" based on the space).
- **Unpivot Columns:** Transform a "wide" table into a "tall" table. This is an essential skill for creating data models that are easy to analyze. For example, converting a table with a separate column for each month into a table with a single "Month" column and a single "Value" column.
---
## 5. Connecting to Relational Data Sources

Relational data sources, like SQL Server, are the most common type of database used in business. They store data in a structured way across multiple, related tables.
- **Supported Sources:** Power BI has a vast number of connectors for databases, including but not limited to:
    - Microsoft SQL Server
    - Azure SQL Database
    - PostgreSQL
    - MySQL
    - Oracle
- **How to Connect:**
    1. Select **Get Data** and choose the appropriate connector (e.g., **SQL Server**).
    2. In the dialog box, you must provide the **Server** name and the **Database** name (which is optional but recommended).

---
## 6. The Most Important Decision: Data Connectivity Mode

When you connect to a relational source, you must choose a **Data Connectivity mode**. This is a critical decision that affects your report's performance, flexibility, and data freshness. 

| Feature                         | Import Mode                                                                                                                            | DirectQuery Mode                                                                                                                  |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Data Location**               | Data is **copied and stored** inside the Power BI file (`.pbix`). The model is self-contained.                                         | Data **remains in the source database**. Power BI sends queries to the database in real-time.                                     |
| **Performance**                 | **Faster.** Visuals query the in-memory, compressed data model, which is highly optimized.                                             | **Slower.** Visual performance depends directly on the speed of the source database.                                              |
| **Data Freshness**              | Data is as fresh as the **last scheduled refresh**.                                                                                    | Data is **near real-time**. Every visual interaction queries the live data source.                                                |
| **Data Size**                   | Limited by memory and the 1 GB dataset size limit on Power BI Pro (larger for Premium).                                                | Can handle **very large datasets** (terabytes) because the data is not imported.                                                  |
| **Power Query Transformations** | **All** Power Query transformations are available.                                                                                     | **Limited** set of transformations are supported. Complex transformations can slow down queries.                                  |
| **DAX Flexibility**             | **All** DAX functions are available, including time intelligence functions.                                                            | **Limited** DAX functions are available. Time intelligence functions are not fully supported without a proper Date table.         |
| **When to Use It**              | ✅ **The default and recommended mode.** Use this for most scenarios to get the best performance and full DAX/Power Query capabilities. | ✅ Use this only when your dataset is **too large to import** or when you have a business requirement for **near real-time data**. |

---
## 7. Using an SQL Statement (Optional)

In the connection dialog for most relational sources, there is an **"Advanced options"** section where you can write a native **SQL statement** (e.g., `SELECT * FROM Sales WHERE Year = 2025`).
- **When to Use It:**
    - To perform complex transformations or pre-filtering that are easier to write in SQL than in Power Query.
    - To select specific columns or join tables on the server side before the data ever gets to Power BI.
- **Best Practice:** While this is a useful option, the recommended approach is to connect directly to tables or views and then perform your transformations in the **Power Query Editor**. Using a custom SQL statement can sometimes _prevent query folding_.

---
## 8. Creating Dynamic Reports with Parameters
[[Query parameters]]
Parameters act as variables in Power Query that can store and pass a value to your transformation steps. They allow you to create dynamic reports where you or your end-users can easily change a core value (like a server name, a file path, or a filter value) without ever having to edit the underlying M code.
- **Primary Use Case:** To make your queries flexible and easily updatable. For example, you can create a single Power BI Template (`.pbit`) file that can be used for different regions by simply changing a "Country" parameter.
**Dynamic reports** are reports in which the data can be changed by a developer according to user specifications. Dynamic reports are valuable because a single report can be used for multiple purposes.
### How to Create and Use a Parameter
Let's use an example where you want to create a report that can be easily switched to show data for a different country.
**Step 1: Create the Parameter**
1. In the Power Query Editor, go to the **Home** tab and select **Manage Parameters > New Parameter**.
2. In the dialog box, configure your parameter:
    - **Name:** `p_Country` (a common practice is to prefix parameter names).    
    - **Type:** `Text`.
    - **Suggested Values:** You can provide a list of values, like `USA`, `Germany`, `Canada`.
    - **Current Value:** `USA`.
3. Click **OK**. The new parameter will appear in the Queries pane.

**Step 2: Use the Parameter in a Query**
1. Select the query you want to filter (e.g., your `Sales` query).
2. Find the `Country` column and click the filter dropdown arrow.
3. Instead of selecting a specific country, choose **Text Filters > Equals...**.
4. In the "Filter Rows" dialog, change the filter type from "Text" to **"Parameter"** and select your `p_Country` parameter from the dropdown.
5. Click **OK**.

**Result:** The `Sales` table is now filtered to show only data where the `Country` column equals the current value of the `p_Country` parameter ("USA").
### How to Change the Parameter's Value
- **In Power BI Desktop:** Go to the **Home** tab and click **Transform data > Edit parameters**. A simple dialog will appear where you can change `p_Country` to "Germany." When you click OK, the `Sales` query will automatically re-run and show data for Germany instead.
- **In the Power BI Service:** After you publish the report, you can go to the **dataset's settings** and change the parameter's value there. ==This allows you to change the data the report is based on without having to republish the PBIX file.== For example, you could have one version of the report in the service that points to your production database and a copy that uses a parameter to point to the test database.
---
## 9. Getting Data from a NoSQL Database

NoSQL databases are different from the relational SQL databases discussed earlier. They don't store data in the traditional table format of rows and columns. Instead, they often store data in a hierarchical, document-like structure, such as JSON.
- **Common Sources:** Azure Cosmos DB, MongoDB, etc.
	- Enter database details (name, URL, endpoint Key blade) after Get Data -> Azure  -> Azure Cosmo DB 
	- Enter account key (for Azure Cosmos DB)
- **Key Challenge:** When you import data from a NoSQL source, it often arrives in Power Query as a single column containing nested data structures called **Records** or **Lists**. Your primary job is to flatten this data into a traditional, tabular format.

When you import a JSON file from a NoSQL database into Power Query, it's often necessary to extract and normalize the data first. This is because JSON data is often stored in a nested or unstructured format, which makes it difficult to analyze or report on directly.
>[!Note]
>- **Transformation -> Parse JSON**: this operation is used when a column of the table contains a JSON documents.  
>- When loading JSON file, Power Query automatically flattens a JSON file into a table.
#### Step 1: Drill Down into the Data
Your initial import will likely look like a single line of text with the word **"Record"** or **"List"**. This represents the top level of the JSON structure. You need to click on this word to drill down into the data.
- **What you see:** A single cell containing the word `Record` (if the JSON is a single object) or `List` (if the JSON is an array of objects).
- **Action:** Click on the word `Record` or `List`. Power Query will then navigate inside that object, showing you the key-value pairs it contains. You might need to repeat this step if your data is nested several layers deep.
#### Step 2: Convert to a Table
After drilling down, you will see a list of the records that make up your data. Now you need to convert this list into a proper table with columns.
- **What you see:** A list of `Record` objects. At the top of the Power Query interface, you will see a banner with a **"To Table"** button.
- **Action:**
    1. Click the **"To Table"** button on the ribbon.
    2. A dialog box will appear. You can just click **OK** without changing the default settings.
    3. This creates a new column (often named `Column1`) containing your `[Record]` objects.
    4. Click the **Expand** icon (↔️) on the `Column1` header.
    5. Select all the fields you want to transform into columns and click **OK**.
##### Examples: 
```JSON
[
    {
      "CustomerID": "ALFKI",
      "CompanyName": "Alfreds Futterkiste",
      "Country": "Germany"
    },
    {
      "CustomerID": "ANATR",
      "CompanyName": "Ana Trujillo Emparedados y helados",
      "Country": "Mexico"
    },
    {
      "CustomerID": "ANTON",
      "CompanyName": "Antonio Moreno Taquería",
      "Country": "Mexico"
    }
]
```

---
## 10. Connecting to Online Services

Online services are cloud-based software-as-a-service (SaaS) applications that you use for business operations, such as customer relationship management (CRM) or financial planning. Power BI offers a wide range of dedicated connectors for these services, which simplifies the process of getting data.
- **Common Sources:** Dynamics 365, Salesforce, Google Analytics, Azure Synapse Analytics.
- **Benefit:** These connectors are specifically designed to work with the data structure of the service. They provide a curated list of tables and entities, making it much easier to find and import the data you need compared to connecting to a raw database.
### The Connection and Authentication Process

Connecting to an online service is a secure process that requires you to prove you have permission to access the data
1. **Select the Connector:** Choose **Get Data** and find the specific connector for your service (e.g., **Salesforce Objects**).
2. **Provide URL (if required):** Some connectors may ask for a specific URL for your organization's environment.
3. **Authenticate:** This is the key step. You will be redirected to a sign-in page for that online service. You must sign in with your work or organizational account credentials. This process (often using OAuth2) grants Power BI permission to access the data on your behalf.
4. **Use the Navigator:** After you successfully sign in, the Power BI **Navigator** will appear, showing a list of available tables and objects from the service for you to import and transform.
---
## 11. Using Pre-Built Power BI Apps
For many popular online services, you can get started even faster by using a pre-built **Power BI App** (also known as a Template App).
- **What it is:** A Power BI App is a complete, ready-made solution that includes a pre-defined data model, a set of reports, and dashboards, all built by the service provider or a partner.
- **How to Get It:** You can find and install these apps from Microsoft AppSource, often directly from within the Power BI service.
- **How it Works:** When you install the app, it will ask you to connect to your data source (e.g., your Google Analytics account). Once you authenticate, the app will automatically populate the pre-built reports with your own data.
- **When to Use It:** An app is the perfect way to get instant insights from a service without having to build a report from scratch. You can also customize the reports and dataset after the app is installed.

---
## 12. Connecting to Azure Analysis Services (AAS)
Azure Analysis Services (AAS) is a powerful, enterprise-grade analytics engine in Azure. It's used to host tabular data models, which are often centrally managed by an IT or BI team. When you connect to AAS from Power BI, you are connecting to a pre-built, curated, and governed data model.
### The Connection Mode: Live Connection
Connecting to AAS uses a special type of data connectivity mode called a **Live Connection**. It's similar to DirectQuery but with some key differences.
- **What it is:** With a Live Connection, you are connecting directly to an existing data model that lives in Azure. The entire model—the tables, relationships, hierarchies, and measures—has already been created and is managed in AAS.
- **How it Works:** Power BI Desktop becomes a "thin" reporting tool. It sends live queries to the AAS model to get the data needed for visuals, but the data and the model logic are never imported into your Power BI file.
### How to Connect to AAS
1. Select **Get Data > Azure > Azure Analysis Services database**.
2. In the dialog box, you must provide the name of the **Server**. Your administrator will provide this server name (e.g., `asazure://westus.asallessons.windows.net/aw-ch-server`).
3. You can optionally specify a **Database**.
4. For the **Connectivity mode**, choose **Connect live**.
5. After authenticating with your organizational account, the **Navigator** will show you the available models (called perspectives or cubes) on that server. You select one model to connect to.
### Key Characteristics and Limitations of a Live Connection

|Feature|Behavior in a Live Connection|
|---|---|
|**Data Model**|You **cannot** change the data model. The relationships, tables, and existing measures are read-only from the AAS source. The "Data" view in Power BI Desktop is disabled.|
|**Power Query**|You **cannot** use the Power Query Editor. All data transformations are expected to have been done in the source AAS model.|
|**Measures**|You **can** create new **report-level measures** using DAX, but you cannot create calculated columns.|
|**Multiple Sources**|You are limited to a **single Live Connection** per Power BI report. You cannot combine data from an AAS model with data from an Excel file or another source in the same report.|
|**When to Use It**|✅ This is the standard method for enterprise BI, where a central team provides a single, governed "source of truth" model, and analysts connect to it to build their reports.|


---
## 13. Power Query Performance 
This is the **most important** area for optimization. A fast and efficient data import process is the foundation of a high-performing report. The goal is to reduce the amount of work Power BI has to do by pushing as much of the transformation work as possible back to the data source.
### The Core Concept: Query Folding
[[Power Query Folding]]
- **What it is:** Query folding is the process where Power Query translates your transformation steps (like filtering, removing columns, grouping, etc.) into a single, native query language (like SQL) that is executed directly by the source database.
- **Why it Matters:** More efficiency in data refreshes and incremental refreshes. It is dramatically more efficient to have a powerful SQL server filter billions of rows down to the one million you need than it is to import all one billion rows into Power BI and then filter them. Query folding pushes the work to the source.
- **How to Check:** In the Power Query Editor, right-click on the last applied step in your query. If the **"View Native Query"** option is clickable (not greyed out), it means that query folding is successfully happening up to that step. If it's greyed out, folding has stopped.
### Query Diagnostics 

### Key Optimization Techniques
1. **Process as much data as possible in the original data source (filtering or removing rows)**
    - **Remove Unnecessary Columns:** If you have 100 columns in your source table but only need 10 for your report, remove the other 90. This is the single most effective way to reduce model size and improve refresh times.
    - **Filter Unnecessary Rows:** If you only need data for the last three years, filter out all the older data.
    - **Order Your Steps:** Perform these filtering and removal steps **as early as possible** in your Power Query process. This ensures that later, more complex steps have less data to work on.
2. **Ensure Query Folding Works:**
    - When connecting to a relational source that supports folding (like SQL Server), prioritize using transformations that can be translated into the native query language.
    - **Transformations that typically work with folding:** Filtering rows, removing/renaming columns, changing data types, simple math operations, merging/joining tables from the same source.
    - **Transformations that often break folding:** Applying a custom M function, using an index column, or connecting to certain data sources (like flat files) that don't have a query language.
3. **Use native SQL queries.** When using DirectQuery for SQL databases, such as the case for our scenario, make sure that you aren't pulling data from stored procedures or common table expressions (CTEs).
4. **Separate date and time, if bound together.** If any of your tables have columns that combine date and time, make sure that you separate them into distinct columns before importing them into Power BI. This approach will increase compression abilities.
---
## 14. Data Import Errors 
[[Error Handling]]

| Name of Error                                         | Possible Reasons / When to Encounter                                                                                                                                                           | Solution(s)                                                                                                                                                                                                                               | Real-Life Example                                                                                                                                                                                                                      |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Query timeout expired** ⏳                           | The query is taking too long, exceeding the time limit set by the database administrator. This often happens when you try to import too many rows/columns or run a very complex SQL statement. | 1. **Reduce the data:** Pull fewer columns or rows.<br>2. **Simplify the query:** Remove complex joins or aggregations from your SQL.<br>3. **Import in chunks:** Create multiple simpler queries and merge them together in Power Query. | An analyst tries to import 10 years of detailed transaction data from the main company SQL Server. The query runs for over 5 minutes and fails because the server's timeout is set to 300 seconds.                                     |
| **We couldn't find any data formatted as a table** 📋 | You are importing data from an Excel file where the data exists as a simple range of cells, not a formally defined **Excel Table**.                                                            | 1. Open the Excel file.<br>2. Highlight your data range.<br>3. Press **Ctrl+T** to format the range as an official Excel Table.<br>4. Re-import the file into Power BI.                                                                   | A user gets a monthly report in an Excel sheet where data is just typed into cells A1 through G100. When they try to import this into Power BI, the error appears because the data isn't a named table.                                |
| **Couldn't find file** 📁                             | The source file has been **moved** to a new location, **renamed**, or your **permissions** to access the file have been changed.                                                               | 1. In Power BI, select **Transform Data**.<br>2. In the Query Settings pane, click the gear icon (⚙️) next to **Source**.<br>3. Update the file path to the new location.                                                                 | A report is built using a CSV file from the "Downloads" folder. The user later moves the CSV to a "Project Data" folder. The next time they try to refresh the report, this error occurs.                                              |
| **Data type errors** 🔢                               | Power BI is unable to correctly interpret the data type of a column from the source, often resulting in **blank columns** or error values.                                                     | **Fix the data type at the source.** If using SQL, use a `CAST` or `CONVERT` function to explicitly set the column's data type before it is imported into Power BI.                                                                       | A `PostalCode` column in a database is set as a numeric type. When it contains a mix of US zip codes (like "90210") and Canadian postal codes (like "M5V 2L9"), Power BI fails to interpret the text-based codes, resulting in blanks. |

---
## 15. Using PBDIS Files to Get Data 
A **PBDIS file** (`.pbids`) is a Power BI data source file that streamlines the "Get Data" experience by storing the connection information for a single data source.
### Purpose
The primary goal of a PBDIS file is to make it easier for new or beginner report creators to connect to the correct data source with the right settings, ensuring consistency across an organization.
### How it Works for a User
When a user opens a `.pbids` file:
1. Power BI Desktop launches.
2. It prompts the user for **credentials** to authenticate to the specified data source.
3. The **Navigator** window opens, showing the tables from that source for the user to select.
4. If the connection mode was not specified in the file, the user will be prompted to choose between **Import** or **DirectQuery**.
### How to Create a PBDIS File
#### Recommended Method: Export from Power BI Desktop
This is the easiest and recommended method as it auto-generates the file.
1. Open an existing `.pbix` file that is already connected to the data source.
2. Go to **File > Options and settings > Data source settings**.
3. Select the data source you want to export.
4. Click **Export PBIDS** and save the file.
#### Manual Method: Create in a Text Editor
You can manually create the `.pbids` file (which is a JSON file) in a text editor.
- You must specify the required connection inputs.
- You can optionally specify the connection `mode` as either `DirectQuery` or `Import`. If the mode is missing, the user will be prompted to choose.
### Limitations
- A PBDIS file can only contain connection information for **one single data source**.
- Connecting to sources with encrypted columns may cause errors.
## 16. Power BI Service: Considerations and Limitations
Some data sources have [limitations](https://learn.microsoft.com/en-us/power-bi/connect-data/service-get-data#considerations-and-limitations) and [other factors](https://learn.microsoft.com/en-us/power-bi/connect-data/power-bi-data-sources)
This section covers the key limits that apply to the Power BI service.
- **Semantic Model Size Limit:**
    - Semantic models stored in **shared capacities** (the standard for Power BI Pro) have a **1 GB** size limit.
    - To use larger semantic models, you must use **Power BI Premium**.
- **Distinct Values in a Column:**
    - When a Power BI semantic model is in **Import mode**, a single column can store a maximum of **1,999,999,997** distinct values.
- **Row Limit (for DirectQuery):**
    - When you use **DirectQuery**, Power BI imposes a limit on the results of any single query sent to the underlying data source.
    - If a query returns more than **1 million rows**, the query will fail and show an error.
    - **Note:** This is a limit on the _query result_, not the total number of rows in the source table, which can be much larger.
- **Column Limit (for the entire model):**
    - The maximum number of columns allowed across **all tables** in a single semantic model is **16,000**.
- **Data Source User Limit:**
    - A single user can have a maximum of **1,000** data sources defined in the Power BI service.
- **Single Sign-On (SSO) Considerations:**
    - **DirectQuery** models can enable SSO, which allows the security in the source system to be applied to the DAX queries executed by each user.
    - Querying an SSO-enabled DirectQuery model using a **Service Principal Name (SPN)** is **not supported**. You must use a **User Principal Name (UPN)** instead.
- **Authentication Dependency (Internet Explorer):**
    - Many data connectors in Power BI Desktop require **Internet Explorer 10 (or later)** to be installed on the machine.
- **Power BI Report Server Compatibility:**
    - Some data connectors are available in the special version of Power BI Desktop optimized for Power BI Report Server, but those data sources are **not actually supported** after you publish the report to the server. Always check the official documentation for the list of supported data sources for your version of Report Server.
- **Multiple Query Behavior:**
    - It is normal for Power BI to send **multiple queries** to a data source for a single user action. This is by design, as Power BI may send separate queries to get schema information, data for different visuals, or to populate caches.

---
## 17. Connect Power BI to OData API 
1. Open Microsoft Power BI.
2. Select **Get Data** > **Blank Query**.
    [![The Blank Query option under the Get Data menu item](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-create-blank-query.png)](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-create-blank-query.png#lightbox)
3. Select **Advanced Editor**.
    [![The Advanced Editor menu item](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-open-advanced-editor.png)](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-open-advanced-editor.png#lightbox)
4. Copy the following code, and paste it in the editor to pull all **Machine Actions** from your organization:
```M Query
let
	Query = "MachineActions",
    Source = OData.Feed("https://api.securitycenter.microsoft.com/api/" & Query, null, [Implementation="2.0", MoreColumns=true])
in
    Source
```
In some cases, sign-in is necessary 
5. Select **Edit Credentials**.
    [![The Edit Credentials menu item](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-edit-credentials.png)](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-edit-credentials.png#lightbox)
6. Select **Organizational account** > **Sign in**.
    [![The Sign in option in the Organizational account menu item](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-set-credentials-organizational.png)](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-set-credentials-organizational.png#lightbox)
7. Enter your credentials and wait to be signed in.
8. Select **Connect**.
    [![The sign-in confirmation message in the Organizational account menu item](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-set-credentials-organizational-cont.png)](https://learn.microsoft.com/en-us/defender-endpoint/media/power-bi-set-credentials-organizational-cont.png#lightbox)
    