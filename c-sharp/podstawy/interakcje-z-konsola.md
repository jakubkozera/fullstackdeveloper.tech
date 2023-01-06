# Interakcje z konsolą

Aby móc wykonać interakcje z konsolą w języku C#, należy użyć klasy `System.Console.` 

## Wyświetlanie tekstu

```

 Console.WriteLine("Tekst, który chcesz wyświetlić");
 Console.Write("");

```

Aby wyświetlić informacje w konsoli, mamy do dyspozycji dwie metody `Console.WriteLine()` oraz `Console.Write()`. Różnica między nimi polega na tym, że metoda `WriteLine` powróci do nowej linii w konsoli, podczas gdy metoda `Write` zostawi kursor na miejscu.

## Odczytywanie danych wprowadzonych przez użytkownika

```

string userName = console.ReadLine();

```

Do odczytu danych wejściowych od użytkownika używa się metody `Console.ReadLine()`.

W powyższym przykładzie zostanie utworzona zmienna o nazwie `userName` typu `string`, do której zostanie przypisana wartość wprowadzona przez użytkownika.
