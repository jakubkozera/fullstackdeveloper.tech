# Asynchroniczne wyjątki

Programowanie asynchroniczne w C# pozwala na tworzenie bardziej wydajnych i responsywnych aplikacji. Jednak praca z metodami asynchronicznymi wiąże się z koniecznością odpowiedniego przechwytywania i obsługi wyjątków. W tym artykule dowiemy się, jak przechwytywać wyjątki z metod asynchronicznych w C# oraz jak zapewnić bezpieczeństwo i niezawodność naszego kodu.

### Przyczyna trudności w przechwytywaniu wyjątków asynchronicznych

Metody asynchroniczne, oznaczone słowem kluczowym "async", wykonują operacje w tle, pozwalając na nieblokującą pracę wątku głównego. To oznacza, że metoda asynchroniczna może zostać przerwana, a następnie wznowiona w innym wątku, zanim zakończy swoje działanie. W przypadku wystąpienia wyjątku, błędne zachowanie może wynikać z nieprawidłowego przechwycenia lub braku przechwycenia wyjątku.

### Przechwytywanie wyjątków z metod asynchronicznych

Przechwytywanie wyjątków z metod asynchronicznych jest istotnym krokiem w zapewnieniu niezawodności i bezpieczeństwa naszego kodu. Aby to osiągnąć, używamy słowa kluczowego "await" do oczekiwania na zakończenie asynchronicznej operacji i przechwycenia ewentualnych wyjątków.

```csharp
async Task DoSomethingAsync()
{
    try
    {
        // Wywołanie asynchronicznej operacji przy użyciu "await"
        await SomeAsyncOperation();
    }
    catch (Exception ex)
    {
        // Obsługa wyjątku
        Console.WriteLine($"Wystąpił wyjątek: {ex.Message}");
    }
}
```

W powyższym przykładzie `DoSomethingAsync` jest asynchroniczną metodą, która wywołuje inną asynchroniczną operację `SomeAsyncOperation`. Dzięki użyciu "await", metoda `DoSomethingAsync` oczekuje na zakończenie `SomeAsyncOperation` i przechwytuje ewentualny wyjątek w bloku `catch`.

### Ręczne propagowanie wyjątków

W przypadku, gdy nie chcemy przechwytować wyjątku wewnątrz metody asynchronicznej, a zamiast tego chcemy przekazać go na zewnątrz, możemy użyć słowa kluczowego "throw" bezpośrednio po "await".

```csharp
async Task DoSomethingAsync()
{
    try
    {
        // Wywołanie asynchronicznej operacji przy użyciu "await"
        await SomeAsyncOperation();
    }
    catch (Exception ex)
    {
        // Obsługa wyjątku lub ręczne jego przekazanie na zewnątrz
        throw;
    }
}
```

W tym przypadku, jeśli `SomeAsyncOperation` zgłosi wyjątek, zostanie on przekazany na zewnątrz metody `DoSomethingAsync`, gdzie może być przechwycony i obsłużony w odpowiednich blokach catch.

### Obsługa wielu asynchronicznych wyjątków

Jeśli chcemy przechwycić wyjątki z wielu asynchronicznych operacji w jednym bloku `catch`, możemy użyć klauzuli "when" do warunkowego przechwycenia.

```csharp
async Task DoSomethingAsync()
{
    try
    {
        // Wywołanie asynchronicznych operacji przy użyciu "await"
        await SomeAsyncOperation1();
        await SomeAsyncOperation2();
    }
    catch (Exception ex) when (ex is OperationException || ex is NetworkException)
    {
        // Obsługa wyjątków typu OperationException lub NetworkException
        Console.WriteLine($"Wystąpił wyjątek: {ex.Message}");
    }
}
```

W powyższym przykładzie, jeśli jedna z asynchronicznych operacji (`SomeAsyncOperation1` lub `SomeAsyncOperation2`) zgłosi wyjątek typu `OperationException` lub `NetworkException`, zostanie on przechwycony w bloku `catch`.

## Różnica między "async Task" a "async void":

W C# mamy dwa główne rodzaje asynchronicznych metod: `async Task` i `async void`. Oto różnice między nimi:

1. **"async Task"**: Metody oznaczone jako `async Task` zwracają typ `Task`, który reprezentuje asynchroniczną operację, która może zwrócić wartość. Jest to preferowany sposób tworzenia asynchronicznych metod, ponieważ umożliwia przechwytywanie wyjątków i obsługę błędów w asynchroniczny sposób.

```csharp
async Task DoSomethingAsync()
{
    // Asynchroniczna logika
}
```

2. **"async void"**: Metody oznaczone jako `async void` nie zwracają wartości, co oznacza, że nie można oczekiwać, że zakończą się synchronicznie. Taka metoda jest używana do obsługi zdarzeń asynchronicznie lub w kontekście aplikacji konsolowej. Jednakże, metody `async void` nie pozwalają na przechwytywanie wyjątków z zewnątrz, co sprawi, że nasz program zakończy swoje działanie, jeżeli wyjątek wystąpi podczas wykonywania takiej metody, jako, że nie mamy sposoby jego przechwycenia.

```csharp
async void DoSomethingAsync()
{
    // Asynchroniczna logika
}
```

### Obsługa asynchronicznych wyjątków:

Aby obsłużyć asynchroniczne wyjątki w C#, musimy korzystać z `await` wewnątrz metody asynchronicznej. W ten sposób asynchroniczne wyjątki zostaną przekazane do kontekstu wywołania, który będzie mógł je przechwycić.

```csharp
async Task DoSomethingAsync()
{
    try
    {
        // Asynchroniczna logika, która może zgłosić wyjątek
        await SomeAsyncOperation();
    }
    catch (Exception ex)
    {
        // Obsługa wyjątku
    }
}
```

Dzięki użyciu `await`, wyjątki zgłaszane przez asynchroniczną operację zostaną przekazane do bloku `catch`, w którym możemy je obsłużyć zgodnie z naszymi wymaganiami.

### Podsumowanie:

Asynchroniczne wyjątki w C# to ważny aspekt asynchronicznego programowania, który wymaga odpowiedniej obsługi. Warto pamiętać o różnicy między "async Task" a "async void", aby unikać pułapek, które mogą wprowadzić trudności w debugowaniu i utrzymaniu kodu. Poprawne używanie `await` w asynchronicznych metodach pozwoli na przechwycenie wyjątków w odpowiednim kontekście, zapewniając bezpieczeństwo i niezawodność naszego kodu. Asynchroniczne programowanie w C# jest potężnym narzędziem, które pozwala na tworzenie wydajnych i responsywnych aplikacji, pod warunkiem, że odpowiednio obsługujemy asynchroniczne wyjątki.

## YouTube

*https://www.youtube.com/watch?v=LL9GEAY_Dlo&t=1616s*