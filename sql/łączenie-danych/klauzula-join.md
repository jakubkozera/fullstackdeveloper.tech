## Łączenie danych z wielu tabel

Łączenie danych w MS SQL, czyli operacja `JOIN`, pozwala na łączenie wierszy z różnych tabel na podstawie określonych kryteriów. W SQL istnieją różne rodzaje `JOIN`, które określają, jakie wiersze zostaną uwzględnione w wynikowym zbiorze danych.

1. **JOIN (INNER JOIN)**: Zwraca wiersze, które mają pasujące wartości w obu tabelach.
2. **LEFT JOIN (LEFT OUTER JOIN)**: Zwraca wszystkie wiersze z lewej tabeli (tabeli zdefiniowanej po lewej stronie zapytania JOIN), a także pasujące wiersze z prawej tabeli. Jeśli w prawej tabeli nie ma pasujących wartości, to dla tych wierszy zostaną zwrócone wartości NULL.
3. **RIGHT JOIN (RIGHT OUTER JOIN)**: Jest odwrotnością LEFT JOIN. Zwraca wszystkie wiersze z prawej tabeli (tabeli zdefiniowanej po prawej stronie zapytania JOIN), a także pasujące wiersze z lewej tabeli. Jeśli w lewej tabeli nie ma pasujących wartości, to dla tych wierszy zostaną zwrócone wartości NULL.
4. **FULL JOIN (FULL OUTER JOIN)**: Zwraca wiersze, które mają pasujące wartości w jednej z tabel. Wszystkie wiersze z obu tabel są zwracane, a jeśli nie ma pasujących wartości, to dla nich zostaną zwrócone wartości NULL.

Zobaczmy jakie rezultaty zwrócą zapytania wykorzystujące róźne typy `JOIN`'ów


```sql
SELECT *
FROM SalesLT.SalesOrderHeader AS soh
INNER JOIN SalesLT.Customer AS c ON soh.CustomerID = c.CustomerID;


```


```sql
SELECT *
FROM SalesLT.Customer AS c
LEFT JOIN SalesLT.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID;


```


```sql
SELECT *
FROM SalesLT.CustomerAddress AS ca
RIGHT JOIN SalesLT.Address AS a ON ca.AddressID = a.AddressID;


```


```sql
SELECT *
FROM SalesLT.Customer AS c
FULL JOIN SalesLT.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID;

```

W każdym z tych zapytań wybieramy różne zestawy kolumn z różnych tabel i łączymy je za pomocą różnych rodzajów JOIN, aby uzyskać różne zestawy wyników w zależności od potrzeb.

## Aliasy

Aliasy w `JOIN` to nadane krótkie nazwy tabelom w zapytaniach SQL. Pozwalają one na zwięzłe odwoływanie się do tych elementów wewnątrz zapytania, co ułatwia czytelność kodu i redukuje powtarzalność. 

W przypadku klauzuli `JOIN`, aliasy są szczególnie użyteczne, gdy łączymy wiele tabel, ponieważ pozwala to uniknąć długich nazw tabel i sprawia, że zapytanie jest bardziej czytelne. 

Na przykład, zamiast używać pełnych nazw tabel, możemy nadawać im aliasy i odwoływać się do nich za pomocą tych aliasów. Przykładowo:




```sql
SELECT soh.SalesOrderID, soh.OrderDate, sod.LineTotal
FROM SalesLT.SalesOrderHeader soh
JOIN SalesLT.SalesOrderDetail as [sod] on sod.SalesOrderID = soh.SalesOrderID

```

W tym przykładzie używamy aliasów do skrócenia długich nazw tabel i ułatwienia odwoływania się do kolumn w zapytaniu.

- `SalesLT.SalesOrderHeader soh`: Nadajemy tabeli `SalesOrderHeader` alias `soh`. Dzięki temu możemy odwoływać się do kolumn z tej tabeli używając krótszego aliasu `soh`, na przykład `soh.SalesOrderID` i `soh.OrderDate`.
- `SalesLT.SalesOrderDetail sod`: Nadajemy tabeli `SalesOrderDetail` alias `sod`. Podobnie jak powyżej, używamy tego aliasu, aby odwoływać się do kolumn z tabeli `SalesOrderDetail`, takich jak `sod.LineTotal`.
- W klauzuli JOIN używamy aliasów w warunku łączenia tabel (`sod.SalesOrderID = soh.SalesOrderID`). Dzięki temu wiadomo, które kolumny są z których tabel, nawet jeśli używamy krótszych aliasów.

