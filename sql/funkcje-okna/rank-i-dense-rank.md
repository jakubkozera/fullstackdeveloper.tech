## Funkcje `RANK()` i `DENSE_RANK()`

### Funkcja `RANK()`

Funkcja `RANK()` zwraca pozycję/ranking w grupie rekordów. Jeśli dwa rekordy mają taką samą wartość, to funkcja `RANK()` zwróci tę samą wartość dla obu rekordów, a następnie przeskoczy do kolejnej wartości. Jej użycie będzie bardzo zbliżone do funkcji `ROW_NUMBER()`, ale z tą różnicą, że funkcja `RANK()` może zwrócić tę samą wartość dla dwóch rekordów, jeśli mają taką samą wartość.

Przykładowo:


```sql
SELECT c.SalesPerson, 
    c.CustomerID, 
    soh.SubTotal, 
    soh.SalesOrderID,
    ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRN,
    RANK() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank

FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID

```


(32 rows affected)



Total execution time: 00:00:00.018





<table><tr><th>SalesPerson</th><th>CustomerID</th><th>SubTotal</th><th>SalesOrderID</th><th>TopCustomerRN</th><th>TopCustomerRank</th></tr><tr><td>adventure-works\jae0</td><td>29736</td><td>108561,8317</td><td>71784</td><td>1</td><td>1</td></tr><tr><td>adventure-works\jae0</td><td>30050</td><td>98278,691</td><td>71936</td><td>2</td><td>2</td></tr><tr><td>adventure-works\jae0</td><td>29546</td><td>88812,8625</td><td>71938</td><td>3</td><td>3</td></tr><tr><td>adventure-works\jae0</td><td>29796</td><td>78029,6898</td><td>71797</td><td>4</td><td>4</td></tr><tr><td>adventure-works\jae0</td><td>29932</td><td>63980,9884</td><td>71898</td><td>5</td><td>5</td></tr><tr><td>adventure-works\jae0</td><td>30113</td><td>38418,6895</td><td>71780</td><td>6</td><td>6</td></tr><tr><td>adventure-works\jae0</td><td>29922</td><td>35775,2113</td><td>71832</td><td>7</td><td>7</td></tr><tr><td>adventure-works\jae0</td><td>30102</td><td>2016,3408</td><td>71846</td><td>8</td><td>8</td></tr><tr><td>adventure-works\jae0</td><td>30019</td><td>2016,3408</td><td>71831</td><td>9</td><td>8</td></tr><tr><td>adventure-works\jae0</td><td>29612</td><td>550,386</td><td>71885</td><td>10</td><td>10</td></tr><tr><td>adventure-works\jae0</td><td>29644</td><td>550,386</td><td>71867</td><td>11</td><td>10</td></tr><tr><td>adventure-works\jae0</td><td>30072</td><td>78,81</td><td>71776</td><td>12</td><td>12</td></tr><tr><td>adventure-works\jae0</td><td>30025</td><td>40,9045</td><td>71917</td><td>13</td><td>13</td></tr><tr><td>adventure-works\jae0</td><td>29741</td><td>38,9536</td><td>71946</td><td>14</td><td>14</td></tr><tr><td>adventure-works\linda3</td><td>29957</td><td>83858,4261</td><td>71783</td><td>1</td><td>1</td></tr><tr><td>adventure-works\linda3</td><td>29660</td><td>57634,6342</td><td>71796</td><td>2</td><td>2</td></tr><tr><td>adventure-works\linda3</td><td>29485</td><td>39785,3304</td><td>71782</td><td>3</td><td>3</td></tr><tr><td>adventure-works\linda3</td><td>29653</td><td>13823,7083</td><td>71858</td><td>4</td><td>4</td></tr><tr><td>adventure-works\linda3</td><td>29531</td><td>6634,2961</td><td>71935</td><td>5</td><td>5</td></tr><tr><td>adventure-works\linda3</td><td>29975</td><td>3324,2759</td><td>71863</td><td>6</td><td>6</td></tr><tr><td>adventure-works\linda3</td><td>29638</td><td>2137,231</td><td>71915</td><td>7</td><td>7</td></tr><tr><td>adventure-works\linda3</td><td>30089</td><td>1141,5782</td><td>71815</td><td>8</td><td>8</td></tr><tr><td>adventure-works\linda3</td><td>29847</td><td>880,3484</td><td>71774</td><td>9</td><td>9</td></tr><tr><td>adventure-works\shu0</td><td>29929</td><td>74058,8078</td><td>71902</td><td>1</td><td>1</td></tr><tr><td>adventure-works\shu0</td><td>29938</td><td>41622,0511</td><td>71845</td><td>2</td><td>2</td></tr><tr><td>adventure-works\shu0</td><td>29877</td><td>12685,8899</td><td>71897</td><td>3</td><td>3</td></tr><tr><td>adventure-works\shu0</td><td>30027</td><td>3398,1659</td><td>71816</td><td>4</td><td>4</td></tr><tr><td>adventure-works\shu0</td><td>29982</td><td>2980,7929</td><td>71920</td><td>5</td><td>5</td></tr><tr><td>adventure-works\shu0</td><td>29568</td><td>2415,6727</td><td>71899</td><td>6</td><td>6</td></tr><tr><td>adventure-works\shu0</td><td>30033</td><td>602,1946</td><td>71856</td><td>7</td><td>7</td></tr><tr><td>adventure-works\shu0</td><td>29584</td><td>246,7392</td><td>71895</td><td>8</td><td>8</td></tr><tr><td>adventure-works\shu0</td><td>29781</td><td>106,5408</td><td>71923</td><td>9</td><td>9</td></tr></table>




