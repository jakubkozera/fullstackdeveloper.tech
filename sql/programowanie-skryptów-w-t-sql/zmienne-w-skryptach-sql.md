## Zmienne w skryptach SQL

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


(1 row affected)



(1 row affected)



Total execution time: 00:00:00.004


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


(4 rows affected)



Total execution time: 00:00:00.007





<table><tr><th>Title</th><th>Description</th><th>PublicationDate</th></tr><tr><td>Harry Potter and the Philosopher&#39;s Stone</td><td>First book in the series</td><td>1997-06-26</td></tr><tr><td>Harry Potter and the Chamber of Secrets</td><td>The second book in the Harry Potter series</td><td>1998-07-02</td></tr><tr><td>Harry Potter and the Order of the Phoenix</td><td>The fifth book in the Harry Potter series</td><td>2003-06-21</td></tr><tr><td>Harry Potter and the Half-Blood Prince</td><td>The sixth book in the Harry Potter series</td><td>2005-07-16</td></tr></table>



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


(4 rows affected)



Total execution time: 00:00:00.004


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


(1 row affected)



(1 row affected)



(20 rows affected)



(22 rows affected)



Total execution time: 00:00:00.042





<table><tr><th>AddressId</th><th>City</th><th>Street</th><th>HouseNumber</th><th>Country</th></tr><tr><td>2</td><td>London</td><td>Oxford Street</td><td>34</td><td>UK</td></tr><tr><td>441</td><td>Paris</td><td>Champs-Élysées</td><td>789</td><td>France</td></tr><tr><td>442</td><td>Tokyo</td><td>Shibuya</td><td>1011</td><td>Japan</td></tr><tr><td>443</td><td>Sydney</td><td>George Street</td><td>99</td><td>Australia</td></tr><tr><td>444</td><td>Berlin</td><td>Alexanderplatz</td><td>1415</td><td>Germany</td></tr><tr><td>445</td><td>Moscow</td><td>Red Square</td><td>1617</td><td>Russia</td></tr><tr><td>446</td><td>Rome</td><td>Via Condotti</td><td>1819</td><td>Italy</td></tr><tr><td>447</td><td>Beijing</td><td>Wangfujing</td><td>2021</td><td>China</td></tr><tr><td>448</td><td>Dubai</td><td>Sheikh Zayed Road</td><td>2223</td><td>UAE</td></tr><tr><td>449</td><td>Toronto</td><td>Yonge Street</td><td>2425</td><td>Canada</td></tr><tr><td>450</td><td>Mexico City</td><td>Paseo de la Reforma</td><td>2627</td><td>Mexico</td></tr><tr><td>451</td><td>Cairo</td><td>Tahrir Square</td><td>2829</td><td>Egypt</td></tr><tr><td>452</td><td>Rio de Janeiro</td><td>Copacabana</td><td>3031</td><td>Brazil</td></tr><tr><td>453</td><td>Bangkok</td><td>Sukhumvit Road</td><td>3233</td><td>Thailand</td></tr><tr><td>454</td><td>Mumbai</td><td>Marine Drive</td><td>3435</td><td>India</td></tr><tr><td>455</td><td>Cape Town</td><td>Long Street</td><td>3637</td><td>South Africa</td></tr><tr><td>456</td><td>Madrid</td><td>Gran Vía</td><td>3839</td><td>Spain</td></tr><tr><td>457</td><td>Seoul</td><td>Myeongdong</td><td>4041</td><td>South Korea</td></tr><tr><td>458</td><td>Oslo</td><td>Karl Johans gate</td><td>4243</td><td>Norway</td></tr><tr><td>459</td><td>Paris</td><td>Champs-Élysées</td><td>789</td><td>France</td></tr></table>






