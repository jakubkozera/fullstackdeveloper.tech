# Abstrakcja

Abstrakcja jest jednym z kluczowych pojęć w programowaniu obiektowym i oznacza proces polegający na oddzieleniu nieistotnych szczegółów implementacji od ważnych koncepcji i relacji. 

Polega ona na utworzeniu abstrakcyjnego pojęcia, które opisuje grupę obiektów i umożliwia traktowanie ich jako jednolitej jednostki, niezależnie od ich konkretnej implementacji. Abstakcja jest realizowana w c# za pomocą klas abstrakcyjnych i interfejsów, które definiują wspólne cechy i zachowania dla grup obiektów.

Głównym celem abstrakcji jest umożliwienie skupienia się na najważniejszych cechach obiektów i oddzielenie ich od szczegółów implementacji. To pozwala na zwiększenie czytelności i przejrzystości kodu oraz umożliwia łatwe utrzymanie i rozwijanie aplikacji.

## Implementacja przy pomocy klasy abstrakcyjnej

Poniżej znajduje się przykład klasy abstrakcyjnej i dwóch klas dziedziczących po niej w języku C#:


```
public abstract class Shape
{
    public abstract double Area();
}

public class Rectangle : Shape
{
    double length;
    double width;

    public Rectangle(double l, double w)
    {
        length = l;
        width = w;
    }

    public override double Area()
    {
        return length * width;
    }
}

public class Circle : Shape
{
    double radius;

    public Circle(double r)
    {
        radius = r;
    }

    public override double Area()
    {
        return Math.PI * radius * radius;
    }
}
```

W powyższym przykładzie, klasa `Shape` jest klasą abstrakcyjną i zawiera metodę abstrakcyjną `Area()`. Klasy `Rectangle` i `Circle` dziedziczą po `Shape` i nadpisują metodę `Area()`, aby zaimplementować obliczanie powierzchni dla odpowiednich kształtów. W ten sposób możemy użyć abstrakcji do zdefiniowania wspólnego interfejsu dla różnych kształtów, a następnie stworzyć konkretne implementacje dla konkretnych kształtów.

Oto przykład wykorzystania powyższego mechanizmu do obliczania powierzchni kilku różnych kształtów:

```
class Program
{
    static void Main(string[] args)
    {
        Shape[] shapes = new Shape[3];
        shapes[0] = new Rectangle(10, 20);
        shapes[1] = new Circle(5);
        shapes[2] = new Rectangle(15, 25);

        foreach (Shape shape in shapes)
        {
            Console.WriteLine("Powierzchnia: " + shape.Area());
        }

        Console.ReadKey();
    }
}
```

W powyższym przykładzie tworzymy tablicę obiektów typu `Shape`, która zawiera trzy różne kształty - prostokąt o wymiarach 10x20, okrąg o promieniu 5 i prostokąt o wymiarach 15x25. Następnie, korzystając z pętli `foreach`, wywołujemy metodę `Area()` dla każdego z tych kształtów i wyświetlamy wynik. Dzięki temu, że wszystkie kształty są traktowane jako obiekty tego samego typu (czyli `Shape`), możemy je przetwarzać w sposób jednolity, niezależnie od ich konkretnej implementacji.