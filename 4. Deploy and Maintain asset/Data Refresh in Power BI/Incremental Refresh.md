**Incremental Refresh** is a powerful feature in Power BI that automates the partitioning of large semantic models. Instead of fully reloading the entire dataset, it only refreshes a small, recent subset of data that has changed.
This is the standard solution for handling very large datasets, as it provides significant benefits:
- **Faster Refreshes:** Only the most recent data (e.g., the last 10 days) is refreshed, not the full history (e.g., 5 years).
- **More Reliable Refreshes:** Short-running connections are less likely to fail due to network problems.
- **Reduced Resource Consumption:** Uses less memory and CPU, both in Power BI and on the source data systems.
- **Enables Large Models:** Allows semantic models with billions of rows to exist without needing to refresh the entire model.
---

### 1. The Rolling Window Pattern

When you define an incremental refresh policy, the Power BI service handles all partitioning for you based on your settings
1. **Historical Period (Archive):** The long-term, historical data that you want to store (e.g., "Store data for the last 5 years"). This data is refreshed infrequently.
2. **Refresh Period (Incremental):** The recent, volatile data that needs to be updated (e.g., "Refresh data from the last 10 days").
3. **The Process:** With each refresh, only the "Refresh Period" partitions are updated. As time moves forward, partitions that are no longer in the refresh period become historical partitions. Historical partitions that are older than the "Historical Period" are automatically dropped from the model.
### 2. Critical Requirements

| **Requirement**     | **Details**                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Supported Plans** | <ul><li>**Incremental Refresh (Standard):** Supported on Power BI Pro, PPU, and Premium.</li><li>**Real-Time Data (with DirectQuery):** **Only** supported on PPU and Premium capacities.</li></ul>                                                                                                                                                                                                                                                                                |
| **Data Sources**    | <ul><li>Must be a structured, relational source like Azure SQL, Azure Synapse, etc.</li><li>The source **must support date filtering**, the table must contain at least one date column.</li><li>The Power Query query **must support Query Folding**. If folding is not possible, Power BI will try to pull the _entire_ table, which defeats the purpose of incremental refresh and will likely fail.</li><li>All partitions must query from a **single data source**.</li></ul> |
### 3. How to Configure Incremental Refresh

Configuration is a four-step process done in Power BI Desktop **before** publishing.
#### Step 1: Create Parameters in Power Query
- You must create two **case-sensitive** `Date/Time` parameters.
- **Name:** **`RangeStart`**
- **Name:** **`RangeEnd`**
- **Current Value:** Set a small, fixed window (e.g., 2 days) to limit the data loaded into Power BI Desktop. The service will override these values after publishing.
#### Step 2: Filter Data in Power Query
- Apply a **Custom Filter** on the date column of your fact table.
- Use the parameters to define the filter. The rule must be set to include the start but not the end, to prevent duplicate rows in partitions.
- **Correct Filter:** `is after or equal to` **`RangeStart`** AND `is before` **`RangeEnd`**
- **Note:** If your date column is an integer key (e.g., `20251231`), you must create a Power Query function to convert the `Date/Time` parameters to an integer to ensure query folding still works.
In Power Query Editor, add filtering steps:
1. Select **Add Step**, or modify the query directly in the formula bar.
2. Use the `Table.SelectRows` function to create filters that reference your parameters.
3. Apply separate filter steps for both the start and end date conditions.
```
#"Filtered Rows" = Table.SelectRows(Source, each [OrderDateKey] >= Int32.From(DateTime.ToText(RangeStart,[Format="yyyyMMdd"]))),
#"Filtered Rows1" = Table.SelectRows(#"Filtered Rows", each [OrderDateKey] < Int32.From(DateTime.ToText(RangeEnd,[Format="yyyyMMdd"])))
```
#### Step 3: Define the Policy
- In Power BI Desktop (Data or Model view), **right-click** your table and select **Incremental refresh**.
	- **Caution**:  If the Power Query expression for the table doesn't include a filter based on the `RangeStart` and `RangeEnd` parameters, the toggle isn't available.
- **Archive data:** Define your total historical period (e.g., store data from the last 5 years).
- **Incrementally refresh data:** Define your refresh period (e.g., refresh data from the last 10 days).
#### Step 4: Publish and Refresh
- **Publish** the report to the Power BI service.
- **Perform the first refresh** in the service. This initial refresh will take a long time as it loads all historical data (e.g., all 5 years).
- All subsequent refreshes will be much faster, as they only load the incremental period (e.g., the last 10 days).
- **Limitation:** After publishing an incrementally refreshed model, you **cannot download the .pbix file** back from the service.
### 4. Optional Settings in the Policy
- **Get the latest data in real time with DirectQuery (Premium only):**
    - This adds a special **DirectQuery partition** to the table.
    - This partition fetches any data that is _newer_ than the last incremental refresh, providing real-time data.
    - This is the feature that enables **"real-time data"** and requires a Premium or PPU capacity.
- **Only refresh complete days:**
    - Ensures that a partial day at the end of the refresh period is not included. This is useful for financial data that is only approved at the end of the day.
- **Detect data changes:**
    - Uses a separate date/time column (like `LastUpdated`) to identify and refresh only the periods where the data has changed, further reducing the amount of data to be refreshed.