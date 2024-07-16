# Zmienne w skryptach SQL



Na serwerach baz danych Microsoft SQL Server, używany jest język Transact-SQL (T-SQL), który między innymi udostępnia możliwość tworzenia zmiennych. Zmienne są obiektami przechowującymi dane. Mogą przechowywać różne typy danych, takie jak liczby, ciągi znaków, daty itp. Zmienne pozwalają na przechowywanie tymczasowych wartości, które mogą być używane w różnych częściach skryptu.



Możemy definiować zmienne w T-SQL na różne sposoby:



1. **DECLARE**: Najczęstszy sposób definiowania zmiennych polega na użyciu instrukcji DECLARE. W tej instrukcji określamy nazwę zmiennej i jej typ danych. Na przykład:

   

   ```sql

    DECLARE @variableName dataType;



   ```



    Gdzie `@variableName` to nazwa zmiennej, a `dataType` to typ danych, który chcemy przechowywać. Na przykład:

    

    ```sql
     DECLARE @number INT;
     DECLARE @text VARCHAR(50);
     DECLARE @date DATE;
    ```



    Możemy też zadeklarować wiele zmiennych w jednej instrukcji DECLARE, oddzielając je przecinkami. Na przykład:

    

    ```sql
     DECLARE @number INT, @text VARCHAR(50), @date DATE;
    ```



    Warto zauważyć, że nazwy zmiennych zaczynają się od znaku '@', co odróżnia je od nazw kolumn w tabelach.







2. **INICJALIZACJA**: Możemy również zainicjować zmienną podczas deklaracji, przypisując jej początkową wartość. Na przykład:

   

   ```sql
    DECLARE @number INT = 10;
    DECLARE @text VARCHAR(50) = 'Sample text';
   ```



   Typ danych zmiennej musi być zgodny z typem wartości, którą chcemy przypisać. Na przykład, zmienna typu INT nie może przechowywać ciągu znaków, a zmienna typu VARCHAR nie może przechowywać liczby.







3. **SELECT INTO**: Innym sposobem jest zainicjowanie zmiennej poprzez wybór wartości z kolumny w zapytaniu SELECT. Na przykład:

   

   ```sql
    DECLARE @newDate DATE;
    SELECT @newDate = date FROM table WHERE condition = 'value';
   ```



    W tym przykładzie, zmienna `@newDate` zostanie zainicjowana wartością z kolumny `date` z tabeli `table`, gdzie spełniony jest warunek `condition = 'value'`. Zapytanie SELECT musi zwracać dokładnie jedną wartość, w przeciwnym razie zostanie zgłoszony błąd.



    Możemy też skrócić powyższe zapytanie do jednej linii, używając instrukcji `SELECT`. Na przykład:

    

    ```sql
     DECLARE @newDate DATE = (SELECT date FROM table WHERE condition = 'value');
    ```



4. **SET**: Możemy również użyć instrukcji SET do przypisania wartości do zmiennej. Na przykład:

   

   ```sql
    DECLARE @result INT;
    SET @result = 100;
   ```



    W tym przykładzie, zmienna `@result` zostanie zainicjowana wartością 100.





### Użycie zmiennych



Gdy już zdefiniujemy zmienne, możemy ich używać w różnych częściach skryptu, na przykład w instrukcjach SELECT, INSERT, UPDATE, DELETE itp. Przykładowo:



```sql
DECLARE @name VARCHAR(50);
SET @name = 'John';
SELECT * FROM table WHERE name = @name;
```



Zmienne możemy wykorzystać w poleceniach `INSERT INTO`, `UPDATE` lub `DELETE`, aby wstawiać, aktualizować lub usuwać dane w tabelach. 



Na przykład w poleceniu `INSERT INTO`:






```sql
DECLARE @authorId INT, @genreId INT;

-- Pobieramy identyfikator autora dla książek z serii "Harry Potter"
SELECT @authorId = AuthorId 
FROM Authors 
WHERE FirstName = 'Joanne' AND LastName = 'Rowling';

-- Pobieramy identyfikator gatunku, np. Fantasy
SELECT @genreId = GenreId 
FROM Genres 
WHERE Name = 'Fantasy';

-- Wstawiamy nową książkę "Harry Potter and the Order of the Phoenix"
INSERT INTO Books (Title, Description, PublicationDate, ISBN, AuthorId, GenreId)
VALUES ('Harry Potter and the Order of the Phoenix', 'The fifth book in the Harry Potter series', '2003-06-21', '9780439358071', @authorId, @genreId);

-- Wstawiamy nową książkę "Harry Potter and the Half-Blood Prince"
INSERT INTO Books (Title, Description, PublicationDate, ISBN, AuthorId, GenreId)
VALUES ('Harry Potter and the Half-Blood Prince', 'The sixth book in the Harry Potter series', '2005-07-16', '9780439784542', @authorId, @genreId);
```


