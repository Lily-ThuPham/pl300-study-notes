## Row-Level Security (RLS)
[Row-level security (RLS) with Power BI - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/en-us/fabric/security/service-admin-row-level-security?source=recommendations)
**Row-Level Security (RLS)** is a feature used to **restrict data access** for specific users. It works by applying filters at the row level, allowing you to control which rows of data users can see within the same report or dataset.

---
### 1. Key Concepts
- **Purpose:** To enforce data restrictions based on the user viewing the content (e.g., a sales manager only sees data for their region).
- **Where it Applies:** RLS is configured on the **semantic model** (dataset).
- **Who it Affects:** In the Power BI service, RLS restrictions **only apply to users assigned the Viewer role** in a workspace. RLS does _not_ apply to users with Admin, Member, or Contributor roles, as they have edit permissions for the semantic model.
### 2. Configuration Based on Connection Type
- **Import / DirectQuery Models:** RLS roles and rules are defined in **Power BI Desktop** before publishing.
- **Analysis Services Live Connections:** RLS is configured **within the source Analysis Services model** itself, not in Power BI.
### 3. Defining Roles and Rules in Power BI Desktop
1. **Open "Manage Roles":** Go to the **Modeling** tab and select **Manage Roles**.
2. **Create Role:** Click **New**, provide a name for the role (e.g., "Sales Manager Region").
3. **Select Table:** Choose the table you want to apply the filter rules to (typically a dimension table, like `Region` or `Employee`).
4. **Define Rules:** Use either the default editor or the DAX editor to create a filter expression that returns TRUE or FALSE.
    - **Default Editor:** Provides a simple interface for basic filters (e.g., `[Country] = "USA"`).
    - **DAX Editor:** Allows for more complex and dynamic rules. DAX expressions must return TRUE/FALSE.
        - **Dynamic RLS:** Use DAX functions `USERNAME()` (returns `DOMAIN\User` in Desktop, UPN in Service) or `USERPRINCIPALNAME()` (returns UPN like an email address) to filter data based on the logged-in user. Example: `[ManagerEmail] = USERPRINCIPALNAME()`
5. **Save:** Click **Save**.

**Bi-directional RLS Filtering:** By default, RLS filters flow in a single direction following active relationships. You can enable bi-directional RLS filtering by editing the relationship and checking **"Apply security filter in both directions."** Use this cautiously, primarily when implementing dynamic RLS based on username at the server level.
### 4. Managing Security in the Power BI Service
After publishing the `.pbix` file, you assign users or groups to the roles you created.
1. In the Power BI service, go to the workspace containing the semantic model.
2. Select **More options (...)** next to the semantic model and choose **Security**.
3. Select the RLS role you want to manage.
4. Enter the email addresses of users or **supported groups** (Distribution, Mail-enabled, Microsoft Entra Security Groups - ==_Note: Microsoft 365 groups are not supported for RLS assignment_==).
	- **Best Practice:** Whenever possible, **map security groups to roles, not individual users**. This simplifies administration, as you can manage user access in Microsoft Entra ID without having to update the RLS settings in Power BI.
5. Click **Add**, then **Save**.
### 5. Validating Roles in the Power BI Service
- **In Desktop:** Use the **Modeling > View as** feature. You can test a role and provide a test username for dynamic RLS (e.g., `manager.north@company.com`).
- **In Service:** Use the **Test as role** feature in the dataset's **Security** page. This is the most accurate way to test the user's experience.

**Validation Best Practice:** When testing dynamic RLS, be sure to test for _unexpected_ values. A weak DAX rule can accidentally grant access to all data.
- **Bad (Unsafe) Rule:** `IF(USERNAME() = "Worker", [Type] = "Internal", TRUE())`
    - _Problem:_ If an unexpected username (like "Wrker") is passed, it will default to `TRUE()` and show all data.
- **Good (Safe) Rule:** `IF(USERNAME() = "Worker", [Type] = "Internal", IF(USERNAME() = "Manager", TRUE(), FALSE()))`
	- _Result:_ An unexpected username will default to `FALSE()`, correctly returning no rows.

