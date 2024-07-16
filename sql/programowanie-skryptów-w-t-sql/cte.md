## CTE

CTE (Common Table Expressions) w MS SQL to tymczasowe zestawy wyników zdefiniowane w ramach zapytania, które mogą być używane przez inne lub to <span style="color: var(--vscode-foreground);">samo</span> <span style="color: var(--vscode-foreground);">zapytanie. CTE są przydatne do podziału skomplikowanych zapytań na bardziej zrozumiałe i łatwiejsze do zarządzania fragmenty. Pozwalają one również na odwoływanie się do siebie nawzajem, co umożliwia tworzenie rekurencyjnych zapytań.</span>

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


(10 rows affected)



Total execution time: 00:00:00.011





<table><tr><th>GenreName</th><th>Title</th></tr><tr><td>Fantasy</td><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td></tr><tr><td>Fantasy</td><td>Harry Potter and the Chamber of Secrets - Special Edition</td></tr><tr><td>Fiction</td><td>The Great Gatsby</td></tr><tr><td>Romance</td><td>Pride and Prejudice</td></tr><tr><td>Drama</td><td>Les Misérables</td></tr><tr><td>Fiction</td><td>Norwegian Wood</td></tr><tr><td>Fiction</td><td>1984</td></tr><tr><td>Horror</td><td>The Shining</td></tr><tr><td>Fantasy</td><td>Harry Potter and the Order of the Phoenix - Special Edition</td></tr><tr><td>Fantasy</td><td>Harry Potter and the Half-Blood Prince - Special Edition</td></tr></table>



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


(3 rows affected)



Total execution time: 00:00:00.014





<table><tr><th>Name</th><th>Surname</th><th>Email</th><th>Title</th><th>AuthorName</th><th>LoanDate</th><th>ReturnDate</th></tr><tr><td>Michael</td><td>Brown</td><td>michael.brown@example.com</td><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td><td>Joanne Rowling</td><td>2021-01-01 00:00:00.0000000</td><td>NULL</td></tr><tr><td>Michael</td><td>Brown</td><td>michael.brown@example.com</td><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>Joanne Rowling</td><td>2024-04-29 10:00:00.0000000</td><td>NULL</td></tr><tr><td>Emma</td><td>Jones</td><td>emma@example.com</td><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>Joanne Rowling</td><td>2024-05-04 15:00:00.0000000</td><td>NULL</td></tr></table>



  

Oprócz rekursywnego CTE, zazwyczaj jest ono stosowane do dzielenia złożonych zapytań na mniejsze, bardziej czytelne części.

Zobaczmy jak przepisać jedno z poprzednich zapytań, na bardziej czytelne zapytanie z użyciem CTE.

```
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


(10 rows affected)



(5 rows affected)



Total execution time: 00:00:00.006





<table><tr><th>Title</th><th>Description</th><th>PublicationDate</th><th>ISBN</th><th>AuthorName</th><th>GenreName</th></tr><tr><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td><td>First book in the series</td><td>1997-06-26</td><td>9780747532743</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>The second book in the Harry Potter series</td><td>1998-07-02</td><td>9780439064866</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>The Great Gatsby</td><td>A classic American novel</td><td>1925-04-10</td><td>9780743273565</td><td>John Smith</td><td>Fiction</td></tr><tr><td>Pride and Prejudice</td><td>A romantic novel by Jane Austen</td><td>1813-01-28</td><td>9780141439518</td><td>Emma Johnson</td><td>Romance</td></tr><tr><td>Les Misérables</td><td>Victor Hugo&#39;s masterpiece</td><td>1862-03-15</td><td>9780140444308</td><td>Jean Dupont</td><td>Drama</td></tr><tr><td>Norwegian Wood</td><td>A novel by Haruki Murakami</td><td>1987-08-04</td><td>9780099543793</td><td>Kenji Tanaka</td><td>Fiction</td></tr><tr><td>1984</td><td>A dystopian novel by George Orwell</td><td>1949-06-08</td><td>9780451524935</td><td>George Orwell</td><td>Fiction</td></tr><tr><td>The Shining</td><td>A horror novel by Stephen King</td><td>1977-01-28</td><td>9780385121675</td><td>Stephen King</td><td>Horror</td></tr><tr><td>Harry Potter and the Order of the Phoenix - Special Edition</td><td>The fifth book in the Harry Potter series</td><td>2003-06-21</td><td>9780439358071</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>Harry Potter and the Half-Blood Prince - Special Edition</td><td>The sixth book in the Harry Potter series</td><td>2005-07-16</td><td>9780439784542</td><td>Joanne Rowling</td><td>Fantasy</td></tr></table>






<table><tr><th>GenreId</th><th>Name</th></tr><tr><td>1</td><td>Fantasy</td></tr><tr><td>443</td><td>Fiction</td></tr><tr><td>444</td><td>Science Fiction</td></tr><tr><td>445</td><td>Romance</td></tr><tr><td>447</td><td>Thriller</td></tr></table>



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


(5 rows affected)



(10 rows affected)



Total execution time: 00:00:00.008





<table><tr><th>GenreId</th><th>Name</th></tr><tr><td>1</td><td>Fantasy</td></tr><tr><td>443</td><td>Fiction</td></tr><tr><td>444</td><td>Science Fiction</td></tr><tr><td>445</td><td>Romance</td></tr><tr><td>447</td><td>Thriller</td></tr></table>






<table><tr><th>Title</th><th>Description</th><th>PublicationDate</th><th>ISBN</th><th>AuthorName</th><th>GenreName</th></tr><tr><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td><td>First book in the series</td><td>1997-06-26</td><td>9780747532743</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>The second book in the Harry Potter series</td><td>1998-07-02</td><td>9780439064866</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>The Great Gatsby</td><td>A classic American novel</td><td>1925-04-10</td><td>9780743273565</td><td>John Smith</td><td>Fiction</td></tr><tr><td>Pride and Prejudice</td><td>A romantic novel by Jane Austen</td><td>1813-01-28</td><td>9780141439518</td><td>Emma Johnson</td><td>Romance</td></tr><tr><td>Les Misérables</td><td>Victor Hugo&#39;s masterpiece</td><td>1862-03-15</td><td>9780140444308</td><td>Jean Dupont</td><td>Drama</td></tr><tr><td>Norwegian Wood</td><td>A novel by Haruki Murakami</td><td>1987-08-04</td><td>9780099543793</td><td>Kenji Tanaka</td><td>Fiction</td></tr><tr><td>1984</td><td>A dystopian novel by George Orwell</td><td>1949-06-08</td><td>9780451524935</td><td>George Orwell</td><td>Fiction</td></tr><tr><td>The Shining</td><td>A horror novel by Stephen King</td><td>1977-01-28</td><td>9780385121675</td><td>Stephen King</td><td>Horror</td></tr><tr><td>Harry Potter and the Order of the Phoenix - Special Edition</td><td>The fifth book in the Harry Potter series</td><td>2003-06-21</td><td>9780439358071</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>Harry Potter and the Half-Blood Prince - Special Edition</td><td>The sixth book in the Harry Potter series</td><td>2005-07-16</td><td>9780439784542</td><td>Joanne Rowling</td><td>Fantasy</td></tr></table>


