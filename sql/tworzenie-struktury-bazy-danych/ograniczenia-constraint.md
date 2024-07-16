# Ograniczenia (`Constraint`s)

Ograniczenia w bazie danych Microsoft SQL Server to reguły lub warunki, które można narzucić na dane przechowywane w tabelach, aby zapewnić integralność danych i uniknąć błędów.

Dostępne ograniczenia to:

- `NOT NULL` - wartość nie może być pusta
- `UNIQUE` - wartość musi być unikalna
- `PRIMARY KEY` - wartość musi być unikalna i nie może być pusta (łączy w sobie `UNIQUE` i `NOT NULL`)
- `FOREIGN KEY` - wartość musi istnieć w innej tabeli
- `CHECK` - wartość musi spełniać określone warunki
- `DEFAULT` - wartość domyślna, która zostanie użyta, jeśli nie zostanie podana wartość

### NOT NULL

Ograniczenie `NOT NULL` oznacza, że wartość nie może być pusta. Wartość musi być podana podczas wstawiania nowego rekordu do tabeli.

Aby dodać ograniczenie `NOT NULL` do kolumny, użyj polecenia `ALTER TABLE` z klauzulą `ALTER COLUMN` i `NOT NULL`.

```
ALTER TABLE table_name
ALTER COLUMN column_name datatype NOT NULL;

```

Możemy też dodać ograniczenie `NOT NULL` podczas tworzenia tabeli.

```
CREATE TABLE table_name (
  column1 datatype NOT NULL,
  column2 datatype
);

```

### UNIQUE

Ograniczenie `UNIQUE` oznacza, że wartość musi być unikalna. Wartość nie może się powtarzać w tej kolumnie.

Aby dodać ograniczenie `UNIQUE` do kolumny, użyj polecenia `ALTER TABLE` z klauzulą `ADD CONSTRAINT` i `UNIQUE`.

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column_name);

```

Możemy też dodać ograniczenie `UNIQUE` podczas tworzenia tabeli.

```
CREATE TABLE table_name (
  column1 datatype UNIQUE,
  column2 datatype,
  ...
);

```

### CHECK

Ograniczenie `CHECK` oznacza, że wartość musi spełniać określone warunki. Przykładowo możemy sprawdzić czy wartość jest większa od zera.

Aby dodać ograniczenie `CHECK` do kolumny, użyj polecenia `ALTER TABLE` z klauzulą `ADD CONSTRAINT` i `CHECK`.

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (column_name > 0);

```

Ograniczenie `CHECK` można również wykorzystać z wartościami z pozostałych kolumn, lub nawet z rezultatami funkcji jak np. `GETDATE()`, aby sprawdzić czy data jest większa od dzisiejszej daty.

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (column_name > other_column_name);

```

Przykład z porównywanie dat:

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (column_name > GETDATE());

```

Co więcej, ograniczenie `CHECK` można również wykorzystać do sprawdzenia czy wartość teskstowa ma np. conajmniej `x` znaków.

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (LEN(column_name) >= x);

```

### DEFAULT

Ograniczenie `DEFAULT` oznacza, że wartość domyślna zostanie użyta, jeśli nie zostanie podana wartość. Wartość domyślna zostanie użyta podczas wstawiania nowego rekordu do tabeli.

Aby dodać ograniczenie `DEFAULT` do kolumny, użyj polecenia `ALTER TABLE` z klauzulą `ADD CONSTRAINT` i `DEFAULT`.

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name DEFAULT default_value FOR column_name;

```

Możemy też dodać ograniczenie `DEFAULT` podczas tworzenia tabeli.

```
CREATE TABLE table_name (
  column1 datatype DEFAULT default_value,
  column2 datatype,
  ...
);

```


### PRIMARY KEY

Ograniczenie `PRIMARY KEY` jest kombinacją ograniczeń `NOT NULL` i `UNIQUE`. Oznacza to, że wartość w kolumnie musi być unikalna i nie może być pusta. Kolumna z kluczem głównym może być również używana do identyfikacji rekordów w tabeli.

Aby dodać ograniczenie `PRIMARY KEY` do kolumny, użyj polecenia `ALTER TABLE` z klauzulą `ADD CONSTRAINT` i `PRIMARY KEY`.

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);

```

Możemy też dodać ograniczenie `PRIMARY KEY` podczas tworzenia tabeli.

```
CREATE TABLE table_name (
  column1 datatype PRIMARY KEY
);

```

### FOREIGN KEY

Ograniczenie `FOREIGN KEY` tworzy połączenie między dwoma tabelami. Wartość w kolumnie z kluczem obcym musi istnieć w kolumnie z kluczem głównym w innej tabeli.

Aby dodać ograniczenie `FOREIGN KEY` do kolumny, użyj polecenia `ALTER TABLE` z klauzulą `ADD CONSTRAINT` i `FOREIGN KEY`.

```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name FOREIGN KEY (column_name)
REFERENCES other_table_name (other_column_name);
```
