# Tworzenie bazy danych

Jak już wiemy na pojedyńczym serwerze MS SQL możemy tworzyć dowolną ilość instancji baz danych. Aktualnie mamy jedną instancję, która była przez nas zaimportowana i jest to instancja `AdventureWorksLT2017`. Aby utworzyć nową bazę danych, możemy albo skorzystać z GUI Azure Data Studio, albo zapytań SQL.

### Utworzenie bazy danych za pomocą GUI

1. W Azure Data Studio przejdź do zakładki `Connections` i połącz się z serwerem.
2. Rozwiń drzewko serwera i kliknij prawym przyciskiem myszy na `Databases`.
3. Wybierz opcję `New Database`.
4. Wypełnij pola:
    - `Database name` - nazwa bazy danych
    - `Owner` - właściciel bazy danych (opcjonalnie)
    - `Collation` - ustawienie sortowania i porównywania (opcjonalnie)

### Utworzenie bazy danych za pomocą zapytań SQL

```
CREATE DATABASE NazwaBazyDanych

```

### Przykład

```
CREATE DATABASE Sklep

```

## Usuwanie bazy danych

Aby usunąć bazę danych, możemy skorzystać z GUI Azure Data Studio lub zapytań SQL.

### Usunięcie bazy danych za pomocą GUI

1. W Azure Data Studio przejdź do zakładki `Connections` i połącz się z serwerem.
2. Rozwiń drzewko serwera i kliknij prawym przyciskiem myszy na nazwę bazy danych.
3. Wybierz opcję `Drop`.

### Usunięcie bazy danych za pomocą zapytań SQL

```
DROP DATABASE NazwaBazyDanych

```

### Przykład

```
DROP DATABASE Sklep

```

## Nazwenictwo baz danych

Nazwy baz danych w SQL Serverze mogą składać się z maksymalnie 128 znaków. Nazwa bazy danych nie może zaczynać się od cyfry ani znaku specjalnego. Nazwa bazy danych nie może zawierać znaków specjalnych, takich jak: `/ \ [ ] : ; | = + * ? < >`.

### Konwencje nazewnictwa

Oto lista konwencji nazewnictwa baz danych po polsku, z przykładowymi nazwami po angielsku:

1. **Snake Case**: Słowa są oddzielane podkreślnikami. Na przykład: `my_database`.
2. **Camel Case**: Słowa są pisane bez spacji, z każdym słowem rozpoczynającym się wielką literą, z wyjątkiem pierwszego. Na przykład: `myDatabase`.
3. **Pascal Case**: Podobne do Camel Case, ale pierwsze słowo również zaczyna się od wielkiej litery. Na przykład: `MyDatabase`.
4. **Upper Case**: Wszystkie litery są pisane wielkimi literami. Na przykład: `MY_DATABASE`.
5. **Lower Case**: Wszystkie litery są pisane małymi literami. Na przykład: `my_database`.
6. **Prefiksowanie**: Dodawanie prefiksu, który identyfikuje typ bazy danych. Na przykład: `db_my_database`. Wybierz konwencję, która najlepiej odpowiada Twoim potrzebom i upewnij się, że stosujesz ją konsekwentnie w swoich projektach.
