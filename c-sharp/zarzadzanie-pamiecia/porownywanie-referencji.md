# Porównywanie referencji 

Porównywanie referencji w języku C# polega na porównaniu dwóch zmiennych referencyjnych, aby sprawdzić, czy wskazują one na ten sam obiekt w pamięci.

Do porównywania referencji można użyć operatora `==`, który zwraca wartość logiczną `true`, jeśli porównywane zmienne referencyjne wskazują na ten sam obiekt w pamięci.

## Przykład użycia operatora `==` 

Do porównania dwóch zmiennych referencyjnych możemy użyć operatora `==` 

```
string a = "test";
string b = "test";
bool result = (a == b);
Console.WriteLine(result); // Output: true
```

W tym przykładzie zmienne `a` i `b` wskazują na ten sam ciąg znaków `test` w pamięci, więc porównanie zwraca wartość logiczną `true`.

## Inne sposoby na porównywanie referencji

Oprócz porównywania referencji za pomocą operatora `==`, w języku C# można również zastosować inne operatory i metody, które umożliwiają dokładniejsze porównywanie referencji.

1. Operator `!=` to przeciwieństwo do operatora `==`, dlatego zwraca wartość logiczną `true`, jeśli porównywane zmienne referencyjne wskazują na różne obiekty w pamięci.

2. Metoda `Object.Equals()` to metoda, która porównuje dwa obiekty, wykorzystując ich implementację metody `Equals()`. W przypadku porównywania referencji, metoda ta zwraca wartość logiczną `true`, jeśli porównywane zmienne referencyjne wskazują na ten sam obiekt w pamięci.

3. Metoda `Object.GetHashCode()` - metoda ta zwraca unikalny identyfikator haszujący dla obiektu, który można wykorzystać do porównywania referencji. Dwie zmienne referencyjne, które wskazują na ten sam obiekt w pamięci, zawsze zwrócą ten sam identyfikator haszujący.

4. Metoda `Equals()` w klasach dziedziczących - jeśli tworzysz własne klasy, możesz zaimplementować własną wersję metody `Equals()`, która porównuje referencje do obiektów w inny sposób niż domyślna implementacja w klasie bazowej `Object`.

5. Metoda `Object.ReferenceEquals()` to metoda statyczna, która porównuje dwa obiekty, ale tylko w oparciu o ich referencję w pamięci. Zwracaja wartość logiczną `true`, jeśli porównywane zmienne referencyjne wskazują na ten sam obiekt w pamięci.


Warto pamiętać, że porównywanie referencji jest różne od porównywania wartości przechowywanych w obiektach. Przykładowo, dwa ciągi znaków, które mają taką samą zawartość, ale są przechowywane jako różne obiekty w pamięci, nie będą uznane za równe, gdy porównujemy referencje. Dlatego w niektórych przypadkach może być konieczne porównanie wartości obiektów, a nie tylko referencji.