## Wpływ typu relacji na wynik klauzuli `JOIN`

W relacyjnych bazach danych, możemy definiować relacje pomiędzy tabelami w stosunku:
- jeden do jednego
- jeden do wielu
- wiele do wielu

W zależności od typu relacji, wynik klauzuli JOIN może być różny. W przypadku relacji jeden do jednego, wynik klauzuli JOIN będzie zawierał tylko jedno połączenie pomiędzy tabelami. W przypadku relacji jeden do wielu, jak i wiele do wielu, wynik klauzuli JOIN będzie zawierał wiele połączeń pomiędzy tabelami.

Przykładowo w relacji jeden do jeden, między tabelami `SalesLT.SalesOrderHeader`, a `SalesLT.Address` istnieje tylko jedno połączenie - każde zamówienie ma przypisany jeden adres dostawy `BillToAddressID`. 



```sql
SELECT sod.SalesOrderNumber, a.*
FROM SalesLT.SalesOrderHeader sod
JOIN SalesLT.Address a on sod.BillToAddressID = a.AddressID
```

W relacji jeden do wielu, między tabelami `SalesLT.Product`, a `SalesLT.ProductModel` istnieje wiele połączeń, jako że jeden model produktu, może mieć np. kilka róźnych rozmiarów.



```sql
SELECT p.ProductID, p.ProductModelID, pm.Name [ProductModelName], p.Name [ProductName]
FROM SalesLT.Product p
JOIN SalesLT.ProductModel pm on pm.ProductModelID = p.ProductModelID
```

W relacji wiele do wielu, potrzeba będzie dołączenia tzw. tabeli łączącej, która przechowuje informacje o powiązaniach wierszy z dwóch róźnych tabel


```sql
SELECT c.CustomerID, a.*
FROM SalesLT.Customer c
JOIN SalesLT.CustomerAddress ca on ca.CustomerID = c.CustomerID
JOIN SalesLT.Address a on a.AddressID = ca.AddressID
```

## Łączenie wielu tabel

Klauzulą `JOIN` jesteśmy w stanie połączyć wiersze z dwóch lub więcej tabel na podstawie wspólnego klucza. W przypadku większej ilości tabel, klauzula `JOIN` może być wielokrotnie zagnieżdżana. W ten sposób możemy, albo dołączyć wiersze do głównej tabeli, albo do jednej z tabel dołączonych `JOIN`'em.

Przykładowo:



```sql
SELECT soh.SalesOrderID, sod.UnitPriceDiscount, p.Name AS ProductName, sod.OrderQty, sod.UnitPrice
FROM SalesLT.SalesOrderHeader AS soh
JOIN SalesLT.SalesOrderDetail AS sod ON soh.SalesOrderID = sod.SalesOrderID
JOIN SalesLT.Product AS p ON sod.ProductID = p.ProductID
WHERE sod.UnitPriceDiscount > 0
```


W tym przykładzie wykonujemy zapytanie, które łączy trzy tabele: `SalesOrderHeader`, `SalesOrderDetail` i `Product`, aby uzyskać informacje o zamówieniach, ich szczegółach i produktach.

1. W klauzuli SELECT wybieramy konkretne kolumny z każdej tabeli: `soh.SalesOrderID` (identyfikator zamówienia), `sod.UnitPriceDiscount` (rabat na cenę jednostkową), `p.Name AS ProductName` (nazwa produktu), `sod.OrderQty` (ilość zamówionego produktu) oraz `sod.UnitPrice` (cena jednostkowa produktu).

2. W klauzuli FROM wskazujemy tabelę `SalesOrderHeader` jako `soh`.

3. Następnie używamy klauzuli JOIN, aby dołączyć tabelę `SalesOrderDetail` jako `sod` na podstawie identyfikatora zamówienia (`soh.SalesOrderID = sod.SalesOrderID`).

4. Kolejnym krokiem jest ponowne użycie klauzuli JOIN, aby dołączyć tabelę `Product` jako `p` na podstawie identyfikatora produktu (`sod.ProductID = p.ProductID`).

5. Klauzula WHERE służy do filtrowania wyników. Tutaj wybieramy tylko te wiersze, gdzie wartość `sod.UnitPriceDiscount` jest większa od zera, co oznacza, że został zastosowany rabat na cenę jednostkową produktu.

Podsumowując, to zapytanie zwraca informacje o zamówieniach, które miały zastosowany rabat na cenę jednostkową produktu, wraz z szczegółowymi danymi dotyczącymi tych zamówień i zamówionych produktów.
