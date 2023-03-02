# Słownik

Słownik to kolekcja danych, która przechowuje pary typu klucz-wartość. Klucz musi być unikalny w ramach słownika, a wartość może być dowolnego typu. Słownik w C# jest implementacją interfejsu `IDictionary<TKey, TValue>`, który definiuje operacje dodawania, usuwania, odczytywania i aktualizacji elementów.

Aby utworzyć nowy słownik, należy użyć klasy Dictionary<TKey, TValue>. Konstruktor klasy Dictionary przyjmuje argument typu `IEqualityComparer`, który określa sposób porównywania kluczy. Jeśli argument nie jest podany, używany jest domyślny komparator. 

Przykładowo, można utworzyć słownik, który przechowuje nazwy i numery telefonów:

```
Dictionary<string, string> phoneBook = new Dictionary<string, string>();
phoneBook.Add("Adam", "123-456-789");
phoneBook.Add("Ewa", "987-654-321");

string adamPhoneNumber = phoneBook["Adam"];
Console.WriteLine(adamPhoneNumber); // wypisze "123-456-789"
```

W powyższym przykładzie utworzyliśmy nowy słownik `phoneBook`, który przechowuje nazwy (klucze) jako stringi i numery telefonów (wartości) również jako wartości tekstowe. Następnie dodaliśmy dwa wpisy do słownika za pomocą metody `Add`. Na koniec, pobraliśmy numer telefonu dla klucza "Adam" używając operatora `[]` i wypisaliśmy jego wartość na konsoli.

## YouTube
https://www.youtube.com/watch?v=ZSMvT037hUo 