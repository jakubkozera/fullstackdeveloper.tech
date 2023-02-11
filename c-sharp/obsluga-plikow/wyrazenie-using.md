# Wyrażenie using

Wyrażenie `using` jest używane do automatycznego zarządzania zasobami, takimi jak pliki i połączenia z bazami danych. W przypadku, gdy blok `using` zostanie zakończony, obiekt, którego użyto, zostanie automatycznie zamknięty i zwolnione zostaną jego zasoby.

## Przykład 

```
using System;
using System.IO;

namespace ConsoleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            using (StreamReader sr = new StreamReader("file.txt"))
            {
                String line = sr.ReadLine();
                Console.WriteLine(line);
            }
        }
    }
}
```

W powyższym przykładzie instrukcja `using` jest używana do otwierania pliku o nazwie „file.txt”. Obiekt `StreamReader` służy do odczytu zawartości pliku, a metoda `ReadLine` służy do odczytu pierwszej linii pliku. Po wyjściu z instrukcji `using` obiekt `StreamReader` jest automatycznie zamykany, a jego zasoby zwalniane. Gwarantuje to, że plik zostanie prawidłowo zamknięty i że wszystkie zasoby używane przez obiekt `StreamReader` zostaną odpowiednio zwolnione, nawet jeśli zostanie zgłoszony wyjątek.

## Czym jest wyrażenie using?

Wyrażenie `using` jest tak naprawdę implementacją bloku `try-finally`. Kiedy wykonywana jest instrukcja `using`, tworzony jest obiekt określony w instrukcji i wykonywany jest kod wewnątrz bloku. Po wykonaniu kodu wewnątrz bloku wykonywany jest blok `finally`. Gwarantuje to, że obiekt określony w instrukcji `using` jest usuwany i zwalniane są jego zasoby nawet jeśli zostanie zgłoszony wyjątek. Oto jak prezentowałby się powyższy przykład, bez użycia bloku `using`.


```
using System;
using System.IO;

namespace ConsoleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            StreamReader sr = new StreamReader("file.txt");
            try
            {
                String line = sr.ReadLine();
                Console.WriteLine(line);
            }
            finally
            {
                if (sr != null)
                {
                    sr.Dispose();
                }
            }
        }
    }
}
```
Instrukcja `using` zapewnia bardziej przejrzysty sposób pisania bloku `try-finally` i jest zalecanym sposobem zwalniania zasobów w języku c#.


## `IDisposable`, a wyrażenie `using`

Aby na danym obiektcie utworzyć blok using, jak w powyższym przykładzie miało to miejsce na klasie `StreamReader`, dany typ musi implementować interface `IDisposable`.

Implementując ten interface, na dowolnej klasie będziemy w stanie zwalniać zewnętrzne zasoby, z których mogłyby korzystać obiekty w naszym programie.

Poniżej znajduje się przykład implementacji tego interfejsu:

```
using System;

class ExampleClass : IDisposable
{
    private bool disposed = false;

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        if (!disposed)
        {
            if (disposing)
            {
                // Zwolnij zasoby zarządzane
            }

            // Zwolnij zasoby niezarządzane
            disposed = true;
        }
    } 
}
```

W powyższym przykładzie klasa `ExampleClass` implementuje interfejs `IDisposable`. Metoda `Dispose` jest główną metodą służącą do zwolnienia zasobów, a metoda `Dispose(bool disposing)` jest wirtualną metodą, którą można nadpisać w klasie pochodnej, aby zwolnić dodatkowe zasoby. 

W praktyce, gdy tworzysz obiekt, który zarządza zasobami, takimi jak pliki, połączenia z bazą danych itp., powinieneś implementować interfejs `IDisposable`, aby mieć pewność, że te zasoby zostaną zwolnione, gdy nie będą już potrzebne. Jest to jest ważne, ponieważ niezwolnione zasoby mogą powodować problemy z wydajnością i stabilnością aplikacji lub nawet doprowadzić do wycieku pamięci.