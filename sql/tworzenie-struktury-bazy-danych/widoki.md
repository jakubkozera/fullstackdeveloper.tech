# Widoki

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

Aby wyświetlić dane z powyższego widoku, wystarczy użyć polecenia `SELECT` i w klauzuli `FROM` podać nazwę widoku, z którego chcemy wyświetlić dane.


```sql
SELECT *
FROM BooksAuthorsView
```


Co więcej widoki, możemy używać w zapytaniach tak samo jak zwykłe tabele, oto kilka przykładów użycia widoku `BooksAuthorsView` z różnymi klauzulami, takimi jak `JOIN`, `WHERE`, i `GROUP BY`.



### Przykład 1: Użycie widoku `BooksAuthorsView` z klauzulą `WHERE`



Wyświetlanie wszystkich książek napisanych przez autorów z `UK`:






```sql
SELECT *
FROM BooksAuthorsView
WHERE AuthorCountry = 'UK';
```


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


### Przykład 5: Użycie widoku `BooksAuthorsView` z klauzulą `ORDER BY`



Wyświetlanie wszystkich książek posortowanych według daty publikacji:






```sql
SELECT *
FROM BooksAuthorsView
ORDER BY PublicationDate DESC;
```


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



```sql
-- zwrócone rezultaty, po zmianie definicji widoku
SELECT *
FROM BooksAuthorsView
```


### Usuwanie widoków





Aby usunąć widok w MS SQL Server, używa się polecenia `DROP VIEW`. Oto przykład, jak usunąć widok:





Powiedzmy, że chcemy usunąć widok `BooksAuthorsView`, który stworzyliśmy wcześniej. Użyjemy następującego polecenia:






```sql
DROP VIEW BooksAuthorsView;
```




### Dlaczego używać widoków zamiast zwykłych SELECT?



1. **Abstrakcja i Prostota**: Widoki mogą ukrywać skomplikowane zapytania SQL, prezentując użytkownikom prosty interfejs.

2. **Bezpieczeństwo**: Widoki mogą ograniczać dostęp do określonych kolumn lub wierszy, poprawiając bezpieczeństwo danych.

3. **Reużywalność**: Widoki mogą być używane wielokrotnie w różnych zapytaniach, co redukuje powtarzanie kodu.

4. **Modularność**: Widoki mogą ułatwiać zarządzanie i organizację logiki baz danych.

5. **Optymalizacja**: Widoki mogą poprawić wydajność poprzez zapisywanie zoptymalizowanych planów wykonania zapytań.




