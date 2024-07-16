# Async i await

Async i Await są mechanizmami wprowadzonymi w języku C# od wersji 5.0, które pozwalają na asynchroniczne programowanie w sposób bardziej czytelny i wydajny. Pozwalają one na efektywne zarządzanie asynchronicznymi operacjami w kodzie, takimi jak wywołania sieciowe, odczyt plików, operacje bazodanowe itp., bez blokowania wątku i bezczynnego oczekiwania na wynik. Dzięki temu aplikacje są bardziej responsywne i mogą lepiej obsługiwać duże obciążenia.

Ważne pojęcia:

1. Asynchroniczność: Oznacza, że zadania nie muszą być wykonywane sekwencyjnie i synchronicznie. Możemy wykonywać wiele operacji równocześnie, co jest szczególnie przydatne w przypadku zadań I/O-zależnych, które wymagają czasu na oczekiwanie na odpowiedź (np. pobieranie danych z Internetu).

2. Task (Zadanie): Task to obiekt reprezentujący asynchroniczne zadanie. Może ono zwracać wynik lub być typu "void". Task reprezentuje zlecone zadanie, które będzie wykonywane w tle.

3. async: Jest to modyfikator, który oznacza, że metoda zawiera kod asynchroniczny. Metoda z modyfikatorem async musi zwracać typ Task lub Task<T> (jeśli ma zwracać wynik).

4. await: Operator await używany jest wewnątrz metody async i wskazuje na punkt, w którym metoda czeka na zakończenie asynchronicznej operacji. Wywołanie z operatorem await pozwala na asynchroniczne czekanie na zakończenie Task-a, bez blokowania wątku.

Przykład - Asynchroniczne pobieranie danych z Internetu:

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        await DownloadDataAsync();
        Console.WriteLine("Pobieranie zakończone!");
    }

    public static async Task DownloadDataAsync()
    {
        using (var client = new HttpClient())
        {
            string url = "https://example.com/data";
            string result = await client.GetStringAsync(url);
            Console.WriteLine("Pobrane dane: " + result);
        }
    }
}
```

W powyższym przykładzie, metoda `DownloadDataAsync` jest oznaczona jako `async`, co pozwala na użycie operatora `await`. Wewnątrz tej metody, używając obiektu `HttpClient`, pobieramy dane z adresu URL asynchronicznie za pomocą metody `GetStringAsync()`. Gdy kod napotka operator `await`, nie blokuje on głównego wątku; zamiast tego wstrzymuje wykonanie metody `DownloadDataAsync`, aż operacja pobierania danych zostanie zakończona. W międzyczasie główny wątek może obsługiwać inne zadania.

Przykłady zastosowań async/await:

1. Aplikacje sieciowe: Gdy aplikacja potrzebuje pobierać dane z serwera lub komunikować się z API, async/await pozwala na wykonywanie tych operacji asynchronicznie, co poprawia responsywność aplikacji i pozwala na jednoczesne przetwarzanie innych zadań.

2. Aplikacje desktopowe: W aplikacjach desktopowych, np. Windows Forms lub WPF, async/await mogą być wykorzystane do asynchronicznego przetwarzania operacji I/O, takich jak odczyt plików lub operacje na bazach danych, bez zamrażania interfejsu użytkownika.

3. Aplikacje mobilne: W aplikacjach na platformy mobilne, async/await pozwalają na wykonywanie operacji sieciowych lub zapisu do bazy danych asynchronicznie, co zapewnia płynne działanie aplikacji i zapobiega zamrożeniu interfejsu użytkownika.

4. Serwisy internetowe: Serwisy internetowe często muszą obsługiwać wiele żądań równocześnie. Mechanizm async/await pozwala na efektywne zarządzanie wieloma żądaniami bez konieczności tworzenia wielu wątków.

Podsumowując, async/await w C# są niezwykle przydatnymi mechanizmami, które umożliwiają programowanie asynchroniczne w sposób bardziej wydajny i czytelny. Pozwalają na skuteczne zarządzanie operacjami I/O-zależnymi, zapewniając responsywność aplikacji i lepszą wydajność.

## YouTube

*https://www.youtube.com/watch?v=LL9GEAY_Dlo&t=310s*