## Transakcje

W MS SQL, transakcje są jednym z najważniejszych elementów, które pozwalają na kontrolowanie spójności danych w bazie. Transakcje pozwalają na wykonywanie wielu operacji jako jedną operację. W przypadku, gdy jedna z operacji zawartych w transakcji nie powiedzie się, to cała transakcja zostaje cofnięta, a baza danych pozostaje w spójnym stanie.

Transakcje w MS SQL są realizowane za pomocą instrukcji `BEGIN TRANSACTION` (lub w skrócie `BEGIN TRAN`), `COMMIT` oraz `ROLLBACK`. Instrukcja `BEGIN TRANSACTION` rozpoczyna nową transakcję, `COMMIT` zatwierdza zmiany dokonane w trakcie transakcji, a `ROLLBACK` cofa zmiany dokonane w trakcie transakcji.

Przykład:

```
BEGIN TRANSACTION
UPDATE table_name
SET column1 = value1
WHERE condition;

UPDATE table_name
SET column2 = value2
WHERE condition;

COMMIT;

```

W powyższym przykładzie, zmiany dokonane w tabeli `table_name` zostaną zatwierdzone, jeżeli obie operacje `UPDATE` zostaną wykonane poprawnie. W przeciwnym wypadku, zmiany zostaną cofnięte, albo przynajmniej tak by się mogło wydawać.

Rozważmy poniższy przykład:


```sql
BEGIN TRAN

INSERT INTO Authors (FirstName, LastName, BirthDate, Country)
VALUES ('Haruki', 'Murakami', '1949-01-12', 'Japan');

Declare @authorId INT = SCOPE_IDENTITY()

Declare @genreId INT = (SELECT TOP 1 GenreId FROM Genres WHERE [Name] = 'Historical') -- NULL

INSERT INTO Books (Title, Description, PublicationDate, ISBN, AuthorId, GenreId)
VALUES ('New Historical book', 'A first book in the series', '2020-03-03', '95532123423', @authorId, @genreId) -- Dla @genreId NULL wystąpi błąd


COMMIT
```


(1 row affected)





The statement has been terminated.



Total execution time: 00:00:00.005


## Flaga `XACT_ABORT`

W MS SQL Serverze flaga `XACT_ABORT` jest domyślnie wyłączona (wartość `OFF`). Oznacza to, że w przypadku błędu w trakcie wykonywania transakcji, błąd jest zwracany, ale transakcja nie jest anulowana. W takim przypadku, jeśli nie zostanie ręcznie anulowana poleceniem `ROLLBACK`, to zostanie zakończona po wykonaniu ostatniej instrukcji. To właśnie przez to w powyższym przykładzie autor, którego dodawaliśmy w ramach transkacji, podczas której wystąpił błąd, został dodany do bazy danych.

Aby zapobiec takiej sytuacji, musielibyśmy ręcznie anulować transkację w przypadku wystąpienia błędu poleceniem `ROLLBACK` - w bloku `TRY ... CATCH`:

Albo, możemy też włączyć flagę `XACT_ABORT`, która automatycznie anuluje transakcję w przypadku wystąpienia błędu. Wtedy nie musimy ręcznie anulować transakcji w bloku `TRY ... CATCH`. Flagę tę można włączyć poleceniem `SET XACT_ABORT ON`:

Rozważmy ten sam przykład, ale z włączoną flagą `XACT_ABORT`:



```sql
SET XACT_ABORT ON;
BEGIN TRAN

INSERT INTO Authors (FirstName, LastName, BirthDate, Country)
VALUES ('Akira', 'Toriyama', '1955-04-05', 'Japan');

Declare @authorId INT = SCOPE_IDENTITY()

Declare @genreId INT = (SELECT TOP 1 GenreId FROM Genres WHERE [Name] = 'Historical') -- NULL

INSERT INTO Books (Title, Description, PublicationDate, ISBN, AuthorId, GenreId)
VALUES ('New Historical book', 'A first book in the series', '2020-03-03', '95532123423', @authorId, @genreId) -- Dla @genreId NULL wystąpi błąd


COMMIT
```


(1 row affected)





Total execution time: 00:00:00.004


## Kluczowe cechy transakcji

Transakcje w MS SQL posiadają kilka kluczowych cech, które charakteryzują transakcje w systemach baz danych. Są to:

1. **Atomowość (Atomicity)**: Oznacza, że transakcja jest atomowa, czyli jednostką niepodzielną. Wszystkie operacje w ramach transakcji muszą zostać wykonane w całości albo wcale. 
    
2. **Spójność (Consistency)**: Oznacza, że transakcja musi zachować spójność danych. Wszystkie ograniczenia integralności danych muszą zostać zachowane przed i po zakończeniu transakcji. W rezultacie, baza danych musi pozostać w spójnym stanie, niezależnie od tego, czy transakcja zakończyła się powodzeniem czy nie.
    
3. **Izolacja (Isolation)**: Oznacza, że ​​transakcje powinny być izolowane od siebie nawzajem. To zapobiega zakłóceniom i zapewnia, że jedna transakcja nie będzie miała wpływu na wyniki innych transakcji, które są jednocześnie wykonywane. Różne poziomy izolacji transakcji, takie jak Read Uncommitted, Read Committed, Repeatable Read i Serializable, kontrolują stopień izolacji między transakcjami.
    
4. **Trwałość (Durability)**: Oznacza, że po zatwierdzeniu transakcji (za pomocą COMMIT), zmiany wprowadzone przez tę transakcję muszą być trwałe i nieodwracalne. Nawet w przypadku awarii systemu, baza danych musi zagwarantować, że zatwierdzone zmiany zostaną zachowane. To oznacza, że system musi utrzymywać kopię zapasową danych lub zapisywać zmiany na trwałym nośniku, aby mogły być przywrócone w przypadku awarii.
    

Cechy te (ACID) są kluczowe dla zapewnienia integralności, spójności i niezawodności danych w systemach baz danych. Dzięki nim transakcje są nie tylko bezpieczne, ale także skuteczne w utrzymaniu integralności danych.
