# `SELECT` - wybieranie danych

Zapytanie SELECT jest podstawowym narzędziem w języku SQL (Structured Query Language), służącym do pobierania danych z bazy danych. Jest to zapytanie, które przeszukuje jedną lub więcej tabel w bazie danych w celu znalezienia i zwrócenia danych, które spełniają określone kryteria.

Ogólna struktura zapytania SELECT jest następująca:

```
SELECT column1, column2, ...
FROM table_name
WHERE condition;

```

- `SELECT`: Określa, które kolumny lub wyrażenia mają być wyświetlone w wynikach zapytania.
- `FROM`: Określa, z którą tabelą lub tabelami w bazie danych związane są dane, które chcemy pobrać.
- `WHERE`: Opcjonalna klauzula, która umożliwia filtrowanie danych na podstawie określonych warunków.

Główne zadania zapytania SELECT to:

1. **Pobieranie danych**: Zapytanie SELECT pozwala na pobieranie danych z określonych kolumn tabeli lub nawet całych wierszy.
2. **Filtrowanie danych**: Za pomocą klauzuli WHERE możemy określić warunki, które muszą być spełnione przez wiersze, aby zostały zwrócone jako wynik zapytania.
3. **Obliczenia**: Możemy wykonywać obliczenia na danych, takie jak suma, średnia, minimum, maksimum itp., i zwracać wyniki jako część zapytania SELECT.
4. **Sortowanie**: Zapytanie SELECT pozwala na sortowanie wyników na podstawie wartości w określonej kolumnie.
5. **Łączenie tabel**: Możemy łączyć dane z różnych tabel za pomocą operacji łączenia, takich jak INNER JOIN, LEFT JOIN, RIGHT JOIN itp.

Zapytanie SELECT jest niezwykle elastycznym narzędziem, które umożliwia zaawansowane manipulacje danymi w bazie danych, co czyni je kluczowym elementem w pracy z bazami danych przy użyciu języka SQL.

Przykładowo, aby pobrać wszystkie Nazwy (kolumna `Name`) produktów z tabeli `SalesLT.Product`, możemy wykonować następujące polecenie:


```sql
SELECT Name
FROM SalesLT.Product
```

W ramach jednego zapytania możemy również pobierać wiele kolumn jednocześnie,  definiując je przecinkami w zapytaniu `SELECT`


```sql
SELECT Name, ProductNumber, ListPrice
FROM SalesLT.Product
```

Nazwy kolumn, możemy też definiować w ramach nawiasów kwadratowych, przykładowo


```sql
SELECT [Name], ProductNumber, [ListPrice]
FROM SalesLT.Product
```

Możemy również zmienić mapowanie nazwy kolumny, do innej nazwy w ramach rezultatów zwróconych przez SQL server, za pomocą słowa kluczowego `as`, lub po prostu po spacji definiując nazwę danego wyniku:


```sql
SELECT [Name] as [ProductName], ProductNumber [PNumber], [ListPrice]
FROM SalesLT.Product
```

Poza tym, możemy również wybrać wszystkie dostępny kolumny, z konkretnej tabeli, za pomocą `*`


```sql
SELECT *
FROM SalesLT.Product
```

Domyślnie SQL Server, zwróci wszystkie wiersze, z tabeli, jeżeli w żaden sposób ich nie filtrujemy, natomiast możemy ograniczyć liczbę zwracanych wierszy, dzięki klauzuli `TOP <liczba_wierszy>`


```sql
SELECT TOP 10 *
FROM SalesLT.Product
```

Liczbę zwracanych wierszy klauzulą TOP, możemy też określić procentowo


```sql
SELECT TOP 10 percent *
FROM SalesLT.Product
```

Jeżeli z konkretnej kolumny, chcielibyśmy uzyskać unikalne wartości, to możemy to zrobić definiując klauzulę `DISTINCT`, przykładowo, aby pobrać wszystkie dostępe kolory produktów (bez powtórzeń):


```sql
SELECT DISTINCT Color
FROM SalesLT.Product
```

Klauzule `DISTINCT` możemy też wykorzsytać do pobrania wielu kolumn z wierszy, w ramach unikalnych wystąpień, przykładowo unikalne pary: kolor-rozmiar


```sql
SELECT DISTINCT Color, Size
FROM SalesLT.Product
```
