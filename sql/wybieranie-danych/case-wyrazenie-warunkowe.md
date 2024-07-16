# `CASE` - wyrażenie warunkowe

Czasem pisząc zapytania SQL, będziemy mieli potrzebę zmienienia wartości zwracanej z danej kolumny na inną postać, przykładowo, status zamówienia, który może być w bazie zapisywanany jako wartość numeryczna: 1,2,3 ... może być reprezentowany jako wartość teskstowa: "Złożono zamówienie", "Opłacono", "Wysłano"..  

Tego typu mapowanie wartości zwracanej, uzyskamy za pomocą `CASE`

  

W języku SQL, `CASE` jest wyrażeniem warunkowym, które umożliwia wykonanie różnych działań w zależności od spełnienia określonych warunków. Można go używać w zapytaniach `SELECT`, `WHERE`, `HAVING` oraz innych klauzulach, aby manipulować wynikami zapytania na podstawie określonych kryteriów.

Najczęściej stosuje się je w klauzuli `SELECT`, aby zwrócić wartość na podstawie spełnionego warunku.

Istnieją dwa główne rodzaje wyrażenia `CASE`:

1. **Proste wyrażenie CASE:** Sprawdza wyrażenie i zwraca wartość na podstawie pierwszego spełnionego warunku.
    
    ```
    CASE expression
        WHEN value1 THEN result1
        WHEN value2 THEN result2
        ...
        ELSE elseResult
    END
    
    ```
    
2. **Skrócone wyrażenie CASE:** Wykonuje porównanie między wyrażeniem a serią warunków. Jeśli warunek jest spełniony, zwraca określoną wartość.
    
    ```
    CASE
        WHEN condition1 THEN result1
        WHEN condition2 THEN result2
        ...
        ELSE elseResult
    END
    
    ```
    

**Przykład użycia:**

Proste wyrażenie CASE:


```sql
SELECT 

    Name,

    CASE Color

        WHEN 'Black' THEN 'Czarny'

        WHEN 'Red' THEN 'Czerwony'

        ELSE Color 

    END AS TranslatedColor

FROM SalesLT.Product;


```

Jeśli nie podamy bloku ELSE, a wartość nie będzie dopasowana, to domyślnie w daną kolumnę zostanie wprowadzona wartość `NULL`.

Sprawdźmy jak zachowa się to samo zapytanie bez: `ELSE Color`:




```sql
SELECT 

    Name,

    CASE Color

        WHEN 'Black' THEN 'Czarny'

        WHEN 'Red' THEN 'Czerwony'

    END AS TranslatedColor

FROM SalesLT.Product;
```

Drugą wersję `CASE` będziemy musieli używać w przypadku sprawdzenia wartości na podstawie warunku logicznego, przykładowo porównując do konkrentej wartości


```sql
SELECT 

    SalesOrderID,

    TotalDue,

    CASE 

        WHEN TotalDue > 10000 THEN 'Big order'

        WHEN TotalDue > 5000 AND Comment != 'TEST' THEN 'Medium order'

        ELSE 'Small order'

    END AS OrderSize

FROM SalesLT.SalesOrderHeader
```
