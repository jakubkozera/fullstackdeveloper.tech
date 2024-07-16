## Funkcje okna

Funkcje okna to zaawansowane funkcje analityczne i agregacyjne, które pozwalają na wykonywanie operacji na zestawie wierszy związanych z bieżącym wierszem bez konieczności używania podzapytań lub dodatkowych tabel. Są one bardzo przydatne do obliczeń, które wymagają kontekstowego przetwarzania danych, takiego jak sumowanie w ramach określonego zakresu wierszy, obliczanie wartości średnich, czy uzyskiwanie rang.

### Podstawowe funkcje okna

1. **Funkcje agregujące**:
    
    - `SUM()`
    - `AVG()`
    - `MAX()`
    - `MIN()`
    - `COUNT()`
    
    Przykład użycia:
    

### Przykładowe dane

Przyjmijmy, że mamy tabelę `employees` z przykładowymi danymi:

| employee\_id | department\_id | salary |
| --- | --- | --- |
| 1 | 10 | 5000 |
| 2 | 20 | 6000 |
| 3 | 10 | 4500 |
| 4 | 30 | 7000 |
| 5 | 20 | 6500 |
| 6 | 30 | 7200 |
| 7 | 10 | 5200 |
| 8 | 20 | 6100 |

### Wynik zapytania z funkcją okna

Poniżej znajduje się wynik zapytania, które oblicza sumę wynagrodzeń w obrębie każdego działu (`department_id`):

```
SELECT 
    employee_id,
    department_id,
    salary,
    SUM(salary) OVER (PARTITION BY department_id) AS department_total_salary
FROM 
    employees;

```

| employee\_id | department\_id | salary | department\_total\_salary |
| --- | --- | --- | --- |
| 1 | 10 | 5000 | 14700 |
| 3 | 10 | 4500 | 14700 |
| 7 | 10 | 5200 | 14700 |
| 2 | 20 | 6000 | 18600 |
| 5 | 20 | 6500 | 18600 |
| 8 | 20 | 6100 | 18600 |
| 4 | 30 | 7000 | 14200 |
| 6 | 30 | 7200 | 14200 |

### Wyjaśnienie wyniku

- **employee\_id**: Identyfikator pracownika.
- **department\_id**: Identyfikator działu, do którego należy pracownik.
- **salary**: Wynagrodzenie pracownika.
- **department\_total\_salary**: Suma wynagrodzeń wszystkich pracowników w danym dziale, obliczona za pomocą funkcji oknaj `SUM(salary) OVER (PARTITION BY department_id)`.

Wynik pokazuje, że dla każdego wiersza (pracownika) sumowane są wynagrodzenia wszystkich pracowników w tym samym dziale (`department_id`). Na przykład, dla działu o identyfikatorze `10` (employee\_id: 1, 3, 7) suma wynagrodzeń wynosi `14700`, a dla działu `20` (employee\_id: 2, 5, 8) suma wynagrodzeń wynosi `18600`.

2. **Funkcje rankingowe**:
    
    - `ROW_NUMBER()`: Nadaje unikalny numer każdemu wierszowi w ramach partycji.
    - `RANK()`: Nadaje numer każdemu wierszowi, ale w przypadku remisów w wartościach, daje te same numery, a następnie przeskakuje numerację.
    - `DENSE_RANK()`: Podobnie jak `RANK()`, ale bez przeskakiwania numeracji.
    - `NTILE(n)`: Dzieli zestaw wierszy na n w miarę równych grup.
    
    Przykład użycia:
    
    ```
    SELECT 
        employee_id,
        salary,
        ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
    FROM 
        employees;
    
    ```
    
