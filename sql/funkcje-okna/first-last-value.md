## Funkcje `FIRST_VALUE` i `LAST_VALUE`

Funkcje `FIRST_VALUE` i `LAST_VALUE` są analitycznymi funkcjami okna, które umożliwiają dostęp do pierwszej lub ostatniej wartości w zestawie danych zdefiniowanym przez klauzulę `OVER`.

### FIRST\_VALUE

Funkcja `FIRST_VALUE` zwraca pierwszą wartość z zestawu danych określonego przez klauzulę okna. Przy jej użyciu, musimy określić po jakiej kolumnie będziemy sortować dane, aby móc znaleźć pierwszą wartość. Tak więc konieczne jest, użycie klauzuli `ORDER BY` wraz z `OVER` w celu określenia kolumny, po której sortujemy dane.

#### Składnia:

```
FIRST_VALUE(expression) OVER ([PARTITION BY column] ORDER BY column [ROWS or RANGE specification])

```

#### Przykład użycia:

Załóżmy, że chcemy znaleźć pierwszą książkę wydaną przez każdego autora w tabeli `Books`. Możemy to osiągnąć za pomocą `FIRST_VALUE`:


```sql
SELECT 
    AuthorId, 
    Title,
    PublicationDate,
    FIRST_VALUE(Title) OVER (PARTITION BY AuthorId ORDER BY PublicationDate) AS FirstBook
FROM 
    Books;

```


Powyższe zapytanie zwróci listę książek z dodatkową kolumną `FirstBook`, która zawiera tytuł pierwszej książki każdego autora w kolejności publikacji.

### LAST\_VALUE

Funkcja `LAST_VALUE` zwraca ostatnią wartość z zestawu danych określonego przez klauzulę okna.

#### Składnia:

```
LAST_VALUE(expression) OVER ([PARTITION BY column] ORDER BY column [ROWS or RANGE specification])

```

#### Przykład użycia:

Załóżmy, że chcemy znaleźć ostatnią książkę wydaną przez każdego autora w tabeli `Books`. Możemy to osiągnąć za pomocą `LAST_VALUE`:




```sql
SELECT 
    AuthorId, 
    Title,
    PublicationDate,
    LAST_VALUE(Title) OVER (PARTITION BY AuthorId ORDER BY PublicationDate ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS LastBook
FROM 
    Books;

```

Jako, że domyślnie zakres wierszy w ramach okna, przy użyciu `LAST_VALUE`, jest od pierwszego wiersza do obecnego, to wykorzystamy `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` w celu zwrócenia ostatniego wiersza w ramach okna.



Powyższe zapytanie zwróci listę książek z dodatkową kolumną `LastBook`, która zawiera tytuł ostatniej książki każdego autora w kolejności publikacji.

###   

### Zastosowanie w kontekście bazy danych

Zapytanie, które zwraca informacje o wypożyczeniach książek, w tym datę wypożyczenia i datę zwrotu, i dodatkową kolumną pokazującą najwcześniejsze wypożyczenie dla każdego użytkownika.




```sql
SELECT 
    UserId, 
    LoanDate,
    ReturnDate,
    FIRST_VALUE(LoanDate) OVER (PARTITION BY UserId ORDER BY LoanDate) AS FirstLoanDate
FROM 
    Loans;

```


(33 rows affected)



Total execution time: 00:00:00.017





