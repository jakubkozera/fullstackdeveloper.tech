# Lista

Lista to kolekcja danych, która przechowuje elementy tego samego typu. Lista w C# jest implementacją interfejsu `IList<T>`, który definiuje operacje dodawania, usuwania, odczytywania i aktualizacji elementów.

Aby utworzyć nową listę w C#, należy użyć klasy `List<T>`. Konstruktor klasy `List` przyjmuje opcjonalny argument `capacity`, który określa początkową pojemność listy.

Przykładowo, można utworzyć listę, która przechowuje liczby całkowite i dodać do niej kilka elementów:

```
List<int> numbers = new List<int>();
numbers.Add(1);
numbers.Add(2);
numbers.Add(3);

Console.WriteLine(numbers[1]); // wypisze "2"
```

W powyższym przykładzie utworzyliśmy nową listę `numbers`, która przechowuje liczby całkowite. Następnie dodaliśmy trzy liczby do listy za pomocą metody `Add`. Na koniec, pobraliśmy drugi element z listy używając operatora `[]` i wypisaliśmy go na konsoli.

Można również utworzyć listę zainicjalizowaną wartościami:

`List<int> numbers = new List<int>() { 1, 2, 3 };`

 Oprócz standardowych metod dodawania, usuwania i odczytywania elementów, lista oferuje wiele innych ciekawych funkcjonalności.

1. Metoda `Contains` - pozwala sprawdzić, czy dany element znajduje się na liście:
    ```
    List<int> numbers = new List<int>() { 1, 2, 3 };
    bool containsTwo = numbers.Contains(2); // true
    ```
2. Metoda `FindAll` - pozwala znaleźć wszystkie elementy, które spełniają określony warunek:
    ```
    List<int> numbers = new List<int>() { 1, 2, 3, 4, 5 };
    List<int> evenNumbers = numbers.FindAll(x => x % 2 == 0); // [2, 4]
    ```
3. Metoda `Sort` - pozwala posortować elementy na liście:
    ```
    List<int> numbers = new List<int>() { 5, 2, 8, 1, 3 };
    numbers.Sort(); // [1, 2, 3, 5, 8]
    ```
4. Metoda `Reverse` - pozwala odwrócić kolejność elementów na liście:
    ```
    List<int> numbers = new List<int>() { 1, 2, 3 };
    numbers.Reverse(); // [3, 2, 1]
    ```


## YouTube
https://www.youtube.com/watch?v=9CcOqfEnV2o 