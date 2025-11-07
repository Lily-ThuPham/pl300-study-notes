_**Power BI Q&A** is a feature that allows users to explore data and get answers by asking questions in **natural language**._
[Q&A for Power BI business users - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-q-and-a)
[Learn how to use natural language to explore data with Power BI Q&A - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/natural-language/q-and-a-intro)
### 1. Where and How to Use Q&A
The Q&A feature is available in different forms across the Power BI ecosystem. It's important to understand where each is used and who the primary user is.

| Location / Method              | How It's Used                                                                             | Primary User    | Can Results Be Saved?                                                                             |
| ------------------------------ | ----------------------------------------------------------------------------------------- | --------------- | ------------------------------------------------------------------------------------------------- |
| **On a Dashboard**             | A Q&A question box appears by default at the top of the dashboard for data exploration.   | Report Consumer | Yes, the resulting visual can be **pinned** to the dashboard.                                     |
| **Q&A Visual in a Report**     | A dedicated visual added to the report canvas for persistent, interactive Q&A.            | Report Consumer | Yes, a report author can **convert** the Q&A result into a standard, static visual in the report. |
| **Q&A Button in a Report**     | A button that opens a temporary, pop-up Q&A window for quick exploration.                 | Report Consumer | No, visuals created this way are for **exploration only** and cannot be saved.                    |
### 2. The User Experience: How Q&A Works
When a user interacts with Q&A, it provides an interactive experience to help form questions and interpret results.

- **Suggestions:** Even before typing, Q&A offers suggested questions based on the data model to help users get started.
- **Autocomplete:** As you type, Q&A provides relevant and contextual suggestions.
- **Underlines:** Q&A uses colored underlines to give feedback on which words it understood:
    - **Solid Blue:** The word was successfully matched to a field or value in the model.
    - **Orange Dotted:** Low confidence match. The word is ambiguous (e.g., "Sales" could be in multiple fields) or is a synonym.
    - **Red Double:** The word was not recognized at all.
- **Automatic Visualization:** Q&A automatically picks the best visual for the answer based on the question and the data types of the fields involved (e.g., questions with dates often result in a line chart). You can override this by adding "as a [chart type]" to your question.

### 3. How to Optimize Q&A for Better Results
For Q&A to work effectively, the underlying data model must be well-structured. As a report author, you can significantly improve the Q&A experience through two main methods: **Q&A Tooling** and **Data Model Best Practices**.

#### 3.1 Using Q&A Tooling (Teaching Q&A)
This is where you explicitly teach Q&A about your business-specific language. You can access it from the **Modeling** ribbon in Power BI Desktop or via the gear icon on a Q&A visual.
**How to Access the Tooling:** You can access the Q&A setup menu from either Power BI Desktop or the Power BI Service.
- **In Power BI Desktop:**
    1. Navigate to the **Modeling** ribbon.
    2. Click the **Q&A Setup** button. This opens the full tooling window 
    or: 
	3. Select a **Q&A visual** on the report canvas.
    4. Click the **gear icon (⚙️)** on the top-right corner of the visual. This will open the Q&A tooling pane. 
- **In the Power BI Service:**
    1. Open a report in **Edit mode**.
    2. Select a **Q&A visual** on the report canvas.
    3. Click the **gear icon (⚙️)** on the top-right corner of the visual. This will open the Q&A tooling pane. 

**The Q&A Tooling Pane:** This pane allows you to train and refine how Q&A understands your data model.
- **Synonyms**: You can only teach Q&A two types of terms - **_Nouns and Adjectives_**
	- Define a noun synonym: You should map it to an existing field in your model (e.g., "Revenue" refers to `[Total Sales]`).
		- Q&A automatically detects when an unrecognized word is a noun by using knowledge from Microsoft Office.
    - Define an adjective filter condition: Some example conditions that you can define are:
		- Country/region which is USA
		- Country/region which is not USA
		- Products > 100
		- Products greater than 100
		- Products = 100
		- Products is 100
		- Products < 100
		- Products smaller than 100

- **Teach Q&A:** This feature allows you to define unrecognized (red-underlined) words.
	- Type a question that contains words that Q&A doesn't recognized.
	- Enter a filter or a field name that corresponds to what the words represents.
	- Save your input.
- **Review questions:** See what questions users have been asking to identify common terms and areas for improvement.
- **Manage Synonyms:** This section allows you to review and manage all the **noun** definitions you have taught Q&A.
- **Manage Relationships:** This section allows you to review and manage the **adjective** (filter condition) definitions you have created.
#### 3.4 Q&A Tooling advanced - Linguistic schema 
The **Linguistic Schema** is an advanced feature that allows data modelers to improve Q&A results by directly editing a text file that defines terminology and relationships. This provides more granular control than the standard Q&A tooling.
- **What it is:** A `.yaml` file that contains definitions for parts of speech, synonyms, and **phrasings** that Q&A should understand for your dataset.
- **How to work with it:** The process involves:
    1. **Exporting** the linguistic schema from the **Modeling** tab in Power BI Desktop.
    2. **Editing** the `.lsdl.yaml` file in a text editor (like Visual Studio Code).
    3. **Importing** the edited file back into Power BI Desktop.

