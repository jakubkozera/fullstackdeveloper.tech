# Instrukcja if-else

Instrukcja warunkowa `if-else` służy do wykonywania różnych fragmentów kodu w zależności od spełnienia określonego wyrażenia logicznego zawartego w instrukcji `if` oraz ewentualnego polecenia `else`, gdy warunek ten nie zostanie spełniony.

## Syntax `if-else`

Aby w prawidłowy sposób utworzyć instrukcję warunkową `if-else`, musimy ją zapisać w prawidłowym syntaxie:


```
if (wyrażenie logiczne)
{
    // kod do wykonania, jeśli wyrażenie jest prawdziwe
}
else
{
    // kod do wykonania, jeśli wyrażenie jest fałszywe
}
```

Jeśli wyrażenie logiczne jest prawdziwe, to zostanie wykonany kod zawarty między nawiasami klamrowymi po słowie kluczowym `if`. Jeśli natomiast jest fałszywe, to zostanie wykonany kod zawarty między nawiasami klamrowymi po słowie kluczowym else.

## else if

Możliwe jest także użycie instrukcji else if pozwala na sprawdzenie kilku warunków sekwencyjnie.

```
if (warunek1)
{
    // kod do wykonania, jeśli warunek1 jest prawdziwy
}
else if (warunek2)
{
    // kod do wykonania, jeśli warunek1 jest fałszywy, a warunek2 jest prawdziwy
}
else
{
    // kod do wykonania, jeśli oba warunki są fałszywe
}


```



## Przykład użycia instrukcji if-elseif-else 


```
int x = 5;

if (x > 10)
{
    Console.WriteLine("x jest większe niż 10");
}
else if (x == 10)
{
    Console.WriteLine("x jest równe 10");
}
else
{
    Console.WriteLine("x jest mniejsze niż 10");
}

```

W powyższym przykładzie, zmienna x jest porównywana z wartością 10. Jeśli jest większa, to zostanie wyświetlone "x jest większe niż 10", jeśli jest równa 10, to zostanie wyświetlone "x jest równe 10", a jeśli żaden z tych warunków nie został spełniony to wykonywanie kodu trafi do instrukcji `else` i w konsoli zostanie wypisana wiadomość "x jest mniejsze niż 10" 

 ## YouTube
https://www.youtube.com/watch?v=yf3FxjDCfqQ 