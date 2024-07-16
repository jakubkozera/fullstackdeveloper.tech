# Yield

Słowo kluczowe `yield` służy do definiowania iteratorów, czyli metod zwracających sekwencję wartości w sposób leniwy, tzn. generowanie kolejnych wartości tylko w momencie ich potrzeby, a nie na raz.

`Yield` jest używane z jednym z trzech operatorów: 
- `yield return` - służy do zwracania kolejnych wartości sekwencji, 
- `yield break` - służy do zakończenia iteratora, 
- `yield default` - służy do zwrócenia wartości domyślnej

## Przykład

```
public static IEnumerable<int> GetEvenNumbers(int max)
{
    for (int i = 0; i <= max; i++)
    {
        if (i % 2 == 0)
        {
            yield return i;
        }
    }
}
```

W powyższym przykładzie metoda `GetEvenNumbers` zwraca sekwencję liczb parzystych od zera do maksymalnej wartości podanej jako argument max. Użycie słowa kluczowego `yield return` pozwala na leniwe generowanie kolejnych liczb parzystych w momencie ich potrzeby, co jest bardziej wydajne niż generowanie całej sekwencji naraz.

Słowo kluczowe `yield` jest przydatne w przypadku przetwarzania dużych ilości danych lub w sytuacjach, gdy nie jest znana pełna sekwencja wartości z wyprzedzeniem. Iterator umożliwia generowanie kolejnych wartości w miarę potrzeby, co pozwala na bardziej efektywne wykorzystanie zasobów systemowych i pamięci.

## YouTube

*https://www.youtube.com/watch?v=K0bceAr3PgM* 