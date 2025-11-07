## **Key Influences Visual**
The **Key Influencers visual** in Power BI is an AI-powered tool that analyzes your data to identify and rank the primary factors driving a specific metric or outcome. It helps you understand _why_ things happen in your data, such as what contributes to low customer ratings or what influences house prices to increase.

---
### 🧠 When to Use It
Use the Key Influencers visual when you want to:
- **Identify Drivers:** See the main factors that affect a metric you're analyzing.
- **Rank Importance:** Compare the relative impact of these factors. For example, does a customer's subscription type affect their rating more than their company size?
### 📊 Key Features of the Visual
The visual is split into two main tabs, with several key components for interpretation:
- **Key Influencers Tab:** Shows the top **individual factors** that contribute to your selected outcome.
    - **Left Pane:** A ranked list of the top influencers. For example, "Role in Org is consumer."
    - **Right Pane:** A detailed chart (e.g., column chart) comparing the selected influencer to other values.
    - **Average Line (Dotted Line):** Represents the average of all _other_ values. This line is dynamic and changes depending on the influencer you select.
    - **Interpretation:** An influencer's impact is often stated as a multiplier (e.g., "Consumers are **2.57 times** more likely to give a low score"). This is calculated by dividing the influencer's rate (green bar) by the average rate of others (dotted line).
- **Top Segments Tab:** Shows how **combinations of factors** affect the metric.
    - **Bubbles:** Each bubble represents a segment (a group of users with specific characteristics).
    - **Bubble Height:** Represents the impact or proportion of the outcome within that segment.
    - **Bubble Size:** Represents the number of data points (population) in that segment. This helps identify addressable groups.
### ⚙️ How to Analyze Different Data Types
The visual adapts its analysis based on the type of metric in the **Analyze** field.
#### **Categorical Analysis**
This is used for metrics with distinct categories (e.g., Rating is "Low" or "High").
- **The Question:** "What influences _Rating_ to be _Low_?"
- **Continuous Factors:** If you use a continuous field like _Tenure_ (customer lifetime) to explain a categorical outcome, the visual will identify trends. For example, "When _Tenure_ **increases** by 13.4 months, the likelihood of a low rating **increases** by 1.23 times."
- **Automatic Binning:** If a continuous factor's relationship with the metric isn't linear, Power BI automatically groups it into bins (e.g., Tenure of 0-12 months, 13-24 months, etc.).
#### **Continuous/Numeric Analysis**
This is used for numerical metrics where you want to see a trend (e.g., _House Price_).
- **The Question:** "What influences _House Price_ to **increase/decrease**?"
- **Interpretation:** The results show the average impact, not a likelihood multiplier. For example, "Houses with an _Excellent_ kitchen quality are, on average, **$158K more expensive** than those without."
#### **Measures & Summarized Columns**
When analyzing a measure (like _Average House Price_), the analysis level is critical.
- **The Problem:** The analysis runs at the level of the fields in **Explain by**. This can be too summarized.
- **The Solution:** Use the **Expand by** field to add a unique identifier (like _House ID_) to set the analysis to a more granular level without treating the ID as an influencer itself.
### 💡 Practical Tips
- **Add Counts:** In the Format pane, enable **Counts** on the Analysis card. This adds a ring around each influencer bubble, showing what proportion of your data it represents. A factor with high impact but a tiny count may be less important to act on.
- **Interactivity:** The visual is dynamic. Clicking on slicers or other visuals on the report canvas will rerun the analysis on the filtered subset of data, allowing you to discover different influencers for different groups (e.g., enterprise vs. small business customers).
### ⚠️ Common Issues & Troubleshooting
- **No Influencers Found:** This often happens if:
    - The explanatory fields have too many categories with too few observations.    
    - You included the metric you're analyzing in both the **Analyze** and **Explain by** fields.
- **Relationship Error:** "A field in `Explain by` isn't uniquely related to the table..."
    - **Cause:** The analysis runs at the level of the `Analyze` metric (e.g., the customer level). If an explanatory field is at a more granular level (e.g., a customer can have multiple devices), an error occurs.
    - **Fix:** Aggregate the explanatory field to the correct level. For instance, instead of using the _Device_ column, use a _Count of Devices_ per customer.
