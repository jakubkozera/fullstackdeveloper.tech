# Pobieranie wartości

Refleksja umożliwia pobieranie wartości właściwości i pól obiektów dynamicznie czyli w czasie wykonywania programu. Można to zrobić przy użyciu metod z klasy `System.Reflection`, takich jak `PropertyInfo`, która zapewnia dostęp do metadanych właściwości czy `FieldInfo`, która pozwala na dostęp do metadanych pól.

## Przykład

```
using System;
using System.Reflection;

namespace FirstProject
{
   
    class Program
    {
        static void Display(object obj)
        {
            Type objType = obj.GetType();
            var properties = objType.GetProperties();

            foreach (var property in properties)
            {
                var propValue = property.GetValue(obj);

                var propType = propValue.GetType();

                if (propType.IsPrimitive || propType == typeof(string))
                {
                    Console.WriteLine($"{property.Name}: {propValue}");

                }
            }
        }


        static void Main(string[] args)
        {
            Address address = new Address()
            {
                City = "Krakow",
                PostalCode = "31-556",
                Street = "Grodzka 5"
            };

            Person person = new Person()
            {
                FirstName = "John",
                LastName = "Doe",
                Address = address
            };
            Console.WriteLine("Person:");
            Display(person);
            Console.WriteLine("Address:");
            Display(address);

        }
    }
}

```

W powyższym przykładzie, stworzyliśmy metodę `Display`, która niezależnie od przyjmowanego typu umożliwia odczytywanie właściwości z klasy i w odpowiedni sposób wypisuje je do konsoli. Korzystając z mechanizmu refleksji byliśmy w stanie odnieść się do każdej właściwości danego typu przy użyciu metody `GetProperties()`, po czym pobraliśmy wartość dla każdej z tych właściwości, dzięki metodzie `GetValue()`. Dodatkowo sprawdziliśmy czy właściwość jest typem prymitywnym lub stringiem, a jeżeli tak, to wypisaliśmy jej wartość do konsoli. 
