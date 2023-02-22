# Stos i sterta

Sterta i stos to dwa różne rodzaje pamięci, które są wykorzystywane w procesie alokacji i zwalniania pamięci.

## Sterta (heap)

Sterta to obszar pamięci, w którym przechowywane są obiekty i dane dynamiczne, czyli te, których rozmiar i miejsce w pamięci nie są znane podczas kompilacji programu. Obiekty tworzone na stercie pozostają w pamięci dopóki nie zostaną usunięte przez program. Sterta jest zwykle alokowana podczas uruchamiania programu i zwiększa swoją wielkość w miarę potrzeby.

Alokacja pamięci na stercie odbywa się za pomocą operatora `new`. Po utworzeniu obiektu, jego referencja jest przechowywana na stosie lub w innych miejscach w pamięci. W C# sterowanie pamięcią jest automatyczne, co oznacza, że system zarządzania pamięcią (garbage collector) usuwa nieużywane obiekty z pamięci, gdy zostaną one odwołane przez program.

## Stos (stack)

Stos to obszar pamięci, w którym przechowywane są zmienne lokalne oraz informacje o wywołaniach funkcji. W przeciwieństwie do sterty, stos jest alokowany w momencie tworzenia każdego wątku, a jego rozmiar jest zwykle stały. Każda funkcja, która jest wywoływana, tworzy na stosie ramkę stosu, która zawiera informacje o wywołaniu, takie jak argumenty funkcji, adres powrotu i wartości zmiennej lokalnej.

Alokacja pamięci na stosie odbywa się automatycznie przy wywoływaniu funkcji, a zwolnienie pamięci następuje automatycznie przy zakończeniu funkcji. Ponieważ stos jest stosunkowo mały i ma stały rozmiar, jego użycie jest zwykle szybsze i efektywniejsze niż stosowanie sterty.

Wadą stosu jest to, że rozmiar stosu jest ograniczony, co oznacza, że funkcje, które używają dużej liczby zmiennych lokalnych lub wywołują wiele funkcji zagnieżdżonych, mogą przekroczyć limit rozmiaru stosu i spowodować przepełnienie stosu (stack overflow).
