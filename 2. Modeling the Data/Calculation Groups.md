[Create calculation groups in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/transform-model/calculation-groups)
[Calculation groups in Analysis Services tabular models | Microsoft Learn](https://learn.microsoft.com/en-us/analysis-services/tabular-models/calculation-groups?view=sql-analysis-services-2025#benefits)
**Calculation Groups** are a powerful feature in Power BI (and Analysis Services Tabular models) designed to significantly **reduce the number of redundant measures** you need to create, especially for common calculations like time intelligence.

---
### 1. The Benefit: Reducing Measure Proliferation
- **Problem:** Complex models often require many similar calculations applied to different base measures (e.g., Sales MTD, Sales QTD, Sales YTD, Orders MTD, Orders QTD, Orders YTD, etc.), leading to a large number of individual measures.
- **Solution:** Calculation groups allow you to define a common calculation pattern (like MTD, QTD, YTD) once as a **calculation item**. This calculation item can then be applied dynamically to any existing base measure in your report.
### 2. How Calculation Groups Appear to Users
- In reporting tools like Power BI, a calculation group appears as a **table with a single column**.
- Users can drag this column into a visual (often as a slicer, filter, or on the columns/rows axis of a matrix).
- Selecting a value (a calculation item) from this column dynamically changes how the base measures in the visual are calculated.
### 3. How They Work: Key Concepts & Functions
- **Structure:** A calculation group consists of:
    - A **Table** (e.g., "Time Intelligence")
    - A **Calculation Column** (e.g., "Time Calculation") - This is the column users interact with.
    - Multiple **Calculation Items** (e.g., "Current", "MTD", "YTD", "PY") - Each item contains a DAX formula.
- **`SELECTEDMEASURE()` Function:** This is the core DAX function used within calculation items. It acts as a **placeholder** that refers to the base measure currently being evaluated in the visual's context (e.g., `[Total Sales]` or `[Total Orders]`).
- **Example Calculation Item (YTD):**
```DAX
-- Inside the "YTD" calculation item:
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

When this item is applied to the `[Total Sales]` measure, `SELECTEDMEASURE()` is replaced by `[Total Sales]`, effectively calculating `CALCULATE([Total Sales], DATESYTD(DimDate[Date]))`.
### 4. Dynamic Format Strings within Calculation Groups
- Calculation items inherit the format string of the base measure by default.
- However, you can define a **dynamic format string expression** for specific calculation items.
- **Example:** For a `YOY%` calculation item, you can set its format string expression to `"0.00%;-0.00%;0.00%"` to ensure it always displays as a percentage, regardless of the base measure's format.
### 5. Precedence: Controlling Evaluation Order
- **What it is:** A numerical property set for each calculation group that determines the **order of evaluation** when multiple calculation groups are applied simultaneously to the same base measure.
- **How it works:** The calculation item from the group with the **higher precedence** value is evaluated first. The `SELECTEDMEASURE()` placeholder within it is then replaced by the expression from the group with the next highest precedence, and so on, until the base measure is reached.
### 6. Creating Calculation Groups
- **Where:** Calculation groups are created in **Power BI Desktop** within the **Model view**.
- **How:**
    1. Go to **Model view**.
    2. Select the **Calculation group** button in the ribbon.
    3. (If prompted) Agree to **discourage implicit measures**. This is a requirement.
    4. A new calculation group table is created. Define calculation items and their DAX expressions using `SELECTEDMEASURE()`.
- **Prerequisite:** Calculation groups **only work with explicit measures** (measures you create with DAX). They do not work with implicit measures (automatic aggregations created by dragging columns into visuals).
### 7. Key Limitations
- **Security:** Object-Level Security (OLS) and Row-Level Security (RLS) cannot be defined _directly_ on calculation group tables themselves.
- **Unsupported Features:**
    - Detail Rows Expressions
    - Start Narrative visuals
    - Implicit column aggregations