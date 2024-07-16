# Indeksy 



Indeks w bazie danych MS SQL (Microsoft SQL Server) jest strukturą, która poprawia wydajność operacji wyszukiwania na tabelach. Działa podobnie jak indeks w książce, który pozwala szybko znaleźć stronę zawierającą poszukiwane informacje. Indeksy są kluczowe dla optymalizacji zapytań SQL, szczególnie w przypadku dużych tabel. Poniżej znajdują się główne cechy i rodzaje indeksów w MS SQL:



### Główne cechy indeksów:

1. **Przyspieszanie operacji wyszukiwania**: Indeksy znacząco skracają czas potrzebny na odnalezienie danych, które spełniają określone kryteria.

2. **Wspomaganie operacji sortowania**: Umożliwiają szybsze sortowanie danych.

3. **Unikalność danych**: Indeksy unikalne wymuszają unikalność wartości w kolumnie lub zestawie kolumn.

4. **Zmniejszanie wydajności wstawiania i aktualizacji**: Chociaż indeksy przyspieszają operacje odczytu, mogą spowolnić operacje zapisu, ponieważ każda zmiana danych wymaga także aktualizacji indeksów.



### Rodzaje indeksów w MS SQL:

1. **Indeks klastrowany (Clustered Index)**:

   - Sortuje i przechowuje dane w tabeli według klucza indeksu.

   - Tabela może mieć tylko jeden indeks klastrowany, ponieważ dane w tabeli mogą być posortowane tylko w jeden sposób.

   - Struktura fizyczna tabeli odpowiada strukturze indeksu klastrowanego.



2. **Indeks nieklastrowany (Non-Clustered Index)**:

   - Przechowuje oddzielną strukturę od danych tabeli.

   - Indeks zawiera wskaźniki do rzeczywistych danych w tabeli.

   - Można utworzyć wiele indeksów nieklastrowanych na jednej tabeli.



3. **Indeks unikalny (Unique Index)**:

   - Gwarantuje, że wszystkie wartości w indeksowanej kolumnie są unikalne.

   - Może być klastrowany lub nieklastrowany.



4. **Indeks pełnotekstowy (Full-Text Index)**:

   - Umożliwia szybkie wyszukiwanie tekstu w dużych kolumnach tekstowych.

   - Wspiera zaawansowane zapytania tekstowe, takie jak wyszukiwanie słów w różnych formach gramatycznych.



5. **Indeks przestrzenny (Spatial Index)**:

   - Wspiera szybkie zapytania na danych przestrzennych, takich jak geolokalizacja.

   



### Struktura danych w indeksie



W bazach danych MS SQL dane w indeksach są przechowywane w uporządkowanej strukturze danych, co umożliwia szybki dostęp do rekordów. Istnieją dwa główne typy indeksów: klastrowane i nieklastrowane, a sposób, w jaki przechowują dane, różni się między nimi.



### Indeks klastrowany (Clustered Index)

W przypadku indeksu klastrowanego dane w tabeli są przechowywane fizycznie na dysku w kolejności określonej przez klucz indeksu klastrowanego. Oznacza to, że struktura fizyczna tabeli jest identyczna ze strukturą indeksu klastrowanego. Indeks klastrowany używa struktury drzewa B+ (B-tree), gdzie:



- **Root Node**: Jest to korzeń drzewa, który zawiera informacje umożliwiające znalezienie odpowiedniej strony danych.

- **Intermediate Nodes**: Węzły pośrednie, które prowadzą do liści drzewa.

- **Leaf Nodes**: Liście drzewa, które zawierają rzeczywiste dane tabeli posortowane według klucza indeksu klastrowanego.



### Przykład struktury indeksu klastrowanego

```plaintext

Root

 ├── Intermediate Node

 │   ├── Leaf Node (Data Page)

 │   ├── Leaf Node (Data Page)

 │   ...

 ├── Intermediate Node

 │   ├── Leaf Node (Data Page)

 │   ├── Leaf Node (Data Page)

 │   ...

```



### Indeks nieklastrowany (Non-Clustered Index)

W przypadku indeksu nieklastrowanego dane tabeli nie są sortowane fizycznie. Zamiast tego, indeks nieklastrowany tworzy oddzielną strukturę, która zawiera klucz indeksu i wskaźniki (pointery) do rzeczywistych danych w tabeli. Struktura ta również opiera się na drzewie B+.



- **Root Node**: Zawiera wskaźniki do węzłów pośrednich lub bezpośrednio do liści.

- **Intermediate Nodes**: Węzły pośrednie, które prowadzą do liści drzewa.

- **Leaf Nodes**: Zawierają klucz indeksu i wskaźniki do wierszy danych w tabeli (klucz klastrowany lub RID).



