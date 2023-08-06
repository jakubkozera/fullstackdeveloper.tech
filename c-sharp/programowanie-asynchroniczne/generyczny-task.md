# Generyczny Task

Generyczny `Task<T>` w kontekście programowania asynchronicznego w C# umożliwia zwracanie rezultatów z metod asynchronicznych. Wcześniej w przykładzie korzystaliśmy z klasy `Task`, która może reprezentować asynchroniczne zadanie bez zwracania wyniku. Jednak gdy chcemy zwrócić wynik z metody asynchronicznej, używamy `Task<T>`, gdzie `T` jest typem zwracanego wyniku.

Przykład - Asynchroniczne pobieranie danych z Internetu i zwracanie wyniku:

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        string data = await DownloadDataAsync();
        Console.WriteLine("Pobrane dane: " + data);
    }

    public static async Task<string> DownloadDataAsync()
    {
        using (var client = new HttpClient())
        {
            string url = "https://example.com/data";
            string result = await client.GetStringAsync(url);
            return result;
        }
    }
}
```

W powyższym przykładzie, metoda `DownloadDataAsync` jest teraz zadeklarowana jako `async Task<string>`, co oznacza, że zwraca wynik typu `string` za pomocą `Task<string>`. Wewnątrz tej metody, asynchronicznie pobieramy dane z adresu URL za pomocą `HttpClient` i zwracamy wynik jako `string`. W `Main` korzystamy z operatora `await` do oczekiwania na zakończenie zadania asynchronicznego i pobrania wyniku.

Generyczny `Task<T>` pozwala na zwracanie wyników różnych typów, na przykład `Task<int>` zwróci wynik typu `int`, `Task<bool>` zwróci wynik typu `bool` itd.

Przykład - Asynchroniczne operacje obliczeniowe:

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        int result = await CalculateAsync(10, 5);
        Console.WriteLine("Wynik obliczenia: " + result);
    }

    public static async Task<int> CalculateAsync(int a, int b)
    {
        await Task.Delay(1000); // Symulacja długiej operacji obliczeniowej
        return a + b;
    }
}
```

W tym przykładzie, metoda `CalculateAsync` przyjmuje dwie liczby całkowite `a` i `b`, a następnie wykonuje asynchronicznie operację obliczeniową, której wynik jest zwracany jako `Task<int>`. W `Main` używamy operatora `await`, aby oczekiwać na zakończenie obliczenia i uzyskać wynik.

Generyczny `Task<T>` jest potężnym narzędziem do programowania asynchronicznego w C#, pozwalając na zwrot wyników z asynchronicznych metod i ułatwiając zarządzanie asynchronicznymi operacjami w aplikacji. Dzięki temu można efektywnie tworzyć bardziej responsywne aplikacje, które jednocześnie przetwarzają dane i obsługują interfejs użytkownika.

## YouTube

*https://www.youtube.com/watch?v=LL9GEAY_Dlo&t=770s*