3. **Funkcje analityczne**:
    
    - `LAG()`: Zwraca wartość z poprzedniego wiersza w stosunku do bieżącego wiersza w oknie.
    - `LEAD()`: Zwraca wartość z następnego wiersza w stosunku do bieżącego wiersza w oknie.
    - `FIRST_VALUE()`: Zwraca pierwszą wartość w ramach partycji.
    - `LAST_VALUE()`: Zwraca ostatnią wartość w ramach partycji.
    
    Przykład użycia:
    
    ```
    SELECT 
        employee_id,
        salary,
        LAG(salary, 1) OVER (ORDER BY salary) AS previous_salary
    FROM 
        employees;
    
    ```
    

### Składnia funkcji okna

Składnia funkcji okna w MS SQL wygląda tak:

```
funkcja_okna() OVER ([PARTITION BY wyrażenie] [ORDER BY wyrażenie] [ROWS lub RANGE wyrażenie])

```

- **OVER**: Definiuje okno, na którym operuje funkcja.
- **PARTITION BY**: Opcjonalne. Dzieli zestaw wierszy na podzbiory, na których będzie operowała funkcja.
- **ORDER BY**: Opcjonalne, ale często używane. Określa kolejność wierszy w obrębie każdej partycji.
- **ROWS lub RANGE**: Opcjonalne. Określa zakres wierszy do uwzględnienia w oknie.

### Przykład pełnego zapytania z funkcjami okna

```
SELECT 
    employee_id,
    department_id,
    salary,
    SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id) AS running_total,
    AVG(salary) OVER (PARTITION BY department_id) AS average_salary,
    ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank_in_department
FROM 
    employees;

```

W powyższym przykładzie:

- `SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id)` oblicza bieżącą sumę wynagrodzeń w ramach każdego działu, uwzględniając kolejność według `employee_id`.
- `AVG(salary) OVER (PARTITION BY department_id)` oblicza średnie wynagrodzenie w ramach każdego działu.
- `ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC)` nadaje rangę wynagrodzeniom w ramach każdego działu.

Funkcje okna znacznie ułatwiają analizę danych i pozwalają na tworzenie zaawansowanych raportów oraz analiz bez konieczności korzystania z bardziej złożonych konstrukcji SQL.

## Przykładowe zastosowanie

Załóżmy, że mamy potrzebę, wybrać `n` najdroższych produktów z tabeli `SalesLT.Product`.

W tym prostym poleceniu, nie byłoby potrzeby używania funkcji oknaj, jako, że wystarczy posortować dane i wybrać pierwsze `n` wierszy.

```
SELECT TOP (n) Name, ListPrice, ProductCategoryID,
FROM SalesLT.Product
ORDER BY ListPrice DESC;

```

Natomiast, co jeśli chcielibyśmy uzyskać najdroższe `n` produkty w każdej kategorii produktów? W takim przypadku, funkcje okna są bardzo przydatne.

Najpierw, musimy nadać rangę każdemu produktowi w ramach jego kategorii, sortując je według ceny.


```sql
SELECT Name, ListPrice, ProductCategoryID, 
    ROW_NUMBER() OVER(PARTITION BY ProductCategoryID ORDER BY ListPrice DESC) CategoryMostExpensiveRank
FROM [SalesLT].[Product]

```


Następnie, możemy wybrać produkty z najwyższą rangą w każdej kategorii.




```sql
SELECT Name, ListPrice, ProductCategoryID
FROM (
    SELECT Name, ListPrice, ProductCategoryID, ROW_NUMBER() OVER(PARTITION BY ProductCategoryID ORDER BY ListPrice DESC) CategoryMostExpensiveRank
    FROM [SalesLT].[Product]
) ranked
WHERE CategoryMostExpensiveRank <= 3;

```

W tym przykładzie, `PARTITION BY` dzieli produkty na grupy według `ProductCategoryID`, a `ORDER BY` sortuje produkty w każdej grupie według `ListPrice`. Następnie, `ROW_NUMBER()` nadaje rangę każdemu produktowi w ramach jego kategorii - odpowiednio oznaczając każdy wiersz z osobna. W zewnętrznym zapytaniu, wybieramy produkty z najwyższą rangą w każdej kategorii, ograniczając wyniki do `n`.

