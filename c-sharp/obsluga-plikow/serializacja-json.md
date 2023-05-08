# Serializacja JSON

**JSON** jest to skrót od **JavaScript Object Notation** to format wymiany danych, który jest często używany do przesyłania danych pomiędzy aplikacjami webowymi i serwerami. JSON jest oparty na składni JavaScript i jest często uważany za alternatywę dla XML.

Dane w formacie JSON są reprezentowane jako ciągi tekstowe i składają się z par klucz-wartość. Klucze są wyrażane jako ciągi tekstowe zawierające nazwy pól, a wartości są wyrażane jako liczby, ciągi tekstowe, obiekty JSON, tablicy lub specjalne wartości (takie jak null, true i false).

Przykład danych w formacie JSON:

```
{
  "name": "Mario",
  "level": 1,
  "isActive": false,
  "healthPoints": 100,
  "statistics": [
    {
        "name": "Strength",
        "points": 10
    },
    {
        "name": "Intelligence",
        "points": 10
    }
  ]
}

```

Serializacja JSON oznacza proces konwersji obiektów w języku C# na strumień bajtów możliwy do zapisania w postaci pliku JSON. Natomiast deserializacja to proces odwrotny, czyli konwersja danych z pliku JSON na obiekty w języku C#. 

Istnieje kilka bibliotek do serializacji i deserializacji JSON, z czego najbardziej popularna to `Newtonsoft.Json`.

Za pomocą tej biblioteki, serializację można wykonać za pomocą metody `JsonConvert.SerializeObject`:

```
using Newtonsoft.Json;

var player = new Player()
    {
        Name = "Mario",
        Level = 1,
        IActive = false,
        HealthPoints = 100,
        Statistics = new List<Statistic>()
        {
            Name = "Strength",
            Points = 10
        },
        {
            Name = "Intelligence",
            Points = 10
        }
    };

string playerSerialized = JsonConvert.SerializeObject(player);
```

Deserializacja danych JSON może być wykonana za pomocą metody `JsonConvert.DeserializeObject`, która jako swój parametr generyczny przyjmuje typ, na który będzie zdeserializowany JSON:

```
var player = JsonConvert.DeserializeObject<Player>(json);
```


## Przypadki użycia JSON

JSON jest popularnym formatem przesyłania danych w aplikacjach .NET. Służy do przesyłania danych pomiędzy aplikacjami w formie tekstowej. Dzięki temu można łatwo wymieniać dane pomiędzy różnymi językami programowania i platformami.

W .NET, JSON jest często używany do komunikacji z serwerami i usługami internetowymi, takimi jak RESTful web services. JSON jest też używany do przechowywania i wymiany danych w aplikacjach mobilnych i w aplikacjach dla przeglądarek.

## YouTube

*https://www.youtube.com/watch?v=RZ5uMSFMDBM*