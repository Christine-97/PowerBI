<!DOCTYPE html>
<html lang="en">

 <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>   
<body>
<h1># PowerBI </h1>


<h2><img src="https://drive.google.com/uc?export=download&id=1H_9MUHK9xMPUTtsVY8mjDs9lcVDIgyBU" width="22"> Write DAX formulas</h2>

Template to create a model calculation:

```
<Calculation name> = <DAX formula>
```

For example, the definition of the Ship Date calculated table that duplicates the Date table data is:
```
Ship Date = 'Date'
```

<div style="background-color: #f0f0f0; padding: 50px;">
A DAX formula consists of expressions that return a result. The result is either a table object or a scalar value. Calculated table formulas must return a table object; calculated column and measure formulas must return a scalar value (single value).

Formulas are assembled by using:
DAX functions </li>
<li>DAX operators</li>
<li>References to model objects</li>
<li>Constant values, like the number 24 or the literal text "FY" (abbreviation for fiscal year)</li>
<li>DAX variables</li>
<li>Whitespace</li>
</ul>
</br>
</div>

|💡 Tip: When you select a DAX function, it also provides you with a definition and description.Use IntelliSense to help you quickly build accurate formulas.🚀|
|------------------------------------------------------------------------------------------------------|


<h3>Table references</h3>

When you reference a table in a formula, officially, the table name is enclosed within single quotation marks. Single quotation marks can be omitted when both of the following conditions are true:

<ul>
<li>The table name does not include embedded spaces.</li>
<li>The table name isn't a reserved word that's used by DAX. All DAX function names and operators are reserved words. Date is a DAX function name, which explains why, when you are referencing a table named Date, that you must enclose it within single quotation marks.</li>
</ul>


<h3>Column references</h3>

When you reference a column in a formula, the column name must be enclosed within square brackets.

A table but not necessarily unique within the model, you can disambiguate the column reference by preceding it with its table name.
Disambiguated column is known as a fully qualified column. Some DAX functions require passing in fully qualified columns.


```
Revenue = SUM(Sales[Sales Amount])
```


<h3>Measure references</h3>

When you reference a measure in a formula, like column name references, the measure name must be enclosed within square brackets.

```
* Same table column reference:

Profit = [Revenue] - [Cost]

______________________________________________________________________

* Different table column reference:

AverageSalesPerCustomer = 
    DIVIDE(
        SUM(Sales[SalesAmount]),
        COUNTROWS(Customers)
    )

```
| 💡 Tip: How to Reference Columns and Measures within the Context of Data Modeling or Analytical Work? |
|------------------------------------------------------------------------------------------------------|
| **1. Measures and Tables:** Measures are mentioned as "model-level objects," part of the overall data model or analytical framework. While measures are assigned to a specific home table for organizational purposes, this assignment is described as a "cosmetic relationship," primarily for organizational or visual purposes in tools like the Fields pane. |
| **2. Column References with Table Names:** The statement recommends that when referencing a column, it's a good practice to precede the column reference with its table name. This is common in data modeling to avoid ambiguity when there are columns with the same name in different tables. For example: TableName.ColumnName. |
| **3. Measures References without Table Names:** In contrast, the statement advises against preceding a measure reference with its table name. Unlike columns, measures are model-level objects, and the guidance suggests that it's unnecessary or not recommended to include the table name when referencing a measure. For example: MeasureName rather than TableName.MeasureName. | 

| **In Summary, the recommendation is to maintain consistency in referencing conventions:** |
|-------------------------------------------------------------------------------------------|
| - Prefer referencing columns with their table names for clarity and to avoid ambiguity.     |
| - Avoid including the table name when referencing measures, as they are considered model-level objects, and the table reference is deemed unnecessary in this context. |

<h3>DAX variables</h3>

Formulas can declare DAX variables to store results.



<h3>Whitespace</h3>

Whitespace refers to characters that you can use to format your formulas in a way that's quick and simple to understand. Whitespace characters include:

<ul>
<li>Spaces</li>
<li>Tabs</li>
<li>Carriage returns</li>
</ul>

