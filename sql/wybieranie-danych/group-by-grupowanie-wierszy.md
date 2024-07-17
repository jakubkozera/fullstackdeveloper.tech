# `GROUP BY` - grupowanie wyników

Klauzula `GROUP BY` w języku SQL jest używana do grupowania wierszy z wyników zapytania według określonych kolumn. Pozwala to na agregowanie danych w grupy na podstawie wspólnych wartości w określonej kolumnie, a następnie wykonywanie funkcji agregujących (takich jak SUM, AVG, COUNT, MAX, MIN) na tych grupach.



**Do czego służy GROUP BY?**



Klauzula GROUP BY jest niezwykle przydatna, gdy chcemy wykonywać obliczenia na danych grupowanych według określonych kryteriów. Pozwala nam ona na wyodrębnienie szczegółowych informacji z dużej ilości danych poprzez podział ich na logiczne grupy na podstawie wartości w określonych kolumnach.



**Przykład:**



Rozważmy tabelę `SalesOrderHeader` zawierającą dane o zamówieniach, takie jak `CustomerID`, i `SubTotal`. Jeśli chcielibyśmy zobaczyć sumę wartości zamówień dla każdego klienta, użylibyśmy klauzuli GROUP BY wraz z funkcją SUM(), aby zgrupować zamówienia według `CustomerID` i obliczyć sumę `SubTotal` dla każdego klienta.



Przykładowe zapytanie może wyglądać tak:






```sql
SELECT CustomerID, SUM(SubTotal) AS TotalOrderValue
FROM SalesLT.SalesOrderHeader
GROUP BY CustomerID;

```



W tym przypadku klauzula GROUP BY grupuje zamówienia według `CustomerID`, a funkcja SUM() oblicza łączną wartość zamówień dla każdego klienta.



Klauzula GROUP BY umożliwia nam również stosowanie wielu kolumn do grupowania, co pozwala na bardziej złożone analizy danych poprzez tworzenie hierarchii grupowania.



Natomiast co istotne, to że w ramach wyników z grupowania, możemy uzyskać tylko informacje o wartościach, które są agregowane. W przypadku zapytania z klauzulą GROUP BY, nie możemy uzyskać informacji o wartościach, które nie są agregowane.



Przykładowo, jeżeli chciałbym dostać informacje o statusie zamówienia, to nie mogę tego zrobić w zapytaniu z klauzulą GROUP BY, ponieważ status zamówienia nie jest agregowany. 






```sql
SELECT CustomerID, [Status], SUM(SubTotal) AS TotalOrderValue
FROM SalesLT.SalesOrderHeader
GROUP BY CustomerID;

```

Żeby poprawnie uzyskać informacje o `CustomerID` jak i `Status`, musiałbym obie te kolumny umieścić w kluczu grupującym:




```sql
SELECT CustomerID, [Status], SUM(SubTotal) AS TotalOrderValue
FROM SalesLT.SalesOrderHeader
GROUP BY CustomerID, [Status];
```

Rezultaty zwracane przez `GROUP BY` możemy też sortować, z tym, że klauzula `ORDER BY` musi znajdować się po `GROUP BY`.



Przykładowo, aby posortować wyniki grupowania po liczbie wariantów danego modelu produktu, możemy użyć poniższego zapytania:






```sql
SELECT ProductModelID, COUNT(*) as [ModelCount]
FROM [SalesLT].[Product]
GROUP BY ProductModelID 
ORDER BY ProductModelID DESC
```

Możemy też posortować po rezultatach funkcji agregującej, odpowiednio dla tego przykładu, aby posortować malejąco po liczbie wariantów danego modelu:


```sql
SELECT ProductModelID, COUNT(*) as [ModelCount]
FROM [SalesLT].[Product]
GROUP BY ProductModelID 
ORDER BY ModelCount DESC
```

---



## Zadanie







1. **Znajdź liczbę miast dla każdego stanu `StateProvince` z osobna:**


<details><summary><b>Rozwiązanie</b></summary>

```sql
-- ROWZWIĄZANIE


SELECT StateProvince, COUNT(DISTINCT City) [NumberOfCities]
FROM SalesLT.Address
GROUP BY StateProvince
```

</details>


2. **Znajdź liczbę klientów obługiwanych przez danego sprzedawcę (tabela `Customer`, kolumna `SalesPerson)`**


<details><summary><b>Rozwiązanie</b></summary>

```sql
-- ROWZWIĄZANIE


SELECT SalesPerson, COUNT(CustomerID) [CustomerCount]
FROM SalesLT.Customer
GROUP BY SalesPerson
```

</details>


3. **Znajdź sprzedawce z największą liczbą przypisanych klientów**


<details><summary><b>Rozwiązanie</b></summary>

```sql
-- ROWZWIĄZANIE


SELECT TOP 1 SalesPerson, COUNT(CustomerID) [CustomerCount]
FROM SalesLT.Customer
GROUP BY SalesPerson
ORDER BY CustomerCount DESC
```

</details>


4. **Oblicz średnią wartość `ListPrice` produktów w danych kolorze, których cena `ListPrice` jest większa niż 100:**



<details><summary><b>Rozwiązanie</b></summary>


```sql
-- ROWZWIĄZANIE

SELECT Color, AVG(ListPrice) AveragePrice
FROM SalesLT.Product
WHERE ListPrice > 100
GROUP BY Color
```

</details>


**5. Znajdź cene najtańszego produktu w danym rozmiarze** `Size`:


<details><summary><b>Rozwiązanie</b></summary>

```sql
-- ROWZWIĄZANIE

SELECT Size, MIN(ListPrice) CheapestPrice
FROM SalesLT.Product
GROUP BY Size
```

</details>
