# Funkcje `RANK()` i `DENSE_RANK()`

### Funkcja `RANK()`

Funkcja `RANK()` zwraca pozycję/ranking w grupie rekordów. Jeśli dwa rekordy mają taką samą wartość, to funkcja `RANK()` zwróci tę samą wartość dla obu rekordów, a następnie przeskoczy do kolejnej wartości. Jej użycie będzie bardzo zbliżone do funkcji `ROW_NUMBER()`, ale z tą różnicą, że funkcja `RANK()` może zwrócić tę samą wartość dla dwóch rekordów, jeśli mają taką samą wartość.

Przykładowo:


```sql
SELECT c.SalesPerson, 
    c.CustomerID, 
    soh.SubTotal, 
    soh.SalesOrderID,
    ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRN,
    RANK() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank
FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
```



W powyższym przykładzie, jeśli dwóch klientów ma taką samą wartość `SubTotal`, to funkcja `RANK()` zwróci tę samą wartość dla obu rekordów, a następnie przeskoczy do kolejnej wartości, natomiast jeśli wartości `SubTotal` są różne, to funkcja `RANK()` zwróci różne wartości dla każdego rekordu, wynik będzie podobny do funkcji `ROW_NUMBER()`. Tak więc, aby zobaczyć róźnice w wyniku tych dwóch funkcji, warto użyć danych, w których wartości `SubTotal` są takie same dla dwóch rekordów. W tym celu, wykonajmy polecenie `UPDATE` na tabeli `SalesLT.[SalesOrderHeader]`:






```sql
UPDATE SalesLT.[SalesOrderHeader]
SET SubTotal = 2016.3408
WHERE SalesOrderID = 71846
UPDATE SalesLT.[SalesOrderHeader]
SET SubTotal = 550.386
WHERE SalesOrderID = 71867
```

Dopiero teraz, gdy conajmniej 2 wiersze mają taką samą wartość w kolumnie w klauzuli `ORDER BY`, widzimy róźnice w rezultacie zapytania. W takim przypadku, wynik zależy od kolejności wierszy w tabeli. `RANK` w ten sam sposób sklasiwuje wiersze z taką samą wartością w kolumnie w klauzuli `ORDER BY`, gdzie `ROW_NUMBER` nie robi tego. 



Co więcej ranking następnego wiersza, raz po tego typu wierszach, jest zwiększany o liczbę wierszy z taką samą wartością w kolumnie w klauzuli `ORDER BY`.





### Funkcja `DENSE_RANK()`



`DENSE_RANK()` działa podobnie jak `RANK()`, ale nie ma przerw w numeracji rankingów. W przypadku, gdy kilka wierszy ma taką samą wartość w kolumnie w klauzuli `ORDER BY`, to rankingi są nadal zwiększane o 1, ale nie ma przerw w numeracji.






```sql
SELECT c.SalesPerson, 
    c.CustomerID, 
    soh.SubTotal, 
    soh.SalesOrderID,
    ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRN,
    RANK() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank,
    DENSE_RANK() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerDenseRank
FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
```


