# Obsługa plików tekstowych


W języku C# klasa `File` udostępnia wiele przydatnych metod i funkcji, które umożliwiają programistom manipulowanie plikami tekstowymi. Klasyfikowana jako część przestrzeni nazw `System.IO`, klasa `File` zapewnia prosty i wygodny sposób zarządzania operacjami na plikach. W tym artykule przyjrzymy się różnym metodom dostępnym w klasie File oraz omówimy ich zastosowania i różnice.

Oto kilka ważnych metod dostępnych w klasie `File`:

1. `ReadAllText(string path)` - Ta metoda umożliwia odczytanie zawartości pliku tekstowego o podanej ścieżce i zwraca ją jako ciąg znaków (string). Przykład użycia:

```csharp
string content = File.ReadAllText("ścieżka_do_pliku.txt");
```

2. `WriteAllText(string path, string contents)` - Ta metoda umożliwia zapisanie zawartości podanego ciągu znaków do pliku tekstowego o podanej ścieżce. Jeśli plik już istnieje, zostanie zastąpiony nową zawartością. Przykład użycia:

```csharp
string content = "To jest przykładowa zawartość pliku.";
File.WriteAllText("ścieżka_do_pliku.txt", content);
```

3. `AppendAllText(string path, string contents)` - Ta metoda umożliwia dodanie podanego ciągu znaków na końcu istniejącego pliku tekstowego o podanej ścieżce. Przykład użycia:

```csharp
string additionalContent = "To jest dodatkowa zawartość.";
File.AppendAllText("ścieżka_do_pliku.txt", additionalContent);
```

4. `ReadAllLines(string path)` - Ta metoda odczytuje wszystkie linie z pliku tekstowego o podanej ścieżce i zwraca je jako tablicę ciągów znaków (string[]). Przykład użycia:

```csharp
string[] lines = File.ReadAllLines("ścieżka_do_pliku.txt");
```

5. `WriteAllLines(string path, string[] contents)` - Ta metoda zapisuje każdy element tablicy ciągów znaków jako oddzielną linię w pliku tekstowym o podanej ścieżce. Przykład użycia:

```csharp
string[] lines = { "Linia 1", "Linia 2", "Linia 3" };
File.WriteAllLines("ścieżka_do_pliku.txt", lines);
```

Różnice między tymi metodami:

- ReadAllText() i WriteAllText() operują na zawartości pliku jako pojedynczy ciąg znaków, podczas gdy ReadAllLines() i WriteAllLines() operują na linie jako tablicę ciągów znaków.
- WriteAllText() zastępuje istniejącą zawartość pliku, podczas gdy AppendAllText() dodaje now

ą zawartość na końcu pliku.
- ReadAllLines() zwraca zawartość pliku jako tablicę linii, podczas gdy ReadAllText() zwraca całą zawartość jako jeden ciąg znaków.

Klasa File w języku C# dostarcza prostych i wygodnych metod do obsługi plików tekstowych. Dzięki tym metodom programiści mogą łatwo czytać, zapisywać, dodawać i modyfikować zawartość plików tekstowych. Należy jednak pamiętać, że operacje na plikach mogą wiązać się z ryzykiem utraty danych, dlatego zawsze warto stosować odpowiednie zabezpieczenia, takie jak obsługa wyjątków i sprawdzanie poprawności ścieżek plików.

## Wyświetlanie plików tesktowych z folderu

Aby przejść po wszystkich plikach tekstowych w danym folderze, można skorzystać z metody `Directory.GetFiles()` w połączeniu z pętlą. Oto przykładowy kod, który ilustruje ten proces:

```csharp
string folderPath = "ścieżka_do_folderu";

// Pobierz wszystkie pliki tekstowe z podanego folderu
string[] files = Directory.GetFiles(folderPath, "*.txt");

// Przejdź po wszystkich plikach
foreach (string file in files)
{
    // Wykonaj operacje na pliku
    Console.WriteLine("Nazwa pliku: " + Path.GetFileName(file));
    Console.WriteLine("Ścieżka pliku: " + file);
    Console.WriteLine("Zawartość pliku:");
    Console.WriteLine(File.ReadAllText(file));
    Console.WriteLine("--------------------------------------");
}
```

W powyższym przykładzie, `folderPath` to ścieżka do folderu, w którym znajdują się pliki tekstowe. Metoda `Directory.GetFiles()` zwraca tablicę zawierającą wszystkie pliki spełniające określony wzorzec, w tym przypadku pliki tekstowe (o rozszerzeniu ".txt").

Następnie, używając pętli `foreach`, iterujemy po wszystkich znalezionych plikach. Wewnątrz pętli można wykonywać dowolne operacje na poszczególnych plikach. W powyższym przykładzie wyświetlamy nazwę pliku, ścieżkę pliku oraz jego zawartość.

Dzięki temu kodowi można łatwo przejść przez wszystkie pliki tekstowe w określonym folderze i wykonać na nich odpowiednie operacje.

## YouTube

*https://www.youtube.com/watch?v=L9pghTjNcmo*