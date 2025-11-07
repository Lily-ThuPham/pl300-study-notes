[Design effective reports in Power BI - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/paths/power-bi-effective/)
# **Scope Report Design Requirements**
## **Determine Power BI Report Types**
[Determine report types - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-requirements/3-determine)

| Report Type        | Primary Goal                                                                           | Typical Audience           | Key Features / Design Focus                                                                                                                                      | Example Question it Answers                         | Contoso Store Example                                                                                                |
| ------------------ | -------------------------------------------------------------------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Dashboard** 📈   | To monitor and interpret key facts as quickly as possible.                             | Executives                 | <ul><li>High-level metrics (KPIs)</li><li>Focused, self-explanatory visuals</li><li>Minimal user interaction</li><li>Often a single page</li></ul>               | "How are we doing?" or "Are we there yet?"          | An executive dashboard showing key performance indicators (KPIs), targets, statuses, and trends.                     |
| **Analytical** 🔍  | To help users discover answers to a broad array of questions through interaction.      | Analysts                   | <ul><li>Many slicers for filtering</li><li>Complex visuals for in-depth detail</li><li>Focus on interactivity (drill-down, drillthrough, tooltips)</li></ul>     | "Why did that happen?" or "What might happen next?" | A sales analysis report that allows drilling into sales revenue from year down to day.                               |
| **Operational** ⚙️ | To monitor current data, make decisions, and act on them, often in real-time.          | Information Workers        | <ul><li>Streamlined UX, minimal clicks</li><li>Focuses on action, not deep analysis</li><li>Can include buttons to trigger actions in external systems</li></ul> | "What needs my attention right now?"                | An inventory report that shows current stock levels and includes a "Submit Order" button to create a purchase order. |
| **Educational** 🎓 | To provide clear narrative and guidance for users unfamiliar with the data or context. | General Audiences / Public | <ul><li>Clear narrative and detailed explanations</li><li>Guided user experience</li><li>Focus on clarity to minimize misinterpretation</li></ul>                | "What is this data telling me?"                     | A report describing COVID-19 vaccination progress that can be filtered by geographic region.                         |

---
## **UI requirements**
UI requirements relate to how reports are consumed and to the appearance and behavior of reports. Including:
1. Form factor 
2. Input method 
3. tyle or theme
4. Accessibility
### 1. Form Factor
Form factor describes the hardware size and page orientation (portrait/landscape) used to view reports.
- **Large Monitors:** Ideal for landscape orientation, allowing for several complex visuals on a single page.
- **Mobile Devices (Phones/Tablets):** Use portrait orientation by default. 
	- Design for this smaller form factor requires fewer and less complex visuals. 
	- Visuals should be larger and well-spaced for easy viewing and interaction. 
	- You can create a specific **mobile view** which might contain a subset of the visuals from the full-sized report.
### 2. Input Method
The way users interact with a device should influence your report design
- **Computers:** Use a keyboard and mouse.
- **Mobile Devices:** Rely on gestures like tap, pinch, and spread. They also support on-screen keyboards, voice control, and barcode readers.
- **Embedded Reports:** Input can be passed **programmatically** from the host application. For example, an application can automatically pass a customer ID to filter an embedded Power BI report to that specific customer.
- **Design Influence:** Knowing the input method affects decisions on the number and complexity of visuals, the spacing between them, and the use of interactive elements like slicers and buttons.
### 3. Style and Theme
Reports should have a consistent and distinctive appearance, typically determined by a deliberate theme that aligns with organizational branding.
- **A theme should include at a minimum:**
    - A brand mark or logo.
    - A palette of colors with sufficient contrast between them.
    - Text settings, including font, size, and color.
