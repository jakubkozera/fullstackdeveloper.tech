# Namespace

`Namespace` to w C# inaczej przestrzeń nazw, czyli mechanizm służący do grupowania typów (takich jak klasy, struktury czy interfejsy) w sposób logiczny. Dzięki przestrzeniom nazw można uniknąć konfliktów nazw typów - przez co bylibyśmy w stanie przykładowo utworzyć dwie klasy o tej samej nazwie, jeżeli zaszłaby taka potrzeba. 

Przestrzenie nazw są zdefiniowane za pomocą słowa kluczowego `namespace`, po którym podaje się nazwę przestrzeni nazw. Typy są deklarowane wewnątrz przestrzeni nazw za pomocą słów kluczowych `class`, `struct`, `interface` i `enum`.

## Przykład

```
namespace Games
{
    public class TicTacToe
    {
        public void Play() { ... }
    }
}
```

W powyższym przykładzie zdefiniowano przestrzeń nazw o nazwie `Games`, w której znajduje się publiczna klasa `TicTacToe` z metodą `Play`. 
Aby skorzystać z tej klasy w innym pliku, należy dołączyć odpowiednią dyrektywą `using`:

```
using Games;

namespace GameConsole 
{
    class Program
    {
        static void Main(string[] args)
        {
            TicTacToe obj = new TicTacToe();
            obj.Play();
        }
    }
}

```

Co więcej, definicja typów (klas, struktur czy enum) musi istnieć wewnątrz jakiegoś `namespace`, kompilator nie zezwoli na utworzenie typu poza nim.

## YouTube

*https://www.youtube.com/watch?v=8nZe6u6CUFw*