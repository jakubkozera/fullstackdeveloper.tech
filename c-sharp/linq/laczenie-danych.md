# Łączenie danych

Łączenie danych jest częstą operacją podczas przetwarzania kolekcji w aplikacjach. Pozwala na połączenie danych z dwóch różnych źródeł na podstawie określonych kluczy. W języku C# LINQ (Language-Integrated Query) mamy dostęp do metody `Join`, która umożliwia łatwe łączenie danych z różnych kolekcji na podstawie wspólnych kluczy. W tym artykule omówimy, jak działa metoda `Join`, `GroupJoin` i jak je użyć do łączenia danych.

## Jak działa metoda Join w LINQ?

Metoda `Join` w LINQ umożliwia łączenie dwóch kolekcji na podstawie wspólnego klucza. Operacja łączenia polega na znalezieniu pasujących par elementów, które mają ten sam klucz w obu kolekcjach. Wynikiem jest nowa kolekcja, która zawiera te pary elementów, w których klucze są zgodne.

Składnia metody `Join` wygląda następująco:

```csharp
public static IEnumerable<TResult> Join<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, TInner, TResult> resultSelector
);
```

Gdzie:
- `outer` i `inner` to dwie kolekcje, które chcemy połączyć.
- `outerKeySelector` i `innerKeySelector` to funkcje lambda, które zwracają klucze dla każdego elementu w odpowiednich kolekcjach.
- `resultSelector` to funkcja lambda, która określa, jakie dane zostaną zwrócone jako wynik połączenia dla każdej pary elementów.

Na pierwszy rzut oka, może wydawać się ona nieco skomplikowana, ale raczej jest to kwestia przerobienia kilku przykładów.

## Przykład użycia metody Join

Załóżmy, że mamy dwie kolekcje - `orders` i `customers`, które chcemy połączyć na podstawie klucza "CustomerId". Każde zamówienie ma przypisany identyfikator klienta, a kolekcja klientów zawiera informacje o tych klientach. Chcemy połączyć te dane, aby uzyskać pełne informacje o każdym zamówieniu wraz z danymi klienta, który zamówienie złożył.

Oto jak to zrobić za pomocą metody `Join`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<Order> orders = new List<Order>
        {
            new Order { OrderId = 1, CustomerId = 101, Amount = 100 },
            new Order { OrderId = 2, CustomerId = 102, Amount = 150 },
            new Order { OrderId = 3, CustomerId = 101, Amount = 200 },
            new Order { OrderId = 4, CustomerId = 103, Amount = 50 }
        };

        List<Customer> customers = new List<Customer>
        {
            new Customer { CustomerId = 101, Name = "John" },
            new Customer { CustomerId = 102, Name = "Alice" },
            new Customer { CustomerId = 103, Name = "Bob" }
        };

  // `orders` - kolekcja do której chcemy "dołączyć" inną kolekcję
// `customers`: pierwszy parametr metody - customers, czyli kolekcja, którą chcemy dołączyć 
// `order => order.CustomerId,` drugi parametr - klucz po, którym będziemy łączyć z pierwszej kolekcji (orders)
// `customer => customer.CustomerId` trzeci parametr - klucz po, którym będziemy łączyć z drugiej kolekcji (customers)

      var orderDetails = orders.Join( 
            customers, 
            order => order.CustomerId, 
            customer => customer.CustomerId, 
            (order, customer) => new
            {
                order.OrderId,
                customer.Name,
                order.Amount
            });
            // funkcja przyjmująca parę dopasowanego elementu z pierwszej kolekcji do drugiej, a rezultatem jest nowy obiekt zwracany jako typ anonimowy z metody Join

 
        foreach (var orderDetail in orderDetails)
        {
            Console.WriteLine($"OrderId: {orderDetail.OrderId}, Customer: {orderDetail.Name}, Amount: {orderDetail.Amount}");
        }
    }
}

class Order
{
    public int OrderId { get; set; }
    public int CustomerId { get; set; }
    public decimal Amount { get; set; }
}

