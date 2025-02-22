
USE WideWorldImporters;

-- Exercise 1
WITH T AS (
    SELECT 
        YEAR(a.OrderDate) AS Year,
        SUM(b.Quantity * b.UnitPrice) AS IncomePerYear,
        MAX(MONTH(a.OrderDate)) AS NumberOfDistinctMonths
    FROM Sales.Orders a
    JOIN Sales.OrderLines b
        ON a.OrderID = b.OrderID
    JOIN Sales.Invoices c
        ON a.OrderID = c.OrderID
    GROUP BY YEAR(a.OrderDate)
), 
T1 AS (
    SELECT *, 
           CAST(IncomePerYear / NumberOfDistinctMonths * 12 AS money) AS YearlyLinearIncome
    FROM T
)
SELECT *,
       (YearlyLinearIncome / LAG(YearlyLinearIncome, 1) OVER (ORDER BY Year) - 1) * 100 AS GrowthRate
FROM T1;

GO

-- Exercise 2
WITH T AS (
    SELECT 
        YEAR(o.OrderDate) AS TheYear,
        DATEPART(Q, o.OrderDate) AS TheQuarter,
        c.CustomerName,
        SUM(il.UnitPrice * il.Quantity) AS IncomePerYear
    FROM Sales.Orders o
    JOIN Sales.Customers c
        ON c.CustomerID = o.CustomerID
    JOIN Sales.Invoices i
        ON o.OrderID = i.OrderID
    JOIN Sales.InvoiceLines il
        ON i.InvoiceID = il.InvoiceID
    GROUP BY YEAR(o.OrderDate), DATEPART(Q, o.OrderDate), c.CustomerName
), 
T1 AS (
    SELECT *, 
           DENSE_RANK() OVER (PARTITION BY TheYear, TheQuarter ORDER BY IncomePerYear DESC) AS DNR
    FROM T
)
SELECT *
FROM T1
WHERE DNR BETWEEN 1 AND 5;

GO

-- Exercise 3
WITH T AS (
    SELECT 
        a.StockItemID, 
        a.StockItemName, 
        SUM(b.ExtendedPrice - TaxAmount) AS TotalProfit
    FROM Warehouse.StockItems a
    JOIN Sales.InvoiceLines b
        ON a.StockItemID = b.StockItemID
    GROUP BY a.StockItemID, a.StockItemName
)
SELECT TOP 10 *
FROM T
ORDER BY TotalProfit DESC;

GO

-- Exercise 4
WITH CTE AS (
    SELECT 
        s.StockItemID, 
        s.StockItemName, 
        s.UnitPrice, 
        s.RecommendedRetailPrice,
        (s.RecommendedRetailPrice - s.UnitPrice) AS NominalProductProfit
    FROM Warehouse.StockItems s
)
SELECT 
    ROW_NUMBER() OVER (ORDER BY NominalProductProfit DESC) AS RN,
    *,
    DENSE_RANK() OVER (ORDER BY NominalProductProfit DESC) AS DNR
FROM CTE;

GO

-- Exercise 5
WITH CTE AS (
    SELECT 
        s.SupplierID,
        CONCAT_WS(' - ', s.SupplierID, s.SupplierName) AS SupplierDetails,
        CONCAT_WS(' ', i.StockItemID, i.StockItemName) AS ProductDetails
    FROM Purchasing.Suppliers s
    JOIN Warehouse.StockItems i
        ON s.SupplierID = i.SupplierID
)
SELECT 
    SupplierDetails,
    STRING_AGG(ProductDetails, ' /, ') AS ProductDetails
FROM CTE
GROUP BY SupplierDetails, SupplierID
ORDER BY SupplierID;

GO

-- Exercise 6
SELECT TOP 5 
    i.CustomerID, 
    ci.CityName, 
    c.CountryName, 
    c.Continent, 
    c.Region,
    FORMAT(SUM(il.ExtendedPrice), 'N2') AS TotalExtendedPrice
FROM Sales.Invoices i
JOIN Sales.InvoiceLines il
    ON i.InvoiceID = il.InvoiceID
JOIN Sales.Customers cu
    ON i.CustomerID = cu.CustomerID
JOIN Application.Cities ci
    ON cu.DeliveryCityID = ci.CityID
JOIN Application.StateProvinces s
    ON s.StateProvinceID = ci.StateProvinceID
JOIN Application.Countries c
    ON c.CountryID = s.CountryID
GROUP BY i.CustomerID, ci.CityName, c.CountryName, c.Continent, c.Region
ORDER BY SUM(il.ExtendedPrice) DESC;

