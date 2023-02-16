# Modyfikatory dostępu

W języku C# modyfikatory dostępu definiują, z jakim poziomem widoczności dostępne są klasy, pola, metody i inne elementy w programie. Dostępne są cztery rodzaje modyfikatorów dostępu: `public`, `private`, `protected` i `internal`. Oprócz nich w C# można również użyć modyfikatora `protected internal`, który łączy funkcjonalności obu modyfikatorów. W tej pracy omówimy każdy z tych modyfikatorów dostępu i przedstawimy ich zastosowanie w programowaniu w języku C#.

## Modyfikator dostępu `public`



Modyfikator `public` oznacza, że dany element jest widoczny wszędzie, zarówno wewnątrz jak i na zewnątrz klasy, w której został zdefiniowany. Elementy `public` są dostępne dla każdego innego elementu w programie, co oznacza, że mogą być wywoływane i modyfikowane przez dowolny kod w programie. Oto przykład użycia modyfikatora `public` w klasie:
```
public class Person
{
   public string name;
   public void SayHello()
   {
      Console.WriteLine("Hello!");
   }
}
```

W powyższym przykładzie pole "name" oraz metoda "SayHello" są oznaczone modyfikatorem public, co oznacza, że są one dostępne z dowolnego miejsca w programie.

## Modyfikator dostępu `private`

Modyfikator `private` oznacza, że dany element jest widoczny tylko wewnątrz klasy, w której został zdefiniowany. Elementy `private` są niedostępne dla innych elementów w programie, co oznacza, że nie mogą być wywoływane ani modyfikowane przez żaden kod poza klasą, w której zostały zdefiniowane. Oto przykład użycia modyfikatora `private` w klasie:

```
public class Person
{
   private int age;
   private void GrowOlder()
   {
      age++;
   }
}
```
W powyższym przykładzie pole "age" oraz metoda "GrowOlder" są oznaczone modyfikatorem private, co oznacza, że są one dostępne tylko wewnątrz klasy `Person`.

## Modyfikator dostępu `protected`

Modyfikator `protected` oznacza, że dany element jest widoczny wewnątrz klasy oraz w klasach pochodnych (dziedziczących) od niej. Elementy `protected` są niedostępne dla innych elementów w programie, co oznacza, że nie mogą być wywoływane ani modyfikowane przez kod poza klasą lub klasami dziedziczącymi. Oto przykład użycia modyfikatora `protected` w klasie:

```
public class Animal
{
   protected string sound;
   protected void MakeSound()
   {
      Console.WriteLine(sound);
   }
}

public class Dog : Animal
{
   public public void Bark()
    {
        sound = "Bark!";
        MakeSound();
    }
}
```

W powyższym przykładzie pole "sound" oraz metoda "MakeSound" są oznaczone modyfikatorem `protected`, co oznacza, że są one dostępne tylko wewnątrz klasy `Animal` oraz w klasach dziedziczących, takich jak klasa `Dog`.

## Modyfikator dostępu `internal`

Modyfikator `internal` oznacza, że dany element jest widoczny tylko wewnątrz tego samego projektu. Elementy `internal` są niedostępne dla elementów poza projektem, co oznacza, że nie mogą być wywoływane ani modyfikowane przez kod poza projektem. Oto przykład użycia modyfikatora `internal` w klasie:

```
internal class Person
{
    internal string name;
    internal void SayHello()
    {
        Console.WriteLine("Hello!");
    }
}
```
W powyższym przykładzie pole "name" oraz metoda "SayHello" są oznaczone modyfikatorem `internal`, co oznacza, że są one dostępne tylko wewnątrz projektu, w którym zostały zdefiniowane.

5. Modyfikator dostępu `protected` `internal`

Modyfikator `protected` `internal` łączy funkcjonalności modyfikatorów `protected` i `internal`. Oznacza to, że dany element jest widoczny wewnątrz klasy, w klasach dziedziczących oraz wewnątrz tego samego projektu. Elementy `protected` `internal` są niedostępne dla elementów poza projektem lub poza klasami dziedziczącymi. Oto przykład użycia modyfikatora `protected` `internal` w klasie:


```
protected internal class Person
{
    protected internal string name;
    protected internal void SayHello()
    {
        Console.WriteLine("Hello!");
    }
}
```
W powyższym przykładzie pole "name" oraz metoda "SayHello" są oznaczone modyfikatorem protected internal, co oznacza, że są one dostępne tylko wewnątrz projektu oraz w klasach dziedziczących.

## Zastosowanie modyfikatorów dostępu

Modyfikatory dostępu są bardzo ważnym narzędziem w języku C# i służą do zapewnienia bezpieczeństwa i poprawności programów. Oto kilka przykładów, w których modyfikatory dostępu mogą być stosowane:

- Jeśli nie chcesz, aby dane pole lub metoda były dostępne dla innych elementów w programie, powinieneś oznaczyć je modyfikatorem `private`.
- Jeśli chcesz, aby dane pole lub metoda były dostępne tylko dla innych elementów w tym samym projekcie, powinieneś oznaczyć je modyfikatorem `internal`.
- Jeśli chcesz, aby dane pole lub metoda były dostępne tylko dla klasy i jej klas dziedziczących, powinieneś oznaczyć je modyfikatorem `protected`.
- Jeśli chcesz, aby dane pole lub metoda były dostępne dla klasy, klas dziedziczących oraz innych elementów w tym samym projekcie, powinieneś oznaczyć je modyfikatorem protected internal.
- Jeśli chcesz, aby dane pole lub metoda były dostępne dla wszystkich elementów w programie, nie powinieneś oznaczać ich żadnym modyfikatorem, ponieważ domyślnym modyfikatorem dostępu w C# jest public.

### Podsumowanie
Modyfikatory dostępu są niezwykle ważnym narzędziem w języku C# i służą do zapewnienia bezpieczeństwa i poprawności programów. Odpowiednie użycie modyfikatorów dostępu pozwala na kontrolowanie dostępu do pól i metod w klasach oraz zapobieganie niepożądanym zmianom w danych.