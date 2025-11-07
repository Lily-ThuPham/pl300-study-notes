[Intro to dashboards for Power BI designers - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/service-dashboards)
**Dashboards** are a feature of the **Power BI service** designed for monitoring key business metrics at a glance. They provide a single-page canvas where you can consolidate and display the most important highlights from your data story.
**APPLIES TO:** ![](https://learn.microsoft.com/en-us/power-bi/includes/media/no-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service

---
## 1. Dashboards vs. Reports
It's crucial to understand the differences between dashboards and the reports they are often based on.

| **Feature**        | **Dashboard**                                                                                                      | **Report**                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| **Availability**   | Power BI service only                                                                                              | Power BI Desktop & Service                                                                  |
| **Pages**          | **One single page** (canvas)                                                                                       | Can have **multiple pages**                                                                 |
| **Data Source(s)** | Can combine visuals from **multiple** reports and semantic models.                                                 | Based on a **single** semantic model.                                                       |
| **Interactivity**  | Limited interactivity. Tiles update when data refreshes. Clicking a tile typically navigates to the source report. | **Highly interactive**. Supports filtering, slicing, cross-highlighting, drillthrough, etc. |
| **Filtering**      | **No** direct filtering or slicing on the dashboard canvas itself.                                                 | Extensive filtering options via Slicers and the Filters pane.                               |
| **Creation**       | Created in the Power BI service, primarily by **pinning** visuals.                                                 | Created primarily in Power BI Desktop.                                                      |
| **Key Feature**    | **Data alerts** can be set on certain tiles (Cards, KPIs, Gauges).                                                 | Supports features like Bookmarks, Drillthrough, detailed data views.                        |
## 2. Dashboard Tiles
**Tiles** are the individual visualizations displayed on a dashboard. They are essentially snapshots or pointers to your data.
### How Tiles are Created:
- **Pinning from Reports (Most Common):** Hover over a visual in a Power BI report and click the **Pin icon (📌)**. You can pin to a new or existing dashboard.
- **Pinning an Entire Report Page (Live Tile):** Pinning a whole page creates a special "live tile." This tile remains interactive (cross-filtering works within the tile) and automatically reflects changes made to the report page.
- **Pinning from Q&A:** Ask a question using the dashboard's Q&A box, and pin the resulting visual.
- **Pinning from Excel:** Pin ranges, tables, or charts from Excel workbooks connected via OneDrive for Business.
- **Pinning from another Dashboard:** Copy a tile from one dashboard to another.
- **Adding Tiles Directly:** Use the **Edit > Add a tile** option directly on the dashboard to add standalone content like:
    - Text boxes
    - Images (linked via URL)
    - Videos (YouTube or Vimeo, linked via URL)
    - Web content (embedding HTML code, like a Twitter feed)
    - Custom streaming data (Microsoft Stream)
#### Real-time Data in Power BI 
- **Push Datasets**:
    - Data pushed from external sources like SQL Server.
    - Stored in Power BI and visuals update in real time.
    - Create report visuals and dashboards as with any imported dataset.
- **Streaming Datasets**:
    - Constantly updated from sources like AWS or Oracle.
    - Not stored in Power BI; used directly in dashboard tiles.
    - No regular report functionality like filters or slicers.
- **PubNub Streaming Datasets**:
    - High reliability and low latency.
    - No data stored in Power BI; real-time data is live streamed.
    - Compatible with web, mobile, and IoT platforms.
#### Choose the right real-time dataset 
- **Push Datasets**: Ideal for creating report visuals that update in real time.
- **Streaming Datasets**: Best for live data without storage in Power BI.
- **PubNub Streaming Datasets**: Suitable for scalable, real-time interactive applications.
### Interacting with Tiles:
- **Clicking a Tile:** Usually navigates you to the underlying report, Q&A question, or custom link associated with it.
- **Moving and Resizing:** In Edit mode, you can drag tiles to rearrange them and use the handles to resize.
- **Tile Menu (Ellipsis ...):** Hovering over a tile reveals a menu with options like:
    - Edit details (change title, subtitle, link)
    - View in focus mode
    - Export data (.csv)
    - Run insights
    - Pin tile (to another dashboard)
    - Delete tile
## 3. Advantages of Dashboards
- **Monitoring:** Provide a quick, consolidated view of the most important metrics.
- **Consolidated View:** Can bring together visuals from multiple reports and data sources.
- **At-a-Glance Insights:** Designed to show highlights and key performance indicators (KPIs) efficiently.
- **Data Updates:** Tiles automatically update when the underlying semantic model is refreshed.
## 4. Who Can Create Dashboards?
- Creating dashboards is a **creator** feature.
- Requires a **Power BI Pro or PPU license** (unless creating in your personal "My Workspace").
- Requires **edit permissions** on the reports you want to pin visuals from.
## 5. Considerations and Limitations
- **Formatting Loss:** When pinning a visual, some formatting (like background color, borders, specific title formatting) might not be preserved on the tile. Conditional formatting is not applied.
- **Static Visual Type:** If you pin a line chart and later change the visual in the report to a bar chart, the dashboard tile will **remain a line chart** (though the data will refresh).
- **Limited Interactivity on Tiles:** Most tiles are not interactive like report visuals (except for live pinned pages). Features like tooltips are basic, and buttons do not trigger actions.
- **No Desktop Creation:** Dashboards cannot be created or edited in Power BI Desktop.
- **Sharing:** Tiles pinned from reports shared with you cannot typically be re-pinned.
## 5. Generating a QR Code for a Dashboard Tile
QR codes in Power BI connect a physical location directly to a specific dashboard tile, accessible via the Power BI mobile app.
- **Purpose:** To allow users to quickly access relevant data by scanning a code placed in a physical location (e.g., on a machine, in a report binder).
- **Availability:** Can be generated in the **Power BI service** for tiles on any dashboard you can view (edit permissions not required).

**How to Create:**
1. Open a dashboard in the Power BI service.
2. Select **More options (...)** on the tile you want a QR code for.
3. Choose **Open in focus mode**.
4. In focus mode, select **More options (...)** again and choose **Generate QR Code**.
5. A dialog box with the QR code appears.
6. You can **Download** the QR code as a JPG file to print or add to documents.

**How it's Used:**
- Colleagues (who have already been granted access to the dashboard) can scan the printed QR code using their Power BI mobile app.
- The app will directly open the specific tile in focus mode.
## 6. Using Dashboard Themes
Dashboard themes allow you to apply a consistent color scheme to your entire dashboard, affecting all visuals pinned to it (with some exceptions).
- **Purpose:** To align the dashboard's appearance with corporate branding, seasonal colors, or a specific visual style.
- **Availability:** Configured in the **Power BI service** (requires edit permissions for the dashboard). Themes are visible on mobile devices but cannot be created there.
- **Effect:** Applying a theme changes the colors used in the dashboard's visuals. This **does not affect** the colors in the original underlying reports.

**How to Apply a Theme:**
1. Open a dashboard you can edit.
2. Select **Edit > Dashboard theme**.
3. Choose from:
    - **Pre-built themes:** Select a standard theme like "Dark."
    - **Custom theme:** Manually select colors for foreground, background, and tiles. You can also optionally add a background image by providing a public **Image URL**.
    - **Upload JSON theme:** Upload a JSON file containing theme definitions. You can use the same JSON theme files created for Power BI Desktop reports or find themes in the Power BI Community Theme Gallery.

**Theme Interaction with Pinned Tiles:**
- When pinning a tile from a report that already has a theme applied, you can choose:
    - **Keep current theme:** The tile retains its original report colors.
    - **Use dashboard theme:** The tile adopts the colors of the dashboard's theme.
- **Limitations:** Dashboard themes cannot be applied to pinned live report pages, iframe tiles, SSRS tiles, workbook tiles, or images. Card visuals have specific font behavior (DIN font, black text by default, but color can be changed via a custom theme).