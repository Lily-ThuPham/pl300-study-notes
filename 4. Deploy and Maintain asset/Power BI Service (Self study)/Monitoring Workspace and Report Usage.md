[Monitor usage metrics in workspaces](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-modern-usage-metrics) 
[Report usage metrics](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-usage-metrics). 
### 1. The Importance of Monitoring Workspace Usage
Monitoring how reports and dashboards are **_accessed, used, and shared_** provides a clear view into the effectiveness and reach of your data solutions. The insights gathered from this data enable data analysts to make informed decisions on **_content optimization, security, and resource allocation_**.
Usage metrics act as a feedback loop, showing how content is being used within the organization. These data-driven insights can help you identify which reports are highly valued and which may be underutilized.
### 2. Usage Metrics Reports
Monitoring is primarily performed using the **Usage Metrics Reports** available in the ==Power BI service==. These reports provide insights into user engagement and report performance.
#### 2.1 Original Usage Metrics Report
- **Focus:** Provides metrics for a single, **individual report**.
- **Key Metrics Tracked:**
    - Number of views.
    - Number of shares.        
    - User interactions on a per-report basis.
#### 2.2 New Workspace Metrics (Preview Feature)
This enhanced feature expands monitoring from individual reports to the **entire workspace**, providing more comprehensive insights.
- **Aggregated Metrics:** Encompasses all the KPIs from the original usage reports and adds new **report performance** information.
- **Performance Data:** Tracks the **typical opening time** of reports, including daily and weekly breakdowns, which helps in identifying and resolving performance bottlenecks.
- **Workspace-Wide View:** Provides performance and usage information on **all reports** within the workspace, allowing for a holistic view of content effectiveness.
### 3. Prerequisites for Accessing Usage Metrics
To run and access the usage metrics data, the following prerequisites must be met:
- You must have a **Power BI Pro** or **Premium Per User (PPU)** license.
- The usage metrics feature captures usage information from **all users**, regardless of the license they are assigned.
- You must have **edit access** to the specific report or workspace to view its usage metrics.
- Your Power BI **admin must enable** the usage metrics feature for content creators in the tenant settings.
### 4. Creating a Workspace Usage Report
The **Workspace Usage Report** is an enhanced monitoring feature in Power BI that provides detailed insights into workspace activity and user engagement. It allows you to analyze how all reports within a workspace are being used, helping you to optimize your content and improve efficiency.
#### 4.1 How to Generate the Usage Metrics Report
1. From the Power BI service, navigate to the desired **Workspace**.
2. Hover over a specific report, select the **More options (...)** menu.
3. Select **View Usage Metrics report**. If this is the first time, Power BI will take a few moments to create the report.   
#### 4.2 Understanding the Original Usage Report
The initial usage report provides a basic overview of a single report's engagement.
- **Key Metrics:**
    - **Report Views:** The total number of times the report has been opened.
    - **Unique Views by Day:** The number of different users who opened the report each day.
    - **Users List:** A list of all users who have accessed the report.
- **Filtering:** You can use slicers to filter the usage data by:
    - **Distribution Method:** (e.g., shared directly vs. accessed through the workspace).
    - **Platform:** (e.g., web browser vs. mobile device).
    - **Report Pages:** To see the usage of individual pages within the report.
#### 4.3 Enabling and Navigating the New Workspace Usage Report
To access the enhanced features, toggle the **"New usage report on"** switch at the top of the usage report. This transforms the single-page report into a more comprehensive, multi-page analysis of the entire workspace.
This new report contains four distinct pages:
- **Report Usage Tab:** Provides a more detailed breakdown of usage for a single report with updated visualizations. You can see metrics like the percentage of access from different platforms (e.g., web vs. mobile) and the distribution of views across different report pages.
- **Report Performance Tab:** This page is crucial for troubleshooting. It shows the report's **loading time** broken down by date, user, country, and the internet browser used.
- **Report List Tab:** This provides a workspace-wide overview, allowing you to monitor the usage and performance of **all reports in the workspace** from a single view, making it easy to compare them.
- **FAQ Tab:** Contains a detailed guide and definitions for all the metrics and terminology used in the new usage monitoring report. 
### 5. Summary of the Workspace Usage Metrics Report

