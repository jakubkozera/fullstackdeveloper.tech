# Słowo kluczowe var

Słowo kluczowe `var` służy do deklarowania zmiennej, której typ jest określony przez wartość przypisaną do niej podczas inicjalizacji. W przeciwieństwie do tradycyjnego podejścia, w którym musisz określić typ zmiennej w momencie jej deklaracji, słowo kluczowe `var` pozwala na automatyczne określenie typu na podstawie wartości przypisanej do zmiennej.

## Przykład

```
var age = 30; // Zmienna "age" jest typu int
var name = "John"; // Zmienna "name" jest typu string
var myList = new List<int>(); // Zmienna "myList" jest typu List<int>
```

> Zmienna zadeklarowana za pomocą słowa kluczowego `var` musi być zainicjalizowana wartością w momencie deklaracji, inaczej program nie skompiluje się.
