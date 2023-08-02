# Weryfikacja danych

Weryfikacja danych jest kluczowym aspektem każdej aplikacji, aby upewnić się, że spełniają one określone kryteria lub warunki. W języku C# LINQ (Language-Integrated Query) mamy do dyspozycji dwie użyteczne metody, które pozwalają na weryfikację danych w kolekcjach: `All` i `Any`. W tym artykule przyjrzymy się tym metodom i jak można ich użyć do sprawdzania danych w różnych scenariuszach.

## Metoda All
Metoda `All` weryfikuje, czy wszystkie elementy w kolekcji spełniają określony warunek. Zwraca wartość logiczną `true`, jeśli każdy element w kolekcji spełnia warunek, w przeciwnym razie zwraca `false`.

Przykład użycia metody `All`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

        bool allNumbersAreEven = numbers.All(num => num % 2 == 0);

        Console.WriteLine("Czy wszystkie liczby są parzyste? " + allNumbersAreEven);
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "Czy wszystkie liczby są parzyste? False", ponieważ nie wszystkie liczby w kolekcji `numbers` są parzyste (np. "1" i "3").

## Metoda Any
Metoda `Any` sprawdza, czy przynajmniej jeden element w kolekcji spełnia określony warunek. Zwraca `true`, jeśli chociaż jeden element w kolekcji spełnia warunek, w przeciwnym razie zwraca `false`.

Przykład użycia metody `Any`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

        bool anyNumberIsEven = numbers.Any(num => num % 2 == 0);

        Console.WriteLine("Czy przynajmniej jedna liczba jest parzysta? " + anyNumberIsEven);
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "Czy przynajmniej jedna liczba jest parzysta? True", ponieważ co najmniej jedna liczba w kolekcji `numbers` jest parzysta (np. "2" i "4").

## Zastosowanie
Metody `All` i `Any` są bardzo przydatne, gdy chcemy zweryfikować dane w kolekcji przed wykonaniem pewnych operacji lub podjąć decyzję na podstawie występowania określonych danych. Możemy je wykorzystać do filtrowania danych, sprawdzania poprawności wprowadzonych wartości czy weryfikowania spełnienia określonych warunków w danych.

Przykładowe zastosowanie `All`:

```csharp
// Sprawdzenie, czy wszyscy pracownicy są pełnoletni
bool allEmployeesAreAdults = employees.All(emp => emp.Age >= 18);
```

Przykładowe zastosowanie `Any`:

```csharp
// Sprawdzenie, czy w liście zamówień jest co najmniej jedno zakończone
bool anyOrderIsCompleted = orders.Any(order => order.Status == OrderStatus.Completed);
```

## Podsumowanie
Metody `All` i `Any` w C# LINQ są potężnymi narzędziami do weryfikacji danych w kolekcjach. Dzięki nim możemy sprawdzać, czy wszystkie elementy spełniają określony warunek (`All`), bądź czy przynajmniej jeden element spełnia ten warunek (`Any`). Pozwalają one na prostą i czytelną weryfikację danych i umożliwiają podjęcie odpowiednich działań na podstawie wyników weryfikacji. Przy rozwiązywaniu różnych problemów związanych z danymi, warto wziąć pod uwagę te metody, gdyż mogą znacznie ułatwić operacje na kolekcjach w języku C#.

## YouTube

*https://www.youtube.com/watch?v=oAr_G12lYdU&t=4245s*