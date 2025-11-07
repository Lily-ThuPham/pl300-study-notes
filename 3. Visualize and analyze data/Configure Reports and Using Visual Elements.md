To create a professional and visually appealing report, you must configure the properties of the report page and its elements. These settings are primarily found in the **Format pane** (the paint roller icon) in Power BI Desktop.

---
## 1. Formatting the Report Page

When **no visual is selected**, the Format pane shows the settings for the report page itself.

| Setting Card          | What It Does                                                       | Key Options & Best Practices                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Page information**  | Sets the name of the page and controls its visibility.             | <ul><li>**Name:** The name that appears on the page tab.</li><li>**Allow use as tooltip:** Enables this page to be used as a custom [report tooltip](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-tooltips).</li><li>**Allow Q&A**.</li></ul>                                                                                                                                                |
| **Canvas settings**   | Defines the size and orientation of the report page.               | <ul><li>**Type:** Choose a predefined size like `16:9` (standard), `Letter`, or a custom size in pixels.</li><li>**Vertical alignment:** Controls how visuals are aligned on the page if the canvas is taller than the screen.</li></ul>                                                                                                                                                                          |
| **Canvas background** | Sets the background for the area **where you place your visuals**. | <ul><li>**Color:** Sets a background color for the canvas.</li><li>**Image:** Adds a background image.</li><li>**Transparency:** The key setting. By default, it's 100% transparent (showing the wallpaper behind it). Reducing this makes the canvas background more opaque.</li></ul>                                                                                                                           |
| **Wallpaper**         | Sets the background for the area **outside** your report page.     | <ul><li>**How it works:** The wallpaper is the furthest-back element. If your canvas background is transparent, the wallpaper will be visible behind your visuals.</li><li>**⚠️ Export to PDF Warning:** The **Export to PDF** feature **does not include the wallpaper**. If you use a dark wallpaper and set your report text to a light color, the text may be nearly invisible in the exported PDF.</li></ul> |
## 2. Page view settings 
Accessing Page view setting **Report view -> View**
The first set of Page view settings controls the display of your report page relative to the browser window. Choose between:
- **Fit to page** (default): Contents are scaled to best fit the page
- **Fit to width**: Contents are scaled to fit within the width of the page
- **Actual size**: Contents are displayed at full size
**Page option**
- **Show gridlines**: Turn on gridlines to help you position objects on the report canvas.
- **Snap to grid**: Use with **Show gridlines** to precisely position and align objects on the report canvas.
- **Lock objects**: Lock all objects on the canvas so that they can't be moved or resized.
- **Selection pane**: The **Selection** pane lists all objects on the canvas. You can decide which to show and which to hide.

## 3. Using Improved Visual Headers

The modern visual header appears **within the visual itself**, allowing for better alignment and a cleaner layout. This is the default behavior for all new reports.
- **Positioning:**
    - If a visual has a **title**, the header icons (pin, expand, ellipses) appear inside the visual, aligned to the right on the same line as the title.
    - If a visual has **no title**, the header floats above the visual, aligned to the right.
    - If a visual is positioned at the very **top of the report**, the header snaps to the **bottom** of the visual to ensure it's always accessible.
- **Configuration:** Each visual has a **Header icons** card in its **Format** section, where you can adjust the appearance and visibility of the icons.
- **Viewing Changes:** Changes to the visual header visibility are only visible in the **reading view** of the Power BI service, not while editing in Power BI Desktop.
- **Enabling for Existing Reports:** For older reports, you must enable this feature by going to **File > Options and settings > Options**, and in the **Report settings** section, check the box for **"Use the modern visual header with updated styling options."**

## Building and Configuring the Filters Pane

The **Filters pane** is a dedicated area in a Power BI report where you can add, configure, and display filters for your report, pages, and visuals.

### Building the Filters Pane
- **Automatic Filters:** When you add a field to a visual, Power BI **automatically adds a filter** to the "Filters on this visual" section for that field.
- **Manual Filters:** You can drag any other field from your data model into one of the three sections of the Filters pane to create **report-level**, **page-level**, or **visual-level** filters.

| **Filter Type**         | **Scope**                                                                                   |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| **Report filter**       | Applies to **all pages** in the report.                                                     |
| **Page filter**         | Applies to **all visuals on a single, specific page**.                                      |
| **Visual filter**       | Applies to only **one, specific visual**.                                                   |
| **Drillthrough filter** | Passes filter context from a source page to a specific **destination (drillthrough) page**. |
### Controlling Visibility
You can control whether the entire Filters pane is visible to users.
- **For Report Consumers (Reading Mode):** To hide the pane from your end-users after publishing, select the **eye icon (👁️)** next to the "Filters" title in the pane while in Power BI Desktop.
- **For Report Authors (Editing Mode):** To temporarily hide the pane in Power BI Desktop to get more canvas space, go to the **View** tab and uncheck the **Filters** box.
### Locking and Hiding Individual Filters
You have granular control over each filter card within the pane.
- **Lock filter 🔒:** This makes the filter **visible but not changeable** for the report consumer.
- **Hide filter 👁️‍🗨️:** This makes the filter **completely invisible** to the report consumer. This is useful for data cleanup filters, like excluding nulls, that the end-user doesn't need to see or modify.

**Bookmarks:** The state of the Filters pane (open, closed, visible) and the state of the filters themselves can be captured in **bookmarks**.
### Formatting the Filters Pane
You can format the pane to match the look and feel of your report. These options are found in the **Format pane** when the report page (wallpaper) is selected.
- **Pane Formatting:** You can change the background color, transparency, border, and title font/color of the entire pane.
- **Card Formatting:** You can set different background colors, borders, and fonts for filter cards based on their state:
    - **Default:** How the card looks when no filter is applied.
    - **Applied:** How the card looks after a user has made a selection. Using different colors for each state makes it obvious which filters are active.
### Other Configuration Options
- **Sort Filters:** By default, filters are sorted alphabetically. You can enable a custom sort by simply dragging and dropping a filter to a new position within its section.
- **Rename Filters:** You can double-click a filter's title to rename it for clarity. This only changes the display name in the filter card, not the field name in your data model.
- **Enable Search:** A search box can be enabled in the report settings to allow users to easily find specific filter cards.
- **Add "Apply" Button (Query Reduction):** In **File > Options**, you can enable an **"Apply" button** for the Filters pane. This allows users to make multiple filter selections and apply them all at once, which reduces the number of queries sent and can improve performance.