In the Power BI service an desktop, you can change the sort order of most visuals to highlight important information. These changes are often saved for your next session.
![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service
### 1. How to Access Sorting Options
In Power BI Service:
1. Open a Power BI report in **Reading view**.
2. Select a visual that can be sorted.
3. Select the **More options (...)** menu in the visual's header.
4. Choose from the available sorting options, which can include **Sort ascending**, **Sort descending**, and **Sort by**.
**Visuals That CANNOT Be Sorted:** It's important to know that some visuals do not support sorting. These include:
- Treemaps
- Filled maps
- Scatter charts
- Gauge charts
- Waterfall charts
- Cards
- Visuals on a dashboard
### 2. Basic Sorting (Single Field)
You can sort a visual by a single field, either alphabetically for text or numerically for numbers.
- **How to change:** In the **More options (...)** menu, select **Sort ascending** or **Sort descending**. A checkmark will indicate the currently active sort field and order.
### 3. Sorting by Multiple Columns (for Tables & Matrices)
For table and matrix visuals, you can create a more complex sorting sequence using multiple columns.
1. **Primary Sort:** Click the column header you want to sort by first. A small arrow will appear, indicating the sort direction.
2. **Secondary Sort:** Hold down the **Shift key** and click a second column header. This will sort the data within the primary sort order.
3. You can continue to hold **Shift** and click additional columns to add more levels to the sort priority.
**Other Shift-Click Actions:**
- **Change Direction:** Hold Shift and click the _same column_ again to toggle between ascending and descending.
- **Reorder Priority:** Hold Shift and click a column you have _already added_ to the sort order. This will move that column to the back of the sort priority.

### 4. Sorting by a Different Field (e.g., Month by Month Number)
Sometimes, you need to sort a column in a non-alphabetical, logical order (e.g., sorting month names chronologically or T-shirt sizes "S, M, L, XL").
- **For Report Consumers:** You **cannot** configure this yourself in Reading view. This sorting logic must be set up in the data model.
- **For Report Designers (with Edit Permissions):** The designer must  sort the field column by using the **"Sort by column"** feature in Power BI Desktop. For example, they would select the `Month Name` column and configure it to be sorted by the `Month Number` column. This ensures that visuals always display months in the correct chronological order.
[Sort one column by another column in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-sort-by-column)
### 5. Saving Your Sort Changes
Power BI is designed to remember the changes you make to a report.
- **Persistent Filters:** By default, any changes you make to filters, slicers, and the **sort order** are saved and will be there when you return to the report later.
- **Reset to Default:** To revert all your changes back to the original state published by the report designer, select the **Reset to default** button in the report's top menu bar.
- **Personal Bookmarks:** If the report designer has enabled the **"Personalize visual"** feature, you can save your specific sort order and other changes as a **personal bookmark** for easy access later.