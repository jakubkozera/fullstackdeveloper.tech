# Generyczne delegaty

Generyczne delegaty to delegaty, które przyjmują lub zwracają typy danych wskazane przez programistę. Dzięki temu mechanizmowi, programiści mogą pisać bardziej ogólne i elastyczne rozwiązania, które mogą działać z różnymi typami danych bez potrzeby pisania osobnego kodu dla każdego typu.

## Predefiniowane generyczne delegaty

W języku C# istnieją cztery predefiniowane generyczne delegaty:

1. `Func<TResult>` - delegat przyjmujący 0 argumentów i zwracający wartość typu `TResult`.
2. `Func<T, TResult>` - delegat przyjmujący 1 argument typu `T` i zwracający wartość typu `TResult`.
3. `Action` - delegat przyjmujący 0 argumentów i nie zwracający wartości.
4. `Action<T>` - delegat przyjmujący 1 argument typu `T` i nie zwracający wartości.

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