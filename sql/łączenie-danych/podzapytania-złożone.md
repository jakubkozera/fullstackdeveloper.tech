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


(26 rows affected)



Total execution time: 00:00:00.023





<table><tr><th>SalesPerson</th><th>CategoryName</th><th>TotalSales</th></tr><tr><td>adventure-works\jae0</td><td>Bike Racks</td><td>304930,0209</td></tr><tr><td>adventure-works\jae0</td><td>Bottles and Cages</td><td>304321,8443</td></tr><tr><td>adventure-works\jae0</td><td>Bottom Brackets</td><td>358593,8916</td></tr><tr><td>adventure-works\jae0</td><td>Brakes</td><td>179384,0309</td></tr><tr><td>adventure-works\jae0</td><td>Caps</td><td>304321,8443</td></tr><tr><td>adventure-works\jae0</td><td>Chains</td><td>179296,9458</td></tr><tr><td>adventure-works\jae0</td><td>Cleaners</td><td>304321,8443</td></tr><tr><td>adventure-works\jae0</td><td>Cranksets</td><td>358593,8916</td></tr><tr><td>adventure-works\jae0</td><td>Derailleurs</td><td>287894,8994</td></tr><tr><td>adventure-works\jae0</td><td>Gloves</td><td>705326,2363</td></tr><tr><td>adventure-works\jae0</td><td>Handlebars</td><td>605057,0568</td></tr><tr><td>adventure-works\jae0</td><td>Helmets</td><td>1021563,4865</td></tr><tr><td>adventure-works\jae0</td><td>Hydration Packs</td><td>346774,4962</td></tr><tr><td>adventure-works\jae0</td><td>Jerseys</td><td>1728401,0293</td></tr><tr><td>adventure-works\jae0</td><td>Mountain Bikes</td><td>2424916,4433</td></tr><tr><td>adventure-works\jae0</td><td>Mountain Frames</td><td>2024985,1945</td></tr><tr><td>adventure-works\jae0</td><td>Pedals</td><td>1085088,4608</td></tr><tr><td>adventure-works\jae0</td><td>Road Bikes</td><td>2801161,5222</td></tr><tr><td>adventure-works\jae0</td><td>Road Frames</td><td>887229,4214</td></tr><tr><td>adventure-works\jae0</td><td>Saddles</td><td>681782,7449</td></tr><tr><td>adventure-works\jae0</td><td>Shorts</td><td>494218,4948</td></tr><tr><td>adventure-works\jae0</td><td>Socks</td><td>282544,4329</td></tr><tr><td>adventure-works\jae0</td><td>Tires and Tubes</td><td>206183,6312</td></tr><tr><td>adventure-works\jae0</td><td>Touring Bikes</td><td>3262654,0358</td></tr><tr><td>adventure-works\jae0</td><td>Touring Frames</td><td>910424,7602</td></tr><tr><td>adventure-works\jae0</td><td>Vests</td><td>609251,8652</td></tr></table>


