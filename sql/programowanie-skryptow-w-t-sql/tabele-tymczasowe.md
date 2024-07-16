# Tabele tymczasowe

Pisząc róźnego rodzaju skrypty w SQL, czasem zdaży się, że potrzebujemy stworzyć tabelę tymczasową, która będzie przechowywać dane tymczasowo, podobnie jak robiły to zmienne zdefiniowane jako: `DECLARE @Zmienna <typ> = <wartość>`, z tym, że tabela tymczasowana jest w stanie przechowywać wiele wierszy, dla wielu kolumn jednocześnie.

W SQL Server mamy do dyspozycji dwie opcje tworzenia tabel tymczasowych: `#Tabela` oraz `##Tabela`.

`#Tabela` jest tworzona w ramach sesji, co oznacza, że jest dostępna tylko dla sesji, w której została utworzona. Po zakończeniu sesji, tabela zostanie usunięta.

`##Tabela` jest tworzona w ramach serwera, co oznacza, że jest dostępna dla wszystkich sesji, które są połączone z serwerem. Po zakończeniu sesji, tabela nie zostanie usunięta, dopóki nie zostanie usunięta ręcznie.

Zazwyczaj nie będziemy mieli potrzeby definiowania tabeli tymczasowej globalnej, dlatego w poniższych przykładach będziemy korzystać z tabeli tymczasowej sesyjnej.

### Tworzenie tabeli tymczasowej

Tabele tymczasowe tworzymy za pomocą polecenia `CREATE TABLE` z dodatkowym znakiem `#` lub `##` przed nazwą tabeli.

```
CREATE TABLE #Tabela (
    Kolumna1 INT,
    Kolumna2 VARCHAR(50)
);

```

### Wstawianie danych do tabeli tymczasowej

Dane wstawiamy do tabeli tymczasowej za pomocą polecenia `INSERT INTO`.

```
INSERT INTO #Tabela (Kolumna1, Kolumna2)
VALUES (1, 'Wiersz 1'),
       (2, 'Wiersz 2'),
       (3, 'Wiersz 3');

```

### `SELECT INTO`

Możemy również skorzystać z polecenia `SELECT INTO`, które pozwala na stworzenie tabeli tymczasowej na podstawie wyniku zapytania `SELECT`.

```
SELECT *
INTO #Tabela
FROM InnaTabela;

```

### Przykład

Załóżmy, że mamy liste państw, dla których chcielibyśmy wyczyścić wszystkie informacje o użytkownikach z danych państw. W tym celu możemy stworzyć tabelę tymczasową, która będzie przechowywać listę państw, dla których chcemy wyczyścić dane - jako, że zwykła zmienna nie jest w stanie przechowywać wielu wartości jednocześnie.


```sql
CREATE TABLE #CountriesToClean (
    Country VARCHAR(50)
);
INSERT INTO #CountriesToClean (Country)
VALUES ('Japan'),
       ('Germany'),
       ('France'),
       ('Italy'),
       ('Australia');

-- wyświetlenie zawartości tabeli tymczasowej
SELECT * FROM #CountriesToClean;
```

Bazując na tej tabeli tymczasowiej, możemy ją teraz wykorzystać do usunięcia informacji o użytkownikach z tych państw.




```sql
BEGIN TRAN
CREATE TABLE #CountriesToClean (
    Country VARCHAR(50)
);
INSERT INTO #CountriesToClean (Country)
VALUES ('Japan'),
       ('Germany'),
       ('France'),
       ('Italy'),
       ('Australia');

-- wyświetlenie zawartości tabeli tymczasowej
SELECT * FROM #CountriesToClean;

-- usunięcie informacji o wypożyczeniach
DELETE l
FROM Loans l
JOIN Users u on u.UserId = l.UserId
JOIN Addresses a on a.AddressId = u.AddressId
WHERE a.Country IN (SELECT Country FROM #CountriesToClean)

-- usunięcie użytkowników
DELETE u
FROM Users u
JOIN Addresses a on a.AddressId = u.AddressId
WHERE a.Country IN (SELECT Country FROM #CountriesToClean)

-- usunięcie adresów
DELETE 
FROM Addresses 
WHERE Country IN (SELECT Country FROM #CountriesToClean)
ROLLBACK TRAN
```

W ten prosty sposób, tworząc tabele tymczasowe, możemy przechowywać wiele wartości w 'jednym miejscu', a następnie wykonywać na nich róźne operacje.
