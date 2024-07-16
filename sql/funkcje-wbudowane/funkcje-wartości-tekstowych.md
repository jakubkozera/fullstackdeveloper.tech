## Funkcje wartości tekstowych
W MS SQL istnieje wiele funkcji do manipulowania tekstem, które pozwalają na modyfikowanie, formatowanie i analizę danych tekstowych. 

Oto kilka z najczęściej używanych:

1. **LEN()** - Zwraca długość łańcucha znaków.



```sql
   SELECT LEN('Hello World');
    
```


   Zapytanie to zwraca długość łańcucha znaków "Hello World", która wynosi 11 znaków.

2. **LEFT()** - Zwraca określoną liczbę znaków z lewej strony łańcucha znaków.



```sql
   SELECT LEFT('Hello World', 5);

```

Zapytanie zwraca pierwsze 5 znaków z lewej strony łańcucha znaków "Hello World".

3. **RIGHT()** - Zwraca określoną liczbę znaków z prawej strony łańcucha znaków.



```sql
   SELECT RIGHT('Hello World', 5);

```

Zapytanie zwraca ostatnie 5 znaków z prawej strony łańcucha znaków "Hello World".

4. **UPPER()** - Konwertuje łańcuch znaków na wielkie litery.


```sql
   SELECT UPPER('hello world');

```

   Zapytanie zamienia wszystkie litery w łańcuchu znaków "hello world" na wielkie litery.

5. **LOWER()** - Konwertuje łańcuch znaków na małe litery.



```sql
   SELECT LOWER('HELLO WORLD');

```

Zapytanie zamienia wszystkie litery w łańcuchu znaków "HELLO WORLD" na małe litery.

6. **SUBSTRING()** - Zwraca część łańcucha znaków rozpoczynając od określonej pozycji i o określonej długości.



```sql
   SELECT SUBSTRING('Hello World', 7, 3);

```

Zapytanie zwraca podciąg łańcucha znaków "Hello World" rozpoczynający się od 7. znaku i mający długość 5 znaków.

7. **REPLACE()** - Zamienia wystąpienia określonego fragmentu łańcucha znaków na inny fragment.



```sql
   SELECT REPLACE('Hello World Hello', 'Hello', 'Hi');

```

Zapytanie zamienia wszystkie wystąpienia łańcucha "Hello" w łańcuchu "Hello World" na "Hi".

8. **TRIM()** - Usuwa spacje z początku i końca łańcucha znaków.



```sql
   SELECT TRIM('   Hello World   ');

```

Zapytanie usuwa spacje z początku i końca łańcucha znaków "   Hello World   ".

9. **CONCAT()** - Łączy dwa lub więcej łańcuchów znaków.



```sql
   SELECT CONCAT('Hello', ' ', 'World');

```

Zapytanie łączy łańcuchy znaków "Hello", " " i "World" w jeden łańcuch "Hello World".

Co więcej funkcję `CONTACT()` można też zastąpić znakiem `+`:



```sql
SELECT 'Hello' + ' ' + 'World';

```


10. **CHARINDEX()** - Zwraca pozycję określonego fragmentu w łańcuchu znaków.



```sql
    SELECT CHARINDEX('ld', 'Hello World ld');

```

Zapytanie zwraca pozycję pierwszego wystąpienia łańcucha "World" w łańcuchu "Hello World", która wynosi 7.
Jeżeli szukana fraza nie zostanie znaleziona, zapytanie zwróci 0.




```sql
SELECT CHARINDEX('Hi', 'Hello World');

```



## Łączenie wywoływań funkcji dla wartości tesktowych

Funkcje dla wartości tesktowych, które zwracają wartości tekstowe, można je łączyć w celu uzyskania bardziej złożonych operacji na tekście.

Przykład 1: Łączenie wywołań funkcji `LOWER()` i `REPLACE()`:
Zamiana "HELLO WORLD" na "hi world" przez zamianę na małe litery i zastąpienie "hello" przez "hi".


```sql
SELECT REPLACE(LOWER('HELLO WORLD'), 'hello', 'hi');

```



W tym przykładzie:
- Funkcja `LOWER('HELLO WORLD')` zamienia tekst "HELLO WORLD" na małe litery, więc zwraca "hello world".
- Funkcja `REPLACE('hello world', 'hello', 'hi')` zamienia wszystkie wystąpienia "hello" w łańcuchu "hello world" na "hi", więc zwraca "hi world".

Przykład 2: Łączenie wywołań funkcji `LEFT()` i `CHARINDEX()`:



```sql
SELECT LEFT('Hello World', CHARINDEX(' ', 'Hello World') - 1);


```

W tym przykładzie:
- Funkcja `CHARINDEX(' ', 'Hello World')` zwraca pozycję pierwszej spacji w tekście "Hello World", czyli 6.
- Funkcja `LEFT('Hello World', 6 - 1)` wybiera pierwsze 5 znaków (do pozycji spacji minus jeden) z lewej strony tekstu "Hello World", czyli "Hello".

## Zadanie

  

1. Zwróć informacje: Imie, Nazwisko oraz inicjały osób z tabeli `SalesLT.Customer`


```sql
-- ROZWIĄZANIE

SELECT FirstName, LastName, LEFT(FirstName, 1) + LEFT(LastName, 1) as Initials
FROM SalesLT.Customer
```

2. Stwórz zapytanie SQL, które wykorzystując kolumnę EmailAddress z tabeli `SalesLT.Customer`, zwróci jedynie część adresu e-mail, która znajduje się przed znakiem '@'. Na przykład, dla adresu e-mail 'robert4@adventure-works.com', zapytanie powinno zwrócić wartość 'robert4'."

Rozwiązanie tego zadania można osiągnąć poprzez zastosowanie funkcji tekstowych, takich jak `LEFT()` i `CHARINDEX()`, aby wyodrębnić część adresu e-mail przed znakiem "@".


```sql
-- ROZWIĄZANIE


SELECT EmailAddress, LEFT(EmailAddress, CHARINDEX('@', EmailAddress) - 1) as UserName
FROM SalesLT.Customer
```

3. Napisz zapytanie SQL, które zwróci identyfikatory produktów `ProductDescriptionID` oraz ich opisy `Description` z tabeli `SalesLT.ProductDescription`, pod warunkiem, że długość opisu przekracza 20 znaków i jednocześnie opis nie zawiera znaku zapytania '?'.


```sql
-- ROZWIĄZANIE


SELECT ProductDescriptionID, Description
FROM SalesLT.ProductDescription
WHERE LEN([Description]) > 20 AND CHARINDEX('?', [Description]) = 0
```
