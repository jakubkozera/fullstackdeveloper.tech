# Przypisywanie wartości

Refleksja w języku C# umożliwia przypisywanie wartości do właściwości i pól obiektów w czasie wykonywania programu. Można to zrobić przy użyciu metod z klasy System.Reflection, takich jak PropertyInfo i FieldInfo.

## Przykład -  to do, do zmiany na coś co się używa na co dzień

```
using System;
using System.Reflection;

class Program
{
    static void Main(string[] args)
    {
        Person person = new Person();
        Type type = person.GetType();

        PropertyInfo propertyInfo = type.GetProperty("Name");
        propertyInfo.SetValue(person, "John Doe");

        Console.WriteLine(person.Name);
    }
}

class Person
{
    public string Name { get; set; }
}
```
W powyższym przykładzie, tworzymy obiekt klasy Person i pobieramy informacje o właściwości "Name" przy użyciu metody GetProperty(). Następnie używamy metody SetValue() do przypisania wartości "John Doe" do właściwości "Name".
