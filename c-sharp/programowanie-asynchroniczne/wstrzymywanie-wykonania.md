# Wstrzymywanie wykonania

Metody `Thread.Sleep` i `Task.Delay` są używane do wstrzymywania wykonania programu, ale różnią się w podejściu i zastosowaniu w programowaniu synchronicznym i asynchronicznym. Oto opis różnic między nimi:

1. `Thread.Sleep`:

`Thread.Sleep` jest metodą synchroniczną i jest dostępna w przestrzeni nazw `System.Threading`. Główną różnicą między `Thread.Sleep` a `Task.Delay` jest to, że `Thread.Sleep` blokuje wątek, w którym została wywołana, przez określony czas, co oznacza, że cały wątek jest bezczynny przez ten czas. To oznacza, że nie można korzystać z innych zadań asynchronicznych ani operacji w tym samym wątku, podczas gdy `Thread.Sleep` jest aktywne.

Przykład - Użycie `Thread.Sleep`:

```csharp
using System;
using System.Threading;

public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Rozpoczęcie programu.");

        Thread.Sleep(3000); // Wstrzymaj wykonanie wątku na 3 sekundy

        Console.WriteLine("Zakończenie programu.");
    }
}
```

2. `Task.Delay`:

`Task.Delay` jest metodą asynchroniczną dostępną w przestrzeni nazw `System.Threading.Tasks`. W przeciwieństwie do `Thread.Sleep`, `Task.Delay` nie blokuje wątku. Zamiast tego zwraca zadanie (`Task`), które jest ukończone po określonym czasie opóźnienia. Dzięki temu można wykorzystać czas oczekiwania do wykonywania innych operacji w tym wątku lub do przetwarzania innych zadań asynchronicznych.

Przykład - Użycie `Task.Delay`:

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        Console.WriteLine("Rozpoczęcie programu.");

        await Task.Delay(3000); // Oczekaj 3 sekundy asynchronicznie

        Console.WriteLine("Zakończenie programu.");
    }
}
```

Różnice między `Thread.Sleep` a `Task.Delay` w programowaniu asynchronicznym:

- `Thread.Sleep` jest używane w programowaniu synchronicznym do wstrzymania wykonania wątku. Powoduje to, że cały wątek jest bezczynny przez określony czas, co może prowadzić do marnowania zasobów, gdy inne wątki są zablokowane oczekując na ukończenie tego wątku.

- `Task.Delay` jest używane w programowaniu asynchronicznym i nie blokuje wątku. Zamiast tego zwraca zadanie, które zostanie ukończone po określonym czasie, co pozwala na asynchroniczne oczekiwanie bez blokowania innych zadań.

W programowaniu asynchronicznym zawsze warto unikać użycia `Thread.Sleep`, ponieważ blokuje on wątek i może wpływać negatywnie na responsywność aplikacji. Zamiast tego zaleca się używanie `Task.Delay` w celu oczekiwania asynchronicznego, co pozwala na lepsze zarządzanie wątkami i zapewnienie płynnego działania aplikacji.


## YouTube

*https://www.youtube.com/watch?v=LL9GEAY_Dlo&t=1360s*