# Regex

Regex to inaczej wyrażenie regularne, czyli zbiór zasad pozwalający na wyszukiwanie ciągów tekstowych zgodnych z określonym wzorcem.

W języku C#, regex jest dostępny jako klasa w przestrzeni nazw `System.Text.RegularExpressions`. Dzięki jej użyciu można sprawdzać czy dany ciąg tekstowy jest zgodny z podanym wzorcem, znajdować w tekście fragmenty spełniające taki wzorzec, a także zamieniać je na inne ciągi tekstowe.

## Przykład 


```
using System;
using System.Text.RegularExpressions;

class RegexExample
{
    static void Main()
    {
        string phoneNumber = "+48555666777";
        string pattern = @"^\\+?[1-9][0-9]{7,14}$";

        bool isPhoneNumber = Regex.IsMatch(phoneNumber, pattern);

        Console.WriteLine(isPhoneNumber); // Output: true
    }
}

```

W tym przykładzie, utworzyliśmy zmienną `phoneNumber` zawierającą przykładowy numer telefonu. Następnie utworzyliśmy zmienną `pattern` zawierającą wzorzec numeru telefonu (w postaci wyrażenia regularnego). Wzorzec ten jest używany przez metodę `IsMatch` klasy `Regex`, aby sprawdzić, czy ciąg tekstowy `phoneNumber` jest zgodny z tym wzorcem. W wyniku tego, zmienna `isPhoneNumber` jest true, ponieważ numer telefonu jest poprawny.