# Interfejs 

Interfejs to abstrakcyjny typ danych, który definiuje, jakie funkcje powinny być dostępne dla danego typu obiektu. Interfejs jest narzędziem do deklarowania kontraktu, w ramach którego klasy i struktury powinny zaimplementować określone metody i właściwości.

Interfejsy nie zawierają implementacji czy danych, definiują jedynie sygnatury metod i właściwości, które powinny być zaimplementowane. Klasy i struktury, które implementują interfejs, muszą zapewnić implementację wszystkich wymaganych metod i właściwości.

## Przykład

```
using System;

interface IShape
{
    decimal Area();
    decimal Perimeter();
}

class Rectangle : IShape
{
    private decimal width;
    private decimal height;

    public Rectangle(decimal width, decimal height)
    {
        this.width = width;
        this.height = height;
    }

    public decimal Area()
    {
        return width * height;
    }

    public decimal Perimeter()
    {
        return 2 * (width + height);
    }
}
```

W powyższym przykładzie, interfejs `IShape` definiuje, jakie funkcje powinny być dostępne dla każdego typu figury geometrycznej. Klasa `Rectangle` implementuje ten interfejs, co oznacza, że jest ona zobowiązana do zaimplementowania wszystkich wymaganych metod i właściwości.

Interfejsy są przydatne w programowaniu, ponieważ pozwalają na deklarowanie kontraktu między obiektami, a także umożliwiają polimorfizm, pozwalający na traktowanie obiektów w sposób niezależny od ich konkretnego typu.