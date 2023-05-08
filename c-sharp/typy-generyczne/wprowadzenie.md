# Typy generyczne

Typy generyczne to mechanizm, który pozwala na tworzenie klas, struktur, interfejsów i metod, które mogą operować na różnych typach danych. Umożliwiają one programistom tworzenie kodu, który jest bardziej elastyczny, ponieważ można używać jednej implementacji kodu dla wielu typów danych.

Oto kilka przykładów typów generycznych w C#:

1. Lista generyczna (`List<T>`) - klasa, która reprezentuje listę elementów o typie `T`. Może przechowywać elementy dowolnego typu.

2. Słownik generyczny (`Dictionary<TKey, TValue>`) - klasa, która reprezentuje słownik, gdzie klucz ma typ `TKey`, a wartość ma typ `TValue`.

3. Kolejka generyczna (`Queue<T>`) - klasa, która reprezentuje kolejkę elementów o typie `T`.

4. Stos generyczny (`Stack<T>`) - klasa, która reprezentuje stos elementów o typie `T`.


## Definicja typów generycznych

Aby zdefiniować własny typ generyczny, będziemy musieli zdefiniować ten typ w specjalnym sytaxie, który wygląda następująco: class `SomeGenericClass<T>`, gdzie tak naprawdę `T`, jest dowolną nazwą typu generycznego i może to być cokolwiek.

W ramach definicji takiej klasy, typ `T` będzię dostępny i możliwy do definicji typów parametrów metod, pól, czy zwracanych wartości.

```
public class MyGenericClass<T>
{
    private T _data;

    public MyGenericClass(T data)
    {
        _data = data;
    }

    public T GetData()
    {
        return _data;
    }
}
```

W tym przykładzie zdefiniowaliśmy ogólną klasę o nazwie `MyGenericClass`, która przyjmuje parametr typu `T`. Zdefiniowaliśmy prywatne pole `_data` typu `T` oraz konstruktor, który pobiera parametr typu `T` i przypisuje go do `_data`.

Zdefiniowaliśmy również publiczną metodę `GetData`, która zwraca wartość `_data`.

Korzystając z tej generycznej (ogólnej) klasy, możemy tworzyć instancje, które przechowują dowolne typy danych, na przykład:

```
var myStringClass = new MyGenericClass<string>("Hello, world!");
string myString = myStringClass.GetData(); // returns "Hello, world!"

var myIntClass = new MyGenericClass<int>(42);
int myInt = myIntClass.GetData(); // returns 42
```
Jak widać, możemy tworzyć instancje `MyGenericClass`, które przechowują `string`, `int` lub dowolny inny typ, określając odpowiedni parametr typu podczas tworzenia instancji.

## YouTube

*https://www.youtube.com/watch?v=6vfC4AmPA4M*