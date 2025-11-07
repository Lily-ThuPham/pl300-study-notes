[Data lineage - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-data-lineage#show-lineage-for-any-artifact)
**Data lineage view** in Power BI gives you a visual map of the relationships and dependencies between all the items in a workspace. It shows you how data flows from the data source, through datasets and dataflows, and into the final reports and dashboards.

Think of it as a **family tree for your data**. You can clearly see which reports are "children" of which datasets, and where those datasets get their information.

---
### How Data Lineage Enhances Collaboration

![Screenshot of the data lineage view in Power BI.](https://learn.microsoft.com/en-us/power-bi/collaborate-share/media/service-data-lineage/service-data-lineage-view.png)
1. **Impact Analysis (Most Important Use Case):**
    - **What it is:** Before you change or delete a dataset, you can use the lineage view to see exactly which reports and dashboards depend on it. This prevents you from accidentally breaking reports that your colleagues rely on.
    - **Exam Scenario:** A question might ask, "You need to update a dataset. What is the best way to understand the impact on existing reports?" The answer would be to use the data lineage view.
2. **Troubleshooting and Quality Control:**
    - **What it is:** If a report is showing incorrect data, you can trace its lineage back to the data source. This helps you quickly identify if the problem is in the report itself, the dataset, or the original data source. It also highlights datasets that are failing to refresh.
    - **Exam Scenario:** You might see a question like, "Users are reporting that data in a specific dashboard is outdated. Where can you quickly check the refresh status of its underlying dataset?" Data lineage view provides this information.
3. **Discovering and Reusing Datasets:**
    - **What it is:** When new team members join a workspace, they can use the lineage view to understand the existing data architecture. It helps them find and reuse certified or promoted datasets instead of creating duplicate ones, which is a key best practice.
    - **Exam Scenario:** A question could be, "How can a new team member identify which datasets are authoritative and ready for use?" The lineage view, with its highlighting of endorsed datasets, is the answer.
4. **Understanding Complex Workspaces:**
    - **What it is:** In a large workspace with dozens of items, the lineage view provides a clear, interactive map of how everything is connected. It simplifies complexity and makes the workspace easier to navigate and manage for the entire team.
    - **Exam Scenario:** You might be asked to describe a tool for visualizing the relationships between all artifacts in a complex workspace. Data lineage view is the feature designed for this.

The data lineage view uses a set of cards and icons to represent different Power BI items (or artifacts) and their status.
To access lineage view, go to the workspace list view. Tap the arrow next to **View** and select **Lineage**.

| Symbol/Feature           | Representation & Meaning                                                                                                                                                                                                                                                                                                           |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Artifact Cards**       | Each item—data source, dataflow, dataset, report, dashboard—is shown as a card with its corresponding icon and name.                                                                                                                                                                                                               |
| **Data Source Icon**     | Represents the origin of your data, such as SQL Server, an Excel file, or another source.                                                                                                                                                                                                                                          |
| **Gateways**             | If a data source is connected via an on-premises gateway, the gateway information is added to the data source card.                                                                                                                                                                                                                |
| **Dataset Icon**         | Represents the data model you built in Power BI. It's the central hub connecting data sources to reports.                                                                                                                                                                                                                          |
| **Report Icon**          | Represents a Power BI report with one or more pages of visuals.<br>If a report in the workspace is built on a semantic model or a dataflow that's located in another workspace, you see the source workspace name on the card of that semantic model or dataflow. Select the name of the source workspace to go to that workspace. |
| **Dashboard Icon**       | Represents a dashboard, which is a canvas containing tiles pinned from reports.                                                                                                                                                                                                                                                    |
| **Endorsement Badges**   | A **Promoted** (silver) or **Certified** (gold) badge will appear on datasets that have been endorsed, signaling to users that they are high-quality, authoritative sources.                                                                                                                                                       |
| **Refresh Status**       | A warning icon (⚠️) will appear on a dataset or dataflow if its last scheduled refresh failed. You can hover over it to see the time of the last refresh and a failure reason.                                                                                                                                                     |
| **Sensitivity Label**    | If a sensitivity label (e.g., "Confidential") has been applied to an artifact, it will be displayed on the card.                                                                                                                                                                                                                   |
| **Double arrows**        | Select the double arrows under the artifact to see its lineage.[Data lineage - Power BI \| Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-data-lineage#show-lineage-for-any-artifact)                                                                                                       |
| **"More options" (...)** | Clicking the ellipsis on any card provides a menu of actions, such as viewing details, managing settings, or analyzing in Excel.                                                                                                                                                                                                   |
### Permissions
- You need a Power BI Pro license to see lineage view.
- Lineage view is available only to users with access to the workspace.
- Users must have an Admin, Member, or Contributor role in the workspace. Users with a Viewer role can't switch to lineage view.

