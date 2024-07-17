# INSERT INTO



Mając utworzoną strukturę bazy, możemy wypełnić ją danymi. W tym celu używamy polecenia `INSERT INTO`. Polecenie to pozwala na dodanie nowego wiersza do tabeli.

    

```sql  
INSERT INTO nazwa_tabeli (kolumna1, kolumna2, kolumna3, ...)
VALUES (wartość1, wartość2, wartość3, ...);
```



Jeśli chcemy dodać wiersz do tabeli, ale nie znamy wartości wszystkich kolumn, możemy pominąć kolumny, które mają być wypełnione wartościami domyślnymi, lub wartością `NULL` (jeżeli jest dopuszczalna). 

W takim przypadku polecenie `INSERT INTO` może wyglądać tak:



```sql
INSERT INTO nazwa_tabeli (kolumna1, kolumna3, ...)
VALUES (wartość1, wartość3, ...);
```



Jeśli chcemy dodać wiele wierszy na raz, możemy użyć polecenia `INSERT INTO` z klauzulą `VALUES` wielokrotnie. 



```sql
INSERT INTO nazwa_tabeli (kolumna1, kolumna2, kolumna3, ...)
VALUES (wartość1, wartość2, wartość3, ...),
       (wartość1, wartość2, wartość3, ...),
       (wartość1, wartość2, wartość3, ...);
```



Ważne jest, aby przy dodawaniu wierszy pamiętać o ograniczeniach nałożonych na tabelę, takich jak klucze główne, unikalne, czy obce. W przypadku naruszenia tych ograniczeń, operacja `INSERT INTO` zakończy się niepowodzeniem.



Przykładowo, żeby dodać nowy wpis do tabeli `Books`, musimy najpierw utworzyć zarówno autora jak i gatunek, z którym dana książka jest powiązana. Następnie możemy dodać nową książkę do tabeli `Books` - o ile wartość dla kolumny `ISBN` będzie unikalna.



### Przykład:



Dodanie gatunku książki do tabeli `Genres`:








```sql
INSERT INTO Genres (Name)
VALUES ('Fantasy');
```

Zwróć uwagę na to, że wartość dla klucza głównego `GenreId`, jest pominięta, jako, że nałożyliśmy na tą kolumnę `IDENTITY(1,1)`, co oznacza, że wartość ta będzie automatycznie generowana przez bazę danych - zaczynając od 1 i zwiększając się o 1 dla każdego nowego wiersza.



Dodanie autora do tabeli `Authors`:




```sql
INSERT INTO Authors (FirstName, LastName, BirthDate, Country)
VALUES ('Joanne', 'Rowling', '1965-07-31', 'UK');
```

Dodanie książki do tabeli `Books`:


```sql
INSERT INTO Books (Title, Description, PublicationDate, ISBN, AuthorId, GenreId)
VALUES ('Harry Potter and the Philosopher''s Stone', 'First book in the series', '1997-06-26', '9780747532743', 1, 1);
```

Jeżeli chcielibyśmy ponownie dodać tą samą książke, to jako, że mamy ograniczenie `UNIQUE` na kolumnie `ISBN`, to nie możemy tego zrobić.



## Pomijanie wartości opcjonalnych



Kolumny, które w danej tabeli są oznaczone jako `NULL`, nie muszą być zdefiniowane w poleceniu `INSERT`. Wtedy zostaną one wstawione jako `NULL`.

Podobnie, jeżeli kolumna ma domyślną (`DEFAULT`) wartość, to również nie musimy jej podawać w poleceniu `INSERT`.




```sql
INSERT INTO [Authors] ([FirstName], [LastName])
VALUES ('Stephen', 'King'),
       ('George', 'Orwell');
```

## Zadanie praktyczne

Dodaj wiersze do tabeli z użytkownikami `Users`, oraz kopiami książek `Copies`, a następnie połącz je relacją wiele do wielu - tak, aby jedna książka, mogła być wypożyczana przez wielu użytkowników, a jeden użytkownik mógł wypożyczać wiele książek.


<details><summary><b>Rozwiązanie</b></summary>

```sql
-- ROZWIĄZANIE
INSERT INTO Addresses (City, Street, HouseNumber, Country)
VALUES ('New York', 'Broadway', '123', 'USA'),
        ('London', 'Oxford Street', '34', 'UK')
        
INSERT INTO Users (Name, Surname, Email, PhoneNumber, AddressId)
VALUES  ('Emma', 'Johnson', 'emma.johnson@example.com', '123456789', 1),
       ('Michael', 'Brown', 'michael.brown@example.com', '987654321', 2)

INSERT INTO Books (Title, Description, PublicationDate, ISBN, AuthorId, GenreId)
VALUES ('Harry Potter and the Chamber of Secrets', 'The second book in the Harry Potter series', '1998-07-02', '9780439064866', 1, 1)

INSERT INTO Copies (Condition, BookId)
VALUES ('Good', 2),
        ('Very Good', 2),
        ('Excellent', 4)

INSERT INTO Loans (UserId, CopyId, LoanDate)
VALUES (1, 1, '2020-01-01'),
       (1, 3, '2021-01-01'),
       (2, 1, '2021-01-01')
```

</details>
