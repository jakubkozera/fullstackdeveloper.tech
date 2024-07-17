# Instrukcje warunkowe

Czasem w naszych skryptach SQL będziemy mieli potrzebę wykonać róźne polecenia SQL, w zależności od jakiegoś warunku, lub inaczej mówiąc, będziemy musieli sterować przepływem egzekucji kodu.
Taką potrzebę zaspokoi nam instrukcja warunkowa.

Instrukcja warunkowa w T-SQL (Transact-SQL) to mechanizm programowania używany do wykonywania różnych działań w zależności od spełnienia określonych warunków. Najczęściej używaną instrukcją warunkową w T-SQL jest `IF`, lub jej wersje `IF..ELSE`, czy nawet bardziej rozbudowane `IF..ELSEIF..ELSE`.

## Instruckja `IF`

Instrukcja `IF` w T-SQL służy do sprawdzenia, czy określony warunek jest spełniony. Jeśli warunek jest spełniony, kod wewnątrz bloku `BEGIN` i `END` zostanie wykonany. Jeśli warunek nie jest spełniony, kod wewnątrz bloku `BEGIN` i `END` zostanie pominięty.

Składnia instrukcji `IF` wygląda następująco:

```
IF warunek
BEGIN
    -- Kod do wykonania, jeśli warunek jest spełniony
END

```

Przykładowo, jeżeli istnieje użytkownik, który jeszcze nie zwrócił książek, to dla takiego użytkownika możemy zaktualizować datę zwrotu wypożyczeń.

W przeciwnym wypadku, czyli jeśli wszystkie książki zostały już zwrócone, blok kodu między `BEGIN` i `END` nie zostanie wykonany.





```sql
DECLARE @UserId INT;
SELECT TOP 1 @UserId = UserId
FROM Loans
WHERE ReturnDate IS NULL
GROUP BY UserId
ORDER BY COUNT(*) DESC

IF @UserId IS NOT NULL
BEGIN
    PRINT 'Aktualizacja ReturnDate'
    UPDATE Loans
    SET ReturnDate = GETDATE()
    WHERE UserId = @UserId
END
```


Aktualizacja ReturnDate



## Instrukcja `IF ELSE`



Do instrukcji `IF` możemy dopisać też blok `ELSE`, który zostanie wykonany, jeśli warunek w `IF` nie zostanie spełniony. 



  

```
IF warunek
BEGIN
    -- Kod do wykonania, jeśli warunek jest spełniony
END
ELSE
BEGIN
    -- Kod do wykonania, jeśli warunek nie jest spełniony
END
```

Przykładowo, dodanie nowego egzemplarza `The Hobbit`, lub aktualizacji stanu istniejących w zależności od liczby dostępnych egzemplarzy w bazie danych:




```sql
DECLARE @theHobbitId INT = (SELECT BookId FROM Books WHERE Title = 'The Hobbit')
DECLARE @theHobbitCopiesCount INT = (SELECT COUNT(CopyId) FROM Copies WHERE BookId = @theHobbitId)
IF @theHobbitCopiesCount > 5
BEGIN 
    PRINT 'Aktualizacja egzemplarzy'
    UPDATE Copies
    SET Condition = 'Good'
    WHERE BookId = @theHobbitId
END
ELSE 
BEGIN
    PRINT 'Dodawanie nowego egzemplarza'
    INSERT INTO Copies (Condition, BookId)
    VALUES ('Ok', @theHobbitId)
END
```


Dodawanie nowego egzemplarza


## Instrukcja `IF ELSE IF ELSE`



W przypadku, gdy mamy do czynienia z wieloma warunkami, które chcemy sprawdzić, możemy skorzystać z instrukcji `IF ELSE IF ELSE`. Instrukcja ta pozwala na sprawdzenie wielu warunków, z których tylko jeden może być spełniony.



Poniższy przykład wyświetli 'Sobota', 'Niedziela' lub 'Inny dzień tygodnia' w zależności od wartości zmiennej `dzienTygodnia`.



```sql
DECLARE @dzienTygodnia INT = 1
IF @dzienTygodnia = 6
BEGIN
    PRINT 'Sobota'
END
ELSE IF @dzienTygodnia = 7
BEGIN
    PRINT 'Niedziela'
END
ELSE
BEGIN
    PRINT 'Inny dzień tygodnia'
END
```



