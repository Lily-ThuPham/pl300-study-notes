**APPLIES TO:** ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service

### Comparison of Chart Types

| **Chart Type**     | **What It Shows / Use case**                                                                                                                                                                                                                                                                                                                                               | **Required Fields**                                                                        | **Key Use Case**                                                                                                                                                             |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Scatter Chart**  | The relationship between **two numerical values**.<br>- Display worksheet data with pairs or grouped sets of values.<br>- Show patterns in large sets of data.<br>- Compare large amounts of data points irrespective of time measurements.<br>- Convert horizontal axis into logarithmic scale.<br>- Substitute for line charts to enable changing horizontal axis scale. | An X-Axis value (numeric) and a Y-Axis value (numeric).<br>A categorical column as legend. | To identify correlations, trends, clusters, and outliers between two variables (e.g., plotting `Sales per Sq Ft` vs. `Total Sales Variance %`).                              |
| **Bubble Chart**   | The relationship between **three numerical values**<br>- Visually emphasize value differences with variable bubble size.<br>- Support scenarios with three data series that each has sets of values.<br>- Present financial data in a visual rather than numerical form.<br>- Display data with quadrants.                                                                 | An X-Axis value, a Y-Axis value, and a **Size** value.                                     | To expand on a scatter chart by using the bubble's size to represent a third measure, visually emphasizing its magnitude (e.g., bubble size represents `This Year's Sales`). |
| **Dot Plot Chart** | The distribution of a **numerical value** across different **categories**.<br>Use cases for the dot plot chart are similar to the scenarios described for scatter and bubble charts. The primary advantage of dot plot charts is the ability to include categorical data along the horizontal axis.                                                                        | A **categorical** field on the X-Axis and a numerical value on the Y-Axis.                 | To see the spread and clustering of individual data points within different categories (e.g., plotting `Sales Variance %` for each individual `District Manager`).           |
### How to Create the Visuals
The creation process often starts with a Scatter chart, which can then be easily converted into a Bubble or Dot Plot chart.

1. **Create a Scatter Chart:**
    - Select two numerical measures and one categorical field (for detail).
    - In the Visualizations pane, select the **Scatter chart** icon.
    - Drag one numerical measure to the **X Axis** and the other to the **Y Axis**.
    - **To ensure each row of your data is plotted as a separate point, you must add a unique identifier field (like a primary key or an index column) to the `Values` field well.** This prevents Power BI from aggregating your data into a single point.
    - Drag the categorical field (e.g., `District`) to the **Legend** to color-code the data points.
2. **Convert to a Bubble Chart:**
    - With the Scatter chart selected, drag a third numerical measure into the **Size** field well. The data points will transform into bubbles, with their size representing the value of this third measure.
3. **Convert to a Dot Plot Chart:**
    - With the Scatter chart selected, remove the numerical field from the **X Axis**.
    - Drag a **categorical field** (e.g., `District Manager`) into the **X Axis** well. The chart will now display the numerical Y-axis values as individual dots plotted for each category on the X-axis.
### Key Formatting and Analytics Features
- **Number of Data Points:** You can adjust the maximum number of data points displayed (up to 10,000) in the **Format > General > Properties > Advanced options**.
- **Markers:** You can change the shape of the data points (e.g., circle, square, triangle) in the **Format > Visual > Markers** section to improve accessibility.
#### Analytics Pane Features
Beyond basic plotting, these visuals offer a rich set of analytical tools, found primarily in the **Analytics pane** (the magnifier glass icon 🔎).
The Analytics pane allows you to add dynamic reference lines and shading to your chart to reveal more insights.

|**Feature**|**What It Does**|**Common Use Case**|
|---|---|---|
|**Median line**|Adds a line representing the median (middle) value for either the X or Y axis.|To quickly see how data points are distributed above or below the median.|
|**Average line**|Adds a line representing the average value for either the X or Y axis.|To identify points that are above or below the overall average.|
|**Constant line**|Allows you to add a static line at any specific value you define on an axis.|To show a target or threshold (e.g., adding a line at the `Sales Target` of $1M).|
|**Min/Max lines**|Adds lines to show the minimum and maximum values in your dataset for a given axis.|To quickly identify the range of your data.|
|**Percentile line**|Adds a line at a specific percentile (e.g., the 90th percentile) of your data.|To identify top performers or outliers that fall above a certain percentile.|
|**Symmetry shading**|Shades the background of the chart to show which data points have a higher value for the X-axis measure compared to the Y-axis measure, and vice-versa.|To quickly identify which axis measure a data point favors, especially when the axes have different ranges.|
|**Ratio line**|Displays a line showing the ratio between the X and Y-axis measures.|To analyze the relationship between two metrics, such as a cost-to-profit ratio.|
#### AI-Powered Anomaly Detection (Scatter Chart)
Power BI includes an AI-powered feature that can automatically analyze your data to explain what makes a certain group of data points different from the rest.
- **What it is:** This feature, often called **"Find where the distribution is different,"** is a form of anomaly detection. It runs a machine learning algorithm to identify the key drivers that distinguish a selected set of points.
- **How to Access:**
    1. On a scatter chart, right-click a specific data point or a cluster of points you want to analyze.
    2. From the context menu, select **Analyze > Find where the distribution is different**.
- **The Insight:** Power BI will generate a new visual in a pop-up window. This visual will show you the factors that most strongly correlate with the group of data points you selected.
- **Real-Life Example:** You have a scatter chart plotting `Customer Satisfaction` vs. `Average Purchase Value`. You notice a cluster of highly satisfied, high-spending customers. You use the "Find where the distribution is different" feature on this cluster. The AI might generate a chart showing that these customers are overwhelmingly from the "West" region and have a "Premium" subscription type, giving you an immediate, actionable insight into who your best customers are.
### Troubleshooting Common Issues
- **Chart shows only one data point:** This happens when Power BI aggregates all your data into a single point because it lacks a field to distinguish the individual rows.
    - **Solution:** Drag a unique identifier column (like a primary key or an index column) into the **Values** field well. This forces the visual to plot a separate point for each unique row.
- **Chart performance is slow:** If your chart has a very high number of data points (approaching the 10,000 limit), it may load slowly.
    - **Solution:** Consider filtering the data to reduce the number of points or confirm that the performance is acceptable for your users after publishing.
### High-Density Sampling: Visualizing Large Datasets
When the number of underlying data points exceeds a visual's display limit (typically ~3,500 for most visuals and 60 series for any visuals), Power BI uses a **high-density sampling algorithm** to create a representative and responsive visualization without plotting every single point. This is the default behavior and can be toggled in the **Format > General** pane.

The maximum number of data limits is higher for the following visual types, which are _exceptions_ to the 3,500 data point limit:
- **150,000** data points maximum for R visuals.
- **30,000** data points for Azure Map visuals.
- **10,000** data points for some scatter chart configurations (scatter charts default to 3500).
- **3,500** for all other visuals using high-density sampling. Some other visuals may visualize more data, but they won't use sampling.
#### How the Algorithm Works
_**High-density Sampling option**_: in **Format Pane -> Properties -> Advanced options** of the visual
The algorithm for high-density line sampling is available for line chart and area chart visuals with a continuous x-axis.
For a high-density visual, **Power BI** intelligently slices your data into high-resolution chunks and then picks important points to represent each chunk. That process of slicing high-resolution data is tuned to ensure that the resulting chart is visually indistinguishable from rendering all of the underlying data points but is faster and more interactive.
The algorithm differs for line/area charts and scatter charts.
- **For Line and Area Charts:**
    1. The algorithm chunks the data into groups called **bins**.
    2. Within each bin, it finds the **minimum and maximum** data values.
    3. These two points (the min and max) become the representatives for that bin. This process ensures that important peaks and troughs (outliers) are captured and displayed in the visual.
- **For Scatter Charts:**
    1. The algorithm eliminates overlapping points to ensure all points in the dataset are represented and can be interacted with.
    2. It works to preserve the overall **shape** of the data, ensuring outliers are still visible.
#### Tooltip Behavior
Because the algorithm only plots representative points (like the min/max in a bin), tooltips may not show a value for every single point along the x-axis. A tooltip will only appear if your cursor is directly over one of the selected representative data points.