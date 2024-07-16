# Typy danych
Typy danych w kontekście baz danych określają rodzaj danych, które mogą być przechowywane w określonym polu w tabeli bazy danych. Każdy typ danych ma swoje własne cechy, takie jak zakres wartości, wymagana ilość pamięci, sposób sortowania itp. Typy danych pomagają bazie danych w interpretacji i przechowywaniu informacji zgodnie z ich właściwościami.
Oto kilka kluczowych cech typów danych w bazach danych:
1. **Zakres wartości**: Określa, jakie wartości mogą być przechowywane w danym polu, na przykład liczby całkowite, łańcuchy znaków, daty itp.
    
2. **Wymagana pamięć**: Każdy typ danych zajmuje określoną ilość pamięci w bazie danych. Na przykład, typ danych INT może wymagać mniej pamięci niż BIGINT.
    
3. **Format danych**: Określa format, w jakim dane są przechowywane i reprezentowane w bazie danych, na przykład liczby całkowite, zmiennoprzecinkowe, daty, czasy itp.
    
4. **Operacje możliwe do wykonania**: Niektóre typy danych pozwalają na określone operacje, takie jak dodawanie, odejmowanie, łączenie, porównywanie itp.
    
5. **Porównywalność i sortowalność**: Niektóre typy danych mogą być sortowane i porównywane, podczas gdy inne mogą mieć ograniczenia w tym zakresie.
    
## Podział typów danych w Microsoft SQL Server według kategorii:
### Typy numeryczne:
1. **BIT**: Typ logiczny przechowujący wartości true/false lub 0/1
2. **TINYINT**: Typ danych całkowitoliczbowy przechowujący liczby całkowite z zakresu od 0 do 255.
3. **SMALLINT**: Typ danych całkowitoliczbowy przechowujący liczby całkowite z zakresu od -32,768 do 32,767.
4. **INT**: Typ danych całkowitoliczbowy przechowujący liczby całkowite z zakresu od -2,147,483,648 do 2,147,483,647.
5. **BIGINT**: Typ danych całkowitoliczbowy przechowujący bardzo duże liczby całkowite z zakresu od -9,223,372,036,854,775,808 do 9,223,372,036,854,775,807.
6. **DECIMAL(p, s)**: Typ danych do przechowywania liczb zmiennoprzecinkowych o stałej precyzji i skali, gdzie p to liczba cyfr całkowitych, a s to liczba cyfr po przecinku.
7. **FLOAT**: Typ danych do przechowywania liczb zmiennoprzecinkowych o podwójnej precyzji.
### Typy znakowe:
1. **CHAR(n)**: Typ danych do przechowywania łańcuchów znaków o stałej długości do n znaków.
2. **VARCHAR(n)**: Typ danych do przechowywania łańcuchów znaków o zmiennej długości do n maksymalnych bajtów.
3. **NCHAR(n)**: Typ danych do przechowywania łańcuchów znaków Unicode o stałej długości do n znaków.
4. **NVARCHAR(n)**: Typ danych do przechowywania łańcuchów znaków Unicode o zmiennej długości do n maksymalnych bajtów.
Różnica między typami danych `CHAR` a `NCHAR` dotyczy sposobu przechowywania znaków w bazie danych:
1. **CHAR**:
    
    - Typ danych `CHAR` służy do przechowywania łańcuchów znaków o stałej długości.
    - Wartość liczby w nawiasach określa liczbę znaków, które mogą być przechowywane w polu `CHAR`. Na przykład, `CHAR(10)` oznacza, że pole będzie przechowywać dokładnie 10 znaków.
    - Jeśli wprowadzona wartość jest krótsza niż określona długość, pole `CHAR` zostanie wypełnione spacjami, aby osiągnąć określoną długość.
2. **NCHAR**:
    
    - Typ danych `NCHAR` służy do przechowywania łańcuchów znaków Unicode o stałej długości.
    - Podobnie jak w przypadku `CHAR`, wartość liczby w nawiasach określa liczbę znaków, które mogą być przechowywane w polu `NCHAR`.
    - W przeciwieństwie do typu `CHAR`, który przechowuje znaki w formacie jednobajtowym (ASCII), typ `NCHAR` przechowuje znaki w formacie Unicode, co oznacza, że może obsługiwać znaki z różnych zestawów znaków, w tym znaki spoza standardowego zestawu ASCII, ale przez to zajmuje dwukrotnie więcej miejsca w pamięci.
Podsumowując, główna różnica między typami danych `CHAR` a `NCHAR` polega na tym, że `CHAR` przechowuje łańcuchy znaków w formacie jednobajtowym, podczas gdy `NCHAR` przechowuje znaki w formacie Unicode. W przypadku stosowania typu `NCHAR`, należy pamiętać, że zajmuje on dwukrotnie więcej miejsca niż `CHAR` ze względu na obsługę Unicode.
### Typy datowe i czasowe:
1. **DATE**: Typ danych do przechowywania daty w formacie YYYY-MM-DD.
2. **TIME**: Typ danych do przechowywania czasu w formacie godzina:minuta:sekunda.
3. **DATETIME**: Typ danych do przechowywania daty i czasu w formacie YYYY-MM-DD godzina:minuta:sekunda.
4. **DATETIME2**: Rozszerzony typ danych do przechowywania daty i czasu z większą precyzją.
5. **SMALLDATETIME**: Typ danych do przechowywania daty i czasu w formacie YYYY-MM-DD godzina:minuta.
6. **TIMESTAMP**: Typ danych do przechowywania znacznika czasu, który automatycznie się aktualizuje po zmianie danych w wierszu.
To są podstawowe typy danych w Microsoft SQL Server, uporządkowane według kategorii. Każdy typ danych ma swoje specyficzne zastosowanie, które można dopasować do wymagań projektu.
### Brak wartości
W SQL, `NULL` to specjalna wartość reprezentująca brak danych lub nieokreśloność. Oznacza to, że pole w bazie danych nie posiada żadnej konkretnej wartości.
Oto kilka cech dotyczących `NULL` w kontekście baz danych:
1. **Brak wartości**: `NULL` oznacza brak konkretnej wartości w danym polu.
    
2. **Nieokreśloność**: Może oznaczać, że wartość jest nieznana, niezdefiniowana lub nie dotyczy danego rekordu.
    
3. **Dopuszczalność**: Pola w bazie danych mogą być zdefiniowane jako NULLABLE (dopuszczające wartość `NULL`) lub `NOT NULL` (nie dopuszczające wartości `NULL`).
    
4. **Porównywanie z NULL**: Operacje porównania z `NULL` są specjalne. Porównanie równości z `NULL` zwróci `FALSE`, a porównanie nierówności zwróci `NULL`. Jak już wiemy, musimy użyć operatora `IS NULL` lub `IS NOT NULL` do sprawdzenia, czy wartość jest `NULL`.
    
Przykład:
- Jeśli masz pole w tabeli, które przechowuje wiek użytkownika, a wiek nie został jeszcze podany, można to pole zostawić puste (`NULL`).
- W przypadku niezdefiniowanej wartości, na przykład w sytuacji, gdy niektóre informacje nie są jeszcze znane, można użyć wartości `NULL`.
`NULL` jest przydatny do obsługi przypadków, gdy nie wszystkie informacje są dostępne lub nie są jeszcze znane. Jednak należy pamiętać, że nadmierny użytek wartości `NULL` może prowadzić do trudności w zapytaniach SQL, ponieważ operacje porównania z `NULL` mają specjalne zachowanie. Dlatego ważne jest ostrożne stosowanie wartości `NULL` i odpowiednie zarządzanie nimi w bazie danych.
