## Funkcje warunkowe

Poznaliśmy już instrukcje `CASE`, która była w stanie zwrócić różne wartości w zależności od spełnienia warunków. W SQL mamy jeszcze kilka przydatnych funkcji, które mogą być prostszą alternatywą dla `CASE`.

### `ISNULL`

Funkcja `ISNULL` zwraca wartość podaną jako pierwszy argument, jeśli nie jest ona `NULL`, w przeciwnym wypadku zwraca wartość podaną jako drugi argument.

```sql
SELECT ISNULL(NULL, 1) AS result;
```

Przykładowo, aby zwrócić informacje 'n/a', dla klientów, którzy nie mają wpisanego drugiego imienia:


```sql
SELECT ISNULL(MiddleName, 'n/a') as MiddleName
FROM SalesLT.Customer
```

### `COALESCE`

Funkcja `COALESCE` zwraca pierwszy niepusty argument. Jeśli wszystkie argumenty są puste, zwraca `NULL`.




```sql
SELECT COALESCE(Title, MiddleName, 'n/a') as [COALESCE]
FROM SalesLT.Customer
```

## `NULLIF`

Funkcja `NULLIF` zwraca wartość `NULL`, jeśli dwa argumenty są równe, w przeciwnym razie zwraca pierwszy argument.




```sql
SELECT NULLIF(1, 1) AS result; -- NULL
SELECT NULLIF(1, 2) AS result; -- 1
```

`IIF`

Funkcja `IIF` to skrót od `Immediate If`. Jest to funkcja, która zwraca wartość w zależności od spełnienia warunku. 

```sql
IIF (warunek, wartość_jeśli_prawda, wartość_jeśli_fałsz)
```

### Przykład

```sql
SELECT IIF(1 > 0, 'Prawda', 'Fałsz') AS Wynik;
```

Funkcja ta może posłużyć nam jako zamiennik dla konstrukcji `CASE WHEN`.




```sql
SELECT 
    SalesOrderID,
    TotalDue,
    CASE 
        WHEN TotalDue > 10000 THEN 'Big order'
        ELSE 'Small order'
    END AS OrderSize
FROM SalesLT.SalesOrderHeader

SELECT 
    SalesOrderID,
    TotalDue,
    IIF(TotalDue > 10000, 'Big order', 'Small order') AS OrderSize
FROM SalesLT.SalesOrderHeader;

```
