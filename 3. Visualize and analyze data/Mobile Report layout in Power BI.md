**APPLIES TO:** ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service
[About mobile-optimized Power BI reports - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/power-bi-create-mobile-optimized-report-about)
While any Power BI report page can be viewed on a mobile device (typically in landscape orientation), you can design a specific **mobile-optimized view** for a better experience in portrait mode. This is not a separate report but a custom layout of your existing report page.
In the Power BI mobile app, reports with mobile-optimized pages are identified with a special icon.

---
### 1. Mobile Authoring Features & Interface
Power BI provides a dedicated **Mobile layout view** in both Power BI Desktop and the Power BI service to create these optimized views.
**How to Access:**
- Use the **layout switcher icons** (web vs. mobile) at the bottom of the Power BI window.
- Go to the **View** ribbon and select **Mobile layout**.
The changes you made on **Mobile layout** will not effect the web report layout. 
The mobile layout interface consists of several key components:

| **Component**            | **Description**                                                                             | **Key Function**                                                                                                                      |
| ------------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Mobile Layout Canvas** | An interactive, phone-shaped canvas with a grid.                                            | This is where you drag and place visuals to build your mobile layout. The canvas is interactive, so you can test buttons and slicers. |
| **Page Visuals Pane**    | A pane that lists all visuals available on the original report page, including hidden ones. | This is your palette. You **drag and drop** visuals from this pane onto the mobile canvas to create your layout.                      |
| **Visualizations Pane**  | The standard formatting pane (paint roller icon).                                           | Used to apply **mobile-specific formatting** to a visual after it has been selected on the canvas.                                    |
| **Selection Pane**       | The standard selection pane for managing object visibility and layering.                    | Used to change the **layering order** of visuals on the mobile canvas, which is important when visuals overlap.                       |
[![Screenshot of mobile layout view in Power BI.](https://learn.microsoft.com/en-us/power-bi/create-reports/media/power-bi-create-mobile-optimized-report-mobile-layout-view/power-bi-mobile-layout-view.png)](https://learn.microsoft.com/en-us/power-bi/create-reports/media/power-bi-create-mobile-optimized-report-mobile-layout-view/power-bi-mobile-layout-view.png#lightbox)
### 2. Building the Mobile Layout
You have two primary methods for creating your mobile layout.
#### Method 1: Automatic Mobile Layout Creation
- **What it is:** Power BI can automatically generate a mobile layout for you by selecting the **Auto-create mobile layout** option.
- **How it works:** The engine analyzes your desktop layout (reading from top to bottom, left to right) and places the visuals on the mobile canvas, trying to preserve functionality.
- **When to Use:** This is an excellent **starting point**, especially for complex reports. It works best with reports that have a simple, horizontal structure and struggles with background images or heavily overlaid visuals.
#### Method 2: Manual Layout Creation
This method gives you full control over the placement and size of every visual
1. **Place Visuals:** **Drag and drop** visuals from the **Page Visuals pane** onto the mobile canvas.
2. **Resize and Reposition:** Select a visual on the canvas and use the handles to resize it. Hold the **Shift** key while dragging a handle to maintain the visual's aspect ratio.
3. **Layer Visuals:** Use the **Selection pane** to change the front-to-back order of any overlapping visuals.
### 3. Optimizing Visual Formatting for Mobile
The **Visualizations pane** allows you to apply formatting that is **specific to the mobile layout only**.
- **Independent Formatting:** When you change a format setting in the mobile layout (e.g., font size), it **disconnects** from the desktop layout setting. A small icon will appear to indicate that the setting has been changed for mobile.
- **Reverting Changes:** You can discard any mobile-specific formatting changes for a visual, which will cause it to reconnect to and inherit its formatting from the desktop layout.
**Common Mobile Formatting Examples:**
- Changing a vertical page navigator into a horizontal one.
- Changing a visual's font size to be smaller and more suitable for a small screen.
- Turning off a visual's legend or axis titles to save space, and turning on data labels instead.
### 4. Best Practices for Mobile Design
- **Focus on Key Content:** Only include the most significant and frequently used visuals in your mobile layout.
- **Simplify:** Use smaller font sizes for titles and remove non-essential details like axis titles or gridlines.
- **Arrange for a Story:** The flow is top-to-bottom. Place the most important visuals at the top.
- **Space Visuals Out:** Leave a small margin between visuals to avoid a cluttered look. Avoid placing large visuals side-by-side.
- **Avoid Double Scrollbars:** Set the height of each visual so that all its content is visible, preventing a scrollbar _inside_ a visual.

### 5. Publishing and Limitations
- **Publishing:** When you publish the main report from Power BI Desktop to the service, the mobile-optimized layout is **published at the same time**.
- **Slicer Selections:** Slicer selections made while editing in the mobile layout view do not carry over to the web layout. When the report is published, the initial slicer selections will always be those that were defined in the **web layout**
- **Tooltips:** Tooltips are disabled on the interactive mobile layout canvas during editing but are fully functional when the report is viewed on a mobile app.