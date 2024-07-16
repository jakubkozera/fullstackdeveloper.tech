## Widoki

Widoki w MS SQL są nazwanymi zapytaniami SELECT, które można zapisać w bazie danych i używać tak, jakby były tabelami (niektórzy nazywają je tabelami wirtualnymi). Widoki nie przechowują danych same w sobie, lecz przechowują zapytania, które są wykonywane w momencie dostępu do widoku. Widoki mogą służyć do abstrakcji danych, bezpieczeństwa oraz uproszczenia skomplikowanych zapytań. Oto kilka przykładów, jak tworzyć i modyfikować widoki.

### Przykład widoku: Tworzenie widoku wyświetlającego szczegóły książek wraz z informacjami o autorach


```sql
CREATE VIEW BooksAuthorsView AS
SELECT 
    b.BookId,
    b.Title,
    b.PublicationDate,
    b.ISBN,
    a.FirstName + ' ' + a.LastName AS AuthorName,
    a.Country AS AuthorCountry
FROM 
    dbo.Books b
INNER JOIN 
    dbo.Authors a ON b.AuthorId = a.AuthorId;

```


Commands completed successfully.



Total execution time: 00:00:00.001


Aby wyświetlić dane z powyższego widoku, wystarczy użyć polecenia `SELECT` i w klauzuli `FROM` podać nazwę widoku, z którego chcemy wyświetlić dane.


```sql
SELECT *
FROM BooksAuthorsView
```


(10 rows affected)



Total execution time: 00:00:00.005





<table><tr><th>BookId</th><th>Title</th><th>PublicationDate</th><th>ISBN</th><th>AuthorName</th><th>AuthorCountry</th></tr><tr><td>2</td><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td><td>1997-06-26</td><td>9780747532743</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>4</td><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>1998-07-02</td><td>9780439064866</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>457</td><td>The Great Gatsby</td><td>1925-04-10</td><td>9780743273565</td><td>John Smith</td><td>USA</td></tr><tr><td>458</td><td>Pride and Prejudice</td><td>1813-01-28</td><td>9780141439518</td><td>Emma Johnson</td><td>UK</td></tr><tr><td>459</td><td>Les Misérables</td><td>1862-03-15</td><td>9780140444308</td><td>Jean Dupont</td><td>France</td></tr><tr><td>460</td><td>Norwegian Wood</td><td>1987-08-04</td><td>9780099543793</td><td>Kenji Tanaka</td><td>Japan</td></tr><tr><td>461</td><td>1984</td><td>1949-06-08</td><td>9780451524935</td><td>George Orwell</td><td>NULL</td></tr><tr><td>476</td><td>The Shining</td><td>1977-01-28</td><td>9780385121675</td><td>Stephen King</td><td>NULL</td></tr><tr><td>482</td><td>Harry Potter and the Order of the Phoenix - Special Edition</td><td>2003-06-21</td><td>9780439358071</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>483</td><td>Harry Potter and the Half-Blood Prince - Special Edition</td><td>2005-07-16</td><td>9780439784542</td><td>Joanne Rowling</td><td>UK</td></tr></table>



Co więcej widoki, możemy używać w zapytaniach tak samo jak zwykłe tabele, oto kilka przykładów użycia widoku `BooksAuthorsView` z różnymi klauzulami, takimi jak `JOIN`, `WHERE`, i `GROUP BY`.

### Przykład 1: Użycie widoku `BooksAuthorsView` z klauzulą `WHERE`

Wyświetlanie wszystkich książek napisanych przez autorów z `UK`:




```sql
SELECT *
FROM BooksAuthorsView
WHERE AuthorCountry = 'UK';

```


(5 rows affected)



Total execution time: 00:00:00.005





<table><tr><th>BookId</th><th>Title</th><th>PublicationDate</th><th>ISBN</th><th>AuthorName</th><th>AuthorCountry</th></tr><tr><td>2</td><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td><td>1997-06-26</td><td>9780747532743</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>4</td><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>1998-07-02</td><td>9780439064866</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>458</td><td>Pride and Prejudice</td><td>1813-01-28</td><td>9780141439518</td><td>Emma Johnson</td><td>UK</td></tr><tr><td>482</td><td>Harry Potter and the Order of the Phoenix - Special Edition</td><td>2003-06-21</td><td>9780439358071</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>483</td><td>Harry Potter and the Half-Blood Prince - Special Edition</td><td>2005-07-16</td><td>9780439784542</td><td>Joanne Rowling</td><td>UK</td></tr></table>




### Przykład 2: Użycie widoku `BooksAuthorsView` z klauzulą `JOIN`

