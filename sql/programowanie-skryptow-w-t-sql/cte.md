# CTE

CTE (Common Table Expressions) w MS SQL to tymczasowe zestawy wyników zdefiniowane w ramach zapytania, które mogą być używane przez inne lub to samo zapytanie. CTE są przydatne do podziału skomplikowanych zapytań na bardziej zrozumiałe i łatwiejsze do zarządzania fragmenty. Pozwalają one również na odwoływanie się do siebie nawzajem, co umożliwia tworzenie rekurencyjnych zapytań. 

CTE są definiowane za pomocą klauzuli `WITH` i mogą być używane w zapytaniach `SELECT`, `INSERT`, `UPDATE` i `DELETE`. Przykładowa składnia CTE wygląda następująco:

```
WITH CTE_Name AS (
    SELECT columns
    FROM table
    WHERE conditions
)
SELECT columns
FROM CTE_Name;

```

CTE można łączyć z innymi CTE lub zapytaniami, co pozwala na tworzenie bardziej złożonych zapytań. Poniżej przedstawiono kilka przykładów użycia CTE w MS SQL.

### 1\. Podstawowe użycie CTE

Przykład CTE wyciągający wszystkie książki wraz z informacjami o autorze i gatunku:


```sql
WITH BookDetails AS (
    SELECT
        b.Title,
        b.Description,
        b.PublicationDate,
        b.ISBN,
        a.FirstName + ' ' + a.LastName AS AuthorName,
        g.Name AS GenreName
    FROM Books b
    JOIN Authors a ON b.AuthorId = a.AuthorId
    JOIN Genres g ON b.GenreId = g.GenreId
)
SELECT GenreName, Title FROM BookDetails;
```


### 2\. Rekurencyjne CTE

Przykład CTE rekurencyjnego, który może być użyty do wyliczenia hierarchii kategorii:


```sql
WITH RecursiveCategoryCTE AS (

    -- Część ankoryczna (początkowa) CTE
    SELECT
        ProductCategoryID,
        ParentProductCategoryID,
        Name,
        CAST(Name AS NVARCHAR(MAX)) AS HierarchyPath,
        0 AS Level
    FROM
        SalesLT.ProductCategory
    WHERE
        ParentProductCategoryID IS NULL
    UNION ALL

    -- Część rekurencyjna CTE
    SELECT
        pc.ProductCategoryID,
        pc.ParentProductCategoryID,
        pc.Name,
        CAST(r.HierarchyPath + ' > ' + pc.Name AS NVARCHAR(MAX)),
        r.Level + 1
    FROM
        SalesLT.ProductCategory pc
    INNER JOIN
        RecursiveCategoryCTE r ON pc.ParentProductCategoryID = r.ProductCategoryID
)

-- Finalne zapytanie do wyświetlenia wyników
SELECT
    ProductCategoryID,
    ParentProductCategoryID,
    Name,
    HierarchyPath,
    Level
FROM
    RecursiveCategoryCTE
ORDER BY
    HierarchyPath;
```



### 3. Złożone zapytanie z użyciem CTE

Przykład CTE używanego do znalezienia użytkowników, którzy wypożyczyli książki o specyficznych warunkach:






```sql
WITH LoanedBooks AS (
    SELECT
        l.LoanId,
        l.UserId,
        l.CopyId,
        l.LoanDate,
        l.ReturnDate,
        b.Title,
        a.FirstName + ' ' + a.LastName AS AuthorName
    FROM Loans l
    JOIN Copies c ON l.CopyId = c.CopyId
    JOIN Books b ON c.BookId = b.BookId
    JOIN Authors a ON b.AuthorId = a.AuthorId
    WHERE b.PublicationDate > '1990-01-01'
),
UserDetails AS (
    SELECT
        u.UserId,
        u.Name,
        u.Surname,
        u.Email,
        u.PhoneNumber,
        a.City,
        a.Street,
        a.HouseNumber,
        a.Country
    FROM Users u
    JOIN Addresses a ON u.AddressId = a.AddressId
)
SELECT
    ud.Name,
    ud.Surname,
    ud.Email,
    lb.Title,
    lb.AuthorName,
    lb.LoanDate,
    lb.ReturnDate
FROM UserDetails ud
JOIN LoanedBooks lb ON ud.UserId = lb.UserId;
```



Oprócz rekursywnego CTE, zazwyczaj jest ono stosowane do dzielenia złożonych zapytań na mniejsze, bardziej czytelne części.

Zobaczmy jak przepisać jedno z poprzednich zapytań, na bardziej czytelne zapytanie z użyciem CTE.

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
-- Z CTE

WITH SalesPersonCategoryTotalSales AS (
    SELECT c.SalesPerson, pc.Name [CategoryName], SUM(soh.TotalDue) as TotalSales
    FROM SalesLT.Customer c 
    JOIN SalesLT.SalesOrderHeader soh on soh.CustomerID = c.CustomerID
    JOIN SalesLT.SalesOrderDetail sod on sod.SalesOrderID = soh.SalesOrderID
    JOIN SalesLT.Product p on p.ProductID = sod.ProductID
    JOIN SalesLT.ProductCategory pc on pc.ProductCategoryID = p.ProductCategoryID
    GROUP BY c.SalesPerson, pc.Name
)

SELECT *
FROM (
    SELECT CategoryName, MAX(TotalSales) TopTotalSales
    FROM SalesPersonCategoryTotalSales
    GROUP BY CategoryName
) SubOuter
JOIN SalesPersonCategoryTotalSales on SalesPersonCategoryTotalSales.CategoryName = SubOuter.CategoryName AND SalesPersonCategoryTotalSales.TotalSales = SubOuter.TopTotalSales
ORDER BY SalesPersonCategoryTotalSales.CategoryName

```

### Ograniczenia CTE

- Jeśli używasz rekursywnego CTE, to musisz uważać na to, aby rekursja była dobrze zdefiniowana i zakończona. W przeciwnym razie może wystąpić błąd przepełnienia stosu.
    
- CTE są zazwyczaj dostępne tylko w zakresie pojedynczego zapytania, co oznacza, że ​​nie można ich używać między wieloma zapytaniami w ramach tej samej transakcji.
    

Przykładowo, poniższe zapytanie zwróci błąd:


```sql
SELECT * FROM BookDetails

WITH BookDetails AS (
    SELECT
        b.Title,
        b.Description,
        b.PublicationDate,
        b.ISBN,
        a.FirstName + ' ' + a.LastName AS AuthorName,
        g.Name AS GenreName
    FROM Books b
    JOIN Authors a ON b.AuthorId = a.AuthorId
    JOIN Genres g ON b.GenreId = g.GenreId
)
SELECT TOP 5 * FROM Genres;
```


Co więcej samo CTE musi znajdować się na początku skryptu, albo zawsze musi być poprzedzone średnikiem.


```sql
SELECT TOP 5 * FROM Genres
WITH BookDetails AS (
    SELECT
        b.Title,
        b.Description,
        b.PublicationDate,
        b.ISBN,
        a.FirstName + ' ' + a.LastName AS AuthorName,
        g.Name AS GenreName
    FROM Books b
    JOIN Authors a ON b.AuthorId = a.AuthorId
    JOIN Genres g ON b.GenreId = g.GenreId
)
SELECT * FROM BookDetails;
```