W powyższym przykładzie, jeśli dwóch klientów ma taką samą wartość `SubTotal`, to funkcja `RANK()` zwróci tę samą wartość dla obu rekordów, a następnie przeskoczy do kolejnej wartości, natomiast jeśli wartości `SubTotal` są różne, to funkcja `RANK()` zwróci różne wartości dla każdego rekordu, wynik będzie podobny do funkcji `ROW_NUMBER()`. Tak więc, aby zobaczyć róźnice w wyniku tych dwóch funkcji, warto użyć danych, w których wartości `SubTotal` są takie same dla dwóch rekordów. W tym celu, wykonajmy polecenie `UPDATE` na tabeli `SalesLT.[SalesOrderHeader]`:




```sql
UPDATE SalesLT.[SalesOrderHeader]
SET SubTotal = 2016.3408
WHERE SalesOrderID = 71846


UPDATE SalesLT.[SalesOrderHeader]
SET SubTotal = 550.386
WHERE SalesOrderID = 71867



```


(1 row affected)



(1 row affected)



Total execution time: 00:00:00.015


Dopiero teraz, gdy conajmniej 2 wiersze mają taką samą wartość w kolumnie w klauzuli `ORDER BY`, widzimy róźnice w rezultacie zapytania. W takim przypadku, wynik zależy od kolejności wierszy w tabeli. `RANK` w ten sam sposób sklasiwuje wiersze z taką samą wartością w kolumnie w klauzuli `ORDER BY`, gdzie `ROW_NUMBER` nie robi tego. 

Co więcej ranking następnego wiersza, raz po tego typu wierszach, jest zwiększany o liczbę wierszy z taką samą wartością w kolumnie w klauzuli `ORDER BY`.


### Funkcja `DENSE_RANK()`

`DENSE_RANK()` działa podobnie jak `RANK()`, ale nie ma przerw w numeracji rankingów. W przypadku, gdy kilka wierszy ma taką samą wartość w kolumnie w klauzuli `ORDER BY`, to rankingi są nadal zwiększane o 1, ale nie ma przerw w numeracji.




```sql
SELECT c.SalesPerson, 
    c.CustomerID, 
    soh.SubTotal, 
    soh.SalesOrderID,
    ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRN,
    RANK() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank,
    DENSE_RANK() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerDenseRank

FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
```


(32 rows affected)



Total execution time: 00:00:00.011





