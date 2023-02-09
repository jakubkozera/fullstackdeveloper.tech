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