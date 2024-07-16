# Funkcje `LEAD` i `LAG` 



Funkcje okna `LEAD` i `LAG` służą do pobierania wartości z wierszy znajdujących się przed lub po bieżącym wierszu w oknie definiowanym przez klauzulę OVER. Obie funkcje wymagają określenia wyrażenia, które określa wartość, która ma zostać pobrana, oraz przesunięcia, które określa odległość wiersza od bieżącego wiersza.



Przykładowo, mająć informacje o wypożyczeniech egzemplarzy przez danego użytkownika, możemy bardzo łatwo uzyskać informacje o poprzednim i następnym wypożyczeniu danego użytkownika. 


 


```sql
SELECT UserId, 
    LoanDate, 
    b.Title
FROM [dbo].[Loans] l
JOIN Copies c on l.CopyId = c.CopyId
JOIN Books b on b.BookId = c.BookId
WHERE UserId = 228
ORDER BY LoanDate
```

Do powyższego zapytania, wystarczy dodać wywołanie funkcji `LEAD`, lub `LAG` w zależności od tego, czy chcemy uzyskać wartość z kolejnego, czy poprzedniego wiersza.






```sql
SELECT UserId, LoanDate, b.Title,
    LEAD(LoanDate) OVER (ORDER BY LoanDate) NextLoanDate, 
    LAG(LoanDate) OVER (ORDER BY LoanDate) PreviousLoanDate
FROM [dbo].[Loans] l
JOIN Copies c on l.CopyId = c.CopyId
JOIN Books b on b.BookId = c.BookId
WHERE UserId = 228
```

Wartość, która chcemy pobrać z następnego lub poprzedniego wiersza, jest dowolna w danym oknie wierszy. Przykładowo, poza samą datą możemy jeszcze wybrac tytuł książki wypożyczonej następnym/poprzednim razem.






```sql
SELECT UserId, LoanDate, b.Title,
    LEAD(LoanDate) OVER (ORDER BY LoanDate) NextLoanDate, 
    LEAD(b.Title) OVER (ORDER BY LoanDate) NextLoanTitle, 
    LAG(LoanDate) OVER (ORDER BY LoanDate) PreviousLoanDate,
    LAG(b.Title) OVER (ORDER BY LoanDate) PreviousLoanTitle
FROM [dbo].[Loans] l
JOIN Copies c on l.CopyId = c.CopyId
JOIN Books b on b.BookId = c.BookId
WHERE UserId = 228
```

Co więcej, zarówno `LEAD` jak i `LAG`, mogą przyjąc drugi parametr, który określa o ile wierszy ma być przesunięty wynik. Dzięki temu można uzyskać wynik z dowolnego wiersza w ramce. Domyślnie jest to wartość 1, ale można to zmienić na dowolną liczbę.





```sql
SELECT UserId, LoanDate, b.Title,
    LEAD(LoanDate, 2) OVER (ORDER BY LoanDate) NextLoanDate, 
    LEAD(b.Title, 2) OVER (ORDER BY LoanDate) NextLoanTitle, 
    LAG(LoanDate, 2) OVER (ORDER BY LoanDate) PreviousLoanDate,
    LAG(b.Title, 2) OVER (ORDER BY LoanDate) PreviousLoanTitle
FROM [dbo].[Loans] l
JOIN Copies c on l.CopyId = c.CopyId
JOIN Books b on b.BookId = c.BookId
WHERE UserId = 228
```







