# Projekcja danych
 
Projekcja danych jest jednym z kluczowych elementów, które czynią LINQ tak potężnym narzędziem w języku C#. Dzięki technice projekcji możemy przekształcić dane z jednej formy do innej, w prosty i czytelny sposób. W tym artykule omówimy metodę `Select`, która jest używana do projekcji danych w LINQ.

## Metoda Select

Metoda `Select` w LINQ jest używana do wybierania i przekształcania danych z kolekcji. Sygnatura tej metody wygląda następująco:

```csharp
public static IEnumerable<TResult> Select<TSource, TResult>(this IEnumerable<TSource> source, Func<TSource, TResult> selector);
```

Metoda `Select`, jest metodą rozszerzającą dowolną kolekcję (`IEnumerable<TSource> source`) i przyjmuje dwa parametry:
- `source`: Kolekcja, z której chcemy wybrać i przekształcić dane.
- `selector`: Delegat, który określa, jak przekształcić każdy element z kolekcji. Ten delegat przyjmuje element z kolekcji i zwraca przekształcony wynik.

Przykład użycia:

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };
var squaredNumbers = numbers.Select(x => x * x);
foreach (var num in squaredNumbers)
{
    Console.WriteLine(num); // Wypisze: 1, 4, 9, 16, 25
}
```

W powyższym przykładzie, używając metody `Select`, każdy element z kolekcji `numbers` został podniesiony do kwadratu i wyniki zostały zapisane w kolekcji `squaredNumbers`.

## Select do zwracania anonimowych kolekcji

Metodę `Select` możemy również wykorzystać do zwracania kolekcji anonimowych - czyli listy obiektów, które nie mają zdefiniowanego typu.

Rozważmy poniższy przykład aplikacji:


```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        // Przykładowa kolekcja obiektów typu Person
        var people = new List<Person>
        {
            new Person { FirstName = "John", LastName = "Doe", Age = 30 },
            new Person { FirstName = "Jane", LastName = "Smith", Age = 25 },
            new Person { FirstName = "Tom", LastName = "Johnson", Age = 40 }
        };

        // Using the Select method to create a new anonymous object containing selected properties
        var anonymousObjects = people.Select(p => new
        {
            FullName = p.FirstName + " " + p.LastName,
            AgeInfo = $"Age: {p.Age} years old"
        });

        // Displaying the results
        foreach (var anonymousObject in anonymousObjects)
        {
            Console.WriteLine(anonymousObject.FullName + ", " + anonymousObject.AgeInfo);
        }
    }
}

class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int Age { get; set; }
}
```

W tym przykładzie mamy klasę `Person` z trzema właściwościami: `FirstName`, `LastName` i `Age`. Wykorzystujemy metodę `Select` do utworzenia nowego anonimowego obiektu, który zawiera tylko dwie właściwości: `FullName` (łącząc imię i nazwisko) oraz `AgeInfo` (zawierający informację o wieku w odpowiednim formacie).

Wynik działania programu będzie wyglądał następująco:

```
John Doe, Age: 30 years old
Jane Smith, Age: 25 years old
Tom Johnson, Age: 40 years old
```

Dzięki temu, że korzystamy z anonimowego typu, nie musimy tworzyć osobnej klasy dla tego jednorazowego użycia, co pozwala na bardziej zwięzły i czytelny kod.
## Zalety projekcji danych przy użyciu Select

1. **Optymalizacja pamięci**: Metoda `Select` pozwala na tworzenie nowych kolekcji tylko z interesującymi nas danymi, co pozwala zaoszczędzić pamięć i poprawić wydajność aplikacji.

2. **Skrócenie kodu**: Zastosowanie metody `Select` pozwala na zwięzły i czytelny zapis przekształceń danych, eliminując potrzebę ręcznego tworzenia pętli.

3. **Zachowanie oryginalnych danych**: Przy użyciu metody `Select`, oryginalna kolekcja pozostaje nietknięta, co jest szczególnie ważne w sytuacjach, gdy potrzebujemy jednocześnie różnych wariantów danych.

4. **Elastyczność**: Metoda `Select` pozwala na dowolne przekształcenia danych, nie tylko matematyczne operacje, ale także na zmianę typów, wybieranie konkretnych właściwości obiektów, itp.

## Podsumowanie

Metoda `Select` w C# LINQ jest potężnym narzędziem do przekształcania danych z jednej formy do drugiej. Dzięki niej możemy wybierać interesujące nas dane, zmieniać ich format, redukować zbiorcze dane, a także zmieniać typy. Prosta i czytelna składnia metody `Select` przyczynia się do zwiększenia czytelności kodu oraz poprawy wydajności aplikacji poprzez optymalne zarządzanie pamięcią. Pamiętaj, że metoda `Select` to tylko jedna z wielu zaawansowanych możliwości, które oferuje LINQ, umożliwiając bardziej efektywne i zwięzłe operacje na danych w języku C#.

## YouTube

*https://www.youtube.com/watch?v=oAr_G12lYdU&t=1523s*