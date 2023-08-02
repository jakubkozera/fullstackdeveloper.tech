# Dzielenie danych

Za pomocą LINQ, będziemy w stanie w pewien sposób wybierać konkretną liczbę elementów z kolekcji. Możemy to zrobić na kilka sposobów:
- wybrać n pierwszych elementów z kolekcji
- wybrać n ostatnich elementów z kolekcji
- wybrać wszystkie elementy z początku kolekcji, które spełają konkretny warunek
- wybrać wszystkie elementy z końca kolekcji, które spełają konkretny warunek

Te cztery sposoby są wykonane za pomocą metod: `Take`, `Skip`, `TakeWhile`, `SkipWhile`


## Metoda Take
Metoda `Take` umożliwia wyodrębnienie określonej liczby elementów z początku kolekcji. Jeśli mamy listę elementów i chcemy wybrać tylko kilka z nich, możemy to zrobić przy użyciu metody `Take`. Metoda ta działa na dowolnej kolekcji implementującej interfejs `IEnumerable<T>`, np. na tablicach, listach czy zapytaniach do bazy danych.

Przykład użycia metody `Take`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        var selectedNumbers = numbers.Take(5);

        foreach (var number in selectedNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wypisanie "1 2 3 4 5", ponieważ metoda `Take(5)` wybrała pierwsze 5 elementów z listy.

## Metoda TakeWhile
Metoda `TakeWhile` działa na podobnej zasadzie jak `Take`, ale zatrzymuje się, gdy warunek spełniony przez elementy nie jest już spełniany. Oznacza to, że bierze tylko te elementy z początku kolekcji, które spełniają określony warunek, a gdy napotka element, który już go nie spełnia, kończy działanie.

Przykład użycia metody `TakeWhile`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 2, 4, 6, 7, 8, 9, 10 };

        var selectedNumbers = numbers.TakeWhile(num => num % 2 == 0);

        foreach (var number in selectedNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wypisanie "2 4 6", ponieważ metoda `TakeWhile` wybiera tylko te elementy, które są parzyste, a kończy działanie, gdy napotka pierwszy element nieparzysty (czyli "7").

## Metoda Skip
Metoda `Skip` pozwala pominąć określoną liczbę elementów na początku kolekcji i zwrócić pozostałe. W ten sposób możemy łatwo usunąć niechciane początkowe elementy z kolekcji.

Przykład użycia metody `Skip`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        var skippedNumbers = numbers.Skip(3);

        foreach (var number in skippedNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wypisanie "4 5 6 7 8 9 10", ponieważ metoda `Skip(3)` pominęła pierwsze 3 elementy.

## Metoda SkipWhile
Podobnie jak `TakeWhile`, metoda `SkipWhile` działa na kolekcji, ale pomija elementy, które spełniają określony warunek, aż napotka pierwszy element, który go nie spełnia. Następnie zwraca pozostałe elementy.

Przykład użycia metody `SkipWhile`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 3, 5, 2, 4, 6, 8, 7, 9, 10 };

        var skippedNumbers = numbers.SkipWhile(num => num % 2 == 1);

        foreach (var number in skippedNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wypisanie "2 4 6 8 7 9 10", ponieważ metoda `SkipWhile` pominęła pierwsze elementy spełniające warunek nieparzystości (czyli "1 3 5"), a następnie zwróciła pozostałe.

## Podsumowanie
Metody `Take`, `TakeWhile`, `Skip` i `SkipWhile` są prostymi narzędziami do dzielenia danych w C# przy użyciu LINQ. Pozwalają one w prosty sposób wybierać lub pomijać odpowiednie elementy z kolekcji na podstawie określonych kryteriów. Dzięki nim operacje na danych stają się bardziej czytelne, eleganckie i wydajne. Znając te metody, możemy wygodnie manipulować naszymi danymi i uzyskiwać dokładnie te fragmenty, które są nam potrzebne.


## YouTube

*https://www.youtube.com/watch?v=oAr_G12lYdU&t=2322s*