| 💡 Tip: Consider the following recommendations: |
|-------------------------------------------------|
| **1. Use Spaces Between Operators:** Ensure readability by including spaces between operators in your formulas. For example, write `a + b` instead of `a+b`. |
| **2. Use Tabs to Indent Nested Function Calls:** When dealing with nested function calls, use tabs for indentation to enhance clarity in your code structure. |
| **3. Use Carriage Returns to Separate Function Arguments:** Especially when function calls or arguments are too long to fit on a single line, use carriage returns for better formatting. In the formula bar, press Shift+Enter to enter a carriage return; pressing Enter alone commits your formula. This makes troubleshooting easier, especially when dealing with missing parentheses. |
| **4. Err on the Side of Too Much Whitespace:** When formatting your code, prioritize having more whitespace than too little. This helps in improving code readability and makes it easier to maintain and troubleshoot. |


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<h4>Revenue YoY % measure</h4>


```
Revenue YoY % =
DIVIDE(
    [Revenue]
        - CALCULATE(
            [Revenue],
            SAMEPERIODLASTYEAR('Date'[Date])
    ),
    CALCULATE(
        [Revenue],
        SAMEPERIODLASTYEAR('Date'[Date])
    )
)
```

<b> Here's an explanation for each part:
<ul>
&#8226;  [Revenue]: This is assumed to be a measure or column representing the revenue for the current period.<br><br>

&#8226;  CALCULATE([Revenue], SAMEPERIODLASTYEAR('Date'[Date])): This part calculates the revenue for the same period in the previous year using the SAMEPERIODLASTYEAR function. 
            The CALCULATE function modifies the filter context, allowing you to evaluate the [Revenue] measure in a different time period.<br><br>

&#8226;  [Revenue] - ...: This subtracts the revenue for the previous year from the revenue for the current year.<br><br>

&#8226;  DIVIDE(..., ...): The DIVIDE function is used to calculate the percentage change. It takes two arguments: the numerator (the difference between current and previous revenue) and the denominator (the revenue for the previous year).<br><br>

</ul>
Final Result: The formula calculates the percentage change in revenue from the previous year to the current year.</b><br>

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<h3>Data Types Reference</h3>

&#10003; Semantic model columns have a set data type, which ensures that all column values conform to that data type. <br>
&#10003; Column data types are defined in Power Query. <br>
&#10003; In the case of calculated columns and measure data, it's inferred from the formula. <br>

&#9733; Model data types aren't the same as DAX data types, though a direct relationship exists between them.


<table>
    <tr>
        <th>Model Data Type</th>
        <th>DAX Data Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Whole number</td>
        <td>64-bit integer</td>
        <td>-263 through 263-1</td>
    </tr>
    <tr>
        <td>Decimal number</td>
        <td>64-bit real</td>
        <td>Negative: -1.79 x 10<sup>308</sup> through -2.23 x 10<sup>-308</sup> - zero (0) - positive: 2.23 x 10<sup>-308</sup> through 1.79 x 10<sup>308</sup> - Limited to 17 decimal digits</td>
    </tr>
    <tr>
        <td>Boolean</td>
        <td>Boolean</td>
        <td>TRUE or FALSE</td>
    </tr>
    <tr>
        <td>Text</td>
        <td>String</td>
        <td>Unicode character string</td>
    </tr>
    <tr>
        <td>Date</td>
        <td>Date/time</td>
        <td>Valid dates are all dates after January 1, 1900</td>
    </tr>
    <tr>
        <td>Currency</td>
        <td>Currency</td>
        <td>-9.22 x 10<sup>14</sup> through 9.22 x 10<sup>14</sup> - limited to four decimal digits of fixed precision</td>
    </tr>
    <tr>
        <td>N/A</td>
        <td>BLANK</td>
        <td>In some cases, it's the equivalent of a database (SQL) NULL</td>
    </tr>
</table>

| 💡 Tip: BLANK Data Type  <br> <ul> 1. DAX uses BLANK for both database NULL and for blank cells in Excel. <br>   2. BLANK doesn't mean zero. Two DAX functions are related to the BLANK data type: the BLANK DAX function returns BLANK, while the ISBLANK DAX function tests whether an expression evaluates to BLANK. </ul>|
|:------------------------------------------------------------------------|

