# Pobieranie danych

LINQ (Language-Integrated Query) to zaawansowany mechanizm w języku C#, który umożliwia łatwe i wydajne zarządzanie kolekcjami danych. Jedną z najważniejszych części LINQ jest możliwość pobierania elementów z kolekcji zgodnie z określonymi kryteriami. Poniżej zostały omówione podstawowe metody LINQ do pobierania pojedynczych elementów z kolekcji: `First`, `FirstOrDefault`, `Single`, `SingleOrDefault` i `Where`.

## 1. Metoda First

Metoda `First` służy do pobierania pierwszego elementu z kolekcji, który spełnia określone warunki. Jeśli nie ma elementu pasującego do podanego warunku, zostanie zgłoszony wyjątek `InvalidOperationException`. Metoda ta jest szczególnie użyteczna, gdy oczekujemy co najmniej jednego elementu w kolekcji i chcemy pobrać ten pierwszy pasujący.

Przykład użycia:

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };
var firstEven = numbers.First(x => x % 2 == 0);
Console.WriteLine(firstEven); // Wypisze: 2
```

## 2. Metoda FirstOrDefault

Metoda `FirstOrDefault` działa bardzo podobnie do metody `First`. Różnica polega na tym, że jeśli nie znaleziono elementu spełniającego warunek, zamiast zgłaszać wyjątek, zwróci domyślną wartość dla danego typu danych (dla typów referencyjnych będzie to null, a dla typów wartościowych - 0, false lub odpowiednik typu).

Przykład użycia:

```csharp
var numbers = new List<int> { 1, 3, 5, 7, 9 };
var firstEvenOrDefault = numbers.FirstOrDefault(x => x % 2 == 0);
Console.WriteLine(firstEvenOrDefault); // Wypisze: 0 (domyślna wartość dla typu int)
```

## 3. Metoda Single

Metoda `Single` służy do pobierania jedynego elementu z kolekcji, który spełnia podany warunek. Jeśli nie zostanie znaleziony dokładnie jeden element pasujący do warunku lub jeśli kolekcja jest pusta, zostanie zgłoszony wyjątek `InvalidOperationException`. Metoda ta jest przydatna w przypadkach, gdy oczekujemy tylko jednego wyniku i chcemy upewnić się, że nie ma więcej niż jeden pasujący element w kolekcji.

Przykład użycia:

```csharp
var fruits = new List<string> { "apple", "banana", "cherry" };
var singleFruit = fruits.Single(x => x.StartsWith("b"));
Console.WriteLine(singleFruit); // Wypisze: banana
```

## 4. Metoda SingleOrDefault

Metoda `SingleOrDefault` działa analogicznie do metody `Single`, ale zwróci domyślną wartość dla danego typu danych, jeśli nie zostanie znaleziony dokładnie jeden pasujący element lub gdy kolekcja jest pusta. Podobnie jak w przypadku metody `FirstOrDefault`, dla typów referencyjnych zwróci null, a dla typów wartościowych - 0, false lub odpowiednik typu.

Przykład użycia:

```csharp
var fruits = new List<string> { "apple", "cherry", "orange" };
var singleFruitOrDefault = fruits.SingleOrDefault(x => x.StartsWith("b"));
Console.WriteLine(singleFruitOrDefault); // Wypisze: null (domyślna wartość dla typu string)
```
## 5. Metoda Where

Metoda `Where` jest używana do filtrowania kolekcji na podstawie określonego warunku. 

Metoda ta zwraca nową kolekcję zawierającą tylko elementy, które spełniają określony warunek. Jest to przydatne, gdy chcemy otrzymać podzbiór danych z oryginalnej kolekcji, który spełnia określone kryteria.

Przykład użycia - pobieranie tylko parzystych elementow z kolekcji typu `int`:

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };
var evenNumbers = numbers.Where(x => x % 2 == 0);
foreach (var number in evenNumbers)
{
    Console.WriteLine(number); // Wypisze: 2, 4
}
```

## Podsumowanie

Metody `Where`, `First`, `FirstOrDefault`, `Single` i `SingleOrDefault` są niezwykle przydatnymi narzędziami w C# LINQ, które umożliwiają precyzyjne pobieranie elementów z kolekcji zgodnie z podanymi kryteriami. Pamiętaj, że korzystając z tych metod, warto zawsze sprawdzić, czy warunek nie jest zbyt restrykcyjny i czy nie będzie powodował nieoczekiwanych wyjątków lub zwracania domyślnych wartości, jeśli dane nie spełniają oczekiwań.

LINQ jest potężnym narzędziem, które ułatwia pracę z danymi i pozwala na bardziej zwięzły i czytelny kod. Znając różnice między metodami `First`, `FirstOrDefault`, `Single` i `SingleOrDefault`, będziesz w stanie bardziej świadomie i skutecznie zarządzać danymi w swoich aplikacjach w C#.
 ## YouTube

*https://www.youtube.com/watch?v=oAr_G12lYdU?t=536*