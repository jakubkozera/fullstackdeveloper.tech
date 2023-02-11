# Dziedziczenie

Dziedziczenie to mechanizm programowania obiektowego, który pozwala na tworzenie nowych klas na bazie już istniejących. Klasa pochodna może dziedziczyć właściwości i metody klasy bazowej. Dzięki temu możliwe jest dziedziczenie zachowania i stanu z klasy bazowej do klasy pochodnej, co umożliwia unikanie powielania kodu i zwiększenie czytelności kodu. Dziedziczenie umożliwia też tworzenie hierarchii klas, co pozwala na łatwe rozszerzanie i modyfikowanie istniejącego kodu w miarę rozwoju aplikacji.

## Przykład

```
using System;

class Animal
{
    public string Name { get; set; }

    public void Eat()
    {
        Console.WriteLine("Animal is eating");
    }
}

class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Dog is barking");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Dog dog = new Dog();
        dog.Name = "Reksio";
        dog.Eat();
        dog.Bark();

        Console.ReadLine();
    }
}
```
W powyższym przykładzie, mamy klasę `Aniamal` z właściwością `Name` u metodą `Eat()`. Klasa `Dog` dziedziczy po klasie `Animal` i dodatkowo posiada swoją metodę `Bark()`. Dzięki temu klasa `Dog` automatycznie dostaje dostęp do właściwości `Name` oraz do metody `Eat()` zdefiniowanej w klasie `Aniaml`.

## Ograniczenia dziedziczenia

W języku C# istnieją kilka ograniczeń związanych z mechanizmem dziedziczenia:

- Jedna klasa może dziedziczyć tylko po jednej klasie nadrzędnej. W językach, takich jak C++ i Java, jest to możliwe dzięki wielodziedziczeniu. W C#, w celu uzyskania wielodziedziczenia, należy użyć interfejsów.

- Klasa dziedzicząca nie może zmienić dostępności metod nadrzędnej. Na przykład, jeśli metoda w klasie nadrzędnej jest oznaczona jako protected, to w klasie dziedziczącej nie można jej oznaczyć jako public.

- Klasa dziedzicząca nie może nadpisać konstruktora nadrzędnej. Konstruktor jest jedyną metodą, która nie może być nadpisana.

- Klasa abstrakcyjna nie może być instancjonowana. Można jedynie tworzyć obiekty klas pochodnych, które ją implementują.