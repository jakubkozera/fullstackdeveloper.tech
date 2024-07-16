# HAVING - Filtrowanie grup

Podobnie jak wiersze w tabeli, możemy również filtrować kolumny w wynikach 'zapytania z grupowaniem'. W tym celu używamy klauzuli `HAVING`. Klauzula `HAVING` działa podobnie jak klauzula `WHERE`, ale jest używana do filtrowania wyników grupowanych. Przykładowa składnia klauzuli `HAVING` wygląda następująco:

```
SELECT column_name, aggregate_function(column_name2)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name2) operator value;

```

Zauważ, że jednocześnie możemy używać klauzuli `WHERE` i `HAVING` w jednym zapytaniu. Klauzula `WHERE` jest używana do filtrowania wierszy przed grupowaniem, a klauzula `HAVING` jest używana do filtrowania grup po grupowaniu.

Przykładowo, chcąc uzyskać informację o tym, które kategorie produktów, mają conajmniej 10 produktów, możemy użyć zapytania:


```sql
SELECT ProductCategoryID, COUNT(*) AS NumberOfProducts

FROM SalesLT.Product

GROUP BY ProductCategoryID

HAVING COUNT(*) > 10;


```

Istotne jest aby w klauzuli `HAVING` umieszczać funkcje agregujące, a nie aliasy kolumn.

Użycie aliasu, w klauzuli `HAVING` spowoduje błąd.






```sql
SELECT ProductCategoryID, COUNT(*) AS NumberOfProducts

FROM SalesLT.Product

GROUP BY ProductCategoryID

HAVING NumberOfProducts > 10;


```

## Zadanie praktyczne

<span style="color: var(--vscode-foreground);"><br></span>

<span style="color: var(--vscode-foreground);">1. Znajdź wszystkich sprzedawców `SalesPerson`, którzy obslugują co najmniej 100 klientów&nbsp;</span> **(tabela `Customer`, kolumna `SalesPerson)`**

> 3 wyniki


```sql
SELECT SalesPerson, COUNT(*) CustomerCount

FROM SalesLT.Customer

GROUP BY SalesPerson

HAVING COUNT(*) > 100
```


(3 rows affected)



Total execution time: 00:00:00.009





<table><tr><th>SalesPerson</th><th>CustomerCount</th></tr><tr><td>adventure-works\jillian0</td><td>148</td></tr><tr><td>adventure-works\josé1</td><td>142</td></tr><tr><td>adventure-works\shu0</td><td>151</td></tr></table>



2\. Znajdź które modele (produktu `ProductModelID`), mają średnią cene produktu `ListPrice` większą niż 300



> 29 wyników


```sql
SELECT ProductModelID, AVG(ListPrice) AveragePrice

FROM SalesLT.Product

GROUP BY ProductModelID

HAVING AVG(ListPrice) > 300
```


(29 rows affected)



Total execution time: 00:00:00.010





<table><tr><th>ProductModelID</th><th>AveragePrice</th></tr><tr><td>5</td><td>1357,05</td></tr><tr><td>6</td><td>1431,50</td></tr><tr><td>7</td><td>1003,91</td></tr><tr><td>9</td><td>337,22</td></tr><tr><td>10</td><td>333,42</td></tr><tr><td>14</td><td>348,76</td></tr><tr><td>15</td><td>361,024</td></tr><tr><td>16</td><td>594,83</td></tr><tr><td>17</td><td>594,83</td></tr><tr><td>19</td><td>3387,49</td></tr><tr><td>20</td><td>2307,49</td></tr><tr><td>21</td><td>1079,99</td></tr><tr><td>22</td><td>769,49</td></tr><tr><td>23</td><td>552,49</td></tr><tr><td>25</td><td>3578,27</td></tr><tr><td>26</td><td>2443,35</td></tr><tr><td>27</td><td>1700,99</td></tr><tr><td>28</td><td>1457,99</td></tr><tr><td>29</td><td>1120,49</td></tr><tr><td>30</td><td>782,99</td></tr><tr><td>31</td><td>539,99</td></tr><tr><td>34</td><td>2384,07</td></tr><tr><td>35</td><td>1214,85</td></tr><tr><td>36</td><td>742,35</td></tr><tr><td>46</td><td>300,215</td></tr><tr><td>51</td><td>330,06</td></tr><tr><td>78</td><td>357,06</td></tr><tr><td>101</td><td>404,99</td></tr><tr><td>125</td><td>327,215</td></tr></table>



3\. Znajdź kolory `Color` produktów, które mają miminalną cenę `ListPrice` 30

> 5 rezultatów


```sql
SELECT Color, MIN(ListPrice) as MinPrice

FROM SalesLT.Product

GROUP BY Color

HAVING MIN(ListPrice) > 30
```


(5 rows affected)



Total execution time: 00:00:00.007





<table><tr><th>Color</th><th>MinPrice</th></tr><tr><td>Blue</td><td>34,99</td></tr><tr><td>Grey</td><td>125,00</td></tr><tr><td>Red</td><td>34,99</td></tr><tr><td>Silver/Black</td><td>40,49</td></tr><tr><td>Yellow</td><td>53,99</td></tr></table>


