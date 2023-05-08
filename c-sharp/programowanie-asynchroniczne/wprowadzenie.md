# Programowanie asynchroniczne wprowadzenie

todo 

Programowanie asynchroniczne polega na tworzeniu kodu, który może wykonywać wiele zadań jednocześnie, bez blokowania głównego wątku programu. Dzięki temu pozwala na bardziej wydajne wykorzystanie zasobów systemowych oraz zapobiega zacinaniu się interfejsu użytkownika.

Programowanie asynchroniczne w C# można realizować za pomocą:

1. Zastosowanie `async/await` - słowo kluczowe `async` oznacza metodę jako asynchroniczną, a słowo kluczowe `await` umożliwia oczekiwanie na zakończenie asynchronicznej metody bez blokowania wątku.

2. Delegaty asynchroniczne - pozwala na asynchroniczne wywoływanie metod bez użycia słowa kluczowego `async` i metody `await`. Zamiast tego, delegat asynchroniczny zwraca obiekt typu `IAsyncResult`, który może być użyty do asynchronicznego oczekiwania na zakończenie metody.
https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/asynchronous-programming-using-delegates 


TPL - parallel programming - not here
 https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/task-based-asynchronous-programming
3. Biblioteka `Parallel` - biblioteka ta pozwala na równoległe wykonywanie zadań za pomocą wielu wątków. Pozwala na asynchroniczne wykonywanie zadań, które można wykonać niezależnie od siebie, w celu zwiększenia wydajności i przyspieszenia działania aplikacji.

https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/async-scenarios 

## YouTube

*https://www.youtube.com/watch?v=LL9GEAY_Dlo&t=3s* 