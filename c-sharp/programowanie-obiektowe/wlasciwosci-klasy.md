# Właściwości klasy

Właściwości klas w języku C# to specjalne metody, które pozwalają na kontrolowanie dostępu do pól w klasie i ich wartości. Dzięki właściwościom można wykonać określone akcje w momencie odczytu lub zapisu wartości pola. Właściwości są użyteczne w wielu przypadkach, na przykład w celu ustawienia ograniczeń na wartości pola lub zabezpieczenia danych przed niepożądanymi zmianami. Poniżej przedstawimy sześć stron, w których opiszemy, czym są właściwości klas w języku C# i jak można z nich korzystać w swoich programach.

## Wprowadzenie do właściwości klas

Właściwości klas to specjalne metody, które umożliwiają kontrolowanie dostępu do pól w klasie. Właściwości pozwalają na definiowanie specjalnych zachowań, które mają miejsce w momencie odczytu lub zapisu wartości pola. Dzięki temu programista może zapewnić bezpieczeństwo i poprawność danych przechowywanych w klasie oraz ułatwić korzystanie z klasy innym programistom.

Właściwości w C# składają się z dwóch metod - `get` i `set`. Metoda get służy do odczytu wartości pola, natomiast metoda set służy do zapisu wartości do pola. Oto przykład prostej klasy z jednym polem i dwoma właściwościami:

```
public class Person
{
    private string name;

    public string Name
    {
        get { return name; }
        set { name = value; }
    }

    public string Greeting
    {
        get { return "Hello, my name is " + name; }
    }
}
```

W powyższym przykładzie klasa Person posiada pole "name" oraz dwie właściwości - Name i Greeting. Właściwość Name umożliwia odczytanie i zapisanie wartości pola "name", natomiast właściwość Greeting umożliwia tylko odczytanie wartości pola.

Kontrola dostępu do właściwości
Właściwości klas pozwalają na kontrolowanie dostępu do pól w klasie. Dzięki temu można ustawić ograniczenia na wartości pola i zabezpieczyć dane przed niepożądanymi zmianami. Oto przykład klasy, która wykorzystuje właściwości do kontrolowania dostępu do pola:

```
public class BankAccount
{
    private decimal balance;

    public decimal Balance
    {
        get { return balance; }
        private set
        {
            if (value < 0)
            {
                throw new ArgumentException("Balance cannot be negative");
            }
            balance = value;
        }
    }

    public void Deposit(decimal amount)
    {
        Balance += amount;
    }

    public void Withdraw(decimal amount)
    {
        Balance -= amount;
    }
}
```
W powyższym przykładzie klasa `BankAccount` została dodana kontrola dostępu do pola "balance". Właściwość Balance umożliwia tylko odczytanie wartości pola, natomiast jego wartość może być zmieniona tylko za pomocą metody Deposit i Withdraw. W przypadku próby ustawienia ujemnej wartości dla pola Balance zostanie rzucony wyjątek.

## Automatyczne właściwości

Właściwości w języku C# mogą być również definiowane jako automatyczne właściwości. Automatyczne właściwości pozwalają na uproszczenie kodu i skrócenie zapisu właściwości bez konieczności implementowania metod `get` i `set`. Właściwość automatyczna jest definiowana poprzez użycie skróconej składni:

```
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```
 W powyższym przykładzie klasa Person zawiera dwie automatyczne właściwości - Name i Age. Dzięki temu kod jest bardziej zwięzły i czytelny.

 ## Właściwości tylko do odczytu

 Właściwości klas mogą być definiowane jako tylko do odczytu. Właściwość tylko do odczytu umożliwia tylko odczytanie wartości pola, ale nie pozwala na zmianę wartości. Właściwość tylko do odczytu jest definiowana poprzez usunięcie metody set z definicji właściwości:

```
 public class Person
{
    public string Name { get; }
    public int Age { get; }
}
```

 W powyższym przykładzie klasy `Person` zawiera dwie właściwości tylko do odczytu - `Name` i `Age`. Dzięki temu programista może zapewnić poprawność i niezmienność danych w klasie.

## Właściwości z użyciem wyrażeń lambda

Właściwości w języku C# mogą być również definiowane z użyciem wyrażeń lambda. Wyrażenia lambda pozwalają na zdefiniowanie metody get i set bez konieczności pisania pełnej definicji metody. Oto przykład klasy z właściwością z użyciem wyrażenia lambda:

```
public class Person
{
    private string name;

    public string Name
    {
        get => name;
        set => name = value ?? throw new ArgumentNullException(nameof(value), "Name cannot be null");
    }
}
```

W powyższym przykładzie klasa Person zawiera właściwość `Name` z użyciem wyrażenia lambda. Wyrażenie lambda w metodzie set zapewnia, że wartość pola `name` nie może być nullem.

## YouTube

*https://www.youtube.com/watch?v=Wboc2rgiNik*