# Przypisywanie wartości

Refleksja w języku C# umożliwia przypisywanie wartości do właściwości i pól obiektów w czasie wykonywania programu. Można to zrobić przy użyciu metod z klasy System.Reflection, takich jak PropertyInfo i FieldInfo.

## Przykład

```
using System;
using System.Reflection;

namespace DynamicSetValue
{
   
    class Program
    {
        static void Main(string[] args)
        {
            Person person = new Person()
            {
                FirstName = "John",
                LastName = "Doe",
                Address = address
            };

            Console.WriteLine("Person:");
            Display(person);

            Console.WriteLine("Insert person property to update");
            var propertyToUpdate = Console.ReadLine();

            Console.WriteLine("Insert value");
            var value = Console.ReadLine();

            SetValue(person, propertyToUpdate, value);

            Console.WriteLine("Person:");
            Display(person);
        }

        static void SetValue<T>(T obj, string propName, string value)
        {
            Type objType = typeof(T);

            var propertyToUpdate = objType.GetProperty(propName);
            if (propertyToUpdate != null)
            {
                propertyToUpdate.SetValue(obj, value);
            }
        }
    }
}
```

W powyższym przykładzie, utworzyliśmy metodę `SetValue`, która dzięki mechnizmowi refleksji, pozwala na przypisywanie wartości do właściwości obiektu, w trakcie trwania programu. 
W metodzie `Main` najpierw stworzyliśmy obiekt klasy `Person` i wyświetliliśmy wartości jego właściwości. Następnie umożliwiliśmy użytkownikowi przypisanie dowolnej wartości do obiektu klasy `Person` z poziomu konsoli, a dzięki użyciu metody `SetValue` dynamicznie zmieniliśmy wartości tych właściwości.