# Funkcje `FIRST_VALUE` i `LAST_VALUE`

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


Powyższe zapytanie doda kolumnę `FirstLoanDate`, która pokazuje datę pierwszego wypożyczenia dla każdego użytkownika.

Funkcje `FIRST_VALUE` i `LAST_VALUE` są szczególnie użyteczne, gdy potrzebujemy analizować pierwsze lub ostatnie wartości w zestawie danych, na przykład przy tworzeniu raportów analitycznych lub przy ocenie trendów w danych historycznych.