#### 3.3 Data Model Best Practices for Q&A
The same best practices for any good data model are essential for Q&A.

|Best Practice|What to Do|Why It's Important for Q&A|
|---|---|---|
|**Add Missing Relationships**|Ensure all tables in your model are correctly related with active, single-direction relationships (star schema).|**This is the most critical step.** Without relationships, Q&A cannot understand how to join tables to answer questions that span multiple tables (e.g., "total sales for Seattle customers"). Q&A can only use **active** relationships.|
|**Rename Tables and Columns**|Use simple, user-friendly names for tables and columns (e.g., "Customers" instead of "CustomerSummary").|Q&A assumes your table and column names accurately reflect their content. Users will ask questions using natural business terms.|
|**Fix Incorrect Data Types**|Ensure date columns are set to the `Date` type and numbers are set to numeric types.|Q&A cannot interpret date or number columns correctly if they are imported as text strings.|
|**Set Default Summarization**|For columns that should not be summed (like `Year` or `ID` columns), set the default **Summarization** to **"Don't summarize."**|This prevents nonsensical results, like Q&A returning a "Sum of Year" when asked "total sales by year."|
|**Set Data Category**|For date and geography columns, set the appropriate **Data Category** (e.g., "City," "Country/Region," "Postal Code").|This helps Q&A choose the right visual (like a map for geography) and understand context (the "when" in a question likely refers to a date column).|
|**Normalize Your Model**|Reshape your data so that each unique "thing" is represented by one table or column. This includes pivoting property bags and unioning partitioned tables.|A normalized model is less ambiguous and easier for Q&A to interpret correctly.|
|**Split Formatted Columns**|Split composite columns into their individual components (e.g., a "Full Address" column into separate columns for Address, City, and Country).|This allows users to ask questions about the individual components, like "sales by city."|
### 4. Creating a Visual with Q&A
This section compares the two methods of creating a visualization: using natural language with **Q&A** versus building it manually in the **report editor**. Often, using Q&A is the faster and easier approach.
#### 4.1 Creating a Visual in a Dashboard using Q&A
1. **Open a dashboard** in the Power BI service.
2. Locate the Q&A box at the top, which says **"Ask a question about your data."**
3. **Type your question** in natural language. As you type, Q&A will:
    - Dynamically change the visualization to best display the answer.
    - Offer suggestions, autocomplete, and spelling corrections to help you format your question.
4. Once you are satisfied with the resulting visual, select **Pin visual** to save it as a new tile on your dashboard

**Example:** Typing `this year sales and last year sales by month as area chart` will generate an area chart comparing the sales figures for both years over time.
#### 4.2 Creating the Same Visual in the Report Editor
This is the standard, manual method for building visuals.
1. **Open a report** in "Editing view" in the Power BI service or Power BI Desktop.
2. **Select a visual type** from the Visualizations pane (e.g., an Area chart).
3. **Drag and drop fields** from the Data pane into the appropriate field wells. To create the same area chart as the example above, you would:
    - Drag `FiscalMonth` to the **Axis** well.
    - Drag `Last Year Sales` and `This Year Sales` to the **Values** well.

### 5. Using Q&A on a Power BI Service Dashboard

The **Q&A feature** on a Power BI dashboard allows users, especially business users without deep technical skills, to explore data and generate visualizations by asking questions in plain language.
#### 5.1 Accessing the Q&A Feature
1. Navigate to the relevant **Dashboard** in the Power BI Service.
2. Locate the question box, typically at the top, labeled **"Ask a question about your data"**.
3. Select this box to open the full Q&A window.
#### 5.2 Using the Q&A Interface
The Q&A window provides suggestions and a text box for your queries.
- **Suggestions:** Power BI offers pre-populated question suggestions to help you get started.
- **Question Box:** Start typing your question here using natural language.
#### 5.3 Building a Visual Step-by-Step (Example)
Let's recreate the example from the transcript: A funnel chart showing the sum of sales by country, excluding blanks
1. **Enter the Calculation:** Start by typing the aggregation you need.
    - _Example:_ `Sum of Sales Amount`
    - _Result:_ Q&A usually shows a Card visual with the total value.    
2. **Specify the Chart Type:** Tell Q&A which visual you want.
    - _Example:_ `Sum of Sales Amount funnel chart` 
    - _Result:_ Q&A changes the visual to a funnel chart, initially showing just the single total value.    
3. **Add the Context/Category:** Specify how you want the data to be broken down.
    - _Example:_ `Sum of Sales Amount funnel chart by Country-Region`
    - _Result:_ The funnel chart now shows the sales amount segmented by each country found in the data.
4. **Apply Filters:** You can add filtering conditions using natural language.
    - _Example:_ `Sum of Sales Amount funnel chart by Country-Region without blank`
    - _Result:_ Q&A understands "without blank" as a filter and removes the blank category from the funnel chart.
#### 5.4 Pinning the Visual
Once you are satisfied with the visual generated by Q&A:
1. Select the **Pin visual** icon in the top-right corner of the Q&A window.
2. Choose the dashboard where you want to add this visual.
3. Select **Pin**.