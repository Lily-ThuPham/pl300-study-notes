[Change how visuals interact in a report - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/service-reports-visual-interactions?tabs=powerbi-desktop#change-the-interaction-behavior)
**Visual interactions** are a feature in Power BI that allows you, as a report author, to define how the visuals on a single report page impact each other. By default, visuals are interactive, but you can customize this behavior to create a more controlled and intuitive user experience.

---
### 1. Introduction to Visual Interactions: Default Behavior
By default, when a user selects a data point on one visual, it affects the other visuals on the page in one of two ways:
- **Cross-filtering:** This removes all but the related data. It acts like a temporary filter.
- **Cross-highlighting:** This does not remove data. Instead, it highlights the related data and dims the rest.
- **Cross-drill filter (less common)**: Cross-drill filters are automatically added to the pane when a drill-down filter is passed to another visual on the report page via the cross-filter or cross-highlight feature.

This default behavior can be changed on a per-visual basis.
### 2. How to Enable and Change Interaction Controls
To customize how visuals interact, you must first enable the interaction controls. This requires **edit permissions** for the report.
**In Power BI Desktop:**
1. Select the visual you want to use as the "source" of the filtering or highlighting.
2. Navigate to the **Format** ribbon.
3. Click **Edit interactions**.

**In the Power BI Service (Editing View)**:
The process is identical to the Desktop version. Select a visual, go to the Format menu, and select Edit interactions.
Once enabled, small interaction icons will appear on the header of all _other_ visuals on the page.
### 3. The Three Interaction Options
For each "target" visual, you can choose how you want the "source" visual to affect it by selecting one of the three icons. The bolded icon is the currently active interaction.

| **Name**                                                                                                                                                 | **Behavior**                                                                                                                | **Which Visuals Are Affected This Way**                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| **Cross-filter** ![](https://learn.microsoft.com/en-us/power-bi/create-reports/media/service-reports-visual-interactions/power-bi-filter-icon.png)       | **Cross-filters** the visual, removing all unrelated data.                                                                  | This is the only option for **line charts, scatter charts, and maps**. |
| **Cross-highlight** ![](https://learn.microsoft.com/en-us/power-bi/create-reports/media/service-reports-visual-interactions/power-bi-highlight-icon.png) | **Cross-highlights** the visual, dimming the unrelated data to show portion of highlighted data in relation with the total. | This is the default for visuals like **bar charts and column charts**. |
| **None** ![](https://learn.microsoft.com/en-us/power-bi/create-reports/media/service-reports-visual-interactions/power-bi-no-impact.png)                 | The selected visual will have **no impact** on this visual.                                                                 | This can be applied to any visual.                                     |
### 4. Interactions with Drillable Visuals
By default, when you drill down in a visual that has a hierarchy, this action **does not affect** any other visuals on the page. However, you can change this to make the drill-down action filter the entire page.
**How to Enable Drilling to Filter the Page:**
1. Select the drillable visual (e.g., a column chart with a hierarchy).
2. Ensure the drill-down feature is enabled for that visual.
3. Go to the **Format** menu on the ribbon.
4. Find the setting **"Apply drill down filters to"** and select **"Entire page."**

**Outcome:** Now, when a user drills down from "Year" to "Quarter" in the source visual, all other visuals on the report page will automatically be filtered to that selected quarter.
### 5. Considerations and Limitations
- **Matrix Visuals:** Be aware that if you build a matrix visual with fields from different, unrelated tables, attempting to cross-highlight by selecting multiple items at different levels of the hierarchy can cause errors on the other visuals.