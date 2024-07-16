# Kaskadowe usuwanie

Jak już się przekonaliśmy, aby usunąc wiersze z tabeli, które są powiązane kluczem obcym wierszami z innej tabeli, musimy najpierw usunąć te powiązane wiersze. W przypadku, gdy te powiązane wiersze również mają powiązania z innymi wierszami, musimy usunąć te wiersze, aż dojedziemy do wierszy, które nie mają powiązań z innymi wierszami.
W takim przypadku w MS SQL możemy skorzystać z kaskadowego usuwania. Kaskadowe usuwanie to mechanizm, który automatycznie usuwa powiązane wiersze z innych tabel, gdy usuwamy wiersz z danej tabeli.
## Kaskodowe zachowania
W MS SQL możemy zdefiniować następujące kaskadowe zachowania:
- `CASCADE`: Usuwa powiązane wiersze z innych tabel.
- `SET NULL`: Ustawia wartość klucza obcego na `NULL`, gdy wiersz z danej tabeli zostanie usunięty.
- `SET DEFAULT`: Ustawia wartość klucza obcego na wartość domyślną, gdy wiersz z danej tabeli zostanie usunięty.
- `NO ACTION`: Uniemożliwia usunięcie wiersza z danej tabeli, jeżeli istnieją powiązane wiersze w innych tabelach. (Domyślnie ustawione)
## Przykład `CASCADE`
W poniższym przykładzie mamy dwie tabele: `Orders` i `OrderDetails`. Tabela `OrderDetails` zawiera klucz obcy `OrderID`, który odnosi się do klucza głównego `OrderID` w tabeli `Orders`.
```
CREATE TABLE Orders
(
    OrderID int PRIMARY KEY,
    OrderNumber nvarchar(10),
    OrderDate datetime,
    CustomerID int
);
CREATE TABLE OrderDetails
(
    DetailID int PRIMARY KEY,
    OrderID int,
    ProductID int,
    Quantity int,
    Price decimal(18,2),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) ON DELETE CASCADE
);
```
Po dodaniu jakiś przykładowych danych do tych tabel:
```
INSERT INTO Orders (OrderID, OrderNumber, OrderDate, CustomerID) VALUES (1, 'ORD001', '2020-01-01', 1);
INSERT INTO OrderDetails (DetailID, OrderID, ProductID, Quantity, Price) VALUES (1, 1, 1, 10, 100);
INSERT INTO OrderDetails (DetailID, OrderID, ProductID, Quantity, Price) VALUES (2, 1, 2, 20, 200);
```
Jeżeli teraz spróbujemy usunąć wiersz z tabeli `Orders`, to wiersze z tabeli `OrderDetails` również zostaną usunięte:
```
DELETE FROM Orders WHERE OrderID = 1;
```
Po wykonaniu powyższego zapytania, wiersze z tabeli `OrderDetails` również zostaną usunięte.
## Przykład `SET NULL`
W poniższym przykładzie mamy dwie tabele: `Orders` i `OrderDetails`. Tabela `OrderDetails` zawiera klucz obcy `OrderID`, który odnosi się do klucza głównego `OrderID` w tabeli `Orders`.
```
CREATE TABLE Orders
(
    OrderID int PRIMARY KEY,
    OrderNumber nvarchar(10),
    OrderDate datetime,
    CustomerID int
);
CREATE TABLE OrderDetails
(
    DetailID int PRIMARY KEY,
    OrderID int,
    ProductID int,
    Quantity int,
    Price decimal(18,2),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) ON DELETE SET NULL
);
```
Po dodaniu jakiś przykładowych danych do tych tabel:
```
INSERT INTO Orders (OrderID, OrderNumber, OrderDate, CustomerID) VALUES (1, 'ORD001', '2020-01-01', 1);
INSERT INTO OrderDetails (DetailID, OrderID, ProductID, Quantity, Price) VALUES (1, 1, 1, 10, 100);
INSERT INTO OrderDetails (DetailID, OrderID, ProductID, Quantity, Price) VALUES (2, 1, 2, 20, 200);
```
Jeżeli teraz spróbujemy usunąć wiersz z tabeli `Orders`, to wartość klucza obcego `OrderID` w tabeli `OrderDetails` zostanie ustawiona na `NULL`:
```
DELETE FROM Orders WHERE OrderID = 1;
```
Po wykonaniu powyższego zapytania, wartość klucza obcego `OrderID` w wierszach z tabeli `OrderDetails` zostanie ustawiona na `NULL`.
## Przykład `SET DEFAULT`
W poniższym przykładzie mamy dwie tabele: `Orders` i `OrderDetails`. Tabela `OrderDetails` zawiera klucz obcy `OrderID`, który odnosi się do klucza głównego `OrderID` w tabeli `Orders`.
```
CREATE TABLE Orders
(
    OrderID int PRIMARY KEY,
    OrderNumber nvarchar(10),
    OrderDate datetime,
    CustomerID int
);
CREATE TABLE OrderDetails
(
    DetailID int PRIMARY KEY,
    OrderID int,
    ProductID int,
    Quantity int,
    Price decimal(18,2),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) ON DELETE SET DEFAULT
);
ALTER TABLE OrderDetails ADD CONSTRAINT DF_Orders_OrderID DEFAULT 1 FOR OrderID;
```
Po dodaniu jakiś przykładowych danych do tych tabel:
```
INSERT INTO Orders (OrderID, OrderNumber, OrderDate, CustomerID) VALUES (1, 'ORD001', '2020-01-01', 1);
INSERT INTO Orders (OrderID, OrderNumber, OrderDate, CustomerID) VALUES (2, 'ORD002', '2020-01-02', 2);
INSERT INTO OrderDetails (DetailID, OrderID, ProductID, Quantity, Price) VALUES (1, 2, 1, 10, 100);
INSERT INTO OrderDetails (DetailID, OrderID, ProductID, Quantity, Price) VALUES (2, 2, 2, 20, 200);
SELECT * FROM Orders
SELECT * FROM OrderDetails
```
Jeżeli teraz spróbujemy usunąć wiersz z tabeli `Orders`, to wartość klucza obcego `OrderID` w tabeli `OrderDetails` zostanie ustawiona na wartość domyślną:
```
DELETE FROM Orders WHERE OrderID = 2;
SELECT * FROM Orders
SELECT * FROM OrderDetails
```
Po wykonaniu powyższego zapytania, wartość klucza obcego `OrderID` w wierszach z tabeli `OrderDetails` zostanie ustawiona na wartość domyślną.
### Dodanie opcji kaskadowego usuwania do istniejącej tabeli
Aby dodać opcję kaskadowego usuwania (lub inną) do istniejącej tabeli, możemy użyć polecenia ALTER TABLE z klauzulą FOREIGN KEY.
```
ALTER TABLE OrderDetails ADD FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) ON DELETE CASCADE;
```
**Zalety kaskadowego usuwania:**
- **Utrzymanie integralności danych:** Zapewnia, że ​​baza danych nie zawiera niepotrzebnych lub niespójnych danych.
- **Ułatwia usuwanie danych:** Pozwala na usunięcie wszystkich powiązanych danych za pomocą jednego polecenia DELETE.
- **Zmniejsza ilość kodu:** Eliminuje potrzebę pisania osobnych instrukcji DELETE dla każdej tabeli.
**Wady kaskadowego usuwania:**
- **Może prowadzić do utraty danych:** Należy zachować ostrożność podczas korzystania z kaskadowego usuwania, ponieważ może ono spowodować usunięcie danych, których nie chcieliśmy usunąć.
- **Może powodować problemy z wydajnością:** Usuwanie dużej ilości danych z wielu tabel może być czasochłonne.
- **Utrudnia odzyskiwanie danych:** Usunięte dane są trwale usuwane i nie można ich łatwo odzyskać.
