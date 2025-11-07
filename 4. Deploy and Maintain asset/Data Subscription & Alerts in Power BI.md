## Data Subscription 
A **subscription** in Power BI automatically sends an email containing a snapshot and a link to a report page or dashboard at specific times or intervals.

| **Feature**              | **Description**                                                                                                                                                                                                                      |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Purpose**              | To automate the delivery of report content to users on a regular schedule.                                                                                                                                                           |
| **What is Delivered**    | An email containing: • A snapshot image of the report page/dashboard. <br>• A link to view the content in the Power BI service. <br>• **(Premium Capacity Only):** Optionally, the full report attached as a PDF or PowerPoint file. |
| **How it's Triggered**   | **Time-driven schedule:** You define the frequency (Hourly, Daily, Weekly, Monthly) and the specific time for the email to be sent.                                                                                                  |
| **Configuration**        | Configured per-user in the Power BI service by clicking the **"Subscribe"** button on a report or dashboard.                                                                                                                         |
| **Permissions Required** | Users need a **Pro or PPU license** to create subscriptions (unless the content is in Premium). They also need **view access** to the report/dashboard.                                                                              |
| **Data Context**         | The snapshot reflects the data based on the **permissions of the person creating the subscription**. Filters applied _at the time of creation_ can be included.                                                                      |
In **Power BI tenant (Fabric Admin portal)** settings, you can configured subscriptions with features described:
- **Users can set up email subscriptions:** This setting enables or disables the ability for users within your organization to create email subscriptions for reports and dashboards.
- **B2B guest users can set up and be subscribed to email subscriptions:** This setting specifically controls whether external Business-to-Business (B2B) guest users are allowed to create and receive email subscriptions for content shared with them. Turning this off prevents B2B guests from subscribing themselves.
- **Users can send email subscriptions to guest users:** This setting controls whether users _within_ your organization can add external guest users as recipients to email subscriptions. Turning this off prevents internal users from subscribing external guests.
### Requirements

| **Requirement**           | **For Creating Your Own Subscription**              | **For Subscribing Others**                                                                                                                               |
| ------------------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Power BI License**      | Pro or PPU (or Free if content is in Premium)       | **Pro or PPU**                                                                                                                                           |
| **Workspace Access**      | Permissions to view the content                     | **Contributor, Member, or Admin** role in the workspace                                                                                                  |
| **Tenant Admin Settings** | Subscriptions must be enabled in the Admin portal.  | Subscriptions must be enabled.                                                                                                                           |
| **External User (B2B)**   | Can subscribe themselves (if admin setting allows). | Cannot subscribe _other_ external users. Internal users can subscribe external guests only if the content is in Premium and the admin setting allows it. |
### How to Create a Subscription
1. Open the report or dashboard in the Power BI service.
2. Select **Subscribe** > **Create a subscription** from the top menu bar.
3. In the **Subscriptions** pane:
    - **Recipients:** Add individual email addresses or **group email aliases**.
    - **Frequency:** Set the schedule (Hourly, Daily, Weekly, Monthly, After data refresh not for paginated reports).
    - **Time & Time Zone:** Specify when the email should be sent.
    - **(Optional) Subject & Message:** Customize the email content.
    - **(Optional) Include/Exclude:** Choose to include a **Link**, **Preview image** (sensitivity labels are _not_ applied to previews), or **Full report attachment** (Premium/PPU only, respects sensitivity labels).
	    - The size of the attachment is limited to no more than 20 pages and less than 25 MB.
    - **(Optional) Permissions:** Grant recipients permission to access the content.
    - **(Optional) Include my changes:** See section below.
