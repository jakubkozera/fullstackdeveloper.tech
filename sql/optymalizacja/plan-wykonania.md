# Plan wykonania

Plan wykonania w MS SQL (Execution Plan) to szczegółowa analiza, jak silnik bazy danych SQL Server wykonuje zapytanie SQL. Jest to zestaw kroków, które SQL Server podejmuje, aby uzyskać dane z bazy danych. Plan wykonania może pomóc zrozumieć, dlaczego dane zapytanie działa szybko lub wolno, oraz zidentyfikować potencjalne problemy z wydajnością.

Istnieją dwa typy planów wykonania w MS SQL:

1. **Plan szacowany (Estimated Execution Plan)**: Jest to przewidywany plan, który SQL Server generuje bez faktycznego wykonania zapytania. Może być używany do analizy zapytań i identyfikacji potencjalnych problemów bez wpływu na wydajność systemu.
    
2. **Plan rzeczywisty (Actual Execution Plan)**: Jest to rzeczywisty plan wykonania, który jest generowany po faktycznym wykonaniu zapytania. Zawiera on dokładne informacje o rzeczywistych zasobach użytych do wykonania zapytania.
    

## Jak uzyskać plan wykonania?

### SQL Server Management studio

#### Plan szacowany

W SQL Server Management Studio (SSMS):

1. Otwórz nowe zapytanie.
2. Wpisz zapytanie SQL.
3. Kliknij przycisk "Display Estimated Execution Plan" (ikona z grafiką planu wykonania) na pasku narzędzi, lub użyj skrótu klawiszowego `Ctrl + L`.

#### Plan rzeczywisty

W SQL Server Management Studio (SSMS):

1. Otwórz nowe zapytanie.
2. Wpisz zapytanie SQL.
3. Kliknij przycisk "Include Actual Execution Plan" (ikona z grafiką planu wykonania z zaznaczonym "Include") na pasku narzędzi, lub użyj skrótu klawiszowego `Ctrl + M`.
4. Wykonaj zapytanie.

### Azure Data studio

W Azure Data Studio możesz uzyskać plan wykonania dla zapytania SQL podobnie jak w SQL Server Management Studio (SSMS). Oto kroki, jak to zrobić:

### Uzyskiwanie planu szacowanego (Estimated Execution Plan)

1. **Otwórz Azure Data Studio**: Uruchom Azure Data Studio na swoim komputerze.
2. **Połącz się z bazą danych**: Połącz się z serwerem SQL i wybierz odpowiednią bazę danych.
3. **Otwórz nowe zapytanie**: Kliknij ikonę „New Query” lub użyj skrótu `Ctrl + N` (Windows/Linux) lub `Cmd + N` (Mac), aby otworzyć nowe okno zapytania.
4. **Wpisz zapytanie SQL**: Wprowadź zapytanie SQL, dla którego chcesz uzyskać plan wykonania.
5. **Wyświetl szacowany plan wykonania**: Kliknij ikonę „Explain” na pasku narzędzi (przycisk z ikoną planu wykonania) lub użyj skrótu `Ctrl + L` (Windows/Linux) lub `Cmd + L` (Mac). Azure Data Studio wygeneruje szacowany plan wykonania i wyświetli go w dolnej części okna.

### Uzyskiwanie rzeczywistego planu wykonania (Actual Execution Plan)

1. **Otwórz Azure Data Studio**: Uruchom Azure Data Studio na swoim komputerze.
2. **Połącz się z bazą danych**: Połącz się z serwerem SQL i wybierz odpowiednią bazę danych.
3. **Otwórz nowe zapytanie**: Kliknij ikonę „New Query” lub użyj skrótu `Ctrl + N` (Windows/Linux) lub `Cmd + N` (Mac), aby otworzyć nowe okno zapytania.
4. **Wpisz zapytanie SQL**: Wprowadź zapytanie SQL, dla którego chcesz uzyskać plan wykonania.
5. **Włącz rzeczywisty plan wykonania**: Przed wykonaniem zapytania, włącz rzeczywisty plan wykonania. Można to zrobić, klikając ikonę „Include Actual Execution Plan” na pasku narzędzi lub używając skrótu `Ctrl + M` (Windows/Linux) lub `Cmd + M` (Mac).
6. **Wykonaj zapytanie**: Wykonaj zapytanie, klikając przycisk „Run” (przycisk z ikoną play) lub używając skrótu `F5`. Po wykonaniu zapytania rzeczywisty plan wykonania zostanie wyświetlony w dolnej części okna.

### Analiza planu wykonania

Po uzyskaniu planu wykonania w Azure Data Studio, możesz przeanalizować różne operatory i ich metadane, takie jak:

- **Koszt operatora (Cost)**: Informuje, jaką część całkowitego kosztu zapytania stanowi dany operator.
- **Szacowana liczba wierszy (Estimated Rows)**: Liczba wierszy, które operator szacuje, że przetworzy.
- **Rzeczywista liczba wierszy (Actual Rows)**: Rzeczywista liczba wierszy przetworzonych przez operatora.
- **Szacowany koszt I/O (Estimated I/O Cost)**: Koszt operacji wejścia/wyjścia.
- **Szacowany koszt CPU (Estimated CPU Cost)**: Koszt operacji procesora.

Plan wykonania w Azure Data Studio jest prezentowany graficznie, podobnie jak w SSMS, co ułatwia zrozumienie przepływu danych i identyfikację potencjalnych problemów z wydajnością zapytania.