- **Low Data Warning:** The visual needs sufficient data to find statistically significant patterns. A general rule of thumb is at least **100 observations** for the state you're analyzing (e.g., 100 customers with "Low" ratings).
- **Limitations:**
    - **Direct Query** and **Live Connection** to Analysis Services are **not supported**.
    - **Publish to web** is **not supported**.

## **Decomposition Tree Visual**
The **decomposition tree** is an artificial intelligence (AI) visualization in Power BI that is excellent for ad hoc exploration and **root-cause analysis**. It automatically aggregates data and allows you to drill down into multiple dimensions in any order you choose.

---
### How to Configure the Visual
The visual requires two types of input in the Visualizations pane:
- **Analyze:** The metric you want to investigate. This must be a **measure or an aggregate**.
- **Explain By:** One or more **dimensions** that you want to use to break down the metric.
Once configured, the visual starts with a single "root node" showing the total value of your `Analyze` metric. You can then click the **plus sign (+)** next to any node to expand it and drill down into one of the dimensions from your `Explain by` field well.
### AI Splits (The Light Bulb Icon 💡)
This is the key AI feature of the decomposition tree. When you choose to drill down, Power BI can automatically suggest the next best dimension to explore to find the highest or lowest values. These AI-driven suggestions appear at the top of the list, marked with a **light bulb icon**.
There are two types of AI analysis you can choose from in the visual's formatting options:
#### Absolute (High/Low Value)
- This is the default analysis type. It scans all available fields and finds the one that contains the absolute highest or lowest value of the measure you are analyzing.
#### Relative
- This is a more advanced analysis. It looks for high or low values that **stand out the most** when compared to the average of the other data in that same column. This is useful for finding interesting outliers that might not be the absolute highest value but are unexpectedly high or low relative to their peers.
##### The Algorithm Behind "Relative" Splits
The "Relative" mode finds values that have the largest difference from the expected average. The calculation is essentially:
`(Actual Value of the Item) / (Average Value for all items in that field)`
**Example:**
- If you are analyzing sales by `Game Genre`, and the `Platform` genre has sales of $19.55M.
- The average sales across all 10 game genres is $4.6M.
- The calculation would be: `19,550,000 / 4,600,000 = 4.25x`
- This means the `Platform` genre's sales are **4.25 times higher** than the expected average, making it a significant "Relative" influencer, even if another genre had a higher absolute sales value.
**Interaction:** The AI splits are dynamic. They will recalculate if you select a different node in the tree or if you cross-filter the decomposition tree by interacting with another visual on the report page.
### Other Key Features
- **Interaction:** Selecting a node from the last level of the tree will **cross-filter** other visuals. Selecting a node from an earlier level will **change the drill-down path**.
- **Locking:** A report creator can **lock** one or more of the top levels of the tree. This prevents report consumers from removing or changing those specific levels, allowing for a guided analysis experience while still permitting free exploration in the lower, unlocked levels.
### Considerations and Limitations
- **Limits:**
    - Maximum number of levels: **50**.
    - Maximum data points that can be visualized at one time: **5,000**.
- **Unsupported Scenarios:** The decomposition tree is **not supported** in the following environments:
    - On-premises Analysis Services.
    - Power BI Report Server.
    - Publish to Web.
- **AI Split Limitations:** AI splits are not supported for Azure Analysis Services or for complex measures.
- **No Q&A Support:** The decomposition tree is not supported inside the Q&A visual.
## **Applying Insights in Power BI (Analyze Feature)**
Power BI's **Insights** feature (found under the "Analyze" right-click menu) uses machine learning algorithms to provide fast, automated, and insightful analysis about your data. It helps you quickly understand the "why" behind your data without manual exploration.
To use the **Analyze** feature, right-click a data point on the visual and then hover over the **Analyze** option to display two further options: **Explain the increase/decrease** and **Find where the distribution is different**.

