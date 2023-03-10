# Metody generyczne

Metody generyczne to metody, które mogą operować na różnych typach danych. W definicji metody używa się typu generycznego zamiast określonego typu danych.

## Przykład

```
public static T Find<T>(T[] array, T value)
{
    foreach (T element in array)
    {
        if (element.Equals(value))
        {
            return element;
        }
    }

    return default(T);
}
```

W tym przykładzie metoda generyczna `Find<T>` operuje na tablicy elementów typu `T` i zwraca pierwszy element w tablicy, który ma wartość równą wartości przekazanej jako drugi argument. Metoda generyczna umożliwia użycie tej samej metody dla różnych typów danych.