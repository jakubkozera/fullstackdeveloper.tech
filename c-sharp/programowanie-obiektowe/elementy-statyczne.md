# Elementy statyczne

Właściwości statyczne w języku C# to właściwości, które są powiązane z samą klasą, a nie z jej instancjami. Oznacza to, że właściwość statyczna jest jedna dla wszystkich obiektów tej samej klasy, a nie jedna dla każdego z nich. Właściwości statyczne są używane w przypadkach, gdy dana wartość jest wspólna dla wszystkich obiektów klasy i nie powinna być różna dla poszczególnych instancji.

Aby utworzyć właściwość statyczną, należy użyć słowa kluczowego static w definicji właściwości:


```
public class Counter
{
    private static int count = 0;

    public static int Count
    {
        get { return count; }
    }

    public Counter()
    {
        count++;
    }
}
```

W powyższym przykładzie mamy klasę `Counter`, która zawiera właściwość statyczną `Count`. Właściwość ta jest jedna dla wszystkich instancji tej klasy i zawiera liczbę obiektów tej klasy, które zostały utworzone. Każdy raz, gdy tworzony jest nowy obiekt `Counter`, wartość właściwości statycznej jest zwiększana o jeden. W ten sposób możemy śledzić liczbę obiektów danej klasy w naszej aplikacji.

Wartość właściwości statycznej jest dostępna przez nazwę klasy, a nie przez nazwę instancji obiektu:

```
Counter counter1 = new Counter();
Counter counter2 = new Counter();

int total = Counter.Count; // total = 2
```

W powyższym przykładzie utworzyliśmy dwa obiekty Counter, a następnie pobraliśmy wartość właściwości statycznej Count za pomocą nazwy klasy. Wartość ta wynosi 2, co odpowiada liczbie utworzonych obiektów.

## Definicja statycznych elementów

Słowa kluczowego `static` na następujących członkach klas:

- Zmienne - można tworzyć statyczne zmienne, które są dostępne dla wszystkich instancji danej klasy.

- Właściwości - można tworzyć statyczne właściwości, które są dostępne dla wszystkich instancji danej klasy.

- Metody - można tworzyć statyczne metody, które są dostępne dla wszystkich instancji danej klasy.

- Konstruktory - można tworzyć statyczne konstruktory, które są wywoływane tylko raz przy pierwszym użyciu klasy.

- Destruktory - można tworzyć statyczne destruktory, które są wywoływane przy zakończeniu aplikacji.

Warto pamiętać, że niektóre z tych członków klas, takie jak destruktory, nie są często używane w praktyce. W przypadku właściwości statycznych i metod statycznych, są one bardziej powszechne i często używane w aplikacjach.

## Zastosowanie słowa kluczowego `static`

Właściwości statyczne w C# można wykorzystać do różnych celów, takich jak:

- Liczenie liczby obiektów danej klasy - jak w powyższym przykładzie.

- Przechowywanie danych globalnych - jeśli chcesz, aby dana wartość była dostępna dla wszystkich instancji danej klasy, możesz ją umieścić w właściwości statycznej.

- Konfiguracja aplikacji - można użyć właściwości statycznej do przechowywania danych konfiguracyjnych aplikacji, które są dostępne dla wszystkich klas w aplikacji.

- Utrzymywanie stanu aplikacji - można użyć właściwości statycznej do zapamiętywania stanu aplikacji, na przykład, aby zapamiętać, czy użytkownik jest zalogowany, czy też nie.

- Tworzenie narzędzi utility - można użyć właściwości statycznej, aby tworzyć narzędzia, które są dostępne dla wszystkich klas w aplikacji.

- Warto pamiętać, że nie należy nadużywać właściwości statycznych, ponieważ mogą one powodować problemy z testowaniem i rozwojem oprogramowania. Dlatego należy używać ich z umiarem i w odpowiednich sytuacjach.

## YouTube
https://www.youtube.com/watch?v=Ji7Jz802UZ4