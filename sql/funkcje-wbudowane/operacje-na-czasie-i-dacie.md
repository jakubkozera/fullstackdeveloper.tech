# Operacje na dacie i czasie





Operacje na czasie i dacie w Microsoft SQL Server obejmują szeroki zakres funkcji i operacji, które umożliwiają manipulację i analizę danych czasowych oraz datowych. Między innymi posłużą one do wykonywania operacji takich jak dodawanie, odejmowanie, porównywanie, formatowanie, konwersja, ekstrakcja i inne.





1. `GETDATE()` - zwraca bieżącą datę i czas








```sql
SELECT GETDATE();
```

2. `DATEADD`: Ta funkcja dodaje określoną liczbę jednostek (dni, miesięcy, lat itp.) do określonej daty.


```sql
SELECT DATEADD(day, 7, GETDATE()); -- Dodaje 7 dni do bieżącej daty
```

W funkcji `DATEADD` możemy też podać wartość ujemną, co pozwala na odjęcie od daty. Wartość ujemna oznacza, że odejmujemy od daty, a wartość dodatnia, że dodajemy do daty.



Przykładowo, aby sprawdzić jaka była data 7 dni temu, możemy użyć:




```sql
SELECT DATEADD(MONTH, 7, GETDATE()) -- odejmuje 7 dni od bieżącej daty
```

Jednostki, które możemy wybrać to:

- `year` (rok)

- `quarter` (kwartał)

- `month` (miesiąc)

- `day` (dzień)

- `week` (tydzień)

- `weekday` (dzień tygodnia, od 1 do 7, gdzie 1 to niedziela i 7 to sobota)

- `hour` (godzina)

- `minute` (minuta)

- `second` (sekunda)

- `millisecond` (milisekunda)

- `microsecond` (mikrosekunda)

- `nanosecond` (nanosekunda)

3. `DATEDIFF`: Pozwala na obliczenie różnicy między dwiema datami w określonych jednostkach (dni, miesiące, lata itp.).


```sql
SELECT DATEDIFF(DAY, '2024-04-14', '2024-04-24'); -- Oblicza różnicę w dniach między dwiema datami
```

4. `DATEPART`: Pozwala na pobranie określonej części daty lub czasu, na przykład dzień, miesiąc, rok itp.


```sql
SELECT DATEPART(DAY, GETDATE()); -- Pobiera bieżący rok
```

Oprócz samej funkcji `DATEPART`, możemy też skorzystać z konkretnych funkcji, takich jak `YEAR()`, `MONTH()`, `DAY()`, które zwracają odpowiednio rok, miesiąc i dzień z daty. 


```sql
SELECT  YEAR(GETDATE()) [Year], 
        MONTH(GETDATE()) [Month], 
        DAY(GETDATE()) [Day]
```

5. `CONVERT`: Funkcja ta konwertuje wartości jednego typu danych na inne, na przykład z daty na ciąg znaków.


```sql
SELECT CONVERT(varchar, GETDATE(), 120); -- Konwertuje bieżącą datę na ciąg znaków w formacie mm/dd/rrrr
```



W przypadku zapytania SQL `CONVERT(varchar, GETDATE(), 101)`, liczba `101` jest kodem formatu daty używanym w funkcji `CONVERT`. Określa on, w jaki sposób data ma zostać sformatowana w postaci ciągu znaków.



W przypadku kodu `101`, oznacza to format daty w stylu amerykańskim: MM/dd/yyyy, gdzie:



- MM oznacza miesiąc w postaci dwucyfrowej,

- dd oznacza dzień w postaci dwucyfrowej,

- yyyy oznacza rok w postaci czterocyfrowej.



Kilka innych popularnych kodów formatu daty, które można użyć w funkcji `CONVERT` w SQL Server:



- 101 - Styl amerykański: MM/dd/yyyy

- 103 - Styl brytyjski: dd/MM/yyyy

- 110 - Format amerykański z myślnikami: MM-dd-yyyy

- 112 - Format liczbowy: yyyyMMdd

- 120 - Format liczbowy z myślnikami: yyyy-MM-dd

- 126 - ISO 8601 (zarezerwowane dla typu danych czasowych): yyyy-MM-ddThh:mm:ss.mmm

6. `FORMAT`: Jest to funkcja, która umożliwia formatowanie dat i czasów zgodnie z określonym wzorcem.


```sql
SELECT FORMAT(GETDATE(), 'yyyy-MM-dd HH:mm'); -- Formatuje bieżącą datę i czas według określonego wzorca
```

Format `'yyyy-MM-dd HH:mm:ss'` oznacza następujące wartości:

- `yyyy`: Rok, wyrażony jako czterocyfrowy.
- `MM`: Miesiąc, wyrażony jako dwucyfrowy (z wiodącym zerem, jeśli jest to konieczne).
- `dd`: Dzień miesiąca, wyrażony jako dwucyfrowy (z wiodącym zerem, jeśli jest to konieczne).
- `HH`: Godzina, wyrażona jako dwucyfrowa w formacie 24-godzinnym (z wiodącym zerem, jeśli jest to konieczne).
- `mm`: Minuta, wyrażona jako dwucyfrowa (z wiodącym zerem, jeśli jest to konieczne).
- `ss`: Sekunda, wyrażona jako dwucyfrowa (z wiodącym zerem, jeśli jest to konieczne).

## Zadanie



1. Obliczanie opóźnienia dostawy zamówienia, róźnica między datą zamówienia `OrderDate` a datą dostawy `ShipDate` w dniach, z tabeli `SalesLT.SalesOrderHeader`


```sql
-- ROZWIĄZANIE

SELECT SalesOrderID, OrderDate, ShipDate, DATEDIFF(DAY, OrderDate, ShipDate) as DeliveryDelaysInDays
FROM SalesLT.SalesOrderHeader
```

2. Napisz zapytanie, które zwróci zamówienia z czerwca 2008 roku (`OrderDate`)


```sql
-- ROZWIĄZANIE

SELECT *
FROM SalesLT.SalesOrderHeader
WHERE YEAR(OrderDate) = 2008 AND MONTH(OrderDate) = 6
```

3. Napisz zapytanie, które zwróci nazwę zamówienia w formacie:

`<SalesOrderNumber>-<OrderDate:yyyyMMdd>`


```sql
-- ROZWIĄZANIE

SELECT SalesOrderNumber, OrderDate, CONCAT(SalesOrderNumber, '-', CONVERT(varchar, OrderDate, 112))
FROM SalesLT.SalesOrderHeader
SELECT SalesOrderNumber, OrderDate, SalesOrderNumber + '-' + FORMAT(OrderDate, 'yyyyMMdd')
FROM SalesLT.SalesOrderHeader
```
