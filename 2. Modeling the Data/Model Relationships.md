[Model relationships in Power BI Desktop - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-relationships-understand)
## **`Model view`** Overview 
The **Model view** can be accessed by selecting the **model** icon on the left sidebar of Power BI desktop. The **Model view** contains the following UI elements:
- **Diagram view (canvas)**
- **Data pane**
- **Properties pane**
- **Home ribbon**
### Diagram view 
Visualize elements of data model: data tables, fields, and relationships.
You can create and configure relationships between tables based on common key fields.
The **connector line** connects two tables. The **1** icon represents the **one** side of the relationship, while the **" * "** icon indicates the **many** side of the relationship.
## Key Relationship Properties
Every relationship is defined by a set of properties that you configure in the Model view.

| Property                          | Description & Options                                                                                                                                                                                                                                                                    | Best Practice / Key Notes                                                                                                                                                                                                                                                    |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cardinality**                   | Defines the data characteristics of the related columns. • **One-to-many (1:_) / Many-to-one (_:1):** One column has unique values, the other has duplicates. • **One-to-one (1:1):** Both columns have unique values. • **Many-to-many (_:_):** Both columns can have duplicate values. | The **one-to-many** relationship is the most common and most efficient type. Use it whenever possible. Many-to-many should only be used for complex requirements.                                                                                                            |
| **Cross filter direction**        | Determines the direction that filters will flow. • **Single:** The filter flows in one direction only (from the "one" side to the "many" side). • **Both (Bi-directional):** The filter can flow in both directions.                                                                     | Use **Single** by default. Bi-directional relationships can cause performance issues and ambiguous filter paths. Only use them when absolutely necessary.<br>It can apply bi-directional filtering when Power BI enforces ==row-level security (RLS) rules==.                |
| **Make this relationship active** | Determines if the relationship is active or inactive. • **Active (Solid Line):** The relationship automatically propagates filters. • **Inactive (Dashed Line):** The relationship only propagates filters when explicitly called by a DAX measure.                                      | You can only have **one active relationship path** between two tables. Inactive relationships are primarily used for **role-playing dimensions** (e.g., when a single Date table is related to both `OrderDate` and `ShipDate` in a Sales table).                            |
| **Assume referential integrity**  | A performance optimization for **DirectQuery** mode. It changes the join type from a safer `OUTER JOIN` to a faster `INNER JOIN`.                                                                                                                                                        | Only enable this if you are certain the "many" side column **never contains NULLs** or values that don't exist in the "one" side table. Incorrectly enabling this will **not cause an error**, but will lead to **incorrect results** where totals do not match the details. |
## The Purpose of a Relationship

The primary purpose of a model relationship is to **propagate filters**. When you apply a filter to one table, that filter travels along the relationship path to a related table. If multiple filters are applied, they work as an **AND** operation, meaning all conditions must be true.

**Best Practice: Star Schema** The recommended model design is a **star schema**. This consists of
- **Fact Tables:** Contain transactional, numeric data (like sales amounts).
- **Dimension Tables:** Contain descriptive attributes (like products, customers, and dates).

Cardinality and cross-filter direction are two key elements of model relationships in Power BI.
[Model relationships in Power BI Desktop - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-relationships-understand)
## **Cardinality** 
The relation between tables in a database.
Indicating how many instances of an entity in one table relate to instances in another
### One-to-one relationship
One of the most common relationships.
In a one-to-one relationship, each row in a table corresponds to no more than one row in another table.
This relationship only supports the **Both** crossfilter direction. This means that when a filter is applied to one table, the filtering propagates to the other table.
### One-to-many relationship 
One-to-many relationship: most common type, each record from a column of Table A corresponds to multiple records in a column of table B. 
For example: stores table and employee table where each store has many employees but each employee works in one store
### Many-to-many relationship 
 Many-to-many relationship: relationship between two fact tables or two dimension tables. For example: a customer can purchase many different bicycle models, each bicycle model can be purchased by multiple customers. 
The disadvantage of a many-to-many relationship is that it introduces ambiguity in data analysis. So, it’s only recommended to use it in certain specific scenarios.
Many-to-Manu relationship can be either of 3 directions:
- Table A to Table B single direction
- Table B to Table A single direction 
- Both direction 
### Relevant DAX Functions for Relationships
You can use DAX to manipulate how relationships behave within a specific calculation.

|DAX Function|Purpose|
|---|---|
|**`RELATED`**|Retrieves a single value from the **"one" side** of a relationship.|
|**`RELATEDTABLE`**|Retrieves a table of all matching rows from the **"many" side** of a relationship.|
|**`USERELATIONSHIP`**|**Activates an inactive relationship** for the duration of a `CALCULATE` expression.|
|**`CROSSFILTER`**|Modifies the **cross filter direction** (e.g., from single to both) for a calculation.|
|**`TREATAS`**|Creates a **virtual relationship** between two tables that are not directly related.|

