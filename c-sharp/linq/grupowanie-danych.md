# Grupowanie danych

Grupowanie danych to często spotykana operacja podczas przetwarzania kolekcji danych. Pozwala na podział elementów na logiczne grupy na podstawie wspólnych atrybutów lub kluczy. W języku C# LINQ mamy dostęp do metody `GroupBy`, która umożliwia łatwe grupowanie danych na podstawie określonych kluczy. W tym artykule omówimy, czym są grupy w LINQ i jak iterować po elementach w każdej grupie.

## Czym są grupy w LINQ?

Grupy w LINQ są wynikiem operacji grupowania danych na podstawie wspólnych kluczy. Każda grupa jest reprezentowana jako obiekt typu `IGrouping<TKey, TElement>`, gdzie `TKey` to typ klucza, a `TElement` to typ elementów w danej grupie. Metoda `GroupBy` tworzy sekwencję grup, w której każda grupa zawiera elementy, których wartość klucza jest taka sama.

Przykładowo, gdy mamy listę pracowników i chcemy je podzielić na grupy na podstawie departamentu, każda grupa będzie reprezentować pracowników z tego samego departamentu.

## Metoda GroupBy

Metoda `GroupBy` umożliwia grupowanie danych w kolekcji na podstawie określonych kluczy. Możemy zdefiniować funkcję (wyrażenie lambda) jako argument metody, która będzie zwracać klucz dla każdego elementu, na podstawie którego nastąpi grupowanie.

Przykład użycia metody `GroupBy`:

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
            new Employee { Name = "John", Department = "HR" },
            new Employee { Name = "Alice", Department = "Finance" },
            new Employee { Name = "Bob", Department = "HR" },
            new Employee { Name = "Eva", Department = "IT" },
            new Employee { Name = "Mike", Department = "IT" }
        };

        var groupedEmployees = employees.GroupBy(emp => emp.Department);

        foreach (var group in groupedEmployees)
        {
            Console.WriteLine("Department: " + group.Key);
            foreach (var employee in group)
            {
                Console.WriteLine(" - " + employee.Name);
            }
        }
    }
}

class Employee
{
    public string Name { get; set; }
    public string Department { get; set; }
}
```

Wynikiem działania tego kodu będzie wypisanie:

```
Department: HR
 - John
 - Bob
Department: Finance
 - Alice
Department: IT
 - Eva
 - Mike
```

## Iteracja po elementach grup

Aby iterować po elementach w każdej grupie, możemy użyć pętli `foreach` do przechodzenia przez każdą grupę zwróconą przez metodę `GroupBy`, a następnie wewnętrznej pętli `foreach`, aby przejść przez elementy w danej grupie.

W powyższym przykładzie, wewnętrzna pętla `foreach` wypisuje imiona pracowników w każdej grupie.

```csharp
foreach (var group in groupedEmployees)
{
    Console.WriteLine("Department: " + group.Key);
    foreach (var employee in group)
    {
        Console.WriteLine(" - " + employee.Name);
    }
}
```

## Podsumowanie

Metoda `GroupBy` w C# LINQ umożliwia łatwe grupowanie danych na podstawie określonych kluczy. Grupy w LINQ są reprezentowane jako obiekty `IGrouping<TKey, TElement>`, które zawierają elementy o tych samych kluczach. Iteracja po elementach grup odbywa się za pomocą zagnieżdżonych pętli `foreach`. Dzięki metodzie `GroupBy` możemy w prosty sposób podzielić dane na logiczne grupy, co jest bardzo przydatne podczas analizy i przetwarzania dużych kolekcji danych w naszych aplikacjach.

## YouTube

*https://www.youtube.com/watch?v=0plHg95D220&t=130s*