<table><tr><th>SalesPerson</th><th>CustomerID</th><th>SubTotal</th><th>SalesOrderID</th><th>TopCustomerRN</th><th>TopCustomerRank</th><th>TopCustomerDenseRank</th></tr><tr><td>adventure-works\jae0</td><td>29736</td><td>108561,8317</td><td>71784</td><td>1</td><td>1</td><td>1</td></tr><tr><td>adventure-works\jae0</td><td>30050</td><td>98278,691</td><td>71936</td><td>2</td><td>2</td><td>2</td></tr><tr><td>adventure-works\jae0</td><td>29546</td><td>88812,8625</td><td>71938</td><td>3</td><td>3</td><td>3</td></tr><tr><td>adventure-works\jae0</td><td>29796</td><td>78029,6898</td><td>71797</td><td>4</td><td>4</td><td>4</td></tr><tr><td>adventure-works\jae0</td><td>29932</td><td>63980,9884</td><td>71898</td><td>5</td><td>5</td><td>5</td></tr><tr><td>adventure-works\jae0</td><td>30113</td><td>38418,6895</td><td>71780</td><td>6</td><td>6</td><td>6</td></tr><tr><td>adventure-works\jae0</td><td>29922</td><td>35775,2113</td><td>71832</td><td>7</td><td>7</td><td>7</td></tr><tr><td>adventure-works\jae0</td><td>30102</td><td>2016,3408</td><td>71846</td><td>8</td><td>8</td><td>8</td></tr><tr><td>adventure-works\jae0</td><td>30019</td><td>2016,3408</td><td>71831</td><td>9</td><td>8</td><td>8</td></tr><tr><td>adventure-works\jae0</td><td>29612</td><td>550,386</td><td>71885</td><td>10</td><td>10</td><td>9</td></tr><tr><td>adventure-works\jae0</td><td>29644</td><td>550,386</td><td>71867</td><td>11</td><td>10</td><td>9</td></tr><tr><td>adventure-works\jae0</td><td>30072</td><td>78,81</td><td>71776</td><td>12</td><td>12</td><td>10</td></tr><tr><td>adventure-works\jae0</td><td>30025</td><td>40,9045</td><td>71917</td><td>13</td><td>13</td><td>11</td></tr><tr><td>adventure-works\jae0</td><td>29741</td><td>38,9536</td><td>71946</td><td>14</td><td>14</td><td>12</td></tr><tr><td>adventure-works\linda3</td><td>29957</td><td>83858,4261</td><td>71783</td><td>1</td><td>1</td><td>1</td></tr><tr><td>adventure-works\linda3</td><td>29660</td><td>57634,6342</td><td>71796</td><td>2</td><td>2</td><td>2</td></tr><tr><td>adventure-works\linda3</td><td>29485</td><td>39785,3304</td><td>71782</td><td>3</td><td>3</td><td>3</td></tr><tr><td>adventure-works\linda3</td><td>29653</td><td>13823,7083</td><td>71858</td><td>4</td><td>4</td><td>4</td></tr><tr><td>adventure-works\linda3</td><td>29531</td><td>6634,2961</td><td>71935</td><td>5</td><td>5</td><td>5</td></tr><tr><td>adventure-works\linda3</td><td>29975</td><td>3324,2759</td><td>71863</td><td>6</td><td>6</td><td>6</td></tr><tr><td>adventure-works\linda3</td><td>29638</td><td>2137,231</td><td>71915</td><td>7</td><td>7</td><td>7</td></tr><tr><td>adventure-works\linda3</td><td>30089</td><td>1141,5782</td><td>71815</td><td>8</td><td>8</td><td>8</td></tr><tr><td>adventure-works\linda3</td><td>29847</td><td>880,3484</td><td>71774</td><td>9</td><td>9</td><td>9</td></tr><tr><td>adventure-works\shu0</td><td>29929</td><td>74058,8078</td><td>71902</td><td>1</td><td>1</td><td>1</td></tr><tr><td>adventure-works\shu0</td><td>29938</td><td>41622,0511</td><td>71845</td><td>2</td><td>2</td><td>2</td></tr><tr><td>adventure-works\shu0</td><td>29877</td><td>12685,8899</td><td>71897</td><td>3</td><td>3</td><td>3</td></tr><tr><td>adventure-works\shu0</td><td>30027</td><td>3398,1659</td><td>71816</td><td>4</td><td>4</td><td>4</td></tr><tr><td>adventure-works\shu0</td><td>29982</td><td>2980,7929</td><td>71920</td><td>5</td><td>5</td><td>5</td></tr><tr><td>adventure-works\shu0</td><td>29568</td><td>2415,6727</td><td>71899</td><td>6</td><td>6</td><td>6</td></tr><tr><td>adventure-works\shu0</td><td>30033</td><td>602,1946</td><td>71856</td><td>7</td><td>7</td><td>7</td></tr><tr><td>adventure-works\shu0</td><td>29584</td><td>246,7392</td><td>71895</td><td>8</td><td>8</td><td>8</td></tr><tr><td>adventure-works\shu0</td><td>29781</td><td>106,5408</td><td>71923</td><td>9</td><td>9</td><td>9</td></tr></table>


