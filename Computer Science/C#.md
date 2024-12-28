# C# Reference Sheet

## Basic Syntax and Data Types

### Value Types
```csharp
// Numeric Types
byte    // 0 to 255
sbyte   // -128 to 127
short   // -32,768 to 32,767
ushort  // 0 to 65,535
int     // -2³¹ to 2³¹-1
uint    // 0 to 2³²-1
long    // -2⁶³ to 2⁶³-1
ulong   // 0 to 2⁶⁴-1
float   // ±1.5e-45 to ±3.4e38
double  // ±5.0e-324 to ±1.7e308
decimal // ±1.0e-28 to ±7.9e28

// Other Value Types
bool    // true or false
char    // Unicode 16-bit character
struct  // User-defined structure
enum    // Enumeration
```

### Reference Types
```csharp
// Basic Reference Types
string str = "Hello World";
object obj = new object();

// Arrays
int[] numbers = new int[5];
string[] names = { "John", "Jane" };

// Nullable Types
int? nullableInt = null;
bool? nullableBool = null;
```

## Control Structures

### Conditional Statements
```csharp
// if-else
if (condition)
{
    // code
}
else if (otherCondition)
{
    // code
}
else
{
    // code
}

// switch
switch (variable)
{
    case value1:
        // code
        break;
    case value2:
        // code
        break;
    default:
        // code
        break;
}

// Pattern matching switch
switch (obj)
{
    case int i:
        // handle integer
        break;
    case string s when s.Length > 0:
        // handle non-empty string
        break;
    case null:
        // handle null
        break;
}
```

### Loops
```csharp
// for loop
for (int i = 0; i < length; i++)
{
    // code
}

// foreach loop
foreach (var item in collection)
{
    // code
}

// while loop
while (condition)
{
    // code
}

// do-while loop
do
{
    // code
} while (condition);
```

## Object-Oriented Programming

### Classes and Objects
```csharp
public class Person
{
    // Fields
    private string name;
    private int age;

    // Properties
    public string Name
    {
        get { return name; }
        set { name = value; }
    }

    // Auto-implemented property
    public int Age { get; set; }

    // Constructors
    public Person()
    {
    }

    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }

    // Methods
    public virtual void Introduce()
    {
        Console.WriteLine($"Hi, I'm {name}");
    }
}
```

### Inheritance
```csharp
public class Employee : Person
{
    public string EmployeeId { get; set; }

    public Employee(string name, int age, string id)
        : base(name, age)
    {
        EmployeeId = id;
    }

    public override void Introduce()
    {
        base.Introduce();
        Console.WriteLine($"My employee ID is {EmployeeId}");
    }
}
```

### Interfaces
```csharp
public interface IPayable
{
    decimal CalculatePay();
    void ProcessPayment();
}

public interface IEmployee
{
    string EmployeeId { get; set; }
    void Work();
}

public class FullTimeEmployee : IPayable, IEmployee
{
    public decimal CalculatePay() => 0m;
    public void ProcessPayment() { }
    public string EmployeeId { get; set; }
    public void Work() { }
}
```

## Collections

### Lists
```csharp
// List<T>
List<string> names = new List<string>();
names.Add("John");
names.AddRange(new[] { "Jane", "Bob" });
names.Remove("John");
names.RemoveAt(0);

// Arrays
string[] arrayNames = new string[3];
string[] initialized = { "John", "Jane", "Bob" };
```

### Dictionaries
```csharp
Dictionary<string, int> ages = new Dictionary<string, int>();
ages.Add("John", 25);
ages["Jane"] = 30;

// Check existence
if (ages.ContainsKey("John"))
{
    int age = ages["John"];
}

// TryGetValue
if (ages.TryGetValue("John", out int johnAge))
{
    Console.WriteLine(johnAge);
}
```

### Sets
```csharp
HashSet<int> numbers = new HashSet<int>();
numbers.Add(1);
numbers.UnionWith(new[] { 2, 3, 4 });
numbers.IntersectWith(new[] { 2, 4 });
```

## LINQ (Language Integrated Query)

### Query Syntax
```csharp
var query = from item in collection
            where item.Property > value
            orderby item.Property
            select item;

var grouped = from item in collection
             group item by item.Property into g
             select new { Key = g.Key, Items = g };
```

### Method Syntax
```csharp
var query = collection
    .Where(item => item.Property > value)
    .OrderBy(item => item.Property)
    .Select(item => item);

var grouped = collection
    .GroupBy(item => item.Property)
    .Select(g => new { Key = g.Key, Items = g });
```

