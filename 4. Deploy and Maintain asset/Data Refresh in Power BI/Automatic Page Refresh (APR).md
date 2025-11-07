_✅ Power BI Desktop ✅Power BI Service_
**Automatic Page Refresh (APR)** enables a report page to automatically query for new data from ==**DirectQuery** sources== at a predefined cadence, making it ideal for monitoring critical, fast-changing events.
[[Storage modes in Power BI#DirectQuery mode]]

---
## Refresh Types
There are two types of automatic page refresh, each serving a different purpose.

| Refresh Type         | How It Works                                                                                                                       | When to Use It                                                                                                                          | Premium Required?                              |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| **Fixed Interval**   | Refreshes all visuals on a page at a constant, predefined interval (e.g., every 5 minutes).                                        | For continuous monitoring scenarios where data updates at a predictable rate.                                                           | No (but intervals are much faster in Premium). |
| **Change Detection** | A specific **DAX measure** is polled at a set interval. Visuals on the page only refresh if the value of that measure has changed. | For high-frequency data sources. It is more efficient as it reduces queries, only refreshing the full report when a change is detected. | **Yes**. Only supported in Premium workspaces. |
## Configuration in Power BI Desktop
APR is configured on a per-page basis in the **Format** pane under the **Page refresh** section. This section only appears if you are connected to a **DirectQuery** source.
- **Fixed Interval Setup:**
    1. Turn the **Auto page refresh** toggle **On**.
    2. Set the desired refresh **interval** (e.g., 10 minutes).
- **Change Detection Setup:**
    1. Select **Change detection** as the type.
    2. Click **Add change detection** and either select an existing measure or create a new one (e.g., `COUNTROWS(Sales)`).
    3. Define the interval at which Power BI will **check for changes** in that measure.
## Performance and Interval Considerations
- **Best Practice:** The refresh interval should match your expected **new data arrival rate**. If data arrives every 15 minutes, your interval should not be less than 15 minutes.
- **Query Time:** Use the **Performance Analyzer** to ensure your visual queries can complete within your configured interval. If a query takes 5 seconds to run, your interval must be longer than 5 seconds.
- **Query Load:** Power BI runs APR queries at a **lower priority**. If a refresh cycle hasn't finished, Power BI will wait for it to complete before issuing the next one.
## Restrictions in the Power BI Service
The minimum allowed refresh interval depends on the workspace type.

| Workspace Type   | Fixed Interval (FI)                                           | Change Detection (CD)                                             |
| ---------------- | ------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Shared (Pro)** | Minimum interval is **30 minutes**.                           | **Not available**.                                                |
| **Premium**      | Minimum interval can be set by an admin (as low as 1 second). | **Available**. Minimum execution interval can be set by an admin. |
