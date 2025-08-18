# Power Over Filters
## The ultimate cheat sheet to control filters

---

-- Sample Dataset
-- Year | Product | Sales Amount | Quantity
-- 2024 | A       | 100          | 2
-- 2024 | B       | 200          | 3
-- 2025 | A       | 300          | 1
-- 2025 | B       | 400          | 4


-- 1. CALCULATE
Sales2025 = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    Sales[Year] = 2025
)
-- Explanation: Overrides filter context to only include Year = 2025
-- Output: 700 (300 + 400)


-- 2. CALCULATETABLE
SalesTable2025 = 
CALCULATETABLE(
    Sales,
    Sales[Year] = 2025
)
-- Explanation: Returns a table containing only rows for Year = 2025

-- Output Table: 
| Year | Product | Sales Amount | Quantity |
| ---- | ------- | ------------ | -------- |
| 2025 | A       | 300          | 1        |
| 2025 | B       | 400          | 4        |



-- 3. FILTER
HighSales = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    FILTER(Sales, Sales[Sales Amount] > 250)
)
-- Explanation: Keeps only rows where Sales Amount > 250
-- Output: 700 (300 + 400)


-- 4. ALL
AllSales = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    ALL(Sales)
)
-- Explanation: Removes all filters and sums entire table
-- Output: 1000 (100 + 200 + 300 + 400)


-- 5. REMOVEFILTERS
NoFilterSales = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    REMOVEFILTERS(Sales[Product])
)
-- Explanation: Removes filters on Product but keeps others like Year
-- Output (if Year slicer = 2025): 700 (A + B)


-- 6. KEEPFILTERS
KeepFilterExample = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    KEEPFILTERS(Sales[Year] = 2025)
)
-- Explanation: Adds Year = 2025 filter without removing existing filters
-- Output (if slicer already on Product A): 300 (only A in 2025)


-- 7. USERELATIONSHIP
SalesByShipDate = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    USERELATIONSHIP(Sales[ShipDate], Date[Date])
)
-- Explanation: Uses ShipDate instead of OrderDate for filtering
-- Output: Depends on Date table


-- 8. CROSSFILTER
CrossFilterExample = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    CROSSFILTER(Sales[CustomerID], Customers[CustomerID], BOTH)
)
-- Explanation: Makes filters flow both directions between Customers and Sales
-- Output: Depends on Customers table


-- 9. TREATAS
TreatAsExample = 
CALCULATE(
    SUM(Sales[Sales Amount]),
    TREATAS({2025}, Sales[Year])
)
-- Explanation: Applies a virtual filter as if Year = 2025 was selected
-- Output: 700

