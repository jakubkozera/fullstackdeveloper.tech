# TRY..CATCH



Pisząc róźnego rodzaju skrypty, zdarza się, że kod może wygenerować błąd. W takich sytuacjach przydatna jest konstrukcja `TRY...CATCH`, która służy do obsługi błędów podczas wykonywania zapytań. Oto jak działa:



**Struktura:**



```sql
BEGIN TRY
  -- Blok kodu, który może potencjalnie spowodować błąd
END TRY

BEGIN CATCH
  -- Blok kodu, który zostanie wykonany w przypadku wystąpienia błędu w bloku TRY
END CATCH
```



**Jak to działa:**



* **Blok TRY:** Zawiera kod, który może potencjalnie spowodować błąd.





* **Blok CATCH:**: Zawiera kod, który zostanie wykonany w przypadku wystąpienia błędu w bloku TRY.

    

    Można tutaj:

    - Wyświetlić komunikat o błędzie użytkownikowi. Informacje o błędzie można uzyskać za pomocą funkcji `ERROR_MESSAGE()`.

    - Zalogować błąd.

    - Wycofać transakcję (jeśli została rozpoczęta).

    - Podjąć inne czynności naprawcze.



**Ważne uwagi:**





* Konstrukcji TRY...CATCH nie można używać wewnątrz funkcji zdefiniowanych przez użytkownika.

* Jeśli w bloku TRY wystąpi błąd składni, blok CATCH nie zostanie uruchomiony.



**Przykład:**




```sql
BEGIN TRY
  -- Kod, który może spowodować błąd, np. dzielenie przez zero
  PRINT '1'
  SELECT 10 / 0;
  PRINT '2'
END TRY

BEGIN CATCH
  -- Wyświetlenie komunikatu o błędzie
  PRINT 'Wystąpił błąd: ' + ERROR_MESSAGE();
END CATCH
```

TRY...CATCH często jest stosowany w wycofywaniu transakcji, w przypadku wystąpienia błędu. 




```sql
BEGIN TRY
    BEGIN TRAN
    INSERT INTO Authors (FirstName, LastName, BirthDate, Country)
    VALUES ('Akira', 'Toriyama', '1955-04-05', 'Japan');
    Declare @authorId INT = SCOPE_IDENTITY()
    Declare @genreId INT = (SELECT TOP 1 GenreId FROM Genres WHERE [Name] = 'Historical') -- NULL
    INSERT INTO Books (Title, Description, PublicationDate, ISBN, AuthorId, GenreId)
    VALUES ('New Historical book', 'A first book in the series', '2020-03-03', '95532123423', @authorId, @genreId) -- Dla @genreId NULL wystąpi błąd
    COMMIT TRANSACTION
END TRY
BEGIN CATCH
    -- Jeśli wystąpi błąd, wykonaj obsługę błędu
    ROLLBACK TRANSACTION; -- Wycofanie transakcji w przypadku błędu
    -- Dodatkowe działania mogą być podejmowane, na przykład logowanie błędu
    PRINT 'Wystąpił błąd: ' + ERROR_MESSAGE();
END CATCH;
```