<table><tr><th>UserId</th><th>LoanDate</th><th>ReturnDate</th><th>FirstLoanDate</th></tr><tr><td>1</td><td>2020-01-01 00:00:00.0000000</td><td>2024-05-05 07:25:20.3266667</td><td>2020-01-01 00:00:00.0000000</td></tr><tr><td>1</td><td>2021-01-01 00:00:00.0000000</td><td>2024-05-05 07:25:20.3266667</td><td>2020-01-01 00:00:00.0000000</td></tr><tr><td>1</td><td>2024-04-05 14:00:00.0000000</td><td>2024-05-05 07:25:20.3266667</td><td>2020-01-01 00:00:00.0000000</td></tr><tr><td>1</td><td>2024-04-19 14:00:00.0000000</td><td>2024-05-05 07:25:20.3266667</td><td>2020-01-01 00:00:00.0000000</td></tr><tr><td>2</td><td>2021-01-01 00:00:00.0000000</td><td>NULL</td><td>2021-01-01 00:00:00.0000000</td></tr><tr><td>2</td><td>2024-04-06 15:00:00.0000000</td><td>2024-04-22 10:00:00.0000000</td><td>2021-01-01 00:00:00.0000000</td></tr><tr><td>2</td><td>2024-04-20 15:00:00.0000000</td><td>2024-05-05 10:00:00.0000000</td><td>2021-01-01 00:00:00.0000000</td></tr><tr><td>2</td><td>2024-04-29 10:00:00.0000000</td><td>NULL</td><td>2021-01-01 00:00:00.0000000</td></tr><tr><td>227</td><td>2024-04-25 20:00:00.0000000</td><td>NULL</td><td>2024-04-25 20:00:00.0000000</td></tr><tr><td>227</td><td>2024-04-26 21:00:00.0000000</td><td>NULL</td><td>2024-04-25 20:00:00.0000000</td></tr><tr><td>228</td><td>2024-04-11 20:00:00.0000000</td><td>NULL</td><td>2024-04-11 20:00:00.0000000</td></tr><tr><td>228</td><td>2024-04-27 22:00:00.0000000</td><td>2024-05-07 12:00:00.0000000</td><td>2024-04-11 20:00:00.0000000</td></tr><tr><td>228</td><td>2024-04-30 11:00:00.0000000</td><td>NULL</td><td>2024-04-11 20:00:00.0000000</td></tr><tr><td>228</td><td>2024-05-04 15:00:00.0000000</td><td>NULL</td><td>2024-04-11 20:00:00.0000000</td></tr><tr><td>228</td><td>2024-05-05 16:00:00.0000000</td><td>NULL</td><td>2024-04-11 20:00:00.0000000</td></tr><tr><td>228</td><td>2024-05-10 07:13:04.4900000</td><td>NULL</td><td>2024-04-11 20:00:00.0000000</td></tr><tr><td>229</td><td>2024-04-13 22:00:00.0000000</td><td>2024-04-24 12:00:00.0000000</td><td>2024-04-13 22:00:00.0000000</td></tr><tr><td>229</td><td>2024-04-14 23:00:00.0000000</td><td>NULL</td><td>2024-04-13 22:00:00.0000000</td></tr><tr><td>232</td><td>2024-04-17 12:00:00.0000000</td><td>NULL</td><td>2024-04-17 12:00:00.0000000</td></tr><tr><td>234</td><td>2004-04-03 12:00:00.0000000</td><td>2024-04-21 12:00:00.0000000</td><td>2004-04-03 12:00:00.0000000</td></tr><tr><td>234</td><td>2024-04-21 16:00:00.0000000</td><td>NULL</td><td>2004-04-03 12:00:00.0000000</td></tr><tr><td>234</td><td>2024-05-06 17:00:00.0000000</td><td>2024-05-10 15:00:00.0000000</td><td>2004-04-03 12:00:00.0000000</td></tr><tr><td>236</td><td>2024-04-08 17:00:00.0000000</td><td>NULL</td><td>2024-04-08 17:00:00.0000000</td></tr><tr><td>236</td><td>2024-04-12 21:00:00.0000000</td><td>NULL</td><td>2024-04-08 17:00:00.0000000</td></tr><tr><td>236</td><td>2024-04-24 19:00:00.0000000</td><td>2024-05-08 09:51:17.5333333</td><td>2024-04-08 17:00:00.0000000</td></tr><tr><td>237</td><td>2024-04-22 17:00:00.0000000</td><td>2024-05-06 11:00:00.0000000</td><td>2024-04-22 17:00:00.0000000</td></tr><tr><td>239</td><td>2024-04-07 16:00:00.0000000</td><td>NULL</td><td>2024-04-07 16:00:00.0000000</td></tr><tr><td>239</td><td>2024-04-23 18:00:00.0000000</td><td>NULL</td><td>2024-04-07 16:00:00.0000000</td></tr><tr><td>240</td><td>2024-04-10 19:00:00.0000000</td><td>NULL</td><td>2024-04-10 19:00:00.0000000</td></tr><tr><td>240</td><td>2024-04-16 11:00:00.0000000</td><td>2024-04-25 13:00:00.0000000</td><td>2024-04-10 19:00:00.0000000</td></tr><tr><td>241</td><td>2024-04-09 18:00:00.0000000</td><td>2024-04-23 11:00:00.0000000</td><td>2024-04-09 18:00:00.0000000</td></tr><tr><td>241</td><td>2024-04-15 10:00:00.0000000</td><td>NULL</td><td>2024-04-09 18:00:00.0000000</td></tr><tr><td>241</td><td>2024-04-28 23:00:00.0000000</td><td>NULL</td><td>2024-04-09 18:00:00.0000000</td></tr></table>




Powyższe zapytanie doda kolumnę `FirstLoanDate`, która pokazuje datę pierwszego wypożyczenia dla każdego użytkownika.

Funkcje `FIRST_VALUE` i `LAST_VALUE` są szczególnie użyteczne, gdy potrzebujemy analizować pierwsze lub ostatnie wartości w zestawie danych, na przykład przy tworzeniu raportów analitycznych lub przy ocenie trendów w danych historycznych.
