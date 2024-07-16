# Optymalizacja



Optymalizacja zapytań SQL to proces polegający na zoptymalizowaniu wydajności zapytań SQL poprzez wybór optymalnych planów wykonania. Optymalizacja zapytań jest kluczowym aspektem projektowania baz danych i programowania aplikacji, ponieważ wpływa na wydajność, skalowalność i efektywność systemu bazodanowego. Zanim zobaczymy jak optymalizować zapytania SQL, warto zrozumieć, jak działają zapytania SQL i jak są przetwarzane przez serwer baz danych.



## Jak działają zapytania SQL?



Podczas wykonywania zapytania po stronie serwera MS SQL Server, odbywa się szereg kroków i procesów mających na celu przetworzenie zapytania oraz zwrócenie wyników do klienta. Oto szczegółowy opis tego, co dzieje się po stronie serwera:



1. **Przyjęcie zapytania**:

   - Serwer odbiera zapytanie SQL od klienta (np. aplikacji, narzędzia do zarządzania bazą danych itp.).

   - Zapytanie to jest następnie przekazywane do parsera zapytań.



2. **Parsowanie**:

   - Parser analizuje zapytanie SQL pod kątem składni i semantyki. Upewnia się, że zapytanie jest poprawne syntaktycznie.

   - Podczas tego kroku, parser generuje drzewo parsowania, które reprezentuje strukturę zapytania.



3. **Optymalizacja**:

   - Optymalizator zapytań (Query Optimizer) przetwarza drzewo parsowania w celu wygenerowania optymalnego planu wykonania zapytania.

   - Optymalizator ocenia różne możliwe sposoby wykonania zapytania (np. użycie różnych indeksów, kolejność dołączania tabel, metody sortowania).

   - Wybiera najefektywniejszy plan na podstawie kosztu operacji (ilości wymaganych zasobów takich jak CPU, pamięć, I/O).



4. **Generowanie planu wykonania**:

   - Optymalizator tworzy fizyczny plan wykonania zapytania, który określa dokładne kroki, jakie serwer musi wykonać, aby zrealizować zapytanie.

   - Plan ten jest przechowywany w pamięci podręcznej (plan cache) dla przyszłych zapytań.



5. **Wykonanie**:

   - Silnik bazy danych (Database Engine) przystępuje do wykonania planu.

   - Jeśli zapytanie dotyczy operacji DML (Data Manipulation Language) takich jak SELECT, INSERT, UPDATE czy DELETE, silnik odpowiednio modyfikuje dane lub pobiera wyniki.

   - Wykonanie może obejmować skanowanie tabel, użycie indeksów, sortowanie wyników, łączenie tabel itp.



6. **Dostęp do danych**:

   - Jeśli zapytanie wymaga dostępu do danych, serwer przetwarza strony danych (data pages) z fizycznych plików bazy danych.

   - Bufory danych w pamięci podręcznej (buffer cache) są używane do optymalizacji dostępu do danych.



7. **Zarządzanie transakcjami**:

   - Jeśli zapytanie jest częścią transakcji, SQL Server zarządza transakcjami, zapewniając integralność i spójność danych.

   - Mechanizmy takie jak logi transakcji (transaction logs) są używane do śledzenia zmian w bazie danych.



8. **Zwracanie wyników**:

   - Po wykonaniu zapytania, wyniki są zwracane do klienta.

   - Dane są przesyłane przez warstwę sieciową (np. TCP/IP) do aplikacji, która je zażądała.



9. **Zarządzanie zasobami**:

   - SQL Server monitoruje i zarządza wykorzystaniem zasobów, takich jak CPU, pamięć, I/O, aby zapewnić optymalną wydajność.

   - Mechanizmy takie jak schedulery, kolejki zadań i limity zasobów są używane do zarządzania obciążeniem.