- **Best Practice:** To manage changes efficiently, design reports to use images and themes stored in a **central repository**. Changes made to the repository will automatically cascade to all reports that use it.
### 4. Accessibility
Reports must be designed to be usable by the broadest possible audience, including users with low vision or other physical disabilities.
#### 4.1 Accessibility Standards and Guidelines
**Web Content Accessibility Guidelines (WCAG)**: Ensure web content is accessible to people with disabilities.
**Key Principles**:
- **Perceivable**: Information and UI components must be presentable to users in ways they can perceive.
- **Operable**: UI components and navigation must be operable.
- **Understandable**: Information and the operation of the UI must be understandable.
- **Robust**: Content must be interpretable by a wide range of user agents, including assistive technologies.
#### 4.2 Power BI Accessibility Features
- **Keyboard Navigation**: Power BI visuals are fully navigable using a keyboard.
- **Screen Reader Compatibility**: Ensures that screen readers can interpret and read out the content.
- **High Contrast Colors**: Improves visibility for users with visual impairments.
- **Focus Mode**: Helps users concentrate on specific parts of the report.
- [**Show Data Table**: Provides an alternative way to view data in a tabular format](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-accessibility-overview)
- **Markers and Pattern Fills**: Helps users with color vision deficiencies distinguish different series in visuals.
- **Built-in Report Themes**: Considers accessibility guidelines to ensure better contrast and readability.
- **Accessibility Checker:** help identify and address accessibility issue
#### 4.3 Built-in Accessibility Features (Requiring Configuration)
As the report author, you must configure these features to create an accessible report.
- **Alt Text:** Provide descriptive alternative text for every meaningful visual, image, and shape. This text is read aloud by screen readers. The description should convey the key insight of the visual, not just its appearance.
- **Tab Order:** Use the **Selection pane** to set a logical navigation order for keyboard users. Decorative items should be hidden from the tab order to avoid confusion.
- **Titles & Labels:** Use clear, descriptive titles for reports and visuals. Avoid jargon and acronyms. Ensure all axis labels and data labels are easy to read and understand.
- **Markers:** Do not use color as the only way to convey information. Use different **marker shapes** (circles, squares, etc.) on line and scatter charts to distinguish different series.
- **Report Themes:** Use themes to ensure sufficient **color contrast** between text and backgrounds (at least a 4.5:1 ratio). Use colorblind-friendly palettes.
#### Power BI Accessibility Shortcuts and Features
##### 1. General Navigation (Applies to All Users)
These shortcuts are used for high-level navigation within the Power BI desktop.

| **Shortcut**               | **Action**                                                                                                                                           |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`?`** or **`Shift + ?`** | Displays the **keyboard shortcut dialog** with a list of common commands.                                                                            |
| **`Ctrl + F6`**            | **Moves focus between the main areas** of Power BI (e.g., from the report canvas to the page tabs, to the side panes).                               |
| **`Tab`**                  | Moves focus to the next object on the page (visual, slicer, button, etc.).                                                                           |
| **`Alt`**                  | (For Authors) Access accessibility feature by showing **KeyTips** for all commands in the ribbon (e.g., pressing `Alt` then `H` opens the Home tab). |
| **`Enter`**                | Selects or activates the focused item.                                                                                                               |
| **`Esc`**                  | Exits the current area, menu, or dialog.                                                                                                             |
##### 2. Consuming Visuals (For Report Consumers)
This 3-level hierarchy allows users to navigate _inside_ a visual.

|**Shortcut**|**Level**|**Action**|
|---|---|---|
|**`Ctrl + Right Arrow`**|**1. Enter Visual**|Moves focus from the visual's border to the _inside_ of the visual (e.g., the plot area).|
|**`Tab`**|**1. Enter Visual**|After entering a visual, `Tab` cycles between the main areas (e.g., plot area, X-axis, legend).|
|**`Enter`**|**2. Enter Area**|Selects a main area (like the plot area or axis) to explore it.|
|**`Tab` / `Arrow Keys`**|**2. Enter Area**|Once in an area, these keys cycle through the individual data points or categories.|
|**`Up / Down Arrow`**|**2. Enter Area**|In a multi-series chart, this can jump to data points in a different series.|
|**`Esc`**|**N/A**|Exits the current area or visual, moving one level back up.|
##### 3. Key Accessibility Tools
These are specific features designed to make reports accessible.

|**Shortcut**|**Tool / Feature**|**What It Does**|
|---|---|---|
|**`Alt + Shift + F11`**|**Show data as a table**|Opens an **accessible HTML table** displaying the data for the **currently selected visual**. This is the primary tool for screen readers to understand a visual's data.|
|**`Ctrl + Shift + F11`**|**Show visuals as tables**|Toggles the **entire report page** into a tabular format, converting most visuals into tables or matrices. This is a report-wide view preference.|
|**High Contrast**|(Windows Setting)|Power BI Desktop and the service will **automatically detect** Windows high-contrast settings and apply them to the report.|
|**`Alt + Shift + F10`**|**Visual Header**|Moves focus to the visual header menu (the `...` icon, filter icon, etc.) to access options like sorting or "Show as a table."|
##### 4. Authoring & Pane Navigation (For Report Authors)
These shortcuts are used for building and configuring reports in the side panes of Power BI Desktop.

