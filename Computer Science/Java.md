# Comprehensive Java Cheat Sheet

## Basic Syntax and Data Types

### Data Types
```java
// Primitive Types
byte b = 127;                // 8-bit, -128 to 127
short s = 32767;             // 16-bit, -32,768 to 32,767
int i = 2147483647;          // 32-bit, -2^31 to 2^31-1
long l = 9223372036854775807L; // 64-bit, -2^63 to 2^63-1
float f = 3.14f;             // 32-bit floating point
double d = 3.14159265359;    // 64-bit floating point
boolean bool = true;         // true or false
char c = 'A';                // 16-bit Unicode character

// Reference Types
String str = "Hello World";  // String literal
Integer intObj = 42;         // Integer wrapper class
Double doubleObj = 3.14;     // Double wrapper class
```

### Type Conversion
```java
// Widening (Implicit)
int x = 10;
long y = x;      // int to long
float z = y;     // long to float

// Narrowing (Explicit)
double d = 3.14159;
int i = (int) d;  // double to int, loses decimal
```

## Control Flow

### Conditional Statements
```java
// if-else
if (condition) {
    // code block
} else if (another_condition) {
    // code block
} else {
    // code block
}

// switch (traditional)
switch (variable) {
    case value1:
        // code block
        break;
    case value2:
        // code block
        break;
    default:
        // code block
}

// switch (modern - Java 12+)
switch (variable) {
    case value1 -> // single line expression
    case value2 -> {
        // multi-line code block
    }
    default -> // default expression
}
```

### Loops
```java
// for loop
for (int i = 0; i < 10; i++) {
    // code block
}

// enhanced for loop (for-each)
for (String item : collection) {
    // code block
}

// while loop
while (condition) {
    // code block
}

// do-while loop
do {
    // code block
} while (condition);
```

## Object-Oriented Programming

### Class Definition
```java
public class Person {
    // Fields
    private String name;
    private int age;
    
    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Getters and Setters
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    // Method overriding
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}
```

### Inheritance
```java
public class Employee extends Person {
    private String employeeId;
    
    public Employee(String name, int age, String employeeId) {
        super(name, age);  // Call parent constructor
        this.employeeId = employeeId;
    }
}
```

### Interfaces
```java
public interface Payable {
    double calculatePay();  // Abstract method
    
    default void printPayDetails() {  // Default method
        System.out.println("Pay amount: " + calculatePay());
    }
}
```

### Abstract Classes
```java
public abstract class Vehicle {
    protected String brand;
    
    public abstract void start();  // Abstract method
    
    public void stop() {  // Concrete method
        System.out.println("Vehicle stopped");
    }
}
```

## Collections Framework

### List Interface
```java
// ArrayList
List<String> arrayList = new ArrayList<>();
arrayList.add("First");
arrayList.add("Second");
arrayList.get(0);  // Access by index

// LinkedList
List<String> linkedList = new LinkedList<>();
linkedList.add("First");
linkedList.addFirst("Zero");  // Specific to LinkedList

// Common operations
list.size();
list.isEmpty();
list.contains(element);
list.remove(element);
list.clear();
```

### Set Interface
```java
// HashSet
Set<String> hashSet = new HashSet<>();
hashSet.add("Apple");
hashSet.add("Apple");  // Duplicate not added

// TreeSet (sorted)
Set<String> treeSet = new TreeSet<>();
treeSet.add("Banana");
treeSet.add("Apple");  // Automatically sorted

// LinkedHashSet (maintains insertion order)
Set<String> linkedHashSet = new LinkedHashSet<>();
```

### Map Interface
```java
// HashMap
Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("One", 1);
hashMap.get("One");  // Returns 1

// TreeMap (sorted by keys)
Map<String, Integer> treeMap = new TreeMap<>();

// LinkedHashMap (maintains insertion order)
Map<String, Integer> linkedHashMap = new LinkedHashMap<>();

// Common operations
map.containsKey(key);
map.containsValue(value);
map.remove(key);
map.keySet();  // Set of keys
map.values();  // Collection of values
map.entrySet();  // Set of key-value pairs
```

## Exception Handling

### Try-Catch Blocks
```java
try {
    // Code that might throw an exception
    riskyOperation();
} catch (SpecificException e) {
    // Handle specific exception
    e.printStackTrace();
} catch (Exception e) {
    // Handle any other exception
} finally {
    // Always executed
    cleanup();
}
```

### Try-with-Resources
```java
try (FileInputStream fis = new FileInputStream("file.txt");
     BufferedReader br = new BufferedReader(new InputStreamReader(fis))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

## Lambda Expressions and Streams

### Lambda Expressions
```java
// Simple lambda
Runnable runnable = () -> System.out.println("Hello");

// Lambda with parameters
Comparator<String> comparator = (s1, s2) -> s1.compareTo(s2);

// Method reference
List<String> list = Arrays.asList("a", "b", "c");
list.forEach(System.out::println);
```

### Streams
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Filter and map
List<Integer> doubled = numbers.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .collect(Collectors.toList());

// Reduce
int sum = numbers.stream()
    .reduce(0, (a, b) -> a + b);

// Parallel stream
numbers.parallelStream()
    .forEach(System.out::println);
```

## File I/O

### File Operations
```java
// Reading a file
Path path = Paths.get("file.txt");
List<String> lines = Files.readAllLines(path);

// Writing to a file
Files.write(path, lines);

// File manipulation
Files.createDirectory(path);
Files.delete(path);
Files.copy(source, target);
Files.move(source, target);
```

### Buffered I/O
```java
// Writing
try (BufferedWriter writer = Files.newBufferedWriter(path)) {
    writer.write("Hello");
    writer.newLine();
}

// Reading
try (BufferedReader reader = Files.newBufferedReader(path)) {
    String line;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
}
```

## Multithreading

### Thread Creation
```java
// Extending Thread
class MyThread extends Thread {
    public void run() {
        // Thread code
    }
}

// Implementing Runnable
class MyRunnable implements Runnable {
    public void run() {
        // Thread code
    }
}

// Usage
Thread thread1 = new MyThread();
Thread thread2 = new Thread(new MyRunnable());
thread1.start();
thread2.start();
```

### Synchronization
```java
public class Counter {
    private int count = 0;
    
    // Method synchronization
    public synchronized void increment() {
        count++;
    }
    
    // Block synchronization
    public void decrement() {
        synchronized(this) {
            count--;
        }
    }
}
```

### Concurrent Collections
```java
// Thread-safe collections
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, Integer> concurrentMap = new ConcurrentHashMap<>();
Queue<String> blockingQueue = new LinkedBlockingQueue<>();
```

## Modern Java Features (Java 8+)

### Optional
```java
Optional<String> optional = Optional.of("value");
optional.isPresent();  // true
optional.get();        // "value"
optional.orElse("default");
optional.ifPresent(System.out::println);
```

### CompletableFuture
```java
CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> "Hello")
    .thenApply(s -> s + " World")
    .thenAccept(System.out::println);
```

### Records (Java 14+)
```java
public record Person(String name, int age) {
    // Compact way to create immutable data classes
}
```

### Pattern Matching (Java 16+)
```java
Object obj = "Hello";
if (obj instanceof String s) {
    // Can use s directly
    System.out.println(s.length());
}
```

## Testing with JUnit

### Basic Test Structure
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    @Test
    void testAddition() {
        Calculator calc = new Calculator();
        assertEquals(4, calc.add(2, 2));
    }
    
    @Test
    void testDivision() {
        Calculator calc = new Calculator();
        assertThrows(ArithmeticException.class,
            () -> calc.divide(1, 0));
    }
}
```
