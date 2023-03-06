# Słowo kluczowe var

Słowo kluczowe `var` służy do deklarowania zmiennej, której typ jest określony przez wartość przypisaną do niej podczas inicjalizacji. W przeciwieństwie do tradycyjnego podejścia, w którym musisz określić typ zmiennej w momencie jej deklaracji, słowo kluczowe `var` pozwala na automatyczne określenie typu na podstawie wartości przypisanej do zmiennej.

## Przykład

```
var age = 30; // Zmienna "age" jest typu int
var name = "John"; // Zmienna "name" jest typu string
var myList = new List<int>(); // Zmienna "myList" jest typu List<int>
```

> Zmienna zadeklarowana za pomocą słowa kluczowego `var` musi być zainicjalizowana wartością w momencie deklaracji, inaczej program nie skompiluje się.


Oto kilka zalet korzystania ze słowa kluczowego `var`:
1. Dłuższa nazwa typu nie jest wymagana: Używanie var eliminuje potrzebę określania nazwy typu zmiennej, co może zaoszczędzić czas i poprawić czytelność kodu.

2. Zmniejszenie powtarzalności kodu: Używanie `var` pozwala na zdefiniowanie zmiennej w jednej linii kodu, co może zmniejszyć powtarzalność kodu.

3. Ułatwienie przepisania kodu: Używanie `var` ułatwia przepisanie kodu między różnymi typami, ponieważ typ zmiennej jest określany automatycznie.

4. Elastyczność typów: Używanie `var` umożliwia przechowywanie różnych typów w zmiennej, co może być przydatne w przypadku, gdy typ zmiennej jest nieznany lub zmienia się dynamicznie.

5. Ułatwienie korzystania z LINQ: Korzystanie z `var` ułatwia korzystanie z LINQ, ponieważ wyrażenia LINQ zwykle zwracają anonimowe typy.

## YouTube
https://www.youtube.com/watch?v=jAm-792vipA