---
### 1. Explain the Increase / Decrease
This insight is used to understand the cause of **fluctuations** between two consecutive data points in a time series or categorical chart.
- **Purpose:** To answer the question, "Why did this value go up or down compared to the previous point?"
- **How to Access:** In a bar or line chart, **right-click a data point** (it cannot be the first one) and select **Analyze > Explain the increase** (or decrease).
- **What You Get:** A pop-up window with an AI-generated visual and a description.
    - The default visual is a **waterfall chart** that shows which categories most influenced the change.
    - You can switch to other visual types like a scatter plot or ribbon chart to see different perspectives.
    - You can add the generated visual directly to your report by clicking the `+` button.
- **How the Algorithm Works:** The algorithm doesn't just find the biggest absolute changes. Instead, it looks for the categories where the **relative contribution** to the total changed the most between the two periods. For example, if a product category grew from 1% of total sales to 6%, it's considered more interesting than a category that grew from 50% to 55%.
### 2. Find Where This Distribution is Different
[Use insights to find where distribution is different - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-insights-find-where-different)
This insight is used to understand what makes a specific category or segment in your data **different from the overall population**.
- **Purpose:** To answer the question, "For this specific category, what other factors make its data distribution unusual?"
- **How to Access:** **Right-click on a data point** (e.g., a single bar in a bar chart) or the visual as a whole, then select **Analyze > Find where this distribution is different**.
- **What You Get:** A pop-up window with a column chart that compares the data distribution for your selected category against the overall distribution for all categories.
- **How the Algorithm Works:** The algorithm essentially tests all other columns in your model as potential filters. It then highlights the filter values that produce a distribution that is the **most statistically different** from the original, unfiltered view.
- **Example:** If your overall sales are split 75% USA and 25% Canada, but for the "Touring Bikes" category the split is 50/50, the insight will highlight "Touring Bikes" as a category where the distribution is significantly different.
### 3. General Considerations and Limitations
It is critical to know that the Insights feature has several limitations.
- **Unsupported Data Sources:** It does **not** work with **DirectQuery** or **Live Connection** models.
- **Unsupported Filters:** It does not work when certain filter types are applied, including:
    - TopN filters
    - Include/Exclude filters
    - Measure filters
- **Unsupported Measures:** It does not work with non-numeric measures or measures that use "Show value as" (e.g., % of Grand Total).
## **Anomaly Detection in Power BI**
**Anomaly detection** is an AI feature that enhances _**line charts only**_ by automatically detecting unexpected data points (anomalies) in your **_time series data_**. It also provides automated explanations to help with root cause analysis.
Anomaly detection in Power BI is a feature that helps you spot unusual patterns in a dataset. These unusual patterns, or anomalies, stand out from most of the data.
- **Early Warning System**: Anomaly detection acts as an early warning system, letting you know about sudden changes in data. This helps businesses react quickly to problems, like noticing a drop in product quality or an increase in customer complaints, before they get worse.
- **Enhanced Business Insights**: Identifying anomalies can also help you find important insights that you might miss. For instance, noticing a sharp rise in sales after a marketing campaign can show you which strategies are working well, helping you make better business decisions.
- **Time-Efficient Analysis**: Manually searching datasets for unusual data is slow and can lead to mistakes. Anomaly detection automates this, quickly finding irregularities in the data, which saves time and effort.
- **Improved Data Quality**: Anomalies can point out errors or inconsistencies in data. Finding these anomalies helps keep the data accurate and high-quality, making sure analyses and reports are based on trustworthy information.

---
### 1. How to Enable and Use Anomaly Detection
1. Select a **line chart** that has time series data in its Axis field.
2. Go to the **Analytics pane** (the magnifier glass icon 🔎) in the Visualizations pane.
3. Expand the **Find anomalies** section and click **Add**.

