# HAVING - Filtrowanie grup

Podobnie jak wiersze w tabeli, możemy również filtrować kolumny w wynikach 'zapytania z grupowaniem'. W tym celu używamy klauzuli `HAVING`. Klauzula `HAVING` działa podobnie jak klauzula `WHERE`, ale jest używana do filtrowania wyników grupowanych. Przykładowa składnia klauzuli `HAVING` wygląda następująco:

```
SELECT column_name, aggregate_function(column_name2)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name2) operator value;

```

Zauważ, że jednocześnie możemy używać klauzuli `WHERE` i `HAVING` w jednym zapytaniu. Klauzula `WHERE` jest używana do filtrowania wierszy przed grupowaniem, a klauzula `HAVING` jest używana do filtrowania grup po grupowaniu.

Przykładowo, chcąc uzyskać informację o tym, które kategorie produktów, mają conajmniej 10 produktów, możemy użyć zapytania:


```sql
SELECT ProductCategoryID, COUNT(*) AS NumberOfProducts
FROM SalesLT.Product
GROUP BY ProductCategoryID
HAVING COUNT(*) > 10;
```

Istotne jest aby w klauzuli `HAVING` umieszczać funkcje agregujące, a nie aliasy kolumn.

Użycie aliasu, w klauzuli `HAVING` spowoduje błąd.






```sql
SELECT ProductCategoryID, COUNT(*) AS NumberOfProducts
FROM SalesLT.Product
GROUP BY ProductCategoryID
HAVING NumberOfProducts > 10;
```

## Zadanie praktyczne

1. Znajdź wszystkich sprzedawców `SalesPerson`, którzy obslugują co najmniej 100 klientów


<details>
<summary>Rozwiązanie</summary>

```sql
SELECT SalesPerson, COUNT(*) CustomerCount
FROM SalesLT.Customer
GROUP BY SalesPerson
HAVING COUNT(*) > 100
```

</details>



2\. Znajdź które modele (produktu `ProductModelID`), mają średnią cene produktu `ListPrice` większą niż 300



> 29 wyników


```sql
SELECT ProductModelID, AVG(ListPrice) AveragePrice
FROM SalesLT.Product
GROUP BY ProductModelID
HAVING AVG(ListPrice) > 300
```


3\. Znajdź kolory `Color` produktów, które mają miminalną cenę `ListPrice` 30

> 5 rezultatów


```sql
SELECT Color, MIN(ListPrice) as MinPrice
FROM SalesLT.Product

HAVING MIN(ListPrice) > 30
```

