# Const i readonly

Słowo kluczowe `const` służy do deklarowania stałej wartości, która nie może być zmieniona w trakcie działania programu. Słowo kluczowe `readonly` natomiast służy do deklarowania wartości, która może być ustawiona tylko raz, podczas inicjalizacji lub w konstruktorze, i nie może być zmieniona później.

```
public class MyClass
{
    public const int MyConst = 10; // stała wartość, której nie można zmienić

    public readonly int MyReadonly; // wartość, która może być ustawiona tylko raz

    public MyClass(int value)
    {
        MyReadonly = value; // można ją ustawić w konstruktorze
    }

    public void ChangeValues()
    {
        // MyConst = 20; // spowoduje błąd kompilacji
        // MyReadonly = 30; // spowoduje błąd kompilacji
    }
}
```

W tym przykładzie `MyConst` to stała wartość, która jest ustawiona na 10 i nie może być zmieniona w żadnym miejscu w programie. Z kolei `MyReadonly` to wartość typu `readonly`, która może być ustawiona w konstruktorze, ale nie może być zmieniona później.

## Const 

Użycie `const` gwarantuje, że wartość zmiennej nie będzie modyfikowana w trakcie działania programu, co może przyczynić się do zwiększenia czytelności kodu oraz uniknięcia błędów. Jego użycie jest zalecane w następujących sytuacjach:

1. Stałe matematyczne - wartości matematyczne, takie jak np. liczba Pi, bądź stałe fizyczne, które mają zawsze tę samą wartość i nie powinny ulec zmianie.
```
public const double Pi = 3.14159265358979323846;
```
2. Stałe tekstowe - wartości tekstowe, takie jak np. stałe nazwy plików, ciągi znaków, które powtarzają się w kodzie i nie powinny ulec zmianie.
```
public const string ProductOwner = "Product Owner";
```
3. Stałe enumeracje - wartości wyliczeniowe, które mają zawsze tę samą wartość i nie powinny ulec zmianie.
```
public enum DaysOfWeek
{
    Monday = 1,
    Tuesday = 2,
    Wednesday = 3,
    Thursday = 4,
    Friday = 5,
    Saturday = 6,
    Sunday = 7
}

public const DaysOfWeek FirstDayOfWeek = DaysOfWeek.Monday;
```

Należy zauważyć, że wartości `const` są domyślnie `static`, co oznacza, że są one przypisane do klasy, a nie do konkretnej instancji tej klasy.

Przykładowo, jeśli mamy klasę `MyClass` z polem `MyConst` zadeklarowanym jako `const`, to odwołując się do niego, możemy napisać `MyClass.MyConst`. Nie ma potrzeby tworzenia instancji klasy `MyClass`, aby uzyskać dostęp do wartości `MyConst`, ponieważ ta wartość jest dostępna dla całej klasy.

## Readonly

Zastosowanie `readonly` pozwala na zainicjalizowanie zmiennej tylko raz, zwykle podczas tworzenia obiektu klasy, oraz dalsze operowanie na tej wartości bez możliwości jej zmiany. 

Typowe scenariusze użycia:

1. Pola inicjowane w konstruktorze - pola klasy, które są inicjowane tylko raz w konstruktorze i powinny być tylko do odczytu.
```
public class MyClass
{
    private readonly int _myInt;

    public MyClass(int myInt)
    {
        _myInt = myInt;
    }

    public int GetMyInt()
    {
        return _myInt;
    }
}
```
2. Pola zależne od innych pól - pola klasy, które są inicjowane tylko raz na podstawie innych pól i powinny być tylko do odczytu.
```
public class Rectangle
{
    private readonly int _width;
    private readonly int _height;
    private readonly int _area;

    public Rectangle(int width, int height)
    {
        _width = width;
        _height = height;
        _area = _width * _height;
    }

    public int GetArea()
    {
        return _area;
    }
}
```
3. Pola stałe obliczane w czasie wykonania - pola klasy, które są obliczane tylko raz w czasie wykonania programu i powinny być tylko do odczytu.
```
public class MathFunctions
{
    private static readonly double _pi;

    static MathFunctions()
    {
        _pi = Math.PI;
    }

    public static double GetPi()
    {
        return _pi;
    }
}
```

Wartości typu `readonly` są przypisane do konkretnej instancji klasy, a nie do całej klasy. Oznacza to, że każda instancja klasy może mieć swoją własną wartość `readonly`. Nie można się do nich odwoływać bezpośrednio poprzez klasę, ponieważ wartość ta jest związana z konkretną instancją.

Przykładowo, jeśli mamy klasę `MyClass` z polem `MyReadonly` zadeklarowanym jako `readonly`, to musimy utworzyć instancję klasy `MyClass`, aby uzyskać dostęp do wartości `MyReadonly`. Możemy uzyskać dostęp do tej wartości za pomocą obiektu klasy, np. `myClassInstance.MyReadonly`, gdzie `myClassInstance` to instancja klasy `MyClass`.

