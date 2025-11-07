# Common visualizations 
[Changing visualization types in Power BI](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-report-change-visualization-type)
[Data visualization for beginners](https://powerbi.microsoft.com/en-us/data-visualization/)
[[Custom Visuals]]
[[Artificial Intelligence Visuals (AI Visuals and Features)]]
### What are visualizations? 
Graphical representations of data, visualization tools like Power BI transform the data into a compelling, interactive and easily digestible format. 
Converting raw data into a visual format can help identify patterns, trends and insights that might not be apparent in text based data.
### Benefits 
- Simplify complex data into intuitive, easy to understand graphical representation 
- Uncover trends and patterns, correlation
- Make data accessible to a more broader audience and increase stakeholders engagement 
- Communicate insights effectively by making them more memorable and persuasive (for example: highlight key performance metrics in a visually engaging way)
- Enable real-time analysis: reports are update in real-time 
### Visualization flow in Power BI
1. Load data from the data source 
2. Transform and pre-process data 
3. Design Visualization  
4. Publish reports 
# Column charts 
Compare different categories in vertical orientation *(fewer than 10 categories on the X axis)* to demonstrate data changes over time or illustrate comparison among items. 
For examples: compare sales of different product categories over the past years.
# Bar charts 
Provide horizontal representation of data, the length of each bar represents the quantity of the data.
Useful to compare larger quantities or categories with lengthy labels. 
Also useful for displaying comparisons among discrete categories or non continuous, distinctly separate groups of data.
# Line charts 
Best suited for showing trends over time.
Useful with large datasets (many data points) and when trends, patterns or fluctuations of data changes over time are of interest.
## Area charts 
Line charts with colored area beneath the lines to emphasize the magnitude of changes.  
These charts help compare two or more quantities and show part to whole relationships over time or across categories, representing how individuals segments contribute to an entire dataset. 
## Stacked area charts 
- **Purpose:** Show the composition of a total quantity over time.
- **Best for:** Comparing multiple categories within a total.
- **Example:** A stacked area chart showing the sales of different product categories over a year.
# Pie chart 
Showcase dataset as portions of a whole.
Pie charts are less effective when there're too many categories to compare resulting in a large number of small slices. In this case, pie chart might be better for clear visualization.
## Donut chart
- **Pie chart:** Has no center hole.
- **Donut chart:** Has a center hole, creating a ring-like appearance.
**Pie charts** are generally preferred when:
- **Data categories are relatively few.** Too many categories can make the chart difficult to read.
- **The proportions of the categories are visually distinct.** If the proportions are too similar, it can be hard to discern differences.
- **You want to emphasize the whole as a single unit.** The lack of a center hole reinforces the idea of a unified whole.
**Donut charts** are often better suited for:
- **Comparing multiple data sets within a single category.** The center hole can be used to display additional information, such as a total value or average.
- **Highlighting a specific category.** The center hole can be used to emphasize a particular category by placing its label or a visual element there.
- **Creating a more visually appealing chart.** The donut chart's ring-like appearance can add a touch of visual interest.
# Tables 
Tables display data in columns and rows providing a comprehensive numerical view of your data. 
Useful to display additional critical details 
# Combo Charts 
**Purpose:**
- **Comparing multiple metrics:** When you want to compare different metrics over the same time period or category.
- **Analyzing trends and patterns:** Identifying trends, correlations, and outliers between different data sets.
- **Understanding relationships:** Exploring the relationships between variables and their impact on overall outcomes.
- **Improving decision-making:** Providing a visual representation of complex data to support informed decision-making.
**Types of Combo Charts:**
- **Line and stacked column chart:** Visualize a total across a series of data and how individual parts contribute to the total.
- **Line and clustered column chart:** Compare multiple sets of data side by side.
### Examples of application 
- **Sales analysis:** Comparing sales trends with order quantity with line & stacked columns chart or customer satisfaction - Line chart for sales trends, column chart for customer satisfaction ratings.
- **Financial analysis:** Analyzing revenue, expenses, and profit margins over time. Line charts for revenue and expenses, stacked column chart for profit margin breakdown.
- **Compare financial ratios**: Line charts for different financial ratios
- **Marketing analysis:** Comparing the performance of different marketing channels or campaigns by using stacked column and line chart.
- **Operational analysis:** Tracking production metrics, inventory levels, and quality control data with multiple lines chart 
- **Customer analysis:** Analyzing customer behavior, satisfaction, and loyalty.
# Select report visuals 
[Select report visuals](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/5-report-visuals)
[[Visual Clarity]]
## Categorical visuals 
Often, bar or column charts are good choices when you need to show data across multiple categories.
- Avoid selecting a visual where color is used to split the data, such as a stacked bar chart with a category legend. Instead, use the category dimension on the axis of a bar chart.
- Avoid a line chart with categorical X-axis because the line implies a relationship between elements 
Sort categorical charts by value rather than in alphabetical category order to provide an intuitive visual that is organized to produce a natural flow.
## Time series visuals 
Always use a line or column chart to show values over time. 
The X-axis should present time, sorted from earliest to latest periods (left to right).
Line charts work well with a consistent flow of data, such as when sales are recorded for every period.
- If no sales are recorded for some periods, the line chart visual will fill such gaps with a straight line
- If missing values are a possibility, a column chart might be a better visual choice because it will help to avoid the interpretation of a non-existent trend.
Other visuals that you can use for time series data include:
- Stacked column chart
- Area chart
- Line and stacked column chart
- Ribbon chart, which has the added benefit of showing rank changes over time
## Proportional visuals 
Column and bar chart visuals work well for visualizing proportions across multiple dimensions.
100% Stacked Bar chart visual shows proportional sales across four stores and allows you to compare across the six product categories. 
Other visuals:
- 100% Stacked Column chart
- Funnel chart
- Treemap
- Pie chart
- Doughnut chart
## Numeric visuals 
Often presented by card visuals, numeric values show high-level callouts that demand immediate attention.
Can also use a multi-row card to display multiple values in a single visual.\
## Grid visuals 
 Tables and matrices:
 - Tables have a fixed number of columns, and each column can express grouped or summarized data
 - Matrices can have groups on columns and rows
 - Additional formatting options: background colors, font colors, or icons
  Matrices provide one of the best experiences for hierarchical navigation
## Performance visuals 
Describing a value and its comparison to a target.
- Gauge
- KPI
- Table, with conditional formatting
- Matrix, with conditional formatting
## Geospatial visuals 
A map visual can occupy considerable space on the report page. Also, geospatial data doesn't always need to be shown in maps. If location isn't highly relevant to the requirements, consider using a categorical visual instead.
## Select report visuals to suit the report layout 
To narrow down the selection, choose the visual that best fits the available space on the report page.
- **Visual Choice:** Multiple visual types can often be used to meet design requirements. 
	- **Data Distribution:** Consider the distribution of your data. Some visuals are better suited for skewed or normal distributions.
- **Space Optimization:** Choose visuals that effectively utilize the available space on the report page.
- **Aesthetic Appeal:** Ensure the chosen visual is visually pleasing and enhances the overall report design.
	- **Screen Readers:** Consider how screen readers will interpret your visuals. Use descriptive labels and avoid relying solely on color for differentiation.
## KPI visualization 
- **Cards:** Display a single value or data point. Ideal for tracking essential statistics on dashboards.
- **Multi-row Cards:** Display multiple data points, one per row. Useful for comparing related metrics.
- **Radial Gauges:** Circular arcs that measure progress towards a goal or target. Visually appealing but space-consuming.
- **KPI Visual:** Combines a primary measure, trend line, and target goal. Offers a comprehensive view of performance.
# Ribbon charts & Waterfall charts 
## **Ribbon charts** 
[Ribbon charts](https://learn.microsoft.com/en-us/power-bi/visuals/desktop-ribbon-charts)
Ideal for sale performance analysis multi-dimensional data such as data changes across categories, it tracks rankings and their shift over time. 
- Represent time-based data 
- Track ranking changes 
- Compare performance of multi-dimensional data 
- Easy to interpret 
**Limits:** 
- Can become cluttered: Ribbon charts can become difficult to read if there are too many dimensions or categories.
- May Not Be Suitable for All Data Types: Ribbon charts are best suited for data that can be represented as stacked areas.
### Key characteristics
- **Multiple Dimensions:** Ribbon charts can simultaneously display data for multiple dimensions, such as time, categories, or groups.
- **Stacked Areas:** The data is represented as stacked areas, where each area represents a different dimension or category.
- **Overlapping Areas:** Overlapping areas can be used to visualize the interaction between different dimensions.
- **Color Coding:** Different colors can be used to represent different dimensions or categories, making the chart easier to interpret.
### Common use 
- **Sales Analysis:** Tracking sales performance over time for different product categories or regions.
- **Financial Analysis:** Analyzing revenue and expenses over time for different departments or business units.
- **Project Management:** Tracking the progress of multiple projects over time.
- **Engineering Analysis:** Visualizing the performance of different components or systems over time.
## **Waterfall charts** 
https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-waterfall-charts
Break down cumulative effects negatively or positively to an outcome. 
Waterfall charts are visual representative of cumulative effect analysis. 
### Cumulative effects: 
refer to how an initial value is effected by a series of sequential factors such as events or changes over times. 
**Application:** 
- Financial analysis with waterfall charts: analyze how net income results from a cumulative effect of revenue, costs, expense, taxes. 
- **Cash Flow Analysis:** Analyzing the inflows and outflows of cash to determine the overall financial health of a business. 
- **Return on Investment (ROI) Calculation:** Understanding the impact of various factors on the overall ROI of a project.
- **Budget Variance Analysis:** Identifying the reasons for budget overruns or underspends.
- **Schedule Variance Analysis:** Understanding the factors that contributed to project delays or early completion.
- **Resource Allocation Analysis:** Evaluating the impact of resource changes on project outcomes.
- **Sales Pipeline Analysis:** Tracking the progress of sales opportunities from lead generation to closure.
- **Marketing Campaign Effectiveness:** Assessing the impact of different marketing channels on revenue generation.
- **Customer Churn Analysis:** Understanding the reasons for customer attrition and identifying areas for improvement.
- **Process Improvement:** Identifying bottlenecks and inefficiencies in a process.
- **Cost Reduction Analysis:** Evaluating the impact of cost-saving initiatives.
- **Productivity Analysis:** Understanding the factors that contribute to or detract from productivity.
# Funnel chart 
[Funnel charts](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-funnel-charts?tabs=powerbi-desktop)
The funnel visualization displays a linear process that has sequential connected stages, where items flow sequentially from one stage to the next.
They're suitable to visualize data that's sequential and moves through ***at least four stages***.
 Funnel charts reveal bottlenecks, help calculate potential outcome by stages 
## Advantages 
- **Visual Representation of a Process:** Funnel charts provide a clear and concise visual representation of a process.
- **Easy to Understand:** The decreasing width of the funnel makes it easy to see the progression of items or people through the stages.
- **Identification of Bottlenecks:** Funnel charts can help identify stages where a large number of items or people drop out of the process.
- **Comparison of Different Stages:** Funnel charts allow for easy comparison of the performance of different stages.
### Limitations 
- **Limited Data Complexity:** Funnel charts are best suited for simple processes with a clear beginning and end.
- **May Not Be Suitable for All Data Types:** Funnel charts are not appropriate for data that does not follow a sequential process.
## Commonly use cases 
- **Sales Funnels:** Tracking the progress of sales leads from initial contact to purchase.
- **Marketing Funnels:** Analyzing the effectiveness of marketing campaigns in generating leads and conversions.
- **Customer Journey:** Visualizing the steps customers take to become loyal customers.
- **Process Optimization:** Identifying bottlenecks or areas for improvement in a process.
# Scatter charts 
[Scatter charts](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-scatter?)
Identify trends, patterns, anomalies (such as outliers), the correlation between the variables. 
Keep a keen eye on outliers to prevent them from skewing the data and effect the statistical characteristics of the data distributions. 
Outliers could provide insights about:
- data gathering mechanism 
- potential issues 
- areas for improvement 
## Interpreting Scatter Charts:
- **Clustering:** Data points that are clustered together indicate a strong correlation between the variables.
- **Outliers:** Data points that are far from the cluster may indicate unusual or exceptional behavior.
- **Trends:** Look for patterns or trends in the data, such as a positive or negative correlation
- **Comparison:** Compare data points from different groups or categories
### Interpreting Anomalies
Once you've identified an anomaly, consider the following questions:
- **Is the anomaly valid?** Could it be due to measurement errors, data entry mistakes, or unusual events?
- **What might have caused the anomaly?** Investigate underlying factors or factors that might have influenced the data point.
- **What are the implications of the anomaly?** Assess the potential impact of the anomaly on your analysis or decision-making.
## Power BI options 
**Formatting:**
- **Marker Size:** Adjust the size of data points to represent a third variable.
- **Marker Shape:** Choose different shapes for data points to distinguish categories.
- **Colors:** Customize the colors used for data points and categories.
- **Labels:** Add labels to data points or axes for clarity.
**Animation:** Add animation to the chart to make it more engaging and interactive.
**Filters:** Apply filters to the chart to focus on specific subsets of data.
# Matrix visualizations 
The matrix visual is similar to a table but has key features that allow the report designer to communicate multiple levels of information in the data:
- data display across multiple dimensions 
- Stepped layout
- Automatically aggregate data
- Drill-down capabilities 
Key features includes:
- Cross-highlighting: Interact with other visuals on the report by selecting rows, columns, or individual cells.
- Copy and paste: Copy individual or multiple cell selections into other applications.
## How Power BI calculates totals 
Power BI calculates subtotals and totals by evaluating the measure over all rows in the underlying data. 
This is a common pattern when the value you’re summing is on the ‘one’ side of a one-to-many relationship.
## Format matrix visuals 
### Drill down 
- Drill down on row headers \
- Drill down on column headers 
### Stepped layout 
Adjust the **Stepped layout** settings. Select the matrix visual and then, in the **Format** section (the paintbrush icon) of the **Visualizations** pane, expand the row headers section:
- Stepped layout toggle 
- Stepped layout indentation 
### Subs and Grand totals 
In **Row grand total** section and **Row subtotals**
# Conditional formatting 
**Conditional formatting** in Power BI allows you to dynamically apply formatting like colors, data bars, or icons to values in **tables and matrices**. This makes it easier to highlight trends, outliers, and key insights at a glance.

To apply conditional formatting, right-click a field in the **Visualizations** pane's field well, select **Conditional formatting**, and choose the type you want to apply.
### Types of Conditional Formatting

|**Formatting Type**|**Purpose**|**How it's Configured**|
|---|---|---|
|**Background Color / Font Color** 🎨|To change the color of the cell's background or the text itself to highlight data.|Based on one of three styles: **Gradient**, **Rules**, or **Field Value**.|
|**Data Bars** 📊|To add a horizontal bar within a cell, where the length of the bar represents the cell's value relative to others.|Can be configured to show the bar only or both the bar and the number. Minimum and maximum values can be set.|
|**Icons** ✨|To add a visual indicator (like an arrow, shape, or flag) to a cell based on its value.|Typically based on **Rules** that you define (e.g., a green up-arrow for values > 0, a red down-arrow for values < 0).|
|**Web URL** 🔗|To turn a text field into a live, clickable hyperlink.|Based on a **Field Value** that contains a full web URL (e.g., `https://www.microsoft.com`).|
### Methods for Applying Color Formatting

When you choose to format by **Background Color** or **Font Color**, you have three main styles to choose from.
#### 1. Gradient (Color Scale)
- **What it does:** Applies a smooth color gradient between a minimum, center (optional), and maximum value.
- **Use Case:** To show the distribution and magnitude of data, like a heat map. For example, coloring low sales values light red and high sales values dark red.
#### 2. Rules
- **What it does:** Applies a specific color to a value if it falls within a predefined range or condition.
- **Use Case:** To highlight values that meet specific business targets. For example:
    - _If value is > 90 (Number), then Green_
    - _If value is between 80 and 90 (Number), then Yellow_
    - _If value is < 80 (Number), then Red_
- **Note for Percentages:** When creating rules for a percentage field, use decimal numbers in the rule (e.g., `0.25` for 25%) and select **Number** as the format, not "Percent."
#### 3. Field Value
- **What it does:** Applies a color based on the value of another field or measure that contains a color name or hex code (e.g., "Green", "#3E4AFF").
- **Use Case:** When you have a DAX measure or a column in your data that already defines the color logic. For example, you can create a measure that returns "red" if a status is "Declined" and "blue" if it's "Accepted," and then use this measure to color your status column.
### Key Considerations
- **Overrides:** Conditional formatting will always **override** any manual background or font color you set on a cell.
- **NaN Values:** Gradient and percentage-based rule formatting may not work correctly if your data contains `NaN` ("Not a Number") values, which are often caused by a divide-by-zero error. Use the `DIVIDE()` DAX function to avoid these errors.
- **Aggregations:** Conditional formatting needs an aggregation or measure to be applied to the value.
- **Printing:** When printing a report, you must enable **"Background graphics"** in your browser's print settings for data bars and background colors to print correctly.