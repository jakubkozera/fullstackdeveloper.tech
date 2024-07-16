# Konstruktor

Konstruktor jest to specjalna metoda, która jest wywoływana automatycznie, gdy obiekt jest tworzony za pomocą operatora `new`. Konstruktor służy do inicjalizacji obiektu, a jego zadaniem jest zapewnienie, że obiekt jest w prawidłowym stanie zaraz po jego utworzeniu. Każda klasa może mieć jeden lub więcej konstruktorów, które różnią się między sobą listą argumentów. Jeśli nie zdefiniujemy żadnego konstruktora w klasie, to kompilator automatycznie dodaje konstruktor bezargumentowy.

## Przykład konstruktora bezparametrowego

```
public class Employee
{
    public Employee()
    {
    }
}
```

## Przykład konstruktora z parametrami

```
public class Car
{
    public string Make { get; set; }
    public string Model { get; set; }
    public int Year { get; set; }

    public Car(string make, string model, int year)
    {
        Make = make;
        Model = model;
        Year = year;
    }
}
```

Aby stworzyć instancję klasy `Car` należy podać odpowiednie wartości parametrów do konstruktora:

```
Car myCar = new Car("Mazda", "CX-5", 2020);
```

## Konstruktory bazowe
Konstruktory bazowe pozwalają na wywołanie konstruktora z klasy bazowej w klasie pochodnej. Jest to przydatne, gdy chcemy użyć konstruktora z klasy bazowej do inicjalizacji części obiektu, a następnie dodać dodatkowe inicjalizacje w klasie pochodnej.

Aby wywołać konstruktor bazowy, należy użyć słowa kluczowego base w ciele konstruktora w klasie pochodnej.

### Przykład konstruktora bazowego
```
public class Vehicle
{
    public string Make { get; set; }
    public string Model { get; set; }

    public Vehicle(string make, string model)
    {
        Make = make;
        Model = model;
    }
}

public class Car : Vehicle
{
    public int Year { get; set; }

    public Car(string make, string model, int year) : base(make, model)
    {
        Year = year;
    }
}
```

W powyższym przykładzie klasa `Vehicle` zawiera konstruktor z parametrami, który jest wywoływany przez konstruktor bazowy w klasie `Car`.

## Konstruktor prywatny

Konstruktor prywatny jest to konstruktor, który jest oznaczony modyfikatorem `private` i nie może być wywoływany bezpośrednio przez inne klasy lub obiekty. Ma on zastosowanie wtedy, gdy chcemy ograniczyć możliwość tworzenia instancji klasy tylko do kodu wewnątrz tej klasy lub jej podklas.

Przykład klasy z prywatnym konstruktorem:

```
public class Singleton
{
    private static Singleton instance;

    private Singleton()
    {
    }

    public static Singleton Instance
    {
        get
        {
            if (instance == null)
            {
                instance = new Singleton();
            }
            return instance;
        }
    }
}
```

W tym przykładzie, klasa `Singleton` jest wzorcem projektowym, który pozwala na utworzenie tylko jednej instancji tej klasy. Konstruktor jest prywatny, aby uniemożliwić tworzenie instancji tej klasy bezpośrednio przez inne klasy lub obiekty. Instancja jest tworzona tylko przez wywołanie właściwości `Instance`, która sprawdza, czy instancja już istnieje, a jeśli nie, to ją tworzy.


## YouTube

*https://www.youtube.com/watch?v=DG9eaBBa5u8*