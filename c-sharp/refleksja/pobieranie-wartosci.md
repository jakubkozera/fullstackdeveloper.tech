# Pobieranie wartości

Refleksja umożliwia pobieranie wartości właściwości i pól obiektów w czasie wykonywania programu. Można to zrobić przy użyciu metod z klasy System.Reflection, takich jak `PropertyInfo` i `FieldInfo`.

## Przykład - to do, do zmiany na coś co się używa na co dzień

```
using System;
using System.Reflection;

class Program
{
    static void Main(string[] args)
    {
        Person person = new Person { Name = "John Doe" };
        Type type = person.GetType();

        PropertyInfo propertyInfo = type.GetProperty("Name");
        object value = propertyInfo.GetValue(person);

        Console.WriteLine(value);
    }
}

class Person
{
    public string Name { get; set; }
}
```

W powyższym przykładzie, tworzymy obiekt klasy Person i przypisujemy wartość do właściwości "Name". Następnie pobieramy informacje o właściwości "Name" przy użyciu metody GetProperty(). Ostatecznie używamy metody GetValue() do pobrania wartości tej właściwości.