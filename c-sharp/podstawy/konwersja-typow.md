# Konwersja typów

Konwersja typów i rzutowanie to procesy zmiany wartości jednego typu na wartości innego typu. Konwersja typów odbywa się w różny sposób w zależności od typu danych i jest używana do zapewnienia zgodności typów w programie.


Aby zmienić wartości wbudowanych typów, na wartości innego typu najczęściej będziemy używać rzutawnia, które tak naprawdę jest specjalnym operatorem pomiędzy dwoma typami.

Przykładowo nie będziemy mieć problemu zrzutować różne typy wartości liczbowych na siebie, przykładowo `int` na `long` czy `byte` na `int`, natomiast zmieniając wartości typu `string` na np. typ `int`, nie będziemy mogli już polegać na rzutowaniu.

Mimo, że dla nas wartość typu `string` = `"4"` odpowiada wartości typu `int` = `4`, to tego typu konwersje,  będziemy musieli zrobić przez parsowanie wartosci (zmiana wartości na wartość innego typu za pomocą metody).

Zanim przejdziemy do parsowania, zobaczmy jak możemy rzutować typy.

W C# istnieją dwie metody rzutowania typów: niejawna i jawna. 

## Rzutowanie niejawne 

Odbywa się automatycznie przez kompilator, gdy przypisujemy wartość zmiennej innego typu do zmiennej o innym typie. 

### Przykład niejawnej konwersji typów
```
int i = 10;
double d = i; 
```

## Rzutowanie jawne 

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

## Parsowanie

Wartość typu `string`, tak naprawdę może repezentować wartość dowolnego typu, przykładowo może to być liczba całkowita, zmiennoprzecinkowa, data czy wartość true/false.

Natomiast w celu przekształcenia tego typu wartości na inny typ, będziemy musieli poslużyć się odpowiednimi metodami konkretnego typu, zazwyczaj używa się metody `TryParse`, która w bezpieczny sposób zwróci rezultat w danym typie, jeżeli takie dana konwersja typów przebiegła prawidłowo.

Oto kilka przykładów parsowania typów wbudowanych w C#:

Parsowanie typu całkowitoliczbowego `int`:

```string str = "123";
int result;
if (int.TryParse(str, out result))
{
    Console.WriteLine(result); // Output: 123
}
```
Parsowanie typu zmiennoprzecinkowego `double`:

```string str = "3.14";
double result;
if (double.TryParse(str, out result))
{
    Console.WriteLine(result); // Output: 3.14
}
```
Parsowanie typu logicznego `bool`:

```string str = "True";
bool result;
if (bool.TryParse(str, out result))
{
    Console.WriteLine(result); // Output: True
}
```
Parsowanie typu znakowego `char`:

```string str = "A";
char result;
if (char.TryParse(str, out result))
{
    Console.WriteLine(result); // Output: A
}
```
Parsowanie typu daty `DateTime`:

```string str = "2022-01-01";
DateTime result;
if (DateTime.TryParse(str, out result))
{
    Console.WriteLine(result.ToString("yyyy-MM-dd")); // Output: 2022-01-01
}
```

## YouTube
*https://www.youtube.com/watch?v=Q0-tG37m2uE*