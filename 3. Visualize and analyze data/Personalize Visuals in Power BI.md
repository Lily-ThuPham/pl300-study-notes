[Personalize visuals in a report - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-personalize-visuals)
**APPLIES TO:** ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service for _**business users**_ ![](https://learn.microsoft.com/en-us/power-bi/includes/media/no-icon.svg) Power BI service for designers & developers ![](https://learn.microsoft.com/en-us/power-bi/includes/media/no-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Requires Pro or Premium license
The **Personalize visuals** feature is a setting that a report _author_ can enable. When active, it empowers report _consumers_ (in Reading view) to make temporary, ad-hoc changes to visuals to explore the data in their own way, without needing edit permissions.

---
### 1. How to Enable the Feature (For Report Authors)
This feature is **off by default** and must be enabled by the report designer.
1. **Report Level:** 
	- In Power BI Desktop, go to **File** > **Options and settings** > **Options** > **Current file** > **Report settings**. Select the **Personalize visuals** checkbox.
	- In Power BI Service, go to **Settings** for your report. Switch on **Personalize visuals** > **Save**.
2. **Page or Visual Level (Optional):** After enabling it for the report, you can then selectively turn it **off** for specific pages (in the page's Format pane) or for individual visuals (in the visual's **Format > General > Header icons** pane).
	- Slide **Personalize visual** > **On** or **Off**.
![Screenshot shows the Personalize visual slider.](https://learn.microsoft.com/en-us/power-bi/create-reports/media/power-bi-personalize-visuals/power-bi-format-visual-personalize-on-off-desktop-2.png)

### 2. The User Experience (For Report Consumers)
When the feature is enabled, report consumers in Reading view will see a new **"Personalize this visual" icon** in the header of the visual.
Clicking this icon opens a **Personalize pane** that allows them to make several types of changes to that specific visual:
- Change the **visualization type** (e.g., from a bar chart to a line chart).
- **Swap out a measure or dimension** (e.g., change from "Total Sales by Country" to "Total Profit by Region").
- Add or remove a **legend**.
- Compare two or more measures.
- Change the **aggregation** (e.g., from Sum to Average).
### 3. Saving and Sharing Personalized Views
- **Changes are Temporary:** User explorations are **not** persistent by default. If the user navigates away, their changes are lost.
- **Saving Changes (Personal Bookmarks):** To save a personalized view, the user must capture it by creating a **Personal Bookmark**.
- **Sharing Changes:** If a user has reshare permissions, they can share a link to the report that includes their personalized changes. The recipient can see the author's original version by selecting **Reset to default**.
- **Resetting:**
    - **Reset this visual:** Resets a single visual to the author's default.
    - **Reset to default:** Resets the entire report page to the author's default.
### 4. Advanced: Using Perspectives
- **The Problem:** In a very large data model with hundreds of fields, giving users access to the entire field list in the Personalize pane can be overwhelming.
- **The Solution:** The report author can use an external tool like **Tabular Editor** to define **Perspectives**. A perspective is a named subset of the model (e.g., a "Sales" perspective that only includes the 10 most important sales and product fields).
- **How it works:** The author can then set the **"Report-reader perspective"** for a report page to one of these perspectives. When a user opens the Personalize pane on that page, they will only see the manageable list of fields from that perspective, not the full data model.
### 5. Key Considerations and Limitations
- **Unsupported Export:** Personalized visuals **are not captured** when exporting to PowerPoint or PDF.
- **Unsupported Sharing:** The feature is **not supported** for reports published using **Publish to web**.
- **Mobile Apps:** Supported on **tablets**, but **not supported** on the Power BI mobile apps for **phones**.    
- **Report Server:** Not available in Power BI Report Server.