> [!Note] The "Test as role" feature has limitations, especially with DirectQuery models using SSO, certain visuals like Q&A "Test as role" also doesn't work for paginated report.
### 6. RLS and Workspace Roles Interaction
- **RLS is Enforced:** For users assigned the **Viewer** role in the workspace. Even if Viewers have Build permissions, RLS applies.
- **RlS is NOT Enforced:** For users assigned **Admin**, **Member**, or **Contributor** roles, as they have edit permissions on the semantic model.
### 7. RLS Optimization Best Practices
- **Model Design:** Efficient RLS depends on a good **star schema**.
- **Filter Dimensions:** It is always more efficient to enforce RLS filters on **dimension tables** (e.g., `Region` table) rather than large fact tables (e.g., `Sales` table).
- **Relationships:** Rely on well-designed, **active relationships** to propagate the RLS filters from the dimension tables to the fact tables. RLS filters only propagate through active relationships.
- **DirectQuery:** If using RLS on DirectQuery tables, ensure the source database is optimized with appropriate indexes.
- **Measure Impact:** Use the **Performance Analyzer** in Power BI Desktop to measure query durations before and after applying RLS (using "View As") to identify performance bottlenecks.
### 8. Advanced RLS Design: Partial RLS
- **Use Case:** When you need a calculation that compares a user's filtered data against the total (e.g., "My Region's Sales as a % of All Region Sales").
- **Problem:** A standard measure for "All Sales" would be filtered by RLS, making it impossible to get the grand total. A DAX expression cannot override RLS.
- **Solution:** Create a **separate summary table** (e.g., a calculated table using `SUMMARIZECOLUMNS`) that contains the grand totals. Crucially, **do not** create a relationship between this new summary table and the dimension table that has the RLS filter on it. Instead, relate both the summary table and the fact table to a shared dimension, like a `Date` table.
    - The RLS filter will flow from `Salesperson` to `Sales` but **will not** flow to the `SalesRevenueSummary` table.
    - This allows a measure like `DIVIDE(SUM(Sales[Revenue]), SUM(SalesRevenueSummary[RevenueAllRegion]))` to work correctly.
### 9. Considerations and Limitations
- Only Import and DirectQuery connections are supported. Live connections to Analysis Services are handled in the on-premises model.
- **Multiple Roles are Additive:** A user can be a member of multiple roles. The permissions are **additive**, meaning the user will see the **union** of data allowed by all their roles. The "once denied, always denied" principle does _not_ apply.
    - _Example:_ If Role A denies all access (`FALSE()`) and Role B allows all access (`TRUE()`), a user in _both_ roles will see **all data**.
- **Alternatives to RLS:** If you only have a few simple, static rules (e.g., one report per region), it can be simpler to avoid RLS. Instead, publish **multiple versions of the report** to different workspaces and assign users to the appropriate workspace.
- **Unsupported Features:** RLS does not work with some features like "Publish to web."
- **Troubleshooting:** If RLS produces unexpected results, check for:
    - Incorrect or **inactive** relationships.
    - A user being mapped to multiple roles, giving them additive permissions.
    - An incorrect User Principal Name (UPN) stored in the data.

> [!Exam Note] 
> You should know how the RLS works when applying multiple roles. 

| **Topic / Question**                                             | **Key Takeaway / Answer**                                                                                                                                                                                                                                                                                                     |
| ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Analysis Services (AS) Data Sources**                          | It depends on the connection mode: • **Import:** Yes, you define RLS in Power BI Desktop just like any other imported table. • **Live Connection:** **No**. RLS cannot be configured in Power BI. It must be defined within the on-premises Analysis Services model itself.                                                   |
| **RLS vs. OLS (Columns/Measures)**                               | **No**. RLS **only filters rows**. It cannot be used to limit access to specific columns or measures. To restrict columns or measures, you must use **Object-Level Security (OLS)**.                                                                                                                                          |
| **Hiding Detailed Data**                                         | **No**. RLS secures individual rows of data. A user who has access to a row can see both the detailed data and any summarized data derived from that row.                                                                                                                                                                     |
| **Interaction with Source DB Security (e.g., SQL Server roles)** | It depends on the connection mode: • **Import:** The security roles in your data source are **ignored**. You must define your RLS rules in Power BI. • **DirectQuery:** The security roles in your data source are **used**. Power BI passes the user's credentials to the source, which then applies its own security rules. |
| **User in Multiple Roles**                                       | **Yes**, a user can be in multiple roles. The permissions are **additive**—the user sees the **union** (combination) of data from all roles they are assigned to (e.g., a user in "Sales" and "Marketing" roles can see data for _both_).                                                                                     |
## Object-Level Security (OLS) in Power BI
[Object-Level Security (OLS) with Power BI - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/en-us/fabric/security/service-admin-object-level-security?source=recommendations&tabs=table)
**Object-Level Security (OLS)** is an advanced security feature that enables model authors to secure specific **tables or columns** from report viewers.
Unlike RLS, which filters _rows_, OLS hides the _objects_ themselves (including their names and metadata). For a user without permission, it's as if the secured table or column doesn't exist.

