# Relacje między tabelami

W Microsoft SQL Server istnieją różne typy relacji, które mogą być definiowane między tabelami. Relacje te są używane do określenia sposobu, w jaki dane w jednej tabeli są powiązane z danymi w innej tabeli. Relacje te są zwykle definiowane za pomocą kluczy obcych, które są kluczami głównymi w innej tabeli. Klucze obce są używane do zapewnienia spójności danych między tabelami i zapobiegania wprowadzaniu błędnych danych.

1. **Relacja jeden-do-jeden (One-to-One)**:
    
    - Każdy wiersz w jednej tabeli może być powiązany z co najwyżej jednym wierszem w drugiej tabeli i odwrotnie.
2. **Relacja jeden-do-wielu (One-to-Many)**:
    
    - Każdy wiersz w jednej tabeli może być powiązany z wieloma wierszami w drugiej tabeli. Jest to najczęstszy rodzaj relacji.
3. **Relacja wiele-do-wielu (Many-to-Many)**:
    
    - W tym przypadku wiele wierszy w jednej tabeli może być powiązanych z wieloma wierszami w drugiej tabeli. Jest ona zwykle realizowana za pomocą tabeli pośredniczącej, zwanej tabelą łączącą lub asocjacyjną, która łączy w sobie klucze główne obu tabel.
4. **Relacja samo-do-siebie (Self-Referencing)**:
    
    - Jest to relacja, w której klucze w jednej tabeli odnoszą się do kluczy tej samej tabeli. Na przykład tabela pracowników, w której jeden pracownik może być przełożonym innego pracownika.

Te są najbardziej powszechne w środowisku MS SQL Server, ale istnieją również inne bardziej zaawansowane typy relacji, które mogą być używane w zależności od potrzeb projektu.

## Definiowanie relacji między tabelami

Oczywiście, oto jak można zdefiniować pierwsze cztery typy relacji w Microsoft SQL Server:

1. **Relacja jeden-do-jeden (One-to-One)**:
    
    - Aby zdefiniować relację jeden-do-jeden, musisz użyć klucza obcego w jednej tabeli, który odnosi się do klucza głównego w drugiej tabeli. Na przykład:
    
    ```
    CREATE TABLE TableA (
        ID INT PRIMARY KEY,
        Column1 VARCHAR(50),
        Column2 INT
    );
    
    CREATE TABLE TableB (
        ID INT PRIMARY KEY,
        Column3 VARCHAR(50),
        TableA_ID INT FOREIGN KEY REFERENCES TableA(ID) -- klucz obcy wskazujący na klucz główny w TableA
    );
    
    ```
    
2. **Relacja jeden-do-wielu (One-to-Many)**:
    
    - W relacji jeden-do-wielu, klucz obcy wskazuje na klucz główny w innej tabeli. Na przykład:
    
    ```
    CREATE TABLE Customer (
        ID INT PRIMARY KEY,
        FirstName VARCHAR(50),
        LastName VARCHAR(50)
    );
    
    CREATE TABLE Order (
        ID INT PRIMARY KEY,
        OrderNumber VARCHAR(20),
        Customer_ID INT FOREIGN KEY REFERENCES Customer(ID) -- klucz obcy wskazujący na klucz główny w Customer
    );
    
    ```
    
3. **Relacja wiele-do-wielu (Many-to-Many)**:
    
    - W relacji wiele-do-wielu, tworzysz tabelę pośredniczącą, która łączy klucze główne obu tabel. Na przykład:
    
    ```
    CREATE TABLE Student (
        ID INT PRIMARY KEY,
        FirstName VARCHAR(50),
        LastName VARCHAR(50)
    );
    
    CREATE TABLE Course (
        ID INT PRIMARY KEY,
        Name VARCHAR(100)
    );
    
    CREATE TABLE Student_Course (
        Student_ID INT,
        Course_ID INT,
        PRIMARY KEY (Student_ID, Course_ID),
        FOREIGN KEY (Student_ID) REFERENCES Student(ID),
        FOREIGN KEY (Course_ID) REFERENCES Course(ID)
    );
    
    ```
    
4. **Relacja samo-do-siebie (Self-Referencing)**:
    
    - W relacji samo-do-siebie, klucz obcy wskazuje na klucz główny tej samej tabeli. Na przykład:
    
    ```
    CREATE TABLE Employee (
        ID INT PRIMARY KEY,
        FirstName VARCHAR(50),
        LastName VARCHAR(50),
        Supervisor_ID INT,
        FOREIGN KEY (Supervisor_ID) REFERENCES Employee(ID)
    );
    
    ```
    

### Opcjonalność relacji

Domyślnie, czyli bez jawnego zdefiniowania braku możliwości wartości `NULL` dla klucza obcego, klucz obcy może przyjmować wartości `NULL`, a to oznacza, że jest to relacja opcjonalna - wiersze z jednej tabeli, mogą, ale nie muszą mieć powiązanie z wierszami drugiej tabeli. Aby zapobiec temu, możesz użyć klauzuli `NOT NULL` w definicji klucza obcego. Na przykład:

```
CREATE TABLE TableA (
    ID INT PRIMARY KEY,
    Column1 VARCHAR(50),
    Column2 INT
);

CREATE TABLE TableB (
    ID INT PRIMARY KEY,
    Column3 VARCHAR(50),
    TableA_ID INT NOT NULL FOREIGN KEY REFERENCES TableA(ID) -- klucz obcy nie może przyjmować wartości NULL
);

```

## Usuwanie tabel z relacjami