### Analiza planu wykonania

Plan wykonania przedstawia różne operatory i ich kolejność wykonywania. Każdy operator ma swoje własne koszty związane z CPU i operacjami we/wy, co pomaga zrozumieć, gdzie mogą występować wąskie gardła. Typowe operatory to:

- **Table Scan**: Skanowanie całej tabeli.
- **Index Scan**: Skanowanie indeksu.
- **Index Seek**: Wyszukiwanie przy użyciu indeksu.
- **Nested Loops, Merge Join, Hash Join**: Różne metody łączenia tabel.

Analiza planu wykonania może pomóc zidentyfikować, które operacje są kosztowne i mogą wymagać optymalizacji. Można również zobaczyć, czy indeksy są wykorzystywane prawidłowo i czy zapytanie jest zoptymalizowane.

W SQL Server (i generalnie w większości systemów baz danych) niektóre operacje są zazwyczaj bardziej kosztowne niż inne. Oto lista operacji, które często generują najwyższe koszty:

### 1\. **Table Scan (Skanowanie tabeli)**

- **Opis**: Przeszukiwanie całej tabeli bez użycia indeksów.
- **Koszt**: Bardzo wysoki, zwłaszcza w przypadku dużych tabel, ponieważ każda wiersz w tabeli musi zostać odczytany.

### 2\. **Index Scan (Skanowanie indeksu)**

- **Opis**: Przeszukiwanie całego indeksu. Jest mniej kosztowne niż skanowanie tabeli, ale wciąż może być zasobochłonne w przypadku dużych indeksów.
- **Koszt**: Wysoki, jeśli indeks jest duży i nie jest wystarczająco selektywny.

### 3\. **Sort (Sortowanie)**

- **Opis**: Sortowanie danych w pamięci lub na dysku, gdy dane nie są już posortowane.
- **Koszt**: Wysoki, zwłaszcza gdy sortowanie musi odbywać się na dużych zestawach danych i nie może być przeprowadzone w pamięci (tzw. sortowanie na dysku).

### 4\. **Hash Match (Mieszanie haszujące)**

- **Opis**: Używane do wykonywania operacji łączenia, agregacji i unii, gdy inne metody łączenia (np. Nested Loops, Merge Join) nie są możliwe lub wydajne.
- **Koszt**: Może być wysoki, szczególnie gdy tabele są duże i mieszanie wymaga dużej ilości pamięci.

### 5\. **Nested Loops (Zagnieżdżone pętle)**

- **Opis**: Łączenie tabel poprzez iterowanie przez jedną tabelę i dla każdej jej wartości przeszukiwanie drugiej tabeli.
- **Koszt**: Może być bardzo wysoki w przypadku dużych tabel, ponieważ dla każdego wiersza w jednej tabeli druga tabela jest przeszukiwana.

### Jak minimalizować koszty operacji?

1. **Indeksowanie**: Używaj odpowiednich indeksów, aby zminimalizować skanowania tabel i indeksów. Indeksy klastrowane i nieklastrowane mogą znacząco poprawić wydajność.
2. **Filtrowanie**: Używaj filtrów w zapytaniach, aby zmniejszyć liczbę przetwarzanych wierszy.
3. **Optymalizacja zapytań**: Analizuj plany wykonania i optymalizuj zapytania, aby unikać kosztownych operacji. Używaj technik takich jak podzapytań, partycjonowania danych, itp.
4. **Aktualizowanie statystyk**: Upewnij się, że statystyki są aktualne, aby optymalizator zapytań mógł generować bardziej wydajne plany wykonania.
5. **Analiza planu wykonania**: Regularnie analizuj plany wykonania i monitoruj wydajność zapytań, aby identyfikować i eliminować wąskie gardła.

Po próbie optymalizacji zapytania, warto ponownie sprawdzić plan wykonania, aby upewnić się, że zmiany przyniosły oczekiwane rezultaty i nie spowodowały nowych problemów wydajnościowych.

### Przykład porównania zapytań z `GROUP BY` i funkcją okna

Załóżmy, że mamy dwa zapytania, które zwracają ten sam rezultat:

Zapytanie 1, z użyciem `GROUP BY`:

```
SELECT c.SalesPerson, pc.Name [CategoryName], SUM(soh.TotalDue) as TotalSales
FROM SalesLT.Customer c 
JOIN SalesLT.SalesOrderHeader soh on soh.CustomerID = c.CustomerID
JOIN SalesLT.SalesOrderDetail sod on sod.SalesOrderID = soh.SalesOrderID
JOIN SalesLT.Product p on p.ProductID = sod.ProductID
JOIN SalesLT.ProductCategory pc on pc.ProductCategoryID = p.ProductCategoryID
GROUP BY c.SalesPerson, pc.Name

```

Zapytanie 2, z użyciem funkcji okna:

```
SELECT DISTINCT 
    c.SalesPerson,
    pc.Name AS CategoryName,
    SUM(soh.TotalDue) OVER (PARTITION BY c.SalesPerson, pc.Name) AS TotalSales
FROM SalesLT.Customer c 
JOIN SalesLT.SalesOrderHeader soh ON soh.CustomerID = c.CustomerID
JOIN SalesLT.SalesOrderDetail sod ON sod.SalesOrderID = soh.SalesOrderID
JOIN SalesLT.Product p ON p.ProductID = sod.ProductID
JOIN SalesLT.ProductCategory pc ON pc.ProductCategoryID = p.ProductCategoryID
ORDER BY CategoryName 

```
