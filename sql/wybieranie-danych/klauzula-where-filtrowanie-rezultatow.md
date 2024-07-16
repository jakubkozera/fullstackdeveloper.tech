# Klauzula `WHERE`

W języku SQL (Structured Query Language), klauzula WHERE określa warunek/warunki używane do filtrowania wyników zapytania SELECT. 

Pozwala ona na wybranie określonych wierszy z tabeli, które spełniają określone kryteria lub warunki.



Klauzula WHERE jest używana w połączeniu z zapytaniem SELECT w celu ograniczenia wyników do tych, które pasują do określonych warunków. Na przykład, jeśli masz tabelę zawierającą dane klientów, możesz użyć klauzuli WHERE, aby wybrać tylko tych klientów, którzy mieszkają w określonym mieście lub którzy mają więcej niż określoną wartość w kolumnie dotyczącej wieku.



Przykładowe użycie klauzuli WHERE w zapytaniu SELECT może wyglądać tak:



```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```



Gdzie:

- `column1`, `column2` to nazwy kolumn, które chcesz wybrać z tabeli.

- `table_name` to nazwa tabeli, z której chcesz wybrać dane.

- `condition` to warunek, który musi być spełniony przez wiersze, aby zostały wybrane. Na przykład, `age > 18` wybierze tylko wiersze, gdzie wartość w kolumnie "age" jest większa niż 18.



Klauzula WHERE może zawierać różne operatory porównania (np. `=`, `>`, `<`, `>=`, `<=`, `<>`), operatory logiczne (np. `AND`, `OR`, `NOT`), a także funkcje i wyrażenia, które umożliwiają bardziej zaawansowane filtrowanie danych.

Oto przykłady zapytań SQL wykorzystujących klauzulę WHERE na tabeli SalesLT.Customer:



Z pojedynczym filtrem wykorzystując operator '=':




```sql
SELECT *
FROM SalesLT.Customer
WHERE LastName = 'Smith';
```

Z pojedynczym filtrem wykorzystując operator `<>`/ `!=`


```sql
SELECT *
FROM SalesLT.Customer
WHERE LastName <> 'Smith';
```

Z pojedynczym filtrem wykorzystując operator `>`:




```sql
SELECT *
FROM SalesLT.Customer
WHERE CustomerID > 100;
```



Z dwoma filtrami łącząc je operatorem `AND`:




```sql
SELECT *
FROM SalesLT.Customer
WHERE FirstName = 'John' AND LastName <> 'Doe';
```



Z dwoma filtrami łącząc je operatorem `OR`:




```sql
SELECT *
FROM SalesLT.Customer
WHERE FirstName = 'John' OR LastName = 'Smith';

```

 Łącząc wiele filtrów przez `AND`, `OR` i nawiasami:




```sql
SELECT *
FROM SalesLT.Customer
WHERE FirstName = 'John' AND (LastName = 'Berger' OR FirstName = 'Margaret') AND LastName <> 'Smith';

```





Oto przykłady zastosowania operatorów `IS NULL` i `IS NOT NULL` w zapytaniach SQL na tabeli SalesLT.Customer:

Znajdź klientów, których pole MiddleName jest puste (NULL):


```sql
SELECT *
FROM SalesLT.Customer
WHERE MiddleName IS NULL


```

Znajdź klientów, którzy mają wprowadzony adres email (niepuste pole MiddleName):


```sql
SELECT *
FROM SalesLT.Customer
WHERE MiddleName IS NOT NULL

```

Co istone, do sprawdzenia wartości `NULL` musimy używać operatora `IS`/`IS NOT`, operatory `=`/`!=` nie zadziałają w oczekiwany sposób.

Jeżeli w konkretnym zapytaniu chcielibyśmy sprawdzić zakres/przedział wartości z danej kolumny, to oczywiście możemy skorzystać z operatora `AND` przykładowo:



```sql
SELECT * FROM table_name WHERE column_name >= value1 AND column_name <= value2;
```



Jednakże, w przypadku gdy chcemy sprawdzić zakres wartości z kilku kolumn, to zamiast wielokrotnego użycia operatora `AND`, możemy skorzystać z operatora `BETWEEN`:



```sql  
SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2;
```



Operator `BETWEEN` sprawdza, czy wartość z danej kolumny znajduje się w przedziale wartości od `value1` do `value2` (włącznie z wartościami `value1` i `value2`).



W poniższym przykładzie, zwrócimy wszystkie rekordy z tabeli `Customers`, gdzie wartość z kolumny `CustomerID` znajduje się w przedziale od 10 do 25 lat (włącznie z wartościami 10 i 25).






```sql
SELECT *
FROM SalesLT.Customer
WHERE CustomerID BETWEEN 10 AND 25;
```

Operator `BETWEEN` możemy też wykorzystać do sprawdzania dat. Wtedy zamiast `AND` używamy `BETWEEN` i podajemy dwie daty.

```sql
SELECT * FROM table_name WHERE date_column BETWEEN '2019-01-01' AND '2019-12-31';
```



