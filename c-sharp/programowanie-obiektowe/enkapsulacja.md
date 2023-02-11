# Enkapsulacja

Enkapsulacja zwana także hermetyzacją, polega na ukrywaniu wewnętrznych szczegółów implementacji obiektu i udostępnianiu jedynie jego interfejsu publicznego, który określa jak można korzystać z tego obiektu.

Enkapsulacja jest kluczowa dla zapewnienia jakości kodu i jego bezpieczeństwa, ponieważ pozwala na łatwiejsze testowanie i utrzymywanie kodu, a także zabezpiecza go przed błędami, które mogą wystąpić w wyniku nieprawidłowego dostępu do wewnętrznych danych i funkcjonalności obiektu.

## Przykład

```
using System;

class BankAccount
{
    private decimal balance;

    public decimal Balance
    {
        get { return balance; }
        set { balance = value; }
    }

    public void Deposit(decimal amount)
    {
        balance += amount;
    }

    public void Withdraw(decimal amount)
    {
        balance -= amount;
    }
}
```

W powyższym przykładzie dane wewnętrzne `balance` są enkapsulowane i dostępne tylko poprzez publiczną właściwość `Balance`. Zdefiniowane funkcje `Deposit` i `Withdraw` umożliwiają kontrolowanie stanu `balance`, ale nie umożliwiają bezpośredniego dostępu do niego. To zapewnia bezpieczeństwo i kontrolę nad danymi wewnętrznymi, a także umożliwia łatwiejsze utrzymywanie i testowanie kodu.



# Scenariusze użycia enkapsulacji

Enkapsulacja jest używana w C# w następujących sytuacjach:

- Ochrona danych - enkapsulacja umożliwia ukrycie prywatnych danych i metod wewnątrz klasy i udostępnianie tylko publicznych danych i metod innym klasom i obiektom.

- Ulepszanie funkcjonalności - enkapsulacja umożliwia modyfikowanie wewnętrznej logiki implementacji klasy bez wpływania na inne klasy i obiekty, które korzystają z tej klasy.

- Zwiększenie bezpieczeństwa - enkapsulacja umożliwia ochronę danych przed nieautoryzowanym dostępem i manipulacją.

- Zwiększenie czytelności kodu - enkapsulacja umożliwia ukrycie skomplikowanej logiki implementacji wewnątrz klasy i udostępnianie prostszej i bardziej czytelnej interfejsu dla innych klas i obiektów.

Enkapsulacja jest ważnym elementem projektowania opartego na obiektach i powinna być stosowana w każdej klasie, w której dane i logika implementacji muszą być ukryte i chronione.