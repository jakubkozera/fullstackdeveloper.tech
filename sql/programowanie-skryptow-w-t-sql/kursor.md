# Kursor

Pętlę `WHILE`, możemy też wykorzystać w połączeniu z kursorem. W SQL Serverze kursor to mechanizm, który pozwala na iterowanie po zbiorze wierszy zwróconych przez zapytanie. Jest to przydatne, gdy mamy potrzebę przetwarzać dane wiersz po wierszu, na przykład wykonując operacje lub obliczenia na każdym wierszu osobno.

Aby zdefiniować kursor, posłużymy się następującym poleceniem:

```
DECLARE cursor_name CURSOR FOR
SELECT column1, column2, ...
FROM table_name
WHERE condition;

```

Gdzie `cursor_name` to nazwa kursora, `column1, column2, ...` to kolumny, które chcemy zwrócić, `table_name` to nazwa tabeli, a `condition` to warunek, który chcemy zastosować do zwróconych wierszy.

Następnie otwieramy kursor i pobieramy pierwszy wiersz za pomocą polecenia `FETCH`:

```
OPEN cursor_name;
FETCH NEXT FROM cursor_name INTO @variable1, @variable2, ...;

```

Gdzie `@variable1, @variable2, ...` to zmienne, do których chcemy przypisać wartości zwrócone przez kursor - tak więc musimy najpierw zadeklarować te zmienne, zanim użyjemy ich w poleceniu `FETCH`, odpowiednio do typów danych zwracanych przez kursor.

Sama operacja `FETCH`, która wybiera kolejny wiersz, zwraca wartość `0`, jeśli wiersz został pomyślnie pobrany, `-1`, jeśli nie ma więcej wierszy do pobrania, a `-2`, jeśli wystąpił błąd. Ta informacja jest przechowywana w zmiennej systemowej `@@FETCH_STATUS` i posłuży nam do sprawdzenia, czy mamy więcej wierszy do przetworzenia.

W zależności od wartości `@@FETCH_STATUS` możemy przetwarzać wiersze w pętli `WHILE`:

```
WHILE @@FETCH_STATUS = 0
BEGIN
    -- Operacje na wierszu
    FETCH NEXT FROM cursor_name INTO @variable1, @variable2, ...;
END

```

Po zakończeniu przetwarzania wierszy, zamykamy i usuwamy kursor, aby zwolnić zasoby:

```
CLOSE cursor_name;
DEALLOCATE cursor_name;

```

Całościowo, utworzonie, użycie, a następnie zamknięcie kursora wygląda tak:

```
DECLARE @variable1 datatype1, @variable2 datatype2, ...

DECLARE cursor_name CURSOR FOR
SELECT column1, column2, ...
FROM table_name
WHERE condition;


OPEN cursor_name;
FETCH NEXT FROM cursor_name INTO @variable1, @variable2, ...;

WHILE @@FETCH_STATUS = 0
BEGIN
    -- Operacje na wierszu
    FETCH NEXT FROM cursor_name INTO @variable1, @variable2, ...;
END

CLOSE cursor_name;
DEALLOCATE cursor_name;
```

### Przykładowe użycie kursora

Oto przykładowe użycie kursora na podstawie schematu bazy danych LibraryDatabase. Załóżmy, że chcemy napisać procedurę składowaną, która wyświetla informacje o autorach i ilości ich książek:


```sql
CREATE PROCEDURE ShowAuthorBookCounts
AS
BEGIN
    DECLARE @AuthorId INT
    DECLARE @FirstName NVARCHAR(50)
    DECLARE @LastName NVARCHAR(50)
    DECLARE @BookCount INT

    -- Deklaracja kursora
    DECLARE authorCursor CURSOR FOR
    SELECT AuthorId, FirstName, LastName
    FROM Authors
    -- Otwarcie kursora
    OPEN authorCursor

    -- Pobranie pierwszego wiersza
    FETCH NEXT FROM authorCursor INTO @AuthorId, @FirstName, @LastName

    -- Pętla przetwarzająca wiersze
    WHILE @@FETCH_STATUS = 0
    BEGIN

        -- Obliczenie liczby książek dla danego autora
        SELECT @BookCount = COUNT(*)
        FROM Books
        WHERE AuthorId = @AuthorId

        -- Wyświetlenie informacji
        PRINT 'Author: ' + @FirstName + ' ' + @LastName + ', Book Count: ' + CAST(@BookCount AS NVARCHAR(10))
        
        -- Pobranie kolejnego wiersza
        FETCH NEXT FROM authorCursor INTO @AuthorId, @FirstName, @LastName
    END

    -- Zamknięcie kursora
    CLOSE authorCursor
    DEALLOCATE authorCursor
END
```


```sql
EXEC ShowAuthorBookCounts
```



Ta procedura składowana otwiera kursor, pobiera informacje o autorach, a następnie dla każdego autora oblicza liczbę książek, które napisał i wyświetla te informacje. Na koniec zamyka i usuwa kursor.



Zwróć uwagę, że używając kursorów w SQL, należy zachować ostrożność, ponieważ mogą one wpływać na wydajność zapytań, szczególnie przy dużych zbiorach danych. Wiele operacji wykonywanych z użyciem kursorów może być zwykle zastąpionych przez zapytania zbiorcze, co może być bardziej wydajne.
