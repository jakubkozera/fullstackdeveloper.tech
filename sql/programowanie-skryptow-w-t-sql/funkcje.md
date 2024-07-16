# Funkcje

Jeśli mamy pewną logikę do obliczania konkretnej wartości, lub zwracania rezultatów w postaci tabeli na podstawie wartości zmiennych, to, żeby nie powielać tej logiki za każdym razem, w Microsoft SQL Server możemy do tego celu wykorzystać funkcje. Funkcje to nazwane bloki kodu, które wykonują określone operacje i zwracają wartość. Mogą one przyjmować argumenty (inaczej parametry), przetwarzać je i zwracać pojedyńczą wartość lub tablicę wartości.&nbsp;</span> 

Rodzaje funkcji w SQL Server to:

1. **Funkcje zdefiniowane przez system**:
    
    - **Funkcje agregujące**: Wykonują operacje agregujące na zestawie wartości, np. `SUM(), AVG(), MAX(), MIN()`.
    - **Funkcje okna**: Obliczają wartość dla każdego wiersza zestawu wynikowego, uwzględniając określone okno wierszy, np. `ROW_NUMBER(), RANK(), NTILE()`.
2. **Funkcje zdefiniowane przez użytkownika (UDF)**:
    
    - **Funkcje skalarne**: Zwracają pojedynczą wartość dla każdego wiersza w zapytaniu.
    - **Funkcje tablicowe**: Zwracają zestaw wartości w formie tabeli.

### Funkcje skalarane

Tworzenie funkcji zdefiniowanych przez użytkownika w SQL Server wymaga zdefiniowania ciała funkcji za pomocą języka T-SQL. Oto przykład tworzenia prostej funkcji skalarnych w SQL Server:

```
CREATE FUNCTION NazwaFunkcji (@ArgumentTypu1 Typ1, @ArgumentTypu2 Typ2, ...)
RETURNS TypZwracany
AS
BEGIN
    -- Ciało funkcji
    DECLARE @wynik TypZwracany;

    -- Logika funkcji
    -- Przypisanie wartości do @wynik

    RETURN @wynik;
END;

```

Aby użyć funkcji, można ją wywołać w zapytaniu lub innej procedurze, podając jej argumenty. Co więcej w przypadku funkcji skalarnych, musimy podać schemat `dbo` przed nazwą funkcji.

Na przykład:

```
SELECT dbo.NazwaFunkcji(Kolumna1, Kolumna2) AS Wynik FROM Tabela;

```

Przykładowo, na podstawie wartości `AuthorId`, możemy zdefiniować funkcję, która zwróci imię i nazwisko autora:


```sql
CREATE FUNCTION GetFullName (@AuthorId INT)
RETURNS NVARCHAR(100)
AS
BEGIN
    DECLARE @FullName NVARCHAR(100);
    SELECT @FullName = CONCAT(FirstName, ' ', LastName) FROM Authors WHERE AuthorId = @AuthorId;
    RETURN @FullName;
END;
```


Commands completed successfully.



Total execution time: 00:00:00.001


Po utworzeniu takiej funkcji, możemy ją wykorzystać, odpowiednio przekazując jej parametr.


```sql
DECLARE @authorId INT = 1
SELECT dbo.GetFullName(@authorId)
PRINT dbo.GetFullName(1)
SELECT TOP 5 AuthorId, dbo.GetFullName(AuthorId) as FullName
FROM Authors

-- poniższe wywołanie GetFullName zwróciło by błąd

-- SELECT TOP 1 AuthorId, GetFullName(AuthorId) as FullName

-- FROM Authors
```




Total execution time: 00:00:00


## Modyfikacja instniejących funkcji



Jeżeli zajdzie potrzeba modyfikacji istniejących funkcji, to istnieje możliwość, albo usunięcia funkcji i zastąpienia jej nową, albo zmodyfikowania istniejącej funkcji. W obu przypadkach, należy pamiętać o tym, żeby nie zmieniać nazwy funkcji, ponieważ wtedy nie będzie możliwości wywołania funkcji z poziomu kodu.



### Usuwanie funkcji



