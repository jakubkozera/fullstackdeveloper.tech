# Powszechne operatory

Operatory w C# to specjalne znaki lub słowa kluczowe, które służą do wykonywania różnych operacji na zmiennych, stałych i obiektach. Są one podstawowymi budulcami języka programowania, ponieważ pozwalają na wykonywanie różnych operacji matematycznych, porównań i manipulacji na danych.

Operatory w C# umożliwiają wykonywanie zadań, takich jak dodawanie, odejmowanie, mnożenie, dzielenie, porównywanie wartości, łączenie wartości logicznych, operacje na bitach, itp. Używanie operatorów zamiast ręcznego wykonywania operacji na zmiennych znacznie ułatwia programowanie i sprawia, że kod jest bardziej czytelny i zwięzły.

Istnieje wiele różnych operatorów, a każdy z nich ma określony priorytet i łączność, co wpływa na kolejność wykonywania operacji. Dlatego ważne jest, aby znać różne operatory i ich zasady działania, aby pisać skuteczny i efektywny kod.

## Przykładowe operatory

1. Przypisania: używane do przypisywania wartości do zmiennych lub właściwości. Przykładowo: `=, +=, -=, *=, /=`.

2. Arytmetyczne: używane do wykonywania operacji matematycznych, takich jak dodawanie, odejmowanie, mnożenie i dzielenie. Przykładowo: `+, -, *, /, %`.

3. Porównania: używane do porównywania wartości, takich jak równość, nierówność, większość, mniejszość i ich warianty. Przykładowo: `==, !=, >, <, >=, <=`.

4. Logiczne: używane do łączenia wyrażeń logicznych i sprawdzania, czy są prawdziwe lub fałszywe. Przykładowo: `&&` (and), `||` (or), `!` (not).

5. Inkrementacji i dekrementacji: używane do zwiększania lub zmniejszania wartości zmiennej o 1. Przykładowo: `++` (inkrementacja), `--` (dekrementacja).

6. Warunkowe: używane do tworzenia warunkowych wyrażeń, które wykonują różne instrukcje w zależności od wartości logicznej. Przykładowo: `?:` - operator warunkowy ternary, który umożliwia wykonanie instrukcji warunkowej w jednej linii.

    ```
    string message = age >= 18 ? "Person is an adult" : "Person is a minor";
    ```
    W tym przykładzie, jeśli `age` jest większe lub równe 18, to zmianna `message` przyjmie wartość "Person is an adult", a jeśli jest mniejsze niż 18, to "Person is a minor".

7. Null-coalescing: używane do ustawiania wartości domyślnej, jeśli zmienna jest równa null. Przykładowo: `??`.
    ```
    int? age = null;
    string name = null; 

    int defaultAge = age ?? 18; 
    string defaultName = name ?? "John Doe"; 
    ```
    W tym przykładzie `age` to wartość typu nullable, a `name` to typ referencyjny, obie zmienne mają przypisaną wartość `null`. Operator `??` jest używany do przypisania wartości domyślnych do `defaultAge` i `defaultName`. Jeśli `age` lub `name` jest równe `null`, to wartości domyślne 18 i "John Doe" są przypisywane do `defaultAge` i `defaultName` odpowiednio.



## YouTube
https://www.youtube.com/watch?v=d1ZyKfTAI9s