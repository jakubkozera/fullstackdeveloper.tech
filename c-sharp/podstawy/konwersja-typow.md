# Konwersja typów

Konwersja typów i rzutowanie to procesy zmiany wartości jednego typu na wartości innego typu. Konwersja typów odbywa się w różny sposób w zależności od typu danych i jest używana do zapewnienia zgodności typów w programie.

W C# istnieją dwie metody konwersji typów: niejawna i jawna. 

## Konwersja niejawna 

Odbywa się automatycznie przez kompilator, gdy przypisujemy wartość zmiennej innego typu do zmiennej o innym typie. 

### Przykład niejawnej konwersji typów
```
int i = 10;
double d = i; 
```

## Konwersja jawna 

Wymaga użycia rzutowania i odbywa się przez jawną deklarację typu.

### Przykład jawnej konwersji typów
```
double d = 10.5;
int i = (int)d; 

```

Rzutowanie może również służyć do konwertowania wartości z jednego typu na inny typ bez utraty informacji. W przypadku konwersji niejawnej, informacje mogą zostać utracone ze względu na ograniczenia typu docelowego.

```
int i = 100;
byte b = (byte)i; 
```
W tym przykładzie, rzutowanie jawne służy do konwersji wartości typu `int` na wartość typu `byte` z zachowaniem wartości, ale w przypadku konwersji niejawnej, wartość 100 wykracza poza zakres typu byte, więc mogłoby dojść do utraty informacji
(niejawna konwersja z int na byte nie byłaby możliwa, ponieważ byte ma mniejszy zakres niż int).

Ważne jest, aby pamiętać, że nie wszystkie typy danych mogą być konwertowane na siebie i rzutowanie może prowadzić do utraty informacji lub błędów, zwłaszcza w przypadku złożonych typów danych.

## YouTube
https://www.youtube.com/watch?v=Q0-tG37m2uE