---
### 1. Key Concepts
- **Purpose:** To protect business-critical or sensitive personal information (e.g., an `Employee` table or a `Salary` column) from unauthorized discovery or access.
- **How it's Defined:** Like RLS, OLS rules are defined within **model roles**.
- **Who it Affects:** OLS **only applies to users with the Viewer role** in a workspace. It does _not_ apply to Admins, Members, or Contributors, as they have edit permissions.
### 2. How to Configure OLS
OLS **cannot** be configured natively in Power BI Desktop. You must use an external tool like **Tabular Editor**.
**Step-by-Step Configuration:**
1. **Create Roles in Power BI Desktop:** First, go to **Modeling > Manage roles** and create the roles (e.g., "HR Manager," "Analyst") just as you would for RLS.
2. **Open Tabular Editor:** Go to the **External tools** ribbon and launch Tabular Editor. It will automatically connect to your open data model.
3. **Find the Role:** In Tabular Editor's Model view, find and select the role you want to configure.
4. **Set Permissions:**
    - Expand the **Table Permissions** for that role.
    - Find the specific table or column you want to secure.
    - Change its permission from `Default` to **`None`**.
        - **To secure a whole table:** Set the table's permission to `None`.
        - **To secure a specific column:** Expand the table, find the column, and set its permission to `None`.
5. **Save and Publish:** Save the changes in Tabular Editor, return to Power BI Desktop, and publish your semantic model to the Power BI service.
6. **Assign Users:** In the Power BI service, go to the semantic model's **Security** page and assign your users or groups to the role you just configured.
### 3. Considerations and Limitations
- **User Experience:** When a user without permission views a report that uses a secured object, the visual will break and show a "field can't be found" error.
- **Unsupported Features:** Semantic models that use OLS are **not supported** with the following Power BI features:
    - Quick Insights
    - Smart Narrative visualizations
    - Excel Data Types gallery
### **Sample Exam Questions 📝**

| No. | Question                                                                                                                                                                                                                                            | Options                                                                                                                                                                                                                                                  | Correct Answer | Explanation                                                                                                                                                                                                                                          |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | You have a Power BI report with a "Sales" table containing data for different regions. You need to ensure sales managers can only see data for their assigned regions. What is the first step?                                                      | A. Publish the report to the Power BI service.<br>B. Create a new role in the Power BI service.<br>C. Create a new role in Power BI Desktop.<br>D. Assign users to the "Sales Manager" role.                                                             | **C**          | RLS roles and their DAX filter rules must first be defined in **Power BI Desktop** before the report is published. Management of user assignments to those roles happens later in the Power BI service.                                              |
| 2   | You are implementing dynamic RLS. The "Employees" table contains an "Email" column with each employee's email address. To ensure employees only see their own data, which DAX function should you use in the role's filter expression?              | A. `NOW()`<br>B. `USERNAME()`<br>C. `USERPRINCIPALNAME()`<br>D. `TODAY()`                                                                                                                                                                                | **C**          | **`USERPRINCIPALNAME()`** returns the User Principal Name (which is typically the user's login email address) in the Power BI service. This allows you to match it directly against the "Email" column in your table.                                |
| 3   | You have published a Power BI report with RLS to a workspace. A user is assigned the **Viewer** role in the workspace and is also assigned to an RLS role. Will RLS be applied for this user?                                                       | A. Yes, because RLS is always applied to all users.<br>B. No, because the user has read-only access.<br>C. Yes, because RLS is applied to users with the "Viewer" role.<br>D. No, because RLS is only applied to "Admins", "Members", or "Contributors". | **C**          | RLS is specifically designed to be enforced for users who are consumers of the content, which corresponds to the **Viewer** role in a workspace. It does not apply to users with edit rights (Admin, Member, Contributor).                           |
| 4   | Your data model has a "Sales" table and a "Region" table with a one-to-many relationship from "Region" to "Sales". You apply an RLS filter on the "Region" table. How do you ensure this filter also restricts the data shown in the "Sales" table? | A. Create a calculated column in the "Sales" table.<br>B. Enable bi-directional cross-filtering on the relationship.<br>C. Create a separate RLS rule for the "Sales" table.<br>D. Merge the "Region" and "Sales" tables.                                | **B**          | To allow an RLS filter on the "one" side of a relationship (Region) to filter the "many" side (Sales), you must edit the relationship. In the relationship properties, you need to check the box for **"Apply security filter in both directions."** |
