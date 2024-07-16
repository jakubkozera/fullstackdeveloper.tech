# Ograniczenia generyczne

Jest to mechanizm, który umożliwia narzucenie ograniczeń na typy generyczne używane w klasach, metodach lub interfejsach. Ograniczenia te pozwalają na bardziej precyzyjne określenie typów, które mogą być używane w kodzie i pozwalają na wykluczenie typów, które nie spełniają określonych wymagań.

## Przykłady 

1. Ograniczenie klasy bazowej - pozwala na określenie, że typ generyczny musi dziedziczyć po konkretnej klasie.

    ```
    public class MyClass<T> where T : MyBaseClass
    {
        
    }
    ```

2. Ograniczenie interfejsu - pozwala na określenie, że typ generyczny musi implementować określony interfejs. 
    ```
    public class MyClass<T> where T : IMyInterface
    {
        
    }
    ```

3. Ograniczenie konstruktora - pozwala na określenie, że typ generyczny musi mieć publiczny konstruktor bezparametrowy lub z określonymi parametrami. 
    ```
    public class MyClass<T> where T : new()
    {
        
    }
    ```

4. Ograniczenie typu generycznego do typów, które posiadają określoną metodę lub właściwość.
    ```
    public class MyClass<T> where T : IComparable<T>
    {
        public void Sort(T[] array)
        {
            Array.Sort(array);
        }
    }
    ```
    W tym przykładzie klasa `MyClass` przyjmuje typ generyczny `T`, który musi implementować interfejs `IComparable<T>`, co oznacza, że typ musi mieć metodę `CompareTo`. W klasie `MyClass` definiujemy metodę `Sort`, która sortuje tablicę elementów typu `T` używając metody `CompareTo`. Dzięki temu ograniczeniu możemy mieć pewność, że typ `T` posiada metodę `CompareTo` i kod nie zostanie wykonany dla typów, które nie mają tej metody.

Ograniczenia generyczne pozwalają na lepszą kontrolę nad typami danych używanymi w kodzie i umożliwiają na uniknięcie błędów wynikających z nieprawidłowego typu danych.

## YouTube

*https://www.youtube.com/watch?v=6vfC4AmPA4M&t=1579s*