10. **Logowanie i monitorowanie**:

    - SQL Server loguje informacje o wykonaniu zapytań, błędach i innych zdarzeniach w dziennikach systemowych (system logs).

    - Monitorowanie wydajności może być realizowane za pomocą narzędzi takich jak SQL Server Profiler czy Extended Events.



Każdy z tych kroków jest zoptymalizowany, aby zapewnić maksymalną wydajność i spójność danych. Ponadto, SQL Server oferuje szereg mechanizmów zabezpieczeń, takich jak uprawnienia użytkowników, szyfrowanie danych, aby chronić dane i kontrolować dostęp.



## Kolejność przetwarzania zapytań SQL



### Przykładowe zapytanie SQL z wszystkimi klauzulami



```sql
SELECT TOP 3 a.Column1, b.Column2, SUM(a.Column3) AS Total
FROM TableA a
JOIN TableB b ON a.ID = b.AID
WHERE a.Column4 = 'SomeValue'
GROUP BY a.Column1, b.Column2
HAVING SUM(a.Column3) > 100
ORDER BY Total DESC 
```



### Kolejność przetwarzania klauzul w SQL Server



1. **FROM**:

   - Określa, z których tabel pobierane są dane. W tym przypadku zaczyna się od `TableA a`.



2. **JOIN**:

   - Łączy tabele według określonych warunków. Tutaj `TableA a` jest łączona z `TableB b` na podstawie warunku `a.ID = b.AID`.



3. **WHERE**:

   - Filtruje wiersze na podstawie określonego warunku. Tutaj filtruje wiersze z `a.Column4 = 'SomeValue'`.



4. **GROUP BY**:

   - Grupuje wiersze na podstawie jednego lub więcej kolumn. W tym przypadku grupuje na podstawie `a.Column1` i `b.Column2`.



5. **HAVING**:

   - Filtruje grupy utworzone przez klauzulę `GROUP BY` na podstawie warunków agregacyjnych. Tutaj grupy są filtrowane na podstawie warunku `SUM(a.Column3) > 100`.



6. **SELECT**:

   - Określa, które kolumny lub wyrażenia mają być zwrócone. Wybiera `a.Column1`, `b.Column2` i `SUM(a.Column3) AS Total`.



7. **ORDER BY**:

   - Sortuje wynikowy zestaw wierszy na podstawie jednej lub więcej kolumn. W tym przypadku sortuje według `Total` malejąco (`DESC`).



8. **TOP 3**:

   - Służy do ograniczenia wyników. `TOP 3`  pobierze tylko 3 wyniki z posortowanego zestawu.



### Opis procesu



1. **FROM**: Serwer SQL ustala, z których tabel będą pobierane dane (`TableA a`).

2. **JOIN**: Następnie łączy te tabele zgodnie z warunkiem `ON` (`a.ID = b.AID`).

3. **WHERE**: Przetwarza filtr, aby uwzględnić tylko te wiersze, które spełniają warunek `a.Column4 = 'SomeValue'`.

4. **GROUP BY**: Grupuje dane według kolumn `a.Column1` i `b.Column2`.

5. **HAVING**: Przetwarza warunek grupowania, filtrując grupy, które spełniają `SUM(a.Column3) > 100`.

6. **SELECT**: Wybiera określone kolumny i wyrażenia do zwrócenia (`a.Column1`, `b.Column2`, `SUM(a.Column3) AS Total`).

7. **ORDER BY**: Sortuje wynikowy zestaw wierszy według `Total DESC`.

8. **TOP 3**: Ograniczy rezultaty tylko do 3 wyników z posortowanego zestawu.



To pozwala na zrozumienie, jak serwer SQL przetwarza zapytania krok po kroku, aby uzyskać ostateczne wyniki.



## Jak optymalizować zapytania SQL?



Optymalizacja zapytań SQL jest kluczowa dla zapewnienia wysokiej wydajności baz danych. Oto kilka strategii i możliwości, które można wykorzystać do optymalizacji zapytań w MS SQL Server:



