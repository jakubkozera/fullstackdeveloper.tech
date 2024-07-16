## Procedury składowane

Procedury składowane w bazach danych Microsoft SQL Server to zestawy instrukcji SQL, które są przechowywane i kompilowane raz, a następnie mogą być wywoływane wielokrotnie przez różne części aplikacji. Tak więc w pewnym sensie są one podobne do funkcji, natomiast różnią się od nich znacząco.

### Funkcje a procedury składowane

Główne róźnice między funkcją, a procedurą składowaną są następujące:

| Funkcja (Function) | Procedura składowana (Stored Procedure) |
| --- | --- |
| Zwraca pojedynczą wartość, zarówno jako tabelę, jak i skalarną. | Może zwrócić zero, pojedynczą wartość lub wiele wartości. |
| Kompilacja i wykonanie odbywają się w czasie wykonywania dla funkcji. | Baza danych zawiera procedury składowane, które zostały sparsowane i skompilowane. |
| Dozwolone są tylko instrukcje SELECT. Instrukcje DML (UPDATE/DELETE/INSERT) są niedozwolone. | Może wykonywać dowolne operacje na obiektach bazy danych, takie jak instrukcje DML i SELECT. |
| Dozwolone są tylko parametry wejściowe. Parametry wyjściowe nie są obsługiwane. | Obsługiwane są zarówno parametry wejściowe, jak i wyjściowe. |
| Nie zezwala na użycie bloków Try...Catch do obsługi wyjątków. | Pozwala na użycie bloków Try...Catch do obsługi wyjątków. |
| Transakcje nie są dozwolone w funkcji. | Procedura składowana może zawierać transakcje. |
| Funkcja nie może wywołać procedury składowanej. | Procedura składowana może być wywołać funkcje, lub inne procedury. |
| Instrukcje SELECT mogą wywoływać funkcje. | Procedury składowane nie mogą być dostępne przez wywołane przez  SELECT/WHERE lub HAVING.<br>Aby uruchomić procedurę składowaną, używamy polecenie EXECUTE (EXEC). |
| W klauzulach JOIN można używać funkcji. | Klauzule JOIN nie mogą używać procedur składowanych. |

Ze względu na te róźnice, procedury składowane są bardziej elastyczne niż funkcje, ale mogą być mniej wydajne. W związku z tym, zaleca się stosowanie funkcji, jeśli chcemy zwrócić pojedynczą wartość, a procedurę składowaną, jeśli chcemy zwrócić wiele wartości, albo wykonać operacje na obiektach bazy danych.

### Tworzenie procedury składowanej

Procedury składowane tworzymy za pomocą polecenia `CREATE PROCEDURE`. Poniżej znajduje się przykład tworzenia procedury składowanej, która zwraca wszystkie rekordy z tabeli `Users`:


```sql
CREATE PROCEDURE GetAllUsers
AS
BEGIN
    SELECT * FROM Users
END

```

W powyższym przykładzie `GetAllUsers` to nazwa procedury składowanej, a `SELECT * FROM Users` to instrukcja SQL, która zwraca wszystkie rekordy z tabeli `Users`. W przeciwieństwie do funkcji, procedura składowana nie zwraca wartości, ale zwraca wynik zapytania SQL, którego nie musimy jawnie określać, jak to miało miejsce w przypadku definicji funkcji.

Aby wywołać procedurę składowaną, używamy polecenia `EXECUTE`:




```sql
EXECUTE GetAllUsers

```


Procedury, podobnie jak funkcje, mogą przyjmować parametry. Poniżej znajduje się przykład procedury składowanej, która przyjmuje parametr `UserId` i zwraca rekord z tabeli `Users` dla danego `UserId`:




```sql
CREATE PROCEDURE GetUserById
    @UserId INT
AS  
BEGIN
    SELECT * FROM Users WHERE UserId = @UserId
END

```


Wywołanie procedury składowanej z parametrem wygląda następująco:




```sql
EXEC GetUserById 1
-- lub 
DECLARE @param INT = 1 
EXECUTE GetUserById @param

EXECUTE GetUserById @UserId = @param
```

### Parametry wyjściowe

Dodatkową cechą, która nie była dostępna przy użyciu funkcji, jest możliwość definiowania parametrów wyjściowych. Parametry wyjściowe są zwracane przez procedurę składowaną i mogą być przypisane do zmiennej.

Przykładowo, procedura składowana, która aktualizuje stan egzemplarza książki w bazie danych, na podstawie `UserId`, może też zwrócić liczbę aktualizowanych rekordów.



```sql
CREATE PROCEDURE UpdateBookCopyCondition
    @UserId INT,
    @NewCondition NVARCHAR(100),
    @UpdatedRecordCount INT OUTPUT
AS
BEGIN
    -- Updating the condition of book copies for the given user
    UPDATE Copies
    SET Condition = @NewCondition
    FROM Copies
    INNER JOIN Loans ON Copies.CopyId = Loans.CopyId
    WHERE Loans.UserId = @UserId

    -- Returning the number of updated records
    SET @UpdatedRecordCount = @@ROWCOUNT
END;
```


Commands completed successfully.



Total execution time: 00:00:00.003