**What You Get:**
- Power BI automatically adds anomaly markers to your chart for any data points that fall outside an expected range.
- It also displays a shaded band representing the **expected range** of values.
### 2. Formatting and Customization
The feature is highly customizable. You can format the:
- **Anomaly markers:** Change their shape, size, and color.
- **Expected range:** Adjust its color, style, and transparency.
- **Algorithm Sensitivity:** In the "Find anomalies" card, you can increase or decrease the **Sensitivity**. A higher sensitivity will flag more data points as anomalies, while a lower sensitivity will be more selective.
### 3. Explanations 
Besides just identifying anomalies, Power BI can help explain _why_ they occurred.
- **How it works:** When you **click on an anomaly marker**, a new **Anomalies pane** appears. Power BI runs an analysis across other fields in your data model to find possible explanations, sorted by their explanatory **strength**.
- **Configuring Explanations:** You can control which fields are used in this analysis by dragging specific dimensions into the **Explain by** field well. This restricts the analysis to only those fields.
- **Strength:** Power BI calculates the "strength" of an explanation as a ratio that compares how much a specific category (e.g., a single seller) deviated from its expected value versus how much the total value deviated. A high strength percentage indicates a strong correlation.
### 4. Key Considerations and Limitations ⚠️
It is critical to know that Anomaly Detection has several limitations.
- **Visual Type:** It is **only supported for line chart visuals**.
- **Axis Requirement:** The line chart's Axis field **must contain time series data**.
- **Unsupported Features:** It is **not compatible** with:
    - Legends, multiple values, or secondary values in the line chart.
    - Forecast, Min, Max, Average, Median, and Percentile lines.
    - Drilling down in a hierarchy.
- **Data Source Limitations:** It is **not supported** for:
    - DirectQuery over an SAP data source.
    - Power BI Report Server.
    - Live Connection to Azure Analysis Services or SQL Server Analysis Services.
- **Data Points:** The analysis requires a minimum of **four data points**.
## **Smart Narrative**
[Create smart narrative summaries - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-smart-narrative)
The **Smart Narrative** visualization is an AI feature that automatically generates a **text summary** of the key insights and trends found in your report visuals. It helps users quickly understand the main takeaways from a page or a specific visual.
**APPLIES TO:** ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service

---
### How to Create a Smart Narrative
There are two main ways to generate a smart narrative:
1. **For an Entire Page:**
    - Click on an empty area of the report canvas.
    - Select the **Smart narrative** icon in the **Visualizations** pane.
    - Power BI will automatically generate a text box containing a summary based on _all_ the visuals currently visible on that page.
2. **For a Single Visual:**
    - **Right-click** on the specific visual you want to summarize.
    - Select **Summarize**.
    - Power BI generates a text summary based only on that visual. You can optionally pin this summary to the report page.
### Customizing the Narrative
The generated summary is highly customizable within the text box.
- **Standard Formatting:** You can edit the text, apply bolding, change colors, etc.
- **Dynamic Values:** This is the key feature for customization. You can add values directly into the text that update dynamically.
    1. Click the **+ Value** button within the text box or type `+` followed by a name.
    2. You can either map the text to existing fields/measures or use natural language to define a **new measure on the fly** (similar to Q&A).
    3. These dynamic values can be formatted (e.g., as currency, with specific decimal places).
### Visual Interactions and Dynamics
- **Cross-Filtering:** The smart narrative summary is **dynamic**. It automatically updates the text and dynamic values when you cross-filter the report by interacting with other visuals (like clicking on a slicer or a segment in a chart).
- **Generation Limits:** Smart Narratives generates up to **four summaries per visual** and up to **16 per page**, picking the most interesting insights based on visual size and location. Summarizing a single visual might generate more specific insights than summarizing the whole page.
### Smart Narrative Icon (Optional)
You can add a small **Smart narrative icon** to the header of individual visuals.
- **How to Enable:** Select a visual, go to the **Format** pane > **General** > **Header icons** > **Icons**, and turn **Smart narrative** to **On**.
- **User Experience:** When a report reader hovers over the visual, they can click this icon to see an on-demand text summary of that visual. This specific summary cannot be pinned to the report.
### Considerations and Limitations
The Smart Narrative feature has several limitations:
- **Unsupported Scenarios:**
    - Cannot be pinned to a dashboard.
    - Does not support Publish to Web or Power BI Report Server.
    - Does not support Live Connection to Analysis Services (on-premises or Azure).
