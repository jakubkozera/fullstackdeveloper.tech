# Instrukcja switch

Słowo kluczowe `switch` w języku C# pozwala na wybór konkretnej implementacji kodu, w zależności od podanego wyrażnia oraz dostępnych zmiennych. 

## Składnia

```
switch (expression)
{
    case value1:
        // code 1
        break;
    case value2:
        // code 2
        break;
    ...
    default:
        // default code
        break;
}
```

W powyższym przykładzie `expression` jest wyrażeniem, którego wartość jest porównywana z wartościami dostępnymi w poszczególnych przypadkach `case`. Kiedy wartość wyrażenia pasuje do wartości jednego z przypadków, kod znajdujący się wewnątrz jest wykonywany. Słowo kluczowe `break` jest używane w celu opuszczenie instrukcji `switch` po wykonaniu odpowiedniego kodu. Jeśli żadna z wartości case nie pasuje do wartości podanej jako `expression`, kod wewnątrz gałęzi `default` jest wykonywany.

> Jeśli w instrukcji `switch` nie zostanie użyte słowo kluczowe `break` po kodzie dla danego przypadku `case`, to kod będzie kontynuowany do następnego przypadku `case`, aż do napotkania słowa kluczowego `break`, `return` lub końca instrukcji `switch`. 

Instrukcja `switch` jest częstą alternatywą dla instrukcji `if-else`, jeżeli chcemy wykonać konkretny kawałek kodu w zależności od jednej wartości.

Oprócz tego `switch` również używany do powiązania wartości dla reprezentowanych w różnych typach, przykładowo, chcąc przedstawicz konkretną wartość liczbową typu `int` jako wartość typu `string`, moglibyśmy to osiągnać w następujący sposób:

```
int someNumber = 1;
string result;

switch(someNumber)
{
    case 1:
        result = "one";
        break;
    case 2:
        result = "two";
        break;
    case 3:
        result = "three";
        break;
        
    default:
        result = "other";
        break;
}
```

## Switch expression od wersji 8.0 C#

W C# od wersji 8.0, pojawiła się nowa składnia dla instrukcji `switch`, nazwana `switch expression`, która pozwala na użycie `switch` jako wyrażenia zwracającego wartość. Głównym założeniem `switch expression` było uproszczenie instrukcji `switch`, którego zadaniem jest przypisanie wartości w zależności od konkretnej zmiennej. (patrz przykład powyżej)

W przeciwieństwie do tradycyjnej składni `switch`, gdzie kod jest wykonywany dla każdego przypadku `case` i `break` jest używany do opuszczenia instrukcji `switch`, w `switch expression` każda gałąź `case` zwraca wartość, a kontrola jest przekazywana po pierwszym pasującym wariancie.

```
string result = someNumber switch
{
    1 => "one",
    2 => "two",
    3 => "three",
    _ => "other"
};
```

W powyższym przykładzie, `someNumber` jest wyrażeniem, którego wartość jest porównywana z wartościami dostępnymi w poszczególnych gałęziach `case`. Kiedy wartość `someNumber` pasuje do wartości jednego z `case`, zwracana jest wartość po lewej stronie strzałki (=>), która jest przypisywana do result. Słowo kluczowe `_` jest używane jako ostatniego `case` i jest równoważne `default` w tradycyjnym `switchu`.

Jest to bardziej czytelna i krótsza składnia niż tradycyjny `switch-case` i pozwala na łatwe użycie `switch` jako wyrażenia zwracającego wartość.