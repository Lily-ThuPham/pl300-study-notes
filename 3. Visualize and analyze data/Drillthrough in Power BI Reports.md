[Drillthrough in Power BI Reports: Navigate to Detailed Insights - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-drillthrough)
**Drillthrough** is a navigation feature in Power BI that allows users to move from a summary visual on one page to a more detailed **destination page**. The destination page is automatically filtered to the specific data context the user selected on the source page.

This feature is essential for creating interactive reports that allow users to explore data from a high-level overview down to granular details.

---
### 1. Key Drillthrough Concepts

|Feature|Description|
|---|---|
|**Drillthrough Page**|A dedicated report page designed to display detailed information about a single entity (e.g., a specific customer or product).|
|**Drillthrough Filters**|The field(s) you place in the **Drillthrough well** of the destination page. This is the crucial step that tells Power BI which field will be used to receive the filter from the source page.|
|**Drillthrough Button**|An interactive button on the source page that becomes active when a user selects a valid data point. Clicking it navigates the user to the drillthrough page.|
|**Cross-report Drillthrough**|An advanced feature that allows users to drill through from a report in one workspace to a different report in the **same workspace**.|

### 2. How to Set Up and Use Drillthrough
#### Creating a Drillthrough Page
1. Create a new report page that will serve as your destination (the "drillthrough page").
2. In the **Visualizations pane** for this new page, find the **Drillthrough** section.
3. Drag the field that you want to filter by into the **"Drillthrough filters"** well (e.g., drag the `Customer Name` field here).
4. Add visuals to the page that will display the detailed information (e.g., cards showing customer details, a table of their orders).
5. Power BI automatically adds a **"Back" button** to the drillthrough page.
#### Using Drillthrough (The User Experience)
1. On a source page, a user **right-clicks a data point** in a visual (e.g., a specific customer's bar in a bar chart).
	- Drillthrough data point is not available for Python and R visuals. 
2. From the context menu, they select **Drillthrough** and choose the destination page.
3. They are navigated to the drillthrough page, which is now filtered to show details for only that selected customer.
#### Adding a Drillthrough Button
A button provides a more obvious visual cue for the drillthrough action.
1. On your source page, go to the **Insert** ribbon and add a **Button**.
2. With the button selected, go to the **Format** pane.
3. Under **Action**, turn the slider to **On**.
4. Set the **Type** to **Drill through**.
5. Set the **Destination** to your drillthrough page.
6. By default, the button will appear **disabled** (grayed out) until a user selects a valid data point in a visual that can filter the drillthrough page.

### 3. Cross-Report Drillthrough
This allows you to link reports together.
- **Requirement:** The source and target reports must be in the **same workspace**.
- **Setup:**
    1. In the **target report's settings** (in Power BI Desktop), enable the **"Cross-report drillthrough"** option.
    2. Ensure that the field names and data types used for the drillthrough match **exactly** between the source and target reports.
    3. Publish both reports to the same workspace.
### 4. Troubleshooting Common Drillthrough Issues

|Issue|Common Causes & Solutions|
|---|---|
|**Drillthrough option doesn't appear in the right-click menu.**|<ul><li>**Verify the filter:** Make sure the correct field is in the "Drillthrough filters" well on the destination page.</li><li>**Match the fields:** The field in the source visual must match the field in the drillthrough filter.</li><li>**No aggregation:** The field in the source visual must not be aggregated (e.g., counted or summed).</li></ul>|
|**Drillthrough button isn't working or is always disabled.**|<ul><li>**Check the action:** Ensure the button's Action Type is set to "Drill through" and a valid Destination is selected.</li><li>**Check the selection:** The button only becomes active after a user selects a data point in a visual that contains the drillthrough field.</li></ul>|
|**Filters aren't applied correctly on the destination page.**|<ul><li>**Check for data transformations:** Ensure the field used for drillthrough hasn't been duplicated or significantly transformed in Power Query, causing a mismatch.</li><li>**Check relationships:** Inactive or incorrect relationships in your model can affect filter propagation.</li></ul>|
|**Cross-report drillthrough fails.**|<ul><li>**Check workspace:** Both reports must be in the same workspace.</li><li>**Check field names:** The field names and data types must match _exactly_.</li><li>**Check setting:** Ensure "Cross-report drillthrough" is enabled in the target report's settings.</li></ul>|