| Page                      | Metric / Visual                | Description                                                                                                                         |
| ------------------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Report usage** 📊       | **Report opens**               | Counts each unique landing on the report, showing how often it has been accessed.                                                   |
|                           | **Report page views**          | Counts the total views across all individual pages within a report.                                                                 |
|                           | **Unique viewers**             | Counts the number of distinct individuals who opened the report at least once.                                                      |
|                           | **Report open trend**          | Demonstrates changes in the view count over the selected time period.                                                               |
|                           | **Distribution**               | Shows how users accessed the report (e.g., through a workspace, a shared link, or an app).                                          |
|                           | **Platform**                   | Indicates if the report was accessed via the Power BI service, a mobile device, or Power BI Embedded.                               |
|                           | **Users**                      | Lists the individual users who opened the report, sorted by their total view count.                                                 |
|                           | **Pages**                      | Slices the usage data by the different pages viewed within the report.                                                              |
| **Report performance** ⏱️ | **Typical opening time**       | Shows the **median** time (in milliseconds) it takes to open the report.                                                            |
|                           | **Opening time trend**         | Analyzes how the report opening time has changed over the selected period.                                                          |
|                           | **Daily performance**          | Shows the performance for the 25th, 50th, and 75th percentiles of open-report actions for each day.                                 |
|                           | **7-day performance**          | Shows each date's performance trend across the previous seven days.                                                                 |
|                           | **Consumption**                | Indicates how the report was opened (e.g., via Power BI service, mobile, embedded).                                                 |
|                           | **Browsers**                   | Provides insights into which internet browsers (e.g., Chrome, Edge, Firefox) were used to open the report.                          |
| **Report list** 📋        | **Active reports**             | Identifies all reports that are currently being used across the entire workspace.                                                   |
|                           | **Total views**                | Aggregates the total number of views for all reports in the workspace.                                                              |
|                           | **Total viewers**              | Summarizes the total number of unique viewers for all reports in the workspace.                                                     |
|                           | **Unused reports**             | Counts the number of reports that have been unopened or inactive over a specific period.                                            |
|                           | **Table**                      | A detailed summary table that provides usage, trend, and interaction data for every report in the workspace.                        |
| **FAQ** ❓                 | **Frequently Asked Questions** | An informational page that provides answers and definitions for key terms and metrics used in the report, such as "What is a view?" |
### 6. Usage Metrics Report Credentials

#### 6.1 Understanding the Usage Metrics Report Dataset
When a user creates a **Usage Metrics Report** within a workspace, Power BI automatically generates a corresponding dataset to hold this usage data.
- **Creation and Ownership:** The dataset is auto-generated, and the user who creates the usage report is designated as the **dataset owner**.
- **Refresh Schedule:** This dataset has a **fixed daily refresh schedule** that cannot be changed by the user. For the refresh to run successfully, it requires valid credentials from the dataset owner.
#### 6.2 Common Causes of Refresh Failure
The daily refresh for the usage metrics report dataset can fail, causing the usage data to become stale. This typically occurs because the dataset owner's credentials become invalid. The common reasons for this are:
- The dataset owner's credentials **expire**.
- The dataset owner is **removed from the workspace**.
- The dataset owner **leaves the organization**.
In any of these cases, a new user must take over ownership of the dataset and update the credentials to restart the daily refresh.
#### 6.3 How to Update the Credentials
A new user, typically a workspace admin, must log in and follow these steps to become the new dataset owner and update the credentials.
1. Navigate to any report in your workspace, select the **More options (...)** menu, and choose **View usage metrics report**.
2. On the usage metrics report page, select the **More options (...)** menu at the top and select **View dataset**. This will take you to the workspace list with the usage metrics report dataset highlighted.
3. In the dataset's settings, scroll down to the **Data source credentials** section.
4. If you are not the current owner, you must first click the **Take over** button. Confirm the action in the window that appears.
5. Once you are the owner, expand the **Data source credentials** section again and select **Edit credentials**.
6. Sign in with your Power BI credentials to re-establish the connection. After a few moments, you will receive a notification that the credentials were updated successfully.
This process ensures that the scheduled daily refresh of the usage metrics report will resume.
