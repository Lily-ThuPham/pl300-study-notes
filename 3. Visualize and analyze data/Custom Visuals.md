## Custom Visuals in Power BI
[Import Power BI visuals from AppSource or from a file - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/developer/visuals/import-visual)
**Custom visuals** are third-party visualizations created by Microsoft, partners, or developers that are not included in the default Visualizations pane. They extend the capabilities of Power BI by offering a wide range of unique chart types and visuals (e.g., word clouds, sunburst charts, Gantt charts).

---
### Types and Sources of Custom Visuals
It is crucial to understand the different types of custom visuals, as this determines their capabilities and security level.

|Type / Source|Description|Key Characteristics|
|---|---|---|
|**AppSource Visuals**|The official marketplace for Power BI visuals.|These are the standard, publicly available custom visuals that you can browse and add directly from within Power BI.|
|**Certified Power BI Visuals** ✅|A subset of AppSource visuals that have passed rigorous testing and have been validated by Microsoft.|**Higher Security & Performance:** Meets Microsoft's code standards. **Full Feature Support:** They support more features, like exporting to PowerPoint and displaying in email subscriptions.|
|**Organizational Visuals** 🏢|A private, internal repository for custom visuals that are managed by your Power BI administrator.|Only visuals approved by your organization are available here. This ensures that all report creators in your company use a consistent and governed set of visuals.|
|**Visual Files (`.pbiviz`)** 📁|A standalone visual file downloaded from the internet or received from a colleague.|These are from unverified sources. You must **only import files from sources you trust**, as they could contain security or privacy risks.|
### How to Import Custom Visuals
There are two primary methods for adding custom visuals to your report in Power BI Desktop or the Power BI service.
#### Method 1: From AppSource (Recommended)
This is the safest and easiest way to add new visuals.
1. In the **Visualizations** pane, click the ellipsis (**...**).
2. Select **Get more visuals**.
3. In the Power BI visuals window, browse or search the AppSource marketplace.
4. Select the visual you want and click **Add**.
#### Method 2: From a Local File (`.pbiviz`)
Use this method when you have received a visual file from a trusted source.
1. In the **Visualizations** pane, click the ellipsis (**...**).
2. Select **Import a visual from a file**.
3. A warning message will appear. If you trust the source, click **Import**.
4. Navigate to the `.pbiviz` file on your computer and open it.
### Managing and Using Custom Visuals
- **Using the Visual:** Once imported, the custom visual appears as a **new icon** at the bottom of your Visualizations pane. You can then add it to your report like any other visual.
- **Pinning for Future Use:** ==An imported visual is only available in the current report.== To make it available in all your future reports, **right-click** its icon and select **Pin to visualization pane**.
### Publishing Reports with Custom Visuals
When you publish a report to the Power BI service, the custom visuals are handled in a way that ensures a seamless experience for your report consumers.
- **Visuals are Embedded:** When you publish a `.pbix` file, the definition of any custom visual you've used is **embedded and packaged** within the published report.
- **No Action Needed for Consumers:** Report viewers **do not need to install anything**. The custom visual will render for them automatically in their web browser, just like a standard visual.
- **Updating a Custom Visual:** If a new version of an AppSource visual is released with bug fixes or new features, it is **not automatically updated** in your published reports. To update the visual, the report author must:
    1. Open the `.pbix` file in Power BI Desktop.
    2. Update the visual from AppSource.
    3. **Republish** the report to the Power BI service.
- **Organizational Visuals:** If your report uses an organizational visual, the Power BI service ensures it renders the version managed by your administrator. This guarantees that all reports across the organization use the same, consistent, and governed version of that visual.
### Characteristics
- **Security:** **Certified** visuals are the most secure option. Non-certified visuals from `.pbiviz` files are not validated by Microsoft and could pose a security risk.
- **Performance:** Some custom visuals may perform more slowly than the standard, built-in visuals.
- **Feature Support:** Non-certified visuals may not support all Power BI features, such as exporting to PowerPoint or displaying in email subscriptions.
## R Visuals in Power BI
[Create advanced analytics and visualizations using R scripts - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/visuals/service-r-visuals)
R visuals allow you to use the powerful analytics and visualization capabilities of the R programming language directly within Power BI. This enables advanced data shaping and analytics, such as forecasting, that go beyond the standard built-in visuals.

---
### Creation and Publishing Workflow
- **Creation:** R visuals can **only be created in Power BI Desktop**.
- **Publishing:** Once created, the report containing the R visual is published to the **Power BI service**, where it can be viewed and interacted with by other users.
### Behavior and Interaction
In the Power BI service, R visuals largely behave like other visuals. Users can filter and slice them. However, there are critical differences:
- **No Tooltips:** R visuals **do not** support tooltips.
- **Limited Interactivity:** R visuals respond to highlighting from other visuals, but you **cannot** select elements within an R visual to cross-filter other visuals on the page.
### Security, Licensing, and R Packages
**Security**
- The Power BI service applies a **"sandbox"** technology to R scripts. This imposes restrictions to protect users from security risks, such as blocking access to the internet or other external resources from within the script.
**Licensing**
- A **Power BI Pro** or **Premium Per User (PPU)** license is required to render, refresh, and interact with R visuals in reports in the Power BI service.
- Users with a **Free** license can only consume R visuals if the report is hosted in a Premium workspace.
**R Packages**
- **Power BI Desktop:** You can install and use **any R package** without limitation, including custom packages.
- **Power BI Service:** Only a **specific list of R packages** published on CRAN (Comprehensive R Archive Network) are supported. Private or custom packages are not supported in the service. You can request for a new package to be added.
### Key Considerations and Limitations
It is crucial to be aware of the following limitations when using R visuals:
- **Data Limits:**
    - The input data used for plotting is limited to **150,000 rows**. If more are selected, only the top 150,000 are used.
    - The input data also has a size limit of **250 MB**.
