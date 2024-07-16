# Polimorfizm

Polimorfizm to koncepcja, która pozwala na wykorzystywanie różnych form obiektów jako tego samego typu. W programowaniu obiektowym jest to realizowane poprzez udostępnianie wspólnego interfejsu dla różnych klas, co umożliwia traktowanie ich jako tego samego typu. W efekcie możliwe jest wykorzystanie wielu różnych typów obiektów w jednym miejscu programu, bez konieczności konkretnego określania każdego z nich.

## Zastosowanie

Z polimorfizmu korzystamy ponieważ:

- Łatwiej wprowadzać zmiany w programie, ponieważ nie trzeba modyfikować kodu w wielu miejscach. Jeśli chcemy dodać nowy typ obiektu, możemy to zrobić poprzez dodanie nowej klasy i nadpisanie wymaganych metod. 

- Umożliwia łatwiejsze utrzymanie kodu, ponieważ kod jest bardziej czytelny i zwięzły. W wyniku tego łatwiej jest zrozumieć, jak kod działa i jakie zmiany należy wprowadzić.

- Zapewnia większą elastyczność kodu poprzez zastosowanie abstrakcji i uogólniania. Ułatwia rozwijanie i skalowanie programu.

## Przykład

```
using System;

public class Shape
{
    public virtual void Draw()
    {
        Console.WriteLine("Drawing shape");
    }
}

public class Circle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing circle");
    }
}

public class Square : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing square");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Shape shape1 = new Circle();
        Shape shape2 = new Square();

        shape1.Draw(); 
        shape2.Draw(); 
    }
}
```

W powyższym przykładzie klasa `Shape` jest bazową klasą dla klas `Circle` i `Square`. Klasa `Circle` i `Square` dziedziczą po klasie `Shape` i nadpisują metodę `Draw()`. W funkcji `Main()` tworzone są obiekty `Circle` i `Square`, które są rzutowane na obiekty typu `Shape`. W wyniku tego, przy wywołaniu metody `Draw()` dla tych obiektów, wywoływana jest właściwa implementacja zdefiniowana w klasach `Circle` i `Square`, mimo że są one traktowane jako obiekty typu `Shape`.

## YouTube

*https://www.youtube.com/watch?v=oWDPGWIMHh0*