GO

-- Exercise 7
WITH T AS (
    SELECT 
        YEAR(o.OrderDate) AS OrderYear,
        MONTH(o.OrderDate) AS OrderMonth,
        SUM(il.ExtendedPrice - il.TaxAmount) AS MonthlyTotal,
        COALESCE(MONTH(o.OrderDate), 13) AS SortOrder
    FROM Sales.Orders o
    JOIN Sales.Invoices i
        ON o.OrderID = i.OrderID
    JOIN Sales.InvoiceLines il
        ON il.InvoiceID = i.InvoiceID
    GROUP BY ROLLUP (YEAR(o.OrderDate), MONTH(o.OrderDate))
    HAVING NOT GROUPING(YEAR(o.OrderDate)) = 1
), 
T1 AS (
    SELECT 
        OrderYear,
        ISNULL(CAST(OrderMonth AS VARCHAR), 'Grand Total') AS OrderMonth,
        FORMAT(MonthlyTotal, 'N2') AS MonthlyTotal,
        FORMAT(SUM(MonthlyTotal) OVER (PARTITION BY OrderYear ORDER BY SortOrder), 'N2') AS Cumulative
    FROM T
)
SELECT 
    OrderYear, 
    OrderMonth, 
    MonthlyTotal,
    CASE 
        WHEN OrderMonth LIKE 'Grand Total' THEN MonthlyTotal
        ELSE Cumulative
    END AS CumulativeTotal
FROM T1
ORDER BY OrderYear;

GO

-- Exercise 8
SELECT *
FROM (
    SELECT 
        YEAR(o.OrderDate) AS OrderYear, 
        DATEPART(MM, o.OrderDate) AS OrderMonth, 
        o.OrderID
    FROM Sales.Orders o
) T
PIVOT (
    COUNT(OrderID) 
    FOR OrderYear IN ([2013], [2014], [2015], [2016])
) pvt
ORDER BY OrderMonth;

GO

-- Exercise 9
WITH T AS (
    SELECT 
        c.CustomerID, 
        c.CustomerName, 
        o.OrderDate,
        LAG(o.OrderDate) OVER (PARTITION BY c.CustomerID ORDER BY o.OrderDate) AS PreviousOrderDate
    FROM Sales.Customers c
    JOIN Sales.Orders o
        ON c.CustomerID = o.CustomerID
), 
T1 AS (
    SELECT 
        *, 
        DATEDIFF(DD, MAX(OrderDate) OVER (PARTITION BY CustomerID), MAX(OrderDate) OVER()) AS DaysSinceLastOrder,
        DATEDIFF(DD, PreviousOrderDate, OrderDate) AS DaysBetweenOrders
    FROM T
), 
T2 AS (
    SELECT 
        CustomerID, 
        CustomerName, 
        OrderDate, 
        PreviousOrderDate,
        DaysSinceLastOrder, 
        AVG(DaysBetweenOrders) OVER (PARTITION BY CustomerID) AS AvgDaysBetweenOrders
    FROM T1
)
SELECT *,
       CASE 
           WHEN DaysSinceLastOrder > (AvgDaysBetweenOrders * 2) THEN 'Potential Churm' 
           ELSE 'Active'
       END AS CustomerStatus
FROM T2;

GO

-- Exercise 10
WITH T AS (
    SELECT 
        cu.CustomerCategoryName,
        CASE
            WHEN c.CustomerName LIKE 'Tailspin%' THEN 'Tailspin' 
            WHEN c.CustomerName LIKE 'Wingtip%' THEN 'Wingtip'
            ELSE c.CustomerName
        END AS CustomerName
    FROM Sales.Customers c
    JOIN Sales.CustomerCategories cu
        ON c.CustomerCategoryID = cu.CustomerCategoryID
), 
T1 AS (
    SELECT 
        CustomerCategoryName, 
        COUNT(DISTINCT CustomerName) AS CustomerCOUNT
    FROM T
    GROUP BY CustomerCategoryName
), 
T2 AS (
    SELECT 
        CustomerCategoryName, 
        CustomerCOUNT, 
        SUM(CustomerCOUNT) OVER () AS TotalCustCount
    FROM T1
)
SELECT 
    CustomerCategoryName, 
    CustomerCOUNT, 
    TotalCustCount,
    CONCAT((CAST(CustomerCOUNT AS money) / TotalCustCount) * 100, '%') AS DistributionFactor
FROM T2
ORDER BY CustomerCategoryName;
