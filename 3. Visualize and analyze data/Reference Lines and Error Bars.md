**Reference lines** and **error bars** are analytical features in Power BI that you add to visuals to highlight significant data points, trends, benchmarks, or uncertainty. They help viewers quickly interpret data and focus on key points. These features are configured in the **Analytics pane** (magnifier glass icon 🔎) of the Visualizations pane in Power BI Desktop.

---
### 1. Reference Lines
Reference lines serve as benchmarks or guides on a visual to make data easier to interpret against a specific value.
#### Types of Reference Lines:
- **Constant Line (X-Axis / Y-Axis):** Represents a fixed value on either axis. Used for benchmarks, targets, or thresholds (e.g., a line showing the sales target).
- **Average Line:** Marks the average value of the measure in the visual. Useful for comparing individual data points against the overall average.
- **Median Line:** Indicates the median (middle) value. Helpful in skewed distributions.
- **Percentile Line:** Displays a specific percentile (e.g., 90th percentile), giving insight into the data spread.
- **Min Line / Max Line:** Highlights the lowest and highest values in the dataset shown in the visual.
- **Trend Line:** (For visuals with time data) Helps identify patterns or trends in data over time.
- **Symmetry Shading:** (For scatter charts) Shades the background to show which points favor the X-axis measure versus the Y-axis measure.
#### Configuration:
In Power BI Desktop or Power BI Service
1. Select a visuals
2. Go to the **Analytics pane**.
3. Expand the desired line type (e.g., **Average line**).
4. Click **+ Add line**.
5. Configure options like **Color**, **Transparency**, **Line style**, **Position**, and whether to show a **Data label**.
### 2. Error Bars
Error bars visually represent **variability or uncertainty** around a data point in a chart (typically bar or column charts). They extend from the main data point to show a potential range of values.
#### Types of Error Bars:
How the upper and lower bounds are calculated depends on the type selected:
- **By field:** Uses values from another specific field in your dataset to define the upper and lower bounds for each data point.
- **By percentage:** Calculates the error range as a consistent percentage above and below each data point's value (e.g., +/- 5%).
- **By percentile:** Calculates bounds based on a specified percentile range of the data (e.g., showing the range from the 25th to 75th percentile).
- **By standard deviation:** Calculates the error range based on a number of standard deviations from the mean for the data points.
#### Configuration:
In Power BI Desktop or Power BI Service
1. Select a visual (typically a column chart).
2. Go to the **Analytics pane**.
3. Expand the **Error bars** section.
4. Turn the feature **On**.
5. Select the **Type** (Field, Percentage, Percentile, Standard Deviation) and configure the relevant **Upper bound** and **Lower bound** settings.
6. Customize the appearance (color, marker shape, error labels) in the **Bar** and **Error labels** sections.
### 3. Forecasting
The **Forecast** feature, also found in the Analytics pane, uses built-in predictive models to extend time series data into the future.
- **Availability:** Only available for **line chart** visuals with time data.
- **Configuration:** You can specify the **Forecast length**, **Confidence interval**, and seasonality.
### 4. Considerations and Limitations
- **Visual Support:** Not all reference lines and error bars are available for all visual types. The Analytics pane will only show options compatible with the selected visual.
    - **Commonly Supported (Lines):** Line, Area, Bar, Column, Scatter charts.
    - **Limited Support (Constant Line Only):** Stacked charts, Waterfall.
    - **Error Bars:** Primarily used on column charts.
    - **Forecasting:** Line charts only.
- **Data Requirements:** Forecasting requires sufficient historical time series data. Percentile lines require imported data or a connection to a modern Analysis Services model.