------------------------------------------------------------------------------------------------------

<h2><img src="https://drive.google.com/uc?export=download&id=12VWb9dFYI3mGJ0MH2xWP5bL3IR-3pHeg" width="21"> Work with DAX functions</h2>

|💡 Tip: A function argument is optional when documentation shows it enclosed within square brackets.|
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

Many functions exist that you won't find in Excel because they're specific to data modeling:

<ul>
&#8226;  Relationship navigation functions<br>
&#8226;  Filter context modification functions<br>
&#8226;  Iterator functions<br>
&#8226;  Time intelligence functions<br>
&#8226;  Path functions<br>
</ul>



|💡 Tip: To search for documentation that is related to a <a href="https://docs.microsoft.com/en-us/dax/countrows-function-dax">DAX functions</a>, in a web search, enter the keyword DAX followed by the function name.|
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

<h3><p>Functions that originate from Excel</p></h3>

The IF DAX function tests whether a condition that's provided as the first argument is met. It returns one value if the condition is TRUE and returns the other value if the condition is FALSE. If logical_test evaluates to FALSE and value_if_false isn't provided, the function will return BLANK.

The function's syntax is:
```
IF(<logical_test>, <value_if_true>[, <value_if_false>])
```

<h3>Functions that don't originate from Excel</h3>

 Two useful DAX functions that aren't specific to modeling and that don't originate from Excel are DISTINCTCOUNT and DIVIDE.

&#9654; DISTINCTCOUNT function : DAX function to count the number of distinct values in a column.

&#9654; You must pass in numerator and denominator expressions. Optionally, you can pass in a value that represents an alternate result. 

The DIVIDE function's syntax is:
```
DIVIDE(<numerator>, <denominator>[, <alternate_result>])
```
------------------------------------------------------------------------------------------------------

<h2><img src="https://drive.google.com/uc?export=download&id=1Y6OfjytssW-3xQYcFr-dP7Fj_nnufyS6" width="21"> Use DAX operators</h2>


Your DAX formulas can use operators to create expressions that perform arithmetic calculations, compare values, work with strings, or test conditions.

<h3>Arithmetic operators</h3>

The following table lists the arithmetic operators.

| Operator | Description      |
|----------|------------------|
| +        | Addition         |
| -        | Subtraction      |
| *        | Multiplication   |
| /        | Division         |
| ^        | Exponentiation   |


<h3>Comparison operators</h3>

The following table lists the comparison operators, which are used to compare two values. The result is either TRUE or FALSE.

| Operator | Description                 |
|----------|-----------------------------|
| =        | Equal to                    |
| ==       | Strict equal to             |
| >        | Greater than                |
| <        | Less than                   |
| >=       | Greater than or equal to    |
| <=       | Less than or equal to       |
| <>       | Not equal to                |


|💡 Tip: This statement is explaining the behavior of comparison operators in the context of a data analysis or programming language, particularly in scenarios where there is a concept of a special placeholder or null value, often represented as "BLANK."|
|-----------------------|
|Let's break down the key points:<br>1. Comparison Operators:<br><ul>Comparison operators are used to compare values in programming or data analysis languages.<br><br>Examples of comparison operators include =, ==, >, <, >=, <=, and <> (not equal to).<br><br><br>2. Strict Equal To (==):<br>The statement notes that the strict equal to operator (==) behaves differently from other comparison operators.<br>It checks for equality of both value and data type.<br><br><br>3. Treatment of BLANK:<br> BLANK is considered as equal to certain values, including zero, an empty string (""), the date December 30, 1899, or FALSE.<br>When using comparison operators like =, >, <, >=, <=, or <>, BLANK is treated as equal to these specific values.<br><br><br>4. Example with [Revenue] = 0:<br>The statement provides an example: [Revenue] = 0 will be TRUE when the value of [Revenue] is either zero or BLANK.<br>In other words, if the value of [Revenue] is zero or if it is BLANK, the expression evaluates to TRUE.<br><br><br>5. Difference with [Revenue] == 0:<br>The statement contrasts this with [Revenue] == 0, which is TRUE only when the value of [Revenue] is zero.<br>In the strict equal to comparison (==), BLANK is not considered equal to zero.<br> </ul>|

