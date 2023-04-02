# Typy wbudowane

Typy wbudowane w C# (ang. built-in types) to typy danych, które są częścią języka i dostarczają podstawową funkcjonalność dla przechowywania i manipulacji wartościami. Są to typy podstawowe, które nie są oparte na klasach lub strukturach.

Oto lista typów wbudowanych w C# i ich przykłady:

- Typy liczb całkowitych: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`

    ```
    int a = 10;
    uint b = 20U;
    ```

    W zależności od użytego typu, będziemy w stanie pod daną zmienną przechowywać więcej lub mniej wartości liczbowych (przykładowo `byte` od 0 do 255, a `ushort` od 0 do 65,535), a co za tym idzie, będą one potrzebowały więcej lub mniej pamięci do przechowywania.

- Typy liczb zmiennoprzecinkowych: `float`, `double`, `decimal`
    ```
    double x = 3.14;
    float y = 2.5f;
    decimal z = 100.00m;
    ```
- Typ logiczny: `bool` - jest w stanie przechowywać informacje o wartości `true` lub `false`, inaczej nazywany flagą bitową.
    ```
    bool isTrue = true;
    bool isFalse = false;
    ```
- Typ znakowy: `char` - jest w stanie przechować informację o pojedyńczym znaku, bądź o wartości Unicode (reprezentującej konkretny znak)
    ```
    char c1 = 'A';
    char c2 = '\u0058'; // Unicode character 'X'
    ```
- Typ tekstowy: `string` - najbardziej uniwersalny typ, pod który możemy przypisać dowolny ciąg znaków. 

    ```
    string str1 = "Hello";
    string str2 = "World";
    string str3 = str1 + " " + str2; // "Hello World"
    ```
- Typ daty i czasu: `DateTime`. Typ `DateTime` jest używany do przechowywania dat i czasu. Jest to typ wartościowy, a jego wartość jest reprezentowana jako liczba dni i części dni (frakcji sekundy) od 1 stycznia 0001 r. n.e. 00:00:00 UTC (Universal Coordinated Time). `DateTime` dostarcza podstawowych funkcjonalności do manipulacji datami i czasami, takich jak dodawanie lub odejmowanie dni, godzin, minut i sekund, porównywanie dat i czasów oraz formatowanie i parsowanie. 

    Oto kilka przykładów użycia typu `DateTime` w C#:

    ```
    DateTime now = DateTime.Now; // bieżąca data i czas
    DateTime today = DateTime.Today; // dzisiejsza data
    DateTime tomorrow = today.AddDays(1); // jutro
    DateTime nextWeek = today.AddDays(7); // za tydzień
    DateTime specifiedDate = new DateTime(2023, 3, 15); // określona data
    ```

## YouTube

*https://www.youtube.com/watch?v=9APHzbMQ-so*