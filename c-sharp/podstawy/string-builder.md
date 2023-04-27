# StringBuilder 

`StringBuilder` jest klasą, która pozwala na wydajne modyfikowanie ciągów znaków i znajduje się w przestrzeni nazw `System.Text`. Jest stosowana, gdy potrzeba wykonać wiele operacji na ciągu znaków, takich jak dodawanie, wstawianie lub usuwanie znaków. Zamiast tworzyć nowy obiekt typu `string` dla każdej operacji (co spowodowałoby alokacje nowej pamięci, za każdym razem gdy zmieniamy wartość typu `string`), `StringBuilder` modyfikuje swój wewnętrzny bufor, co może poprawić wydajność programu. 

## Przykład 

```
using System;
using System.Text;

class Program
{
    static void Main(string[] args)
    {
        StringBuilder sb = new StringBuilder();

        // Dodawanie ciągów znaków do StringBuilder
        sb.Append("Hello world!");

        // Usuwanie ciągu znaków
        sb.Remove(6, 6);

        // Wstawianie ciągu znaków w określonym miejscu
        sb.Insert(6, "You!");

        // Pobieranie ciągu znaków z StringBuilder
        string result = sb.ToString();

        // Wypisanie wyniku
        Console.WriteLine(result); //Hello You!
    }
}
```

W powyższym przykładzie tworzymy nowy obiekt `StringBuilder`, następnie dodajemy "Hello world!" do niego za pomocą metody `Append`. Potem usuwamy 6 znaków od pozycji 6 przy pomocy metody `Remove`. Kolejny krok to wstawienie "You!" na pozycji 6 dzięki metodzie `Insert`. Na koniec pobieramy ciąg znaków przy pomocy metody `ToString` i wypisujemy wynik na konsoli.

## Kiedy stosować String a kiedy StringBuilder

Jeżeli przewidujemy, że ciąg znaków będzie często modyfikowany, warto rozważyć użycie klasy `StringBuilder` zamiast `String`.

Na przykład, jeśli masz pętlę, w której każdy przebieg dodaje nowy ciąg znaków do istniejącego ciągu znaków, to użycie `StringBuilder` może znacznie poprawić wydajność, ponieważ `StringBuilder` modyfikuje swój wewnętrzny bufor, a nie tworzy nowego obiektu ciągu znaków dla każdej operacji.

Z drugiej strony, jeśli nie planujesz modyfikować ciągu znaków i tylko odczytywać lub przechowywać stały ciąg znaków, `String` jest lepszym wyborem. `String` jest niezmienną klasą, co oznacza, że ​​po utworzeniu ciągu znaków, nie można go zmienić. Jest to przydatne, jeśli chcesz mieć pewność, że ciąg znaków nie zostanie zmieniony przez błąd w kodzie.

## YouTube

*https://www.youtube.com/watch?v=CIUnlNucU0o*