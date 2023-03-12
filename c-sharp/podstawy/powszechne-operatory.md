# Powszechne operatory

Operatory w C# to specjalne znaki lub słowa kluczowe, które służą do wykonywania różnych operacji na zmiennych, stałych i obiektach. Są one podstawowymi budulcami języka programowania, ponieważ pozwalają na wykonywanie różnych operacji matematycznych, porównań i manipulacji na danych.

Operatory w C# umożliwiają wykonywanie zadań, takich jak dodawanie, odejmowanie, mnożenie, dzielenie, porównywanie wartości, łączenie wartości logicznych, operacje na bitach, itp. Używanie operatorów zamiast ręcznego wykonywania operacji na zmiennych znacznie ułatwia programowanie i sprawia, że kod jest bardziej czytelny i zwięzły.

Istnieje wiele różnych operatorów, a każdy z nich ma określony priorytet i łączność, co wpływa na kolejność wykonywania operacji. Dlatego ważne jest, aby znać różne operatory i ich zasady działania, aby pisać skuteczny i efektywny kod.

## Przykładowe operatory

1. Przypisania: używane do przypisywania wartości do zmiennych lub właściwości. Przykładowo: `=, +=, -=, *=, /=`.
    ```
    int i = 1;
    i+=2; // po tej operacji zmienna i zostanie zwiększona o 2
    ```

2. Arytmetyczne: używane do wykonywania operacji matematycznych, takich jak dodawanie, odejmowanie, mnożenie i dzielenie. Przykładowo: `+, -, *, /, % (reszta z dzielenia)`.

    ```
    int i = 1;
    int j = i + 2;
    ```

3. Porównania: używane do porównywania wartości, takich jak równość, nierówność, większość, mniejszość i ich warianty. Przykładowo: `==, !=, >, <, >=, <=`. Operatory te zwracają wartość logiczną `(bool) [true/false]`

    ```
    int max = 10;
    int current = 9;

    bool currentGreaterThanMax = current > max;
    ```

4. Logiczne: używane do łączenia wyrażeń logicznych i sprawdzania, czy są prawdziwe lub fałszywe. Przykładowo: `&&` (and), `||` (or), `!` (not).

    Operator `&&` zwróci wartość `true`, jeżeli oba argumenty są równe wartości `true`, w przeciwnym wypadku zwróci wartość `false`.


    Operator `||` zwróci wartość `true`, jeżeli conajmniej jeden argument jest równy wartości `true`, w przeciwnym wypadku zwróci wartość `false`.
    ```
    bool isOverEighteen = false;
    bool hasParentalApprove = true;

    bool canProceed = isOverEighteen || hasParentalApprove; // true
    ```
    Operator `!` zawsze zwraca przeciwną wartość argumentu. Dla wartości `true`, zwróci wartość `false` i vice versa: dla wartości `false`, zwróci wartość `true`;

    ```
    string status = "Active";
    bool isNotActive = !(status == "Active"); lub w skróconej formie 'status != "Active"

    ```


5. Inkrementacji i dekrementacji: używane do zwiększania lub zmniejszania wartości zmiennej o 1. Przykładowo: `++` (inkrementacja), `--` (dekrementacja). W zależności od pozycji argumentu (przed lub po operatorze) wartość zostanie zmienszona/zwiększona w danej linii, lub dopiero w następnej.

    Przykład **post**-inkrementacji
    ```
    int i = 1;
    i++; // i = 1 (post-inkrementacja, zwiększa wartość w następnej linii)
    // i = 2
    ```

    Przykład **pre**-inkrementacji
    ```
    int i = 1;
    ++i; // i = 2 (pre-inkrementacja, zwiększa wartość w danej linii)
    // i = 2
    ```

    W analogiczny sposób działa operator deinkrementacji `--`.

6. Warunkowe - operator trójskładnikowy, używany do tworzenia warunkowych wyrażeń, które wykonują różne instrukcje w zależności od wartości logicznej. Operator warunkowy trójskładnikowy (ternary)umożliwia wykonanie instrukcji warunkowej w jednej linii.

    ```
    string message = age >= 18 ? "Person is an adult" : "Person is a minor";
    ```
    W tym przykładzie, jeśli `age` jest większe lub równe 18, to zmianna `message` przyjmie wartość "Person is an adult", a jeśli jest mniejsze niż 18, to "Person is a minor".

    Jest to skrócona wersja przypisana wartości `message` z wykorzystaniem instrukcji `if`.
    ```
    string message;
    if(age >= 18)
    {
        message = "Person is an adult";
    }
    else
    {
        message = "Person is a minor";
    }
    ```




## YouTube
https://www.youtube.com/watch?v=d1ZyKfTAI9s