![Screenshot of the Subscribe to emails screen.](https://learn.microsoft.com/en-us/power-bi/collaborate-share/media/end-user-subscribe/power-bi-report-subscribes.png)
4. Select **Save**
### Subscribing with Your Own Changes ("Include my changes")

![Screenshot showing the My changes section of the Subscriptions pane.](https://learn.microsoft.com/en-us/power-bi/collaborate-share/media/end-user-subscribe/power-bi-my-changes.png)
When you subscribe to a report (not a dashboard or paginated report) that someone else created or shared with you, you can apply your own filters, slicers, or other modifications and save that specific view within your subscription.
- **When it appears:** The **"Include my changes"** option only appears in the subscription pane _after_ you have applied _filters, slicers, spotlights, drills, or cross-highlighting_ to the report page that differ from the author's published view.
- _**Note**_ : The **Include my changes** field isn't available for dashboards or paginated reports.
- **How to use it:**
    1. Apply your desired filters/changes to the report page.
    2. Go to **Subscribe > Create a subscription** or edit an existing one.
    3. Under **More options**, check the box for **Include my changes**.
    4. You can use the **Preview** button to compare the original author's view with your modified view before saving.
    5. Select **Save** (or **Update** if editing).
- **Outcome:** The email snapshots sent by this subscription will reflect the report page with _your specific changes_ applied, rather than the default view.
### Using Group Email Aliases
Instead of adding individual email addresses, you can subscribe certain types of groups.

| Group type                                                                                                                                                                     | Supported in email subscriptions |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------- |
| [Microsoft 365 groups](https://learn.microsoft.com/en-us/microsoft-365/admin/create-groups/office-365-groups)                                                                  | No                               |
| [Distribution groups](https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups)                          | Yes                              |
| [Dynamic distribution groups](https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups)  | Yes                              |
| [Security groups](https://learn.microsoft.com/en-us/microsoft-365/admin/email/create-edit-or-delete-a-security-group)                                                          | No                               |
| [Mail-enabled security groups](https://learn.microsoft.com/en-us/microsoft-365/admin/create-groups/compare-groups?view=o365-worldwide#microsoft-365-groups&preserve-view=true) | Yes                              |
- **Premium Requirement for External Groups:** If the report/dashboard is hosted in a **Premium capacity**, you can subscribe group aliases even if they contain external users. Otherwise, you can only subscribe groups containing users within your organization's domain.
### 6. Managing Subscriptions
- **Your Subscriptions:** Users can manage all their own subscriptions across all workspaces via **Settings (gear icon ⚙️) > Power BI settings > General > Notifications**.
- **Workspace Subscriptions:** Users with **Admin** role in a workspace can view and manage _all_ subscriptions within that workspace (via **Manage all** in the subscription pane).
### 7. Key Considerations and Limitations
- **Data Context & RLS:** The snapshot image shows data based on the **permissions of the subscription creator**. Be cautious when subscribing others to reports with Row-Level Security (RLS).
- **Paginated Reports:** Allow setting specific parameter values per subscription, support various attachment formats, but do not support "After Data Refresh" frequency.
- **Unsupported Visuals:** Certain visuals (uncertified custom visuals, ESRI maps, Power Apps, etc.) will show an error symbol in the email snapshot.
- **Refresh Limits:** Subscriptions run based on the data available _after_ the latest semantic model refresh. They do not trigger a refresh themselves.
- **Automatic Pausing:** Subscriptions pause after two months of inactivity (no views) unless a subscription exists. The schedule is also disabled after four consecutive failures or credential issues.
## Data Alerts
### **Key Concepts 💡**

**Data alerts** are a feature in the **Power BI service** that automatically notifies you when data in your dashboards changes beyond limits you set. You can set alerts on specific visuals to monitor key metrics without having to constantly check a dashboard.
When a metric crosses a defined threshold, Power BI triggers a notification. This allows for proactive monitoring of business goals and key performance indicators (KPIs).
### **Where and How to Set Alerts**
- **Location:** Alerts can **only be set in the Power BI service**, not in Power BI Desktop or Power BI Mobile (though you can view notifications on mobile).
- **Visual Types:** Alerts can only be created on ==**KPIs**, **cards**, and **gauges**.==
- **Data Types:** Alerts only work with **numeric data types**.
- **Process:** To set an alert, you pin an eligible visual (KPI, card, or gauge) from a report to a **dashboard**. On the dashboard, you select the ellipsis (...) on the tile and choose "Manage alerts" to configure the threshold and notification frequency.
### **Limitations and Critical Rules**
- **Who Sees the Alert:** Alerts are **private to the user who creates them**. Even if you are the dashboard owner, you cannot see the alerts set by a colleague you shared the dashboard with, and they cannot see yours.
- **Licensing and Access:** You must have a **Power BI Pro** or **Premium Per User (PPU)** license to set alerts. You can set alerts on content in any workspace you can access.
- **Data Source and Refresh:**
    - Alerts work on data that is **refreshed**. For standard datasets (import mode), notifications are only sent **after a data refresh** runs.
    - Alerts do **not** work for tiles created from **streaming datasets** (push datasets) that are pinned _directly from the dashboard_ using "Add tile". However, if you first create a streaming dataset report visual and pin _that_ to the dashboard, you **can** set alerts on it. This is a subtle but important distinction.
    - For live connection datasets (like Analysis Services), Power BI checks for changes periodically, and alerts will trigger when the data is updated at the source.
- **Integrations:** You can use Power Automate (Flow) in conjunction with data alerts to trigger more complex workflows, like sending a message to a Microsoft Teams channel or creating a record in another system.
### **Sample Exam Questions 📝**

| No. | Question                                                                                                                                                                                                                                                            | Options                                                                                                                                                                                                                                                     | Correct Answer | Explanation                                                                                                                                                                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | On which of the following report visuals can you set a data alert after pinning it to a dashboard?                                                                                                                                                                  | A. A table visual.<br>B. A slicer.<br>==**C. A card visual showing total sales.**==<br>D. A map visual.                                                                                                                                                     | **C**          | Data alerts can only be set on **cards, KPIs, and gauges**. The other visual types are not supported for this feature.                                                                 |
| 2   | A user with a Power BI Free license is viewing a dashboard shared with them from a Premium capacity workspace. Why can't they set a data alert on a KPI tile?                                                                                                       | A. They need to be the owner of the dashboard.<br>B. Alerts are not supported in Premium capacity.<br>==**C. The user needs a Pro or PPU license.**==<br>D. The underlying data is from a streaming dataset.                                                | **C**          | The ability to **create** data alerts is a feature exclusive to users with a **Power BI Pro or PPU license**, regardless of the workspace capacity type.                               |
| 3   | You set an alert to notify you if "Inventory Count" drops below 100. The data is from a dataset that is refreshed once daily at 8:00 AM. At 10:00 AM, the source data is updated and the inventory count drops to 95. When will you receive the alert notification? | A. Immediately at 10:00 AM.<br>==**B. The next day at approximately 8:00 AM, after the scheduled refresh completes.**==<br>C. You will not receive an alert because the data source is not a live connection.<br>D. At the top of the next hour (11:00 AM). | **B**          | For datasets in import mode, the data alert function only checks the data **after a dataset refresh**. The trigger will only occur after the next scheduled refresh successfully runs. |
