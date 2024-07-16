# `ORDER BY` - sortowanie wyników

Oprócz wybierania wyników czy ich filtrowania, w prosty sposób za pomocą SQL'a możemy też je sortować  

W języku SQL klauzula `ORDER BY` jest używana w zapytaniach `SELECT` do sortowania wyników według określonej kolumny lub kolumn. Pozwala to na uporządkowanie wyników w odpowiedniej kolejności przed ich prezentacją użytkownikowi.

Klauzula `ORDER BY` jest szczególnie przydatna, gdy chcemy, aby wyniki zapytania były wyświetlane w określonym porządku, na przykład alfabetycznie, numerycznie lub chronologicznie.

Składnia klauzuli `ORDER BY` jest prosta. Możemy podać jedną lub więcej kolumn, według których chcemy posortować wyniki, oraz kierunek sortowania (rosnąco lub malejąco).

Przykładowa składnia klauzuli `ORDER BY`:

```
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;

```

Gdzie:

- `column1`, `column2`, ... to nazwy kolumn, według których chcemy posortować wyniki.
- `table_name` to nazwa tabeli, z której pobieramy dane.
- `ASC` oznacza sortowanie rosnące (domyślne, jeśli nie jest podane).
- `DESC` oznacza sortowanie malejące.

Przykładowo, aby posortować wyniki zapytania SELECT tabeli Customers według kolumny LastName w porządku alfabetycznym rosnącym, użylibyśmy klauzuli ORDER BY w ten sposób:


```sql
SELECT *
FROM SalesLT.Customer
ORDER BY LastName 
```

Jeżeli mamy potrzebę sortowania więcej niż 1 kolumny, możemy to zrobić, przykładowo, w następujący sposób:




```sql
SELECT *
FROM SalesLT.Customer
ORDER BY LastName ASC, FirstName DESC;
```

W połączeniu z ograniczeniem zwracanych rezultatów przez `TOP 1` możemy zastosować zapytanie z `ORDER BY` w celu znalezienia największej wartości w kolumnie. W przypadku, gdy wartość jest unikalna, zapytanie zwróci jedną wartość. W przeciwnym przypadku zwróci jedną z wartości, które są największe.



Przykładowo, aby pobrać zamówienie z największą kwotą całkowitą, możemy użyć zapytania:






```sql
SELECT TOP 1 *
FROM [SalesLT].[SalesOrderHeader]
ORDER BY SubTotal DESC;
```

Klauzula ORDER BY może być również stosowana do sortowania wyników w oparciu o wyrażenia lub funkcje, a nie tylko o konkretne kolumny.





---



## Zadanie praktyczne:





Napisz zapytanie SQL, które wykonają:

1. Sortowanie szczegółów zamówienia (tabela `SalesLT.SalesOrderDetail`) według ilości zamówionej (`OrderQty`) w kolejności malejącej, zwracając informacje z kolumn `SalesOrderID`, `OrderQty` oraz `UnitPrice`, tylko dla zamówień, które mają ilość zamówionych produktów większą niż 5.:








```sql
SELECT SalesOrderId, OrderQty, UnitPrice
FROM SalesLT.SalesOrderDetail
WHERE OrderQty > 5
ORDER BY OrderQty DESC
```

2. Sortowanie zamówień (tabela: `SalesLT.SalesOrderHeader`) według daty zamówienia `OrderDate` w kolejności rosnącej, dodatkowo jeśli zamówienia mają tą samą datę to posortujemy je według ceny całkowitej `SubTotal` w kolejności malejącej.




```sql
SELECT *
FROM SalesLT.SalesOrderHeader
ORDER BY OrderDate ASC, SubTotal DESC
```

3. Sortowanie produktów (tabela `[SalesLT].[Product]`) po cenie `ListPrice`, w celu znalezienia i zwrócenia tylko najtańszego


```sql
SELECT TOP 1 *
FROM SalesLT.Product
ORDER BY ListPrice ASC
```



