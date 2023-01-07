# Enum

 Enum jest to typ wyliczeniowy, który pozwala na zdefiniowanie zbioru stałych wartości, które mogą zostać przypisane do zmiennej. 

 ## Pzykład

 ```
enum UserRole {
    Admin,
    Editor,
    Reader
}

 ```

 W tym przypadku został zdefiniowany enum o nazwie `UserRole`, który może przyjmować jedną z trzech wartości: `Admin`, `Editor` lub `Reader`. 
 
 > Wartości te są nazwane elementami enuma i są typu całkowitego, domyślnie są to wartości typu `int`, zaczynające się od 0. 
 
 Możemy również nadać im inne wartości całkowite:

 ```
enum UserRole {
    Admin = 1,
    Editor = 2,
    Reader = 3
}
 ```

 Enum jest stosowany gdy chcemy ograniczyć możliwe wartości jakiejś zmiennej do stałego zbioru wartości i nadać im konkretne nazwy. Dzięki jego zastosowaniu możemy zwiększyć czytelność i zrozumiałość naszegokodu.