|**Pane**|**Shortcuts**|
|---|---|
|**Formatting Pane**|• **`Tab`** moves through the controls in each card. • **`Enter`** expands/collapses a card or toggles an On/Off switch.|
|**Data Pane**|• **`Tab`** moves to the search bar and then to each table. • **`Right / Left Arrow`** keys expand or collapse a single table. • **`Alt + Shift + 9`** expands all tables. • **`Alt + Shift + 1`** collapses all tables. • **`Shift + F10`** opens the context menu for a field (e.g., to "Add to filters").|
|**Selection Pane**|• **`F6`** activates the selection pane (to use arrow keys). • **`Up / Down Arrow`** keys navigate between objects/groups. • **`Ctrl + Shift + S`** toggles the Show/Hide (visibility) of an object. • **`Ctrl + Shift + F`** moves an object forward (Bring up). • **`Ctrl + Shift + B`** moves an object backward (Send down).|

---
## **UX Requirements**

### 1. Enable Interactive Exploration
Interactivity allows users to engage with reports to discover insights on their own.
- **Drilling:** Configure visuals with hierarchies to allow users to **drill up** and **drill down** through levels of detail (e.g., from year to month).
- **Drill through:** Allow users to navigate from a summary visual to a detail page that is filtered to the specific data point they selected. This can be enhanced by adding **drillthrough buttons**.
- **Navigation:** Implement buttons or other navigation elements to move between report pages or to other related reports.
- **Filtering:** Provide **filters** and **slicers** to empower users to narrow down the data to what is most relevant to them.
### 2. Provide Flexible Data Access
Empower users to engage with and retrieve information in different ways.
- **Export Data:** Allow users to export the data from visuals into Excel or `.csv` files for further analysis.
- **Natural Language Q&A:** Include the **Q&A visual**, which lets users ask questions in plain language (e.g., "show top 10 products by sales") and receive an automatic visualization.
- **Data Alerts:** In the Power BI service, users can set up data alerts on dashboard tiles to be notified when a key metric crosses a specific threshold.
- **Actions:** Configure actions to link to external webpages, open applications, or trigger workflows (e.g., using Power Automate).
### 3. Support Scenario Analysis and Customization
Allow users to test different situations and personalize their view of the data.
- **What-If Analysis:** Use **what-if parameters** with sliders to let users dynamically adjust a variable (like a sales growth percentage) and see the immediate impact on their data.
- **Printing:** Ensure page layouts are designed to print well, either to a physical printer or as a PDF document.
### 4. Automate Delivery and Encourage Collaboration
Support ongoing engagement and teamwork directly within the Power BI service
- **Subscriptions:** Allow users to subscribe to a report page or dashboard to receive an email with a snapshot of the report on a scheduled basis (e.g., every Monday morning).
- **Collaboration:** Enable the **Commenting** feature, which allows users to add feedback, ask questions, and have conversations directly within the context of the report.

