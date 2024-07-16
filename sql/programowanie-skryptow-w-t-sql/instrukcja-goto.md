# Instrukcja `GOTO`

Oprócz instrukcji, które w skryptach T-SQL sterują przepływem wykonywania kodu, takimi jak: instrukcja `IF..ELSE`, czy `TRY..CATCH`, mamy również instrukcję `GOTO`, która pozwala na skok do określonego miejsca w kodzie.

Instrukcja `GOTO` jest instrukcją bezwarunkową, co oznacza, że zawsze przenosi sterowanie do określonego miejsca w kodzie, niezależnie od tego, czy warunek jest spełniony, czy nie. Aby wykorzystać `GOTO`, musimy określić w kodzie etykietę, do której chcemy skoczyć. Etykieta jest to nazwa, zakończona znakiem dwukropka, która identyfikuje miejsce w kodzie, do którego chcemy przejść.

Wykorzystując instrukcję `GOTO` w połączeniu z instrukcją `IF`, możemy zaimplementować prosty mechanizm pętli w T-SQL, który wykona kawałek kodu, określoną ilość razy.


```sql
DECLARE @counter INT = 0;
loop: -- etykieta (label)
SET @counter = @counter + 1;
PRINT 'Hello World!';
IF @counter < 5
BEGIN
    GOTO loop;
END
```

Ten prosty mechanizm, możemy np. wykorzystać w celu dodania określonej ilości rekordów do tabeli. Poniższa procedura dodaje do tabeli `Copies`, określoną ilość nowych kopii książki o podanym `BookId`. 




```sql
CREATE PROCEDURE AddCopies
    @BookId INT,
    @Count INT
AS
BEGIN
    DECLARE @i INT = 0;
add_copies_loop:
    IF @i < @Count
    BEGIN
        INSERT INTO Copies (BookId, Condition) 
        VALUES (@BookId, 'New');
        SET @i = @i + 1;
        GOTO add_copies_loop;
    END
END
```

### Kiedy używać `GOTO`

Mimo, że instrukcja `GOTO` jest bardzo prosta, to przez to, że możne ona w dowolny sposób zmieniać kolejność wykonywania skryptu, nie jest zalecane jej używanie - jako, że taki kod ciężko się czyta i utrzymuje. Zamiast tego, zaleca się używanie pętli i instrukcji warunkowych, aby zwiększyć czytelność kodu i swobodnie sterować przepływem skryptu, jeżeli jest taka potrzeba.