<table><tr><th>UserId</th><th>Name</th><th>Surname</th><th>Email</th><th>PhoneNumber</th><th>AddressId</th></tr><tr><td>1</td><td>Emma</td><td>Johnson</td><td>emma.johnson@example.com</td><td>343-456-789</td><td>NULL</td></tr><tr><td>2</td><td>Michael</td><td>Brown</td><td>michael.brown@example.com</td><td>343-456-789</td><td>2</td></tr><tr><td>224</td><td>Alice</td><td>Johnson</td><td>alice@example.com</td><td>123-456-7890</td><td>NULL</td></tr><tr><td>226</td><td>Charlie</td><td>Williams</td><td>charlie@example.com</td><td>111-222-3333</td><td>441</td></tr><tr><td>227</td><td>David</td><td>Brown</td><td>david@example.com</td><td>444-555-6666</td><td>442</td></tr><tr><td>228</td><td>Emma</td><td>Jones</td><td>emma@example.com</td><td>777-888-9999</td><td>443</td></tr><tr><td>229</td><td>Fiona</td><td>Taylor</td><td>fiona@example.com</td><td>999-888-7777</td><td>444</td></tr><tr><td>230</td><td>George</td><td>Anderson</td><td>george@example.com</td><td>666-555-4444</td><td>445</td></tr><tr><td>231</td><td>Hannah</td><td>Martinez</td><td>hannah@example.com</td><td>333-222-1111</td><td>446</td></tr><tr><td>232</td><td>Isaac</td><td>Garcia</td><td>isaac@example.com</td><td>000-999-8888</td><td>447</td></tr><tr><td>233</td><td>Jack</td><td>Rodriguez</td><td>jack@example.com</td><td>111-000-7777</td><td>448</td></tr><tr><td>234</td><td>Karen</td><td>Hernandez</td><td>karen@example.com</td><td>222-111-6666</td><td>449</td></tr><tr><td>235</td><td>Liam</td><td>Lopez</td><td>liam@example.com</td><td>333-444-5555</td><td>450</td></tr><tr><td>236</td><td>Mia</td><td>Gonzalez</td><td>mia@example.com</td><td>666-777-8888</td><td>451</td></tr><tr><td>237</td><td>Noah</td><td>Perez</td><td>noah@example.com</td><td>999-888-7777</td><td>452</td></tr><tr><td>238</td><td>Olivia</td><td>Torres</td><td>olivia@example.com</td><td>000-111-2222</td><td>453</td></tr><tr><td>239</td><td>Peter</td><td>Sanchez</td><td>peter@example.com</td><td>444-555-6666</td><td>454</td></tr><tr><td>240</td><td>Quinn</td><td>Ramirez</td><td>quinn@example.com</td><td>777-888-9999</td><td>455</td></tr><tr><td>241</td><td>Rachel</td><td>Rivera</td><td>rachel@example.com</td><td>123-456-7890</td><td>456</td></tr><tr><td>242</td><td>Samuel</td><td>Smith</td><td>samuel@example.com</td><td>987-654-3210</td><td>457</td></tr><tr><td>243</td><td>Taylor</td><td>Baker</td><td>taylor@example.com</td><td>111-222-3333</td><td>458</td></tr><tr><td>244</td><td>Alice</td><td>Johnson</td><td>alice@example.com</td><td>123-456-7890</td><td>459</td></tr></table>



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


(2 rows affected)



(2 rows affected)



(22 rows affected)



(24 rows affected)



Total execution time: 00:00:00.015





<table><tr><th>AddressId</th><th>City</th><th>Street</th><th>HouseNumber</th><th>Country</th></tr><tr><td>2</td><td>London</td><td>Oxford Street</td><td>34</td><td>UK</td></tr><tr><td>441</td><td>Paris</td><td>Champs-Élysées</td><td>789</td><td>France</td></tr><tr><td>442</td><td>Tokyo</td><td>Shibuya</td><td>1011</td><td>Japan</td></tr><tr><td>443</td><td>Sydney</td><td>George Street</td><td>99</td><td>Australia</td></tr><tr><td>444</td><td>Berlin</td><td>Alexanderplatz</td><td>1415</td><td>Germany</td></tr><tr><td>445</td><td>Moscow</td><td>Red Square</td><td>1617</td><td>Russia</td></tr><tr><td>446</td><td>Rome</td><td>Via Condotti</td><td>1819</td><td>Italy</td></tr><tr><td>447</td><td>Beijing</td><td>Wangfujing</td><td>2021</td><td>China</td></tr><tr><td>448</td><td>Dubai</td><td>Sheikh Zayed Road</td><td>2223</td><td>UAE</td></tr><tr><td>449</td><td>Toronto</td><td>Yonge Street</td><td>2425</td><td>Canada</td></tr><tr><td>450</td><td>Mexico City</td><td>Paseo de la Reforma</td><td>2627</td><td>Mexico</td></tr><tr><td>451</td><td>Cairo</td><td>Tahrir Square</td><td>2829</td><td>Egypt</td></tr><tr><td>452</td><td>Rio de Janeiro</td><td>Copacabana</td><td>3031</td><td>Brazil</td></tr><tr><td>453</td><td>Bangkok</td><td>Sukhumvit Road</td><td>3233</td><td>Thailand</td></tr><tr><td>454</td><td>Mumbai</td><td>Marine Drive</td><td>3435</td><td>India</td></tr><tr><td>455</td><td>Cape Town</td><td>Long Street</td><td>3637</td><td>South Africa</td></tr><tr><td>456</td><td>Madrid</td><td>Gran Vía</td><td>3839</td><td>Spain</td></tr><tr><td>457</td><td>Seoul</td><td>Myeongdong</td><td>4041</td><td>South Korea</td></tr><tr><td>458</td><td>Oslo</td><td>Karl Johans gate</td><td>4243</td><td>Norway</td></tr><tr><td>459</td><td>Paris</td><td>Champs-Élysées</td><td>789</td><td>France</td></tr><tr><td>460</td><td>New York</td><td>Broadway</td><td>123</td><td>USA</td></tr><tr><td>461</td><td>Tokyo</td><td>Shibuya</td><td>456</td><td>Japan</td></tr></table>






