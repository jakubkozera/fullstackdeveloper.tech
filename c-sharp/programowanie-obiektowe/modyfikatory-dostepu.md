# Modyfikatory dostępu

todo by you
W języku C# istnieje 4 lub 5 modyfikatorów dostępu: 

1. public
2. private
3. protected
4. internal
5. file

1. public: Klasa lub element, który jest oznaczony jako public jest dostępny z każdego miejsca w kodzie.

2. private: Klasa lub element, który jest oznaczony jako private jest dostępny tylko wewnątrz klasy, w której został zdefiniowany.

3. protected: Klasa lub element, który jest oznaczony jako protected jest dostępny tylko wewnątrz klasy i w klasach pochodnych.

4. internal: Klasa lub element, który jest oznaczony jako internal jest dostępny tylko wewnątrz bieżącego projektu.

inna opcja to:

https://learn.microsoft.com/pl-pl/dotnet/csharp/language-reference/keywords/accessibility-levels

public	Dostęp nie jest ograniczony.
protected	Dostęp jest ograniczony do zawierającej klasy lub typów pochodzących z klasy zawierającej.
internal	Dostęp jest ograniczony do bieżącego zestawu.
protected internal	Dostęp jest ograniczony do bieżącego zestawu lub typów pochodzących z zawierającej klasy.
private	Dostęp jest ograniczony do typu zawierającego.
private protected	Dostęp jest ograniczony do zawierającej klasy lub typów pochodzących z klasy zawierającej w bieżącym zestawie.


Warto pamiętać, że modyfikatory dostępu służą do ochrony danych i kontrolowania dostępności kodu, co pozwala na zachowanie odpowiedniej spójności i bezpieczeństwa danych w aplikacji.