1. **Użycie indeksów**:

   - Tworzenie indeksów na kolumnach, które są często używane w klauzulach WHERE, JOIN i ORDER BY.

   - Korzystanie z indeksów pokrywających (covering indexes), które zawierają wszystkie kolumny potrzebne w zapytaniu.



2. **Analiza planów wykonania**:

   - Użycie narzędzia SQL Server Management Studio (SSMS) do analizowania planów wykonania zapytań.

   - Identyfikowanie kosztownych operacji i dostosowywanie zapytań lub struktury bazy danych.



3. **Optymalizacja zapytań**:

   - Redukcja liczby operacji na dużych zbiorach danych.

   - Unikanie złożonych podzapytań i korzystanie z JOIN zamiast podzapytań w klauzuli WHERE.

   - Używanie odpowiednich typów danych i unikanie konwersji typów w zapytaniach.



4. **Używanie hintów**:

   - Stosowanie hintów, takich jak `INDEX`, `JOIN`, `FORCE ORDER`, aby wpływać na sposób wykonania zapytania przez optymalizator.

   - Używanie ich z rozwagą, aby nie ograniczać możliwości optymalizatora.



5. **Zarządzanie statystykami**:

   - Regularne aktualizowanie statystyk dotyczących rozkładu danych w tabelach.

   - Automatyczna aktualizacja statystyk lub ręczne wymuszanie ich aktualizacji za pomocą polecenia `UPDATE STATISTICS`.



6. **Używanie widoków indeksowanych**:

   - Tworzenie widoków indeksowanych dla często używanych złożonych zapytań.

   - Poprawa wydajności poprzez materializowanie wyników zapytań w indeksach.



7. **Optymalizacja operacji JOIN**:

   - Upewnienie się, że kolumny używane w operacjach JOIN są indeksowane.

   - Minimalizacja liczby kolumn wybieranych w zapytaniach.



8. **Zarządzanie blokadami i izolacją transakcji**:

   - Używanie odpowiednich poziomów izolacji transakcji, aby unikać zbędnych blokad i zwiększać współbieżność.

   - Monitorowanie i zarządzanie blokadami za pomocą narzędzi takich jak SQL Server Profiler i Extended Events.



9. **Używanie tymczasowych tabel i zmiennych tabelowych**:

   - Przechowywanie wyników pośrednich w tymczasowych tabelach, aby zredukować złożoność zapytań.

   - Ostrożne korzystanie ze zmiennych tabelowych, które mogą nie zawsze być optymalizowane tak dobrze jak tabele tymczasowe.



10. **Fragmentacja i reorganizacja indeksów**:

    - Regularne monitorowanie i naprawianie fragmentacji indeksów za pomocą poleceń `REBUILD` i `REORGANIZE`.



11. **Podział tabel (partitioning)**:

    - Podział dużych tabel na mniejsze, łatwiejsze do zarządzania partycje, co może znacząco poprawić wydajność operacji na dużych zestawach danych.



Stosując te techniki, można znacznie poprawić wydajność zapytań SQL i ogólną efektywność działania bazy danych MS SQL Server.





## Jak podejść do optymalizacji



### 1. Nie ma złotego środka



Każda baza danych i zapytanie są inne, dlatego nie ma uniwersalnego rozwiązania, które sprawdzi się w każdej sytuacji. Optymalizacja wymaga dostosowania strategii do specyficznych potrzeb i warunków danego systemu. Wymaga to zrozumienia kontekstu, w jakim działają zapytania, oraz dostosowania metod optymalizacji do unikalnych wyzwań związanych z danymi i obciążeniem.



### 2. Technika prób i błędów



Optymalizacja zapytań SQL często wymaga eksperymentowania z różnymi podejściami, aby znaleźć najbardziej efektywne rozwiązanie. Próbując różnych strategii, takich jak dodawanie indeksów, modyfikacja zapytań czy zmiana konfiguracji serwera, można zidentyfikować te, które przynoszą najlepsze rezultaty. Ważne jest, aby systematycznie testować każdą zmianę i monitorować jej wpływ na wydajność.



