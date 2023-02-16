# Metody w C#

Metody w języku C# to zbiór instrukcji, które wykonują określone zadanie. Metody służą do modularnego projektowania i organizacji kodu, ponieważ pozwalają na oddzielenie logiki biznesowej od innych elementów programu. Metody w C# mogą przyjmować argumenty, zwracać wartości i wywoływać inne metody. W tym artykule omówimy podstawowe koncepcje związane z metodami w C#.

## Deklarowanie metod w C#

Aby stworzyć metodę w C#, należy użyć słowa kluczowego "void" (jeśli metoda nie zwraca żadnej wartości) lub określić typ zwracanej wartości. Następnie należy podać nazwę metody, a jeśli metoda przyjmuje argumenty, należy określić ich typy i nazwy. Oto przykład prostej metody w C#:

```
public void Hello(string name)
{
    Console.WriteLine("Hello, " + name);
}
```

W tym przykładzie metoda "Hello" przyjmuje jeden argument typu string o nazwie "name" i nie zwraca żadnej wartości. Wywołanie metody wygląda następująco:
```
Hello("John");
````
Wynik działania tej metody to "Hello, John".

Natomiast jako, że metody muszą być definiowane wewnątrz klas, to aby je wywołać poza daną klasą, będziemy musieli utworzyć obiekt danego typu.

Przykładowo mają poniższa klasę `User`, aby wywołać z niej metodę `Hello`, musimy utworzyć obiekt klasy `User`.

```
public class User
{
    public void Hello(string name)
    {
        Console.WriteLine("Hello, " + name);
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        User user = new User();
        user.Hello("John");
    }
}
```
## Przeciążanie metod w C#

W języku C# istnieje możliwość przeciążania metod, czyli definiowania wielu metod o tej samej nazwie, ale o różnych parametrach. W ten sposób można zapewnić większą elastyczność w używaniu metody w zależności od potrzeb programu. Oto przykład przeciążania metody w C#:

```
public void Sum(int x, int y)
{
    Console.WriteLine(x + y);
}

public void Sum(double x, double y)
{
    Console.WriteLine(x + y);
}
```
W tym przykładzie zdefiniowano dwie metody o nazwie "Sum", ale jedna przyjmuje argumenty typu int, a druga typu double. Wywołanie tych metod wygląda następująco:

```
Sum(2, 3);      // wynik: 5
Sum(2.5, 3.7);  // wynik: 6.2
```

## Metody statyczne w C#

Metody statyczne w C# to metody, które są wywoływane na poziomie klasy, a nie na poziomie obiektu. Metody statyczne nie wymagają utworzenia obiektu danej klasy, co oznacza, że można je wywoływać bez konieczności tworzenia instancji klasy. Oto przykład metody statycznej w C#:

```
public class Calculator
{
    public static int Add(int x, int y)
    {
        return x + y;
    }
}
```
W tym przykładzie metoda "Add" jest statyczna i zwraca sumę dwóch liczb całkowitych. Można ją wywołać bez tworzenia obiektu klasy, na przykład w ten sposób:

```
int result = Calculator.Add(2, 3);
```
Warto zauważyć, że w tym przypadku nie trzeba tworzyć obiektu klasy `Calculator` przed wywołaniem metody `Add`.


## Dobre praktyki

Oto kilka dobrych praktyk dotyczących tworzenia metod w klasach w języku C#:

1. Zachowaj jednoznaczność i klarowność nazw metod.

Nazwy metod powinny jednoznacznie określać, co dana metoda robi. Nazwy powinny być krótkie i zwięzłe, ale jednocześnie nie powinny być zbyt skrótowe. Dobra nazwa metody powinna być łatwa do zrozumienia dla innych programistów. Pamiętaj, aby w kodzie używać języka angielskiego.

2. Ogranicz długość metody

Długość metody powinna być ograniczona. Zbyt długie metody są trudne do zrozumienia, a ich modyfikacja i testowanie może być kłopotliwe. Dobrą praktyką jest tworzenie metod, których długość nie przekracza 20-30 linii kodu. Jeżeli twoja metoda wymaga większych implementacji, postaraj się ją rozbić na mniejsze części.

3. Zachowaj spójność w stylu kodowania.

Styl kodowania powinien być spójny. Dla każdego projektu należy ustalić określone standardy formatowania kodu, takie jak użycie tabulacji lub spacji, ustawienia wcięć, itp. W ten sposób kod będzie łatwiejszy do zrozumienia i utrzymania.

4. Użyj parametrów i typów zwrotnych odpowiednio.

Parametry i typy zwrotne powinny być używane odpowiednio. Jeśli metoda przyjmuje wiele parametrów, należy zastanowić się nad utworzeniem obiektu, który będzie zawierał te parametry. Typ zwracany powinien jednoznacznie określać, co metoda zwraca.

5. Użyj wyjątków do obsługi błędów

Wyjątki powinny być używane do obsługi błędów w kodzie. W przypadku wystąpienia błędu, wyjątek pozwoli na przekazanie informacji o błędzie do miejsca, w którym można go obsłużyć.

6. Dostosuj metody do zasad SOLID

Metody powinny być zgodne z zasadami SOLID, które stanowią fundament programowania obiektowego. Zasady SOLID określają, jak projektować i implementować klasowe struktury, takie jak klasy i metody, aby były elastyczne, łatwe do modyfikowania i utrzymania

