## Tabele w bazie danych

Tabela jest strukturą danych, która przechowuje informacje w formie wierszy i kolumn. Każda tabela składa się z nazwanych kolumn, które określają typy danych, jakie mogą być przechowywane w danej kolumnie, oraz rzeczywistych danych, które są przechowywane w wierszach tabeli.

## Tworzenie tabeli

Aby utworzyć tabelę w bazie danych, należy użyć polecenia `CREATE TABLE`. Poniżej znajduje się przykład tworzenia tabeli `users` z kolumnami `id`, `name` i `age`:

```
CREATE TABLE Users (
    Id INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);

```

W powyższym przykładzie:

- `Id` jest kolumną typu `INT` i jest kluczem głównym tabeli.
- `Name` jest kolumną typu `VARCHAR(50)`, która przechowuje łańcuchy znaków o maksymalnej długości 50 znaków.
- `Age` jest kolumną typu `INT`, która przechowuje liczby całkowite.

## Usuwanie tabeli

Aby usunąć tabelę z bazy danych, należy użyć polecenia `DROP TABLE`. Poniżej znajduje się przykład usuwania tabeli `Users`:

```
DROP TABLE Users;

```

## Tworzenie struktury dla bazy danych biblioteki

Zanim utworzymy strukture tabeli dla bazy danych biblioteki, musimy najpierw utworzyć instancję bazy danych. Poniżej znajduje się przykład tworzenia bazy danych `Library`:


```sql
CREATE DATABASE LibraryDatabase;
```

Po połączeniu się do nowo utworzonej bazy, możemy przejść do utworzenia struktury tabel.  
  
Tabela `Authors`




```sql
CREATE TABLE Authors (
    AuthorId INT PRIMARY KEY IDENTITY(1,1),
    FirstName NVARCHAR(50) NOT NULL,
    LastName NVARCHAR(50) NOT NULL,
    BirthDate DATE,
    Country NVARCHAR(50)
);
```

Kolumna `AuthorId` jest kluczem głównym w tej tabeli, a to zapewni nam unikalność wierszy. Co więcej klucz główny przez właściwość `IDENTITY(1,1)` będzie automatycznie inkrementowany, co oznacza, że nie musimy go wypełniać podczas dodawania nowego wiersza. 

Stwórzmy też pozostałe tabele, jeszcze bez kluczy obcych, które dodamy później.


```sql
CREATE TABLE Genres (
    GenreId INT PRIMARY KEY IDENTITY(1,1),
    [Name] NVARCHAR(50) NOT NULL
);

CREATE TABLE Books (
    [BookId] INT PRIMARY KEY IDENTITY(1,1),
    [Title] NVARCHAR(255) NOT NULL,
    [Description] NVARCHAR(255) NULL,
    [PublicationDate] DATE,
    [ISBN] VARCHAR(20) NOT NULL
);

CREATE TABLE Copies (
    CopyId INT PRIMARY KEY IDENTITY(1,1),
    Condition NVARCHAR(100),
);
```

Zwróć uwagę, że nazwy kolumn możemy definiować w nawiasach kwadratowych, ale nie jest to konieczne.


