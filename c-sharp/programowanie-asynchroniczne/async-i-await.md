# Async i await

W C# asynchroniczne programowanie można realizować za pomocą słowa kluczowego `async` oraz metody `await`. Kiedy metoda oznaczona jest jako `async`, oznacza to, że może ona wykonywać operacje asynchroniczne. Metoda ta może zawierać wywołania innych metod, które również są oznaczone jako `async`.

Kiedy wywołujemy metodę oznaczoną jako `async`, możemy ją oczekiwać za pomocą metody `await`. Metoda `await` umożliwia programowi kontynuowanie działania, dopóki nie zostanie zakończone wykonywanie metody `async`, na którą czekamy. W tym czasie program może wykonywać inne operacje.

Przykładowo, jeśli chcemy pobrać dane z internetu w sposób asynchroniczny, możemy użyć metody `HttpClient.GetAsync` oznaczonej jako `async`. Następnie, zamiast czekać na zakończenie pobierania danych, możemy kontynuować działanie programu, aż dane zostaną pobrane. Gdy dane zostaną pobrane, program wróci do funkcji, która zawierała wywołanie asynchroniczne i kontynuuje jej wykonanie.

## Przykład
```
async Task DownloadFileAsync()
{
    HttpClient client = new HttpClient();
    HttpResponseMessage response = await client.GetAsync("http://www.example.com/file.zip");
    byte[] data = await response.Content.ReadAsByteArrayAsync();
    // Zapisz pobrane dane do pliku
}
```

W powyższym przykładzie metoda `DownloadFileAsync` pobiera plik z internetu za pomocą metody `HttpClient.GetAsync`. Następnie wykorzystuje metodę `await`, aby oczekiwać na pobranie pliku. Kiedy pobieranie zostanie zakończone, pobrane dane są zapisywane do pliku.