- **Unsupported Visuals:** Does not work with:
    - Tables, matrices, R visuals, Python visuals, custom visuals.
    - Key influencers (under certain conditions).
    - Map visuals with non-aggregated latitude/longitude.
- **Calculations:** Does not support summaries of visuals containing on-the-fly Q&A calculations or complex measures like "percent of grand total."

## **Automatic Data Insights in Power BI**
[Generate data insights on your semantic model automatically - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/service-insights)
Power BI includes several AI-driven features that automatically analyze your data to find trends, patterns, and anomalies, presenting them as visuals or explanations. These features help you discover insights you might have missed during manual exploration.
**APPLIES TO:** ![](https://learn.microsoft.com/en-us/power-bi/includes/media/no-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service

---
### 1. Comparison of Insight Features

| **Feature Name**                                                               | **What it Analyzes**                                                    | **How to Access**                                                                                                      | **Availability**           | **Outcome**                                                                                                                                                                               |
| ------------------------------------------------------------------------------ | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Analyze** (Explain increase/decrease / Find where distribution is different) | A **single data point** or the change between points within one visual. | **Right-click** a data point in a visual and select **Analyze**.                                                       | Power BI Desktop & Service | A **pop-up window** with an AI-generated visual (e.g., waterfall chart) explaining the specific change or difference. You can add this visual to your report.                             |
| **Quick Insights** (on a Dataset/Semantic Model)                               | The **entire semantic model**.                                          | In the **Power BI service**, select **More options (...)** next to a semantic model and choose **Get quick insights**. | Power BI Service only      | A **new, temporary report page** ("Quick Insights canvas") is generated with up to 32 insight cards showing various trends, correlations, outliers, etc., found across the whole dataset. |
| **Quick Insights** (on a Dashboard Tile)                                       | The data underlying a **single dashboard tile**.                        | In the **Power BI service**, select **More options (...)** on a dashboard tile and choose **View insights**.           | Power BI Service only      | The tile opens in **Focus mode**. Insight cards related specifically to that tile's data appear on the right. You can run further "scoped insights" on these cards.                       |
### 2. Types of Insights Automatically Generated
Power BI uses a set of sophisticated statistical algorithms to discover potentially interesting insights. These can include:
- **Category Outliers (Top/Bottom):** Highlights categories with significantly larger values than others.
- **Change Points in a Time Series:** Identifies significant shifts in trends over time.
- **Correlation:** Detects when multiple measures show similar patterns when plotted against a category.
- **Low Variance:** Finds cases where data points for a dimension are clustered closely around the mean.
- **Majority (Major Factors):** Finds cases where most of a total value comes from a single factor.
- **Outliers (Clustering):** Detects specific categories with values significantly different from others (not time-related).
- **Overall Trends in Time Series:** Detects upward or downward trends.
- **Seasonality in Time Series:** Finds weekly, monthly, or yearly patterns.
- **Steady Share:** Highlights parent-child relationships where the child's share of the parent's total remains consistent over time.
- **Time Series Outliers:** Detects specific dates/times with values significantly different from others.
### 3. Optimizing Your Data for Quick Insights
To improve the quality and likelihood of generating Quick Insights on a semantic model:
- **Hide unnecessary columns:** Quick Insights doesn't search hidden columns. Hide duplicate or irrelevant columns.
- **Use a mix of data types:** Include names, times, dates, and numbers.
- **Avoid duplicate information:** Remove redundant columns (e.g., full state names and state abbreviations).
- **Ensure statistical significance:** Insights may not generate if the data model is too simple, has too little data, or lacks sufficient date or numeric columns.
### 4. Key Limitations
- **Data Sources:** Quick Insights only works with data **imported** into Power BI. It does not support DirectQuery, streaming, or PUSH datasets.
- **Security:** Row-Level Security (RLS) is **not supported** by Quick Insights, even in import mode.
- **Dashboard Tiles:** "View insights" on a tile is not available for all tile types (e.g., custom visuals, streaming data, DirectQuery tiles, or tiles protected by RLS).
- **Analyze Feature:** The "Analyze" feature (Explain increase/decrease/distribution) also has limitations, including not working with DirectQuery/Live Connect or certain filter types.