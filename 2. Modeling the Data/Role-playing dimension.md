## Dimensions
In data analysis, dimensions represent attributes or business entities used to organize data. For example, in a sales dataset, dimensions could include product, customer, and date.
## Role playing dimensions 
- When two model tables have multiple relationships, it could be because your model has a role-playing dimension.
- Role playing dimensions are instances of the same dimension used multiple times in a data model, allow to explore data from different perspectives without duplicating data tables.
	- **Benefits**: By using role playing dimensions, you can avoid duplicating data tables and optimize your data model. It provides flexibility in analyzing data from different angles without the need for separate tables for each perspective or adjust analysis based on different categories of products.
- Active relationships are connections between tables that are actively used for analysis, reporting, and visualization.
- Inactive relationships are valid connections that are not currently being used.
- Power BI marks active relationships with a solid line and inactive relationships with a dotted line.
### Configure role-playing dimensions
- Establish the active and inactive relationships between two related tables. 
	- Active relationship - solid line: validate the relationship
	- Inactive relationship - dashed line: uncheck "Make this relationship active"
- Create measures with `CALCULATE` and `USERELATIONSHIP` function 
## `USERELATIONSHIP` function 
[USERELATIONSHIP function (DAX) - DAX | Microsoft Learn](https://learn.microsoft.com/en-us/dax/userelationship-function-dax)
The **`USERELATIONSHIP`** function allows to utilize an inactive relationship for specific analytical needs. It overrides the default relationship and establishes a temporary relationship between tables based on the inactive relationship.
It is most useful when ==there are multiple relationships between two tables==.
**Syntax:**
```DAX
USERELATIONSHIP (Table_name1 [columnName1], Table_name2 [columnName2])
```
### Recommended practices 
1. Use calculate functions: It is not intended to be used elsewhere, and attempting to use it outside of these functions will result in an error.
2. Switching multiple relationships
3. Existing Relationship: The **`USERELATIONSHIP`** function requires that the relationship between the tables already exists in the data model.
4. Context modification and Flexibility 
### Consideration 
1. Only use `USERELATIONSHIP` with DAX functions that take filter as an argument. 
2. Cannot use the `USERELATIONSHIP`function when Row-level security is implemented. 
3. Defined relationships are already available.
4. Nesting up to 10 `USERALTIONSHIP` function in a single expression. 
5. `USEREALTIONSHI` can only activate relationship in one direction. To activate a bidirectional inactive relationship, use two `USERELATIONSHIP` in a single expression.