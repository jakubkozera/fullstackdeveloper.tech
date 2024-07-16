# `UNION`

Klauzla `JOIN`, pozwoliła nam połączyć informacje z wielu tabel w jednym zapytaniu. Jednak co jeśli, mamy potrzebę połączenia wierszy wyników z dwóch zapytań? 

W takim przypadku możemy użyć klauzli `UNION`.

`UNION` (unia) pozwala na połączenie wyników z dwóch zapytań w jednym wyniku. Jednak zapytania muszą mieć taką samą liczbę kolumn, a kolumny muszą mieć takie same typy danych. Co więcej duplikaty są automatycznie usuwane, o ile nie użyjemy klauzli `UNION ALL`.

### Składnia operatora `UNION`

```
SELECT kolumna1, kolumna2, ...
FROM tabela1
[WHERE warunek]

UNION

SELECT kolumna1, kolumna2, ...
FROM tabela2
[WHERE warunek]

```

### Składnia operatora `UNION ALL`

```
SELECT kolumna1, kolumna2, ...
FROM tabela1
[WHERE warunek]

UNION ALL

SELECT kolumna1, kolumna2, ...
FROM tabela2
[WHERE warunek]

```

### Zasady użycia operatora `UNION`

1. **Liczba kolumn**: Każde zapytanie SELECT w unii musi mieć tę samą liczbę kolumn.
2. **Typy danych**: Kolumny muszą mieć zgodne typy danych w odpowiadających sobie pozycjach.
3. **Kolejność kolumn**: Kolejność kolumn musi być taka sama w każdym zapytaniu SELECT.

### Przykład

Załóżmy, że mamy dwie tabele, `Klienci_2023` i `Klienci_2024`, które mają podobną strukturę i chcemy połączyć dane z obu tabel.

```
SELECT Imie, Nazwisko, Miasto
FROM Klienci_2023

UNION

SELECT Imie, Nazwisko, Miasto
FROM Klienci_2024;

```

Powyższe zapytanie zwróci unikalny zestaw wyników łączący dane z obu tabel.

Jeśli chcemy zachować wszystkie wiersze, w tym duplikaty, użyjemy `UNION ALL`:

```
SELECT Imie, Nazwisko, Miasto
FROM Klienci_2023

UNION ALL

SELECT Imie, Nazwisko, Miasto
FROM Klienci_2024;

```

### Praktyczne zastosowanie

Operator `UNION` jest użyteczny, gdy trzeba połączyć dane z różnych tabel lub wyników różnych zapytań, np. scalanie danych historycznych z danych bieżących, łączenie danych z różnych źródeł czy agregowanie wyników wielu podzapytań w jeden wynik.

#### Przykład: Lista unikalnych adresów wysyłkowych i bilingowych

Załóżmy, że chcemy uzyskać listę unikalnych adresów, które są używane zarówno jako adresy wysyłkowe (`ShipToAddressID`), jak i adresy bilingowe (`BillToAddressID`).


```sql
SELECT AddressID, AddressLine1, AddressLine2, City, StateProvince, CountryRegion, PostalCode
FROM SalesLT.Address
WHERE AddressID IN (SELECT ShipToAddressID FROM SalesLT.SalesOrderHeader)
UNION
SELECT AddressID, AddressLine1, AddressLine2, City, StateProvince, CountryRegion, PostalCode
FROM SalesLT.Address
WHERE AddressID IN (SELECT BillToAddressID FROM SalesLT.SalesOrderHeader);
```

Wiersze zwracane przez unie, mogą pochodzic z róźnych tabel, o ile są zgodne z typem zwracanym przez unie. Możemy przykładowo zwrócić informacje o zarówno nazwach produktów jak i nazwach kategorii, w ramach jednego zapytania.


```sql
SELECT [Name], 'Product' as [Type]
FROM SalesLT.ProductModel
UNION
SELECT [Name], 'Category' as [Type]
FROM SalesLT.ProductCategory
```
