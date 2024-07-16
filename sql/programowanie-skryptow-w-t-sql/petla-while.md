# Pętla `WHILE`

Zdarza się, że w skryptach, które tworzymy mamy potrzebę wykonania jakiegoś fragmentu kodu wielokrotnie. W takich sytuacjach przydaje się pętla `WHILE`. Pętla ta wykonuje blok kodu dopóki spełniony jest konkretny warunek. Jeżeli warunek nie będzie spełniony, to pętla nie wykona swojego bloku kodu.

Przykładowo, aby wykonać dany kawałek kodu 10 razy, możemy posłużyć się zmienną, która będzie przechowywała wartość licznika, który będzie zwiększany o 1 w każdym obiegu pętli. W momencie, gdy licznik osiągnie wartość 10, pętla zakończy swoje działanie.


```sql
DECLARE @counter INT = 1;
WHILE @counter <= 10
BEGIN
    -- wyświetlenie aktualnej wartości licznika
    PRINT @counter;

    -- zwiększenie licznika o 1
    SET @counter = @counter + 1;
END
PRINT 'Koniec skryptu'
```

W powyższym przykładzie pętla zakończy się, kiedy zmienna `@counter` osiągnie wartość 11.





### Instrukcja `BREAK`



Pętle możemy zakończyć wcześniej, niż wynikałoby to z warunku logicznego. W tym celu służy instrukcja `BREAK`. Przykład:






```sql
DECLARE @counter INT = 1;
WHILE @counter <= 10
BEGIN
    IF @counter = 7
    BEGIN
        PRINT 'Jawny koniec wykonywania pętli'
        BREAK -- natychmiastowe zakończenie pętli
    END

    -- wyświetlenie aktualnej wartości licznika
    PRINT @counter;

    -- zwiększenie licznika o 1
    SET @counter = @counter + 1;
END
PRINT 'Koniec skryptu'
```

Tym razem pętla przerwie swoje działanie, jeszcze przed wypisaniem wartości 7





### Instrukcja `CONTINUE`



Oprócz natychmiastowego przerwania pętli instrukcją `BREAK`, mamy również możliwość natychmiastowego przejścia do kolejnej iteracji pętli, za pomocą instrukcji `CONTINUE`. Jednak korzystając z `CONTINUE` oraz wartości licznika, musimy pamiętać o tym, aby zwiększyć wartość licznika o 1, w przeciwnym wypadku pętla będzie nieskończona.










```sql
DECLARE @counter INT = 1;
WHILE @counter <= 10
BEGIN
    IF @counter % 2 = 0
    BEGIN 
        PRINT 'Pominięcie pętli dla wartości parzystych'
        SET @counter = @counter + 1 -- zwiększenie licznika, aby uniknać pętli nieskończonej
        CONTINUE
    END
    IF @counter = 7
    BEGIN
        PRINT 'Jawny koniec wykonywania pętli'
        BREAK -- natychmiastowe zakończenie pętli
    END

    -- wyświetlenie aktualnej wartości licznika
    PRINT @counter;

    -- zwiększenie licznika o 1
    SET @counter = @counter + 1;
END
PRINT 'Koniec skryptu'
```


1



Pominiecie petli dla wartosci parzystych



3



Pominiecie petli dla wartosci parzystych



5



Pominiecie petli dla wartosci parzystych



Jawny koniec wykonywania petli



Koniec skryptu



Total execution time: 00:00:00


## Zadanie praktyczne



Wykorzystując pętle `WHILE` napisz procedure, która przyjmuje dwa parametry:

- `BookId` - identyfikator książki

- `NewCopiesCount` - liczba nowych kopii książki



Procedura ma zwiększyć liczbę kopii książki, dodając nowe (`Condition = 'New'`) o `NewCopiesCount` w bazie danych, z tym, że całkowita liczba kopii książki nie może przekroczyć 10.



Przykładowo, dla książki `BookId = 1`, która aktualnie ma 7 kopii, jeśli procedura zostanie wywołana z parametrami `BookId = 1` i `NewCopiesCount = 5`, to liczba kopii książki powinna zostać zwiększona do 10.





Natomiast jeśli książka ma ponownie 7 kopii i procedura zostanie wywołana z parametrami,  `BookId = 1`, `NewCopiesCount = 2`, to liczba kopii książki powinna zostać zwiększona do 9.



Dla książek, które mają już 10 kopii lub więcej, procedura nie powinna dodawać nowych kopii.



Całość przetestuj na przykładowych danych, w różnych scenariuszach.




```sql
-- ROZWIĄZANIE
CREATE PROCEDURE IncreaseCopies
    @BookId INT,
    @NewCopiesCount INT
AS 
BEGIN
    DECLARE @CurrentCopies INT
    SELECT @CurrentCopies = COUNT(*)
    FROM Copies
    WHERE BookId = @BookId
    IF @CurrentCopies + @NewCopiesCount > 10
        SET @NewCopiesCount = 10 - @CurrentCopies
    DECLARE @i INT = 0
    WHILE @i < @NewCopiesCount
    BEGIN

        -- dodatkowe zabezpieczenie
        SELECT @CurrentCopies = COUNT(*)
        FROM Copies
        WHERE BookId = @BookId
        IF @CurrentCopies >= 10
            BREAK
        ---------
        INSERT INTO Copies (BookId, Condition)
        VALUES (@BookId, 'New')
        SET @i = @i + 1
    END
END
```
