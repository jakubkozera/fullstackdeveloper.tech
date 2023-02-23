# Metoda GroupJoin 

Metoda `GroupJoin` w LINQ służy do łączenia dwóch kolekcji na podstawie klucza, ale w odróżnieniu od metody `Join`, zachowuje elementy z pierwszej kolekcji, które nie mają dopasowania w drugiej kolekcji. Metoda `GroupJoin` tworzy grupy elementów z pierwszej kolekcji oraz odpowiadających im elementów z drugiej kolekcji w postaci klucz-wartość, gdzie kluczem jest wartość z pierwszej kolekcji, a wartością jest kolekcja elementów z drugiej kolekcji. Wynikiem działania metody `GroupJoin` jest sekwencja wynikowa z elementami, które zawierają klucz z pierwszej kolekcji i kolekcję dopasowanych elementów z drugiej kolekcji lub pustą kolekcję, jeśli brak dopasowania.

Metoda `GroupJoin` przyjmuje cztery argumenty:

- drugą sekwencję,
- klucz z pierwszej kolekcji,
- klucz z drugiej kolekcji,
- funkcję wyjściową, która tworzy obiekt wynikowy z grupy kluczy i wartości

Metoda `GroupJoin` jest przydatna, gdy chcemy połączyć dwie kolekcje i utworzyć grupy na podstawie kluczy z pierwszej kolekcji, a następnie dla każdej grupy dodać kolekcję elementów z drugiej kolekcji, które pasują do klucza.

## Przykład

```
class Department
{
    public int Id { get; set; }
    public string Name { get; set; }
}

class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int DepartmentId { get; set; }
}

// Create some sample data
var departments = new List<Department>
{
    new Department { Id = 1, Name = "Sales" },
    new Department { Id = 2, Name = "Marketing" },
    new Department { Id = 3, Name = "Engineering" }
};

var employees = new List<Employee>
{
    new Employee { Id = 1, Name = "John", DepartmentId = 1 },
    new Employee { Id = 2, Name = "Mary", DepartmentId = 1 },
    new Employee { Id = 3, Name = "Bob", DepartmentId = 2 },
    new Employee { Id = 4, Name = "Alice", DepartmentId = 2 },
    new Employee { Id = 5, Name = "Jane", DepartmentId = 3 }
};

// Use GroupJoin to create a list of departments, each with a list of employees
var result = departments.GroupJoin(
    employees,
    d => d.Id,
    e => e.DepartmentId,
    (department, employees) => new
    {
        Department = department,
        Employees = employees.ToList()
    }
);

// Print out the result
foreach (var department in result)
{
    Console.WriteLine($"Department: {department.Department.Name}");
    Console.WriteLine("Employees:");
    foreach (var employee in department.Employees)
    {
        Console.WriteLine($"- {employee.Name}");
    }
    Console.WriteLine();
}
```

Powyższy kod używa metody `GroupJoin` do połączenia list departametów i pracowników na właściwościach `Id` i `DepartmentId`. Wynikiem tego jest lista obiektów typu `Department` oraz listę obiektów `Employee`, które należą do tego działu. Na końcu kod drukuje działy i ich powiązanych pracowników.