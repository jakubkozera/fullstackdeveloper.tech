## UPDATE - modyfikacja danych

Aktualizacja danych jest jedną z kluczowych operacji w zarządzaniu bazami danych. Pozwala na zmianę istniejących rekordów w tabelach, co jest niezbędne w dynamicznym środowisku biznesowym. W systemach bazodanowych, takich jak Microsoft SQL Server (MS SQL) istnieje specjalne polecenie `UPDATE`, które umożliwia dokonywanie takich zmian. 

### Składnia Polecenia UPDATE w MS SQL

Polecenie UPDATE w MS SQL służy do modyfikacji istniejących rekordów w tabelach. Jego składnia jest względnie prosta i wygląda następująco:

```
UPDATE nazwa_tabeli
SET kolumna1 = wartość1, kolumna2 = wartość2, ...
WHERE warunek;

```

- `nazwa_tabeli`: Określa nazwę tabeli, w której chcemy dokonać aktualizacji.
- `kolumna1 = wartość1, kolumna2 = wartość2, ...`: Określa konkretne kolumny, które chcemy zaktualizować, oraz ich nowe wartości.
- `WHERE warunek`: Jest opcjonalnym elementem, który pozwala na określenie warunku, który musi być spełniony przez rekordy, aby zostały zaktualizowane. Jeśli ten fragment jest pominięty, wszystkie rekordy w tabeli zostaną zaktualizowane.

### Przykładowe Zastosowania Polecenia UPDATE

#### 1\. Aktualizacja Danych o Autorze

Załóżmy, że chcemy zaktualizować datę urodzenia autora w tabeli `Authors`. Przykładowo, zmieniamy datę urodzenia dla autora o identyfikatorze `3` na `1980-05-15`.


```sql
UPDATE Authors
SET BirthDate = '1980-05-15'
WHERE AuthorId = 3;
```

#### 2\. Zmiana Numeru Telefonu Użytkownika

Jeśli użytkownik zmienia numer telefonu, musimy zaktualizować ten szczegół w tabeli `Users`. Załóżmy, że użytkownik o identyfikatorze `2` zmienia numer telefonu na `123-456-789`.

 


```sql
UPDATE Users
SET PhoneNumber = '123-456-789'
WHERE UserId = 2;
```

#### 3\. Modyfikacja Stanu Egzemplarza Książki

Jeśli stan egzemplarza książki się zmienia (na przykład w wyniku naprawy lub zniszczenia), możemy zaktualizować tę informację w tabeli `Copies`. Załóżmy, że zmieniamy stan egzemplarza o identyfikatorze <span style="font-size: 12px;">1&nbsp;</span> na "<span style="color: rgb(206, 145, 120); font-family: Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; white-space: pre;">Not good</span><span style="color: var(--vscode-foreground);">".</span>


```sql
UPDATE Copies
SET Condition = 'Not good'
WHERE CopyId = 1;
```

### Aktualizacja z użyciem danych z innej tabeli

Czasami potrzebujemy zaktualizować dane w jednej tabeli na podstawie informacji z innej tabeli.
Przykładowo, jeżeli chcielibyśmy zmodyfikować powiązanie książki, z autorem na podstawie wartości `AuthorId`, to zamiast hard-codoania wartości `AuthorId` w zapytaniu `UPDATE`, możemy użyć zapytania `FROM` do pobrania wartości `AuthorId` z tabeli `Authors` i użyć jej w zapytaniu `UPDATE`.


```sql
UPDATE Books
SET AuthorId = a.AuthorId
FROM Authors a
WHERE Books.BookId = 2 AND a.FirstName = 'Stephen' AND a.LastName = 'King'
```

Zauważ, że w klauzuli `FROM` jesteśmy w stanie użyć alias, natomiast w `UPDATE`, juz nie, ale nadal możemy filtorwać wiersze z tabeli `Books`, w klauzuli `WHERE`, specyfikując kolumny pełną nazwą (tabela.kolumna).

Co więcej, jeżeli byłaby potrzeba połączyć wielu tabel, to również możemy wykorzystać klazulę `JOIN`, aby połączyć tabele, a następnie filtrować wiersze w klauzuli `WHERE`.


## `UPDATE`, a ograniczenia

Wykonując polecenie `UPDATE`, nadal będą obowiązywały nas ograniczenia zdefiniowane w tabeli, podobnie jak to miało miejsce przy tworzeniu nowych wpisów. Przykładowo, na tabeli `Genres` mieliśmy ograniczenie, które wymagało, aby długość nazwy gatunku była większa niż 2 znaki. W poniższym przykładzie spróbujemy zmienić nazwę gatunku na taką, która przekracza to ograniczenie.




```sql
UPDATE Genres
SET Name = 'SF'
WHERE GenreId = 1
```




The statement has been terminated.



Total execution time: 00:00:00.001


Podobny błąd dostaniemy również np. podczas ustawiania klucza obcego, który nie istnieje w tabeli, do której chcemy go przypisać.




```sql
UPDATE Books
SET AuthorId = 9999
WHERE BookId = 2
```




The statement has been terminated.



Total execution time: 00:00:00.002



#### Podsumowanie

Polecenie `UPDATE` w MS SQL jest niezwykle przydatnym narzędziem do aktualizacji danych w bazach danych. Pozwala ono na skuteczną zmianę istniejących rekordów zgodnie z określonymi warunkami. Zrozumienie składni i zastosowań tego polecenia jest kluczowe dla skutecznego zarządzania danymi w środowisku SQL Server. Pamiętajmy jednak, żeby zawsze ostrożnie korzystać z tego rodzaju operacji, aby uniknąć przypadkowego uszkodzenia danych.
