# `ref` i `out`

Przekazując do metod zmienne typów wartościowych, tak naprawdę operując w metodzie na parametrze, który został przekazany operujemy na kopii wartości, którą sprecyzowaliśmy jako parametr tej metody. Jednak czasem istnieje potrzeba, aby operować na konkretnej referencji danej wartości, aby miec możliwość jej modyfikacji, również poza daną metodą (co nie jest możliwe jeżeli operujemy na kopii wartości).

Zarówno `ref` jak i `out` umożliwiają przekazywanie argumentów przez referencję do metody, jednak istnieją subtelne różnice w ich użyciu. 

## `ref`

Słowo kluczowe `ref` służy do przekazywania argumentów metod przez referencję. Oznacza to, że w przypadku jego użycia jako modyfikatora argumentu, przekazywana jest nie wartość zmiennej, lecz jej referencja w pamięci.

Przykładowo, jeśli zdefiniujemy metodę o sygnaturze:

```
void Increment(ref int x)
{
    x++;
}
```

To wywołując tę metodę w ten sposób:

```
int a = 1;
Increment(ref a);
```

Zmienna `a` zostanie przekazana do metody `Increment` przez referencję, co oznacza, że po wykonaniu metody, wartość `a` będzie wynosić 2.

Słowo kluczowe `ref` jest przydatne, gdy chcemy, aby zmiany dokonane na argumentach metod były widoczne poza nią, a także gdy chcemy uniknąć kopiowania dużych struktur danych przy przekazywaniu ich jako argumentów metod. Warto jednak zwrócić uwagę, że użycie słowa kluczowego `ref` niesie ze sobą pewne ryzyko i powinno być stosowane ostrożnie, aby uniknąć niepożądanych efektów ubocznych.

## `out`

Słowo kluczowe `out` służy do zwracania więcej niż jednej wartości z metody. Umożliwia to przekazanie argumentów przez referencję i ich zmodyfikowanie w ciele metody.

Podobnie jak słowo kluczowe `ref`, `out` umożliwia przekazywanie argumentów przez referencję, ale istnieje jedna istotna różnica - argumenty przekazywane przez `out` nie muszą być inicjalizowane przed przekazaniem ich do metody. Wewnątrz metody muszą one jednak zostać zainicjalizowane przez tę metodę przed jej zakończeniem. W przypadku argumentów przekazywanych przez `ref`, inicjalizacja jest wymagana przed ich przekazaniem do metody.

Oto przykład użycia słowa kluczowego `out`:

```
public void Divide(int dividend, int divisor, out int quotient, out int remainder)
{
    quotient = dividend / divisor;
    remainder = dividend % divisor;
}
```

W tym przykładzie metoda `Divide` przyjmuje dwa argumenty `dividend` i `divisor`, a następnie zwraca dwa argumenty `quotient` i `remainder`, które są obliczone w ciele metody. Zwracanie tych wartości przez argumenty przekazywane przez `out` umożliwia zwrócenie dwóch wartości z jednej metody.

Można użyć również zmiennej zdefiniowanej z wykorzystaniem słowa kluczowego `out` w wywołaniu metody:

```
int quotient;
int remainder;
Divide(10, 3, out quotient, out remainder);
```

W tym przykładzie zmienne `quotient` i `remainder` zostaną zainicjalizowane wartościami obliczonymi przez metodę `Divide`.

Słowo kluczowe `out` jest przydatne, gdy musimy zwrócić więcej niż jedną wartość z metody, ale chcemy uniknąć tworzenia struktury lub klasy, aby przechowywać te wartości jako pola.

## Różnice

1. Argumenty przekazywane przez `ref` muszą być inicjalizowane przed przekazaniem ich do metody, podczas gdy argumenty przekazywane przez `out` nie muszą.

2. W przypadku `ref`, wartość przekazywana jest do metody i może być modyfikowana, ale nie ma gwarancji, że zostanie ona zmodyfikowana. W przypadku `out`, wartość musi zostać zainicjalizowana przez metodę, a wartość zwrócona musi być wartością przypisaną do argumentu `out`.

3. Słowo kluczowe `ref` może być użyte do przekazywania argumentów przez referencję do metod, które są metodami wywoływanymi przez wartość (metody rozszerzające). Słowo kluczowe `out` nie może być używane w taki sposób.

4. W przypadku `ref`, argument musi być zainicjalizowany przed przekazaniem go do metody, a zmiana wartości argumentu w ciele metody zmienia również wartość oryginalnej zmiennej przekazanej do metody. W przypadku `out`, argument może nie być zainicjalizowany przed przekazaniem go do metody, a wartość argumentu musi zostać ustawiona w ciele metody i zostanie zwrócona po zakończeniu metody.