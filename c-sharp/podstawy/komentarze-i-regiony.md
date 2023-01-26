# Komentarze i regiony

## Komentarze jednoliniowe 


Komentarze jednoliniowy jest tworzony przez umieszczenie dwóch ukośników `//` przed treścią komentarza.

```
class Program
{
    static void Main(string[] args)
    {
        // Komentarz jednoliniowy
        Console.WriteLine("Hello world!");
    }
}
```


## Komentarze wieloliniowe

Komentarz wieloliniowy jest tworzony przez umieszczenie symbolu `/*` na początku komentarza i symbolu `*/` na jego końcu.

```
class Program
{
    static void Main(string[] args)
    {
        /* To
        jest
        komentarz 
        wielolinowy */
        Console.WriteLine("Hello world!");
    }
}
```

Trzeba jednak pamiętać o tym, że kod powinien być tak napisany, aby jego działanie było jasne i zrozumiałe bez konieczności czytania komentarzy lub dokumentacji. Oznacza to, że zmiennym i funkcjom powinny być nadawane sensowne nazwy opisujące w czytelny sposób do czego służą. 

Zbyt duża ilość komentarzy zaciemni kod i sprawi, że będzie go ciężej utrzymać i rozwijać.

## Regiony

Regiony to specjalne komentarze wieloliniowe, które pozwalają na grupowanie kodu w logiczne bloki. Służą do organizacji kodu i ułatwiają nawigację po nim. Regiony są tworzone dzięki użyciu słów kluczowych `#region` i `endregion`.

```

class Program
{
    static void Main(string[] args)
    {
        #region Zmienne
        int a = 10;
        int b = 20;
        #endregion

        #region Obliczenia
        int c = a + b;
        Console.WriteLine("Suma a i b wynosi: " + c);
        #endregion
    }
}
```
W powyższym przykładzie utworzono dwa regiony o nazwach "Zmienne" i "Obliczenia".