# Funkcje `NTILE`

Funkcja okienna NTILE w SQL służy do podziału zbioru wyników na określoną liczbę równych grup. Funkcja ta jest przydatna, gdy chcemy równomiernie rozłożyć wyniki na grupy, czy też sklasyfikować konkretne wiersze pod kątem danej wartości. 

### Składnia

```
NTILE ( liczba_grup ) OVER (PARTITION BY kolumna ORDER BY kolumna)

```

- **liczba\_grup**: Liczba grup, na które chcemy podzielić wyniki.
- **PARTITION BY kolumna**: Opcjonalny parametr, który pozwala podzielić wyniki na grupy w obrębie partycji. Domyślnie cały zbiór wyników jest traktowany jako jedna partycja.
- **ORDER BY kolumna**: Określa porządek, w jakim wyniki są przypisywane do grup.

### Przykład: Podział na 4 grupy według ceny

Załóżmy, że chcemy podzielić produkty na 4 grupy według ceny (`ListPrice`). W tym przypadku użyjemy funkcji NTILE, aby zobaczyć, jak produkty są rozmieszczone w tych grupach.


```sql
SELECT 
    ProductID, 
    Name, 
    ListPrice,
    ProductCategoryID,
    NTILE(4) OVER (ORDER BY ListPrice) AS PriceGroup
FROM 
    SalesLT.Product;
```


Rezultaty będą zawsze zwracane w postaci wartości od 1 do n (w tym przypadku do 4), dzięki czemu, możemy bardzo łatwo przekształcić ten wynik na wartość tesktową, która będzie odpowiadała odpowiedniemu wynikowi. 




```sql
SELECT 
    ProductID, 
    Name, 
    ListPrice,
    ProductCategoryID,
    CASE NTILE(4) OVER (ORDER BY ListPrice)
        WHEN 1 THEN 'Najniższa cena'
        WHEN 2 THEN 'Niska cena'
        WHEN 3 THEN 'Wysoka cena'
        WHEN 4 THEN 'Najwyższa cena'
    END AS PriceGroupDescription
FROM 
    SalesLT.Product;
```



Całość możemy też dodatkowo dzielić na podgrupy poleceniem `PARTITION BY`, tym razem wypisując grupę cenową, dla każdej kategorii produktów z osobna.



```sql
SELECT 
    ProductID, 
    Name, 
    ListPrice,
    ProductCategoryID,
    CASE NTILE(4) OVER (PARTITION BY ProductCategoryID ORDER BY ListPrice)
        WHEN 1 THEN 'Najniższa cena'
        WHEN 2 THEN 'Niska cena'
        WHEN 3 THEN 'Wysoka cena'
        WHEN 4 THEN 'Najwyższa cena'
    END AS PriceGroupDescription
FROM 
    SalesLT.Product;
```


### Zastosowanie

Funkcja NTILE jest używana w różnych scenariuszach, takich jak:



1. **Analiza sprzedaży**: Grupowanie produktów lub zamówień w celu analizy rozkładu cen, ilości, czy dat zamówień.

2. **Marketing**: Segmentacja klientów na grupy według wartości zakupów, częstotliwości zamówień, itp.

3. **Zarządzanie zapasami**: Podział produktów na grupy w celu optymalizacji zarządzania zapasami.



Funkcja NTILE ułatwia analizę danych, szczególnie gdy potrzebujemy równomiernie podzielić wyniki na określoną liczbę grup. Dzięki temu możemy lepiej zrozumieć rozkład danych i podejmować bardziej świadome decyzje biznesowe.
