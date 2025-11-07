Query parameters are functions used to create adaptable, reusable queries for efficient data retrieval and transformation.
A parameter serves as a way to easily store and manage a value that can be reused in many different ways.
## Benefits if creating parameters 
- Centralized view of all your parameters through the **Manage Parameters** window.
- Reusability of the parameter in multiple steps or queries.
- Makes the creation of custom functions straightforward and easy.
## Operations
**Power Query Editor -> Home Tab -> Manage Parameters -> Name the parameters and list the values -> OK -> OK** 
## Two commonly used scenarios 
- **Step argument**—You can use a parameter as the argument of multiple transformations driven from the user interface.
- **Custom Function argument**—You can create a new function from a query, and reference parameters as the arguments of your custom function.
# Helper queries 
Helper queries are additional queries that are automatically created with the main data queries in Microsoft Power BI. 
Helper queries serve the purpose of performing various data cleansing tasks such as removing duplicates, handling missing values, standardizing formats, and correcting errors. By using helper queries, you can ensure that your data is consistent and reliable for further analysis.
It's important to note that these helper queries are linked to the main query and should not be deleted, as they play a crucial role in supporting the main query's functionality.
![[Pasted image 20240711164750.png]]
# When helper queries need to be disabled 
- **Performance optimization**: In some cases, helper queries can consume additional system resources and impact the overall performance of your Power BI report. If you notice significant slowdowns or excessive resource usage, disabling unnecessary helper queries can help improve performance.
- **Streamlining the data flow**: If you have multiple helper queries in your report, disabling some of them can simplify the data transformation process. This can be useful when you want to focus on specific data flows and remove any unnecessary complexity.
- **Reducing clutter and improving organization**: When working on complex Power BI projects with numerous queries, disabling helper queries that are no longer needed can help declutter your workspace and improve overall organization. This can make it easier to navigate and maintain your report.
- **Security and data privacy**: In certain scenarios, you may have helper queries that contain sensitive or confidential data. Disabling these queries ensures that the data is not accessible or visible to unauthorized users, providing an extra layer of security and data privacy.
