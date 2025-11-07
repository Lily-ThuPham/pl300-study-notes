## Reference Queries 
A feature allow to establish a connection between an existing query and a new query. 
The new query uses the steps of a previous query without having to duplicate the query. 
Use Reference to create two queries with different steps but with both sharing a set of initial steps.
- The referenced or original query will contain all of the initial common steps that both child or referencing queries share 
- any change to the original query (parent query) will cascade to the referencing child queries
#### Applications: 
Use a query as a data source and perform transformation steps in other queries.
Once the updates are made in the master query, changes will be applied to all reference queries. 
#### Benefits 
- Re-usability: promote consistency, reduce the risk of error
- Efficiency: avoid repetition
- Scalability: scalable data transformation workflows, separate queries for data sources
### Modular approach
It's possible to create a single query with all the transformations and calculations. But if the number of steps are too great, it's recommended to split the query into multiples queries, where one query references the next
### Operations 
Create a Reference query function will: 
- Make a copy of query 
- Establish a connection 
- The new query will have a single step: sourcing from the original query and will not include the applied steps of the original query.
### Reference queries and dataflows 
Reference queries allow streamlining and optimization of the data transformation process. While dataflows offer a centralized and scalable approach for a data preparation, providing a self-service environment for users to create  and manage ERL processes.
### Optimize reference queries 
To minimize their impact on data refreshes
- Limit the number of references layers 
- Optimize query transformation 
- Manage the refresh schedule to avoid excessive load on data sources during peak times
- Monitor and analyze performance 

## Copying or Duplicating best practice  
[Share a query - Power Query | Microsoft Learn](https://learn.microsoft.com/en-us/power-query/share-query)
- Use **Copy to create a copy of a referencing query along with all of its source queries** (Duplicate only create a copy of the referencing data source but not its original referenced one).
- Either copy or duplicate to create a branch query from an original query, while keeping complete isolation between them.
	- Transformations copied from the original query will execute in both queries. 
	- Changes to transformations in the original query will not impact the duplicate query.

| Feature                   | Copy / Duplicate                                                                                                              | Reference                                                                                                                                                   |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Independence**          | **Independent** ↔️<br>Creates a new, standalone query.                                                                        | **Dependent** 🔗<br>Creates a child query linked to a parent.                                                                                               |
| **M Code**                | The entire M code (all steps) from the original query is cloned.                                                              | The M code is just a single line: `Source = #"Original Query Name"`                                                                                         |
| **Cascading Changes**     | **No.** Changes to the original query do NOT affect the copy.                                                                 | **Yes.** Changes to the parent query DO affect the referenced (child) query.                                                                                |
| **Upstream Dependencies** | `Copy` will also copy any parent queries. `Duplicate` will not.                                                               | A referenced query is always dependent on its parent query.                                                                                                 |
| **Primary Use Case**      | To create a slightly different version of a query without altering the original (e.g., changing a filter or the data source). | To create a "base" query with common steps and then branch off to create multiple specialized queries from that clean base. (Staging/Transformation Layer). |
# Reference Queries 
A feature allow to establish a connection between an existing query and a new query. 
The new query uses the steps of a previous query without having to duplicate the query. Additionally, any changes on the original query will transfer down to the referenced query.
## Applications: 
Use a query as a data source and perform transformation steps in other queries.
Once the updates are made in the master query, changes will be applied to all reference queries. 
# Benefits 
- Re-usability: promote consistency, reduce the risk of error
- Efficiency: avoid repetition
- Scalability: scalable data transformation workflows, separate queries for data sources
## Application 
An example in advanced transformations 
### Modular approach
It's possible to create a single query with all the transformations and calculations. But if the number of steps are too great, it's recommended to split the query into multiples queries, where one query references the next
# Operations 
Create a Reference query function will: 
- Make a copy of query 
- Establish a connection 
- The new query will have a single step: sourcing from the original query and will not include the applied steps of the original query.
# Reference queries and dataflows 
Reference queries allow streamlining and optimization of the data transformation process. While dataflows offer a centralized and scalable approach for a data preparation, providing a self-service environment for users to create  and manage ERL processes.
# Optimize reference queries 
To minimize their impact on data refreshes
- Limit the number of references layers 
- Optimize query transformation 
- Manage the refresh schedule to avoid excessive load on data sources during peak times
- Monitor and analyze performance 