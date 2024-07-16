## Metody generyczne

Metody generyczne pozwalają na definiowanie funkcji, które mogą działać z różnymi typami danych. Zamiast używać konkretnych typów jako argumentów funkcji, programista może zadeklarować jedno lub więcej parametrów typu, które będą zastąpione przez rzeczywiste typy podczas wywoływania metody. To pozwala na ponowne użycie jednej funkcji dla wielu różnych typów, co prowadzi do bardziej elastycznego i czytelnego kodu.

### Składnia metody generycznej:

Oto przykład prostej metody generycznej, która zwraca większą z dwóch liczb:

```csharp
public T Max<T>(T a, T b) where T : IComparable<T>
{
    return a.CompareTo(b) > 0 ? a : b;
}
```

W powyższym przykładzie użyliśmy `T` jako parametru typu. Dzięki temu możemy użyć tej metody z różnymi typami, pod warunkiem, że typ implementuje interfejs `IComparable<T>`, co umożliwia porównywanie obiektów tego samego typu.

### Zalety metody generycznej:

1. **Uniwersalność**: Metody generyczne pozwalają na tworzenie funkcji, które mogą działać na różnych typach danych, co prowadzi do bardziej ogólnego i ponownie używalnego kodu.

2. **Elastyczność**: Programista może używać tej samej funkcji dla wielu różnych typów, eliminując potrzebę tworzenia osobnych funkcji dla każdego typu danych.

3. **Typowe bezpieczeństwo**: Dzięki ograniczeniom typów (constraints), które można zdefiniować dla parametrów typu, metody generyczne zapewniają bezpieczeństwo typów i eliminują ryzyko błędów typowania.

4. **Poprawa wydajności**: Unikanie rzutowania typów wewnątrz funkcji, jak to ma miejsce w przypadku niegenerycznych metod, prowadzi do lepszej wydajności i mniejszego narzutu czasowego.

### Podsumowanie:

Metody generyczne w języku C# pozwalają na tworzenie bardziej uniwersalnych, elastycznych i bezpiecznych funkcji, które mogą operować na różnych typach danych. Dzięki temu programiści mogą unikać powielania kodu i tworzyć bardziej czytelny, łatwiejszy w utrzymaniu i wydajniejszy kod. Metody generyczne są nieocenionym narzędziem w zestawie funkcji języka C#, które pozwalają na lepsze zarządzanie typami danych i dostarczają potężnych możliwości programowania.

## YouTube

*https://www.youtube.com/watch?v=6vfC4AmPA4M&t=2301s*