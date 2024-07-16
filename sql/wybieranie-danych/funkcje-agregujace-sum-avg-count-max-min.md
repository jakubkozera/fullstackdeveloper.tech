# Funkcje agregujące 

Poza podstawowymi klauzulami, które poznaliśmy do tej pory, SQL oferuje również funkcje agregujące, które pozwalają na przetwarzanie zestawów danych i zwracanie jednej wartości wynikowej. Jest to przydatna funkcja w analizie danych, pozwalająca na obliczanie sum, średnich wartości, liczby wierszy, maksimum, minimum itp. w kolumnach tabeli. 

**Wstęp do funkcji agregujących w SQL:**

Funkcje agregujące w języku SQL są używane do przetwarzania zestawów danych, grupując je według określonych kryteriów i zwracając jedno wartość wynikową. Te funkcje wykonują operacje matematyczne lub logiczne na zestawach danych w kolumnach tabeli, aby uzyskać pożądane wyniki, takie jak suma, średnia, liczba wierszy, maksimum lub minimum.

**Opis pojedynczych funkcji agregujących z przykładami:**

1. **SUM**: Funkcja `SUM()` oblicza sumę wartości w określonej kolumnie tabeli.
   - Przykład: Obliczenie łącznej wartości zamówień w tabeli SalesLT.SalesOrderHeader.
   


```sql
   SELECT SUM(TotalDue) AS TotalOrdersValue
   FROM SalesLT.SalesOrderHeader;

```


2. **AVG**: Funkcja `AVG()` oblicza średnią wartość w określonej kolumnie tabeli.
   - Przykład: Obliczenie średniej wartości produktów w tabeli SalesLT.Product.




```sql
   SELECT AVG(ListPrice) AS AveragePrice
   FROM SalesLT.Product;

```


3. **MAX**: Funkcja `MAX()` zwraca maksymalną wartość w określonej kolumnie tabeli.
   - Przykład: Znalezienie najwyższej wartości w kolumnie StandardCost w tabeli SalesLT.Product.




```sql
   SELECT MAX(StandardCost) AS MaxStandardCost
   FROM SalesLT.Product;

```


4. **MIN**: Funkcja `MIN()` zwraca minimalną wartość w określonej kolumnie tabeli.
   - Przykład: Znalezienie najniższej wartości w kolumnie OrderDate w tabeli SalesLT.SalesOrderHeader.




```sql
SELECT MIN(OrderDate) AS EarliestOrderDate
FROM SalesLT.SalesOrderHeader;
```

5\. <span style="color: #569cd6;font-weight: bold;"><strong>COUNT</strong></span>: Funkcja `COUNT()` zwraca liczbe wierszy zwróconych przez zapytanie. Funkcja ta przyjmuje jeden argument, który może być kolumną, wyrażeniem, literałem lub `*`.


```sql
SELECT COUNT(*) 
FROM SalesLT.Address
WHERE StateProvince = 'California';


```

Za jej pomocą możemy też zliczać unikalne wartości, przykładowo liczbę 'unikalnych' miast ze stanu \`California\`, możemy uzyskać w następujący sposób:


```sql
SELECT COUNT(DISTINCT City)
FROM SalesLT.Address
WHERE StateProvince = 'California'
```

Jeżeli podamy do niej nazwę kolumny, `COUNT()` zwraca liczbę wierszy, w których wartość kolumny nie jest `NULL`. Funkcja `COUNT()` zwraca wartość całkowitą.


```sql
SELECT COUNT(MiddleName)
FROM SalesLT.Customer;

```