- **Calculation Timeout:** If an R visual's calculation exceeds **60 seconds**, the script will time out and display an error.
- **Unsupported Data Types:** The `Time` data type is not supported. You should use `Date/Time` instead.
- **Unsupported Features:**
    - R visuals **do not display** when using **Publish to web**.
    - R visuals are **not included** when printing a report.
- **DirectQuery Limitation:** R visuals are **not supported** in DirectQuery mode for Analysis Services.
- **Error Handling:** If an R script encounters an error (e.g., a missing package in the service), the visual will not be plotted, and an error message will be displayed on the canvas.
### Creating R visual
#### Prerequisites
Before you start, you must have two things installed on your local machine.
1. **Power BI Desktop**.
2. A local installation of the **R language**.
#### Steps to Create an R Visual
[Create Power BI visuals using R - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-r-visuals)
##### 1. Enable R Scripting in Power BI Desktop
First, you need to tell Power BI Desktop where to find your R installation.
1. In Power BI Desktop, go to **File > Options and settings > Options**.
2. In the Options window, select **R scripting**.
3. In the **Detected R home directories**, ensure that the correct path to your R installation is selected. If not, browse to the correct folder.
##### 2. Add the R Visual to Your Report
1. In the **Visualizations** pane, select the **R script visual** icon.
2. Power BI will add a placeholder for the R visual on your report canvas and open an **R script editor** pane at the bottom of the screen.
##### 3. Add Data to the Visual
This is the most important step. You add the data you want to analyze from your **Data pane** into the **Values** field well of the R visual.
- **Action:** Drag fields (columns or measures) into the **Values** well.
- **What Happens:** Power BI takes the data from these fields and automatically creates an R **data frame** named `dataset`. Any duplicate rows are removed. You will use this `dataset` data frame in your R script.
##### 4. Write Your R Script
Now, you write the R code in the **R script editor** pane that will generate your plot. The script should perform any necessary analysis and then create a plot.
- **Example Script:** Let's say you added `[Sales Amount]` and `[Product Cost]` to the Values well. You could write a simple script to create a scatter plot.
```R
    # The 'dataset' data frame is automatically created by Power BI
    # with the data you added to the 'Values' well.
    
    # Use the plot() function from base R to create a scatter plot
    plot(dataset$`Sales Amount`, dataset$`Product Cost`)
```
##### 5. Run the Script
Click the **Run script** icon in the header of the R script editor pane.
**Outcome:** Power BI will execute your R script. If the script runs successfully and generates a plot, that plot will appear in the R visual placeholder on your report canvas. If there are any errors in your code or if a required R package is not installed, an error message will be displayed instead.
## Python Visuals in Power BI
[Learn which Python packages are supported - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/connect-data/service-python-packages-support)
Python visuals allow you to use the extensive data visualization libraries of Python, such as `pandas` and `Matplotlib`, to create highly customized visuals directly within a Power BI report.

---
### Prerequisites
Before you can create a Python visual, you must have the following installed and configured on your local machine:
- **Python:** A local installation of the Python runtime.
- **Power BI Desktop:** With Python scripting enabled in **File > Options and settings > Options > Python scripting**.
- **Python Libraries:** The required libraries, such as `pandas` and `Matplotlib`, must be installed in your Python environment.
### How to Create a Python Visual
The creation process happens entirely within **Power BI Desktop**.
1. **Enable Script Visuals:** Select the **Python visual** icon from the **Visualizations** pane. If prompted, click **Enable**.
2. **Add Data:** Drag the fields (columns or measures) you want to analyze from the **Data pane** into the **Values** field well of the visual.
3. **Automatic Data Frame:** Power BI automatically takes the data you added and creates a **pandas DataFrame** named `dataset`. Duplicate rows are removed by default.
4. **Write Your Python Script:** In the **Python script editor** pane that appears at the bottom, write your Python code. This script will typically use a library like `Matplotlib` to create a plot based on the `dataset` DataFrame.
5. **Run the Script:** Click the **Run** icon in the header of the script editor. If the script is successful, the plot will appear in the Python visual on your report canvas.
**Example Script (Scatter Plot):** This script assumes you have added `Age` and `Weight` to the `Values` well.
```python
import matplotlib.pyplot as plt 
dataset.plot(kind='scatter', x='Age', y='Weight', color='red') 
plt.show()
```
### Behavior and Interaction
- **Refreshing:** Python visuals automatically refresh and re-run their script upon data updates, filtering, or highlighting from other visuals.
- **Limited Interactivity:** The image generated by the script is **not interactive**.
    - They **do not** support tooltips.
    - You **cannot** select elements within a Python visual to cross-filter other visuals on the page.
### Security, Licensing, and Limitations
#### Security
- Because Python visuals run scripts, Power BI will display a **security warning** the first time you interact with one. You should only enable them if you trust the author and the source of the script.
#### Licensing
- A **Power BI Pro** or **Premium Per User (PPU)** license is required to render Python visuals in the Power BI service.
- Users with a **Free** license can only consume Python visuals if the report is hosted in a Premium workspace.
#### Key Limitations
- **Data Limits:**
    - The input data is limited to **150,000 rows**.
    - The input data also has a size limit of **250 MB**.
- **Calculation Timeout:** If a Python script takes longer than **five minutes** to execute, it will time out and display an error.
- **Resolution:** All Python visuals are displayed at 72 DPI.
- **No Column Renaming:** The script refers to columns by their original names; you cannot rename them in the visual's field well.
- **No Interaction:** As mentioned, Python visuals do not support tooltips or cross-filtering other elements.
- **Default Plotting Device:** Your script must plot to the Python default display device to render correctly on the canvas.