## Funkcja `ROW_NUMBER()`

Funkcja `ROW_NUMBER()` zwraca numer wiersza w wynikowym zbiorze danych. Funkcja ta jest często używana w połączeniu z `PARTITION BY` w celu przypisania numeru wiersza w ramach grupy, jak i `ORDER BY` w celu uporządkowania wyników.

### Składnia

```
ROW_NUMBER() OVER (PARTITION BY column1, column2,... ORDER BY column1, column2,...)

```

### Przykład

Rozważmy poniższe zapytanie, które zwraca informacje o klientach, ich sprzedawcach i kwotach sprzedaży.


```sql
SELECT c.SalesPerson, c.CustomerID, soh.SubTotal
FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
```

Żeby z tych danych, zwrócić tylko np. 3 największych klientów, dla każdego sprzedawcy z osobna, możemy najpierw użyć funkcji `ROW_NUMBER()` w celu przypisania numeru do każdego wiersza w grupie sprzedawcy, posortowanego malejąco według wartości sprzedaży. 




```sql
SELECT c.SalesPerson, c.CustomerID, soh.SubTotal, 
    ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank
FROM SalesLT.[SalesOrderHeader] soh
JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID
```

Następnie, wybieramy tylko te wiersze, które mają numer mniejszy lub równy 3.


```sql

SELECT * 
FROM (
    SELECT c.SalesPerson, c.CustomerID, soh.SubTotal, ROW_NUMBER() OVER (PARTITION BY SalesPerson ORDER BY SubTotal DESC) as TopCustomerRank
    FROM SalesLT.[SalesOrderHeader] soh
    JOIN SalesLT.Customer c on c.CustomerID = soh.CustomerID) ranked
WHERE TopCustomerRank <= 3

```

W ten sposób, byliśmy w stanie przefiltrować tylko tych klientów, którzy na podstawie 'rankingu' pod kątem wielkości zamówienia u konkretnego sprzedawcy, byli w top 3.

### `ROW_NUMBER` w paginacji rezultatów

W róźnego rodzaju aplikacjach, często potrzebujemy wyświetlić dane w sposób paginowany, po to, aby do klienta nie zwracać wszystkich danych na raz, co mogłoby spowodować przeciążenie serwera. W takich przypadkach przydatne jest wykorzystanie funkcji `ROW_NUMBER` w celu numerowania rekordów w wynikowym zbiorze danych - które następnie możemy wybrać z odpowiedniej 'strony' (np. 10 rekordów na stronę).

Przykładowo, aby zwrócić dane z tabeli `SalesLT.SalesOrderHeader` w sposób paginowany, możemy najpierw wykorzystać funkcję `ROW_NUMBER` w celu numerowania rekordów, a następnie wybrać odpowiednie rekordy z odpowiedniej strony.


```sql
    SELECT *, ROW_NUMBER() OVER(ORDER BY SalesOrderID) AS RowNumber
    FROM SalesLT.SalesOrderHeader
```

Mając dane oznaczone w ten sposób, możemy tą informacje wykorzystać, aby pobrać wyniki z drugiej strony


```sql

DECLARE @PageSize INT = 10;
DECLARE @PageNumber INT = 3;

SELECT *
FROM (
    SELECT 
        *,
        ROW_NUMBER() OVER(ORDER BY SubTotal) AS RowNumber
    FROM 
        SalesLT.SalesOrderHeader
) AS RowNumberedResults
WHERE 
    RowNumber BETWEEN (@PageNumber - 1) * @PageSize + 1 AND @PageNumber * @PageSize;


```


(10 rows affected)



Total execution time: 00:00:00.010





