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


## Porównanie po wartościach typów referencyjnych

Wszystkie powyższe metody operują na referencjach konkretnych obiektów, jednak często będziemy musieli zaimplementować mechanizm porównania dwóch obiektów typu referencyjnego po konkretnych wartościach z danego obiektu.

W tym celu będziemy musieli napisać własną implementacje metody `Equals`.

Oto przykładowa implementacja klasy w C#, która zawiera pola `Name` i `Age`, konstruktor i nadpisaną metodę `Equals`:

```
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    public override bool Equals(object obj)
    {
        if (obj == null || GetType() != obj.GetType())
            return false;

        Person otherPerson = (Person)obj;
        return (Name == otherPerson.Name) && (Age == otherPerson.Age);
    }
}
```

W powyższej klasie `Equals` została nadpisana w celu porównania dwóch obiektów klasy Person na podstawie ich pól `Name` i `Age`. Metoda ta porównuje typy obiektów oraz zawartość ich pól i zwraca wartość true jeśli obiekty są sobie równe.

Przykład użycia metody Equals w celu porównania dwóch obiektów klasy Person:
```
Person person1 = new Person("John", 30);
Person person2 = new Person("John", 30);

bool areEqual = person1.Equals(person2);

Console.WriteLine("Person1 and Person2 are equal: " + areEqual); // Output: Person1 and Person2 are equal: True
```


W powyższym przykładzie tworzymy dwie instancje klasy `Person` o takich samych wartościach pól `Name` i `Age`. Następnie wywołujemy metodę `Equals` na obiekcie `person1`, przekazując jako argument obiekt `person2`. Metoda ta porównuje obiekty i zwraca wartość `true`, co oznacza, że obiekty są sobie równe.

## Operator `==` a porównywanie obiektów

Operator `==` w C# jest domyślnie przeciążony dla typów referencyjnych w taki sposób, że porównuje on referencje do obiektów, a nie ich zawartość. W związku z tym, jeśli chcemy porównać dwa obiekty klasy `Person` na podstawie ich zawartości, musimy przeciążyć ten operator w naszej klasie.

Oto przykładowa implementacja przeciążenia operatora `==` w klasie `Person`:

```
public static bool operator ==(Person person1, Person person2)
{
    if (ReferenceEquals(person1, person2))
    {
        return true;
    }

    if ((person1 is null) || (person2 is null))
    {
        return false;
    }

    return person1.Equals(person2);
}

public static bool operator !=(Person person1, Person person2)
{
    return !(person1 == person2);
}
```

W powyższym kodzie operator `==` został przeciążony w taki sposób, że najpierw sprawdza on, czy obiekt `person1` i `person2` są identyczne, tzn. czy mają te same referencje. Jeśli tak, to zwraca true. Następnie sprawdza, czy któryś z obiektów jest wartością `null` i jeśli tak, to zwraca `false`. W przeciwnym razie wywołuje metodę `Equals` na obiekcie person1, przekazując jako argument obiekt `person2`.

Dzięki przeciążeniu operatora `==` możemy teraz porównać dwa obiekty klasy Person za pomocą tego operatora, tak jak w poniższym przykładzie:

```
Person person1 = new Person("John", 30);
Person person2 = new Person("John", 30);

bool areEqual = person1 == person2;

Console.WriteLine("Person1 and Person2 are equal: " + areEqual); // Output: Person1 and Person2 are equal: True
```

W tym przykładzie porównujemy obiekty `person1` i `person2` za pomocą operatora `==`. Dzięki przeciążeniu tego operatora w klasie `Person`, porównanie to porównuje zawartość pól `Name` i `Age` tych obiektów, a nie ich referencje, więc zwraca wartość true, co oznacza, że obiekty są sobie równe.