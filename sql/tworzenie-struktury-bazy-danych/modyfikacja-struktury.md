# Modyfikacja struktury

Poza tworzeniem nowych tabel i relacji między nimi, za pomocą poleceń SQL będziemy też w stanie modyfikować już istniejące struktury. Przykładowo, kiedy będziemy mieli potrzebę dodania nowej kolumny do tabeli, zmiany typu kolumny, usunięcia kolumny, zmiany nazwy kolumny, zmiany nazwy tabeli, usunięcia tabeli, dodania nowej relacji, itp.
### Dodawanie nowej kolumny
Jak już widzieliśmy na poprzednich przykładach aby dodać nową kolumnę do istniejącej tabeli, używamy polecenia `ALTER TABLE` z klauzulą `ADD`.
```
ALTER TABLE table_name
ADD column_name column_type;
```
### Utworzenie relacji między istniejącymi tabelami
W celu utworzenia relacji między istniejącymi tabelami, używamy polecenia `ALTER TABLE` z klauzulą `ADD CONSTRAINT` i podajemy nazwę relacji, typ relacji, nazwę kolumny z tabeli źródłowej oraz nazwę kolumny z tabeli docelowej.
```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
FOREIGN KEY (column_name) REFERENCES table_name(column_name);
```
### Zmiana nazwy relacji
Zmienienie nazwy relacji wiąże się z usunięciem starej relacji i utworzeniem nowej relacji z nową nazwą. W tym celu używamy polecenia `ALTER TABLE` z klauzulą `DROP CONSTRAINT` i `ADD CONSTRAINT`.
### Usunięcie relacji
Aby usunąć relację, używamy polecenia `ALTER TABLE` z klauzulą `DROP CONSTRAINT`.
```
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```
### Zmiana nazwy kolumny
Aby zmienić nazwę kolumny, używamy polecenia `EXEC` z funkcją `sp_rename`, gdzie podajemy starą nazwę kolumny, nową nazwę kolumny oraz typ obiektu, który chcemy zmienić.
```
EXEC sp_rename 'Samples.Name',  'NewName', 'COLUMN';
```
### Zmiana typu kolumny
Jeżeli chcemy zmienić typ kolumny, używamy polecenia `ALTER TABLE` z klauzulą `ALTER COLUMN`.
```
ALTER TABLE table_name
ALTER COLUMN column_name new_column_type;
```
Przy zmianie typu kolumny, warto pamiętać, że nowy typ kolumny musi być zgodny z typem danych, które są już w tej kolumnie. W przeciwnym razie, otrzymamy błąd. Np. jeżeli kolumna zawiera dane tekstowe, to nie możemy zmienić typu tej kolumny na typ liczbowy.
### Usunięcie kolumny
W celu usunięcia kolumny z istniejącej tabeli, używamy polecenia `ALTER TABLE` z klauzulą `DROP COLUMN`.
```
ALTER TABLE table_name
DROP COLUMN column_name;
```
### Zmiana nazwy tabeli
Aby zmienić nazwę tabeli, używamy polecenia `EXEC` z funkcją `sp_rename`, gdzie podajemy starą nazwę tabeli oraz nową nazwę tabeli.
```
EXEC sp_rename 'OldTable', 'NewTable';
```
### Usunięcie tabeli
W celu usunięcia tabeli, używamy polecenia `DROP TABLE`.
```
DROP TABLE table_name;
```


## Przykładowe wywołania na nowej tabeli



```sql
-- UTWORZENIE TABELI
CREATE TABLE Samples  (
	SampleId INT PRIMARY KEY IDENTITY(1,1),
    Name NVARCHAR(50),
)

-- DODANIE KOLUMNY
ALTER TABLE Samples
ADD BookId INT;

-- DODANIE FK
ALTER TABLE Samples
ADD CONSTRAINT FK_Samples_Books
FOREIGN KEY (BookId) REFERENCES Books(BookId);

-- USUNIĘCIE FK
ALTER TABLE Samples
DROP CONSTRAINT FK_Samples_Books;

-- ZMIANA NAZWY KOLUMNY
EXEC sp_rename 'Samples.Name',  'NewName', 'COLUMN';

-- ZMIANA TYPU DANYCH KOLUMNY
ALTER TABLE Samples
ALTER COLUMN [NewName] NVARCHAR(100);

-- USUNIĘCIU KOLUMNY
ALTER TABLE Samples
DROP COLUMN [NewName];

-- ZMIANA NAZWY TABELI
EXEC sp_rename 'Samples', 'NewSamples';

-- USUNUNIĘCIE TABELI
DROP TABLE NewSamples;
```
