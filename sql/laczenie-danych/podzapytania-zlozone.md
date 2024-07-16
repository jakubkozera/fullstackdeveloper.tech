Znajdź sprzedawców, którzy zrobili największe obroty (`TotalDue` z tabeli `SalesOrderHeader`) w danej kategorii produktów.






```sql
SELECT c.SalesPerson, pc.Name [CategoryName], SUM(soh.TotalDue) as TotalSales
FROM SalesLT.Customer c 
JOIN SalesLT.SalesOrderHeader soh on soh.CustomerID = c.CustomerID
JOIN SalesLT.SalesOrderDetail sod on sod.SalesOrderID = soh.SalesOrderID
JOIN SalesLT.Product p on p.ProductID = sod.ProductID
JOIN SalesLT.ProductCategory pc on pc.ProductCategoryID = p.ProductCategoryID
GROUP BY c.SalesPerson, pc.Name
```


```sql
SELECT SubOuter2.*
FROM (
    SELECT CategoryName, MAX(TotalSales) TopTotalSales
    FROM (SELECT c.SalesPerson, pc.Name [CategoryName], SUM(soh.TotalDue) as TotalSales
        FROM SalesLT.Customer c 
        JOIN SalesLT.SalesOrderHeader soh on soh.CustomerID = c.CustomerID
        JOIN SalesLT.SalesOrderDetail sod on sod.SalesOrderID = soh.SalesOrderID
        JOIN SalesLT.Product p on p.ProductID = sod.ProductID
        JOIN SalesLT.ProductCategory pc on pc.ProductCategoryID = p.ProductCategoryID
        GROUP BY c.SalesPerson, pc.Name) SubInner
    GROUP BY CategoryName
) SubOuter
JOIN (
    SELECT c.SalesPerson, pc.Name [CategoryName], SUM(soh.TotalDue) as TotalSales
    FROM SalesLT.Customer c 
    JOIN SalesLT.SalesOrderHeader soh on soh.CustomerID = c.CustomerID
    JOIN SalesLT.SalesOrderDetail sod on sod.SalesOrderID = soh.SalesOrderID
    JOIN SalesLT.Product p on p.ProductID = sod.ProductID
    JOIN SalesLT.ProductCategory pc on pc.ProductCategoryID = p.ProductCategoryID
    GROUP BY c.SalesPerson, pc.Name
) SubOuter2 on SubOuter2.CategoryName = SubOuter.CategoryName AND SubOuter2.TotalSales = SubOuter.TopTotalSales
ORDER BY CategoryName
```


```sql
SELECT *
FROM (SELECT c.SalesPerson, pc.Name [CategoryName], SUM(soh.TotalDue) as TotalSales
    FROM SalesLT.Customer c 
    JOIN SalesLT.SalesOrderHeader soh on soh.CustomerID = c.CustomerID
    JOIN SalesLT.SalesOrderDetail sod on sod.SalesOrderID = soh.SalesOrderID
    JOIN SalesLT.Product p on p.ProductID = sod.ProductID
    JOIN SalesLT.ProductCategory pc on pc.ProductCategoryID = p.ProductCategoryID
    GROUP BY c.SalesPerson, pc.Name) SubOuter
WHERE SubOuter.TotalSales = (SELECT MAX(TotalSales)
                            FROM (SELECT c.SalesPerson, pc.Name [CategoryName], SUM(soh.TotalDue) as TotalSales
                            FROM SalesLT.Customer c 
                            JOIN SalesLT.SalesOrderHeader soh on soh.CustomerID = c.CustomerID
                            JOIN SalesLT.SalesOrderDetail sod on sod.SalesOrderID = soh.SalesOrderID
                            JOIN SalesLT.Product p on p.ProductID = sod.ProductID
                            JOIN SalesLT.ProductCategory pc on pc.ProductCategoryID = p.ProductCategoryID
                            GROUP BY c.SalesPerson, pc.Name) SubInner
                            WHERE SubOuter.CategoryName = SubInner.CategoryName
                            )
ORDER BY CategoryName
```