Aby usunąć funkcję, zdefiniowaną przez użytkownika w MS SQL, należy użyć polecenia `DROP FUNCTION`. Polecenie to przyjmuje jeden argument, którym jest nazwa funkcji, którą chcemy usunąć. Poniżej znajduje się przykład usunięcia funkcji `dbo.NazwaFunkcji`:



```sql
DROP FUNCTION dbo.NazwaFunkcji;
```





### Modfikacja funkcji



Aby zmodyfikować funkcję, zdefiniowaną przez użytkownika w MS SQL, należy użyć polecenia `ALTER FUNCTION`. Polecenie to przyjmuje dwa argumenty, pierwszym z nich jest nazwa funkcji, którą chcemy zmodyfikować, a drugim jest nowa definicja funkcji. Poniżej znajduje się przykład zmodyfikowania funkcji `dbo.NazwaFunkcji`:






```sql
ALTER FUNCTION GetFullName (@AuthorId INT)
RETURNS NVARCHAR(150) -- Zmieniamy typ z NVARCHAR(100) na NVARCHAR(150) aby pomieścić więcej informacji
AS
BEGIN
    DECLARE @FullName NVARCHAR(150); -- Zmieniamy rozmiar zmiennej
    DECLARE @BirthDate DATE; -- Deklarujemy zmienną przechowującą datę urodzenia

    -- Pobieramy pełne imię i nazwisko autora
    SELECT @FullName = CONCAT(FirstName, ' ', LastName) FROM Authors WHERE AuthorId = @AuthorId;

    -- Pobieramy datę urodzenia autora
    SELECT @BirthDate = BirthDate FROM Authors WHERE AuthorId = @AuthorId;

    -- Zwracamy pełne imię i nazwisko oraz datę urodzenia w formie pełnej daty
    RETURN CONCAT(@FullName, ' (Data urodzenia: ', CONVERT(NVARCHAR, @BirthDate, 103), ')');
END;
```


Commands completed successfully.



Total execution time: 00:00:00.002


Po modyfikacji funkcji, zwraca teraz ona nowe rezultaty:


```sql
DECLARE @authorId INT = 1
SELECT dbo.GetFullName(@authorId)
PRINT dbo.GetFullName(1)
SELECT TOP 5 AuthorId, dbo.GetFullName(AuthorId) as FullName
FROM Authors
```


Joanne Rowling (Data urodzenia: 31/07/1965)



## Funkcje tablicowe



W celu zdefiniowania funkcji tablicowej, która zwraca rezultaty pod postacią wierszy i kolumn, musimy użyć słowa kluczowego `RETURNS TABLE` w definicji funkcji. 





```sql
CREATE FUNCTION GetTableData(@param PARAMETER_TYPE)
RETURNS TABLE
AS
RETURN
(
    SELECT column1, column2, column3
    FROM table_name
    WHERE column1 = @param
);
```



Zauważ, że jeśli w naszej funkcji odrazu zwracamy rezultaty w jednym poleceniu, to możemy pominąć definicje bloku kodu `BEGIN...END` i odrazu zwrócić wartość poleceniem `RETURN`.



Przykładowo, funkcja zwracająca informacje o książkach danego autora, mogłaby wyglądać następująco:






```sql
CREATE FUNCTION GetAuthorsBooks (@AuthorId INT)
RETURNS TABLE
AS
RETURN 
(
    SELECT BookId, Title, [Description], PublicationDate, [Name] as Genre
    FROM [Books] b
    JOIN [Genres] g on b.GenreId = g.GenreId
    WHERE AuthorId = @AuthorId
);
```


Commands completed successfully.



Total execution time: 00:00:00.001


Aby wywołać tą funkcje, ponownie będziemy musieli do niej przekazać parametr, a rezultat może nam posłużyć jako tabela, którą możemy filtrować, łączyć z innymi czy grupować.


