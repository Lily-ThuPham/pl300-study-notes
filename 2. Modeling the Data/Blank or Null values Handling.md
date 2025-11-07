[Handling BLANK in DAX - SQLBI](https://www.sqlbi.com/articles/blank-handling-in-dax/)
The **`BLANK()`** value in DAX represents the absence of a value. It is different from `NULL` in SQL, and its behavior, particularly its automatic conversion to zero or an empty string, is a frequent source of errors if not understood correctly.
[Avoid converting BLANKs to values in DAX - DAX | Microsoft Learn](https://learn.microsoft.com/en-us/dax/best-practices/dax-avoid-converting-blank)

---
### 1. The Core Behavior: Automatic Conversion
The most important concept is that DAX automatically converts `BLANK()` to **`0` (zero)** or an **empty string (`""`)** depending on the context of the operation.
- In **arithmetic operations** (like addition or subtraction), `BLANK()` is treated as `0`.
- In **string operations** (like concatenation), `BLANK()` is treated as `""`.
### 2. BLANK() in Arithmetic Operations 
DAX generally converts `BLANK()` to zero when performing math, except for multiplication and division by blank.

| Expression                  | Result      | Explanation                                                                                                                   |
| --------------------------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `BLANK()`                   | Blank value | Returns a blank (null) value.                                                                                                 |
| `BLANK() = 0`               | `True`      | `BLANK()` is treated as zero in loose equality. The standard equals (`=`) operator allows the conversion of `BLANK()` to `0`. |
| `BLANK() = FALSE`           | `True`      | `BLANK()` is treated as `FALSE` in loose equality.                                                                            |
| `BLANK() == FALSE`          | `False`     | Strict equality checks type; `BLANK ≠ FALSE`.                                                                                 |
| `BLANK() == 0`              | `False`     | Strict equality checks type; `BLANK ≠ 0`.                                                                                     |
| `BLANK() == BLANK()`        | `True`      | Two blank values are considered equal.                                                                                        |
| `BLANK() && TRUE`           | `False`     | Logical `AND` with `BLANK()` returns `FALSE`.                                                                                 |
| `BLANK() \|\| TRUE`         | `True`      | Logical `OR` with `BLANK()` returns `TRUE`.                                                                                   |
| `BLANK() + 4`               | 4           | `BLANK()` acts as zero in addition.                                                                                           |
| `BLANK() + BLANK()`         | Blank value | Adding two blanks returns blank.                                                                                              |
| `BLANK() - 4`               | -4          | `BLANK()` acts as zero in subtraction.                                                                                        |
| `BLANK() - BLANK()`         | Blank value | Subtracting two blanks returns blank.                                                                                         |
| `4 / BLANK()`               | Infinite    | Division by zero returns infinity.                                                                                            |
| `BLANK() / BLANK()`         | Blank value | Division of blank by blank returns blank.                                                                                     |
| `BLANK() * 4`               | Blank value | Multiplying blank returns blank.                                                                                              |
| `BLANK() / 4`               | Blank value | Division of blank returns blank.                                                                                              |
| `BLANK() ^ 1`               | Blank value | Blank raised to any power returns blank.                                                                                      |
| `1 ^ BLANK()`               | 1           | Any number raised to blank (zero) returns 1.                                                                                  |
| `INT(BLANK())`              | Blank value | `INT` of blank returns blank.                                                                                                 |
| `CONVERT(BLANK(), INTEGER`) | Blank value | Conversion of blank returns blank.                                                                                            |
| `BLANK() = ""`              | `True`      | `BLANK()` is loosely equal to empty string. The standard equals (`=`) operator allows the conversion of `BLANK()` to `""`.    |
| `BLANK() == ""`             | `False`     | Strict equality fails due to type mismatch.                                                                                   |
| `BLANK() & "A"`             | `A`         | Concatenating blank with string returns the string.                                                                           |
| `"A" & BLANK()`             | `A`         | Concatenating string with blank returns the string.                                                                           |
| `BLANK() IN { 0 }`          | `False`     | `BLANK()` is not strictly in the set containing 0.                                                                            |
| `BLANK() IN { BLANK() }`    | `True`      | `BLANK()` is in the set containing BLANK.                                                                                     |

### 3. `BLANK()` in Standard Aggregation Functions (`SUM, AVERAGE, MIN, MAX`)
All standard aggregation functions in DAX are designed to **ignore `BLANK()` values**. They perform their calculations only on the valid, non-blank data in the column.

| **Function**  | **Behavior with BLANK() Values**                                                                  | **Example**                                                                                                                                        |
| ------------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`SUM`**     | **Ignores** `BLANK()` values.                                                                     | If a column contains `{10, 20, BLANK()}`, `SUM` will return **`30`**.                                                                              |
| **`AVERAGE`** | **Ignores** `BLANK()` values in both the numerator (the sum) and the denominator (the count).     | If a column contains `{10, 20, BLANK()}`, `AVERAGE` calculates `(10 + 20) / 2`, returning **`15`**. It does **not** calculate `(10 + 20 + 0) / 3`. |
| **`MIN`**     | **Ignores** `BLANK()` values. It will not return `0` unless `0` is an actual value in the column. | If a column contains `{10, 20, BLANK()}`, `MIN` will return **`10`**.                                                                              |
| **`MAX`**     | **Ignores** `BLANK()` values.                                                                     | If a column contains `{10, 20, BLANK()}`, `MAX` will return **`20`**.                                                                              |
| **`COUNT`**   | **Ignores** `BLANK()` values. It only counts non-blank cells.                                     | If a column contains `{10, 20, BLANK()}`, `COUNT` will return **`2`**.                                                                             |
### 4. Common Pitfalls and Scenarios
- **Nested `IF` Statements:** The order of your checks matters. Because `BLANK() = 0` is true, an `IF` statement checking for `BLANK()` will also catch zeros. Use `ISBLANK()`.
- **`COUNTROWS` on an Empty Table:** `COUNTROWS` on an empty table returns **`BLANK()`**, not `0`. To force the result to be a number, add `+ 0`.
- **`BLANK` in Boolean Expressions:** In modern versions of DAX, a logical expression will return `FALSE` instead of `BLANK()`.