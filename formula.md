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
    USERELATIONSHIP ( Sales[Shipping Date], 'Date'[Date] )
)

```

Return value: The function returns no value; the function only enables the indicated relationship for the duration of the calculation.

------------------------------------------------------------------------------------------------------

<h2><img src="https://drive.google.com/uc?export=download&id=1H_9MUHK9xMPUTtsVY8mjDs9lcVDIgyBU" width="22">Time-related dimension</h2>

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
------------------------------------------------------------------------------------------------------


<b>
&#8226; is the HTML entity for a bullet point.<br>
    
&#9654; is the HTML entity for a right-pointing arrowhead.<br>

&#10003; is the HTML entity for a check mark.<br>
</b>

</body>
</html>


