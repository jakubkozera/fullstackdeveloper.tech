# Pętle



Petle w języku C# to swojego rodzaju funkcje, które pozwalają na powtarzanie określonej sekwencji instrukcji wielokrotnie, aż do spełnienia określonego warunku lub przez określoną liczbę iteracji. W C# dostępne są cztery typy pętli: while, do-while, for i foreach, każda z nich służy do wykonywania określonych zadań w zależności od potrzeb programu.


## Pętla `while`

Pętla `while` w C# powtarza instrukcje w jej ciele, dopóki określony warunek jest prawdziwy. W przeciwnym razie pętla jest zakończona. Poniżej znajduje się przykład użycia pętli while w C#:

```csharp
int i = 0;
while (i < 5)
{
    Console.WriteLine(i);
    i++;
}
```

W powyższym przykładzie zmienna i jest inicjalizowana wartością 0, a następnie pętla `while` wykonuje instrukcje w ciele, dopóki i jest mniejsze niż 5. W każdej iteracji wartość zmiennej i jest zwiększana o 1, a na ekranie wyświetlana jest wartość zmiennej i. Wynikiem działania powyższego kodu będzie wyświetlenie liczb 0, 1, 2, 3 i 4.

*https://www.youtube.com/watch?v=0VOP8TC4pq0*

## Pętla `do-while`

Pętla `do-while` w C# działa podobnie do pętli while, z tą różnicą, że warunek jest sprawdzany po wykonaniu instrukcji w ciele pętli. Oznacza to, że instrukcje w ciele pętli są wykonywane co najmniej raz, niezależnie od wartości warunku. Poniżej znajduje się przykład użycia pętli `do-while` w C#:

```csharp
int j = 0;
do
{
    Console.WriteLine(j);
    j++;
} while (j < 5);
```

W powyższym przykładzie zmienna j jest inicjalizowana wartością 0, a następnie instrukcje w ciele pętli są wykonywane, dopóki j jest mniejsze niż 5. W każdej iteracji wartość zmiennej j jest zwiększana o 1, a na ekranie wyświetlana jest wartość zmiennej j. Wynikiem działania powyższego kodu będzie wyświetlenie liczb 0, 1, 2, 3 i 4.

*https://www.youtube.com/watch?v=0P86Equ77Nk*

## Pętla `for`

Pętla `for` w C# pozwala na określenie liczby iteracji, w których instrukcje w ciele pętli będą wykonywane.

Składnia pętli `for` w C# jest następująca:

```csharp
for (inicjalizacja; warunek; inkrementacja/dekrementacja)
{
    // instrukcje do wykonania
}
```

Zmienna, która jest inicjalizowana w sekcji inicjalizacji, jest zwykle używana jako licznik iteracji pętli. Warunek określa, kiedy pętla powinna się zakończyć, a inkrementacja/dekrementacja określa, jak wartość zmiennej licznika powinna być zmieniana w każdej iteracji. Poniżej znajduje się przykład użycia pętli `for` w C#:

```csharp
for (int k = 0; k < 5; k++)
{
    Console.WriteLine(k);
}
```

W powyższym przykładzie zmienna k jest inicjalizowana wartością 0, a następnie pętla `for` wykonuje instrukcje w ciele, dopóki k jest mniejsze niż 5. W każdej iteracji wartość zmiennej k jest zwiększana o 1, a na ekranie wyświetlana jest wartość zmiennej k. Wynikiem działania powyższego kodu będzie wyświetlenie liczb 0, 1, 2, 3 i 4.

*https://www.youtube.com/watch?v=Nd28PoctXCg*

## Pętla `foreach`

Pętla `foreach` w C# służy do iterowania po kolekcjach, takich jak tablice, listy, słowniki, itp. Składnia pętli `foreach` w C# jest następująca:

```csharp
foreach (typ elementu in kolekcja)
{
    // instrukcje do wykonania
}
```

Typ elementu musi być tym samym typem, co typ elementów w kolekcji. W każdej iteracji pętli, element jest przypisywany do zmiennej o nazwie elementu, a instrukcje w ciele pętli są wykonywane. Poniżej znajduje się przykład użycia pętli foreach w C#:

```csharp
int[] tablica = { 1, 2, 3, 4, 5 };
foreach (int element in tablica)
{
    Console.WriteLine(element);
}
```

W powyższym przykładzie pętla foreach iteruje po tablicy tablica, a w każdej iteracji wartość elementu jest przypisywana do zmiennej o nazwie element. Instrukcje w ciele pętli wyświetlają wartość elementu na ekranie. Wynikiem działania powyższego kodu będzie wyświetlenie liczb 1, 2, 3, 4 i 5.

*https://www.youtube.com/watch?v=aW4XFmd-Pkc*

## Podsumowanie

Pętle w języku C# są używane wtedy, gdy chcemy powtarzać określone instrukcje wielokrotnie. Są one często stosowane w programowaniu, ponieważ pozwalają na automatyzację powtarzających się zadań, co z kolei zwiększa wydajność i poprawia jakość kodu.

Istnieją różne sytuacje, w których pętle są szczególnie przydatne. Na przykład, gdy chcemy wykonać jakieś zadanie określoną ilość razy lub kiedy nie wiemy, ile razy chcemy wykonać zadanie, ale chcemy zakończyć po spełnieniu pewnego warunku. Poniżej przedstawiamy kilka przykładów, kiedy używa się pętli:

1. Przetwarzanie danych: Pętle są szczególnie przydatne, gdy chcemy przetworzyć dużą ilość danych. Na przykład, gdy mamy do czynienia z dużą liczbą rekordów w bazie danych, możemy użyć pętli do powtarzania określonych operacji dla każdego rekordu.

2. Wprowadzanie danych: Pętle są również przydatne, gdy chcemy umożliwić użytkownikowi wprowadzenie dużej ilości danych. Na przykład, gdy tworzymy program do wprowadzania danych dotyczących klientów, możemy użyć pętli do pobierania danych dla każdego klienta.

3. Obsługa plików: Pętle są również używane w przypadku przetwarzania plików. Na przykład, gdy chcemy przetworzyć wszystkie pliki w określonym katalogu, możemy użyć pętli do iteracji po wszystkich plikach i wykonania określonych operacji na każdym z nich.

4. Algorytmy: Pętle są niezbędne w algorytmach, w których musimy wykonać określone operacje wiele razy. Na przykład, gdy tworzymy program do sortowania danych, możemy użyć pętli do powtarzania operacji sortowania dla każdego elementu.

Podsumowując, pętle są niezbędne w programowaniu, gdy chcemy wykonać określone zadanie wielokrotnie lub gdy nie wiemy, ile razy musimy wykonać zadanie, ale chcemy zakończyć je po spełnieniu pewnego warunku. W języku C# dostępnych jest kilka typów pętli, które pozwalają na osiągnięcie tego celu w sposób prosty i efektywny.


