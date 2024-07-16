## `UNION`

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


(169 rows affected)



Total execution time: 00:00:00.017





<table><tr><th>Name</th><th>Type</th></tr><tr><td>All-Purpose Bike Stand</td><td>Product</td></tr><tr><td>Bike Wash</td><td>Product</td></tr><tr><td>Cable Lock</td><td>Product</td></tr><tr><td>Chain</td><td>Product</td></tr><tr><td>Classic Vest</td><td>Product</td></tr><tr><td>Cycling Cap</td><td>Product</td></tr><tr><td>Fender Set - Mountain</td><td>Product</td></tr><tr><td>Front Brakes</td><td>Product</td></tr><tr><td>Front Derailleur</td><td>Product</td></tr><tr><td>Full-Finger Gloves</td><td>Product</td></tr><tr><td>Half-Finger Gloves</td><td>Product</td></tr><tr><td>Headlights - Dual-Beam</td><td>Product</td></tr><tr><td>Headlights - Weatherproof</td><td>Product</td></tr><tr><td>Hitch Rack - 4-Bike</td><td>Product</td></tr><tr><td>HL Bottom Bracket</td><td>Product</td></tr><tr><td>HL Crankset</td><td>Product</td></tr><tr><td>HL Fork</td><td>Product</td></tr><tr><td>HL Headset</td><td>Product</td></tr><tr><td>HL Mountain Frame</td><td>Product</td></tr><tr><td>HL Mountain Front Wheel</td><td>Product</td></tr><tr><td>HL Mountain Handlebars</td><td>Product</td></tr><tr><td>HL Mountain Pedal</td><td>Product</td></tr><tr><td>HL Mountain Rear Wheel</td><td>Product</td></tr><tr><td>HL Mountain Seat/Saddle 1</td><td>Product</td></tr><tr><td>HL Mountain Seat/Saddle 2</td><td>Product</td></tr><tr><td>HL Mountain Tire</td><td>Product</td></tr><tr><td>HL Road Frame</td><td>Product</td></tr><tr><td>HL Road Front Wheel</td><td>Product</td></tr><tr><td>HL Road Handlebars</td><td>Product</td></tr><tr><td>HL Road Pedal</td><td>Product</td></tr><tr><td>HL Road Rear Wheel</td><td>Product</td></tr><tr><td>HL Road Seat/Saddle 1</td><td>Product</td></tr><tr><td>HL Road Seat/Saddle 2</td><td>Product</td></tr><tr><td>HL Road Tire</td><td>Product</td></tr><tr><td>HL Touring Frame</td><td>Product</td></tr><tr><td>HL Touring Handlebars</td><td>Product</td></tr><tr><td>HL Touring Seat/Saddle</td><td>Product</td></tr><tr><td>Hydration Pack</td><td>Product</td></tr><tr><td>LL Bottom Bracket</td><td>Product</td></tr><tr><td>LL Crankset</td><td>Product</td></tr><tr><td>LL Fork</td><td>Product</td></tr><tr><td>LL Headset</td><td>Product</td></tr><tr><td>LL Mountain Frame</td><td>Product</td></tr><tr><td>LL Mountain Front Wheel</td><td>Product</td></tr><tr><td>LL Mountain Handlebars</td><td>Product</td></tr><tr><td>LL Mountain Pedal</td><td>Product</td></tr><tr><td>LL Mountain Rear Wheel</td><td>Product</td></tr><tr><td>LL Mountain Seat/Saddle 1</td><td>Product</td></tr><tr><td>LL Mountain Seat/Saddle 2</td><td>Product</td></tr><tr><td>LL Mountain Tire</td><td>Product</td></tr><tr><td>LL Road Frame</td><td>Product</td></tr><tr><td>LL Road Front Wheel</td><td>Product</td></tr><tr><td>LL Road Handlebars</td><td>Product</td></tr><tr><td>LL Road Pedal</td><td>Product</td></tr><tr><td>LL Road Rear Wheel</td><td>Product</td></tr><tr><td>LL Road Seat/Saddle 1</td><td>Product</td></tr><tr><td>LL Road Seat/Saddle 2</td><td>Product</td></tr><tr><td>LL Road Tire</td><td>Product</td></tr><tr><td>LL Touring Frame</td><td>Product</td></tr><tr><td>LL Touring Handlebars</td><td>Product</td></tr><tr><td>LL Touring Seat/Saddle</td><td>Product</td></tr><tr><td>Long-Sleeve Logo Jersey</td><td>Product</td></tr><tr><td>Men&#39;s Bib-Shorts</td><td>Product</td></tr><tr><td>Men&#39;s Sports Shorts</td><td>Product</td></tr><tr><td>Minipump</td><td>Product</td></tr><tr><td>ML Bottom Bracket</td><td>Product</td></tr><tr><td>ML Crankset</td><td>Product</td></tr><tr><td>ML Fork</td><td>Product</td></tr><tr><td>ML Headset</td><td>Product</td></tr><tr><td>ML Mountain Frame</td><td>Product</td></tr><tr><td>ML Mountain Frame-W</td><td>Product</td></tr><tr><td>ML Mountain Front Wheel</td><td>Product</td></tr><tr><td>ML Mountain Handlebars</td><td>Product</td></tr><tr><td>ML Mountain Pedal</td><td>Product</td></tr><tr><td>ML Mountain Rear Wheel</td><td>Product</td></tr><tr><td>ML Mountain Seat/Saddle 1</td><td>Product</td></tr><tr><td>ML Mountain Seat/Saddle 2</td><td>Product</td></tr><tr><td>ML Mountain Tire</td><td>Product</td></tr><tr><td>ML Road Frame</td><td>Product</td></tr><tr><td>ML Road Frame-W</td><td>Product</td></tr><tr><td>ML Road Front Wheel</td><td>Product</td></tr><tr><td>ML Road Handlebars</td><td>Product</td></tr><tr><td>ML Road Pedal</td><td>Product</td></tr><tr><td>ML Road Rear Wheel</td><td>Product</td></tr><tr><td>ML Road Seat/Saddle 1</td><td>Product</td></tr><tr><td>ML Road Seat/Saddle 2</td><td>Product</td></tr><tr><td>ML Road Tire</td><td>Product</td></tr><tr><td>ML Touring Seat/Saddle</td><td>Product</td></tr><tr><td>Mountain Bike Socks</td><td>Product</td></tr><tr><td>Mountain Bottle Cage</td><td>Product</td></tr><tr><td>Mountain Pump</td><td>Product</td></tr><tr><td>Mountain Tire Tube</td><td>Product</td></tr><tr><td>Mountain-100</td><td>Product</td></tr><tr><td>Mountain-200</td><td>Product</td></tr><tr><td>Mountain-300</td><td>Product</td></tr><tr><td>Mountain-400</td><td>Product</td></tr><tr><td>Mountain-400-W</td><td>Product</td></tr><tr><td>Mountain-500</td><td>Product</td></tr><tr><td>Patch kit</td><td>Product</td></tr><tr><td>Racing Socks</td><td>Product</td></tr><tr><td>Rear Brakes</td><td>Product</td></tr><tr><td>Rear Derailleur</td><td>Product</td></tr><tr><td>Road Bottle Cage</td><td>Product</td></tr><tr><td>Road Tire Tube</td><td>Product</td></tr><tr><td>Road-150</td><td>Product</td></tr><tr><td>Road-250</td><td>Product</td></tr><tr><td>Road-350</td><td>Product</td></tr><tr><td>Road-350-W</td><td>Product</td></tr><tr><td>Road-450</td><td>Product</td></tr><tr><td>Road-550</td><td>Product</td></tr><tr><td>Road-550-W</td><td>Product</td></tr><tr><td>Road-650</td><td>Product</td></tr><tr><td>Road-750</td><td>Product</td></tr><tr><td>Short-Sleeve Classic Jersey</td><td>Product</td></tr><tr><td>Sport-100</td><td>Product</td></tr><tr><td>Taillight</td><td>Product</td></tr><tr><td>Touring Front Wheel</td><td>Product</td></tr><tr><td>Touring Pedal</td><td>Product</td></tr><tr><td>Touring Rear Wheel</td><td>Product</td></tr><tr><td>Touring Tire</td><td>Product</td></tr><tr><td>Touring Tire Tube</td><td>Product</td></tr><tr><td>Touring-1000</td><td>Product</td></tr><tr><td>Touring-2000</td><td>Product</td></tr><tr><td>Touring-3000</td><td>Product</td></tr><tr><td>Touring-Panniers</td><td>Product</td></tr><tr><td>Water Bottle</td><td>Product</td></tr><tr><td>Women&#39;s Mountain Shorts</td><td>Product</td></tr><tr><td>Women&#39;s Tights</td><td>Product</td></tr><tr><td>Accessories</td><td>Category</td></tr><tr><td>Bib-Shorts</td><td>Category</td></tr><tr><td>Bike Racks</td><td>Category</td></tr><tr><td>Bike Stands</td><td>Category</td></tr><tr><td>Bikes</td><td>Category</td></tr><tr><td>Bottles and Cages</td><td>Category</td></tr><tr><td>Bottom Brackets</td><td>Category</td></tr><tr><td>Brakes</td><td>Category</td></tr><tr><td>Caps</td><td>Category</td></tr><tr><td>Chains</td><td>Category</td></tr><tr><td>Cleaners</td><td>Category</td></tr><tr><td>Clothing</td><td>Category</td></tr><tr><td>Components</td><td>Category</td></tr><tr><td>Cranksets</td><td>Category</td></tr><tr><td>Derailleurs</td><td>Category</td></tr><tr><td>Fenders</td><td>Category</td></tr><tr><td>Forks</td><td>Category</td></tr><tr><td>Gloves</td><td>Category</td></tr><tr><td>Handlebars</td><td>Category</td></tr><tr><td>Headsets</td><td>Category</td></tr><tr><td>Helmets</td><td>Category</td></tr><tr><td>Hydration Packs</td><td>Category</td></tr><tr><td>Jerseys</td><td>Category</td></tr><tr><td>Lights</td><td>Category</td></tr><tr><td>Locks</td><td>Category</td></tr><tr><td>Mountain Bikes</td><td>Category</td></tr><tr><td>Mountain Frames</td><td>Category</td></tr><tr><td>Panniers</td><td>Category</td></tr><tr><td>Pedals</td><td>Category</td></tr><tr><td>Pumps</td><td>Category</td></tr><tr><td>Road Bikes</td><td>Category</td></tr><tr><td>Road Frames</td><td>Category</td></tr><tr><td>Saddles</td><td>Category</td></tr><tr><td>Shorts</td><td>Category</td></tr><tr><td>Socks</td><td>Category</td></tr><tr><td>Tights</td><td>Category</td></tr><tr><td>Tires and Tubes</td><td>Category</td></tr><tr><td>Touring Bikes</td><td>Category</td></tr><tr><td>Touring Frames</td><td>Category</td></tr><tr><td>Vests</td><td>Category</td></tr><tr><td>Wheels</td><td>Category</td></tr></table>


