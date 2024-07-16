## Podzapytania (sub-queries)

Zapytania zagnieżdżone, zwane także podzapytaniami lub sub-query, to zapytania SQL umieszczone wewnątrz innego zapytania SQL. Podzapytanie może być używane w różnych częściach zapytania głównego, takich jak warunek WHERE, klauzula FROM, czy też SELECT. Mają one wpływ na wykonanie zapytania poprzez dostarczenie wyniku, który jest używany jako filtr lub kolumna w głównym zapytaniu.

Zapytania zagnieżdżone możemy wykorzystać do:

1. **Filtrowanie wyników**: Podzapytania mogą służyć do filtrowania wyników na podstawie wyników innych zapytań. Na przykład, można utworzyć podzapytanie do wybrania klientów, którzy dokonali zakupu w określonym przedziale dat.
2. **Zwracanie rezultatów**: Podzapytania mogą zwracać pojedynczą wartość, która jest następnie wykorzystywana jako kolumna w głównym zapytaniu. Na przykład, można użyć sub-query do obliczenia sumy wartości w kolumnie i wyświetlenia jej w rezultatach.
3. **Uwzględnianie w warunkach logicznych**: Podzapytania mogą być wykorzystywane w warunkach logicznych, takich jak IN, NOT IN, aby sprawdzić, czy pewne warunki są spełnione.
4. **Zagnieżdżanie zapytań**: Podzapytania mogą być zagnieżdżane w innych podzapytaniach, co pozwala na tworzenie bardziej złożonych zapytań.
5. **Wybieranie danych**: Podzapytania mogą być używane do wybierania danych z innych tabel, które są używane w ramach klauzuli `FROM` lub `JOIN`.

Przykładowo, aby zwrócić produkty, które mają cene powyżej średniej ceny wszystkich produktów, możemy wykorzystać podzapytanie do obliczenia średniej wartości wszystkich produktów, a rezultat porównać do zwrócenia głównego zapytania


```sql
SELECT Name, ListPrice
FROM SalesLT.Product
WHERE ListPrice > (
    SELECT AVG(ListPrice)
    FROM SalesLT.Product
)
```

Zwrócenie listy produktów, które nie zostały sprzedane


```sql
SELECT [Name]
FROM SalesLT.Product
WHERE ProductID NOT IN (
    SELECT ProductID
    FROM SalesLT.SalesOrderDetail
);
```

Subqueries mają też zastosowanie w ramach klauzuli `SELECT`, aby zwrócić wynik z jednego zapytania, które jest używane jako część innego zapytania. W takim przypadku zapytanie zagnieżdżone jest wykonywane dla każdego wiersza zwróconego przez zapytanie zewnętrzne.

Przykładowo, zapytanie wyświetlające liczbę produktów dla każdej kategorii (bez grupowania):


```sql
SELECT pc.Name AS Category, (SELECT COUNT(*) FROM SalesLT.Product AS p WHERE p.ProductCategoryID = pc.ProductCategoryID) AS ProductCount
FROM SalesLT.ProductCategory pc

```

Czy też, zapytanie wyświetlające nazwę kategorii produktu oraz najdroższy produkt w każdej kategorii:


```sql
    SELECT pc.Name AS Category, 
           (SELECT TOP 1 Name 
            FROM SalesLT.Product AS p 
            WHERE p.ProductCategoryID = pc.ProductCategoryID 
            ORDER BY ListPrice DESC) AS MostExpensiveProduct
    FROM SalesLT.ProductCategory AS pc

```

Podzapytania można też zagnieżdżać, co pozwala na bardziej złożone zapytania. Jeżeli w poprzednim przykładzie, chcielibyśmy zwrócić tylko te wiersze, których wartość `MostExpensiveProduct` nie jest `NULL`, to nie jesteśmy w stanie tego zrobić po prostu dodając warunek `WHERE MostExpensiveProduct IS NOT NULL`, ponieważ jest to wartość obliczana w podzapytaniu. Możemy jednak zrobić to w następujący sposób, tworząc zapytanie zagnieżdżone w ramach klauzuli `FROM`:





```sql
SELECT Category, MostExpensiveProduct
FROM (
    SELECT pc.Name AS Category, 
           (SELECT TOP 1 Name 
            FROM SalesLT.Product AS p 
            WHERE p.ProductCategoryID = pc.ProductCategoryID 
            ORDER BY ListPrice DESC) AS MostExpensiveProduct
    FROM SalesLT.ProductCategory AS pc
) AS subquery
WHERE MostExpensiveProduct IS NOT NULL

```

Zauważ, że korzystając z subquery w ramach klauzuli `FROM` musimy zawsze nadać alias dla tej subquery. W przeciwnym razie otrzymamy błąd.

Podzapytania możemy też wykorzystać w ramach klauzuli `JOIN`, co pozwala na bardziej złożone zapytania.

Tutaj podobnie jak w klauzuli `FROM`, będziemy musieli nadać alias podzapytaniu, aby móc się do niego odwołać w klauzuli `JOIN`.

 W poniższym przykładzie wykorzystamy podzapytanie wyświetlające nazwę kategorii produktu oraz najdroższy produkt w każdej kategorii:




```sql
SELECT pc.Name AS Category, p.Name AS MostExpensiveProduct
FROM SalesLT.ProductCategory AS pc
JOIN (
    SELECT ProductCategoryID, MAX(ListPrice) AS MaxPrice
    FROM SalesLT.Product
    GROUP BY ProductCategoryID
) AS subquery ON pc.ProductCategoryID = subquery.ProductCategoryID
JOIN SalesLT.Product AS p ON subquery.ProductCategoryID = p.ProductCategoryID AND subquery.MaxPrice = p.ListPrice;

```

## Wpływ subqueries na wydajność zapytania w bazie danych

Użycie subqueries może wpłynąć na wydajność zapytania, ale nie zawsze jest to regułą. W niektórych przypadkach zagnieżdżone zapytania mogą być wydajne i potrzebne do uzyskania żądanych wyników. Jednakże nieoptymalne użycie zapytań zagnieżdżonych może prowadzić do spowolnienia zapytania. Oto kilka czynników, które mogą wpłynąć na wydajność zapytań z subqueries:
1. **Liczba zapytań**: Zbyt wiele zagnieżdżonych zapytań może powodować znaczny wzrost liczby operacji odczytu i przetwarzania danych, co może spowodować spowolnienie zapytania.
2. **Brak indeksów**: Jeśli podzapytania są wykonywane na dużych zbiorach danych, a kolumny używane w warunkach nie są zaindeksowane, może to prowadzić do skanowania całej tabeli, co znacznie spowolni zapytanie.
3. **Niewydajne zapytania zagnieżdżone**: Nieoptymalnie napisane subqueries mogą być bardziej kosztowne niż efektywne operacje łączenia tabel lub inne metody przetwarzania danych.
4. **Złożoność logiczna zapytań**: Bardzo złożone logicznie subqueries mogą prowadzić do trudności w optymalizacji przez silnik bazy danych, co może skutkować spowolnieniem zapytania.
Podsumowując, użycie subqueries może wpłynąć na wydajność zapytania, ale jest to zależne od wielu czynników. Optymalne projektowanie i optymalizacja zapytań są kluczowe dla zapewnienia jak najlepszej wydajności zapytań zagnieżdżonych.
