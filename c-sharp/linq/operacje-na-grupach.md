# Operacje na grupach

Operacje na grupach danych są kluczowym aspektem analizy danych i raportowania w aplikacjach. W języku C# LINQ (Language-Integrated Query) mamy dostęp do wielu przydatnych metod, które pozwalają na wykonywanie różnych operacji na grupach danych. W tym artykule skupimy się na czterech głównych operacjach, które możemy wykonać na grupach danych za pomocą metod LINQ: `Min`, `Max`, `Sum` i `Average`.

## Metoda Min
Metoda `Min` zwraca najmniejszą wartość w danej grupie. Działa na wartościach liczbowych, datach i innych typach, które można porównać.

Przykład użycia metody `Min`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 10, 5, 20, 15, 30 };

        var minNumber = numbers.Min();

        Console.WriteLine("Najmniejsza liczba: " + minNumber);
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "Najmniejsza liczba: 5", ponieważ `Min` zwróciła najmniejszą liczbę z listy.

## Metoda Max
Metoda `Max` zwraca największą wartość w danej grupie. Podobnie jak `Min`, działa na wartościach liczbowych, datach i innych typach porównywalnych.

Przykład użycia metody `Max`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 10, 5, 20, 15, 30 };

        var maxNumber = numbers.Max();

        Console.WriteLine("Największa liczba: " + maxNumber);
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "Największa liczba: 30", ponieważ `Max` zwróciła największą liczbę z listy.

## Metoda Sum
Metoda `Sum` oblicza sumę wartości numerycznych w danej grupie.

Przykład użycia metody `Sum`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 10, 5, 20, 15, 30 };

        var sumOfNumbers = numbers.Sum();

        Console.WriteLine("Suma liczb: " + sumOfNumbers);
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "Suma liczb: 80", ponieważ `Sum` obliczyła sumę liczb z listy.

## Metoda Average
Metoda `Average` oblicza średnią wartość numeryczną w danej grupie.

Przykład użycia metody `Average`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 10, 5, 20, 15, 30 };

        var averageOfNumbers = numbers.Average();

        Console.WriteLine("Średnia liczb: " + averageOfNumbers);
    }
}
```

Wynikiem działania tego kodu będzie wydrukowanie "Średnia liczb: 16", ponieważ `Average` obliczyła średnią liczb z listy.

## Przydatność i zastosowanie

Metody `Min`, `Max`, `Sum` i `Average` są bardzo użyteczne w analizie danych i raportowaniu. Pozwalają one na szybkie wyznaczanie ekstremalnych wartości, sumy lub średniej dla grup danych. Możemy ich użyć, gdy potrzebujemy szybkich obliczeń na wielu wartościach numerycznych w grupach, co jest częstym przypadkiem w analizie danych, statystykach czy generowaniu raportów.

Na przykład, możemy użyć tych metod do obliczenia najwyższego wyniku z testu dla grupy uczniów, sumy zamówień dla danego klienta, minimalnej temperatury dla grupy dni w danym miesiącu i wielu innych scenariuszach.

```csharp
// Przykład użycia dla kolekcji obiektów typu Employee z polem Salary
var maxSalary = employees.Max(emp => emp.Salary);
var minSalary = employees.Min(emp => emp.Salary);
var totalSalary = employees.Sum(emp => emp.Salary);
var averageSalary = employees.Average(emp => emp.Salary);
```

## Zgrupowane kolekcje

Metody `Min`, `Max`, `Sum` i `Average` mogą być używane na wynikach grupowania uzyskanych za pomocą metody `GroupBy`. Po wykonaniu metody `GroupBy`, otrzymujemy sekwencję grup danych, gdzie każda grupa jest reprezentowana przez obiekt typu `IGrouping<TKey, TElement>`. Te metody pozwalają na wykonanie odpowiednich operacji na wartościach numerycznych zawartych w grupach.

Oto przykładowy scenariusz, w którym używamy tych metod na wynikach grupowania:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<Employee> employees = new List<Employee>
        {
            new Employee { Name = "John", Department = "HR", Salary = 3000 },
            new Employee { Name = "Alice", Department = "Finance", Salary = 4000 },
            new Employee { Name = "Bob", Department = "HR", Salary = 3500 },
            new Employee { Name = "Eva", Department = "IT", Salary = 4500 },
            new Employee { Name = "Mike", Department = "IT", Salary = 4200 }
        };

        var groupedEmployees = employees.GroupBy(emp => emp.Department);

        foreach (var group in groupedEmployees)
        {
            Console.WriteLine("Department: " + group.Key);
            var minSalary = group.Min(emp => emp.Salary);
            var maxSalary = group.Max(emp => emp.Salary);
            var totalSalary = group.Sum(emp => emp.Salary);
            var averageSalary = group.Average(emp => emp.Salary);

            Console.WriteLine(" - Min salary: " + minSalary);
            Console.WriteLine(" - Max salary: " + maxSalary);
            Console.WriteLine(" - Total salary: " + totalSalary);
            Console.WriteLine(" - Average salary: " + averageSalary);
        }
    }
}

class Employee
{
    public string Name { get; set; }
    public string Department { get; set; }
    public int Salary { get; set; }
}
```

W powyższym przykładzie, najpierw grupujemy pracowników na podstawie departamentu. Następnie iterujemy po wynikach grupowania za pomocą pętli `foreach`. Wewnątrz tej pętli możemy wykonać operacje na wartościach numerycznych, takie jak znalezienie najmniejszej (`Min`) i największej (`Max`) pensji w danej grupie, obliczenie sumy (`Sum`) pensji dla grupy oraz średniej (`Average`) pensji w danej grupie.

Warto zauważyć, że używając tych metod na obiektach `IGrouping<TKey, TElement>`, mamy dostęp do atrybutu `Key`, który reprezentuje wartość klucza grupy. W przykładzie wyświetlamy wartość klucza, czyli departament, dla każdej grupy. Następnie dla każdej grupy obliczamy odpowiednie wartości statystyczne na podstawie wynagrodzeń pracowników w tej grupie.

Podsumowując, metody `Min`, `Max`, `Sum` i `Average` mogą być używane na wynikach grupowania (`IGrouping<TKey, TElement>`) do wykonania operacji statystycznych lub obliczeń na wartościach numerycznych w poszczególnych grupach danych.

## Podsumowanie

Metody `Min`, `Max`, `Sum` i `Average` w C# LINQ są bardzo użytecznymi narzędziami do wykonywania różnych operacji na grupach danych. Pozwalają one na szybkie wyznaczanie wartości ekstremalnych, sumy oraz średniej dla wartości numerycznych w kolekcjach. Dzięki nim operacje na danych stają się bardziej czytelne i wydajne, a programiści mogą łatwo analizować dane w swoich aplikacjach. Warto zapoznać się z tymi metodami, gdyż są one niezwykle przydatne w analizie danych i statystykach w języku C#.

## YouTube

*https://www.youtube.com/watch?v=0plHg95D220&t=781s*