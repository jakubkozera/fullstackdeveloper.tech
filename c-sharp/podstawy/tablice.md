# Tablice

Tablice to w C# struktury, które pozwalają na przechowywanie wielu wartości tego samego typu w jednej zmiennej. Można je porównać do skrzynek pocztowych, w których można umieścić wiele listów, z tym że w przypadku tablic przechowujemy wiele wartości. 

Dla przykładu, gdybyś chciał przechować wyniki testów matematycznych dla pięciu uczniów, to zamiast tworzyć pięć różnych zmiennych dla każdego wyniku, można by utworzyć jedną tablicę i zapisać wyniki w niej.

Tablice w C# są numerowane od 0, czyli pierwszy element znajduje się pod indeksem 0, drugi pod indeksem 1 i tak dalej. Aby uzyskać dostęp do konkretnego elementu tablicy, musimy użyć jego indeksu.

Poniżej przedstawiam prosty przykład, który ilustruje tworzenie i używanie tablic:

```csharp
// deklaracja i inicjalizacja tablicy
int[] wyniki = { 85, 72, 96, 68, 90 };

// wyświetlanie wartości w tablicy
Console.WriteLine("Wyniki testów:");
Console.WriteLine("Uczeń 1: " + wyniki[0]);
Console.WriteLine("Uczeń 2: " + wyniki[1]);
Console.WriteLine("Uczeń 3: " + wyniki[2]);
Console.WriteLine("Uczeń 4: " + wyniki[3]);
Console.WriteLine("Uczeń 5: " + wyniki[4]);
```

W tym przykładzie tworzymy tablicę `wyniki`, która zawiera wyniki pięciu uczniów. Następnie wyświetlamy wartości w tablicy za pomocą indeksów.

Samą deklarację i inicjalizację tablicy: `int[] wyniki = { 85, 72, 96, 68, 90 };` możemy rozbić na: samą definicje, inicjalizację tablicy, a następnie inicjalizacje, każdego z 5 elementów w następujący sposób:


```csharp
int[] wyniki;         // deklaracja zmiennej typu int[] o nazwie "wyniki"
wyniki = new int[5];  // utworzenie tablicy o rozmiarze 5 i przypisanie jej do zmiennej "wyniki"
wyniki[0] = 85;       // inicjalizacja pierwszego elementu tablicy wartością 85
wyniki[1] = 72;       // inicjalizacja drugiego elementu tablicy wartością 72
wyniki[2] = 96;       // inicjalizacja trzeciego elementu tablicy wartością 96
wyniki[3] = 68;       // inicjalizacja czwartego elementu tablicy wartością 68
wyniki[4] = 90;       // inicjalizacja piątego elementu tablicy wartością 90
```

W pierwszej linii kodu deklaruję zmienną `wyniki` jako tablicę liczb całkowitych (`int[]`). Następnie w drugiej linii tworzę nową tablicę o rozmiarze 5 przy pomocy słowa kluczowego `new`, a wynik przypisuję do zmiennej `wyniki`.

Kolejne pięć linii kodu inicjalizuje kolejne elementy tablicy wartościami, odwołując się do nich po indeksach: pierwszy element ma indeks 0, drugi 1 itd. Po inicjalizacji wartości wszystkich elementów, zmienna `wyniki` będzie zawierać tablicę o wartościach `{85, 72, 96, 68, 90}`.

## Modyfikacja tablic

Korzystając z tablic, istotny jest fakt, że są one statycznej długości. Po inicjalizacji tablicy, będzie ona zawsze przechowywała określoną liczbę elementów. Nie będziemy mogli tej liczby, ani zmniejszać - poprzez usuwanie elementów z tablicy, ani powiększać - dodając nowe elementy do tablicy.

Przykładowo, jeżeli sprobowalibyśmy odnieść się do element z indeksem 5, tablicy `wyniki` i przypisać do niego jakąś wartość: `wyniki[5] = 39;`, to ten kawałek kodu wyrzuci wyjątek podczas działania pogramu (runtime) o nazwie *IndexOutOfRangeException*.

Możemy natomiast zmieniać wartości pod konkretnymi indeksami tablicy. Aby zmienić wartość w tablicy, należy odwołać się do elementu tablicy, którego wartość chcemy zmienić, i przypisać mu nową wartość. Na przykład:

```csharp
int[] tablica = { 1, 2, 3 };
tablica[1] = 4;
Console.WriteLine(tablica[1]); // wypisze: 4, mimo, że początkowo pod tym indeksem była wartość 2
```

W tym przykładzie tworzymy tablicę `tablica`, która zawiera trzy liczby całkowite. Następnie zmieniamy wartość drugiego elementu na 4 i wypisujemy go na ekran.

O czym również warto pamiętać, to silne typowanie elementów tablicy. W tablicy typu `int[]`, nie będziemy mieć możliwości dodania elementu typu `string`. Przykładowo:

`int[] wyniki = { 8, "7", 6 };` wyrzuci wyjątek już podczas budowania programu, informując że wartość typu `string`, nie możemy przpisać do tablicy `int[]`

## YouTube

*https://www.youtube.com/watch?v=82e-eymInHs*