### Common LINQ Operations
```csharp
// Filtering
var filtered = collection.Where(x => x.Value > 10);

// Sorting
var sorted = collection.OrderBy(x => x.Value)
                      .ThenByDescending(x => x.Name);

// Projection
var projected = collection.Select(x => new { x.Name, x.Value });

// Aggregation
var sum = collection.Sum(x => x.Value);
var avg = collection.Average(x => x.Value);
var count = collection.Count(x => x.Value > 10);
```

## Asynchronous Programming

### Async/Await
```csharp
public async Task<string> GetDataAsync()
{
    try
    {
        using var client = new HttpClient();
        string result = await client.GetStringAsync(url);
        return result;
    }
    catch (Exception ex)
    {
        // Handle exception
        throw;
    }
}

// Usage
public async Task ProcessDataAsync()
{
    string data = await GetDataAsync();
    await SaveDataAsync(data);
}
```

### Task Parallel Library
```csharp
// Parallel.For
Parallel.For(0, 1000, i =>
{
    // Parallel operation
});

// Parallel.ForEach
Parallel.ForEach(collection, item =>
{
    // Parallel operation
});

// Task.WhenAll
Task[] tasks = new Task[10];
for (int i = 0; i < 10; i++)
{
    tasks[i] = DoWorkAsync();
}
await Task.WhenAll(tasks);
```

## Exception Handling

### Try-Catch Blocks
```csharp
try
{
    // Code that might throw exception
}
catch (SpecificException ex)
{
    // Handle specific exception
}
catch (Exception ex)
{
    // Handle any other exception
}
finally
{
    // Always executed
}
```

### Custom Exceptions
```csharp
public class CustomException : Exception
{
    public CustomException() { }
    
    public CustomException(string message)
        : base(message) { }
    
    public CustomException(string message, Exception inner)
        : base(message, inner) { }
}
```

## File Operations

### File I/O
```csharp
// Reading
string content = File.ReadAllText("file.txt");
string[] lines = File.ReadAllLines("file.txt");

// Writing
File.WriteAllText("file.txt", content);
File.WriteAllLines("file.txt", lines);

// Using StreamReader/StreamWriter
using (var reader = new StreamReader("file.txt"))
{
    while (!reader.EndOfStream)
    {
        string line = await reader.ReadLineAsync();
    }
}
```

### File Management
```csharp
// Check existence
if (File.Exists("file.txt"))
{
    // File operations
}

// Copy and Move
File.Copy("source.txt", "dest.txt");
File.Move("old.txt", "new.txt");

// Delete
File.Delete("file.txt");
```

## Delegates and Events

### Delegates
```csharp
public delegate void MessageHandler(string message);

// Action and Func delegates
Action<string> print = Console.WriteLine;
Func<int, int, int> add = (a, b) => a + b;

// Multicast delegate
MessageHandler handler = PrintToConsole;
handler += PrintToFile;
handler -= PrintToConsole;
```

### Events
```csharp
public class Publisher
{
    public event EventHandler<CustomEventArgs> CustomEvent;

    protected virtual void OnCustomEvent(CustomEventArgs e)
    {
        CustomEvent?.Invoke(this, e);
    }
}

// Usage
publisher.CustomEvent += (sender, e) =>
{
    // Handle event
};
```

## Generics

### Generic Classes
```csharp
public class GenericRepository<T> where T : class
{
    private List<T> items = new List<T>();

    public void Add(T item)
    {
        items.Add(item);
    }

    public IEnumerable<T> GetAll()
    {
        return items;
    }
}
```

### Generic Methods
```csharp
public T GetValue<T>(string key) where T : struct
{
    // Implementation
}

public void Swap<T>(ref T a, ref T b)
{
    T temp = a;
    a = b;
    b = temp;
}
```

## Extension Methods

### Definition and Usage
```csharp
public static class StringExtensions
{
    public static int WordCount(this string str)
    {
        return str.Split(new[] { ' ' },
            StringSplitOptions.RemoveEmptyEntries)
            .Length;
    }
}

// Usage
string text = "Hello World";
int wordCount = text.WordCount();
```

## Attributes and Reflection

### Custom Attributes
```csharp
[AttributeUsage(AttributeTargets.Class)]
public class CustomAttribute : Attribute
{
    public string Description { get; }

    public CustomAttribute(string description)
    {
        Description = description;
    }
}

// Usage
[Custom("Sample description")]
public class MyClass { }
```

### Reflection
```csharp
// Get type information
Type type = typeof(MyClass);
Type type2 = obj.GetType();

// Get methods
MethodInfo[] methods = type.GetMethods();

// Invoke method
object instance = Activator.CreateInstance(type);
MethodInfo method = type.GetMethod("MethodName");
method.Invoke(instance, parameters);
```