Jeśli chcesz usunąć tabelę, która ma relacje z innymi tabelami, musisz najpierw usunąć relacje, a następnie usunąć tabelę. Na przykład, a między tabelami `TableA` i `TableB` jest relacja jeden-do-jeden, a chcesz usunąć tabelę `TableA`, musisz najpierw usunąć relację (albo tabelę zależną), a następnie usunąć tabelę docelową. Oto jak to zrobić:

```

ALTER TABLE TableB
DROP CONSTRAINT <nazwa ograniczenia (constraint)>; -- usuń relację

DROP TABLE TableA; -- usuń tabelę

```

Jeżeli najpierw spróbował byś usunać tabelę `TableA`, otrzymałbyś błąd, ponieważ tabela `TableA` ma relację z tabelą `TableB`.

## Jawne nazywanie ograniczenia relacji

W powyższych przykładach, nazwy ograniczeń relacji są generowane automatycznie przez system bazodanowy. Możesz jednak nadać im własne nazwy, co ułatwi zarządzanie nimi. Oto jak to zrobić:

```
 
CREATE TABLE TableA (
    ID INT PRIMARY KEY,
    Column1 VARCHAR(50),
    Column2 INT
);

CREATE TABLE TableB (
    ID INT PRIMARY KEY,
    Column3 VARCHAR(50),
    TableA_ID INT, -- kolumna klucza obcego (bez ograniczenia)
    CONSTRAINT FK_TableB_TableA FOREIGN KEY (TableA_ID) REFERENCES TableA(ID) -- Jawnie nazwane ograniczenie klucza obcego
);

```

## Dodawanie relacji do istniejących tabel

Jeśli chcesz dodać relację do istniejących tabel, możesz użyć polecenia `ALTER TABLE`. Na przykład, aby dodać relację jeden-do-wielu do istniejących tabel, możesz użyć poniższego polecenia:

```

-- Krok 1: Dodaj nową kolumnę do tabeli
ALTER TABLE TableB
ADD TableA_ID INT;

-- Krok 2: Dodaj ograniczenie klucza obcego, odnoszące się do nowej kolumny
ALTER TABLE TableB
ADD CONSTRAINT FK_TableB_TableA FOREIGN KEY (TableA_ID) REFERENCES TableA(ID);


```

## Zadanie praktyczne

Do bazy `LibraryDatabase` dodaj nowe tabele:

1. `Users` z kolumnami:
    
    - `UserId` - klucz główny
    - `Name` - imię użytkownika
    - `Surname` - nazwisko użytkownika
    - `Email` - adres email użytkownika
    - `PhoneNumber` - numer telefonu użytkownika (opcjonalnie)
2. `Addresses` z kolumnami:
    
    - `AddressId` - klucz główny
    - `City` - miasto zamieszkania
    - `Street` - ulica zamieszkania
    - `HouseNumber` - numer domu
    - `Country` - kraj zamieszkania

Następnie utworz poniższe relacje:

- `Users` i `Address` - relacja jeden do jednego
- `Books` i `Authors` - relacja jeden do wielu
- `Books` i `Genres` - relacja jeden do wielu
- `Copies` i `Books` - relacja jeden do wielu
- `Users` i `Copies` - relacja wiele do wielu w postaci tabeli pośredniej `Loans` z kolumnami:
    - `LoanId` - klucz główny
    - `UserId` - klucz obcy do tabeli `Users`
    - `CopyId` - klucz obcy do tabeli `Copies`
    - `LoanDate` - data wypożyczenia
    - `ReturnDate` - data zwrotu (opcjonalnie)


```sql
-- ROZWIĄZANIE
CREATE TABLE Addresses (
    AddressId INT PRIMARY KEY IDENTITY(1,1),
    City NVARCHAR(50) NOT NULL,
    Street NVARCHAR(50) NOT NULL,
    HouseNumber NVARCHAR(10) NOT NULL,
    Country NVARCHAR(50) NOT NULL,
)

CREATE TABLE Users (
    UserId INT PRIMARY KEY IDENTITY(1,1),
    Name NVARCHAR(50) NOT NULL,
    Surname NVARCHAR(50) NOT NULL,
    Email NVARCHAR(50) NOT NULL,
    PhoneNumber NVARCHAR(25),
    AddressId INT,
    CONSTRAINT FK_Users_Addresses FOREIGN KEY (AddressId) REFERENCES Addresses(AddressId) 
)

ALTER TABLE Books
ADD AuthorId INT;

ALTER TABLE Books
ADD CONSTRAINT FK_Books_Authors FOREIGN KEY (AuthorId) REFERENCES Authors(AuthorId);

ALTER TABLE Books
ADD GenreId INT NOT NULL;

ALTER TABLE Books
ADD CONSTRAINT FK_Books_Genres FOREIGN KEY (GenreId) REFERENCES Genres(GenreId);

ALTER TABLE Copies
ADD BookId INT NOT NULL;

ALTER TABLE Copies
ADD CONSTRAINT FK_Copies_Books FOREIGN KEY (BookId) REFERENCES Books(BookId);

CREATE TABLE Loans (
    LoanId INT PRIMARY KEY IDENTITY(1,1),
    UserId INT NOT NULL,
    CopyId INT NOT NULL,
    LoanDate DATETIME2 NOT NULL,
    ReturnDate DATETIME2 NULL,
    CONSTRAINT FK_Loans_Users FOREIGN KEY (UserId) REFERENCES Users(UserId),
    CONSTRAINT FK_Loans_Copies FOREIGN KEY (CopyId) REFERENCES Copies(CopyId),
)
```
