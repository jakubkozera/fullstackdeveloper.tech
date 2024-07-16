# Generyczne delegaty

Generyczne delegaty to delegaty, które przyjmują lub zwracają typy danych wskazane przez programistę. Dzięki temu mechanizmowi, programiści mogą pisać bardziej ogólne i elastyczne rozwiązania, które mogą działać z różnymi typami danych bez potrzeby pisania osobnego kodu dla każdego typu.

## Predefiniowane generyczne delegaty

W języku C# istnieją cztery predefiniowane generyczne delegaty:

1. `Func<TResult>` - delegat przyjmujący 0 argumentów i zwracający wartość typu `TResult`.
2. `Func<T, TResult>` - delegat przyjmujący 1 argument typu `T` i zwracający wartość typu `TResult`.
3. `Action` - delegat przyjmujący 0 argumentów i nie zwracający wartości.
4. `Action<T>` - delegat przyjmujący 1 argument typu `T` i nie zwracający wartości.
5. `Predicate<T>` - delegat przyjmujący 1 argument typu `T` i  zwracający wartości typu `bool`.

Każdy z tych predykatów: `Func`, `Action` i `Predicate`, mają swoje definicje z liczbą parametrów od 1 do 15.

Powyższe delegaty są używane do definiowania funkcji anonimowych, które mogą działać z różnymi typami danych. Dzięki nim programiści mogą pisać bardziej elastyczne i ogólne rozwiązania, bez potrzeby pisania osobnego kodu dla każdego typu danych. Oto przykład użycia tych delegatów:

```
Func<int> getInt = () => 42;
Console.WriteLine(getInt()); 

Func<string, int> parse = int.Parse;
Console.WriteLine(parse("123")); 

Action printHello = () => Console.WriteLine("Hello");
printHello(); 

Action<string> greet = name => Console.WriteLine($"Hello, {name}!");
greet("John"); 

```

W tym przykładzie, używamy delegatów `Func` i `Action`, aby definiować funkcje anonimowe, które działają z różnymi typami danych. Pierwsza funkcja zwraca wartość typu `int`, druga parsuje `string` na `int`, trzecia nie przyjmuje argumentów, a czwarta przyjmuje argument typu `string`.

Najczęściej te generyczne delegaty można spotkać przy metodach LINQ, które są parametrami metod filtrowania, sortowania czy pobierania wartości.

Poniżej kilka typowych przykładów ich użycia:

1. Użycie delegatu Func do filtrowania danych za pomocą metody Where:
```
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6 };
List<int> evenNumbers = numbers.Where(x => x % 2 == 0).ToList();
```

W tym przykładzie delegat Func jest używany do określenia warunku filtrowania - tylko liczby parzyste są wybierane z listy numbers.

2. Użycie delegatu Action do przetwarzania danych za pomocą metody ForEach:

```
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6 };
numbers.ForEach(x => Console.WriteLine(x));
```

W tym przykładzie delegat Action jest używany do określenia akcji, która ma zostać wykonana dla każdego elementu listy numbers - w tym przypadku wyświetlenie wartości liczby na konsoli.

3. Użycie delegatu Comparison do sortowania danych za pomocą metody Sort:

```
List<string> words = new List<string> { "apple", "banana", "cherry", "date" };
words.Sort((x, y) => x.Length.CompareTo(y.Length));
```

W tym przykładzie delegat Comparison jest używany do określenia sposobu sortowania danych - według długości każdego słowa w liście words.

4. Użycie delegatu Predicate do filtrowania danych za pomocą metody FindAll:
```
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6 };
List<int> oddNumbers = numbers.FindAll(x => x % 2 != 0);
```
W tym przykładzie delegat Predicate jest używany do określenia warunku filtrowania - tylko liczby nieparzyste są wybierane z listy numbers.


## YouTube

*https://www.youtube.com/watch?v=6vfC4AmPA4M&t=2626s*