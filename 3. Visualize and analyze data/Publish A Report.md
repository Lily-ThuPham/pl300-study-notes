Power BI provides two hosting options:
1. Power BI service, a cloud-based hosting 
2. Power BI report server on-premises hosting.

### Power BI Service reports and analytics 
Power BI service, offered by Microsoft and integrated with Azure and Office 365, is a cloud-based platform for hosting reports.
Purposes of publishing reports to Power BI Service:
- Create business dashboard
- Share reports and dashboards within and outside your organization 
- Manage assets (reports, datasets, dashboards, etc.) and create audience-specific workspaces and apps.
##### Analytical tools and features on Power BI service:
- Dataflows
- Shared dataset
- Datamart
- Data lineage
- Sensitivity labels
- Deployment pipelines
- Workspaces
- Apps
## What is published to Power BI service?
When you publish a Power BI file from the desktop to the Power BI service, you publish the following components:
- The data tables and columns
- The data model and schema design
- Any reports and visualizations you have created in Report view.
- All DAX measures you have created in the data model.
- - The reports and any semantic model (datasets) you have in the Power BI desktop will be published to Power BI service with the same name.
- If your Power BI desktop file has _**sensitivity labels**_, the reports published to Power BI service will inherit the labels.
- If your Power BI report has a DirectQuery connection with an on-premises SQL Server database, you must install and configure a data gateway to access the reports from Power BI service.
- _**Themes**_: Power BI also lets you keep this original theme or switch to the dashboard's theme when pinning a visual element as a tile to the dashboard.
## Replacing the existing file published from Power BI desktop
If you edit a report in Power BI Desktop after publishing it to Power BI service, you must publish it again to update both the report and its datasets in the service.
When replacing an existing file:
- You cannot publish two models with the same name.
- If you rename or delete a column or DAX measure in your Power BI desktop file, the visualization will be broken based on these changes.
- When you make changes to a Power BI file and republish it, a message indicates the number of reports, dashboards, and workspaces impacted by the change and asks you to confirm that you want to replace the current model with a modified one.