_**Visual calculations** are DAX calculations that are defined and executed directly on a visual._
### Key Characteristics
- **Defined on the Visual:** The DAX formula for a visual calculation is ==stored with the visual itself==, not in the semantic model.
- **Simplified Context:** They operate only on the data that is currently **present in the visual**. This removes the complexity of the full semantic model and filter context, making the DAX easier to write and understand.
- **Dependencies:** A visual calculation can refer to any data in its host visual, including columns, measures, or even other visual calculations. To use a field from your model in a visual calculation, you must first add that field to the visual.
### Benefits of Using a Visual Calculation
- **Simplicity:** The DAX required is often easier to write and maintain compared to traditional measures because you don't have to worry about complex filter interactions from the wider data model.
- **Performance:** ==They operate on **aggregated data**== (like measures) instead of row-level data (like calculated columns), which often results in better performance. When you have a choice,==a visual calculation is usually faster than creating a new, complex measure==.
- **Flexibility:** Because they are part of the visual, they can refer to the visual's structure, offering more flexibility for certain calculations.

---
### Create Visual Calculations 
To create a visual calculation, select a visual and then choose **New calculation** from the **Home** ribbon.
The edit mode window has three main parts:
1. **Visual Preview:** Shows the final visual you are working with.
2. **Formula Bar:** Where you type your DAX expression for the calculation.
3. **Visual Matrix:** Shows the underlying data for the visual in a table format and displays the results of your calculations as you create them.
#### Adding a Calculation
You add a visual calculation by typing its DAX expression into the formula bar.
- **Example:** `Profit = [Sales Amount] – [Total Product Cost]`
- **Evaluation:** By default, visual calculations are evaluated **row-by-row** within the visual matrix, similar to how a calculated column works. Because of this, you often don't need to add aggregation functions like `SUM`. It's a best practice to omit them when not necessary to keep the expressions simple.
#### Hiding Fields
In the visual calculation edit mode, you can **hide fields** from the final visual.
- **Purpose:** This is useful when you want to show only the result of your calculation (e.g., `Profit`) without cluttering the visual with the input fields (e.g., `Sales Amount` and `Total Product Cost`).
- **Behavior:** A hidden field is removed from the final visual on the report canvas, but it remains in the **visual matrix**. This ensures that your visual calculations can still refer to the hidden fields and continue to work correctly.
#### Using Templates
Visual calculations include built-in templates to help you quickly write common business calculations. You can access these by selecting the template button in the formula bar.
Available templates include:
- **Running sum**
- **Moving average**
- **Percent of parent**
- **Average of children**
- **Versus previous**
- **Versus next**
#### Available DAX Functions
- **Available:** You can use many existing DAX functions and a new set of functions created specifically for visual calculations.
- **Not Available:** Functions that rely on **model relationships** are not available because visual calculations operate only on the data within the visual's matrix. This includes functions like `USERELATIONSHIP`, `RELATED`, and `RELATEDTABLE`.
---
### Parameters with Visual Calculations
Visual calculations have optional parameters that give you more control over how they are calculated, with the two most important being **`Axis`** and **`Reset`**.
#### The `Axis` Parameter 🧭
The **`Axis`** parameter influences the **direction** in which a visual calculation travels across the visual's data matrix. By default, it is set to `ROWS`, meaning the calculation is evaluated vertically, from top to bottom.
The available `Axis` parameter values are:

|Value|Description|
|---|---|
|**`ROWS`**|Vertically across rows from top to bottom.|
|**`COLUMNS`**|Horizontally across columns from left to right.|
|**`ROWS COLUMNS`**|Vertically down each column, continuing column by column.|
|**`COLUMNS ROWS`**|Horizontally across each row, continuing row by row.|

#### The `Reset` Parameter 🔄
The **`Reset`** parameter influences if and when a function **resets its value** (e.g., to 0) as it moves through the visual matrix. By default, it is set to `None`, meaning the calculation never restarts.
The valid values for the `Reset` parameter are:
- **`NONE`:** (Default) The calculation never resets.
- **`HIGHESTPARENT`:** The calculation resets whenever the value of the **highest-level field** on the axis changes.
- **`LOWESTPARENT`:** The calculation resets whenever the value of the **immediate parent field** on the axis changes.
- **A numerical value:** Allows you to specify which level of the hierarchy to reset by (e.g., `1` for the top level).
##### Example: Understanding `Reset`
Consider a visual with a hierarchy of **Year > Quarter > Month**.
- `RUNNINGSUM([Sales Amount])`
    - This uses the default `NONE` reset. The sum will continuously accumulate across all years without ever restarting.
- `RUNNINGSUM([Sales Amount], HIGHESTPARENT)`
    - The highest parent is **Year**. The running sum will start from 0 at the beginning of **each year**.
- `RUNNINGSUM([Sales Amount], LOWESTPARENT)`
    - When looking at the Month level, the lowest (immediate) parent is **Quarter**. The running sum will start from 0 at the beginning of **each quarter**.