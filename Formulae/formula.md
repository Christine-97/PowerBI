<!DOCTYPE html>
<html lang="en">

 <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>   
<body>
<h1># PowerBI Formula </h1>


<h2><img src="https://drive.google.com/uc?export=download&id=1H_9MUHK9xMPUTtsVY8mjDs9lcVDIgyBU" width="22"> DAX formulas</h2>


&#9654; SUMX = Returns the sum of an expression evaluated for each row in a table. <br>
&#9654; SUM = Adds all the numbers in a column.


```
Sumx = SUMX(<table>, <expression>)
SUM(<column>)
```

SUMX & SUM Return value: A decimal number


------------------------------------------------------------------------------------------------------


<h2><img src="https://drive.google.com/uc?export=download&id=1H_9MUHK9xMPUTtsVY8mjDs9lcVDIgyBU" width="22">Role-playing dimension</h2>

<h3>USERELATIONSHIP</h3>
The expression calculates the total sales for August based on the shipping date.
<ul>
<b>SUM</b> - calculates the total Sales column from the Sales table<br>
<b>FILTER</b> - filters the values for August from the Month column of the Date table<br>
<b>USERELATIONSHIP</b> - overrides the table relationship to consider the shipping date instead of the order date, which is the default relationship.<br>
</ul>

&#9654; working with pre-established inactive  relations.

```
Syntax:
USERELATIONSHIP(<columnName1>,<columnName2>)

eg.
August Sales by Shipping date =
CALCULATE 
(
    SUM ( Sales[Sales Amount] ),
    FILTER ( 'Date', 'Date'[Month] = "August" ),
    USERELATIONSHIP ( Sales[Shipping Date].[Date] )
)

```

Return value: The function returns no value; the function only enables the indicated relationship for the duration of the calculation.

------------------------------------------------------------------------------------------------------

<h2><img src="https://drive.google.com/uc?export=download&id=1H_9MUHK9xMPUTtsVY8mjDs9lcVDIgyBU" width="22">Time-related dimension</h2>



<p>Time intelligence functions are a crucial element of data analysis. They can be used to perform calculations over different periods. They are particularly useful for trend analysis, forecasting, and performance comparison. Some of the most crucial functions that provide time intelligence output can be classified as follows: </p>

<ul>
&#8226; Time comparison functions: These functions compare one date or time to another. For instance, comparing total revenue with the revenue from the last quarter. </br>
&#8226; Aggregate functions: Aggregations show the year-to-date, month-to-date or anything similar. </br>
&#8226; Information functions: These provide snapshots of information, like a month-opening or year-end balance. These functions are especially important in financial management.</br>

</ul>


<h3>SAMEPERIODLASTYEAR</h3>
&#9654; SAMEPERIODLASTYEAR = Returns a table that contains a column of dates shifted one year back in time from the dates in the specified dates column, in the current context. <br>

```

Syntax:
SAMEPERIODLASTYEAR(<dates>)  

Example:
TOTALYTD(<expression>,<dates>[,<filter>][,<year_end_date>])

```

Return value: A single-column table of date values.


Remarks: The dates argument can be any of the following:
<ul>
&#8226; A reference to a date/time column, <br>
&#8226; A table expression that returns a single column of date/time values,<br>
&#8226; A Boolean expression that defines a single-column table of date/time values.<br>
&#8226; Constraints on Boolean expressions are described in the topic, CALCULATE.<br>
&#8226; The dates returned are the same as the dates returned by this equivalent formula: DATEADD(dates, -1, year)<br>
&#8226; This function is not supported for use in DirectQuery mode when used in calculated columns or row-level security (RLS) rules.<br>
</ul>


<h3>DATEADD</h3>

&#9654; DATEADD = Returns a table that contains a column of dates, shifted either forward or backward in time by the specified number of intervals from the dates in the current context. <br>

```
Syntax:
DATEADD(<dates>,<number_of_intervals>,<interval>)

Example:
DATEADD(DateTime[DateKey],-1,year)

```

Return value: A single-column table of date values.

Remarks: The dates argument can be any of the following:

<ul>
&#8226; A reference to a date/time column,<br>
&#8226; A table expression that returns a single column of date/time values,<br>
&#8226; A Boolean expression that defines a single-column table of date/time values.<br>
&#8226; If the number specified for number_of_intervals is positive, the dates in dates are moved forward in time; if the number is negative, the dates in dates are shifted back in time.<br>
&#8226; The interval parameter is an enumeration, not a set of strings; therefore values should not be enclosed in quotation marks. Also, the values: year, quarter, month, day should be spelled in full when using them.<br>
&#8226; The result table includes only dates that exist in the dates column.<br>
&#8226; If the dates in the current context do not form a contiguous interval, the function returns an error.<br>
&#8226; This function is not supported for use in DirectQuery mode when used in calculated columns or row-level security (RLS) rules.<br>
</ul>

-------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

Creating hierarchy


<h3>CALENDARAUTO Function</h3>

```
Tablename = CALENDARAUTO([fiscal_year_end_month])  

Example
In this example, the MinDate and MaxDate in the data model are July 1, 2010 and June 30, 2011.

CALENDARAUTO() will return all dates between January 1, 2010 and December 31, 2011.

CALENDARAUTO(3) will return all dates between April 1, 2010 and March 31, 2012.
```

<h3>NOTES</h3>

After using delimiter option in data transform, always use TRIM from format options (all in power query > TRANSFORM TAB)
-------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>



<b>
&#8226; is the HTML entity for a bullet point.<br>
    
&#9654; is the HTML entity for a right-pointing arrowhead.<br>

&#10003; is the HTML entity for a check mark.<br>
</b>

</body>
</html>


