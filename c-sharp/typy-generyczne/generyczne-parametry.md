# Generyczne parametry

Generyczne parametry pozwalają na zdefiniowanie klas, struktur, interfejsów, metod i delegatów, które nie są związane z konkretnym typem danych. Zamiast tego, w momencie definiowania tych konstrukcji, programista może określić jeden lub więcej parametrów typu, które będą zastępowane przez konkretne typy danych podczas korzystania z nich. Pozwala to na tworzenie kodu, który może działać z różnymi typami, a jednocześnie zachowuje statyczne typowanie, eliminując ryzyko błędów wynikających z niepoprawnego typowania.

### Przykład użycia generycznych parametrów:

Załóżmy, że chcemy napisać klasę, która reprezentuje parę wartości różnych typów. Tradycyjny sposób implementacji tej klasy może wyglądać następująco:

```csharp
class Pair
{
    private object first;
    private object second;

    public Pair(object first, object second)
    {
        this.first = first;
        this.second = second;
    }

    public object GetFirst() => first;
    public object GetSecond() => second;
}

```

Jednakże, korzystając z generycznych parametrów, możemy stworzyć bardziej ogólną (generyczną) i bezpieczną implementację tej klasy:

```csharp
class Pair<TFirst, TSecond>
{
    private TFirst first;
    private TSecond second;

    public Pair(TFirst first, TSecond second)
    {
        this.first = first;
        this.second = second;
    }

    public TFirst GetFirst() => first;
    public TSecond GetSecond() => second;
}
```

Teraz możemy tworzyć obiekty klasy `Pair` dla różnych typów danych:

```csharp
var pair1 = new Pair<int, string>(42, "Example");
var pair2 = new Pair<double, bool>(3.14, true);
```

### Zalety generycznych parametrów:

1. **Wielokrotnego użytku**: Generyczne parametry pozwalają na ponowne wykorzystanie kodu dla różnych typów danych, co przyczynia się do zwiększenia wydajności i utrzymania przejrzystości kodu.

2. **Typowe bezpieczeństwo**: Dzięki generycznym parametrom błędy związane z typowaniem są wykrywane już w fazie kompilacji, co pozwala uniknąć wielu błędów w trakcie działania programu.

3. **Wyraźniejszy kod**: Użycie generycznych parametrów pozwala na zwiększenie czytelności kodu, ponieważ programista nie musi korzystać z niejasnych rzutowań i konwersji typów.

4. **Lepsza wydajność**: Generyczne parametry pozwalają na generowanie bardziej zoptymalizowanego kodu, ponieważ kod jest w pełni typowany w czasie kompilacji, a nie wymaga dodatkowych sprawdzeń typów podczas działania programu.

### Podsumowanie:

Generyczne parametry w języku C# to narzędzie, które pozwala na tworzenie elastycznego, bezpiecznego i wydajnego kodu. Pozwalają programistom na pracę z różnymi typami danych, jednocześnie zachowując pełne typowanie w czasie kompilacji. Dzięki temu kod staje się bardziej czytelny, łatwiejszy do utrzymania i mniej podatny na błędy. Generyczne parametry są jednym z najważniejszych elementów języka C#, które przyczyniają się do jego popularności i użyteczności w dzisiejszym świecie programowania.

## YouTube

*https://www.youtube.com/watch?v=6vfC4AmPA4M&t=774s*