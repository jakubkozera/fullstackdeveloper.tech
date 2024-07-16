# Kolekcje - wprowadzenie

W języku C# istnieje wiele rodzajów kolekcji, które służą do przechowywania i zarządzania grupą obiektów. Oto kilka najczęściej używanych typów kolekcji:

- `List<T>` reprezentuje dynamiczną listę obiektów, która automatycznie zmienia swój rozmiar w miarę dodawania i usuwania elementów. Elementy listy mogą być dowolnego typu.

- `Dictionary<TKey, TValue>` reprezentuje słownik, czyli zbiór par typu klucz-wartość. Klucze muszą być unikalne, a wartości mogą być dowolnego typu.

- `HashSet<T>` to kolekcja, która przechowuje unikalne elementy w dowolnej kolejności. Elementy zbioru mogą być dowolnego typu. `HashSet<T>` wykorzystuje algorytm haszujący do szybkiego sprawdzenia, czy dany element już istnieje w zbiorze. Jeśli element już istnieje, nie zostanie dodany ponownie ponieważ `HashSet<T>` nie umożliwia duplikowania elementów, a każdy element jest identyfikowany przez swój unikalny hash code.

W języku C# istnieje wiele innych typów kolekcji, w tym `LinkedList`, `SortedList`, `SortedSet` i wiele innych. Każda z tych kolekcji ma swoje zastosowanie i charakterystyczne cechy, dlatego ważne jest, aby wybrać odpowiedni typ kolekcji do rozwiązania konkretnej potrzeby programistycznej.

Pod generyczny typ `T`, możemy wstawić dowolny typ wbudowany jak np. `int`, `string` czy `DateTime`, ale równie dobrze może to być klasa zdefniowana w ramach naszego programu.

## YouTube

*https://www.youtube.com/watch?v=iqjdNDrBHRw*