Połączenie widoku `BooksAuthorsView` z tabelą `Genres`, aby uzyskać szczegóły książek wraz z nazwą gatunku:




```sql
SELECT 
    bav.BookId,
    bav.Title,
    bav.AuthorName,
    g.Name AS GenreName
FROM 
    BooksAuthorsView bav
INNER JOIN 
    Books b ON bav.BookId = b.BookId
INNER JOIN 
    Genres g ON b.GenreId = g.GenreId;

```


(10 rows affected)



Total execution time: 00:00:00.006





<table><tr><th>BookId</th><th>Title</th><th>AuthorName</th><th>GenreName</th></tr><tr><td>2</td><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>4</td><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>457</td><td>The Great Gatsby</td><td>John Smith</td><td>Fiction</td></tr><tr><td>458</td><td>Pride and Prejudice</td><td>Emma Johnson</td><td>Romance</td></tr><tr><td>459</td><td>Les Misérables</td><td>Jean Dupont</td><td>Drama</td></tr><tr><td>460</td><td>Norwegian Wood</td><td>Kenji Tanaka</td><td>Fiction</td></tr><tr><td>461</td><td>1984</td><td>George Orwell</td><td>Fiction</td></tr><tr><td>476</td><td>The Shining</td><td>Stephen King</td><td>Horror</td></tr><tr><td>482</td><td>Harry Potter and the Order of the Phoenix - Special Edition</td><td>Joanne Rowling</td><td>Fantasy</td></tr><tr><td>483</td><td>Harry Potter and the Half-Blood Prince - Special Edition</td><td>Joanne Rowling</td><td>Fantasy</td></tr></table>




### Przykład 3: Użycie widoku `BooksAuthorsView` z klauzulą `GROUP BY`

Wyświetlanie liczby książek napisanych przez każdego autora:




```sql
SELECT 
    AuthorName,
    COUNT(*) AS BooksCount
FROM 
    BooksAuthorsView
GROUP BY 
    AuthorName;

```


(7 rows affected)



Total execution time: 00:00:00.005





<table><tr><th>AuthorName</th><th>BooksCount</th></tr><tr><td>Emma Johnson</td><td>1</td></tr><tr><td>George Orwell</td><td>1</td></tr><tr><td>Jean Dupont</td><td>1</td></tr><tr><td>Joanne Rowling</td><td>4</td></tr><tr><td>John Smith</td><td>1</td></tr><tr><td>Kenji Tanaka</td><td>1</td></tr><tr><td>Stephen King</td><td>1</td></tr></table>




### Przykład 4: Użycie widoku `BooksAuthorsView` z klauzulą `HAVING`

Wyświetlanie autorów, którzy napisali więcej niż jedną książkę:




```sql
SELECT 
    AuthorName,
    COUNT(*) AS BooksCount
FROM 
    BooksAuthorsView
GROUP BY 
    AuthorName
HAVING 
    COUNT(*) > 1;

```


(1 row affected)



Total execution time: 00:00:00.005





<table><tr><th>AuthorName</th><th>BooksCount</th></tr><tr><td>Joanne Rowling</td><td>4</td></tr></table>




### Przykład 5: Użycie widoku `BooksAuthorsView` z klauzulą `ORDER BY`

Wyświetlanie wszystkich książek posortowanych według daty publikacji:




```sql
SELECT *
FROM BooksAuthorsView
ORDER BY PublicationDate DESC;

```


(10 rows affected)



Total execution time: 00:00:00.004





<table><tr><th>BookId</th><th>Title</th><th>PublicationDate</th><th>ISBN</th><th>AuthorName</th><th>AuthorCountry</th></tr><tr><td>483</td><td>Harry Potter and the Half-Blood Prince - Special Edition</td><td>2005-07-16</td><td>9780439784542</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>482</td><td>Harry Potter and the Order of the Phoenix - Special Edition</td><td>2003-06-21</td><td>9780439358071</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>4</td><td>Harry Potter and the Chamber of Secrets - Special Edition</td><td>1998-07-02</td><td>9780439064866</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>2</td><td>Harry Potter and the Philosopher&#39;s Stone - Special Edition</td><td>1997-06-26</td><td>9780747532743</td><td>Joanne Rowling</td><td>UK</td></tr><tr><td>460</td><td>Norwegian Wood</td><td>1987-08-04</td><td>9780099543793</td><td>Kenji Tanaka</td><td>Japan</td></tr><tr><td>476</td><td>The Shining</td><td>1977-01-28</td><td>9780385121675</td><td>Stephen King</td><td>NULL</td></tr><tr><td>461</td><td>1984</td><td>1949-06-08</td><td>9780451524935</td><td>George Orwell</td><td>NULL</td></tr><tr><td>457</td><td>The Great Gatsby</td><td>1925-04-10</td><td>9780743273565</td><td>John Smith</td><td>USA</td></tr><tr><td>459</td><td>Les Misérables</td><td>1862-03-15</td><td>9780140444308</td><td>Jean Dupont</td><td>France</td></tr><tr><td>458</td><td>Pride and Prejudice</td><td>1813-01-28</td><td>9780141439518</td><td>Emma Johnson</td><td>UK</td></tr></table>



