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

Natomiast zastosowanie klas abstrakcyjnych w programach niesie też ze sobą kilka ograniczeń i wad, takich jak:

 - Złożoność: Klasa abstrakcyjna jest bardziej skomplikowana niż zwykła klasa i wymaga dodatkowej wiedzy i umiejętności do prawidłowego zastosowania.

- Dziedziczenie: Klasa abstrakcyjna może być dziedziczona tylko przez jedną klasę pochodną, co może być problematyczne w przypadku bardziej złożonych projektów.

- Ograniczenie funkcjonalności: Klasa abstrakcyjna nie może być utworzona jako obiekt i jest używana tylko jako bazowa klasa dla dziedziczenia.

- Trudność w testowaniu: Klasa abstrakcyjna może być trudna do przetestowania, ponieważ nie można jej użyć jako obiektu i testować jej implementacji, a musi być testowana poprzez testowanie klas pochodnych.

Podsumowując, klasy abstrakcyjne powinny być używane z umiarem i tylko wtedy, gdy jest to naprawdę konieczne w projekcie. W przeciwnym razie może to prowadzić do bardziej skomplikowanego kodu i negatywnie wpłynąć na jego wydajność i łatwość testowania. 
Najczęstszą alternatywą do klas abstracyjnych są interfejsy, które w większości przypadków są wystarczające, a dodatkowo nie nakładają ograniczeń, jak robi to klasa abstrakcyjna.

## YouTube
https://www.youtube.com/watch?v=MqJwL1XInng&t=4s
