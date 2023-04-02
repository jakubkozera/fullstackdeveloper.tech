# Interakcje z konsolą

## Wstęp

Zanim zaczniesz tworzyć aplikacje webowe, desktopowe czy mobilne, to najłatwieszym sposobem na interakcje z programem jest komunikacja poprzez konsole. W konsoli, w bardzo prosty sposób będziemy w stanie wyświetlać wiadomości, czy też przez konsolę będziemy przesyłać informacje do programu. 

Aby móc wykonać interakcje z konsolą w języku C#, należy użyć klasy `System.Console` 

## Wyświetlanie tekstu

```

 Console.WriteLine("Tekst, który chcesz wyświetlić");
 Console.Write("");

```

> Do użycia klasy `Console` w powyższy sposób, musisz najpierw wskazać kompilatorowi korzystanie z przestrzeni nazw `System`, poprzez dodanie `using System;` na samej górze pliku c-sharp.


Aby wyświetlić informacje w konsoli, mamy do dyspozycji dwie metody `Console.WriteLine()` oraz `Console.Write()`. Różnica między nimi polega na tym, że metoda `WriteLine` powróci do nowej linii w konsoli, podczas gdy metoda `Write` zostawi kursor na miejscu.

## Odczytywanie danych wprowadzonych przez użytkownika

```

string userName = Console.ReadLine();

```

Do odczytu danych wejściowych od użytkownika używa się metody `Console.ReadLine()`.

W powyższym przykładzie zostanie utworzona zmienna o nazwie `userName` typu `string`, do której zostanie przypisana wartość wprowadzona przez użytkownika.

## YouTube
test
*https://www.youtube.com/watch?v=XXZ64uxg2_g*