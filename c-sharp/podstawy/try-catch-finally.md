# Instrukcja try-catch-finally

Instrukcja `try-catch-finally` jest wykorzystywana do obsługi wyjątków. Blok `try` zawiera kod, który może zgłosić wyjątek i jest wykonywany dopóki nie zostanie pomyślnie wykonany lub zostanie zgłoszony wyjątek. Blok `catch` określa w jaki sposób obsłużyć wyjątek. Dobrą praktyką jest przechwytywanie jak najbardziej szczegółowych typów wyjątków zamiast ogólnego typu wyjątku, aby można było go obsłużyć w bardziej odpowiedni sposób. Możliwe jest użycie więcej niż jednej klauzuli `catch`, w takiej sytuacji klauzule są badane w kolejności, dlatego znaczenie ma ich kolejność.  Kod zawarty w bloku `finally` zostanie wykonany niezależnie od tego, czy został zgłoszony wyjątek, czy nie i stosowany jest na przykład do zwalniania zasobów. 

## Przykład

```
class Program
{
    static void Main(string[] args)
    {
        FileStream file = null;
        try
        {
            file = new FileStream("file.txt", FileMode.Open);
            // Read or write to the file
        }
        catch (IOException e)
        {
            Console.WriteLine("An error occurred while reading or writing to the file.");
        }
        finally
        {
            // This code will always be executed

            if (file != null)
            {
                file.Close();
            }
        }
    }
}

```

W tym przykładzie obiekt `FileStream` jest tworzony w bloku `try` w celu otwarcia pliku do odczytu lub zapisu. Jeśli wyjątek `IOException` zostanie zgłoszony podczas odczytu lub zapisu do pliku, blok `catch` obsłuży wyjątek i wyświetli komunikat. Blok `finally` zostanie wykonany niezależnie od tego, czy został zgłoszony wyjątek, czy nie, a służy do zamknięcia obiektu `FileStream` i zwolnienia powiązanych z nim zasobów.

todo - should using be described in that place?
Możliwe jest również użycie instrukcji `using`, która automatycznie zwolni zasoby po użyciu.