Tylko jeden z bloków `IF`, `ELSE IF` lub `ELSE` zostanie wykonany. W powyższym przykładzie, jeśli wartość zmiennej `dzienTygodnia` wynosi 6, zostanie wyświetlony napis 'Sobota'. Jeśli wartość zmiennej wynosi 7, zostanie wyświetlony napis 'Niedziela'. W przeciwnym przypadku zostanie wyświetlony napis 'Inny dzień tygodnia'.




```sql
DECLARE @userId INT, @totalLoans INT;
SELECT TOP 1 @userId = UserId, @totalLoans = COUNT(*) 
FROM Loans
GROUP BY UserId
ORDER BY COUNT(*) DESC
SELECT @userId, @totalLoans
IF @totalLoans > 5
BEGIN
    PRINT 'Usuwanie wpisu wypożyczeń'
    DELETE FROM Loans 
    WHERE UserId = @userId AND CopyId IN (SELECT CopyId 
                                          FROM Copies
                                          WHERE Condition != 'Good')
END
ELSE IF @totalLoans > 3
BEGIN
    PRINT 'Aktualizacja stanu egzemplarzy'
    UPDATE Copies
    SET Condition = 'Ok'
    WHERE CopyId IN (SELECT CopyId FROM Loans WHERE UserId = @userId)
END
ELSE
BEGIN
    PRINT 'Dodawanie nowego wypożyczenia'
    DECLARE @leastLoanedCopyId INT = (SELECT TOP 1 CopyId 
                                      FROM Loans
                                      GROUP BY CopyId
                                      ORDER BY COUNT(*))
    INSERT INTO Loans (UserId, CopyId, LoanDate)
    VALUES (@userId, @leastLoanedCopyId, GETDATE())
END
```


Aktualizacja stanu egzemplarzy



W zależności od złóżoności logiki biznesowej, instrukcję `ELSE IF` można powielać, aby sprawdzić więcej warunków, a sama instrukcja `ELSE` nie jest obowiązkowa.


## Zadanie



Napisz skrypt, który sprawdzi, czy aktualnie jest więcej książek wypożyczonych, jeszcze nie oddanych, niż tych, które zostały już zwrócone. W zależności od wyniku, skrypt powinien wyświetlić odpowiedni komunikat o ile jest więcej książek zostało już zwrócone lub jeszcze nie.



Przykładowo, jeżeli w bazie było 5 wypożyczonych książek, z czego 3 zostały już zwrócone, a 2 jeszcze nie -  to skrypt powinien wyświetlić komunikat "Wypożyczono o 1 więcej książek, które zwrócono".



Aby poprawnie wyświetlić komunikat, to do konwersji zmiennej liczbowej na typ tekstowy użyj funkcji `CONVERT(NVARCHAR, @zmiennaTypuInt)`.


<details><summary>Rozwiązanie</summary>

```sql
DECLARE @returnedCopiesCount INT, @notReturnedCopiesCount INT;
SET @returnedCopiesCount = (SELECT COUNT(*) FROM Loans WHERE ReturnDate IS NOT NULL)
SET @notReturnedCopiesCount = (SELECT COUNT(*) FROM Loans WHERE ReturnDate IS NULL)
PRINT @returnedCopiesCount
PRINT @notReturnedCopiesCount
IF @returnedCopiesCount > @notReturnedCopiesCount
BEGIN
    DECLARE @difference INT = @returnedCopiesCount - @notReturnedCopiesCount
    PRINT 'Zwrócono o' + CONVERT(NVARCHAR, @difference) + ' więcej niż wypożoczono'
END
ELSE IF @returnedCopiesCount = @notReturnedCopiesCount
BEGIN 
    PRINT 'Zwrócono tyle samo książek, co jeszcze nie zwrócono'
END
ELSE 
BEGIN
    DECLARE @differenceNotReturned INT = @notReturnedCopiesCount - @returnedCopiesCount
    PRINT 'Nie zwrócono o ' + CONVERT(NVARCHAR, @differenceNotReturned) + ' więcej niż do tej pory zwrócono'
END
```


13



19



Nie zwrócono o6 wiecej niz do tej pory zwrócono

</details>

