# Wyrażenie lambda 

Wyrażenie lambda to krótki zapis funkcji anonimowej, która może być użyta w kodzie jako argument metody lub przypisana do zmiennej. Jest to sposób na definiowanie funkcji w locie bez konieczności pisania pełnej definicji funkcji.

Przykładowo, wyrażenie lambda może wyglądać następująco:

`x => x * x`

Ten kod oznacza, że funkcja przyjmuje argument `x` i zwraca jego wartość podniesioną do kwadratu. Można to przypisać do zmiennej i wykorzystać w kodzie w następujący sposób:

```
Func<int, int> square = x => x * x;
int result = square(5); // wartość result będzie równa 25

```

W powyższym przykładzie utworzyliśmy funkcję anonimową o nazwie `square`, która przyjmuje argument typu `int` i zwraca również wartość typu `int`. Następnie wywołaliśmy tę funkcję, przekazując jej argument 5 i zapisaliśmy wynik do zmiennej `result`.

https://www.youtube.com/watch?v=6L6W9L5XgXE 