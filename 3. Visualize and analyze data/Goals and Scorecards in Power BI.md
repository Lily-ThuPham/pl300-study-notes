The **Goals** feature in Power BI (often referred to as **Metrics** or **Scorecards**) allows organizations to curate key business objectives and track their progress against measurable targets within a single, collaborative pane. It promotes accountability, alignment, and visibility for teams.
**APPLIES TO:** ![](https://learn.microsoft.com/en-us/power-bi/includes/media/no-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service

---
### 1. Key Components
- **Goal/Metric:** A specific business objective you want to track (e.g., "Increase Monthly Sales"). It typically has a **Current** value and a **Target** value.
- **Scorecard:** A collection of related Goals, often belonging to a specific team or initiative (e.g., "Sales Team Q4 Scorecard").
- **Submetrics:** You can break down a main Goal into smaller, contributing submetrics for more granular tracking.
- **Check-ins:** A feature allowing users to manually update the status or value of a Goal and add notes, providing context for progress or setbacks.
![Screenshot of goals page with goals, scorecards, and samples.](https://learn.microsoft.com/en-us/power-bi/create-reports/media/service-goals-introduction/power-bi-goals-hub.png)
### 2. Creating Scorecards and Goals
#### Creating a Scorecard
1. In the Power BI service navigation pane, select **Metrics** to open the Metrics hub.
2. Select **New metric set**.
3. Give the scorecard a name and select a workspace to save it in. Power BI automatically creates the scorecard and an associated semantic model to store the goals data.
#### Creating a Goal
1. Within the scorecard (in Edit mode), select **Add metric**.
2. Define the **Metric name** and **Owner**.
3. Set the **Current** and **Target** values. You have two options:
    - **Manual Entry:** Type the values directly into the fields.
    - **Connect to data:** Link the Current and/or Target value to a specific data point on an existing Power BI report visual.
        - Click **Connect to data**.
        - Browse and select the desired report.
        - Navigate to the visual containing the data point.
        - Select the specific data point, visual, legend, or axis value you want to connect to.
        - Click **Connect**. Power BI will automatically track this value.
4. Set the **Status**, **Start date**, and **End date** for the goal.
5. Select **Save**.
### 3. Key Features and Settings
- **Tracking Cycle:** By default, goals are tracked daily. You can change this cadence (e.g., weekly, monthly) in the goal's **Settings** tab within the **Details** pane. This affects trend calculations but not the data refresh frequency.
- **Sharing:** You can share scorecards like dashboards using the **Share** button. Recipients need appropriate licenses (see below). Workspace roles (Admin, Member, Contributor) determine if shared users can edit the scorecard.
- **Metrics Hub:** The central place in the Power BI service to view recommended scorecards, recent ones, favorites, and those shared with you.
### 4. Data Updates for Connected Goals
- Connected goal values are **not** updated in real-time.
- They update only when the **underlying semantic model** that the source report is based on **is refreshed**.
- If the source semantic model is not on a scheduled refresh, the connected goal values will not update automatically.
### 5. Licensing Requirements

|**Action**|**Minimum Requirement**|
|---|---|
|Author & Share Scorecards/Goals, Perform Check-ins|**Power BI Pro** or **PPU** license|
|View Scorecards/Goals|**Power BI Pro** or **PPU** license **OR** **Free** license if the content is in a **Premium/Fabric Capacity**|
|View Samples & Author in "My Workspace"|**Free** license|
### 6. Considerations and Limitations
- **History:** Connecting to a single data point will not pull its history. You must connect to a time series visual to get historical data.
- **Manual Updates:** Only manually entered goals can be updated during a check-in. Connected goals pull data directly from the report.
- **Workspace Role:** You need a Contributor or Owner role in a workspace to create a scorecard there.
- **Unsupported Features:**
    - Row-Level Security (RLS) is not supported.
    - Publish-to-web.
    - Business-to-business (B2B) sharing across tenants.
    - Embedding in SharePoint or via Power BI embedded analytics.
    - Bring Your Own Key (BYOK).
    - Multi-Geo capacities.
- **Subgoal Limit:** Maximum of four levels of subgoals.