Poza `BETWEEN`, w ramach klauzuli `WHERE`, możemy też wykorzystać operator `IN`, który pozwala na sprawdzenie, czy wartość z danej kolumny znajduje się w podanej liście.

```sql
SELECT * FROM table_name WHERE column_name IN ('value1', 'value2', 'value3');
```



Przykładowo, żeby sprawdzić czy nazwisko klienta znajduje się w liście 'Smith', 'Johnson', 'Williams', możemy użyć zapytania:


```sql
SELECT * 
FROM SalesLT.Customer 
WHERE LastName IN ('Smith', 'Johnson', 'Williams');
```

### `LIKE`



Operator `LIKE` w MS SQL jest używany do wyszukiwania wzorców w kolumnach tekstowych. Pozwala na dopasowywanie wartości w kolumnach do określonego wzorca przy użyciu specjalnych znaków, takich jak `%` (procent) i `_` (podkreślenie).



Oto jak działają te znaki:

- `%` (procent) zastępuje dowolną liczbę znaków (w tym zero znaków).

- `_` (podkreślenie) zastępuje dokładnie jeden znak.



Przykłady zastosowania operatora `LIKE`:



1. **Wyszukiwanie wartości zaczynających się na określony ciąg znaków:**

   ```sql
   SELECT * FROM tabela WHERE kolumna LIKE 'abc%';
   ```

   To zapytanie zwróci wszystkie wiersze, gdzie kolumna zaczyna się od "abc".



2. **Wyszukiwanie wartości kończących się na określony ciąg znaków:**

   ```sql
   SELECT * FROM tabela WHERE kolumna LIKE '%xyz';
   ```

   To zapytanie zwróci wszystkie wiersze, gdzie kolumna kończy się na "xyz".



3. **Wyszukiwanie wartości zawierających określony ciąg znaków:**

   ```sql
   SELECT * FROM tabela WHERE kolumna LIKE '%def%';
   ```

   To zapytanie zwróci wszystkie wiersze, gdzie kolumna zawiera "def" w dowolnym miejscu.



4. **Wyszukiwanie wartości z określonymi znakami na konkretnych pozycjach:**

   ```sql
   SELECT * FROM tabela WHERE kolumna LIKE 'a_c';
   ```

   To zapytanie zwróci wszystkie wiersze, gdzie kolumna zaczyna się na "a", ma dowolny jeden znak w środku, a następnie "c" (np. "abc", "a3c", ale nie "ac").



5. **Łączenie różnych wzorców:**

   ```sql
   SELECT * FROM tabela WHERE kolumna LIKE 'a%c%';
   ```

   To zapytanie zwróci wszystkie wiersze, gdzie kolumna zaczyna się na "a" i zawiera "c" w dowolnym miejscu po "a" (np. "abc", "a123c").



Operator `LIKE` jest bardzo przydatny do wyszukiwania i filtrowania danych tekstowych w bazach danych, szczególnie gdy nie znamy dokładnych wartości, które chcemy znaleźć, ale znamy pewne wzorce, które te wartości powinny spełniać.



Przykładowo, aby pobrać informacje klientów, których nazwiska kończą się na 'sen':




```sql
SELECT *
FROM SalesLT.Customer
WHERE LastName LIKE '%sen';
```

Albo, aby pobrać klientów, których imię zaczyna się na "A" i kończy na "a", możemy użyć zapytania:






```sql
SELECT *
FROM SalesLT.Customer
WHERE FirstName LIKE 'A%a';
```

Co ciekawe, w zależności od ustawień konkretnej bazy, operator `LIKE`, może ignorować wielkość liter i domyślnie (bez jawnego ustawiania opcji CASE SENSITIVE), powyższe zapytanie, możemy również zapisać w taki sposób:






```sql
SELECT *
FROM SalesLT.Customer
WHERE FirstName LIKE 'a%a';
```

Natomiast `_`, zazwyczaj posłuży nam do określenia, konkretnych wartości w ramach wyszukiwania po tekście.



Przykładowo, 3 literowe imie, kończące się na 'e'


```sql
SELECT *
FROM SalesLT.Customer
WHERE FirstName LIKE '__e';
```

### Użycie LIKE w nietypowy sposób

Choć `LIKE` nie jest tak potężny jak regex, można go czasem użyć do bardziej zaawansowanego dopasowywania:

- `[abc]` - dowolny znak z listy
- `[^abc]` - dowolny znak poza listą
- `[a-z]` - dowolny znak w zakresie


```sql
-- pobranie użytkowników z imieniem zaczynającym się od a, k, lub l

SELECT *
FROM SalesLT.Customer
WHERE FirstName LIKE '[akl]%'; 
```


```sql
-- pobranie użytkowników z imieniem niezaczynającym się od a, k, lub l

SELECT *
FROM SalesLT.Customer
WHERE FirstName LIKE '[^akl]%'; 
```


```sql
-- pobranie użytkowników z imieniem kończącym się na literę w zakresie od a do e

SELECT *
FROM SalesLT.Customer
WHERE FirstName LIKE '%[a-e]';
```