---
# **Report structure**
## 1.Report structure 
Report objects include:
- **Visuals** - Visualizations of semantic model data.
- **Elements** - Provide visual interest but don't use semantic model data. Elements include text boxes, buttons, shapes, and images.
## 2. Analytical Report layout 
### General Page Design
- An analytical report can have one or more pages. Each page should have a clear purpose and should not combine unrelated subjects.
- Pages consist of report objects, which can be data visuals or decorative elements like images and text.
### Placement
This principle concerns the ordered arrangement of report objects.
- **Reading Order:** Place the most important information in the **upper-left corner**. Arrange other elements to be read from left to right and top to bottom. For right-to-left (RTL) languages, place the most important information in the **upper-right**.
- **Alignment:** Align the vertical and horizontal edges of report objects to create an ordered and visually pleasing layout.
- **Rule of Thirds:** For a more dynamic layout, divide the page into an invisible 3x3 grid. Place key report objects along the lines or at their intersections.
### Balance
Balance is the visual weight of objects spread across the page.
- **Symmetrical Balance:** Distribute the visual weight evenly on both halves of the page.
- **Asymmetrical Balance:** Achieved through contrast. A common guide is the **golden ratio**, where a page has one large visual to draw initial attention, supported by smaller visuals that provide additional context.
### Proximity
Proximity is about the nearness of report objects.
- **Grouping:** Place related visuals near one another to form logical groups.
- **Separation:** Use white space to visually separate different groups of objects on the page. This avoids clutter and makes the report easier to understand.
### Contrast
Contrast is used to emphasize important objects and direct the user's attention.
- **How to Achieve:** Use opposing elements like contrasting colors, different font sizes or properties (bold, regular), or different line weights.
- **Purpose:** To guide the report consumer to where they should look first or which visual is most important.
### Repetition
Repetition creates association, consistency, and strengthens the report layout.
- **How to Achieve:** Repeat a design choice for related objects. For example, use the same visual type (like a single-value card) for all of your key metrics.
- **Purpose:** This helps users quickly understand and interpret a group of related items because they are presented in a consistent, predictable way.
## 3. Designing Visually Appealing Reports
A well-designed report guides the user to quickly find and understand answers. Good design can also allow for more visuals on a page without it appearing cluttered.
### Space
Space is essential for reducing clutter and increasing readability.
- **Margins:** Maintain a consistent border area around the edges of each report page. Margin sizes should be equal on both sides, with the top and bottom margins potentially being different to accommodate titles or slicers.
- **Object Spacing:** Provide sufficient space around and between visuals. This prevents overlapping, especially with visual headers, which can make them difficult to interact with. Use different amounts of space to visually separate sections, but avoid excessive spacing which can unbalance the layout.
### Size
Size relates to both the report page and the visuals on it.
- **Page Size:** Can be set to predefined or custom dimensions. Be aware that very large page sizes filled with many visuals can increase the time it takes for the report to render.
- **Visual Size:** As a general rule, the **more important the visual, the larger its size**. Larger visuals naturally draw the user's focus first. When using a series of similar visuals, such as card visuals, they should be equally sized.
### Alignment
Properly aligning visuals ensures the report looks ordered and professional.
- The edges of different visuals should be in alignment, and the spacing between them should be consistent. The alignment commands on the **Format** ribbon can help with this.
- **Implied Sections:** Create logical groups by aligning visuals in close proximity with consistent spacing between them.
- **Explicit Sections:** Create clear, visible groups by placing colored background shapes behind a set of related visuals.
### Color
Use color sparingly and meaningfully to avoid distracting the user.
- **Palette:** Stick to a few softer colors as a base, often aligned with corporate branding. The data itself should be the focus. Reserve bolder, more vibrant colors to highlight exceptions or key data points.
- **Contrast:** Ensure that colors are sufficiently contrasting. This is critical for creating accessible reports for users with low vision. For example, avoid using light yellow text on a white background.
##### Color theory
Color theory includes: 
- Color wheel
- Color harmony 
- Color psychology 
- Color symbolism
1.  **Color Wheel**:
    - **Primary Colors**: Red, blue, yellow.
    - **Secondary Colors**: Mixes of primary colors like orange, green, purple.
    - **Tertiary Colors**: Mixes of primary and secondary colors.
2. **Color Harmony**:
    - **Complementary Colors**: Opposite hues on the color wheel.
    - **Analogous Colors**: Groups of colors next to each other on the color wheel
    - **Triadic Colors**: A three-pointed triangle selection from the color wheel.
    - **Monochromatic Colors**: Variations of the same color.
3. **Color Psychology and Symbolism**:
    - Colors can evoke emotions and influence behavior.
    - Different cultures may have different interpretations of colors.
### Consistency
Strive for consistency across all report design elements, including spacing, size, alignment, and especially format options like fonts, font sizes, and colors.
- **Report Theme:** The quickest and most effective way to enforce consistency is to use a **report theme**. A theme applies a predefined set of formatting options to the entire report, including visuals and the Filters pane.
- **Customization and Overrides:** You can use a built-in theme as a starting point and customize it. However, be aware that if you explicitly set a format option on a visual (e.g., manually changing a bar color), that setting will **override** the report theme. If you later change the theme, your manually overridden settings will not be updated.
- **Sharing Themes:** You can export your report theme as a JSON file and apply it to other reports to ensure a consistent look and feel across all of your projects.

---
## 4. Guide to Selecting Power BI Visuals