`@@ROWCOUNT` - zmienna systemowa, która przechowuje liczbę zaktualizowanych rekordów w ostatnim zapytaniu `UPDATE` lub `DELETE`. W przypadku zapytania `SELECT` zwraca liczbę zwróconych rekordów.

Parametry:
- `@UserId`: Identyfikator użytkownika, dla którego mają zostać zaktualizowane egzemplarze książki.
- `@NewCondition`: Nowy stan, który ma być przypisany do egzemplarzy książki.
- `@UpdatedRecordCount`: Parametr wyjściowy, który zwraca liczbę zaktualizowanych rekordów.

Wywołanie tej procedury, wygląda następująco:


```sql
DECLARE @UserId INT = 228; -- Example user ID
DECLARE @NewCondition NVARCHAR(100) = 'Good'; -- Example new condition

DECLARE @UpdatedRecordCount INT;

-- Execute the stored procedure
EXEC UpdateBookCopyCondition 
    @UserId = @UserId,
    @NewCondition = @NewCondition,
    @UpdatedRecordCount = @UpdatedRecordCount OUTPUT;

-- Output the number of updated records
PRINT 'Number of updated records: ' + CAST(@UpdatedRecordCount AS NVARCHAR(10));

```


(1 row affected)



Number of updated records: 1



Total execution time: 00:00:00.004


### Modyfikacja implementacji procedury

Aby zmienić aktualną implementację procedury, możemy to zrobić podobnie jak przy modyfikacji funkcji: albo usunąc i dodając nową, albo nadpisać istniejącą. 

W celu usunięcia definicji procedury, należy użyć komendy `DROP PROCEDURE`:



```sql
DROP PROCEDURE GetAllUsers
```




Total execution time: 00:00:00


Natomiast poleceniem `ALTER PROCEDURE` możemy zmienić definicję procedury



```sql
ALTER PROCEDURE UpdateBookCopyCondition
    @UserId INT,
    @NewCondition NVARCHAR(100),
    @UpdatedRecordCount INT OUTPUT
AS
BEGIN
    -- Updating the condition of book copies for the given user
    UPDATE Copies
    SET Condition = @NewCondition
    FROM Copies
    INNER JOIN Loans ON Copies.CopyId = Loans.CopyId
    WHERE Loans.UserId = @UserId AND ReturnDate IS NOT NULL -- new logic


    -- Returning the number of updated records
    SET @UpdatedRecordCount = @@ROWCOUNT
END;
```


Commands completed successfully.



Total execution time: 00:00:00.001


## Zadanie

1. Stwórz procedurę składowaną, która na podstawie tytułu książki oraz identyfikatora użytkownika rezerwuje dostępny egzemplarz (`Copy`) danej książki i tworzy wpis w tabeli `Loans`. Procedura ma zwracać informację o tym, czy wypożyczenie zostało wykonane, pod postacią wartości typu `BIT`. Całość przetestuj, dla tytułów, które zarówno mają dostępne aktualnie egzemplarze, jak i nie mają ich.


```sql
-- ROZWIĄZANIE

CREATE PROCEDURE LoanBook
    @UserId INT,
    @BookTitle NVARCHAR(255),
    @LoanSuccess BIT OUTPUT
AS
BEGIN
    DECLARE @CopyId INT
    SELECT TOP 1 @CopyId = CopyId
    FROM Copies c
    INNER JOIN Books b on b.BookId = c.BookId
    WHERE b.Title = @BookTitle AND CopyId NOT IN (
        SELECT CopyId
        FROM Loans
        WHERE c.CopyId = CopyId
            AND LoanDate < GETDATE()
            AND ReturnDate IS NULL
    ) 
    IF @CopyId IS NOT NULL
    BEGIN
        INSERT INTO Loans (UserId, CopyId, LoanDate)
        VALUES (@UserId, @CopyId, GETDATE())
        SET @LoanSuccess = 1
    END
    ELSE
    BEGIN
        SET @LoanSuccess = 0
    END
END

```

2. Napisz procedurę składowaną, która generuje raport o wypożyczonych książkach na podstawie ilości dni, które upłynęły od wypożyczenia jako parametr wejściowy.

Raport powinien zawierać informacje o tym, kto, kiedy i co wypożyczył: (użytkownik, tytuł, data wypożyczenia)

Procedura powinna również zwracać liczbę egzemplarzy książek (parametr wyjściowy), które zostały wypożyczone na tyle dni lub dłużej.


```sql
-- ROZWIĄZANIE

CREATE PROCEDURE GenerateLoanedBooksReport
    @DaysSinceLoan INT,
    @NumberOfLoanedBooks INT OUTPUT
AS
BEGIN
    SELECT l.LoanId, u.Name + ' ' + u.Surname as [UserName], b.Title, l.LoanDate
    FROM Loans l
    JOIN Users u on l.UserId = u.UserId
    JOIN Copies c on l.CopyId = c.CopyId
    JOIN Books b on c.BookId = b.BookId
    WHERE DATEDIFF(DAY, l.LoanDate, GETDATE()) >= @DaysSinceLoan
    AND l.ReturnDate IS NULL
    SET @NumberOfLoanedBooks = @@ROWCOUNT
END

```
