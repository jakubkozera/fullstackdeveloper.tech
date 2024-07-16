## Funkcje okienne agregujące

Funkcje okienne agregujące są jednym z najważniejszych narzędzi w analizie danych. Pozwalają one na obliczanie wartości funkcji agregujących na podzbiorach danych, które są zdefiniowane przez okno. Okno to zbiór wierszy, które są grupowane na podstawie określonych kryteriów. Funkcje agregujące, takie jak: `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()` są obliczane dla każdego okna z osobna.

Tak więc, o ile w danym zapytaniu zwracamy informacje, które chcielibyśmy dodatkowo przetworzyć, to zamiast używania podzapytań, możemy wykorzystać funkcje okna, aby uzyskać te informacje w jednym zapytaniu.

## `SUM()`

Funkcja `SUM()` oblicza sumę wartości w kolumnie. W przypadku funkcji okiennej `SUM()` wartości są sumowane dla każdego okna z osobna.

Przykładowo, mając bazowę zapytanie z tabeli `SalesLT.SalesOrderDetail`:


```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice
FROM 
    SalesLT.SalesOrderDetail;

```


Możemy obliczyć sumę wartości w kolumnie `OrderQty` dla każdego zamówienia, korzystając z funkcji okiennej `SUM()`:




```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice,
    SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS OrderQtySum
FROM
    SalesLT.SalesOrderDetail;

```


W wyniku otrzymamy kolumnę `OrderQtySum`, która zawiera sumę wartości w kolumnie `OrderQty` dla każdego zamówienia z osobna

Podobny wynik, dostalibyśmy z poniższego zapytania:




```sql
SELECT 
    SOD.SalesOrderID,
    SOD.SalesOrderDetailID,
    SOD.OrderQty,
    UnitPrice,
    (SELECT SUM(OrderQty)
     FROM SalesLT.SalesOrderDetail SOD2
     WHERE SOD2.SalesOrderID = SOD.SalesOrderID) AS OrderQtySum
FROM
    SalesLT.SalesOrderDetail SOD;


```

## `AVG()`

Funkcja `AVG()` oblicza średnią wartości w kolumnie. W przypadku funkcji okiennej `AVG()` wartości są obliczane dla każdego okna z osobna.

Przykładowo, mając bazowę zapytanie z tabeli `SalesLT.SalesOrderDetail`:


```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice
FROM
    SalesLT.SalesOrderDetail;

```


Możemy obliczyć średnią wartości w kolumnie `UnitPrice` dla każdego zamówienia, korzystając z funkcji okiennej `AVG()`:




```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice,
    AVG(UnitPrice) OVER(PARTITION BY SalesOrderID) AS UnitPriceAvg
FROM
    SalesLT.SalesOrderDetail;

```


W wyniku otrzymamy kolumnę `UnitPriceAvg`, która zawiera średnią wartości w kolumnie `UnitPrice` dla każdego zamówienia z osobna.

## `MIN()`/ `MAX()`

Funkcje `MIN()` i `MAX()` obliczają odpowiednio minimalną i maksymalną wartość w kolumnie. W przypadku funkcji okiennej wartości są obliczane dla każdego okna z osobna.

Przykładowo, mając bazowę zapytanie z tabeli `SalesLT.SalesOrderDetail`:




```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice
FROM
    SalesLT.SalesOrderDetail;

```


Możemy obliczyć minimalną i maksymalną wartość w kolumnie `UnitPrice` dla każdego zamówienia, korzystając z funkcji okiennej `MIN()` i `MAX()`:




```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice,
    MIN(UnitPrice) OVER(PARTITION BY SalesOrderID) AS UnitPriceMin,
    MAX(UnitPrice) OVER(PARTITION BY SalesOrderID) AS UnitPriceMax
FROM
    SalesLT.SalesOrderDetail;

```


W wyniku otrzymamy kolumny `UnitPriceMin` i `UnitPriceMax`, które zawierają odpowiednio minimalną i maksymalną wartość w kolumnie `UnitPrice` dla każdego zamówienia z osobna.

## `COUNT()`

Funkcja `COUNT()` oblicza liczbę wierszy w kolumnie. W przypadku funkcji okiennej wartości są obliczane dla każdego okna z osobna.

Przykładowo, mając bazowę zapytanie z tabeli `SalesLT.SalesOrderDetail`:




```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice
FROM
    SalesLT.SalesOrderDetail;

```


Możemy obliczyć liczbę wierszy dla każdego zamówienia, korzystając z funkcji okiennej `COUNT()`:




```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice,
    COUNT(*) OVER(PARTITION BY SalesOrderID) AS OrderDetailCount
FROM
    SalesLT.SalesOrderDetail;

```


W wyniku otrzymamy kolumnę `OrderDetailCount`, która zawiera liczbę wierszy dla każdego zamówienia z osobna.





##  Zadanie


Wykorzystując funkcję okienną `SUM`, dowiedz się, ile największych sprzedaży dokonał, sprzedawca `adventure-works\jae0`, zanim przekroczył łączną kwotę sprzedaży `(tabela: SalesOrderHeader, kolumna: SubTotal)` 500 000. 


```sql
-- ROZWIĄZANIE

SELECT COUNT(*)
FROM (
    SELECT c.SalesPerson, soh.SubTotal,
        SUM(SubTotal) OVER (ORDER BY SubTotal DESC) RunningSum
    FROM SalesLT.SalesOrderHeader soh
    JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
    WHERE c.SalesPerson = 'adventure-works\jae0'
) sub
WHERE RunningSum < 500000


```


(1 row affected)



Total execution time: 00:00:00.005





<table><tr><th>(No column name)</th></tr><tr><td>6</td></tr></table>