class Customer
{
    public int CustomerId { get; set; }
    public string Name { get; set; }
}
```

Wynikiem działania tego kodu będzie wydrukowanie:

```
OrderId: 1, Customer: John, Amount: 100
OrderId: 2, Customer: Alice, Amount: 150
OrderId: 3, Customer: John, Amount: 200
OrderId: 4, Customer: Bob, Amount: 50
```

## Metoda GroupJoin

Metoda `GroupJoin` w C# LINQ jest kolejnym narzędziem, które pozwala na łączenie danych z dwóch różnych kolekcji na podstawie wspólnego klucza. W porównaniu do metody `Join`, która zwraca tylko dopasowane pary elementów, metoda `GroupJoin` tworzy hierarchiczną strukturę, która zawiera elementy z pierwszej kolekcji wraz z pasującymi elementami z drugiej kolekcji. W tym artykule omówimy, jak działa metoda `GroupJoin` i jakie są różnice między `Join` a `GroupJoin`.

## Jak działa metoda GroupJoin w LINQ?

Metoda `GroupJoin` w LINQ działa podobnie jak metoda `Join`, ale różni się w wynikach, które generuje. W przypadku metody `GroupJoin`, wynikiem jest sekwencja grup (hierarchiczna struktura), w której każda grupa reprezentuje element z pierwszej kolekcji oraz wszystkie pasujące elementy z drugiej kolekcji, które mają ten sam klucz.

Składnia metody `GroupJoin` wygląda następująco:

```csharp
public static IEnumerable<TResult> GroupJoin<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, IEnumerable<TInner>, TResult> resultSelector
);
```

Gdzie:
- `outer` i `inner` to dwie kolekcje, które chcemy połączyć.
- `outerKeySelector` i `innerKeySelector` to funkcje lambda, które zwracają klucze dla każdego elementu w odpowiednich kolekcjach.
- `resultSelector` to funkcja lambda, która określa, jakie dane zostaną zwrócone jako wynik połączenia dla każdego elementu z pierwszej kolekcji oraz pasujących elementów z drugiej kolekcji.

## Przykład użycia metody GroupJoin

Załóżmy, że nadal mamy dwie kolekcje - `orders` i `customers`, które chcemy połączyć na podstawie klucza "CustomerId". Każde zamówienie ma przypisany identyfikator klienta, a kolekcja klientów zawiera informacje o tych klientach. Chcemy użyć metody `GroupJoin`, aby uzyskać hierarchiczną strukturę, która zawiera informacje o każdym zamówieniu oraz wszystkich klientach, którzy złożyli to zamówienie.

Oto jak to zrobić za pomocą metody `GroupJoin`:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<Order> orders = new List<Order>
        {
            new Order { OrderId = 1, CustomerId = 101, Amount = 100 },
            new Order { OrderId = 2, CustomerId = 102, Amount = 150 },
            new Order { OrderId = 3, CustomerId = 101, Amount = 200 },
            new Order { OrderId = 4, CustomerId = 103, Amount = 50 }
        };

        List<Customer> customers = new List<Customer>
        {
            new Customer { CustomerId = 101, Name = "John" },
            new Customer { CustomerId = 102, Name = "Alice" },
            new Customer { CustomerId = 103, Name = "Bob" }
        };

        var orderDetails = orders.GroupJoin(
            customers,
            order => order.CustomerId,
            customer => customer.CustomerId,
            (order, matchingCustomers) => new
            {
                order.OrderId,
                Customers = matchingCustomers.Select(cust => cust.Name).ToList(),
                order.Amount
            });

        foreach (var orderDetail in orderDetails)
        {
            Console.WriteLine($"OrderId: {orderDetail.OrderId}, Customers: {string.Join(", ", orderDetail.Customers)}, Amount: {orderDetail.Amount}");
        }
    }
}

class Order
{
    public int OrderId { get; set; }
    public int CustomerId { get; set; }
    public decimal Amount { get; set; }
}

class Customer
{
    public int CustomerId { get; set; }
    public string Name { get; set; }
}
```

Wynikiem działania tego kodu będzie wydrukowanie:

```
OrderId: 1, Customers: John, Amount: 100
OrderId: 2, Customers: Alice, Amount: 150
OrderId: 3, Customers: John, Amount: 200
OrderId: 4, Customers: Bob, Amount: 50
```

## Różnice między Join a GroupJoin

Różnica między `Join` a `GroupJoin` polega na wynikach, które są generowane:

- `Join`: Zwraca tylko dopasowane pary elementów z dwóch kolekcji, czyli elementy, które mają wspólne klucze.

- `GroupJoin`: Zwraca sekwencję grup (hierarchiczną strukturę), gdzie każda grupa reprezentuje element z pierwszej kolekcji oraz wszystkie pasujące elementy z drugiej kolekcji, które mają ten sam klucz.

Podsumowując, metoda `GroupJoin` pozwala na bardziej zaawansowane łączenie danych, które generuje wynik w postaci hierarchicznej struktury, umożliwiając łatwiejsze korzystanie z powiązanych danych. Jest to przydatne, gdy chcemy otrzymać dane w formie hierarchicznej, np. lista zamówień wraz z wszystkimi klientami, którzy złożyli te zamówienia. W zastosowaniach, gdzie potrzebujemy prostych, płaskich wyników, metoda `Join` może być bardziej odpowiednia. Wybór odpowiedniej metody zależy od konkretnego przypadku i oczekiwanego wyniku.


## YouTube

*https://www.youtube.com/watch?v=0plHg95D220&t=1264s*