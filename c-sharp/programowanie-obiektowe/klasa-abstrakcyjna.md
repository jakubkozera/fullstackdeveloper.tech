# Klasa abstrakcyjna

Klasa abstrakcyjna to specjalny typ klasy, z której nie można utworzyć instancji obiektu, ale może być dziedziczona przez inne klasy. Klasa abstrakcyjna definiuje wspólny zestaw funkcji i właściwości, które są wspólne dla wszystkich klas pochodnych.

Klasy abstrakcyjne są używane, aby zdefiniować abstrakcyjne kontrakty dla innych klas. Klasa abstrakcyjna może zawierać abstrakcyjne metody, które muszą być zaimplementowane przez klasy pochodne. Abstrakcyjne metody są deklarowane bez implementacji.

## Przykład 

```
using System;

abstract class Shape
{
    public abstract decimal Area();
    public abstract decimal Perimeter();
}

class Rectangle : Shape
{
    private decimal width;
    private decimal height;

    public Rectangle(decimal width, decimal height)
    {
        this.width = width;
        this.height = height;
    }

    public override decimal Area()
    {
        return width * height;
    }

    public override decimal Perimeter()
    {
        return 2 * (width + height);
    }
}
```

W powyższym przykładzie, klasa abstrakcyjna `Shape` definiuje abstrakcyjne metody `Area` i `Perimeter`, które muszą być zaimplementowane przez klasy pochodne. Klasa `Rectangle` dziedziczy z klasy `Shape` i zaimplementowała wymagane metody.

Klasy abstrakcyjne są przydatne w programowaniu, ponieważ pozwalają na stworzenie wspólnego kontraktu dla wielu klas, co umożliwia łatwiejszą implementację i utrzymanie kodu.