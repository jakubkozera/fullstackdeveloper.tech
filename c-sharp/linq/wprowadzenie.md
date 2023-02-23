# Wprowadzenie do LINQ

LINQ (Language Integrated Query) to technologia zintegrowanego zapytania języka C#, która umożliwia tworzenie zapytań do różnych źródeł danych, takich jak kolekcje, bazy danych, pliki XML i inne, w sposób wygodny i czytelniejszy niż tradycyjne metody zapytań.

LINQ udostępnia szereg metod rozszerzeń dla kolekcji, takich jak `Select`, `Where`, `OrderBy`, `GroupBy` i wiele innych, które umożliwiają łatwe i szybkie filtrowanie, sortowanie i grupowanie danych.

## Przykład

```
List<string> names = new List<string> { "Jakub", "Klaudia", "Ola", "Janusz" };

var namesStartingWithJ = names
    .Where(name => name.StartsWith("J"))
    .OrderBy(name => name);

foreach (var name in namesStartingWithJ)
{
    Console.WriteLine(name);
}
```

W tym przykładzie, LINQ jest używany do filtrowania listy imion i zwraca tylko te, które zaczynają się od litery "J" i sortuje je alfabetycznie. Wynik jest następnie wyświetlany w konsoli za pomocą pętli foreach.

LINQ operując na interfejsie `IEnumerable` będziemy mogli wykorzystać za równo dla kolekcji w pamięci programu, jak i tworzyć w ten sam sposób kwerendy do bazy danych, wykorzystując do tego np. bilbiotekę Entity Framework.