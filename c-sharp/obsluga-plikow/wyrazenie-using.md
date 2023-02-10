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


