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


(32 rows affected)



Total execution time: 00:00:00.004





<table><tr><th>SalesOrderID</th><th>TotalDue</th><th>OrderSize</th></tr><tr><td>71774</td><td>972,785</td><td>Small order</td></tr><tr><td>71776</td><td>87,0851</td><td>Small order</td></tr><tr><td>71780</td><td>42452,6519</td><td>Big order</td></tr><tr><td>71782</td><td>43962,7901</td><td>Big order</td></tr><tr><td>71783</td><td>92663,5609</td><td>Big order</td></tr><tr><td>71784</td><td>119960,824</td><td>Big order</td></tr><tr><td>71796</td><td>63686,2708</td><td>Big order</td></tr><tr><td>71797</td><td>86222,8072</td><td>Big order</td></tr><tr><td>71815</td><td>1261,444</td><td>Small order</td></tr><tr><td>71816</td><td>3754,9733</td><td>Small order</td></tr><tr><td>71831</td><td>2228,0566</td><td>Small order</td></tr><tr><td>71832</td><td>39531,6085</td><td>Big order</td></tr><tr><td>71845</td><td>45992,3665</td><td>Big order</td></tr><tr><td>71846</td><td>2711,4098</td><td>Small order</td></tr><tr><td>71856</td><td>665,4251</td><td>Small order</td></tr><tr><td>71858</td><td>15275,1977</td><td>Big order</td></tr><tr><td>71863</td><td>3673,3249</td><td>Small order</td></tr><tr><td>71867</td><td>1170,5376</td><td>Small order</td></tr><tr><td>71885</td><td>608,1766</td><td>Small order</td></tr><tr><td>71895</td><td>272,6468</td><td>Small order</td></tr><tr><td>71897</td><td>14017,9083</td><td>Big order</td></tr><tr><td>71898</td><td>70698,9922</td><td>Big order</td></tr><tr><td>71899</td><td>2669,3183</td><td>Small order</td></tr><tr><td>71902</td><td>81834,9826</td><td>Big order</td></tr><tr><td>71915</td><td>2361,6403</td><td>Small order</td></tr><tr><td>71917</td><td>45,1995</td><td>Small order</td></tr><tr><td>71920</td><td>3293,7761</td><td>Small order</td></tr><tr><td>71923</td><td>117,7276</td><td>Small order</td></tr><tr><td>71935</td><td>7330,8972</td><td>Small order</td></tr><tr><td>71936</td><td>108597,9536</td><td>Big order</td></tr><tr><td>71938</td><td>98138,2131</td><td>Big order</td></tr><tr><td>71946</td><td>43,0437</td><td>Small order</td></tr></table>



Zwróc uwagę na to, że warunki są sprawdzane, dopóki nie zostaną spełnione. Ponownie, jeżeli żadna z wartości nie spełnia warunku, to trafiamy do instrukcji `ELSE`, a jeżeli jej nie ma, to zwrócona zostaje wartość `NULL`.