|***In summary, the behavior described highlights how certain comparison operators treat BLANK as equal to specific values, while the strict equal to operator checks for both value and data type, resulting in a more precise comparison. This understanding is crucial when working with data that may contain null or special values.|
|-------------|                                                                                                                                                                                                                                                                          

<h3>Text concatenation operator</h3>

Use the ampersand (&) character to connect, or concatenate, two text values to produce one continuous text value.

```
Model Color = 'Product'[Model] & "-" & 'Product'[Color]
```

<h3>Logical operators</h3>

Use logical operators to combine expressions that produce a single result. The following table lists all logical operators.


| Operator | Description |
|----------|-------------|
| &&       | Creates an AND condition between two expressions where each has a Boolean result. If both expressions return TRUE, the combination of the expressions also returns TRUE; otherwise, the combination returns FALSE. |
| \|\| (double pipe) | Creates an OR condition between two logical expressions. If either expression returns TRUE, the result is TRUE; only when both expressions are FALSE is the result FALSE. |
| IN       | Creates a logical OR condition between each row that is being compared to a table. Note: The table constructor syntax uses braces. |
| NOT      | Inverts the state of a Boolean expression (FALSE to TRUE, and vice versa). |

```
An example that uses the IN logical operator:

ANZ Revenue =
CALCULATE(
    [Revenue],
    Customer[Country-Region] IN {
        "Australia",
        "New Zealand"
    }
)
```
------------------------------------------------------------------------------------------------------

#Exercise: Adding a calculated table and column

#Step 1: Download and Load Data
#Step 2: Remove all duplicate values and set the relationships between the tables.

  To eliminate all duplicate data, access the Power Query editor, right-click on the SalesOrderNumber columns, and select Remove duplicates from the drop-down menu.


#Step 3: Create a calculated table.

Access the Model view in the calculations group to create a new table. Select New table. Copy and paste the following DAX code into the formula bar:


- ADDCOLUMNS: Adds calculated columns to the given table or table expression. In this instance, the Sales table is the main table to which you need to add two more columns, one from the Date table and one from the Product table.

- Year and Color in double quotes are the names of the new columns to be added in the new calculated table.

- RELATED: Returns a related value from another table. In this case, Product color values from the Product table and Year information from the Date table.

```
Yearly Sales by color =
ADDCOLUMNS (
Sales,
"Year", RELATED ( 'Date'[Year]),
"Color", RELATED ( Products[Color]))
```
#Step 4: Create calculated columns.

To create a new column, select the Date table from the Data pane on the right side of Power BI interface. Access Model view in the Calculations group and select New column. Copy and paste the following DAX code into the formula bar:

- QUARTER: Returns each quarter as a number from the Date column.

- Date in single quotes is the table, and Date in square brackets is the column within the table.

```
Qtr = QUARTER('Date'[Date])
```

Select the Date table from the Data pane on the right side of Power BI interface. Access Model view in the Calculations group and select New column. Copy and paste the following DAX code into the formula bar:

-LEFT: Returns the specified number of characters from the start of a text string.

-Date in single quotes is the table to be referenced, and Month in square brackets is the column name. The number 3 specifies the number of characters in the short month column.

```
Month =LEFT ( 'Date'[Month], 3 )
```

To create a new column, select the Product table from the Data pane on the right side of Power BI interface. Access Model view in the calculations group. Then select New column to expand the formula bar. Copy and paste the following DAX code into the formula bar:

- RELATED here is the same as referencing a column from another table.

```
Product Color = RELATED ( Products[Color] )
```


<b>
&#8226; is the HTML entity for a bullet point.<br>
    
&#9654; is the HTML entity for a right-pointing arrowhead.<br>

&#10003; is the HTML entity for a check mark.<br>
</b>

</body>
</html>

