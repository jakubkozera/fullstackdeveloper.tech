# Słownik

Słownik to kolekcja danych, która przechowuje pary typu klucz-wartość. Klucz musi być unikalny w ramach słownika, a wartość może być dowolnego typu. Słownik w C# jest implementacją interfejsu `IDictionary<TKey, TValue>`, który definiuje operacje dodawania, usuwania, odczytywania i aktualizacji elementów.


## Unikalność kluczy w słowniku

W słowniku (dictionary) klucze muszą być unikalne, co oznacza, że ​​nie mogą istnieć dwa elementy o tym samym kluczu. Jeśli spróbujemy dodać element do słownika z kluczem, który już istnieje, to wartość przypisana do tego klucza zostanie zastąpiona nową wartością.

W przypadku, gdy próbujemy dodać do słownika element z kluczem, który już istnieje, a wartość, która ma być przypisana do tego klucza jest różna, nowa wartość zastąpi starą. Dlatego ważne jest, aby upewnić się, że klucze są unikalne, aby uniknąć niepożądanych nadpisywań.

W słownikach klucze mogą być dowolnego typu, pod warunkiem, że są one unikalne i implementują interfejs `IEquatable<T>` lub implementują metodę `Equals()`. Dlatego klucze mogą być typami wartościowymi (np. `int`, `double`, `DateTime`) lub typami referencyjnymi (np. `string`, `List<T>`, `MyClass`).

Wartości w słowniku nie muszą być unikalne i mogą być dowolnego typu, włączając w to również typy wartościowe i referencyjne.

## Inicjalizacja słownika



Aby utworzyć nowy słownik, należy użyć klasy `Dictionary<TKey, TValue>`. 

Przykładowo, można utworzyć słownik, który przechowuje nazwy i numery telefonów:

```
Dictionary<string, string> phoneBook = new Dictionary<string, string>();
phoneBook.Add("Adam", "123-456-789");
phoneBook.Add("Ewa", "987-654-321");

string adamPhoneNumber = phoneBook["Adam"];
Console.WriteLine(adamPhoneNumber); // wypisze "123-456-789"
```

W powyższym przykładzie utworzyliśmy nowy słownik `phoneBook`, który przechowuje nazwy (klucze) jako stringi i numery telefonów (wartości) również jako wartości tekstowe. Następnie dodaliśmy dwa wpisy do słownika za pomocą metody `Add`. Na koniec, pobraliśmy numer telefonu dla klucza "Adam" używając operatora `[]` i wypisaliśmy jego wartość na konsoli.

Ten sam kawałek kodu, moglibyśmy zaimplementować, wykorzystując inicjalizację słownika, zamiast wywoływać dwa razy metodę `Add`.

```
Dictionary<string, string> phoneBook = new Dictionary<string, string>()
{
    {"Adam", "123-456-789"},
    {"Ewa", "987-654-321"}
};

string adamPhoneNumber = phoneBook["Adam"];
Console.WriteLine(adamPhoneNumber); // wypisze "123-456-789"
```

Po takiej inicjalizacji, nadal możemy wykorzystać metodę `Add`, aby dodawać nowe elementy do słownika:

```
phoneBook.Add("Jan", "555-123-456");
```
Możemy też zmienić numer telefonu dla istniejącego kontaktu, używając indeksera:

```
phoneBook["Adam"] = "111-222-333";
```

## Pobieranie wartości ze słownika

W C# można pobierać wartości ze słownika (dictionary) na kilka sposobów:

1. Korzystając z operatora indeksowania `[]` i klucza, np. `var value = dictionary[key];`
2. Korzystając z metody `TryGetValue()` i klucza, np. `bool success = dictionary.TryGetValue(key, out var value);`
3. Korzystając z metody `ContainsKey()` i operatora indeksowania `[]`, np. `if (dictionary.ContainsKey(key)) { var value = dictionary[key]; }`
4. Korzystając z `metody ContainsKey()` i metody `TryGetValue()`, np. `if (dictionary.ContainsKey(key)) { bool success = dictionary.TryGetValue(key, out var value); }`


Różnice między tymi sposobami obejmują:

1. Operator indeksowania `[]` zwróci wyjątek `KeyNotFoundException`, jeśli klucz nie istnieje w słowniku, natomiast metoda `TryGetValue()` zwróci `false` i ustawia wartość na domyślną, jeśli klucz nie istnieje w słowniku.
2. Metoda `TryGetValue()` zwróci wartość, jeśli klucz istnieje w słowniku, w przeciwnym razie ustawia wartość na domyślną i zwraca `false`.
3. Metoda `ContainsKey()` zwraca wartość logiczną, która określa, czy klucz istnieje w słowniku, a operator indeksowania `[]` zwraca wartość klucza lub wyjątek `KeyNotFoundException`, jeśli klucz nie istnieje w słowniku.
4. Metoda `ContainsKey()` zwraca wartość logiczną, która określa, czy klucz istnieje w słowniku, a metoda `TryGetValue()` zwraca wartość, jeśli klucz istnieje w słowniku, w przeciwnym razie ustawia wartość na domyślną i zwraca `false`.


W przypadku, gdy nie jesteśmy pewni, czy dany klucz istnieje w słowniku, lepiej użyć metody `TryGetValue()`, aby uniknąć wyjątków.



 

## YouTube
*https://www.youtube.com/watch?v=ZSMvT037hUo* 