| Visual Category  | Purpose / Use Case                                                            | Recommended Visuals                                                                                    | Key Design Tips & Best Practices                                                                                                                                                                                                                                                                    |
| ---------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Categorical**  | To show data across multiple distinct categories.                             | <ul><li>Bar Chart</li><li>Column Chart</li></ul>                                                       | <ul><li>**Sort by value** (descending or ascending) to draw attention, not alphabetically.</li><li>Avoid using a line chart, as it incorrectly implies a relationship between unrelated categories.</li><li>Bar charts are often easier to read than column charts in wide, short spaces.</li></ul> |
| **Time Series**  | To show trends and values over a period of time.                              | <ul><li>Line Chart</li><li>Column Chart</li><li>Area Chart</li><li>Ribbon Chart</li></ul>              | <ul><li>The X-axis must always be sorted chronologically.</li><li>Use a **line chart** for continuous data. You can add a forecast for projections.</li><li>Use a **column chart** if there might be gaps in the data to avoid showing a misleading trend line.</li></ul>                           |
| **Proportional** | To show data as a part of a whole and compare distributions.                  | <ul><li>100% Stacked Bar/Column</li><li>Funnel Chart</li><li>Treemap, Pie, Doughnut</li></ul>          | <ul><li>These visuals show the **relative percentage**, not the actual values.</li><li>They should only be used when all values are either positive or all are negative.</li><li>Useful for comparing distributions across different categories (e.g., product mix per store).</li></ul>            |
| **Numeric**      | To display high-level, single-value callouts that demand immediate attention. | <ul><li>Card</li><li>Multi-row Card</li></ul>                                                          | <ul><li>Ideal for dashboards and analytical reports to communicate important data quickly and clearly.</li></ul>                                                                                                                                                                                    |
| **Grid**         | To convey detailed information in a structured, tabular format.               | <ul><li>Table</li><li>Matrix</li></ul>                                                                 | <ul><li>Use **conditional formatting** (data bars, icons, colors) to add visual context to the numbers.</li><li>A **matrix** is excellent for hierarchical navigation, allowing users to drill down on both rows and columns.</li></ul>                                                             |
| **Performance**  | To show a value's progress or status against a target.                        | <ul><li>KPI</li><li>Gauge</li><li>Table/Matrix with conditional formatting</li></ul>                   | <ul><li>A KPI visual requires three inputs: a **value**, a **target**, and a **time series**.</li><li>Use colors or icons to clearly indicate status (e.g., favorable vs. unfavorable variance).</li></ul>                                                                                          |
| **Geospatial**   | To display data that has a geographic component.                              | <ul><li>Map (shows bubbles for specific locations)</li><li>Filled Map (shows shaded regions)</li></ul> | <ul><li>Choose the map type based on your data's granularity: a **Map** is better for dispersed cities, while a **Filled Map** is better for states or countries.</li><li>Consider if a map is truly necessary; sometimes a simple bar chart of locations is clearer.</li></ul>                     |

---
## 5. Report Filters and Slicers
[Apply filters and slicers to reports - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/6-report-filters)
### The Five Levels of Report Filtering
Filtering in Power BI is a layered process. Understanding these levels is key to controlling how your report behaves.
1. **Semantic Model (Row-Level Security - RLS):** This is a **security** filter applied at the data model level. It restricts data visibility based on the user who is viewing the report. This filter cannot be seen or overridden by the report designer.
2. **Report-Level Filter:** A global filter applied in the **Filters pane** that affects **all visuals on all pages** of the report.
3. **Page-Level Filter:** A filter applied in the **Filters pane** that affects **all visuals on a single, specific page**. It adds to any existing report-level filters.
4. **Visual-Level Filter:** A filter applied in the **Filters pane** that affects only **one, specific visual**. It adds to any existing report and page-level filters.
5. **Measure Filter (DAX):** A filter applied directly within a DAX formula using functions like `CALCULATE` or time intelligence functions. This type of filter can **override** filters from the report structure (visual, page, and report levels).
### Applying Filters at Design Time
#### Using the Filters Pane
The Filters pane is your primary tool for adding persistent filters to your report structure. It has three sections that correspond to the filter levels:
- **Filters on all pages:** Sets report-level filters.
- **Filters on this page:** Sets page-level filters.
- **Filters on this visual:** Sets visual-level filters. This section is only visible when a single visual is selected.

**Key Features of the Filters Pane:**
- **Filtering with Measures:** Unlike report and page-level filters, a **visual-level filter** can use a measure to eliminate groups (e.g., show only stores where total sales are greater than $1M).
- **Filter Types:** You can apply different types of filters to a field, including *Basic (selecting from a list), Advanced (e.g., "contains" or "starts with"), Top N, and Relative Date/Time.*
- **Locking and Hiding:** You can **lock** filters to prevent end-users from changing them. You can also **hide** filters so they are not visible to users at all. Hiding is useful for data cleanup filters, like removing blanks.
#### Using Slicers
A slicer is a visual on the report canvas whose sole purpose is to filter other visuals on the page.
- **Behavior:** By default, a slicer filters all other visuals on the same page. You can change this behavior using the **Edit interactions** feature. You can also use **Sync slicers** to make a slicer affect visuals on other pages.
- **Layout:** The slicer's layout automatically adapts to the data type of the field it's using:
    - **Text:** Creates a list of items to select.
    - **Numeric/Date:** Creates a range slider (e.g., "between").
