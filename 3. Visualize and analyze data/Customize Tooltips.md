[Customizing tooltips in Power BI Desktop - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-custom-tooltips?tabs=powerbi-desktop)
**Tooltips** provide contextual information and detail when a user hovers over a data point on a visual. Power BI offers two main ways to customize them: by adding fields to the tooltip bucket and by creating a dedicated report page.
_**Extra:**[Create modern visual tooltips (preview) - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-visual-tooltips?tabs=desktop-new)_
### 1. Default Tooltips and Simple Customization
By default, a tooltip displays the value and category of the data point. You can easily add more information to this default tooltip.
- **How to Customize:**
    1. Select the visual you want to modify.
    2. In the **Visualizations** pane, find the **Tooltips** field well.
    3. Drag any additional fields or measures you want to display from your Data pane into this bucket.
    4. In the **Format > Properties or General > Tooltips**, you can also customize **text style** and **background**.
- **Changing Aggregation:** You can also change the aggregation of a field in the Tooltips bucket (e.g., from Sum to Average) by clicking the arrow next to its name.
### 2. Report Page Tooltips (Advanced Customization)
For a richer, fully customized experience, you can design an entire report page to act as a tooltip. This allows you to include multiple visuals, images, and formatted text.
#### Step 1: Create the Tooltip Page
1. Create a **new page** in your report.
2. Go to the **Format** pane for that new page.
3. Under **Canvas settings**, change the **Type** to **Tooltip**. This resizes the page to a small, tooltip-friendly canvas.
4. Under **Page information**, turn the **Allow use as tooltip** slider to **On**. This is the crucial step that registers the page as a potential tooltip.
5. Design your tooltip by adding visuals (cards, charts, images) to the small canvas.
#### Step 2: Configure the Tooltip to Appear
You can make the tooltip appear either automatically or manually.
- **Automatic Trigger (Recommended):**
    1. On your tooltip page, drag the field(s) that should trigger the tooltip into the **Tooltips** field well at the bottom of the Visualizations pane.
    2. Now, on any other report page, any visual that uses that same field will automatically show your custom tooltip page when a user hovers over it. The tooltip will be filtered to the specific data point being hovered over.
- **Manual Trigger:**
    1. Select a specific visual on your main report page.
    2. Go to the **Format** pane for that visual and expand the **Tooltips** card.
    3. Change the **Type** to **Report page**.
    4. For **Page**, select the tooltip page you created. This manually overrides the default or automatic tooltip for that specific visual.

### Comparison of Tooltip Types

|**Feature**|**Simple Tooltip (Fields in Bucket)**|**Report Page Tooltip**|
|---|---|---|
|**Content**|A simple list of text values and numbers.|Can include multiple **visuals**, images, and rich text formatting.|
|**Complexity**|Very easy and quick to set up.|Requires more effort to design a separate report page.|
|**Flexibility**|Limited formatting.|Highly flexible and visually rich.|
|**Use Case**|Adding a few extra data points to the default hover-over.|Creating a detailed "glance card" with charts and KPIs that provide deep context.|
### Considerations and Limitations
- **Unsupported Visuals:** Report page tooltips do not work with Python and R visuals.
- **Dashboards:** Dashboards in the Power BI service do not support report page tooltips; they will show the basic tooltip instead.
- **Line Charts:** When used on a line chart with multiple lines (a legend), a report tooltip will show aggregated data for all lines at that point, not just the specific line you are hovering over.
- **Cross-Highlighting:** Report tooltips always show the **highlighted** data, even if you are hovering over a faded (un-highlighted) part of a visual.