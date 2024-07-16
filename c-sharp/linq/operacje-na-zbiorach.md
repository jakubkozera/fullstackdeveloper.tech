# Operacje na zbiorach danych

Operując na różnych zbiorach danych, czasem będziemy mieli potrzebe w pewien sposób sprawdzić, które elementy występują w obu zbiorach, lub po prostu połączyć wszystkie unikalne elementy, lub wybrać tylko te elementy z pierwszej kolekcji, które nie występują w innej.
Tego typu rezultaty możemy osiągnać za pomocą następujących metod z LINQ

## Metoda Distinct
Metoda `Distinct` pozwala usunąć duplikaty z kolekcji. Dzięki temu możemy łatwo uzyskać unikalne elementy z listy czy innego typu kolekcji.

Przykład użycia metody `Distinct`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 2, 3, 4, 4, 5 };

        var uniqueNumbers = numbers.Distinct();

        foreach (var number in uniqueNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "1 2 3 4 5", ponieważ metoda `Distinct` usunęła duplikaty z listy.

## Metoda Union
Metoda `Union` pozwala na połączenie dwóch kolekcji, usuwając jednocześnie powtarzające się elementy. Wynikiem działania tej metody będzie zbiór zawierający unikalne elementy z obu kolekcji.

Przykład użycia metody `Union`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers1 = new List<int> { 1, 2, 3, 4 };
        List<int> numbers2 = new List<int> { 3, 4, 5, 6 };

        var combinedNumbers = numbers1.Union(numbers2);

        foreach (var number in combinedNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "1 2 3 4 5 6", ponieważ metoda `Union` połączyła obie listy, usuwając jednocześnie powtarzające się elementy "3" i "4".

## Metoda Intersect
Metoda `Intersect` pozwala na znalezienie wspólnych elementów występujących w dwóch kolekcjach. Wynikiem działania tej metody będzie zbiór zawierający tylko te elementy, które występują w obu kolekcjach.

Przykład użycia metody `Intersect`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers1 = new List<int> { 1, 2, 3, 4 };
        List<int> numbers2 = new List<int> { 3, 4, 5, 6 };

        var commonNumbers = numbers1.Intersect(numbers2);

        foreach (var number in commonNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "3 4", ponieważ metoda `Intersect` wybrała tylko te elementy, które występują zarówno w kolekcji `numbers1`, jak i `numbers2`.

## Metoda Except
Metoda `Except` pozwala na wybór elementów występujących tylko w jednej kolekcji i nie występujących w drugiej. Metoda ta zwraca zbiór elementów, które są unikalne dla pierwszej kolekcji i nie mają swojego odpowiednika w drugiej kolekcji.

Przykład użycia metody `Except`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers1 = new List<int> { 1, 2, 3, 4 };
        List<int> numbers2 = new List<int> { 3, 4, 5, 6 };

        var uniqueNumbers = numbers1.Except(numbers2);

        foreach (var number in uniqueNumbers)
        {
            Console.Write(number + " ");
        }
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "1 2", ponieważ metoda `Except` wybrała tylko te elementy, które występują w kolekcji `numbers1`, ale nie występują w kolekcji `numbers2`.

## Podsumowanie
Metody `Distinct`, `Union`, `Intersect` i `Except` w C# LINQ są narzędziami do wykonywania różnych operacji na zbiorach danych. Pozwalają na łatwe usuwanie duplikatów, łączenie kolekcji, znajdowanie wspólnych elementów oraz wybieranie unikalnych elementów między dwoma zbiorami. Dzięki nim operacje na danych stają się bardziej wydajne i czytelne, a programiści mogą łatwiej manipulować danymi w swoich aplikacjach. Warto zapoznać się z tymi metodami, gdyż mogą znacznie ułatwić pracę z kolekcjami danych w języku C#.
## YouTube

*https://www.youtube.com/watch?v=oAr_G12lYdU&t=3461s*