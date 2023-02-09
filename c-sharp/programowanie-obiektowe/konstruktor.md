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