<table><tr><th>SalesOrderID</th><th>RevisionNumber</th><th>OrderDate</th><th>DueDate</th><th>ShipDate</th><th>Status</th><th>OnlineOrderFlag</th><th>SalesOrderNumber</th><th>PurchaseOrderNumber</th><th>AccountNumber</th><th>CustomerID</th><th>ShipToAddressID</th><th>BillToAddressID</th><th>ShipMethod</th><th>CreditCardApprovalCode</th><th>SubTotal</th><th>TaxAmt</th><th>Freight</th><th>TotalDue</th><th>Comment</th><th>rowguid</th><th>ModifiedDate</th><th>RowNumber</th></tr><tr><td>71832</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71832</td><td>PO10353140756</td><td>10-4020-000088</td><td>29922</td><td>639</td><td>639</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>35775,2113</td><td>2862,0169</td><td>894,3803</td><td>39531,6085</td><td>NULL</td><td>addb8620-432a-456e-8470-1bedd4bc3457</td><td>2008-06-08 00:00:00.000</td><td>21</td></tr><tr><td>71780</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71780</td><td>PO19604173239</td><td>10-4020-000340</td><td>30113</td><td>653</td><td>653</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>38418,6895</td><td>3073,4952</td><td>960,4672</td><td>42452,6519</td><td>NULL</td><td>a47665d2-7ac9-4cf3-8a8b-2a3883554284</td><td>2008-06-08 00:00:00.000</td><td>22</td></tr><tr><td>71782</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71782</td><td>PO19372114749</td><td>10-4020-000582</td><td>29485</td><td>1086</td><td>1086</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>39785,3304</td><td>3182,8264</td><td>994,6333</td><td>43962,7901</td><td>NULL</td><td>f1be45a5-5c57-4a50-93c6-5f8be44cb7cb</td><td>2008-06-08 00:00:00.000</td><td>23</td></tr><tr><td>71845</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71845</td><td>PO2697119362</td><td>10-4020-000187</td><td>29938</td><td>1020</td><td>1020</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>41622,0511</td><td>3329,7641</td><td>1040,5513</td><td>45992,3665</td><td>NULL</td><td>e68f7ee9-c581-45cd-9c4f-386aeda74d84</td><td>2008-06-08 00:00:00.000</td><td>24</td></tr><tr><td>71796</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71796</td><td>PO17052159664</td><td>10-4020-000420</td><td>29660</td><td>1058</td><td>1058</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>57634,6342</td><td>4610,7707</td><td>1440,8659</td><td>63686,2708</td><td>NULL</td><td>917ef5ba-f32d-4563-8588-66db0bcdc846</td><td>2008-06-08 00:00:00.000</td><td>25</td></tr><tr><td>71898</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71898</td><td>PO5713190501</td><td>10-4020-000052</td><td>29932</td><td>637</td><td>637</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>63980,9884</td><td>5118,4791</td><td>1599,5247</td><td>70698,9922</td><td>NULL</td><td>96f84d24-3355-43d2-b5a3-55e97c17e58c</td><td>2008-06-08 00:00:00.000</td><td>26</td></tr><tr><td>71902</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71902</td><td>PO5539125166</td><td>10-4020-000061</td><td>29929</td><td>999</td><td>999</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>74058,8078</td><td>5924,7046</td><td>1851,4702</td><td>81834,9826</td><td>NULL</td><td>137850d6-efdf-4de1-920f-5757a86cdaaf</td><td>2008-06-08 00:00:00.000</td><td>27</td></tr><tr><td>71797</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71797</td><td>PO16501134889</td><td>10-4020-000142</td><td>29796</td><td>642</td><td>642</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>78029,6898</td><td>6242,3752</td><td>1950,7422</td><td>86222,8072</td><td>NULL</td><td>bb3fee84-c8bf-4dd2-bcca-675ab6a11c38</td><td>2008-06-08 00:00:00.000</td><td>28</td></tr><tr><td>71783</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71783</td><td>PO19343113609</td><td>10-4020-000024</td><td>29957</td><td>992</td><td>992</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>83858,4261</td><td>6708,6741</td><td>2096,4607</td><td>92663,5609</td><td>NULL</td><td>7db2329e-6446-42a8-8915-9c8370b68ed8</td><td>2008-06-08 00:00:00.000</td><td>29</td></tr><tr><td>71938</td><td>2</td><td>2008-06-01 00:00:00.000</td><td>2008-06-13 00:00:00.000</td><td>2008-06-08 00:00:00.000</td><td>5</td><td>0</td><td>SO71938</td><td>PO8468183315</td><td>10-4020-000016</td><td>29546</td><td>635</td><td>635</td><td>CARGO TRANSPORT 5</td><td>NULL</td><td>88812,8625</td><td>7105,029</td><td>2220,3216</td><td>98138,2131</td><td>NULL</td><td>a36ee74a-cf0d-4024-a1ce-4eaffd1f85f0</td><td>2008-06-08 00:00:00.000</td><td>30</td></tr></table>




W powyższym przykładzie, zwracamy 10 rekordów z tabeli `SalesLT.SalesOrderHeader` zaczynając od 11 rekordu (strona 2, 10 rekordów na stronę).

Jeśli klient aplikacji, miałby możliwość sortowania wyników paginacji, to musimy pamiętać o tym, aby odpowiednio sortować dane wewnątrz `OVER(ORDER BY ..)`