- **Styles and Options:**
    - You can change the style of a list slicer to a **dropdown** to save space on the report page. Dropdown slicers also improve performance as they only query the data when opened.
    - You can enable options like **Single select** to force the user to choose only one item at a time.
    - Date slicers have a **Relative date** option for filtering by periods like "last 7 days" or "next 2 weeks."

---
## 6. Other Filtering Techniques

Beyond the Filters pane and Slicers, you can enable filtering through user interaction.
### Visual Interactions
By default, selecting a data point in one visual (e.g., a column in a bar chart) will **cross-filter** or **cross-highlight** other visuals on the same page. This makes any visual act like a temporary slicer. This behavior can be modified or disabled at design time by using the **Edit interactions** feature.
### Drillthrough
This allows users to navigate from a data point on a summary page to a dedicated **drillthrough page**. The destination page is automatically filtered by the context of the data point the user selected.
### Report Tooltip
These are custom, small report pages that appear when a user hovers over a data point. The tooltip page automatically receives the filter context from that data point, allowing you to show more detailed, contextual information on hover.
### Bookmarks
A bookmark captures and saves a specific view of a report page, including the state of all filters, slicers, and visuals. Bookmarks can be created by both authors and consumers (personal bookmarks). They can be activated from the Bookmarks pane or by clicking a button, image, or shape. A common use case is to create a bookmark of the default filter state and link it to a **"Reset slicers" button**.
### Report Options and Query Reduction
Report authors can configure settings to control the user's filtering experience and improve performance.
- **Filter Control:** You can disable persistent filters, hide visual headers, hide the filter icon on a specific visual, or prevent users from changing filter types (e.g., from basic to advanced).
- **Query Reduction:** You can configure options to reduce the number of queries sent, such as adding an "Apply" button to slicers and filters so that changes are only submitted after the user clicks it.
### Filters Pane vs. Slicers: A Comparison
| Feature / Aspect       | Filters Pane                                                                                                                    | Slicers                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Performance**        | Faster report rendering (no visual to draw).                                                                                    | -                                                                                   |
| **Page Space**         | Takes up no space on the report canvas.                                                                                         | -                                                                                   |
| **Filter Complexity**  | Supports advanced types like **Top N** and conditions like "contains" or "is blank." Can also filter by a **measure's result**. | 🚩Limited to simpler selections (list, dropdown, range).                            |
| **Control**            | Filters can be **locked** to prevent changes and **hidden** from users entirely.                                                | -                                                                                   |
| **Disadvantages**      |                                                                                                                                 |                                                                                     |
| **Design Flexibility** | Limited styling options; fixed position on the side of the report.                                                              | Can be placed anywhere on the page and highly formatted to match the report theme.  |
| **User Experience**    | Can be less intuitive; applied visual-level filters are not always obvious to the user.                                         | Selections are always visible on the canvas, making the current filter state clear. |
| **Performance**        | -                                                                                                                               | 🚩Slower report rendering due to the time it takes to draw the visual.              |
| **Page Space**         | -                                                                                                                               | 🚩Takes up valuable space on the report canvas that could be used for data visuals. |

### Filtering tips

Here are some filtering tips to help you produce successful report designs:
- Use either filters or slicers. Avoid using both filter techniques because it can create confusion.
- In the **Filters** pane, consider locking or hiding visual-level filters to avoid confusing report consumers. (Often, report consumer shouldn't modify or see visual-level filters.)
- Create a bookmark to reset all slicers to default values. Then, add a button to the page to invoke the bookmark. For example, the button could be captioned as _Reset slicers_.
- When a requirement is in place to lay out many slicers, consider creating a page that is dedicated to showing all slicers. For example, the page could be named _Slicers_. Sync the slicers to other pages and then set the slicers as hidden on those pages. This design technique requires that report consumers should always go to the _Slicers_ page to modify slicer settings. To help them, you can add a page navigation button at a consistent location on each page so that they can easily return to the _Slicers_ page.
- Consider using other visuals in place of slicers. Be sure to show report consumers how to cross filter by using these visuals.