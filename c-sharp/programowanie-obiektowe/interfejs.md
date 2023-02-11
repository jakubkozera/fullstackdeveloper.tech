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

## Interface a klasa abstrakcyjna - różnice

Podobną funkcjonalność w C# spełniają klasy abstrakcyjne, ale jest między nimi kilka różnic:

- Definicja: Interfejs jest zbiorem zadeklarowanych publicznych metod, właściwości i zdarzeń, które muszą być zaimplementowane przez klasy lub struktury, które go implementują. Natomiast klasa abstrakcyjna jest szablonem klasy, który może zawierać implementacje i jest używany jako bazowa klasa dla dziedziczenia.

- Implementacja: Interfejs może być implementowany przez wiele klas i struktur, natomiast klasa abstrakcyjna może być dziedziczona tylko przez jedną klasę pochodną.

- Dziedziczenie: Interfejs nie może dziedziczyć od żadnej klasy, ale może być dziedziczony przez wiele klas i struktur, natomiast klasa abstrakcyjna może dziedziczyć od innej klasy abstrakcyjnej lub klasy implementującej interfejs.

- Metody: W interfejsie wszystkie metody są deklarowane jako abstrakcyjne, a ich implementacja jest zobowiązana w klasach, które go implementują. W klasie abstrakcyjnej metody mogą być abstrakcyjne lub zawierać implementację.

- Konstruktory: Interfejs nie może zawierać żadnych konstruktorów, natomiast klasa abstrakcyjna może zawierać konstruktory i jest w stanie wywołać konstruktor bazowej klasy.

Ogólnie rzecz biorąc, interfejs jest używany do definiowania standardowego zachowania, które musi być implementowane przez różne klasy, natomiast klasa abstrakcyjna jest używana jako bazowa klasa dla dziedziczenia i zawiera implementację części logiki.