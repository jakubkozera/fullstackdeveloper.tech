# Sortowanie danych

Sortowanie danych można wykonać w bardzo prosty sposób dzięki wykorzystaniu metod z LINQ.

## Metoda OrderBy

Metoda `OrderBy` umożliwia sortowanie danych w kolekcji po jednym lub więcej kluczach sortowania. Przykładowo, aby posortować listę zwierząt w kolejności alfabetycznej, można użyć następującego kodu:

```
List<string> animals = new List<string> { "dog", "cat", "elephant", "lion", "zebra" };

var sortedAnimals = animals
    .OrderBy(animal => animal);

foreach (var animal in sortedAnimals)
{
    Console.WriteLine(animal);
}
```

W powyższym kodzie wykorzystano metodę `OrderBy`, która przyjmuje jako argument wyrażenie lambda, które określa klucz sortowania. W tym przypadku, kluczem sortowania jest każde zwierzę w liście. Następnie, wykorzystano pętlę foreach do iterowania po posortowanej liście i wypisania każdego zwierzęcia na ekranie.

## Metoda OrderByDescending

Aby posortować dane w kolejności malejącej, można użyć metody `OrderByDescending`. Przykładowo, aby posortować listę liczb w kolejności malejącej, można użyć następującego kodu:

```
List<int> numbers = new List<int> { 5, 1, 4, 2, 3 };

var sortedNumbers = numbers.OrderByDescending(number => number);

foreach (var number in sortedNumbers)
{
    Console.WriteLine(number);
}
```

## Sortowanie danych z użyciem wielu kluczy

Metoda `OrderBy` i `OrderByDescending` umożliwiają sortowanie danych po jednym kluczu sortowania. W przypadku, gdy chcemy sortować dane według wielu kluczy, można użyć metod `ThenBy` i `ThenByDescending`. Przykładowo, aby posortować listę osób według wieku, a następnie nazwiska, można użyć następującego kodu:

```
List<Person> people = new List<Person>
{
    new Person { Name = "John", Age = 30 },
    new Person { Name = "Jane", Age = 25 },
    new Person { Name = "Bob", Age = 30 },
    new Person { Name = "Alice", Age = 25 }
};
var sortedPeople = people.OrderBy(person => person.Age)
                            .ThenBy(person => person.Name);

foreach (var person in sortedPeople)
{
    Console.WriteLine($"{person.Name} ({person.Age})");
}
```

W powyższym przykładzie wykorzystano metodę `OrderBy`, aby posortować dane według wieku, a następnie metodę `ThenBy`, aby posortować dane według nazwiska.