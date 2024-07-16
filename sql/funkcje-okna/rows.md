##  `ROWS`

`ROWS` to jedna z opcji używana w funkcjach okna, która pozwala definiować ramy okna. Ramy okna określają zbiór wierszy, które są brane pod uwagę przez funkcję okna w trakcie wykonywania operacji. 

W kontekście funkcji okna, `ROWS` jest jedną z dwóch dostępnych opcji definiowania ramek, obok `RANGE`. Obie te opcje różnią się sposobem określania zasięgu wierszy w ramce:

1. **`ROWS`**: Specyfikuje dokładną liczbę wierszy w ramce, niezależnie od wartości danych. Używając `ROWS`, definiujesz ramkę jako pewną liczbę wierszy przed i/lub po bieżącym wierszu.

2. **`RANGE`**: Specyfikuje ramkę w oparciu o zakres wartości danych w określonej kolumnie. Używając `RANGE`, możesz określić ramkę jako wszystkie wiersze, które mają wartości w określonym zakresie względem bieżącego wiersza.


### Wartości `ROWS`

1. **UNBOUNDED PRECEDING**: Określa, że ramka zaczyna się od pierwszego wiersza w zestawie wyników (czyli od początku zestawu wyników lub partycji).

2. **UNBOUNDED FOLLOWING**: Określa, że ramka kończy się na ostatnim wierszu w zestawie wyników (czyli do końca zestawu wyników lub partycji).

3. **CURRENT ROW**: Określa, że ramka zawiera tylko bieżący wiersz.

4. **n PRECEDING**: Określa, że ramka zaczyna się `n` wierszy przed bieżącym wierszem.

5. **n FOLLOWING**: Określa, że ramka kończy się `n` wierszy po bieżącym wierszu.

Te wartości mogą być używane w różnych kombinacjach, aby określić ramy wierszy, które będą brane pod uwagę przez funkcję okna. Poniżej znajdują się przykłady różnych kombinacji:

### Przykłady użycia ROWS w ramach okna

1. **ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING**:
   - Cały zestaw wyników będzie brany pod uwagę.

   ```sql
   SELECT
       column1,
       SUM(column2) OVER (ORDER BY column1 ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS sum_column2
   FROM
       table_name;
   ```

2. **ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW**:
   - Zaczyna od pierwszego wiersza do bieżącego wiersza.

   ```sql
   SELECT
       column1,
       SUM(column2) OVER (ORDER BY column1 ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS sum_column2
   FROM
       table_name;
   ```

3. **ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING**:
   - Od bieżącego wiersza do ostatniego wiersza w zestawie wyników.

   ```sql
   SELECT
       column1,
       SUM(column2) OVER (ORDER BY column1 ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS sum_column2
   FROM
       table_name;
   ```

4. **ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING**:
   - Bieżący wiersz oraz jeden wiersz przed i po bieżącym wierszu.

   ```sql
   SELECT
       column1,
       SUM(column2) OVER (ORDER BY column1 ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS sum_column2
   FROM
       table_name;
   ```

5. **ROWS BETWEEN 2 PRECEDING AND CURRENT ROW**:
   - Zaczyna od dwóch wierszy przed bieżącym wierszem do bieżącego wiersza.

   ```sql
   SELECT
       column1,
       SUM(column2) OVER (ORDER BY column1 ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS sum_column2
   FROM
       table_name;
   ```

6. **ROWS BETWEEN CURRENT ROW AND 2 FOLLOWING**:
   - Od bieżącego wiersza do dwóch wierszy po bieżącym wierszu.

   ```sql
   SELECT
       column1,
       SUM(column2) OVER (ORDER BY column1 ROWS BETWEEN CURRENT ROW AND 2 FOLLOWING) AS sum_column2
   FROM
       table_name;
   ```

### Wartości ROWS

- `UNBOUNDED PRECEDING`
- `UNBOUNDED FOLLOWING`
- `CURRENT ROW`
- `n PRECEDING` (gdzie `n` jest liczbą całkowitą)
- `n FOLLOWING` (gdzie `n` jest liczbą całkowitą)

Te wartości można łączyć w różny sposób w ramach klauzuli `ROWS BETWEEN` w funkcjach okna, co pozwala na elastyczne i precyzyjne określanie zakresu wierszy dla analiz.


### Domyślna wartość zakresu wierszy w funkcji okna

Domyślna ramka okna dla funkcji okna w SQL Server zależy od tego, czy używasz klauzuli `ORDER BY` w funkcji okna. Oto szczegóły:

1. **Bez `ORDER BY`**:
   - Jeśli nie używasz klauzuli `ORDER BY`, domyślną ramką okna jest całe okno. W praktyce oznacza to, że wszystkie wiersze w danym zestawie wyników (lub partycji, jeśli używasz `PARTITION BY`) są brane pod uwagę przez funkcję okna.
   - W praktyce odpowiada to ramce `RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`.

2. **Z `ORDER BY`**:
   - Jeśli używasz klauzuli `ORDER BY`, domyślną ramką okna jest `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`. Oznacza to, że funkcja okna uwzględnia wszystkie wiersze od początku zestawu wyników (lub partycji) do bieżącego wiersza, włączając w to wiersz bieżący.
   - To domyślne zachowanie może mieć różne implikacje w zależności od rodzaju funkcji okna i danych. Na przykład w przypadku funkcji sumujących, takich jak `SUM` lub `AVG`, domyślna ramka będzie uwzględniać wszystkie wiersze do bieżącego wiersza, co może być przydatne do obliczeń bieżących sum lub średnich.

### Przykłady

Wcześniej widzieliśmy przykład, który sumował wartości `OrderQty`, z tabeli `Sales.SalesOrderDetail` i bez użycia `ORDER BY`, domyślnie uwzględniał wszystkie wiersze w partycji. 




```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice,
    SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS OrderQtySum
FROM
    SalesLT.SalesOrderDetail;
```

Teraz zobaczmy, jak zmienia się zachowanie, gdy używamy `ORDER BY`


```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice,
    SUM(OrderQty) OVER(PARTITION BY SalesOrderID ORDER BY OrderQty) AS OrderQtySum
FROM
    SalesLT.SalesOrderDetail;
```

Tym razem, suma jest narastająca, z tym, że wiersze o tej samej wartości są traktowane równorzędnie, jako, że bez jawnego użycia `ROWS`, zakres jest domyślnie `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` - czyli bazuje on na wartościach (wartości mogą być równorzędne), a nie konkretnych wierszach.

Jeżeli teraz do tego samego zapytania, dodamy jawnie użycie `ROWS`, to wynik sumy będzie narastający



```sql
SELECT 
    SalesOrderID,
    SalesOrderDetailID,
    OrderQty,
    UnitPrice,
    SUM(OrderQty) OVER(PARTITION BY SalesOrderID ORDER BY OrderQty ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS OrderQtySum
FROM
    SalesLT.SalesOrderDetail;
```