```sql
DECLARE @authorId INT = 1
SELECT * 
FROM GetAuthorsBooks(@authorId)
WHERE PublicationDate > '2000-01-01'
SELECT Genre, COUNT(*) PublishedBooks
FROM GetAuthorsBooks(@authorId)
GROUP BY Genre
SELECT ab.*, b.ISBN
FROM GetAuthorsBooks(@authorId) ab
JOIN Books b on b.BookId = ab.BookId
```


Zauważ, że w przypadku funkcji tablicowych, nie ma już potrzeby jawnego używania schematu `dbo`. W przypadku funkcji skalarnej, schemat był wymagany. 





Implementacje funkcji tablicowych możemy modyfikować w podobny sposób jak to miało miejsce dla funkcji skalaranych. Będziemy albo usuwać i tworzyć na nowo funkcje, lub poleceniem `ALTER FUNCTION`, nadpiszemy aktualną implementację. 






```sql
ALTER FUNCTION GetAuthorsBooks (@AuthorId INT)
RETURNS TABLE
AS
RETURN 
(
    SELECT BookId, 
        Title, 
        [Description], 
        PublicationDate, 
        [Name] as Genre,
        (SELECT COUNT(*) FROM Copies WHERE BookId = b.BookId) as CopiesCount
    FROM [Books] b
    JOIN [Genres] g on b.GenreId = g.GenreId
    WHERE AuthorId = @AuthorId
);
```


Commands completed successfully.



Total execution time: 00:00:00.001


Po modyfikacji funkcji tablicowej, będzie ona zwracała nowe rezultaty


```sql
DECLARE @authorId INT = 1
SELECT * 
FROM GetAuthorsBooks(@authorId)
WHERE PublicationDate > '2000-01-01'
SELECT Genre, COUNT(*) PublishedBooks
FROM GetAuthorsBooks(@authorId)
GROUP BY Genre
SELECT ab.*, b.ISBN
FROM GetAuthorsBooks(@authorId) ab
JOIN Books b on b.BookId = ab.BookId
```


## Zadanie



1. Stwórz funkcje skalarną, która zwraca liczbę dostępnych (nie wypożyczonych aktualnie) egzemplarzy danej książki - na podstawie tytułu książki. 



Następnie przetestuj działanie funkcji dla kilku przykładowych tytułów, odpowiednio zmieniając wypożyczenia danego egzemplarzu książki, tak aby wynik zwracany z funkcji się róźnił.




```sql
-- ROZWIĄZANIE
CREATE FUNCTION CountAvailableCopiesByTitle(@Title nvarchar(255))
RETURNS int
AS
BEGIN
    DECLARE @BookId int;
    DECLARE @AvailableCopies int;

    -- Znajdź identyfikator książki na podstawie tytułu
    SELECT @BookId = BookId FROM dbo.Books WHERE Title = @Title;

    -- Zlicz dostępne egzemplarze danej książki
    SELECT @AvailableCopies = COUNT(*)
    FROM dbo.Copies c
    WHERE c.BookId = @BookId
    AND CopyId NOT IN (
        SELECT CopyId
        FROM Loans
        WHERE c.CopyId = CopyId
            AND LoanDate < GETDATE()
            AND ReturnDate IS NULL
    )
    RETURN @AvailableCopies;
END;
```

2. Stwórz funkcję tablicową, która zwróci następujące informację o nie zwróconych książkach użytkownika, na podstawie jego imienia i nazwiska:



- tytuł książki

- autora książki

- datę wypożyczenia



Następnie przetestuj działanie funkcji na przykładowych danych.


```sql
-- ROZWIĄZANIE
CREATE FUNCTION GetUnreturnedBooksByUser(@FirstName NVARCHAR(55), @LastName NVARCHAR(55))
RETURNS TABLE
AS
RETURN 
(
    SELECT b.Title, CONCAT(a.FirstName, ' ', a.LastName) [Author], l.LoanDate
    FROM Loans l
    JOIN Copies c on c.CopyId = l.CopyId
    JOIN Books b on b.BookId = c.BookId
    LEFT JOIN Authors a on b.AuthorId = a.AuthorId
    JOIN Users u on l.UserId = u.UserId
    WHERE u.Name = @FirstName AND Surname = @LastName AND l.ReturnDate IS NULL
)
```