### Przykład struktury indeksu nieklastrowanego

```plaintext

Root

 ├── Intermediate Node

 │   ├── Leaf Node (Key, Pointer)

 │   ├── Leaf Node (Key, Pointer)

 │   ...

 ├── Intermediate Node

 │   ├── Leaf Node (Key, Pointer)

 │   ├── Leaf Node (Key, Pointer)

 │   ...

```



### Przykładowa implementacja indeksu klastrowanego i nieklastrowanego

```sql

-- Tworzenie tabeli
CREATE TABLE dbo.PrzykladowaTabela (
    ID INT PRIMARY KEY,
    Nazwa NVARCHAR(50)
);

-- Tworzenie indeksu klastrowanego (domyślnie tworzony na kluczu podstawowym)
CREATE CLUSTERED INDEX idx_klastrowany ON dbo.PrzykladowaTabela(ID);

-- Tworzenie indeksu nieklastrowanego
CREATE NONCLUSTERED INDEX idx_nieklastrowany ON dbo.PrzykladowaTabela(Nazwa);
```



### Podsumowanie

- **Indeks klastrowany**: Dane są przechowywane fizycznie w kolejności określonej przez klucz indeksu. Indeks klastrowany zmienia fizyczną organizację danych w tabeli.

- **Indeks nieklastrowany**: Dane są przechowywane niezależnie, a indeks przechowuje klucz i wskaźniki do rzeczywistych danych. Struktura ta pozwala na szybki dostęp do danych bez zmiany fizycznej organizacji tabeli.



Oba rodzaje indeksów używają drzewa B+, które umożliwia szybkie wyszukiwanie, wstawianie i usuwanie danych w dobrze zorganizowany sposób.



### Selektywność indeksu



Selektywność indeksu to miara, która określa, jak dobrze dany indeks może zawęzić wyniki zapytania. W skrócie, selektywność mówi nam, ile rekordów z tabeli zostanie wybranych przy użyciu danego indeksu w zapytaniu. Im wyższa selektywność, tym mniej rekordów zostanie przeszukanych, co zazwyczaj przekłada się na lepszą wydajność zapytań.



Formalnie, selektywność jest zdefiniowana jako stosunek liczby unikalnych wartości w kolumnie, do całkowitej liczby rekordów w tej kolumnie. Oznacza to, że im mniejszy stosunek, tym większa selektywność, ponieważ oznacza to, że mniej wartości kolumny powtarza się, co oznacza, że indeks będzie bardziej skuteczny w wyborze odpowiednich rekordów.



Wartość selektywności waha się od 0 do 1. 

- Jeśli wszystkie wartości w kolumnie są unikalne, selektywność wynosi 1.

- Jeśli wszystkie wartości w kolumnie są takie same, selektywność wynosi 0.



### Dlaczego selektywność jest istotna?



Selektywność indeksu ma duże znaczenie dla wydajności zapytań SQL, ponieważ wpływa na to, jak dobrze indeks może redukować liczbę rekordów, które muszą być przeszukane w celu znalezienia odpowiednich wyników. Optymalny indeks powinien być jak najbardziej selektywny, aby jak najbardziej ograniczyć ilość przeszukiwanych danych.



### Przykład:

Rozważmy tabelę zawierającą dane o produktach, a w niej kolumnę `Kategoria`:

- Jeśli kolumna `Kategoria` zawiera tylko kilka unikalnych wartości (np. 5 kategorii wśród 1000 produktów), to indeks na tej kolumnie będzie bardzo selektywny.

- Natomiast jeśli kolumna `Kategoria` zawiera dużo powtarzających się wartości (np. statusy zamówień: "złożone", "w trakcie", "wysłane"), to indeks na tej kolumnie będzie mniej selektywny.



Ważne jest, aby projektując bazę danych i tworząc indeksy, zwrócić uwagę na selektywność, aby maksymalizować wydajność zapytań. Optymalizacja indeksów może obejmować tworzenie indeksów na bardziej selektywnych kolumnach lub łączenie kilku kolumn w jednym indeksie w celu zwiększenia selektywności. Jednak zbyt duża liczba indeksów może prowadzić do nadmiernego zużycia zasobów, dlatego należy znaleźć równowagę pomiędzy selektywnością a liczbą indeksów.









Indeksy są niezbędnym elementem optymalizacji baz danych, pomagając w zwiększaniu wydajności zapytań oraz zapewnianiu integralności danych. Jednak ich nadmiarowe użycie może prowadzić do obniżenia wydajności operacji zapisu, dlatego zawsze warto przeprowadzać analizę i testy wydajności przy projektowaniu i implementacji indeksów.