### 3. Zrozum dane i zapytanie



Pełne zrozumienie struktury danych i specyfiki zapytań jest kluczowe dla efektywnej optymalizacji. Zrozumienie, jak dane są przechowywane, jakie są ich relacje, oraz jak zapytania je przetwarzają, pozwala na bardziej świadome podejmowanie decyzji optymalizacyjnych. Analizując schemat bazy danych oraz wzorce zapytań, można zidentyfikować potencjalne problemy i optymalizować zapytania bardziej precyzyjnie.



### 4. Monitorowanie i profilowanie



Stale monitorowanie wydajności zapytań oraz używanie narzędzi do profilowania jest niezbędne, aby identyfikować i diagnozować problemy z wydajnością. Narzędzia takie jak SQL Server Profiler czy Extended Events pozwalają na zbieranie szczegółowych informacji o wykonywaniu zapytań, co umożliwia wykrywanie wąskich gardeł i obszarów wymagających optymalizacji. Regularne monitorowanie pomaga również w szybkim reagowaniu na zmieniające się warunki pracy bazy danych.



### 5. Testuj na realistycznych danych



Optymalizacja i testowanie zapytań powinny być przeprowadzane na danych, które realistycznie odzwierciedlają rzeczywiste obciążenie i rozmiar bazy danych. Testowanie na małych, sztucznych zbiorach danych może prowadzić do fałszywych wniosków i nieefektywnych optymalizacji. Używanie danych produkcyjnych lub ich reprezentatywnych kopii pozwala na dokładniejszą ocenę wpływu zmian i bardziej trafne decyzje optymalizacyjne.





## Metryki wydajności zapytań SQL



Metryki pomiaru wydajności zapytań SQL pomagają zrozumieć, jak efektywnie zapytania wykorzystują zasoby systemowe oraz jak szybko przetwarzają dane. Oto kluczowe metryki, które warto monitorować:



### 1. **Czas wykonania (Execution Time)**



- **Całkowity czas wykonania (Total Execution Time)**: Łączny czas od momentu rozpoczęcia do zakończenia wykonania zapytania.

- **Czas CPU (CPU Time)**: Czas procesora zużyty na wykonanie zapytania.



### 2. **Ilość operacji wejścia/wyjścia (I/O Operations)**



- **Liczba odczytów logicznych (Logical Reads)**: Ilość stron danych odczytanych z pamięci podręcznej.

- **Liczba odczytów fizycznych (Physical Reads)**: Ilość stron danych odczytanych z dysku, gdy nie były dostępne w pamięci podręcznej.

- **Liczba zapisów logicznych (Logical Writes)**: Ilość stron danych zapisanych do pamięci podręcznej.

- **Liczba zapisów fizycznych (Physical Writes)**: Ilość stron danych zapisanych na dysk.



### 3. **Koszt zapytania (Query Cost)**



- **Szacowany koszt zapytania (Estimated Query Cost)**: Wartość oszacowana przez optymalizator SQL Server, która reprezentuje względny koszt wykonania zapytania.

- **Rzeczywisty koszt zapytania (Actual Query Cost)**: Faktyczny koszt wykonania zapytania po jego zakończeniu.



### 4. **Wykorzystanie pamięci (Memory Usage)**



- **Pamięć zużyta na wykonanie zapytania (Query Memory Usage)**: Ilość pamięci zużytej podczas wykonania zapytania.

- **Wykorzystanie pamięci podręcznej (Cache Usage)**: Jak efektywnie zapytanie korzysta z pamięci podręcznej danych i planów wykonania.



### 5. **Liczba wierszy (Row Counts)**



- **Liczba przetworzonych wierszy (Rows Processed)**: Ilość wierszy przetworzonych przez zapytanie.

- **Liczba zwróconych wierszy (Rows Returned)**: Ilość wierszy zwróconych przez zapytanie.