### Przykład 6: Użycie widoku `BooksAuthorsView` z `JOIN`, `GROUP BY`, i `HAVING`

Wyświetlanie gatunków oraz liczby książek w każdym gatunku dla autorów z `UK`, którzy napisali więcej niż jedną książkę:




```sql
SELECT 
    g.Name AS GenreName,
    COUNT(bav.BookId) AS BooksCount
FROM 
    BooksAuthorsView bav
INNER JOIN 
    Books b ON bav.BookId = b.BookId
INNER JOIN 
    Genres g ON b.GenreId = g.GenreId
WHERE 
    bav.AuthorCountry = 'UK'
GROUP BY 
    g.Name
HAVING 
    COUNT(bav.BookId) > 1
```


(1 row affected)



Total execution time: 00:00:00.006





<table><tr><th>GenreName</th><th>BooksCount</th></tr><tr><td>Fantasy</td><td>4</td></tr></table>



### Przykład widoku: Tworzenie widoku wyświetlającego wszystkie wypożyczenia z informacjami o użytkownikach i książkach


```sql
CREATE VIEW LoansDetailsView AS
SELECT 
    l.LoanId,
    u.Name + ' ' + u.Surname AS UserName,
    b.Title AS BookTitle,
    l.LoanDate,
    l.ReturnDate
FROM 
    dbo.Loans l
INNER JOIN 
    dbo.Users u ON l.UserId = u.UserId
INNER JOIN 
    dbo.Copies c ON l.CopyId = c.CopyId
INNER JOIN 
    dbo.Books b ON c.BookId = b.BookId;

```

### Przykład widoku: Tworzenie widoku wyświetlającego książki według gatunku


```sql
CREATE VIEW BooksByGenreView AS
SELECT 
    g.Name AS GenreName,
    b.Title,
    b.PublicationDate
FROM 
    dbo.Books b
INNER JOIN 
    dbo.Genres g ON b.GenreId = g.GenreId;

```

### Modyfikowanie widoku

Aby zmodyfikować istniejący widok, używamy polecenia `ALTER VIEW`:




```sql
ALTER VIEW BooksAuthorsView AS
SELECT 
    b.BookId,
    b.Title,
    b.Description, -- Dodano kolumnę opisu książki
    b.PublicationDate,
    b.ISBN,
    a.FirstName + ' ' + a.LastName AS AuthorName,
    a.Country AS AuthorCountry
FROM 
    dbo.Books b
INNER JOIN 
    dbo.Authors a ON b.AuthorId = a.AuthorId;

```


Commands completed successfully.



Total execution time: 00:00:00.002



```sql
-- zwrócone rezultaty, po zmianie definicji widoku

SELECT *
FROM BooksAuthorsView
```




Total execution time: 00:00:00.001


### Usuwanie widoków


Aby usunąć widok w MS SQL Server, używa się polecenia `DROP VIEW`. Oto przykład, jak usunąć widok:


Powiedzmy, że chcemy usunąć widok `BooksAuthorsView`, który stworzyliśmy wcześniej. Użyjemy następującego polecenia:




```sql
DROP VIEW BooksAuthorsView;

```


Commands completed successfully.



Total execution time: 00:00:00.002




### Dlaczego używać widoków zamiast zwykłych SELECT?

1. **Abstrakcja i Prostota**: Widoki mogą ukrywać skomplikowane zapytania SQL, prezentując użytkownikom prosty interfejs.
2. **Bezpieczeństwo**: Widoki mogą ograniczać dostęp do określonych kolumn lub wierszy, poprawiając bezpieczeństwo danych.
3. **Reużywalność**: Widoki mogą być używane wielokrotnie w różnych zapytaniach, co redukuje powtarzanie kodu.
4. **Modularność**: Widoki mogą ułatwiać zarządzanie i organizację logiki baz danych.
5. **Optymalizacja**: Widoki mogą poprawić wydajność poprzez zapisywanie zoptymalizowanych planów wykonania zapytań.


