### 1. Grouping and layering visuals: Organizing Your Report Canvas
**Grouping** allows you to combine multiple report objects (visuals, buttons, shapes, text boxes) and treat them as a single object. This is the foundation for creating organized and complex interactive layouts.
#### Selection Pane
The Selection Pane in Power BI allows you to manage the visibility and layering of objects on your report page.
1. **Opening the Selection Pane**: You can enable the Selection pane from the **View** tab in Power BI Desktop.
2. **Navigating the Selection Pane**: Once opened, you can use the **F6** key to activate the Selection pane. Use the **Up** and **Down** arrow keys to navigate through the different objects listed.
3. **Managing Object Visibility**: To hide or show an object, select it and press **Ctrl + Shift + S**.
4. **Reordering Objects**: You can change the layering order of objects. To move an object up in the layer order, press **Ctrl + Shift + F**, and to move it down, press **Ctrl + Shift + B**.
5. **Multi-selecting Objects**: If you want to select multiple objects at once, you can use **Ctrl + Space**.
#### Naming visuals 
Visuals such as charts, matrixes, cards are automatically named by their titles (Visual **Format > General > Title**). You can rename other report elements (text boxes, buttons, shapes,...) by double clicking their names on **Selection pane**. 
#### Key Features of Grouping
- **How to Create:** **Ctrl+Click** to select multiple objects on the canvas, then right-click and select **Group > Group** on the **Report view > Format** pane. Rename the group by double click on the Group name.
- **Management via the Selection Pane:** Groups are managed in the **Selection pane** (found under the **View** tab). This pane is essential for working with groups effectively.
    - You can **rename** a group by double-clicking its name in the pane.
    - You can create **nested groups** by dragging one group into another.
    - You can easily **show or hide** an entire group by clicking the eye icon next to its name. Hiding a group hides all the visuals within it.
- **Applying a Background Color:** You can go to the **Format** pane for a group and apply a background color. This not only visually groups the items but also changes the selection behavior: clicking on the empty space _between_ visuals within the group will now select the entire group.
#### How to Select and Manage Visuals Within a Group
This can be tricky, but there are two main ways to interact with items inside a group.
- **On the Report Canvas:**
    - **First Click:** Clicking any visual within a group will select the **entire group**.
    - **Second Click:** Clicking the same visual again will drill in and select the **individual visual** itself.
- **In the Selection Pane (Recommended Method):**
    - The Selection pane shows a hierarchical list of all objects on the page.
    - To select the **entire group**, click the group's name in the pane.
    - To select a **single visual inside a group**, simply find and click on that visual's name within the group's hierarchy in the pane. This is the most precise way to select a specific nested item.

### 2. Bookmarks: Capturing Report States
A **bookmark** is a saved "snapshot" of the current state of a report page. It's the core mechanism for creating guided stories, presentations, and custom navigation experiences.
#### Key Features of Bookmarks
- **What is saved:** When you create a bookmark, it saves the following elements:
    - The current page
    - All applied **Filters** and **Slicers**
    - The **Visual selection state** (like cross-highlighting)
    - The **Sort order** of visuals
    - The current **Drill location** in a visual
    - The **Visibility of objects** (as configured in the **Selection pane**)
- **How to Create:**
    1. Go to the **View** tab and enable the **Bookmarks** and **Selection** panes.
    2. Set up your report page to the exact state you want to capture (apply filters, hide visuals, etc.).
    3. In the **Bookmarks** pane, click **Add**.
- ==**Bookmark Properties:**== You can control which properties a bookmark affects. By selecting **More options (...)** next to a bookmark, you can choose whether it updates:
    - **Data:** Controls whether the bookmark applies the saved filters and slicers.
    - **Display:** Controls whether the bookmark applies visibility changes (from the Selection pane) and spotlight effects.
    - **Current page:** Controls whether activating the bookmark will navigate the user to the page it was created on.
    - **All visuals / Selected visuals:** Allows you to create a bookmark that only affects specific visuals you have selected.

**Best Practice:** When creating bookmarks for navigation or toggling visuals, it's often a good idea to **uncheck the "Data" property**. This ensures that when a user clicks a button to show a hidden chart, it doesn't also reset all the filters and slicers they have already applied.
### 3. Buttons: Enabling User Actions
**Buttons** are interactive objects that you add to your report to trigger specific actions when a user clicks them. They are what bring your bookmarks and navigation to life.
- **Creation:** On the **Insert** ribbon, select **Buttons** and choose from a variety of pre-styled options (e.g., Back, Blank). You can also turn **shapes and images** into buttons by assigning an action to them.
	In Power BI Desktop, in **Report view**, on the **Insert** ribbon, select **Buttons** to reveal a drop-down menu.
	In the Power BI service, open the report in Editing view. Select **Buttons** in the top menu bar to reveal a drop-down menu,
![Screenshot showing Add an Apply all slicers button control in Power BI Desktop.](https://learn.microsoft.com/en-us/power-bi/create-reports/media/buttons-apply-all-clear-all-slicers/power-bi-apply-all-button-dropdown.png)
#### Key Features of Buttons

- **Customization (Button States):** A key feature of buttons is the ability to set different formatting for each of their states to provide clear visual feedback to the user. These states are:
    - **Default:** How the button appears normally.
    - **On hover:** How it appears when a user's mouse is over it.
    - **On press:** How it appears at the moment it is clicked.
    - **Disabled:** How it appears when its action is not available (e.g., a drillthrough button when nothing is selected).
- **Actions:** The most important feature is the **Action** you assign to the button. The most common action types are:
    - **Bookmark:** Activates a specific bookmark you have created. This is the most common use case for custom navigation.
    - **Page navigation:** Navigates the user to a different page in the report.
    - **Drill through:** A special type of button that is only enabled when a user has selected a valid data point. Clicking it navigates them to a drillthrough page filtered to their selection.
    - **Back:** Returns the user to the previous page they were on.
    - **Web URL:** Opens an external web page.
### 4. Built-in Navigators (Page and Bookmark)
To save significant development time, Power BI has built-in **navigators** that automatically create and manage a group of buttons for you.
- **Page Navigator:** Automatically creates a button for **every visible page** in your report. The buttons stay in sync with your page names and order, making it the fastest way to build a standard page navigation menu.
- **Bookmark Navigator:** Automatically creates a button for **every bookmark** in a specific bookmark group you select. This is the best way to create a toggle switch experience (e.g., a two-button navigator linked to a bookmark group containing "Show Chart" and "Show Table" bookmarks).