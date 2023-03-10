# Generyczne parametry

Generyczne parametry umożliwiają tworzenie klas, metod lub interfejsów, które przyjmują typy danych jako parametry. 

Aby utworzyć generyczny parametr, musimy użyć symbolu `<typ>`. Możemy nazwać ten parametr dowolnie, ale zazwyczaj stosuje się konwencję `T` lub `K`. Następnie możemy użyć tego parametru w kodzie, tak jakby był to zwykły typ. Przykładem klasy z generycznym parametrem może być klasa `List<T>`, która reprezentuje listę elementów dowolnego typu:

```
public class List<T>
{
    private T[] items;

    public List()
    {
        items = new T[0];
    }

    public void Add(T item)
    {
        Array.Resize(ref items, items.Length + 1);
        items[items.Length - 1] = item;
    }

    public T this[int index]
    {
        get { return items[index]; }
        set { items[index] = value; }
    }

    public int Count
    {
        get { return items.Length; }
    }
}
```

W tym przykładzie klasa List przyjmuje typ generyczny `T`, który reprezentuje typ elementów znajdujących się na liście. W klasie definiujemy metodę `Add`, która dodaje element do listy, index, który umożliwia dostęp do elementów listy za pomocą indeksu, a także właściwość `Count`, która zwraca liczbę elementów na liście.

Aby utworzyć instancję klasy `List` z konkretnym typem elementów, musimy przekazać typ jako argument generycznego parametru `T`. Na przykład, jeśli chcemy utworzyć listę liczb całkowitych, możemy napisać:

```
List<int> list = new List<int>();
```

Generyczne parametry w C# pozwalają na pisanie bardziej ogólnych i elastycznych rozwiązań, które mogą działać z różnymi typami danych. Dzięki temu mechanizmowi unikamy konieczności pisania osobnego kodu dla każdego typu, co zwiększa wydajność i ułatwia utrzymanie kodu.