
### 1. Slicers vs. the Filters Pane
While both are used for filtering, the choice between them is a tradeoff between performance and user experience.

|**Feature / Aspect**|**Filters Pane**|**Slicers**|
|---|---|---|
|**✅ Advantages**|**Performance:** Faster report rendering as no visual needs to be drawn. **Space:** Takes up no space on the report canvas. **Advanced Options:** Supports **Top N** filters and can filter by a **measure's result**.|**Design Flexibility:** Can be placed anywhere on the page and highly formatted. **User Experience:** Current filter selections are always visible on the canvas. **Functionality:** Supports hierarchies, images, and can be synced across pages.|
|**❌ Disadvantages**|**Design Flexibility:** Limited styling and fixed position. **User Experience:** Can be less intuitive; applied filters are not always obvious.|**Performance:** Slower rendering due to the visual. **Space:** Takes up valuable space on the report canvas. **Filter Complexity:** Does not support advanced types like "Top N."|
#### Filter slicers
- Apply visual-level filters to a slicer to reduce the list of values it shows. 
- Filtering a slicer only changes the values shown in the slicer, not the filter it applies to other visuals when you make a selection. 
- **Examples:**
	- For example, filter out blank values from a list slicer or certain dates from a range slicer. 
	- For example, apply a filter to a range slicer to show only certain dates. The selection in the slicer only shows the first and last dates from that range, but you still see other dates in your other visuals. When you change the selected range in the slicer, you see the other visuals update. Clear the slicer to show all dates again.

### 2. Syncing slicers 
#### Sync slicer across pages
You can sync a slicer and use it on any or all pages in a report.
- Power BI Desktop : In **Report view**, click on **Sync slicers** button to open the **Sync slicers pane**.
- Power BI Service: In the Power BI service, on the **View** menu, select the **Sync slicers pane**.
Choose a slicer, the **Sync slicers** pane appears like this:
![Screenshot of Sync District Monthly Sales slicer.](https://learn.microsoft.com/en-us/power-bi/visuals/media/power-bi-visualization-slicers/9-sync-slicers.png)
Configure report pages on which the slicer should be visible or should be applied. When a slicer is make visible on another page, a copy of that slicer is automatically created on the page. 
#### Group and Sync different slicers 
You can also sync two or more separate slicers. Syncing slicers is useful when working with composite models, as you might want to make the same selection across sources without relying on cross-source group relationships. 
Steps to Sync Slicers:
1. **Open the Sync Slicers Pane**  
    Go to the **View** menu and enable the **Sync slicers pane**.
2. **Group the Slicers**
- Select a slicer and expand **Advanced options** in the Sync pane.
- Enter a **group name** (any name you choose).
- Repeat for other slicers you want to sync—use the **exact same group name**.
3. **Choose Sync Options**
- **Sync filter changes**: Keeps filter selections aligned across slicers.
- **Sync field changes**: Ensures field changes are mirrored across slicers.
- You can choose one or both depending on your needs.
4. **Test the Sync**  
    Change a selection in one slicer and confirm the others update accordingly.
    
⚠️**You cannot group a date slicer and a category slicer together in Power BI.** Slicer grouping only works when the slicers are based on the _same field_ or _compatible fields_

### 3. Advanced Interactive Features
[Create Apply all and Clear all slicers buttons in reports - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/buttons-apply-all-clear-all-slicers?tabs=powerbi-service)
[Create a relative date slicer or filter in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/visuals/desktop-slicer-filter-date-range)
[Use report readers to change visuals - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/power-bi-field-parameters)

### 4. Types of Filters in Power BI Reports
Filters in Power BI behave differently depending on how they are created. This table breaks down the various filter types and the level of control a report author has over each in the Filters pane.

| **Filter Type**       | **How It Is Created**                                                                             | **Author Control (Edit, Delete, Hide, Lock)**                                                                                            |
| --------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Automatic**         | **Automatically** added to a visual when you add a field to it.                                   | **Can't be deleted**. Can be edited, hidden, and locked.                                                                                 |
| **Manual**            | An author **drags and drops** a field into any section of the Filters pane.                       | **Full control:** Can be edited, deleted, hidden, and locked.                                                                            |
| **Include / Exclude** | **Automatically** added when you right-click a data point and choose "Include" or "Exclude."      | **Cannot be edited or renamed**. Can be deleted, hidden, and locked.                                                                     |
| **Drill-down**        | **Automatically** added to the Filters pane when you drill down into a visual's hierarchy.        | **Can be cleared**, but not deleted or locked. To remove it, you must drill up in the visual.                                            |
| **Cross-drill**       | **Automatically** added to a visual when it is filtered by a drill-down action in another visual. | **No control**. This filter is transient and cannot be modified in the pane.                                                             |
| **Drillthrough**      | Passed from a source page to a **drillthrough (destination) page**.                               | The main drillthrough fields can be edited and locked. Filters passed from the source page are transient and cannot be locked or hidden. |
| **URL**               | Added to the report by a **query parameter in the URL**.                                          | **Can be cleared or edited**, but not locked or hidden. To remove it, you must modify the URL.                                           |
| **Pass-through**      | A visual-level filter created automatically by the **Q&A visual**.                                | **Can be deleted or hidden**, but not edited, cleared, or locked.                                                                        |
