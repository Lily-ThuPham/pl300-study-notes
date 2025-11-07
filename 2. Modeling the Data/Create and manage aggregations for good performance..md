***Aggregations** (a useful feature within composite mode) are pre-calculated summary tables that improve query performance.* 
[user-defined aggregations](https://learn.microsoft.com/en-us/power-bi/transform-model/aggregations-advanced) in Power BI and how to [configure](https://learn.microsoft.com/en-us/power-bi/enterprise/aggregations-auto) them.
Dimensional data sources, like data warehouses and data marts, can use [relationship-based aggregations](https://learn.microsoft.com/en-us/power-bi/transform-model/aggregations-advanced#aggregation-based-on-relationships). Hadoop-based large-data sources often [base aggregations on GroupBy columns](https://learn.microsoft.com/en-us/power-bi/transform-model/aggregations-advanced#aggregation-based-on-groupby-columns).
# Benefits of aggregations to performance 
- **Enhancing Query Speed**: Aggregated data is cached, using fewer resources and speeding up query performance.
- **Faster Refreshes**: Smaller cache sizes reduce refresh times, delivering data to users more quickly.
- **Model Size Management**: Helps reduce and maintain the size of large semantic models.
- **Future Proofing**: Proactively mitigates potential performance and refresh issues as the model grows.
# Create aggregations
Before creating aggregations, consider the granularity level (e.g., daily, monthly, yearly).
Different ways to create aggregations:
- Create a table with aggregation and import it into Power BI
- Create a view for aggregation and import that view 
- User Power Query Editor to create aggregations step-by-step. 
**Example:**
If you have a `FactInternetSales` table and you want to aggregate _sales_ by `OrderDateKey`, `CustomerKey`, and `ProductSubCategoryKey`, you would:

1. Select `FactInternetSales` in Power Query Editor.
2. Expand `ProductSubCategoryKey` from the related `Product` table.
3. Use **Group By** to group by `OrderDateKey`, `CustomerKey`, and `ProductSubCategoryKey`.
4. Sum the `SalesAmount` column.
5. Rename the resulting table to `AggregatedSales`.
6. Load the table into your model.
When creating an aggregation, you must reference the data model's fact table to keep the original table intact.
## After creating aggregations 
Before using the aggregation in the reports, you need to establish relationships, configure storage mode and manage the aggregations. 
- Establish the relationships with other existing tables 
- **Storage Mode:** Set the storage mode of the aggregated table to **"Import"** to store it in Power BI's memory for faster access.
- **Dual Storage Mode:** If necessary, consider setting the dimension tables to **_dual storage mode_** to allow them to act both as direct query and import sources.
- **Regular Updates:** Ensure that the aggregations are updated as the underlying data changes. This is crucial for maintaining accuracy and relevance.
- **Performance Monitoring:** Monitor the performance of your reports and visuals after implementing aggregations. If you notice any performance issues, you may need to adjust the aggregations or consider other optimization techniques.
- **Scalability:** If you anticipate future growth in your data volume, create and manage aggregations proactively to ensure that your solution can scale smoothly.

|Table on the _many_ sides|Table on the _1_ side|
|---|---|
|Dual|Dual|
|Import|Import or Dual|
|DirectQuery|DirectQuery or Dual|
## Manage aggregation 

### 1. Configuring Aggregations in Power BI Desktop
[User-defined aggregations - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/transform-model/aggregations-advanced#aggregation-based-on-relationships)
Once both tables are in your model, you must tell Power BI how to use the aggregation table.
1. In any view in Power BI Desktop, find your aggregation table (e.g., `Sales Agg`) in the **Data pane**.
2. **Right-click** the table and select **Manage aggregations**.
3. The **Manage aggregations** dialog box will appear. For each column in your aggregation table, you must define its behavior:
    - **Summarization:** Choose the aggregation function used for this column (e.g., Sum, Count, Min, Max, GroupBy, Count table rows).
    - **Detail Table:** Select the large source table that this aggregation summarizes (e.g., `Sales`).
    - **Detail Column:** Select the corresponding column in the detail table.

![Manage aggregations dialog for the Driver Activity Agg table](https://learn.microsoft.com/en-us/power-bi/transform-model/media/aggregations-advanced/aggregations_11.png)
1. After configuring all columns, select **Apply all**. The aggregation table will automatically be hidden from the Report view.
### 2. Storage Modes and Aggregations

The aggregation feature works by interacting with table-level storage modes.
- **Aggregation Table:** The storage mode for the aggregation table (e.g., `Sales Agg`) must be set to **Import**. This caches the summarized data in memory for the fastest possible query performance.
- **Detail Table:** The storage mode for the detail table (e.g., `Sales`) must be **DirectQuery**. This keeps the massive dataset in its source.
- **Dimension Tables:** Any dimension tables that are related to both the aggregation table and the detail table should be set to **Dual** storage mode. This allows Power BI the flexibility to act as either Import (when querying the aggregation cache) or DirectQuery (when a query needs to drill down to the detail table).
> [!Note] The aggregation table has the flexibility of being loaded in various ways:
> - Loading with ETL/ELT process.
> - Power Query M Expression.
> - Import storage mode with or without Incremental data refresh. 
> - DirectQuery and be optimized for fast queries using [columnstore indexes](https://learn.microsoft.com/en-us/sql/relational-databases/indexes/columnstore-indexes-overview).

### 3. Types of Aggregations
There are two primary methods for defining how aggregations work, depending on your data model.
#### Aggregations Based on Relationships
- **Use Case:** Best for **dimensional models** (star/snowflake schemas) from sources like data warehouses.
- **How it Works:** Aggregation hits are determined by the **relationships** between your dimension tables and the aggregation table. The `GroupBy` entries in the "Manage aggregations" dialog are optional (except for DISTINCTCOUNT) because the relationships guide the behavior.
- **Requirement:** The relationships must be **regular relationships** (typically one-to-many, with both tables from a single source).
#### Aggregations Based on GroupBy Columns
- **Use Case:** Best for **Hadoop-based big data models** that are often denormalized into a single large fact table without relationships.
- **How it Works:** Aggregation hits are determined by matching the columns used in a visual to the **GroupBy** columns defined in the "Manage aggregations" dialog.
- **Requirement:** The **GroupBy entries are mandatory**. Without them, the aggregations will not be hit.
### 4. Advanced Concepts
- **Aggregation Precedence:** You can have multiple aggregation tables with different levels of granularity. The **Precedence** setting allows you to specify a priority. Power BI will check the table with the highest precedence first. If that table can't answer the query, it will then check the table with the next highest precedence, and so on.
- **Row-Level Security (RLS):** For RLS to work correctly with aggregations, the security expression should filter both the aggregation table and the detail table, which is typically achieved by applying the filter to a shared dimension table (the dimension table which can filter both aggregation table and detail table).
- **Detecting Aggregation Hits:** You can use tools like **SQL Profiler** and its "Aggregate Table Rewrite Query" extended event to detect whether your report queries are successfully hitting the aggregation table or are reverting to the DirectQuery source.
- **Validations:** The "Manage aggregations" dialog enforces several rules, such as:
    - The detail table must be in DirectQuery mode.
    - Chained aggregations (where an aggregation table refers to another aggregation table) are not allowed.
    - The data types of the aggregation column and detail column must match (with some exceptions for Count).