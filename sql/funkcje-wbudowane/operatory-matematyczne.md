# Operatory matematyczne w SQL



Pracując z róźnymi rodzajami danych, często konieczne jest wykonywanie operacji matematycznych na wartościach liczbowych.





W języku SQL istnieją podstawowe operatory matematyczne, które można używać do wykonywania operacji arytmetycznych na danych numerycznych. Oto lista podstawowych operatorów matematycznych w SQL:



1. **Dodawanie (+)**: Używane do dodawania dwóch wartości.



   ```sql
   SELECT column1 + column2 AS sum FROM table_name;
   ```



2. **Odejmowanie (-)**: Używane do odejmowania jednej wartości od drugiej.



   ```sql
   SELECT column1 - column2 AS difference FROM table_name;
   ```



3. **Mnożenie (*)**: Używane do mnożenia dwóch wartości.



   ```sql
   SELECT column1 * column2 AS product FROM table_name;
   ```



4. **Dzielenie (/)**: Używane do dzielenia jednej wartości przez drugą.



   ```sql
   SELECT column1 / column2 AS quotient FROM table_name;
   ```



5. **Modulo (%)**: Używane do uzyskania reszty z dzielenia jednej wartości przez drugą.



   ```sql
   SELECT column1 % column2 AS remainder FROM table_name;
   ```



6. **Potęgowanie (^)**: Używane do podnoszenia jednej wartości do potęgi drugiej.



   ```sql
   SELECT POWER(column1 [liczba], [potęga]) AS result FROM table_name;
   ```



Te operatory mogą być używane zarówno w zapytaniach SELECT, jak i w innych klauzulach SQL, takich jak WHERE czy ORDER BY, do wykonywania operacji matematycznych na danych numerycznych znajdujących się w kolumnach tabeli.





Przykładowo, aby obliczyć marżę zysku dla produktów w tabeli `Products`, można użyć następującego zapytania SQL:






```sql
SELECT [Name], ListPrice, StandardCost, ListPrice - StandardCost AS ProfitMargin
FROM SalesLT.Product;
```

W języku SQL możemy łączyć operacje matematyczne w ramach jednej kalkulacji, stosując odpowiednie operatory i nawiasy w celu określenia kolejności operacji. Jest to często wykorzystywane, aby wykonać bardziej zaawansowane obliczenia w zapytaniach SQL.



Na przykład, możemy połączyć różne operacje matematyczne, takie jak dodawanie, odejmowanie, mnożenie i dzielenie, w jednej kalkulacji. Poniżej znajduje się przykładowe zapytanie SQL, które wykonuje takie obliczenia:






```sql
SELECT (5 + 3) * 2 / 4 - 1 AS result;
```





W tym przykładzie:

- Najpierw dodajemy 5 i 3, co daje 8.

- Następnie mnożymy wynik przez 2, co daje 16.

- Potem dzielimy wynik przez 4, co daje 4.

- Na końcu odejmujemy 1, co daje ostateczny wynik 3.



Warto zauważyć, że nawiasy są używane w celu jasnego określenia kolejności operacji. Operacje wewnątrz nawiasów są wykonywane najpierw, a następnie wyniki są używane w kolejnych operacjach.



Dlatego też, odpowiednie użycie nawiasów pozwala na wykonywanie złożonych operacji matematycznych w ramach jednej kalkulacji w zapytaniach SQL.



Przykładowo, żeby obliczyć wartość zamówienia, bez części dziesiętnej, możemy użyć następującego zapytania SQL:






```sql
SELECT SalesOrderID, SubTotal, SubTotal - SubTotal % 1 [SubTotalRounded]
FROM [SalesLT].[SalesOrderHeader]
```

## Funkcje matematyczne w SQL



Oprócz operatorów matematycznych, w języku SQL istnieje kilka funkcji, które są używane do wykonywania operacji matematycznych na wartościach liczbowych. Oto kilka przykładów funkcji matematycznych w SQL:



1. **ABS()**: Zwraca wartość bezwzględną danej liczby.






```sql
   SELECT ABS(-10) AS absolute_value; -- Wynik: 10
```



2. **ROUND()**: Zaokrągla daną liczbę do określonej liczby miejsc po przecinku.






```sql
   SELECT ROUND(3.14159, 2) AS rounded_value; -- Wynik: 3.14
```



3. **CEILING()**: Zaokrągla daną liczbę w górę do najbliższej liczby całkowitej.






```sql
   SELECT CEILING(4.3) AS rounded_up_value; -- Wynik: 5
```



4. **FLOOR()**: Zaokrągla daną liczbę w dół do najbliższej liczby całkowitej.






```sql
   SELECT FLOOR(4.7) AS rounded_down_value; -- Wynik: 4
```



5. **SQRT()**: Zwraca pierwiastek kwadratowy danej liczby.






```sql
   SELECT SQRT(25) AS square_root; -- Wynik: 5
```



6. **EXP()**: Podnosi liczbę e do potęgi danej liczby.






```sql
   SELECT EXP(2) AS exponentiation; -- Wynik: 7.389...
```



7. **LOG()**: Zwraca logarytm naturalny danej liczby.






```sql
   SELECT LOG(10) AS natural_logarithm; -- Wynik: 2.302...
```



8. **POWER()**: Podnosi podaną liczbę do określonej potęgi.






```sql
   SELECT POWER(2, 3) AS result; -- Wynik: 8 (2^3 = 8)
```



9. **SIGN()**: Zwraca znak danej liczby (-1 dla liczby ujemnej, 0 dla zera, 1 dla liczby dodatniej).






```sql
   SELECT SIGN(3240) AS sign_value; -- Wynik: -1
```



Te funkcje matematyczne mogą być używane w zapytaniach SQL do wykonywania różnych operacji na wartościach liczbowych. Ważne jest zrozumienie, że dostępność i składnia tych funkcji mogą się różnić w zależności od konkretnej bazy danych. Warto zajrzeć do dokumentacji swojej bazy danych, aby uzyskać pełen zestaw funkcji matematycznych dostępnych w danym środowisku.