#### Relationship Evaluation (Advanced Concept)
Power BI internally classifies relationships as either **regular** or **limited**. This is not a setting you can change, but it's important to understand the implications.
- **Regular Relationships:** This is the standard for one-to-many relationships where Power BI can guarantee a "one" side (i.e., it contains unique values). These are the most efficient relationships. If there are data integrity issues (a value on the "many" side has no match on the "one" side), Power BI handles this gracefully by creating a blank virtual row.
- **Limited Relationships:** A relationship is "limited" when there is no guaranteed "one" side. This occurs with **many-to-many** relationships or relationships that cross different source groups in a **composite model**. These relationships are less performant and will simply drop rows where there is a data integrity violation, which can lead to unexpected results.
### Performance preference
The following list orders filter propagation performance, from fastest to slowest performance:
1. One-to-many intra source group relationships
2. Many-to-many model relationships achieved with an intermediary table and that involve at least one bi-directional relationship
3. Many-to-many cardinality relationships
4. Cross source group relationships
## **Granularity** 
The level of detail (or depth) in a dataset. 
[Define data granularity - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/5-data-granularity)
### High granularity: 
Datasets that capture detailed information, associated attributes and metrics:
- In-depth data exploration 
- Data flexibility to aggregate and summarize
- Accurate decision making 
However:
- High granularity results in larger datasets which can slow down data processing
### Low granularity:
Datasets that capture high-level information or an aggregated level overboard or categories. 
- Simplified analysis 
- Improved performance by reducing data volume which lead to faster query execution 
- Quick identification of trends and patterns 
Low granularity data provides a broader view of the data and is easier to manage due to smaller datasets.
### Importance of data granularity 
Granularity will influence the establishment of correct cardinality and cross-filter direction. 
- Misjudging the level of granularity can lead to mispresented data and incorrect business insights.
- Excessive granularity can lead to too much data and slow down your queries.
## Creating relationship in Power Bi 
There are two ways relationships can be created in Microsoft Power BI: automatically, or manually.
## Autodetect relationships 
When you load two to more tables using Power Query, Power BI desktop autodetects the relationships between the loaded tables based on a common column. Cardinality and cross-filter direction are automatically set.
**Autodetect relationships** function in Power BI desktop can be disable. 
## Manually create relationships 
In **Model view**, access the **Home** tab, then select **Manage Relationships**. This action brings up the **Create relationship** dialog box.
### **Cross-filter direction**
Refer to the pathway direction of filtering between two related tables in a data models.
Power BI relationships are directional in nature. Unlike other database management systems, the direction significantly impacts how filtering operates. 
[Bidirectional cross-filtering in Power BI Desktop - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-bidirectional-filtering)
### **Single direction** 
Propagates from one table to another, default setting in Power BI. 
With a single cross-filter direction:
- Only one table in a relationship can be used to filter the data. 
- For a one-to-many or many-to-one relationship, the cross-filter direction will be from the "one" side, meaning that the filtering will occur in the table that has many values.
### **Bi-directional filtering** 
Filtering against the direction of a relationship. It allows filtering from one table to another vice versa. 
It is useful when there's a need to answer specific questions or generate reports based on multiple tables. 
**Downfalls of bi-directional filtering:**
- Negatively impacts performance, lower performance
- Ambiguous filter propagation paths, oversampling, unexpected results 
Cross-filter direction in Power BI can be changed using DAX function. ==You should not enable bi-directional cross-filtering relationships unless you fully understand the ramifications of doing so==. Potential scenarios: 
1. Comparative Analysis: If you want to compare the performance or metrics of different subsets of data independently, you can disable filter propagation.
2. What-If Analysis: When performing what-if analysis or scenario modeling, you may want to isolate specific data points or variables to see the impact on your analysis. Disabling filter propagation helps you focus on the specific data points without interference from other related tables.
3. Drill-Through Analysis: In some cases, you may want to drill down into specific details of a particular data point without affecting the overall analysis. By disabling filter propagation, you can explore the details without the filters being applied to other related tables.
4. Customized Reporting: If you need to create customized reports that require specific data combinations or calculations, disabling filter propagation can help you achieve the desired results. 
### Cardinality and cross-filter direction 
For One-to-one relationships: only option is bi-directional cross-filtering.
For Many-to-many relationships, can either filter single direction or both directions. 
	The ambiguity that is associated with bi-directional cross-filtering is amplified in a many-to-many relationship because multiple paths will exist between different tables.