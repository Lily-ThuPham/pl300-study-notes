### Changing Data Source Settings
This is vital for maintaining the accuracy of your reports when a data source location or its credentials change.
1. In Power BI Desktop, navigate to **File > Options and settings > Data source settings**.
2. From the list, select the data source you need to update.
3. Click **Change Source...** to modify its details (e.g., a new file location or server name).
4. Click **Edit Permissions...** to update credentials.
5. Select **OK** to confirm and validate the new connection.

### Grouping Data Sources (in Power Query)
Grouping queries in the Power Query Editor helps to organize your workflow, especially in projects with many data sources.
1. In Power BI Desktop, select **Transform Data** to open the Power Query Editor.
2. In the **Queries** pane on the left, right-click in a blank space and select **New Group**.
3. Name the new group (folder).
4. To add queries to the group, simply **drag and drop** them into the folder.
### Managing Data Source Permissions (in Power BI Service)
This is crucial for safeguarding sensitive information and controlling who can access or modify your published datasets.
1. Log into the **Power BI Service** and navigate to your workspace.
2. Hover over the dataset you want to manage, select the **More options (...)** ellipsis, and choose **Manage permissions**.
3. In the **Manage permissions** window, select **Add User**.
4. Enter the user's email address and use the checkboxes to grant specific permissions.
5. To restrict a user from modifying the dataset, **uncheck** the `Allow recipients to modify this dataset` box.
6. You can also manage existing users' access levels (**Reshare**, **Build**, **Write**) or **Remove Access** by clicking the ellipsis next to their name.
### Limitation and considerations of data sources 
- Data sources for the Power BI service are limited to 1000 data sources per user.
- The total number of columns that can be used in all the tables within a dataset is restricted to 16,000 columns. This limitation applies to the Power BI service and the datasets used in Power BI Desktop.
- Several of the data connectors used in Power BI Desktop require Internet Explorer 10, or a newer version, for authentication.
- Some data sources may need to satisfy specific requirements to work properly.