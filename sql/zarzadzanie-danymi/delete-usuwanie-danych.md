# `DELETE` - usuwanie danych

Poza dodawaniem i modyfikowaniem danych, dane możemy też usuwać z tabel.

Klauzula `DELETE` w MS SQL służy do usuwania rekordów z tabel bazy danych. Jest to jedna z podstawowych instrukcji języka SQL, używanych do manipulowania danymi.

### Składnia:

```
DELETE FROM nazwa_tabeli
[WHERE warunek];

```

- `DELETE`: Słowo kluczowe informujące system SQL o operacji usuwania.
- `FROM`: Określa tabelę, z której mają zostać usunięte rekordy.
- `nazwa_tabeli`: Podaj nazwę tabeli, z której chcesz usunąć dane.
- `WHERE`: Opcjonalna klauzula służąca do określenia warunku, który muszą spełniać rekordy, aby zostać usuniętymi.
- `warunek`: Określa kryteria, na podstawie których wybierane są rekordy do usunięcia.

**Przykład:**

Usuń wszystkie rekordy z tabeli `Copies`, których stan jest `Bad`

```
DELETE FROM Copies
WHERE Condition = 'Bad'

```

### Ważne uwagi:

- Usunięcie rekordów za pomocą klauzuli DELETE jest **nieodwracalne**. Przed wykonaniem takiej operacji, upewnij się, że masz kopię zapasową danych.
- Należy zachować ostrożność podczas używania klauzuli DELETE bez klauzuli `WHERE`. Spowoduje to usunięcie **wszystkich** rekordów z tabeli.
- Klauzula DELETE może być używana w połączeniu z innymi instrukcjami SQL, takimi jak `SELECT` i `JOIN`, aby precyzyjnie określić, które rekordy mają zostać usunięte.

## `DELETE` z klazulą `SELECT`

Możemy również użyć klauzuli `DELETE` w połączeniu z klauzulą `SELECT`, aby usunąć rekordy, które spełniają określone kryteria, po to, aby zamiast hardcodować np. `id`, które chcemy usunąć, możemy je wybrać dynamicznie.

**Przykład:**

Usuń wszysztkie rekordy z tabeli `Copies`, dla książek, których autorem jest `Stephen King`

```
DELETE FROM Copies
WHERE BookId IN (SELECT BookId FROM Books
                JOIN Authors a ON Books.AuthorId = a.AuthorId
                WHERE a.FirstName = 'Stephen' AND a.LastName = 'King')

```

## `DELETE` z klauzulą `JOIN`

Możemy również użyć klauzuli `DELETE` w połączeniu z klauzulą `JOIN`, aby usunąć rekordy z jednej tabeli, które spełniają określone kryteria w innej tabeli.

**Przykład:**

Usuń wszysztkie rekordy z tabeli `Copies`, dla książek, których autorem jest `Stephen King`

```
DELETE Copies
FROM Copies
JOIN Books ON Copies.BookId = Books.BookId
JOIN Authors a ON Books.AuthorId = a.AuthorId
WHERE a.FirstName = 'Stephen' AND a.LastName = 'King'

```

## `DELETE` a wartości powiązane

Jeśli usuwamy rekordy z tabeli, które są powiązane z innymi rekordami w innych tabelach, musimy upewnić się, że te powiązane rekordy są najpierw usunięte. W przeciwnym razie, operacja `DELETE` może spowodować błąd, jeśli naruszy ograniczenia klucza obcego.

Czyli przykładowo, jeżeli chcielibyśmy usunać wpis z tabeli `Addresses`, który jest powiązany z rekordem w tabeli `Users`, musimy najpierw usunąć rekord z tabeli `Users`, a następnie rekord z tabeli `Addresses` - o ile ponownie przy usuwaniu z tabeli `Users` nie naruszymy ograniczeń klucza obcego.

Tak więc, żeby usunać rekord z dowolnej tabeli, który jest powiązany z innymi rekordami w innych tabelach, musimy najpierw usunąć rekordy z tych innych tabel, które są z nimi powiązane. Albo o ile to możliwe, zmienić klucz obcy w tabeli powiązanej na `NULL` (jeśli jest to dozwolone).


```sql
SELECT * 
FROM Addresses
SELECT *
FROM Users
```


```sql
-- PRÓBA USUNIĘCIA WPISÓW Z TABELI ADDRESSES, Z KTÓRYM POWIĄZANY JEST REKORD Z TABELI USERS
DELETE FROM Addresses
WHERE Country = 'USA'
```




The statement has been terminated.



Przykładowe rozwiązanie problemu z ustawieniem wartości `NULL` dla kolumny `AddressId` w tabeli `Users`


```sql
UPDATE Users
SET AddressId = NULL
WHERE AddressId IN (SELECT AddressId FROM Addresses WHERE Country = 'USA')
DELETE FROM Addresses
WHERE Country = 'USA'
```



Innym podejściem byłoby najpierw usunięcie powiązanych rekordów z tabeli `Users` - o ile inne referencje nie zablokują operacji.


```sql
DELETE Users
WHERE AddressId IN (SELECT AddressId FROM Addresses WHERE Country = 'UK')
DELETE FROM Addresses
WHERE Country = 'UK'
```



