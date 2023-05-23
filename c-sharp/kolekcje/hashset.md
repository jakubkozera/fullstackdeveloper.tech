# HashSet

HashSet w C# jest strukturą danych, która reprezentuje zbiór unikalnych elementów. Oznacza to, że w HashSet nie może istnieć duplikatów wartości. Jest często używany, gdy potrzebujemy przechowywać kolekcję elementów, ale nie jest istotna kolejność ich przechowywania, a jednocześnie chcemy mieć pewność, że każdy element występuje tylko raz.

HashSet jest implementacją interfejsu ISet<T> w języku C#. Oznacza to, że dostarcza wszystkie operacje zdefiniowane przez ten interfejs, takie jak dodawanie elementów, usuwanie elementów, sprawdzanie, czy dany element istnieje w zbiorze, operacje na zbiorach (unia, przecięcie, różnica) oraz wiele innych.

Przykład użycia HashSet w C#:

```csharp
HashSet<string> imiona = new HashSet<string>();

imiona.Add("Anna");
imiona.Add("Jan");
imiona.Add("Anna"); // duplikat zostanie zignorowany

Console.WriteLine(imiona.Count); // Wypisze: 2

imiona.Remove("Jan");

Console.WriteLine(imiona.Contains("Jan")); // Wypisze: False

foreach (string imie in imiona)
{
    Console.WriteLine(imie);
}
```

W powyższym przykładzie tworzony jest HashSet przechowujący imiona. Dodawane są imiona "Anna", "Jan" i ponownie "Anna". Jednak HashSet ignoruje duplikaty, więc końcowa liczba elementów wynosi 2. Następnie usuwane jest imię "Jan". Sprawdzane jest, czy "Jan" nadal istnieje w zbiorze (false). Na koniec iterujemy przez wszystkie imiona i wypisujemy je na konsoli.

HashSet oferuje również różne metody i właściwości, które ułatwiają pracę z nim, takie jak Clear() (usuwanie wszystkich elementów), UnionWith() (unia dwóch zbiorów), IntersectWith() (przecięcie dwóch zbiorów), IsSubsetOf() (sprawdzenie, czy zbiór jest podzbiorem innego zbioru) i wiele innych.

## HashSet, a słownik

HashSet i słownik (Dictionary) są dwoma różnymi strukturami danych w języku C#, choć obie są używane do przechowywania kolekcji elementów. Oto kilka głównych różnic między nimi:

1. Unikalność kluczy: W słowniku, każdy klucz musi być unikalny i jednoznacznie identyfikować wartość. W HashSet natomiast, nie ma pojęcia kluczy i przechowuje tylko unikalne wartości.

2. Pary klucz-wartość: Słownik składa się z par klucz-wartość, gdzie klucz służy do identyfikacji wartości. W HashSet natomiast, przechowuje się tylko wartości.

3. Indeksowanie: Słownik pozwala na indeksowanie, czyli otrzymywanie wartości na podstawie klucza. W HashSet nie można indeksować, ponieważ nie ma kluczy.

4. Wyszukiwanie: Wyszukiwanie w słowniku jest bardziej efektywne i szybsze niż w HashSet, ponieważ odbywa się na podstawie kluczy. HashSet nie ma tych korzyści i wyszukiwanie jest bardziej zbliżone do listy lub tablicy.

5. Funkcjonalność: Słownik oferuje bardziej rozbudowane metody i właściwości, takie jak TryGetValue() (sprawdzenie, czy istnieje klucz i otrzymanie wartości), ContainsKey() (sprawdzenie, czy istnieje klucz) oraz wiele innych. HashSet skupia się na operacjach typowych dla zbiorów, takich jak dodawanie, usuwanie, sprawdzanie przynależności, operacje na zbiorach i inne.

Ogólnie rzecz biorąc, jeśli potrzebujesz przechowywać unikalne wartości bez przyporządkowanych kluczy, to HashSet jest dobrym wyborem. Jeśli natomiast potrzebujesz przechowywać pary klucz-wartość, gdzie klucz jednoznacznie identyfikuje wartość, to słownik (Dictionary) jest bardziej odpowiedni. Wybór między nimi zależy od konkretnego przypadku użycia i wymagań aplikacji.