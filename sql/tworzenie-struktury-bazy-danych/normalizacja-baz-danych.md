# Normalizacja baz danych

**Normalizacja** to proces organizowania danych w bazie danych. Obejmuje on tworzenie tabel i ustanawianie relacji między nimi zgodnie z regułami, które mają na celu ochronę danych i zwiększenie elastyczności bazy danych poprzez eliminowanie nadmiarowości oraz niespójnych zależności. Nadmiarowe dane zajmują dodatkowe miejsce na dysku i przyczyniają się do problemów z utrzymywaniem spójności. Gdy trzeba zmienić dane istniejące w więcej niż jednym miejscu, wszystkie te lokalizacje muszą być zmienione w ten sam sposób. Na przykład zmiana adresu klienta jest łatwiejsza, jeśli te dane są przechowywane tylko w tabeli **Customers** i nigdzie indziej w bazie danych. Niespójne zależności oznaczają, że dane są zależne od nieodpowiednich informacji. Na przykład, podczas gdy adres klienta powinien znajdować się w tabeli **Customers**, wynagrodzenie pracownika obsługującego tego klienta powinno znajdować się w tabeli **Employees**, ponieważ jest zależne od pracownika.

### Reguły normalizacji

Istnieje kilka reguł normalizacji bazy danych, każda nazywana "formą normalną". Pierwsza reguła to **pierwsza normalna forma** (1NF), a jeśli baza danych spełnia pierwsze trzy reguły, jest uważana za znormalizowaną w **trzeciej normalnej formie** (3NF). Choć istnieją inne poziomy normalizacji, trzecia normalna forma jest zazwyczaj wystarczająca dla większości aplikacji. W praktyce, normalizacja wymaga często dodatkowych tabel, co może być postrzegane jako niewygodne. Decydując się na naruszenie jednej z trzech pierwszych reguł, należy przewidzieć potencjalne problemy, takie jak nadmiarowe dane i niespójne zależności.

### Pierwsza postać normalna (1NF)

- Wyeliminuj powtarzające się grupy w poszczególnych tabelach.
- Utwórz osobną tabelę dla każdego zestawu powiązanych danych.
- Zidentyfikuj każdy zestaw powiązanych danych za pomocą klucza głównego. Nie należy używać wielu pól w jednej tabeli do przechowywania podobnych danych. Na przykład, aby śledzić pozycję magazynową z różnych źródeł, najlepiej umieścić informacje o dostawcach w osobnej tabeli **Dostawcy** i połączyć ją z magazynem za pomocą klucza.

### Druga postać normalna (2NF)

- Utwórz osobne tabele dla zestawów wartości dotyczących wielu rekordów.
- Powiąż te tabele za pomocą klucza obcego. Rekordy nie powinny zależeć od niczego innego niż klucz główny tabeli. Na przykład adres klienta powinien być przechowywany tylko w tabeli **Klienci** lub w osobnej tabeli **Adresy**, a nie powtarzać się w innych tabelach jak **Zamówienia** czy **Faktury**.

### Trzecia postać normalna (3NF)

- Eliminuj pola, które nie zależą od klucza. Wartości w wierszu, które nie są częścią klucza, nie powinny znajdować się w tej tabeli. Na przykład informacje o uniwersytetach powinny być przechowywane w osobnej tabeli **Uniwersytety**, a nie w tabeli **Kandydaci**.

### Wyjątki

Choć przestrzeganie trzeciej normalnej formy jest teoretycznie pożądane, nie zawsze jest praktyczne. Zbyt wiele małych tabel może pogorszyć wydajność lub spowodować inne problemy. Dlatego warto stosować trzecią postać normalną do danych często zmienianych i projektować aplikacje tak, aby weryfikowały powiązane pola po zmianie jednego z nich.

### Normalizowanie przykładowej tabeli

#### Tabela nieznormalizowana:

| Nr studenta | Opiekun | Pokój opiekuna | Zajęcia 1 | Zajęcia 2 | Zajęcia 3 |
| --- | --- | --- | --- | --- | --- |
| 1022 | Czarnecki | 412 | 101-07 | 143-01 | 159-02 |
| 4123 | Borkowski | 216 | 101-07 | 143-01 | 179-04 |

#### Pierwsza normalna forma (1NF)

Tabela powinna mieć tylko dwa wymiary. Powtarzające się grupy zajęć należy przenieść do osobnej tabeli:

| Nr studenta | Opiekun | Pokój opiekuna | Nr zajęć |
| --- | --- | --- | --- |
| 1022 | Czarnecki | 412 | 101-07 |
| 1022 | Czarnecki | 412 | 143-01 |
| 1022 | Czarnecki | 412 | 159-02 |
| 4123 | Borkowski | 216 | 101-07 |
| 4123 | Borkowski | 216 | 143-01 |
| 4123 | Borkowski | 216 | 179-04 |

#### Druga normalna forma (2NF)

Eliminujemy nadmiarowe dane poprzez podział tabeli: **Studenci:**

| Nr studenta | Opiekun | Pokój opiekuna |
| --- | --- | --- |
| 1022 | Czarnecki | 412 |
| 4123 | Borkowski | 216 |
| **Rejestracja:** |  |  |
| Nr studenta | Nr zajęć |  |
| --- | --- |  |
| 1022 | 101-07 |  |
| 1022 | 143-01 |  |
| 1022 | 159-02 |  |
| 4123 | 101-07 |  |
| 4123 | 143-01 |  |
| 4123 | 179-04 |  |

#### Trzecia normalna forma (3NF)

Eliminujemy dane zależne od klucza. Przenosimy atrybut **Pokój opiekuna** do osobnej tabeli: **Studenci:**

| Nr studenta | Opiekun |
| --- | --- |
| 1022 | Czarnecki |
| 4123 | Borkowski |
| **Wykładowcy:** |  |
| Nazwa | Pokój |
| Czarnecki | 412 |
| Borkowski | 216 |