W zapytaniach `SELECT`, zazwyczaj posłużą nam do wybrania kolumny, której wartości chcemy zobaczyć. 


```sql
DECLARE @authorId INT = (
    SELECT AuthorId 
    FROM Authors 
    WHERE FirstName = 'Joanne' AND LastName = 'Rowling'
), 
@genreId INT = (
    SELECT GenreId 
    FROM Genres 
    WHERE Name = 'Fantasy'
);

-- Wybieramy książki danego autora i gatunku
SELECT b.Title, b.Description, b.PublicationDate
FROM Books b
WHERE b.AuthorId = @authorId
AND b.GenreId = @genreId;
```



Podobnie możemy je wykorzystać w zapytaniach `UPDATE`, czy `DELETE`, aby zmodifikować lub usunąć rekordy spełniające określone kryteria.


```sql
DECLARE @authorId INT, @genreId INT;

-- Przypisujemy wartość do zmiennej autorId
SET @authorId = (
    SELECT AuthorId 
    FROM Authors 
    WHERE FirstName = 'Joanne' AND LastName = 'Rowling'
);

-- Przypisujemy wartość do zmiennej genreId
SET @genreId = (
    SELECT GenreId 
    FROM Genres 
    WHERE Name = 'Fantasy'
);

-- Aktualizujemy tytuły książek danego autora i gatunku
UPDATE Books
SET Title = CONCAT(Title, ' - Special Edition')
WHERE AuthorId = @authorId
AND GenreId = @genreId;
```



## Funkcja `SCOPE_IDENTITY()` w SQL Server

Do tej pory, dodając wiersze powiązane do dwóch tabel, musieliśmy znać identyfikator wiersza wstawionego do pierwszej tabeli, aby go użyć w przy wstawianiu wiersza drugiej tabeli.

Przykładowo, chcąc utworzyć nowy adres, a następnie powiązać go z nowym użytkownikiem, musieliśmy znać identyfikator wiersza wstawionego do tabeli adresów, aby go użyć w tabeli użytkowników.


```sql
-- Wstawiamy nowy adres do tabeli Addresses
INSERT INTO [Addresses] ([City], [Street], [HouseNumber], [Country])
VALUES
('Paris', 'Champs-Élysées', '789', 'France')

-- Sprawdzenie nowo dodanego rekordu
SELECT * FROM Addresses

-- Wstawiamy nowego użytkownika do tabeli Users, używając podzapytania do pobrania identyfikatora ostatnio wstawionego adresu
INSERT INTO [Users] ([Name], [Surname], [Email], [PhoneNumber], [AddressId])
VALUES
('Alice', 'Johnson', 'alice@example.com', '123-456-7890', ?)
```

W tym samym celu, w SQL Server możemy użyć funkcji `SCOPE_IDENTITY()`, aby uzyskać identyfikator wiersza wstawionego do tabeli w bieżącym zakresie.





```sql
-- Wstawiamy nowy adres do tabeli Addresses
INSERT INTO [Addresses] ([City], [Street], [HouseNumber], [Country])
VALUES
('Paris', 'Champs-Élysées', '789', 'France')

-- Pobieramy identyfikator adresu, który został automatycznie wygenerowany
DECLARE @NewAddressId INT = SCOPE_IDENTITY()

-- Wstawiamy nowego użytkownika do tabeli Users i przypisujemy mu nowo wstawiony adres
INSERT INTO Users ([Name], [Surname], [Email], [PhoneNumber], [AddressId])
VALUES
('Alice', 'Johnson', 'alice@example.com', '123-456-7890', @NewAddressId)
SELECT * FROM Addresses
SELECT * FROM Users
```



Wykorzystując funkcje `SCOPE_IDENTITY()` musimy mieć na uwadzę, że w przypadku wielu wstawień w jednym zapytaniu, zwrócona wartość będzie ostatnia z nich. 


```sql
-- Wstawiamy nowe adresy do tabeli Addresses
INSERT INTO [Addresses] ([City], [Street], [HouseNumber], [Country])
VALUES
('New York', 'Broadway', '123', 'USA'),
('Tokyo', 'Shibuya', '456', 'Japan')

-- Pobieramy identyfikator ostatnio wstawionego adresu
DECLARE @LastAddressId INT
SET @LastAddressId = SCOPE_IDENTITY()

-- Wstawiamy nowych użytkowników do tabeli Users, używając identyfikatora ostatnio wstawionego adresu
INSERT INTO [Users] ([Name], [Surname], [Email], [PhoneNumber], [AddressId])
VALUES
('John', 'Doe', 'john.doe@example.com', '111-222-3333', @LastAddressId),
('Emily', 'Smith', 'emily.smith@example.com', '444-555-6666', @LastAddressId)

SELECT * FROM Addresses
SELECT * FROM Users
```



