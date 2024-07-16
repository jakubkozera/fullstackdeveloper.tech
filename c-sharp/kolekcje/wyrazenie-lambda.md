# Wyrażenie lambda 

Wyrażenie lambda to krótki zapis funkcji anonimowej, która może być użyta w kodzie jako argument metody lub przypisana do zmiennej. Jest to sposób na definiowanie funkcji w locie bez konieczności pisania pełnej definicji funkcji.

Przykładowo, bez wykorzystania lambdy, możemy utworzyć metodę do obliczania kwadratu danej liczby w następujący sposób:

```
int Square(int value)
{
    return x * x;
}
```
Natomiast tą samą metodę możemy zapisać pod postacią anonimowej funkcji, wykorzystując do tego skrócony zapis lambdy:

`x => x * x`

Ten kod oznacza, że funkcja przyjmuje argument `x` i zwraca jego wartość podniesioną do kwadratu. Można to przypisać do zmiennej i wykorzystać w kodzie w następujący sposób:

```
Func<int, int> square = x => x * x;
int result = square(5); // wartość result będzie równa 25

```

W powyższym przykładzie utworzyliśmy funkcję anonimową o nazwie `square`, która przyjmuje argument typu `int` i zwraca również wartość typu `int`. Następnie wywołaliśmy tę funkcję, przekazując jej argument 5 i zapisaliśmy wynik do zmiennej `result`.

## Zastosowanie

Wyrażenia lambda w C# są przydatne w wielu sytuacjach, w których potrzebujemy przekazać krótką funkcję jako argument do innej funkcji, lub kiedy potrzebujemy stworzyć anonimową funkcję, której nie ma sensu definiować w oddzielnym bloku kodu.

Przykładowo wyrażenia lambda są często używane do przetwarzania kolekcji w C# przy użyciu metody `IEnumerable<T>.Where`, `IEnumerable<T>.Select`, `IEnumerable<T>.OrderBy`, `IEnumerable<T>.GroupBy`, itp. 

Na przykład, aby wyfiltrować listę liczb całkowitych, możemy użyć następującego wyrażenia lambda:

``numbers.Where(x => x > 10)``

Tutaj do metody `Where` (która filtruje kolekcje na podstawie metody zwracającej wartość `true`/`false`, dla każdego z elementów), przekazaliśmy anonimową funkcje za pomocą lambdy, która sprawdzi czy konkretny element kolekcji jest większy od 10.

## YouTube

*https://www.youtube.com/watch?v=6L6W9L5XgXE* 