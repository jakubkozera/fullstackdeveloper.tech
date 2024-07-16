# Funkcja `ROW_NUMBER()`

Funkcja `ROW_NUMBER()` zwraca numer wiersza w wynikowym zbiorze danych. Funkcja ta jest często używana w połączeniu z `PARTITION BY` w celu przypisania numeru wiersza w ramach grupy, jak i `ORDER BY` w celu uporządkowania wyników.

### Składnia

```
ROW_NUMBER() OVER (PARTITION BY column1, column2,... ORDER BY column1, column2,...)

```

### Przykład

Rozważmy poniższe zapytanie, które zwraca informacje o klientach, ich sprzedawcach i kwotach sprzedaży.


```sql
SELECT c.SalesPerson, c.CustomerID, soh.SubTotal
FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
```

Żeby z tych danych, zwrócić tylko np. 3 największych klientów, dla każdego sprzedawcy z osobna, możemy najpierw użyć funkcji `ROW_NUMBER()` w celu przypisania numeru do każdego wiersza w grupie sprzedawcy, posortowanego malejąco według wartości sprzedaży. 






```sql
SELECT c.SalesPerson, c.CustomerID, soh.SubTotal, 
    ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank
FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
```

Następnie, wybieramy tylko te wiersze, które mają numer mniejszy lub równy 3.


```sql
SELECT * 
FROM (
    SELECT c.SalesPerson, c.CustomerID, soh.SubTotal, ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank
    FROM SalesLT.[SalesOrderHeader] soh
    JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID) ranked
WHERE TopCustomerRank <= 3
```

W ten sposób, byliśmy w stanie przefiltrować tylko tych klientów, którzy na podstawie 'rankingu' pod kątem wielkości zamówienia u konkretnego sprzedawcy, byli w top 3.

### `ROW_NUMBER` w paginacji rezultatów

W róźnego rodzaju aplikacjach, często potrzebujemy wyświetlić dane w sposób paginowany, po to, aby do klienta nie zwracać wszystkich danych na raz, co mogłoby spowodować przeciążenie serwera. W takich przypadkach przydatne jest wykorzystanie funkcji `ROW_NUMBER` w celu numerowania rekordów w wynikowym zbiorze danych - które następnie możemy wybrać z odpowiedniej 'strony' (np. 10 rekordów na stronę).

Przykładowo, aby zwrócić dane z tabeli `SalesLT.SalesOrderHeader` w sposób paginowany, możemy najpierw wykorzystać funkcję `ROW_NUMBER` w celu numerowania rekordów, a następnie wybrać odpowiednie rekordy z odpowiedniej strony.


```sql
    SELECT *, ROW_NUMBER() OVER(ORDER BY SalesOrderID) AS RowNumber
    FROM SalesLT.SalesOrderHeader
```

Mając dane oznaczone w ten sposób, możemy tą informacje wykorzystać, aby pobrać wyniki z drugiej strony


```sql
DECLARE @PageSize INT = 10;
DECLARE @PageNumber INT = 3;
SELECT *
FROM (
    SELECT 
        *,
        ROW_NUMBER() OVER(ORDER BY SubTotal) AS RowNumber
    FROM 
        SalesLT.SalesOrderHeader
) AS RowNumberedResults
WHERE 
    RowNumber BETWEEN (@PageNumber - 1) * @PageSize + 1 AND @PageNumber * @PageSize;
```


W powyższym przykładzie, zwracamy 10 rekordów z tabeli `SalesLT.SalesOrderHeader` zaczynając od 11 rekordu (strona 2, 10 rekordów na stronę).



Jeśli klient aplikacji, miałby możliwość sortowania wyników paginacji, to musimy pamiętać o tym, aby odpowiednio sortować dane wewnątrz `OVER(ORDER BY ..)`