<table><tr><th>UserId</th><th>Name</th><th>Surname</th><th>Email</th><th>PhoneNumber</th><th>AddressId</th></tr><tr><td>1</td><td>Emma</td><td>Johnson</td><td>emma.johnson@example.com</td><td>343-456-789</td><td>NULL</td></tr><tr><td>2</td><td>Michael</td><td>Brown</td><td>michael.brown@example.com</td><td>343-456-789</td><td>2</td></tr><tr><td>224</td><td>Alice</td><td>Johnson</td><td>alice@example.com</td><td>123-456-7890</td><td>NULL</td></tr><tr><td>226</td><td>Charlie</td><td>Williams</td><td>charlie@example.com</td><td>111-222-3333</td><td>441</td></tr><tr><td>227</td><td>David</td><td>Brown</td><td>david@example.com</td><td>444-555-6666</td><td>442</td></tr><tr><td>228</td><td>Emma</td><td>Jones</td><td>emma@example.com</td><td>777-888-9999</td><td>443</td></tr><tr><td>229</td><td>Fiona</td><td>Taylor</td><td>fiona@example.com</td><td>999-888-7777</td><td>444</td></tr><tr><td>230</td><td>George</td><td>Anderson</td><td>george@example.com</td><td>666-555-4444</td><td>445</td></tr><tr><td>231</td><td>Hannah</td><td>Martinez</td><td>hannah@example.com</td><td>333-222-1111</td><td>446</td></tr><tr><td>232</td><td>Isaac</td><td>Garcia</td><td>isaac@example.com</td><td>000-999-8888</td><td>447</td></tr><tr><td>233</td><td>Jack</td><td>Rodriguez</td><td>jack@example.com</td><td>111-000-7777</td><td>448</td></tr><tr><td>234</td><td>Karen</td><td>Hernandez</td><td>karen@example.com</td><td>222-111-6666</td><td>449</td></tr><tr><td>235</td><td>Liam</td><td>Lopez</td><td>liam@example.com</td><td>333-444-5555</td><td>450</td></tr><tr><td>236</td><td>Mia</td><td>Gonzalez</td><td>mia@example.com</td><td>666-777-8888</td><td>451</td></tr><tr><td>237</td><td>Noah</td><td>Perez</td><td>noah@example.com</td><td>999-888-7777</td><td>452</td></tr><tr><td>238</td><td>Olivia</td><td>Torres</td><td>olivia@example.com</td><td>000-111-2222</td><td>453</td></tr><tr><td>239</td><td>Peter</td><td>Sanchez</td><td>peter@example.com</td><td>444-555-6666</td><td>454</td></tr><tr><td>240</td><td>Quinn</td><td>Ramirez</td><td>quinn@example.com</td><td>777-888-9999</td><td>455</td></tr><tr><td>241</td><td>Rachel</td><td>Rivera</td><td>rachel@example.com</td><td>123-456-7890</td><td>456</td></tr><tr><td>242</td><td>Samuel</td><td>Smith</td><td>samuel@example.com</td><td>987-654-3210</td><td>457</td></tr><tr><td>243</td><td>Taylor</td><td>Baker</td><td>taylor@example.com</td><td>111-222-3333</td><td>458</td></tr><tr><td>244</td><td>Alice</td><td>Johnson</td><td>alice@example.com</td><td>123-456-7890</td><td>459</td></tr><tr><td>245</td><td>John</td><td>Doe</td><td>john.doe@example.com</td><td>111-222-3333</td><td>461</td></tr><tr><td>246</td><td>Emily</td><td>Smith</td><td>emily.smith@example.com</td><td>444-555-6666</td><td>461</td></tr></table>


