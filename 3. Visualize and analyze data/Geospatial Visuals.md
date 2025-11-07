## **Choropleth maps (Filled maps)**
![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI service
[Create and use filled maps (choropleth maps) in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-filled-maps-choropleths?tabs=powerbi-desktop)
A filled, or _choropleth_, map uses shading, tinting, or patterns to display how a value differs in proportion across a geography or region. You can quickly display relative differences with shading that ranges from light (less frequent or lower) to dark (more frequent or greater).
![Screenshot of a filled map of the United States.](https://learn.microsoft.com/en-us/power-bi/visuals/media/power-bi-visualization-filled-maps-choropleths/large-map.png)

##### **Key features**:
- **Predefined Boundaries**: Field maps utilize geographical boundaries provided by Power BI's built-in mapping capabilities, which means users do not need to supply custom geographic data.
- **Color Shading**: They use color gradients to represent data values, allowing users to visualize data distribution and patterns across various regions.
- **Simplicity**: Field maps offer a straightforward approach to map visualization, making it easy to gain quick insights into data distribution.
##### **Appropriate Data types**:
Choropleth maps are particularly effective for visualizing data that has clear geographic boundaries and can be represented by varying intensities of color or patterns.
The data should include at least two columns:
- the geographical regions 
- the relevant quantitative data, such as total sales, revenue, or profit corresponding to each region.
###### Creating a Data Model
In Power BI, creating an effective data model is the foundation of any compelling visualization. Ensure that the columns representing regions are in text format and contain matching names or codes for the regions present in the map data visualization. Similarly, the quantitative data should be in numerical format for accurate analysis.
### Use Cases for Choropleth Maps 
Filled maps are a great choice in many scenarios:
- Display quantitative information on a map.
- Show spatial patterns and relationships.
- Support standardized data.
- Work with socioeconomic data.
- Support defined regions.
- Display an overview of distribution across geographic locations.
### Create and Utilize filled maps 
#### Enabling Shape Map Visual
To use shape maps in Power BI, you need to enable the feature:
1. Navigate to **File > Options and Settings > Options > Global > Preview features**.
2. Select the shape map visual checkbox and click OK.
3. Restart Power BI Desktop.
#### Configuring Choropleth map 
- **Customize Colors**: Select the view tab to change the color scheme to a more accessible one, such as accessible city park. Apply gradient colors by going to format visual > visual > fill colors, and turning the gradient toggle to the on position. Add light blue for the minimum, purple for the center, and black for the maximum.
- **Adjust Border Color**: Change the border color to black and set the width to three.
- **Display Map Keys**: Select the map settings dropdown, then view map type key. This action opens a dialog that lists the map keys. You can change the map type to view keys for other countries if required.
- **Choose Projection**: Use the projection option to present a 3D object on a 2D map. Power BI selects Albers USA map style by default, but other options like equirectangular, Mercator, and orthographic are available.
- **Enable Zoom Options**: Access the zoom dropdown and toggle on the zoom on selection and manual zoom options.
### Getting data ready for Power BI Maps 
#### Identifying suitable data for the filled map visual 
- **Geographical Information**: Columns representing geographical regions (e.g., countries, states, cities) or latitude and longitude coordinates.
- **Quantitative Data**: Columns with corresponding data values you want to visualize (e.g., sales, revenue, population).
#### Data Formats
- **State Names and Codes**: Ensure consistency in spelling and format (e.g., "USA" vs. "United States").
- **Latitude and Longitude**: Use coordinates to represent specific locations.
#### Cleaning and Formatting Data 
- **Consistency**: Ensure geographical region names are consistent and match the map data visualization.
- **Handling Missing Data**: Replace missing values with default values or exclude them from the visualization.
#### Optimizing Data for Performance
- **Aggregation**: Summarize data at higher levels (e.g., state or country) to reduce data volume and improve performance.
- **Custom Regions**: Import custom map data in JSON format for unique geographical boundaries.
#### Verifying Geographical Data
- **Validation**: Use Power BI tools to validate and correct geographical data alignment.
- **Data Categories**: Assign appropriate data categories (e.g., country, city, state) to geographical data in Power BI Desktop.
## **Shape map**
![](https://learn.microsoft.com/en-us/power-bi/includes/media/yes-icon.svg) Power BI Desktop ![](https://learn.microsoft.com/en-us/power-bi/includes/media/no-icon.svg)  Power BI service
[Use Shape Maps in Power BI Desktop (Preview) - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/visuals/desktop-shape-map)
Shape maps enable users to represent geographical and sales data effectively, **Shape map** doesn't show precise geographical locations of data points on a map. Instead, its main purpose is to compare regions on a map by coloring them differently.
![Screenshot of a shape map example.](https://learn.microsoft.com/en-us/power-bi/visuals/media/desktop-shape-map/power-bi-shape-map.png)
#### Create and configure shape map 
- To use shape maps in Power BI, you must enable the feature in the options menu and restart Power BI Desktop.
- **Apply gradient colors** to represent data values effectively and customize the map's appearance by changing border colors and widths.
- **Map Keys and Projections**: Display map keys and choose from different projection options like Albers USA, equirectangular, Mercator, and orthographic.
	- **Albers USA**: It keeps the shapes of states and regions looking more accurate compared to other projections. t’s often used for maps that need to show data across the U.S., like demographic information or weather patterns.
	- **Equirectangular**: This projection takes the globe and flattens it into a rectangle. It keeps the same size and shape for each cell in the grid, making it easy to understand, but it can distort areas, especially near the poles.
	- **Mercator**: This is a cylindrical projection that stretches the map as you move away from the equator. It’s great for navigation because it keeps angles straight, but it makes land areas near the poles look much larger than they really are.
	- **Orthographic**: This projection shows the Earth as if you were looking at it from space. It gives a 3D effect. You can see the curvature of the Earth, but you can only see half of the planet at a time.
- **Zoom Options**: Enable zoom on selection and manual zoom options for better interactivity.
### Load a custom TopoJSON map
1. Add or select a Shape map visual.
2. Open the **Format** pane and expand **Map settings**.
3. In **Map type**, select **Custom map**.
4. Select **Add a map type**.
5. Browse to and select your **.topojson** file, then select **Open**.
6. (Optional) Select **View map type key** to verify region names or IDs match your **Location** field values.
## Geo hierarchy - Tips with Map visualizations
A **geo hierarchy** in Power BI is a structured way to organize geographical data into levels that allow for detailed analysis and visualization.
1. **Continent**: The broadest level, categorizing data by continents (e.g., North America, Europe, Asia).
2. **Country**: The next level, representing individual countries within each continent.
3. **Region**: Subdivisions within countries, which can vary (e.g., states in the USA, provinces in Canada).
4. **City**: A more granular level focusing on specific cities within each region.
5. **District/Neighborhood**: The most detailed level, representing smaller areas within cities.
Creating a geo hierarchy is crucial for drilling down into specific locations, such as states and cities, to provide a comprehensive analysis.
**Benefits of Using Geo Hierarchy:**
- **Drill Down Functionality**: Users can click on a geographical area (e.g., a country) to view more detailed data (e.g., sales by state or city).
- **Enhanced Insights**: It allows for a clearer understanding of data trends and patterns at different geographical levels.
**Setting Up the Data**
- Properly formatting geographical columns in the data tables is necessary to ensure accurate location representation, including setting data categories for country, state, and city.
- The sales amount should be formatted as currency, and a filled map visual can be created by dragging the relevant fields into the location and tooltip areas.
**Enhancing Insights with Drill Down Features**
- Utilizing drill down functions allows users to navigate through the geo hierarchy, from country to state to city, providing detailed sales insights at each level.
- Color coding the map based on sales data enhances visual differentiation, and filters can be applied to focus on specific regions, such as the United States.
# Accessing the map 
Power BI offers various map styles, including Road and Aerial, allowing users to select the most suitable visual representation for their data.
#### Formatting and customizing maps 
- Conditional formatting allows users to modify map colors to represent different sales values, with yellow indicating lower sales and purple indicating higher sales.
- Labels and titles can be renamed for clarity, making the visual less cluttered and easier to understand.
#### Enhancing user interaction 
- Tooltips can be customized to display relevant information when hovering over regions, with options to change background colors and data display styles.
- A well-designed map visual, such as renaming fields and adjusting titles, contributes to creating engaging dashboards and reports in Power BI.

| Feature                      | Shape Maps                                                                                                                                          | Filled Maps (Choropleth Maps)                                                                                                                                                                                                                     |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Customization**            | High customization, allowing users to import custom geographic data. Ideal for unique boundaries and territories.                                   | Utilizes predefined geographical boundaries from Bing Maps. Minimal customization required.                                                                                                                                                       |
| **Data Sources**             | Requires users to provide custom geographic data, typically in TopoJSON format.                                                                     | Uses Bing Maps' extensive geographic database.                                                                                                                                                                                                    |
| **Precision**                | Accurate representation of non-standard geographic regions. Suitable for precise and granular visualizations.                                       | Provides a more generalized view of data distribution. Suitable for high-level overviews.                                                                                                                                                         |
| **Use Cases**                | Best for visualizing complex geographic representations like sales territories, customer distribution, or custom-defined administrative boundaries. | Ideal for showcasing high-level data patterns like population densities, sales performance by country, or regional sales growth.<br>Most effective when visualized data has clear geographic boundaries, such as countries, states, or districts. |
| **Handling Data Complexity** | Can handle intricate boundaries and smaller regions due to user-provided geographic data.                                                           | Simplified visualization process; does not require specialized geographic data sets.                                                                                                                                                              |
| **Integration**              | Does not integrate with external geographic databases.                                                                                              | Integrated with Bing Maps/Azure Maps, ensuring accurate and up-to-date boundary information.                                                                                                                                                      |
| **Examples**                 | Visualizing company-specific sales territories with unique boundaries.                                                                              | Quickly assessing sales densities by country or region using color gradients.                                                                                                                                                                     |