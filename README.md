<h1># PowerBI </h1>


<h2>Write DAX formulas</h2>

Template to create a model calculation:

```
<Calculation name> = <DAX formula>
```

For example, the definition of the Ship Date calculated table that duplicates the Date table data is:
```
Ship Date = 'Date'
```

A DAX formula consists of expressions that return a result. The result is either a table object or a scalar value. Calculated table formulas must return a table object; calculated column and measure formulas must return a scalar value (single value).

Formulas are assembled by using:
DAX functions </li>
<li>DAX operators</li>
<li>References to model objects</li>
<li>Constant values, like the number 24 or the literal text "FY" (abbreviation for fiscal year)</li>
<li>DAX variables</li>
<li>Whitespace</li>
</ul>



```
💡 Tip: When you select a DAX function, it also provides you with a definition and description.Use IntelliSense to help you quickly build accurate formulas.🚀
```


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

