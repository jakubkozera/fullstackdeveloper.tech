# Równoległe zadania

Wykonywanie równoległych zadań jest niezwykle przydatne, aby zwiększyć wydajność aplikacji, szczególnie w przypadku operacji I/O-zależnych lub obliczeń, które mogą być wykonywane niezależnie od siebie. W C#, do równoczesnego wykonywania wielu zadań asynchronicznych, używamy metod `Task.WhenAll` i `Task.WhenAny`.

1. `Task.WhenAll`:

`Task.WhenAll` pozwala na oczekiwanie na zakończenie wielu zadań asynchronicznych jednocześnie. Metoda ta przyjmuje jako argumenty kolekcję `Task` lub `Task<T>` i zwraca jedno zadanie (`Task`), które zostanie ukończone, gdy wszystkie przekazane zadania zakończą swoje działanie.

Przykład - Wykonywanie wielu operacji asynchronicznych jednocześnie:

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        Task<int> task1 = SomeAsyncOperation(1, 1000);
        Task<int> task2 = SomeAsyncOperation(2, 1500);
        Task<int> task3 = SomeAsyncOperation(3, 500);

        await Task.WhenAll(task1, task2, task3);

        Console.WriteLine("Wszystkie operacje zakończone.");
        Console.WriteLine("Wyniki:");
        Console.WriteLine("Operacja 1: " + task1.Result);
        Console.WriteLine("Operacja 2: " + task2.Result);
        Console.WriteLine("Operacja 3: " + task3.Result);
    }

    public static async Task<int> SomeAsyncOperation(int operationId, int delay)
    {
        await Task.Delay(delay); // Symulacja długiej operacji asynchronicznej
        Console.WriteLine("Operacja " + operationId + " zakończona.");
        return operationId;
    }
}
```

W powyższym przykładzie równocześnie uruchamiamy trzy asynchroniczne operacje `SomeAsyncOperation`, które symulują długie operacje z różnymi opóźnieniami. Za pomocą `Task.WhenAll` oczekujemy na zakończenie wszystkich operacji jednocześnie. Dzięki temu każda operacja może być wykonywana niezależnie od pozostałych, co przyspiesza działanie programu.

2. `Task.WhenAny`:

`Task.WhenAny` pozwala na oczekiwanie na zakończenie dowolnej operacji asynchronicznej spośród przekazanych zadań. Metoda ta również przyjmuje jako argumenty kolekcję `Task` lub `Task<T>`, a następnie zwraca jedno zadanie (`Task`), które zostanie ukończone, gdy dowolne z przekazanych zadań zostanie zakończone.

Przykład - Wykonywanie wielu operacji asynchronicznych i oczekiwanie na pierwszą zakończoną operację:

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        Task<int> task1 = SomeAsyncOperation(1, 1000);
        Task<int> task2 = SomeAsyncOperation(2, 1500);
        Task<int> task3 = SomeAsyncOperation(3, 500);

        Task<int> firstCompletedTask = await Task.WhenAny(task1, task2, task3);

        Console.WriteLine("Pierwsza operacja zakończona: " + firstCompletedTask.Result);
    }

    public static async Task<int> SomeAsyncOperation(int operationId, int delay)
    {
        await Task.Delay(delay); // Symulacja długiej operacji asynchronicznej
        Console.WriteLine("Operacja " + operationId + " zakończona.");
        return operationId;
    }
}
```

W tym przykładzie uruchamiamy trzy asynchroniczne operacje `SomeAsyncOperation` z różnymi opóźnieniami. Za pomocą `Task.WhenAny` oczekujemy na zakończenie pierwszej zakończonej operacji. Wartość zwracana przez `Task.WhenAny` wskazuje na zadanie, które zostało zakończone jako pierwsze.

Podsumowując, `Task.WhenAll` pozwala na oczekiwanie na zakończenie wszystkich zadań asynchronicznych jednocześnie, podczas gdy `Task.WhenAny` pozwala na oczekiwanie na zakończenie dowolnego z przekazanych zadań. Wykorzystanie tych mechanizmów jest niezwykle użyteczne do równoległego wykonywania wielu operacji i zwiększenia wydajności aplikacji.

## YouTube

*https://www.youtube.com/watch?v=LL9GEAY_Dlo&t=973s*